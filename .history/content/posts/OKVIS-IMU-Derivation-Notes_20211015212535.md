---
title: Notes on State Derivation of IMU Model in OKVIS
date: 2018-05-14 
mathjax: true
tags: [SLAM, VIO]
categories: Robotics
---
## Background
In OKVIS paper, states are:
$$
\mathbf{x}_{\mathrm{R}}:=\left[_{W} \mathbf{r}_{S}^{\mathrm{T}}, \mathbf{q}_{W S}^{\mathrm{T}}, s \mathbf{v}^{\mathrm{T}}, \mathbf{b}_{\mathrm{g}}^{\mathrm{T}}, \mathbf{b}_{\mathrm{a}}^{\mathrm{T}}\right]^{\mathrm{T}} \in \mathbb{R}^{3} \times S^{3} \times \mathbb{R}^{9}
$$

The minimal robot error state error:
$$
\delta \boldsymbol{\chi}_{\mathrm{R}}=\left[\delta \mathbf{p}^{\mathrm{T}}, \delta \boldsymbol{\alpha}^{\mathrm{T}}, \delta \mathbf{v}^{\mathrm{T}}, \delta \mathbf{b}_{\mathrm{g}}^{\mathrm{T}}, \delta \mathbf{b}_{\mathrm{a}}^{\mathrm{T}}\right]^{\mathrm{T}} \in \mathbb{R}^{15}
$$

We devive the linearized model of the error states:

$$
\delta \dot{\boldsymbol{\chi}}_{\mathrm{R}} \approx \mathbf{F}_{c}\left(\overline{\mathbf{x}}_{\mathrm{R}}\right) \delta \boldsymbol{\chi}_{\mathrm{R}}+\mathbf{G}\left(\overline{\mathbf{x}}_{\mathrm{R}}\right) \mathbf{w}
$$

## Derivation
### Translation

$$\begin{aligned} \delta_{W} \dot{\mathbf{r}}_{S} &=\delta \mathbf{C}_{WS}{_S\mathbf{v}}
\\ &=\dot{\mathbf{C}}_{WS} { _S\mathbf{v} + \mathbf{C}_{WS}} {_S\mathbf{\dot{v}}}
\\ &=-[\delta \boldsymbol{a}]_{\times} \mathbf{C}_{WS} {_S\mathbf{v}}+\mathbf{C}_{W S} \delta_{S} \mathbf{v} 
\\ &=-\left[\mathbf{C}_{WS} {_S\mathbf{v}}\right]_{\times} \delta \boldsymbol{\alpha}+\mathbf{C}_{W S} \delta_{S} \mathbf{v} 
\\ &=\left[\mathbf{C}_{W S}{_S\mathbf{v}}\right]_{\times} \delta \boldsymbol{a}+\mathbf{C}_{W S} \delta_{S} \mathbf{v} \end{aligned}$$

### Rotation
$$\because \mathbf{C}_{W S}=\left[\mathbf{I}-[\delta \boldsymbol{a}]_{\times}\right] \overline{\mathbf{C}}_{W S} \quad \therefore[\delta \boldsymbol{a}]_{\times}=\mathbf{I}-\mathbf{C}_{W S} \overline{\mathbf{C}}_{W S}^{T}$$

$$\therefore[\delta \ddot{a}]_{\times}=-\dot{\mathbf{C}}_{W S} \overline{\mathbf{C}}_{W S}^{T}-\mathbf{C}_{W S} \dot{\overline{\mathbf{C}}}_{W S}^{T}$$

$$
\begin{aligned} \because \dot{\mathbf{C}}_{W S} &=\mathbf{C}_{W S} \mathbf{\Omega}, \quad \mathbf{\Omega}=[\mathbf{\omega}]_{\times} \\ \dot{\overline{\mathbf{C}}}_{W S} &=\overline{\mathbf{C}}_{W S} \overline{\mathbf{\Omega}}, \quad \overline{\mathbf{\Omega}}=[\overline{\mathbf{\omega}}]_{\mathbf{X}} \end{aligned}
$$

