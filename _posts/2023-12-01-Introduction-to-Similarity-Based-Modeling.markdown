---
title:  "Introduction to Similarity-Based Model for Anomaly Detection"
date:   2023-12-01 12:30:00
categories: [anomaly-detection, similarity-based-modeling, non-parametric, machine-learning, predictive-maintenance, unsupervised-learning]
tags: [anomaly-detection, similarity-based-modeling, non-parametric, machine-learning, predictive-maintenance, unsupervised-learning]
author: Redoine Z.
---


Similarity-Based Modeling is a non-parametric unsupervised learning technique that enables modeling the working state of a system, primarily used for anomaly detection.

## Context
Let \\(D \in \mathcal{M}_{n,p}(\mathbb{R})\\) such that each row \\(D_i = x(t_i) \in \mathbb{R}^p\\) is a measure of \\(p\\) sensors \\(x_j\\) describing the given state of a working system at time \\(t_i\\).

$$
D = \begin{bmatrix}
x_1(t_1) & \ldots & x_j(t_1) & \ldots & x_p(t_1) \\ 
\vdots & \vdots & \vdots & \vdots & \vdots \\ 
\vdots & \vdots & \vdots & \vdots & \vdots \\ 
x_1(t_i) & \ldots & x_j(t_i) & \ldots & x_p(t_i)\\ 
\vdots & \vdots & \vdots & \vdots & \vdots\\ 
x_1(t_n) & \ldots & x_j(t_n) & \ldots & x_p(t_n)
\end{bmatrix}
$$

Given the knowledge of \\(D\\), we are going to present a technique modeling the working system based on similarity operators. This technique is called "Similarity-based Modeling" and helps detect anomalies by assessing how well a new observation \\(x(\tau)\\) is similar to the observations collected in \\(D\\). As a result, the choice of \\(D\\) is a question of matter and should take domain knowledge into account.

**Remark:** \\(D\\) is called the state matrix of the system.

## Linear Modeling
Given a new observation \\(x(\tau)\\) of the system at time \\(\tau\\), the linear statement of this model is described by:

$$
\begin{matrix}
\underset{\omega(\tau) \in \mathbb{R}^n}{\min}  \left \| \hat{x}_{\omega}(\tau) - x(\tau) \right \|^2\\ \\
\hat{x}_{\omega}(\tau) = \omega (\tau) \cdot D
\end{matrix}.
$$

To simplify the notations, we will avoid writing \\(\tau\\) and \\(\omega\\).

### Optimal Solution
Let \\(E:\omega \mapsto |\hat{x} - x|^2 \\). The directional derivative of \\(E\\) along a given vector \\(\nu\\) at a given point \\(\omega\\) is defined as 

$$
\nabla_{\nu} E(\omega) := \underset{\varepsilon \mapsto 0}{\lim} \frac{E(\omega + \varepsilon \nu) - E(\omega)}{\varepsilon}
$$

$$
\nabla_{\nu} E (\omega) := \nabla E(\omega) \cdot \nu
$$

One can calculate \\(\nabla E_{\nu}(\omega)\\) to identify the gradient of \\(E\\) at point \\(\omega\\) and show that:

$$
\nabla E (\omega) = 2 \omega \cdot D \cdot  D^T - 2 x \cdot D^T
$$

Let \\(\omega_0\\) be a critical point of \\(E\\). Therefore,

$$
\omega_0 \cdot D \cdot D^T = x \cdot D^T
$$

We can immediately conclude that \\(\omega_0\\) is the unique global extremum if and only if \\(D \cdot D^T\\) is non-singular. Furthermore, one can calculate the Hessian matrix of \\(E\\) at any point \\(\omega\\) and show that: 

$$
\nabla^2 E(\omega) = 2 D \cdot D^T
$$

Hence, we can conclude that for all \\(\omega\\), \\(\nabla^2 E(\omega)\\) is positive definite. This means that \\(\omega_0\\) is a minimum (local or global). Therefore, \\(\omega_0\\) is the global minimum if and only if \\(D D^T\\) is non-singular. In this case, we have an analytical formula to compute and determine \\(\omega_0\\):

$$\omega_0 = (x \cdot D^T) \cdot (D\cdot D^T)^{-1}$$

### Comments
The linear statement of the Similarity-Based Modeling has some drawbacks, and the main one is the fact that \\(DD^T\\) needs to be non-singular to compute the global minimum. Furthermore, the linear statement fails to model the system when the data is not linear enough.
