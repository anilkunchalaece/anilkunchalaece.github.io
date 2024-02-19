---
layout: post
title: "SMPL-based 3D Pedestrian Pose Prediction "
categories:
  - PhD
  - Publication
# tags:
#   - Machine Learning
excerpt: Adversarial SMPL based 3D Pedestrian Pose Prediction
comments: false
category: 
  - Projects
---

## Overview
**Title:** SMPL-Based 3D Pedestrian Pose Prediction

**Published in:** 2021 16th IEEE International Conference on Automatic Face and Gesture Recognition (FG 2021)

![image]({{ site.url }}{{ site.baseurl }}/assets/images/fg2021/ADV_SMPL_AWARE.png)
**Adversarial SMPL-based Recurrent Neural Network Architecture**


## Abstract
In 3D pedestrian pose prediction, joint-rotation-based pose representation is extensively used due to the unconstrained degree of freedom for each joint and its ability to regress the 3D statistical wireframe. However, all the existing joint-rotation-based pose prediction approaches ignore the centrality of the distinct pose parameter components and are consequently prone to suffer from error accumulation along the kinematic chain, which results in unnatural human poses. In joint-rotationbased pose prediction, Skinned Multi-Person Linear (SMPL) parameters are widely used to represent pedestrian pose.

In this work, a novel SMPL-based pose prediction network is proposed to address the centrality of each SMPL component by distributing the network weights among them. Furthermore, to constrain the network to generate only plausible human poses, an adversarial training approach is employed. The effectiveness of the proposed network is evaluated using the PedX and BEHAVE datasets. The proposed approach significantly outperforms state-of-the-art methods with improved prediction accuracy and generates plausible human pose predictions.

## Key Contributions
- We designed a multi-layer perception generative adversarial network to penalize the network for unnatural poses while allowing natural one.
- The SMPL-based architecture is proposed to address the centrality of global rotation and translation parameters with respect to the pose parameters

## Qualitative Results
![image]({{ site.url }}{{ site.baseurl }}/assets/images/fg2021/ADV_SMPL_AWARE_Results.png)

## Publication Link and Code
- <a href="https://arrow.tudublin.ie/cgi/viewcontent.cgi?article=1374&context=scschcomcon" target="_blank">Read the full paper</a>
- <a href="https://youtu.be/OeOTEcbYsrI" target="_blank">FG 2021 Presentation Video</a>
- <a href="https://drive.google.com/file/d/1yl6l8_vDKse4vCQ_LtTk6dgMY3LTmAqw/view?usp=sharing" target="_blank">FG 2021 Presentation Slides</a>
- <a href="https://drive.google.com/file/d/1K3FvySkvguGt_yD-mFijZyALVjKBzN14/view?usp=sharing" target="_blank">FG 2021 Poster</a>
- <a href="https://github.com/anilkunchalaece/ADV-SA-LSTM" target="_blank">Source Code</a>