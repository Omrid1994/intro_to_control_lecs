# Introduction to Control Theory



(section-label-1)=
## Stability of Linear Systems

We assume that the students are familiar with the basic concepts of linear systems analysis.

A linear time-invariant (LTI) system $\Sigma$ can be modeled by state-space equations 

\begin{align*}
	\begin{cases}
		\dot{x}(t)=Ax(t)+Bu(t),\\
		y(t)=Cx(t)+Du(t).
	\end{cases}
\end{align*}
Here $x(t)\in\mathbb{C}^n$ is the state, $u(t)\in\mathbb{C}^m$ is the input, $y(t)\in\mathbb{C}^p$ is the output. $A,B,C,D$ are matrices of suitable dimensions. The system is called SISO (single-input single-output) if $m=p=1$, MISO (multiple-input single-output) if $m>1,\;p=1$, etc. The matrices $A,B,C$ may be infinite (for example, in systems containing delay lines, or systems modeling heat propagation, or systems describing acoustic or electromagnetic waves, where $n=\infty$). The system is called <u>finite-dimensional</u> if $n$ is finite, so that the matrices $A,B,C$ are finite. $n$ is called the <u>order</u> of $\Sigma$.

The <u>transfer function</u> of $\Sigma$ is
\begin{align*}
	G(s)=C(sI-A)^{-1}B+D,\;\text{for }s\notin\sigma(A).
\end{align*} 
This is a <u>proper rational function</u>. "Rational" means that each entry in the matrix $G$ is the ratio of two polynomials, and "proper" means that $G$ tends to a finite value at infinity, $G(\infty)=D$. $G$ is called <u>strictly proper</u> if $G(\infty)=0$, i.e., $D=0$.
```{tip}
Some text that will give you readers some tips!
```