$$\begin{aligned} \therefore[\delta \dot{\mathbf{a}}]_{\mathrm{X}} &=-\mathbf{C}_{W S} \mathbf{\Omega} \overline{\mathbf{C}}_{W S}^{T}-\mathbf{C}_{W S}\left(\overline{\mathbf{C}}_{W S} \overline{\mathbf{\Omega}}\right)^{T}
\\\\ &=-\mathbf{C}_{W S} \mathbf{\Omega} \overline{\mathbf{C}}_{W S}^{T}+\mathbf{C}_{W S} \overline{\mathbf{\Omega}}^{T} \overline{\mathbf{C}}_{W S}^{T}
\\\\ &=-\left[\mathbf{I}-[\delta \boldsymbol{a}]_{\times}\right] \overline{\mathbf{C}}_{W S} \mathbf{\Omega} \overline{\mathbf{C}}_{W S}^{T}+\left[\mathbf{I}-[\delta \boldsymbol{a}]_{\times}\right] \overline{\mathbf{C}}_{W S} \overline{\mathbf{\Omega}}^{T} \overline{\mathbf{C}}_{W S}^{T} \\\\
&=-\overline{\mathbf{C}}_{W S} \mathbf{\Omega} \overline{\mathbf{C}}_{W S}^{T}+[\delta \boldsymbol{a}]_{\times} \overline{\mathbf{C}}_{W S} \mathbf{\Omega} \overline{\mathbf{C}}_{W S}^{T}+\overline{\mathbf{C}}_{W S} \overline{\mathbf{\Omega}}^{T} \overline{\mathbf{C}}_{W S}^{T}-[\delta \boldsymbol{a}]_{\times} \overline{\mathbf{C}}_{W S}^{T} \overline{\mathbf{C}}_{W S}^{T} \\\\
&=-\overline{\mathbf{C}}_{W S}(\mathbf{\Omega}-\overline{\boldsymbol{\Omega}}) \overline{\mathbf{C}}_{W S}^{T}+[\delta \boldsymbol{a}]_{\times} \overline{\mathbf{C}}_{W S}(\mathbf{\Omega}-\overline{\boldsymbol{\Omega}}) \overline{\mathbf{C}}_{W S}^{T} \end{aligned}$$

Let $[\delta \mathbf{\omega}]_{\times}=\mathbf{\Omega}-\overline{\mathbf{\Omega}}$, ignore $[\delta \dot{\boldsymbol{a}}]_{\times} \approx-\overline{\mathbf{C}}_{W S}[\delta \boldsymbol{\omega}]_{\times} \overline{\mathbf{C}}_{W S}^{T}$

$${\because[\mathbf{C r}]_{\times}=\mathbf{C}[\mathbf{r}]_{\times} \mathbf{C}^{T}}$$

$${\therefore[\delta \dot{\boldsymbol{a}}]_{\times}=-\left[\overline{\mathbf{C}}_{W S} \delta \mathbf{\omega}\right]_{\times} \Rightarrow \delta \dot{\boldsymbol{\alpha}}=-\overline{\mathbf{C}}_{W S} \delta \boldsymbol{\omega}}$$

$${\because \delta \mathbf{\omega}=\delta\left(\tilde{\mathbf{\omega}}+\mathbf{w}_{\mathrm{g}}-\mathbf{b}_{\mathrm{g}}\right)=-\delta \mathbf{b}_{\mathrm{g}}}$$

$${\therefore \delta \dot{\boldsymbol{\alpha}}=-\overline{\mathbf{C}}_{W S}\left(-\delta \mathbf{b}_{\mathrm{g}}\right)=\overline{\mathbf{C}}_{W S} \delta \mathbf{b}_{\mathrm{g}}}$$

### Velocity

