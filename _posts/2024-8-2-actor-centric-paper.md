---
layout: post
title: "Actor-Centric Spatio-Temporal Feature Extraction for Action Recognition"
categories:
  - PhD
  - Publication
# tags:
#   - Machine Learning
excerpt: Actor-Centric Spatio-Temporal Feature Extraction for Action Recognition
comments: false
category: 
  - Projects
---

## Overview
**Title:** Actor-Centric Spatio-Temporal Feature Extraction for Action Recognition

**Published in:** 2023 International Conference on Computer Vision and Image Processing (CVIP 2023)

![image]({{ site.url }}{{ site.baseurl }}/assets/images/cvip_2023/actor_centric.png)
**Proposed Actor-Centric Tubelet Action Recognition Network Compared to Existing Frame-based Action Recognition Networks**


## Abstract
Action understanding involves the recognition and detection of specific actions within videos. This crucial task in computer vision gained significant attention due to its multitude of applications across various domains. The current action detection models, inspired by 2D object detection methods, employ two-stage architectures. The first stage is to extract actor-centric video sub-clips, i.e. tubelets of individuals, and the second stage is to classify these tubelets using action recognition networks. The majority of these recognition models utilize a frame-level pre-trained 3D Convolutional Neural Networks (3D CNN) to extract spatio-temporal features of a given tubelet. This, however, results in suboptimal spatio-temporal feature representation for action recognition, primarily because the actor typically occupies a relatively small area in the frame.

This work proposes the use of actor-centric tubelets instead of frames to learn spatio-temporal feature representation for action recognition. We present an empirical study of the actor-centric tubelet and frame-level action recognition models and propose a baseline for actor-centric action recognition. We evaluated the proposed method on the state-of-the-art C3D, I3D, and SlowFast 3D CNN architectures using the NTURGBD dataset. Our results demonstrate that the actor-centric feature extractor consistently outperforms the frame-level and large pre-trained fine-tuned models. The source code for the tubelet generation is available at <a href="https://github.com/anilkunchalaece/ntu_tubelet_parser"> https://github.com/anilkunchalaece/ntu_tubelet_parser.</a>

## Key Contributions
- We conducted an extensive comparative study of frame-based and actor-centric tubelet-based feature extraction for action classification.
- We propose an actor-centric tubelet-based backbone that enhances spatio-temporal feature extraction for action classification and detection compared to the existing frame-level models.

## Qualitative Results
![image]({{ site.url }}{{ site.baseurl }}/assets/images/cvip_2023/results.png)

## Publication Link and Code
- <a href="https://arrow.tudublin.ie/cgi/viewcontent.cgi?article=1454&context=scschcomcon" target="_blank">Read the full paper</a>
- <a href="https://drive.google.com/file/d/1MENLg1BWRT_PEb_m8GerouIeSCwkI3me/view?usp=drive_link" target="_blank">CVIP 2023 Presentation Slides</a>
- <a href="https://github.com/anilkunchalaece/mmaction2-af_new" target="_blank">Source Code</a>