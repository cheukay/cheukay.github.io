---
title: Maximum Likelihood Estimation - Machine Learning Notes 1
date: 2018-10-12 
mathjax: true
tags: ["Machine Learning"]
categories: ["Robotics"]
---
## Parameter Estimation
How do we find appropriate distribution to a random variable?

**3 steps:**
* Choose a parameter model (e.g. Gaussian)
* Assemble a collecxtion of sample from $X$, which is $D = \{x_1, x_2, ..., x_N\}$
(we assume that $x_1, x_2, ..., x_N$ are independent, that means $x_i $ are IID)
* Maximum Likelihood Principle: "The optimal parameter $\theta^*$ is that maximize the probability (likelihood) of the data $D$ "

## Maximum Likelihood Estimation (MLE)

$$
\begin{aligned} \theta^{*} &=\arg\max_{\theta} \frac{P(D | \theta)}{\log P(D | \theta)} \\\\ &=\arg \max _{D} \operatorname{\log} P(D | \theta) \end{aligned}
$$

$P(D | \theta)$ is likelihood of data w.r.t. $\theta$, $\log P(D | \theta)$, a function of $\theta$, is the log likelihood.

### Data Log Likelihood

$$\begin{aligned} l(\theta) &=\log P(D|\theta) \\\\ &=\log _{i=1}^{N} p\left(x_{i} | \theta\right) \\\\ &=\sum_{i=1}^{N} \log P\left(x_{i} | \theta\right) \end{aligned}$$

### To get ML solution
* if $\theta$ is scalar:
  1. $\frac{\partial}{\partial \theta} \log P(D | \theta)=0$  at $\theta^{*}$
  2. $\frac{\partial^{2}}{\partial \theta^{2}} \log p(D | \theta)<0$ at at $\theta^{*}$
  3. check boundary condiction on $\theta$

* if $\theta$ is scalar:
  1. $$\nabla_{\theta}(\theta)=\left[\begin{array}{c}{\frac{\partial}{\partial \theta_{1}}l(\theta)} \\\\...\\\\ {\frac{\partial}{\partial \theta_{2}}(\phi \theta)}\end{array}\right]=0$$
  2. $$\nabla_{\theta}^{2}(\omega)=\left[\begin{array}{c}{\frac{\partial^{2}}{\partial p_{2}}l(\theta)\cdots\frac{\partial^{2}}{\partial \theta_{0}\partial\theta_{p}}l(\theta)} \\\\ {\cdots}  \\\\ {\frac{\partial^{2}}{\partial \theta_{p} \mu_{0}}l(\theta)\cdots \frac{\partial^{2}}{\partial \theta_{p}}l(\theta)}\end{array}\right] < 0$$

--------------
## Example

### Bernoulli
Bernoulli distribution:$\theta=\pi, 0 \leq \pi \leq 1, x \in(0,1]$. Its log likelihood is:
$$
\begin{aligned} l(\theta) &=\sum_{i=1}^{N} \log p\left(x_{i} | \theta\right)=\sum_{i=1}^{N} \log \left[\pi^{x_{i}}(1-\pi)^{t-x_{i}}\right] \\\\ &=\sum_{i=1}^{N}\left[x_{i} \log \pi+\left(1-x_{i}\right) \log (1-\pi)\right] \\\\ &=\left(\sum_{i=1}^{\sum} x_{i}\right) \log \pi+\left[\sum_{i=1}^{N}\left(1-x_{i}\right)\right] \log (1-\pi) \end{aligned}$$
let $\sum_{i=1}^{N} x_{i}^{\prime}=m$, we have:
$$l(\theta)=m \log \pi+(N-m) \log (1-\pi)$$

Solve it:
1. First derivative:
   $$\frac{\partial}{\partial x}(w)=\frac{m}{\lambda}-\frac{m-m}{1-\lambda}=0$$
$$\begin{array}{r}{(1-\pi) m-\pi(N-m)=0} \\\\ {m-\pi m-\pi N+\pi m=0} \\\\ {\pi N=m}\end{array}$$

2. Second derivative:
   $$\begin{aligned} \frac{\partial^{2}}{\partial \pi^{2}}(1 \theta) &=\frac{\partial}{\partial \Omega}\left(\frac{m}{\pi}-\frac{N-m}{1-\pi}\right) \\\\ &=-\frac{m}{\pi^{2}}-\frac{N-m}{(1-\pi)^{2}} \end{aligned}$$