$$
\begin{array}{l}{\delta_{S} \dot{\mathbf{v}}=\delta\left(_{S} \mathbf{a}+\mathbf{w}_{a}-\mathbf{b}_{a}+\mathbf{C}_{S W W} \mathbf{g}-\left(_{S} \mathbf{\omega}\right) \times_{S} \mathbf{v}\right)} \\\\ {\quad=-\delta \mathbf{b}_{a}+\mathbf{C}_{S W}[\delta \boldsymbol{a}]_{\times W} \mathbf{g}-\left[\delta_{S} \mathbf{\omega}\right]_{\times S} \mathbf{v}-\left[_{S} \mathbf{\omega}\right]_{\times} \delta_{S} \mathbf{v}} \\\\ {\quad=-\mathbf{C}_{S W}\left[_{W} \mathbf{g}\right]_{\times} \delta \boldsymbol{\alpha}-\left[-\delta \mathbf{b}_{g}\right]_{\times S} \mathbf{v}-\left[_{S} \boldsymbol{\omega}\right]_{\times} \delta_{S} \mathbf{v}-\delta \mathbf{b}_{a}} \\\\ {\quad=-\mathbf{C}_{S W}\left[_{W} \mathbf{g}\right]_{\times} \delta \boldsymbol{\alpha}-\left[_{S} \mathbf{\omega}\right]_{\times} \delta_{S} \mathbf{v}-\left[_{S} \mathbf{v}\right]_{\times} \delta \mathbf{b}_{g}-\delta \mathbf{b}_{a}}\end{array}
$$

### Gyro Bias

$$\delta \dot{\mathbf{b}}_{g}=0$$

### Accelerometer Bias

$$\delta \dot{\mathbf{b}}_{\mathrm{a}}=-\frac{1}{\tau} \delta \mathbf{b}_{\mathrm{a}}$$

Finally, we get:
$$
\delta \dot{\boldsymbol{\chi}}_{\mathrm{R}} \approx \mathbf{F}_{c}\left(\overline{\mathbf{x}}_{\mathrm{R}}\right) \delta \boldsymbol{\chi}_{\mathrm{R}}+\mathbf{G}\left(\overline{\mathbf{x}}_{\mathrm{R}}\right) \mathbf{w}
$$
where
$$
\mathbf{F}_{c}=\left[\begin{array}{ccccc}{\mathbf{0}_{3 \times 3}} & {\left[\mathbf{C}_{W S S} \overline{\mathbf{v}}\right]^{\times}} & {\overline{\mathbf{C}}_{W S}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} \\ {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\overline{\mathbf{C}}_{W S}} & {\mathbf{0}_{3 \times 3}} \\ {\mathbf{0}_{3 \times 3}} & {-\overline{\mathbf{C}}_{W S}\left[_{W \mathbf{B}}\right]^{\times}} & {-\left[_{S} \overline{\boldsymbol{\omega}}\right]^{\times}} & {-[s \overline{\mathbf{v}}]^{\times}} & {-\mathbf{I}_{3}} \\ {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} \\ {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {\mathbf{0}_{3 \times 3}} & {-\frac{1}{\tau} \mathbf{I}_{3}}\end{array}\right],
$$
and
$$
\mathbf{G}=\left[\begin{array}{cccc}{\mathbf{0}} & {\mathbf{0}} & {\mathbf{0}} & {\mathbf{0}} \\ {\mathbf{I}_{3}} & {\mathbf{0}} & {\mathbf{0}} & {\mathbf{0}} \\ {\mathbf{0}} & {\mathbf{I}_{3}} & {\mathbf{0}} & {\mathbf{0}} \\ {\mathbf{0}} & {\mathbf{0}} & {\mathbf{I}_{3}} & {\mathbf{0}} \\ {\mathbf{0}} & {\mathbf{0}} & {\mathbf{0}} & {\mathbf{I}_{3}}\end{array}\right]
$$

## Reference
1. Leutenegger, S., Lynen, S., Bosse, M., Siegwart, R., & Furgale, P. (2015). Keyframe-based visual–inertial odometry using nonlinear optimization. The International Journal of Robotics Research, 34(3), 314-334.
2. Savage, Paul G. "Strapdown inertial navigation integration algorithm design part 1: Attitude algorithms." Journal of guidance, control, and dynamics 21.1 (1998): 19-28.
3. Savage, Paul G. "Strapdown inertial navigation integration algorithm design part 2: Velocity and position algorithms." Journal of Guidance, Control, and Dynamics 21.2 (1998): 208-221.
4. Shin, Eun-Hwan, and Naser El-Sheimy. "An unscented Kalman filter for in-motion alignment of low-cost IMUs." Position Location and Navigation Symposium, 2004. PLANS 2004. IEEE, 2004.
5. Sola, Joan. "Quaternion kinematics for the error-state KF." Laboratoire d’Analyse et d’Architecture des Systemes-Centre national de la recherche scientifique (LAAS-CNRS), Toulouse, France, Tech. Rep (2012).

