---
layout: post
title: "Simple Project"
categories:
  - Machine Learning
# tags:
#   - Machine Learning
excerpt: How to add Project in bog
comments: false
category: 
  - Projects
---

<!-- You just need to add 

~~~yaml
category: 
  - Projects
~~~ -->

This section is just my notepad. I post stuff of which I might do in future

# **TODO**

## *Learning Stuff*
  1. Basic DL model using [CIFAR](https://www.cs.toronto.edu/~kriz/cifar.html) and Pytorch
     1. Download CIFAR using `wget https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz`
  2. Re-implement it using Pytorch Lightning
  3. Hyper optimization tuning using RayTune
     1. Training parameters (like learning rate) tuning
     2. Model parameters (No Of parameters in each layer & No of Layers) tuning
  4. Model Interpretability using [Captum](https://captum.ai/)
     1. Explore model input interpretability for images

## *OpenMMLab*
  1. Test MMDetection
  2. Test MMPose
  3. Try to combine both detection and pose

### MMDetection Logs
- Got Error - *KeyError: 'Cascade Mask R-CNN'*
  - Refer [Issue](https://github.com/open-mmlab/mmdetection/issues/8122) and [Ans] (https://github.com/open-mmlab/mmdetection/issues/8122#issuecomment-1158658158)