3. Boundary condiction:
$$\hat{\pi}=\frac{m}{N}, 0 \leq m \leq N, 0 \leq \hat{\pi} \leq 1$$

### Gaussian
* $\theta=\mu$, assume that $\sigma^2$ is known:
$$
\begin{aligned}l(\theta) &=\sum_{v=1}^{N} \log P\left(x_{i} | \theta\right) \\ &=\sum_{i=1}^{N} \log \frac{1}{\sqrt{2 \pi} b} e^{-\frac{1}{2} \frac{\left(x_{i}-\mu\right)^{2}}{\sigma^{2}}} \\ &=\sum_{i=1}^{N}-\frac{1}{2} \log 2 \pi-\frac{1}{2} \log b^{2}-\frac{1}{2 b^{2}}\left(x_{i}-\mu\right)^{2} \\ &=-\frac{N}{2} \log 2 \pi-\frac{N}{2} \log b^{2}-\frac{1}{2 b^{2}} \sum_{i=1}^{N}\left(x_{i}-\mu\right)^{2} \end{aligned}
$$

1. First derivative:
$$
\begin{aligned} \frac{\partial}{\partial \mu}(\omega) &=\frac{\partial}{\partial \mu}\left(-\frac{1}{2 b^{2}} \sum_{i=1}^{N}\left(x_{i}-\mu\right)^{2}\right) \\ &=-\frac{1}{2 \partial^{2}} \sum_{i=1}^{N} 2\left(x_{i}-\mu\right)(-1)=0 \\ & \Rightarrow \sum_{i=1}^{N}\left(x_{i}-\mu\right)=0 \Rightarrow \sum_{i=1}^{N} x_{i}-N_{\mu}=0 \\ \Rightarrow & \hat{M}=\frac{1}{N} \sum_{j=1}^{N} x_{i} \end{aligned}
$$

2. Second derivative:
$$\frac{\partial^{2}}{\partial \mu^{2}}l(\theta)=\frac{\partial}{\partial \mu}\left(x_{i}-\mu\right)=-1<0.$$

* $\theta = \sigma^2$, assume that $\mu$ is known:

$$\begin{aligned} \frac{\partial}{\partial \sigma^{2}}l(\theta)=& \frac{\partial}{\partial \sigma^{2}}\left[-\frac{N}{2} \log 2 \pi-\frac{N}{2} \log b^{2}-\frac{1}{2 \theta^{2}} \sum_{i=1}^{N}\left(x_{i}-\mu\right)^{2}\right]\\ 
&=-\frac{N}{2} \frac{1}{\sigma^{2}}+\frac{1}{2} \frac{1}{\sigma^{4}}\sum_{i=1}^{N}\left(x_{i}-\mu\right)^{2}=0 \\ 

& =-\frac{N}{2} \sigma^{2}+\frac{1}{2} \sum_{i=1}^{N}\left(x_{i}-\mu\right)^{2}=0 \end{aligned}$$

$$\hat{\sigma}^{2}=\frac{1}{N} \sum_{i=1}^{N}\left(x_{i}-\mu\right)^{2}$$

$$\frac{\partial^{2}}{\partial\left(\sigma^{2}\right)^{2}}l(\theta)= ...$$
-----------
## Estimator
* The **estimate** ($\hat{\mu}$) is a number;
* The **estimator** ($\mu$) is random variables.

 The estimate is the value of an estimator for a given dataset $D$.
 Since the estimator is a random variable, then we can calculate the mean and variance , which help us to qualify how good the estimator is.

## Bias and Variance
For $\hat{\theta} = f(x_1, x_2, ..., x_N)$, the question is:
1. Will the estimator converge to the true value of $\theta$?
   $$\operatorname{Bias}(\hat{\theta})=E_{x_{1}...x_{N}}[\hat{\theta}-\theta]=E[\hat{\theta}]-\theta$$
2. How long would it take? How many samples we need?

   $$\operatorname{Var}(\hat{\theta})=E_{x_{1}...x_{N}}\left[(\hat{\theta}-E(\hat{\theta}))^{2}\right]$$


## Summary
### Important Asymptotic Properties of MLE

1. Consistent: as $N \rightarrow \infty$, the estimated value converges to the true value.

2. Efficient: as $N \rightarrow \infty$, the Cramér–Rao lower bound (CRLB) is bounded on the variance of any unbiased estimator, i.e. no unbiased estimator can get lower variance.