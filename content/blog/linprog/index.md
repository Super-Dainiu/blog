---
title: Linear Programming
date: "2022-06-06"
description: "Review of Linear Programming"
---

## Interior Point Method

#### Intro

There are three types of Interior Point Methods.

- Affine Scaling Algorithm
- Potential Reduction
- Path Following ✌
  - Primal -> Barrier Method
  - Primal-Dual -> KKT System

In this chapter, we will consider the linear programming problem in standard form.
$$
\begin{align}

\min\, &c^Tx\\
\textrm{s.t}\, &Ax=b\\
&x>0

\end{align}
$$


**Def 4.1** Given polyhedron $P=\{x|Ax=b, x\ge 0\}$, the interior point of  $P$ is defined as $\{x\in P|x>0\}$. #

#### Primal Method

If we only consider the primal problem, we could integrates inequality constraints to the objective function using a logarithmic barrier $\phi(x) = \sum_{i=1}^n log(x_i)$.

**Def 4.2 (Barrier Method)**  To solve the LP problem in standard form, we introduce a variable $\mu > 0$, and the problem can be reformulated as $(P_\mu)$,
$$
\begin{align}
	\min &\quad c^Tx-\mu\sum^n_{i=1}log(x_i)\\
	\textrm{s.t}&\quad Ax=b
\end{align}
$$
$\forall \mu > 0$, $\exist$ unique $x(\mu)$ that solves $(P_\mu)$. When $\mu\downarrow0$, $\lim_{\mu\rightarrow0}x(\mu) = x^*$.#

#### Primal-Dual Method

If we consider both the primal and dual problem, we could solve the KKT condition of the LP problem. Let us start with the KKT condition of the standard form.
$$
\left\{\begin{array}{l}
A x=b \\
A^{\top} y+s=c \\
x_{i} s_{i}=0 \quad i=1, \cdots, 2, n \\
(x, s)>0
\end{array}\right.
$$
Define the non-linear system,
$$
F(x, y, s)=
\begin{pmatrix}
Ax-b\\
A^T+s-c\\
x\circ s
\end{pmatrix} = 0
$$
Intuitively, we will use Newton method to solve non-linear systems. But here, we will first define a feasible set $\mathcal{F}={(x, y, s)|Ax=b, A^Ty+s=c, (x, s)>0}$, and a central path $(x(\mu), y(\mu), s(\mu))\in \mathcal{F}$, which converges to $F(x, y, s)=0$. The central path is given by,
$$
F(x(\mu), y(\mu), s(\mu))=
\begin{pmatrix}Ax-b\\
A^T+s-c\\
x\circ s - \mu
\end{pmatrix} 
= 0
$$
**Def 4.3 (Primal-Dual Method)** Given the above central path. $\forall \mu > 0$, $\exist$ unique $$(x(\mu), y(\mu), s(\mu))\in \mathcal{F}$$ that solves $F(x(\mu), y(\mu), s(\mu))=0$. When $\mu\downarrow0$, $\lim_{\mu\rightarrow0}(x(\mu), y(\mu), s(\mu)) = (x^*, y^*, s^*)$.#
