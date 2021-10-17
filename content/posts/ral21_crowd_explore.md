---
title: A Hierarchical Approach for Mobile RobotExploration in Pedestrian Crowd
date: 2021-10-08
tags: ["Robotics", "Learning","Exploration","Navigation"]
categories: ["Robotics"]
---

![](/image/crowd_explore_system.png)

## Overview
In this work, a hierarchical approach is proposed for both effective exploration and collision-free navigation in crowded environments. The central idea of our approach is to combine local and global information to ensure the safety and efficiency of the exploration planner. Besides, our planning method utilizes a reinforcement learning (RL)-based obstacle avoidance algorithm that allows the robot to safely follow the exploration planner's path through the pedestrian crowd.
:The proposed system is thoroughly evaluated in simulation environments, and the results show that it outperforms existing methods in terms of not only the exploration efficiency but also the localization and mapping accuracy.

## Method 
![](/image/crowd_explore_pipeline.png)

A hierarchical autonomous exploration planner is designed to determine an exploration tour with Travel-Salesman-Problem (TSP)-based planner on the global map and to refine the exploration path with the Next-Best-View (NBV)-based planner on local maps and, respectively.
Based on the optimized hierarchical exploration strategy, an RL-based collision avoidance algorithm is embedded to ensure the robot executing the navigation task safely and efficiently through the crowd. Our collision avoidance controller also implicitly models the crowd flow distribution locally around the robot to minimize the inter-interruption between the robot and the crowd, which not only improves the exploration efficiency but also increases the success rate and accuracy in both mapping and localization. 
The proposed system is thoroughly evaluated in an extensive simulation experiment, where the impact of different planning and navigation methods for navigation in crowds is investigated.

## Result
Experimental simulated results in a variety of different environments demonstrate the advantages of the hierarchical exploration strategy.
In addition, the RL-based navigation module is shown to significantly improve the localization and mapping accuracy of SLAM when exploring autonomously in a crowd.
Overall, the proposed hierarchical TSP-based autonomous exploration system outperforms the baseline approach in terms of operational efficiency and SLAM accuracy, and is able to finish the exploration tasks reliably in challenging crowded environments.