---
title: Linear Programming
date: "2022-06-06"
description: "Review of Linear Programming"
---

## Interior Point Method

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


**Def 4.1** Given polyhedron $P=\{x|Ax=b, x\ge 0\}$, the interior point of  $P$ is defined as $\{x\in P|x>0\}$.

**Def 4.2 (Barrier Method)**  To solve the LP problem in standard form, we introduce a variable $\mu > 0$, and the problem can be reformulated as,
$$
\begin{align}
	\min &\quad c^Tx-\mu\sum^n_{i=1}log(x_j)\\
	\textrm{s.t}&\quad Ax=b
\end{align}
$$
