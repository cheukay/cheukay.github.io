---
title: Vanilla Policy Gradient 笔记
date: 2019-10-10 16:03:50
mathjax: true
tags: [Reinforcement Learning, Notes]
categories: Robotics
---

> 本文基于[OpenAI Spinning Up](https://spinningup.openai.com/en/latest/index.html#) 以及 Sutton 《Reinforcement Learning: An Introduction》，中文术语以后者中文版（俞凯 译）为准。

## 背景
策略梯度背后的关键思想是提高导致高回报的动作的概率，
并降低导致低回报的操作的概率，直到获得最佳策略。

### 速览
* VPG 是一种同轨策略（On-policy）的算法。
* VPG 可用于带有离散或连续动作空间的环境。
* VPG 的 Spinning Up 实现支持 MPI 并行化。

## 核心公式
令 $\pi_{\theta}$ 表示以 $\theta$ 参数化的策略，而 $J(\pi_{\theta})$ 表示预期的有限视界、未打折的策略收益。 $J(\pi_{\theta})$的梯度为：

$$\nabla_{\theta} J(\pi_{\theta}) = E_{\tau \sim \pi_{\theta}}{
    \sum_{t=0}^{T} \nabla_{\theta} \log \pi_{\theta}(a_t|s_t) A^{\pi_{\theta}}(s_t,a_t)
    },$$

其中 $\tau$ 是轨迹，而 $A^{\pi_{\theta}}$ 是当前策略的优势函数。

策略梯度算法的工作原理是通过随机梯度上升来增强策略性能，用以更新策略参数：

$$\theta_{k+1} = \theta_k + \alpha \nabla_{\theta} J(\pi_{\theta_k})$$

策略梯度实现通常基于无限视界、打折的收益来计算优势函数估计，
尽管其他情况下使用有限视界、未打折的策略梯度公式。

> Sutton 书中解释 MDP 概念中通常分为三种任务：有限视界，不定视界以及无限视界
> * 有限视界（finite- horizon）：交互在特定固定数量的时间步长后终止
> * 不定视界（indefinite-horizon）：交互可以任意长单最后必须终止
> * 无限视界（infinite-horizon）：交互永不终止

### 试探与开发
VPG 以同轨策略训练随机策略。
这意味着 VPG 会根据其最新的随机策略的最新本通过采样动作来进行试探。
动作选择的随机性取决于初始条件和训练过程。
在训练过程中，由于更新规则鼓励该策略开发已经发现的收益，因此该策略通常变得越来越少随机性。
这可能会导致策略陷入局部最优状态。

## 伪代码
TBD

## 细节
TBD

## 参考文献
* Policy Gradient Methods for Reinforcement Learning with Function Approximation, Sutton et al. 2000
* Optimizing Expectations: From Deep Reinforcement Learning to Stochastic Computation Graphs, Schulman 2016(a)
* Benchmarking Deep Reinforcement Learning for Continuous Control, Duan et al. 2016
* High Dimensional Continuous Control Using Generalized Advantage Estimation, Schulman et al. 2016(b)