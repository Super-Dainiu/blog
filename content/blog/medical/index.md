---
title: Medical Image Processing
date: "2022-06-23"
description: "Cheatsheet of Medical Image Processing"
---

## Enhancement

### Filtering

Additive model
$$
\underbrace{f(x, y)}_{\text {observed image }}=\underbrace{u(x, y)}_{\text {unstained image }}+\underbrace{n(x, y)}_{\text {noise }}, \quad(x, y) \in \Omega
$$
Method noise ($\mathcal{D}$ is the denoising operator)
$$
f(x, y)-\mathcal{D}\{f\}(x, y)
$$
Ideal denoising operator $\mathcal{D}$ should have
$$
f(x, y)-\mathcal{D}\{f\}(x, y)\sim\mathcal{N}(\cdot|\mu, \sigma)
$$
An isotropic Gaussian filter
$$
\begin{aligned}
&G_{\sigma}(x, y)=\frac{1}{2 \pi \sigma^{2}} e^{-\frac{x^{2}+y^{2}}{2 \sigma^{2}}} \\
&u(x, y)=G_{\sigma}(x, y) * f(x, y)
\end{aligned}
$$
Implementation (suppress the high frequency information)
$$
u(x, y)=\mathcal{F}^{-1}\left\{e^{-2 \pi^{2} \sigma^{2}\left(\xi_{1}^{2}+\xi_{2}^{2}\right)} \hat{f}\left(\xi_{1}, \xi_{2}\right)\right\}
$$

### Scale Space

#### Heat Equation

Green's Theorem
$$
\underbrace{\oint_{\partial\Omega} \vec{F} \cdot \vec{n} d s}_{\substack{\text { Outward } \\ \text { Flux }}}=\iint_{\Omega}\underbrace{\left(\frac{\partial M}{\partial x}+\frac{\partial N}{\partial y}\right)}_{\text {Divergence }} d x d y
$$
Heat flow is a vector field


$$
V(x, y, t)=-c(x, y) \nabla u(x, y, t)
$$
where $\nabla=\left(\frac{\partial}{\partial x}, \frac{\partial}{\partial y}\right), c(x, y)$ is the thermal conductivity.

Temperature change over $\Omega_p$
$$
-\oint_{\partial \Omega_{p}} V(x, y, t) \cdot n d s=-\iint_{\Omega_{p}} \operatorname{div}(V(x, y, t)) d x d y
$$
Taking the limit of $\left|\Omega_{p}\right| \rightarrow 0$, the rate of change becomes
$$
\frac{\partial u(x, y, t)}{\partial t} = \operatorname{div}(c(x, y) \nabla u(x, y, t))
$$

#### Isotropic Diffusion

Solve $u(x, y, t)$ from a PDE
$$
\begin{aligned}
&\frac{\partial u}{\partial t}=\frac{\partial^{2} u}{\partial x^{2}}+\frac{\partial^{2} u}{\partial y^{2}} \\
&u(x, y, 0)=f(x, y)
\end{aligned}
$$
Frequence domain
$$
\begin{gathered}
u(x, y, t) \stackrel{\mathcal{F}}{\rightarrow} \hat{u}\left(\xi_{1}, \xi_{2}, t\right)\\
\frac{\partial}{\partial t} \hat{u}\left(\xi_{1}, \xi_{2}, t\right)=-4 \pi^{2}\left(\xi_{1}^{2}+\xi_{2}^{2}\right) \hat{u}\left(\xi_{1}, \xi_{2}, t\right) \quad \text { (differentiation property) } \\
\hat{u}\left(\xi_{1}, \xi_{2}, 0\right)=\hat{f}\left(\xi_{1}, \xi_{2}\right) .
\end{gathered}
$$
Solution
$$
\hat{u}\left(\xi_{1}, \xi_{2}, t\right)=\hat{u}\left(\xi_{1}, \xi_{2}, 0\right) e^{-4 \pi^{2}\left(\xi_{1}^{2}+\xi_{1}^{2}\right) t}
$$
Equivalent to Gaussian smoothing
$$
\begin{gather}
g_{\tau}(x, y)=\frac{1}{4 \pi \tau} e^{-\frac{x^{2}+y^{2}}{4 \tau}}, \quad \tau=\frac{\sigma^{2}}{2} \\
u(x, y, \tau)=g_{\tau}(x, y) * f(x, y) \\
u(x, y, 0)=f(x, y)
\end{gather}
$$

