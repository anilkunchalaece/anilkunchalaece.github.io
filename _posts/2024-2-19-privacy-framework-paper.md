---
layout: post
title: "Towards A Framework for Privacy-Preserving Pedestrian Analysis"
categories:
  - PhD
  - Publication
# tags:
#   - Machine Learning
excerpt: Towards A Framework for Privacy-Preserving Pedestrian Analysis
comments: false
category: 
  - Projects
---

## Overview
**Title:** Towards A Framework for Privacy-Preserving Pedestrian Analysis

**Published in:** 2023 IEEE CVF Winter Conference on Applications of Computer Vision (WACV 2023)

![image]({{ site.url }}{{ site.baseurl }}/assets/images/wacv2023/wacv2023-results.png)
**Qualitative results for the proposed and baseline methods**


## Abstract
The design of pedestrian-friendly infrastructures plays a crucial role in creating sustainable transportation in urban environments. Analyzing pedestrian behaviour in response to existing infrastructure is pivotal to planning, maintaining, and creating more pedestrian-friendly facilities. Many approaches have been proposed to extract such behaviour by applying deep learning models to video data. Video data, however, includes an broad spectrum of privacy-sensitive information about individuals, such as their location at a given time or who they are with. Most of the existing mod-
els use privacy-invasive methodologies to track, detect, and analyse individual or group pedestrian behaviour patterns.

As a step towards privacy-preserving pedestrian analysis, this paper introduces a framework to anonymize all pedestrians before analyzing their behaviors. The proposed framework leverages recent developments in 3D wireframe reconstruction and digital in-painting to represent pedestrians with quantitative wireframes by removing their images while preserving pose, shape, and background scene context. To evaluate the proposed framework, a generic metric is introduced for each of privacy and utility. Experimental evaluation on widely-used datasets shows that the proposed framework outperforms traditional and state-of-the-art image filtering approaches by generating best privacy utility
trade-off.

## Key Contributions
- A novel end-to-end framework is introduced to generate a privacy-enhanced version of a given video or
image sequence.
- Both a generic utility and statistical similarity-based privacy metrics are proposed to evaluate the privacy utility trade-off.

## Overview of the proposed framework
![image]({{ site.url }}{{ site.baseurl }}/assets/images/wacv2023/wacv2023-framework.png)

## Privacy-Utility Trade-off
![image]({{ site.url }}{{ site.baseurl }}/assets/images/wacv2023/wacv2023-results-plots.png)

## Publication Link and Code
- <a href="https://arrow.tudublin.ie/cgi/viewcontent.cgi?article=1411&context=scschcomcon" target="_blank">Read the full paper</a>
- <a href="https://www.youtube.com/watch?v=Ke5vPS9fwUA" target="_blank">WACV 2023 Presentation Video</a>
- <a href="https://drive.google.com/file/d/1ZROKNr6W2BqqKL1qUM2tOAF-ckC4zrZi/view?usp=sharing" target="_blank">WACV 2023 Presentation Slides</a>
- <a href="https://drive.google.com/file/d/1DIcMZizTPD4LhC8Ir7pYvc7vNcjhyS4v/view?usp=sharing" target="_blank">WACV 2023 Poster</a>
- <a href="https://github.com/anilkunchalaece/privacyFramework" target="_blank">Source Code</a>