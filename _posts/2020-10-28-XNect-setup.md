---
layout: post
title: "Xnect - Installation and running demo"
categories:
  - Machine Learning
tags:
  - Machine Learning
excerpt: In this post I will explain how to setup XNect and run the demo provided in the example
comments: false

---

In this Post I will show how to install [XNect](https://gvv.mpi-inf.mpg.de/projects/XNect/) and Run the demo in C/C++ Library provided by xNect Team.   

In summary you need to install following dependencies 
1. OpenCV 3.4.11 - *recommended , dont use Opencv 4*
2. Protobuf
3. Boost 1.58.0
4. CUDA - *8 or 9 recommened but I tested with 10*
5. Caffe - *need to make few modifications before installation*  

#### Machine Configuration
I tested using machine with following configuration

~~~
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=19.10
DISTRIB_CODENAME=eoan
x86_64
Kernal - 5.3.0-64-generic 
~~~

![image]({{ site.url }}{{ site.baseurl }}/assets/images/nvidia_info.jpg)

#### 1. installing openCV and contrib libs
~~~shell
  wget -c  -O opencv-3.4.11.tar.gz https://github.com/opencv/opencv/archive/3.4.11.tar.gz       
  tar xvzf opencv-3.4.11.tar.gz

  wget -c -O opencv_contrib-3.4.11 https://github.com/opencv/opencv_contrib/archive/3.4.11.tar.gz  
  tar xvzf opencv_contrib-3.4.11.tar.gz  

  rm opencv-3.4.11.tar.gz opencv_contrib-3.4.11.tar.gz

  cd opencv-3.4.11
  mkdir build
  cd build

  # Run cmake - Check XNect readme.md for flags
  cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=/home/anil/Documents/xNect/opencv_contrib-3.4.11/modules -D BUILD_EXAMPLES=ON -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D BUILD_TIFF=ON ..

  make -j$(nproc)
  sudo make install
  sudo ldconfig
~~~

Once installtion completed, check it
~~~shell
python
>>> import cv2
>>> cv2.__version__
'3.4.11'
~~~

#### 2. installing protobuf  
~~~shell
sudo apt-get install autoconf automake libtool curl make g++ unzip -y
git clone https://github.com/google/protobuf.git
cd protobuf
git submodule update --init --recursive
./autogen.sh
./configure CFLAGS="-fPIC" CXXFLAGS="-fPIC"  (Why ? I dont know - Check XNect Readme)
sudo make install
sudo ldconfig
~~~

#### 3. installing boost 1.58.0
download  boost from [here](https://www.boost.org/users/history/)
~~~shell
tar xvzf boost-1.58.tar
cd boost-1.58/tools/build
/bootstrap.sh --prefix=path/to/installation/prefix
./b2 install
~~~
- Add PREFIX/bin to your PATH environment variable.

#### 4. installing caffe
BVLC GitHub repository and grab the latest version of Caffe
~~~shell
git clone https://github.com/BVLC/caffe.git
cd caffe
#copy make file 
cp Makefile.config.example Makefile.config
~~~

and make the following edits to *Makefile.config* - these are used to specify that we need to install caffe with GPU and CUDA support

~~~config
# cuDNN acceleration switch (uncomment to build with cuDNN).
USE_CUDNN := 1

# Uncomment if you're using OpenCV 3
OPENCV_VERSION := 3

# We need to be able to find Python.h and numpy/arrayobject.h.
PYTHON_INCLUDE := /usr/include/python2.7 \
        /usr/local/lib/python2.7/dist-packages/numpy/core/include

# Uncomment to support layers written in Python (will link against    Python libs)
WITH_PYTHON_LAYER := 1

# Whatever else you find you need goes here.
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/
~~~

and based on the cuda version you are using uncomment architectures

~~~config
# CUDA architecture setting: going with all of them.
# For CUDA < 6.0, comment the *_50 through *_61 lines for compatibility.
# For CUDA < 8.0, comment the *_60 and *_61 lines for compatibility.
# For CUDA >= 9.0, comment the *_20 and *_21 lines for compatibility.
CUDA_ARCH := 
		# -gencode arch=compute_20,code=sm_20 \
		# -gencode arch=compute_20,code=sm_21 \
		-gencode arch=compute_30,code=sm_30 \
		-gencode arch=compute_35,code=sm_35 \
		-gencode arch=compute_50,code=sm_50 \
		-gencode arch=compute_52,code=sm_52 \
		-gencode arch=compute_60,code=sm_60 \
		-gencode arch=compute_61,code=sm_61 \
		-gencode arch=compute_61,code=compute_61
~~~
##### 4.1 Removing clip layer and adding other necessary files
I'm just copy + pasting steps/info in XNect readme.md document. Please refer document for more info (I'm not sure whether I can add that Info here are not due to licencing issues)
1. Copy folders from XNect source to caffe (Include and src)
2. Make necessary changes to *caffe.proto* ( Need to add extra layers )
3. Add new layer description
4. Remove cliplayer from caffe - incluing .hpp , .cpp files

##### 4.2 compile caffe
API comes with gcc-6.4 support , I'm unable to compile this with current gcc in my system i.e gcc-9, so In order to specify different compiler for gcc  
[ref](https://stackoverflow.com/questions/17275348/how-to-specify-new-gcc-path-for-cmake)

~~~shell
export CC=/usr/local/bin/gcc-6.4
export CXX=/usr/local/bin/g++-6.4
#cmake /path/to/your/project
#make
~~~
Run cmake and make for caffe
~~~shell
cmake -DProtobuf_LIBRARY_DEBUG=/home/anil/Documents/xNect/protobuf/src/.libs/libprotobuf.so -DProtobuf_PROTOC_EXECUTABLE=/home/anil/Documents/xNect/protobuf/src/.libs/protoc -DProtobuf_LIBRARY_RELEASE=/home/anil/Documents/xNect/protobuf/src/.libs/libprotobuf.a  -DProtobuf_LITE_LIBRARY_RELEASE=/home/anil/Documents/xNect/protobuf/src/.libs/libprotobuf-lite.a -DBOOST_INCLUDEDIR=/usr/include/boost/  -DBOOST_LIBRARYDIR=/home/anil/Documents/xNect/boost/lib -DProtobuf_INCLUDE_DIR=/home/anil/Documents/xNect/protobuf/src/ -DProtobuf_PROTOC_LIBRARY_RELEASE=/home/anil/Documents/xNect/protobuf/src/.libs/libprotoc.so ..

make all -j$(nproc) && make test -j$(nproc) && make runtest -j$(nproc) && make pycaffe -j$(nproc)
~~~

Once done, Add follwing to .bashrc
```
export PYTHONPATH=/home/anil/Documents/xNect/caffe/python:$PYTHONPATH
```

check caffe
~~~shell
python
>>> import caffe
~~~

##### build project and run demo
~~~shell
cmake -DOpenCV_DIR=/usr/share/opencv  -DCaffe_DIR=/home/anil/Documents/xNect/caffe/build ..
make -j$(nproc)
cd ../bin/Release
./XNECT
~~~

##### References
1. I found a nice article about [installing caffe in ubuntu](https://chunml.github.io/ChunML.github.io/project/Installing-Caffe-Ubuntu/).
2. [Protobuf installation](https://gist.github.com/diegopacheco/cd795d36e6ebcd2537cd18174865887b)
3. [Boost 1.58 Installation](https://www.boost.org/doc/libs/1_66_0/more/getting_started/unix-variants.html)
