---
title: Multi-scale Guided Mask Refinement for RGB-D Perception
date: 2018-08-25
comments: true
tags: ["Computer Vision", "Object Segmentation", "Depth Completion"]
categories: ["Robotics"]
---
![The pipeline of the proposed multi-scale guided mask refinement.](/image/ms_system.gif)

 Pixel-level object segmentation is highly desired in robot perception systems due to its importance for many vision applications. Existing approaches for pixel-level segmentation are mainly based on deep neutral networks (DNN), which can achieve high accuracy in generating the semantic masks. However, they still have difficulties in being applied to robot vision due to the large requirements of storage and computing resources. Motivated by the recent works on utilizing depth cues and edge-preserving components for more accurate segmentations.

<!--more-->
![Visual comparisons on a RGB-D frame in Cespatx_ds.](/image/ms_result.png)
 In this paper, we propose to imitate the DNN architecture using light-weight components and design a multi-scale guided mask refinement method to enhance the coarse segmentations to fine-scale ones. Taking foreground segmentation and temporal object segmentation as two representative applications, we quantitatively evaluate the proposed method on benchmark datasets. It is demonstrated in the experimental results that our method can achieve not only significant accuracy improve- ments compared to other alternatives, but also the superior edge-preserving capability with limited storing and computing resources. We believe that our method is feasible for real-time pixel-level perception on robotic systems due to its scalable implementation and small resource requirements.

 [This project have be published on SPL.](https://ieeexplore.ieee.org/abstract/document/8573890)