#### Anisotropic Diffusion

$$
\begin{aligned}
u_{t} &=\operatorname{div}(c(x, y, t) \nabla u) \\
&=c_{x} u_{x}+c u_{x x}+c_{y} u_{y}+c u_{y y} \\
&=\nabla c \cdot \nabla u+c \nabla^{2} u
\end{aligned}
$$
Choice of $c(x, y, t)$
$$
\begin{aligned}
c(x, y, t) &=e^{-(\|\nabla u\| / k)^{2}} \\
\text { or } c(x, y, t) &=\frac{1}{1+\left(\frac{\|\nabla u\|}{k}\right)^{2}} .
\end{aligned}
$$

#### Method noise

Taylor expansion trick
$$
\begin{aligned}
u(x, y, \tau) &=u(x, y, 0)+\tau u_{t}(x, y, 0)+O\left(\tau^{2}\right)
\end{aligned}
$$
Hence,
$$
f-\mathcal{D}\{f\}=-\tau u_{t}(x, y, 0)+O\left(\tau^{2}\right)
$$
For different methods
$$
f-\mathcal{GF}\{f\}=-\tau \nabla^2f+O\left(\tau^{2}\right)\\
f-\mathcal{AD}\{f\}=-\tau \operatorname{div}\left(c(x, y, 0)\nabla f\right)+O\left(\tau^{2}\right)
$$

### Calculus of variations

<img src="img/1.JPG" style="zoom:67%;" />

### Total Variance Denoising

Energy function
$$
\min _{u} \iint_{\Omega} \underbrace{\|\nabla u\|}_{\text {total variation }}+\frac{\lambda}{2}(f-u)^{2} d x d y .
$$
E-L equation
$$
\begin{aligned}
\frac{\delta E}{\delta u} &=\lambda(u-f)-\frac{\partial}{\partial x}\left(\frac{u_{x}}{\sqrt{u_{x}^{2}+u_{y}^{2}}}\right)-\frac{\partial}{\partial y}\left(\frac{u_{y}}{\sqrt{u_{x}^{2}+u_{y}^{2}}}\right) \\
&=\lambda(u-f)-\operatorname{div}\left(\frac{\nabla u}{\|\nabla u\|}\right)
\end{aligned}
$$
Method noise
$$
f-T V D\{f\}=-\frac{1}{\lambda} \operatorname{curv}(T V D\{f\})
$$

### Solve PDE

<a href="ref/常微分方程.pdf">Lecture notes (previous course)</a>

### Roadmap

<img src="img/2.JPG" style="zoom:67%;" />

## Registration

General Formulation
$$
E(\phi) = d(I, J\circ\phi) + \lambda L(\phi)
$$

### Similarity metrics

1. Sum of square distance

$$
d(I, J) = \sum_{x\in\Omega}\left(I(x) - J(x)\right)^2
$$

2. Cross correlation

   Cross correlation quantifies the linear relationship

$$
\begin{aligned}
&c c(I, J)=\frac{\mathbb{E}\left[\left(i-\mu_{i}\right)\left(j-\mu_{j}\right)\right]}{\mathbb{E}\left[\left(i-\mu_{i}\right)^{2}\right]^{\frac{1}{2}} \mathbb{E}\left[\left(j-\mu_{j}\right)^{2}\right]^{\frac{1}{2}}} \propto \frac{\left\langle I-\mu_{I}, J-\mu_{J}\right\rangle}{\sigma_{I} \sigma_{J}}\\
&\text { where }\left\{\begin{array}{l}
i=I(x), x \sim u\left(\Omega_{d}\right) \\
j=J(x), x \sim u\left(\Omega_{d}\right)
\end{array}\right.
\end{aligned}
$$

3. Mutual information

$$
\begin{aligned}
\operatorname{MI}(I ; J) &=\mathrm{KL}(P(i, j) \| P(i) P(j)) \\
&=\sum_{i} \sum_{j} P(i, j) \log \frac{P(i, j)}{P(i) P(j)}\\
&=\sum_i\sum_j P(i, j)\log P(i, j) - \sum_i P(i)\log P(i) - \sum_j P(j)\log P(j)\\
&=-H(I, J)+H(I)+H(J)
\end{aligned}
$$

