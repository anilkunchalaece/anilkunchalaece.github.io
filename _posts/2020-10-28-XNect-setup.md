---
layout: post
title: "Xnect - Installtion and Running an Example"
categories:
  - Machine Learning
tags:
  - Machine Learning
---

In this Post I will show how to install XNect and Run the demo provided in example
### installing openCV and contrib libs
Ref - [link](https://chunml.github.io/ChunML.github.io/project/Installing-Caffe-Ubuntu/)

download following  
opencv3.4.11 and opencv_contrib 3.4.11   
- opencv 3.4.11 

	1. `wget -c  -O opencv-3.4.11.tar.gz https://github.com/opencv/opencv/archive/3.4.11.tar.gz`        
	2. `tar xvzf opencv-3.4.11`   



- opencv contrib 3.4.11  
```
wget -c -O opencv_contrib-3.4.11 https://github.com/opencv/opencv_contrib/archive/3.4.11.tar.gz  
tar xvzf opencv_contrib-3.4.11  
```

- make opecv
```
cd opencv-3.4.11
mkdir build
cd build
```
Then run following command ( Check Xnect readme for flags)

```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=/home/anil/Documents/xNect/opencv_contrib-3.4.11/modules -D BUILD_EXAMPLES=ON -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D BUILD_TIFF=ON ..
```

Then
```
make -j$(nproc)
sudo make install
sudo ldconfig
```

Once installtion completed, check it

```
python
>>> import cv2
>>> cv2.__version__
'3.4.11'
```

# installing protobuf  
[ref](https://gist.github.com/diegopacheco/cd795d36e6ebcd2537cd18174865887b)

```
sudo apt-get install autoconf automake libtool curl make g++ unzip -y
git clone https://github.com/google/protobuf.git
cd protobuf
git submodule update --init --recursive
./autogen.sh
./configure CFLAGS="-fPIC" CXXFLAGS="-fPIC"  (Why ? I dont know - Check XNect Readme)
sudo make install
sudo ldconfig
```

# installing boost 1.58.0
[ref] (https://www.boost.org/doc/libs/1_66_0/more/getting_started/unix-variants.html)
- download  boost from [here](https://www.boost.org/users/history/)
```
tar xvzf boost-1.58
/bootstrap.sh --prefix=path/to/installation/prefix
./b2 install
```
- Add PREFIX/bin to your PATH environment variable.

# installing caffe
- BVLC GitHub repository and grab the latest version of Caffe
```
git clone https://github.com/BVLC/caffe.git
cd caffe
```

- copy make file 
```
cp Makefile.config.example Makefile.config

```

- and do the following edits

```
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
```

and based on the cuda version uncomment architectures

```
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
```

- compile caffe

Specify different compiler for gcc  
[ref] (https://stackoverflow.com/questions/17275348/how-to-specify-new-gcc-path-for-cmake)

```
export CC=/usr/local/bin/gcc
export CXX=/usr/local/bin/g++
cmake /path/to/your/project
make
```

```
 cmake -DProtobuf_LIBRARY_DEBUG=/home/anil/Documents/xNect/protobuf/src/.libs/libprotobuf.so -DProtobuf_PROTOC_EXECUTABLE=/home/anil/Documents/xNect/protobuf/src/.libs/protoc -DProtobuf_LIBRARY_RELEASE=/home/anil/Documents/xNect/protobuf/src/.libs/libprotobuf.a  -DProtobuf_LITE_LIBRARY_RELEASE=/home/anil/Documents/xNect/protobuf/src/.libs/libprotobuf-lite.a -DBOOST_INCLUDEDIR=/usr/include/boost/  -DBOOST_LIBRARYDIR=/home/anil/Documents/xNect/boost/lib -DProtobuf_INCLUDE_DIR=/home/anil/Documents/xNect/protobuf/src/ -DProtobuf_PROTOC_LIBRARY_RELEASE=/home/anil/Documents/xNect/protobuf/src/.libs/libprotoc.so ..
```

```
make all -j$(nproc) && make test -j$(nproc) && make runtest -j$(nproc) && make pycaffe -j$(nproc)
```

- Add follwing to .bashrc
```
export PYTHONPATH=/home/anil/Documents/xNect/caffe/python:$PYTHONPATH
```

- check caffe
```
python
>>> import caffe
```

I get the following error when I run that
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/anil/Documents/xNect/caffe/python/caffe/__init__.py", line 1, in <module>
    from .pycaffe import Net, SGDSolver, NesterovSolver, AdaGradSolver, RMSPropSolver, AdaDeltaSolver, AdamSolver, NCCL, Timer
  File "/home/anil/Documents/xNect/caffe/python/caffe/pycaffe.py", line 15, in <module>
    import caffe.io
  File "/home/anil/Documents/xNect/caffe/python/caffe/io.py", line 2, in <module>
    import skimage.io
ImportError: No module named skimage.io

```
looks like it is redirecting to caffe folder, so now I need to install skimage

```
pip install scikit-image
```

# build project
```
cmake -DOpenCV_DIR=/usr/share/opencv  -DCaffe_DIR=/home/anil/Documents/xNect/caffe/build ..
cd ../bin/Release
./XNECT
```
It will run the example
