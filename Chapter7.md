# Chapter 7: State-Space Analysis

So far we considered linear control systems represented by their  transfer function. We now assume that the linear control system is described by a set of ordinary differential equations:


```{math}
:label: eq:state_space

\dot x(t)&=Ax(t)+B u(t),\\
y(t)&=C x(t)+D u(t).\nonumber
```

Here, $x:[0,\infty)\to \mathbb{R}^n$ is the state vector that describes the internal state of the system, $u:[0,\infty)\to\mathbb{R}^m$
is the input, and $y:[0,\infty)\to \mathbb{R}^p$ is the output. The dimensions of the matrices are then
 
$$
A\in\mathbb{R}^{n\times n},\; 
B\in \mathbb{R}^{n\times m},\; 
C\in \mathbb{R}^{p\times n},\; 
D\in \mathbb{R}^{p\times m}.
$$

An important advantage  of the state space approach is that it allows the analysis of multi-input and multi-output systems.

The solution of {eq}`eq:state_space` is

```{math}
    x(t)&= e^{At}x(0)+\int_0^t e^{A(t-s)}Bu(s)ds,\\
    y(t)&= C \left  (e^{At}x(0)+\int_0^t e^{A(t-s)}Bu(s)ds \right )+Du(t),\nonumber
```

where $e^A$ is the matrix exponential of $A$ (see Chapter 0). 

Applying a Laplace  transform to {eq}`eq:state_space` gives

$$
    s \hat x(s)-x(0)&=A \hat x (s)+B \hat u (s),\\
    \hat y(s)&=C\hat x(s)+D \hat u(s),
$$

and for $x(0)=0$ this yields

$$
\frac{\hat y(s)}{\hat u(s)}  = C (sI_n-A)^{-1} B+D,
$$

where $I_n$ is the $n\times n$ identity matrix. 


## Observability


Assume that we observe  the input and output on a time interval $[0,T]$, for some $T>0$, but we do not know $x(0)$ and thus we do not know $x(t)$ at any time $t$. A natural question  is: can we determine  $x(0)$ (and thus $x(t)$ for all $t$) based on observing $u(t),y(t)$ for $t\in[0,T]$? 

The system {eq}`eq:state_space` is called observable on the time interval $[0,T]$ if it is possible to uniquely determine $x(0)$ from observing $u(t),y(t)$ for $t\in[0,T]$. Since we assume that the input is known, it is enough to consider the system:

```{math}
:label: eq:system_obsvr

        \dot{x}(t)&=Ax(t),\\
        y(t)&=Cx(t).\nonumber
```

Note that this implies that 

```{math}
:label: eq:yt_obser
  y(t)=Ce^{At}x(0) \text{ for all } t\geq0.   
```
 
```{prf:definition}
The system {eq}`eq:system_obsvr` is called observable on the time interval $[0,T]$ if it is possible to uniquely determine $x(0)$ from   observing $ y(t)$ for $t\in[0,T]$.
```

Since the system is defined by the pair of matrices $(A,C)$,  we will sometimes use the terminology $(A,C)$ is observable rather than {eq}`eq:system_obsvr` is observable. 

Define the $L_2$ norm of the vector $y(t)\in\mathbb{R}^p$ by

$$
| y(t)  |_2 : =(|y_1(t)|^2+|y_2(t)|^2+\cdots+|y_p(t)|^2)^{1/2}.
$$

```{prf:proposition}
:label: prop:obser_y2

The system {eq}`eq:system_obsvr` is  observable on $[0,T]$ if and only if for every $x(0)\in\mathbb{R}^n$, $x(0)\neq0$, the output $y$ that corresponds to the initial state $x(0)$ satisfies

$$
    \int_0^T | y(t) |_2^2 dt>0.
$$
```

In other words, $y(t)$ is not zero on   the entire time   interval $t\in[0,T]$. 

```{prf:proof}
First assume that there exists $x(0)\in\mathbb{R}^n\setminus\{0\}$ for which $y(t)= 0$ for all $t\in[0,T]$. It follows from {eq}`eq:yt_obser` that for $x(0)=0$ we also have $y(t)=0$ for all $t\in[0,T]$, so there are two different initial conditions that produce  the same output on $[0,T]$, and thus  the system is not observable.   
Now assume that the condition in the proposition holds. Fix $a,b\in\mathbb{R}^n$, with $a\not =b$, and consider {eq}`eq:system_obsvr` with $x(0)=a$ and with $x(0)=b$. Let $y^a(t)$, $y^b(t)$ denote the corresponding outputs at time $t$. Then

$$
       y^a(t)-y^b(t)&=Ce^{At}a-Ce^{At}b\\
       &=Ce^{At} (a-b),
$$

that is, the output of the system for the initial condition $x(0)=a-b$. Since the condition in the proposition holds  and $a-b\not=0$, we conclude that $y^a(t)-y^b(t)$ is not identically zero on $[0,T]$, the output is different for any two different initial conditions. 
```

````{prf:example}
:label: exa:simp_non_obser

Consider the system

```{math}
:label: eq:unobser_simple
  \dot x_1 & =x_1-x_2,\nonumber \\
  \dot x_2&=-3 x_2 , \\
  y&=x_2.\nonumber
```
Fix $T>0$.
Consider the initial condition $x(0)=\begin{bmatrix}
1\\0
\end{bmatrix}$. Then $x_2(t)=0$ for all $t\in[0,T]$, so $y(t)=0$
for all $t\in[0,T]$. We conclude that the condition in {prf:ref}`prop:obser_y2`
does not hold, so the system is not observable. Indeed, the output only provides information on $x_2$, but $x_2$ does not depend, and thus provides no information, on $x_1$.  
````

### Kalman Rank Condition for Observability

The next result is known as the Kalman rank condition for observability, derived by 
Rudolf E. Kalman (who is well-known also for inventing the Kalman filter). To state it, we define the observability matrix of {eq}`eq:system_obsvr` as

$$
\mathcal O(A,C):= \begin{bmatrix} 
C\\ CA\\ CA^2\\ \vdots\\ CA^{n-1}
\end{bmatrix}.
$$

Note that $\mathcal{O}(A,C)$ has dimensions $(np) \times n$. 

```{prf:theorem}
The system {eq}`eq:system_obsvr` is observable if and only if
 
$$
    \text{rank}( \mathcal{O} (A,C))=n. 
$$
```


````{prf:proof}
Suppose that $(A,C)$ is not observable. Then there there exists $x_0\in\mathbb{R}^n$, $x_0\neq0$ such that $Ce^{At}x_0=0$ for all $t\in[0,T]$. Differentiating with respect to time, we obtain $CAe^{At}x_0=0$ for all $t\in[0,T]$, differentiating again we obtain $CA^2e^{At}x_0=0$ for all $t\in[0,T]$, etc. Taking now $t=0$, we obtain

$$
    Cx_0=0,\;CAx_0=0,\;CA^2x_0=0,...
$$

which implies that

$$
        \begin{bmatrix}
            C\\CA\\CA^2\\\vdots\\CA^{n-1}
        \end{bmatrix}x_0=0.
$$

This shows that the $n$ columns of this matrix are linearly dependent, hence the rank of the matrix $\mathcal{O}(A,C)$ is less then $n$. 
    
To prove the converse implication, suppose that the rank of $\mathcal{O}(A,C)$ is not $n$, hence it is $<n$, so that its columns are linearly dependent. Therefore, there exists $x_0\in\mathbb{R}^n$, $x_0\neq0$ such that

```{math}
:label: eq:obser_mat_dege

        \begin{bmatrix}
            C\\CA\\CA^2\\\vdots\\CA^{n-1}
        \end{bmatrix}x_0=0.
```

Let $p_A(s):=\det(s I_n -A)$ be the characteristic polynomial of $A$. Then, according to the Cayley-Hamilton theorem (see Chapter 0), we have $p_A(A)=0$. Thus, if 

$$
        p_A(s)=s^n+a_{n-1}s^{n-1}+\cdots+a_1s+a_0,
$$

then

```{math}
:label: eq:cay_hamil_A

        A^n+a_{n-1}A^{n-1}+\cdots+a_1A+a_0I_n=0.
```

Multiplying with $x_0$ from the right and with $C$ from the left, to get

$$
       C A^n x_0+a_{n-1} C A^{n-1}x_0+\cdots+a_1 C Ax_0+a_0Cx_0=0.
$$

and using {eq}`eq:obser_mat_dege`  implies that $CA^nx_0=0$. Now, we multiply {eq}`eq:cay_hamil_A` with $x_0$ from the right and with $CA$ from the left, obtaining $CA^{n+1}x_0=0$. By induction, we obtain that

$$
        CA^kx_0=0\text{ for all }k\in\{0,1,\dots\}.
$$

Since $y(t)=Ce^{At}x_0$ has the Taylor expansion, 

$$
        y(t)=Cx_0+tCAx_0+\frac{t^2}{2}CA^2x_0+\frac{t^3}{6}CA^3x_0+\cdots
$$

and since all the coefficients in this Taylor series are zero, as we have just shown, it follows that $y(t)=0$ for all $t\geq0$. Since the initial state $x_0\neq0$, it follows that $(A,C)$ is not observable.
````

```{prf:remark}
Note that the Kalman rank condition is independent of $T$, the length of the time interval. Thus, it does not matter how we choose $T>0$ in the definition of observability. Therefore, in the sequel, we do not say that "$(A,C)$ is observable on the  time interval $[0,T]$", but that "$(A,C)$ is observable".
```


```{prf:example}
Consider again the system {eq}`eq:unobser_simple` in {prf:ref}`exa:simp_non_obser`. In this case, $n=2$, $p=1$,  $A=\begin{bmatrix}
    1&-1\\ 0& -3
\end{bmatrix}$, and $C=\begin{bmatrix}0 & 1 \end{bmatrix}$. Thus,

$$
\mathcal{O}(A,C)=\begin{bmatrix}
    C\\CA
\end{bmatrix}=\begin{bmatrix}
    0& 1\\0&-3
\end{bmatrix}.
$$

We see that $\text{rank}(\mathcal{O}(A,C))=1<n=2$, so the system is not observable. 
```

### Kalman Canonical Form

When system {eq}`eq:system_obsvr` is  not observable   it 
can   be decomposed into an observable part and an unobservable part. Before stating it, we recall the effect of a coordinate transformation on {eq}`eq:system_obsvr`.
Let $T\in\mathbb{R}^{n\times n}$ be an invertible matrix, and define $z(t):=Tx(t) $. 
Then

$$
    \dot z &= T \dot x \\
         &= T A x\\
         &= TA T^{-1} z,
$$

and

$$
    y &= C x \\
    &= C T^{-1} z, 
$$

so we get a system in the form {eq}`eq:system_obsvr` with matrices $(TA T^{-1},CT^{-1})$. The observability matrix of the new system is

$$
\mathcal O(TA T^{-1},CT^{-1})&= \begin{bmatrix} 
CT^{-1}\\CT^{-1} TA T^{-1}\\C T^{-1} (TA T^{-1})^2\\ \vdots\\CT^{-1} (TA T^{-1})^{n-1}
\end{bmatrix}\\
&=\begin{bmatrix} 
C
\\C A \\C  A ^{2}\\ \vdots\\C
A ^{n-1}
\end{bmatrix}T^{-1}\\
&=\mathcal{O}(A,C) T^{-1}.
$$

This implies that $\text{rank}(\mathcal{O}(A,C)) = \text{rank}(\mathcal{O}(TAT^{-1},CT^{-1}))$. 

````{prf:theorem}
:label: thm:from_x_to_z

Suppose that $n_1:=\text{rank}(\mathcal{O}(A,C))<n$. Then there exists an invertible matrix $T\in\mathbb{R}^{n\times n}$ such that $z(t):=Tx(t) $ satisfies

```{math}
:label: eq:z_obser

    \dot z(t)&=\begin{bmatrix}
        \dot z_O(t)\\ \dot z_{UO}(t)
    \end{bmatrix}=\begin{bmatrix}
        \bar A_{11}&0 \\
        \bar A_{21}&\bar A_{22}
    \end{bmatrix} \begin{bmatrix}
        z_O(t)\\z_{UO}(t)
    \end{bmatrix},\nonumber\\
    y(t)&=\begin{bmatrix}
        \bar C & 0
    \end{bmatrix} 
   \begin{bmatrix}
       z_O(t)\\z_{UO}(t)
   \end{bmatrix} ,
```
with $z_O(t)\in\mathbb{R}^{n_1}$, $z_{UO}(t)\in \mathbb{R}^{n-n_1}$, and the pair $(\bar A_{11},\bar C) $ observable.  
````

Writing this explicitly gives

$$
    \dot z_O&=\bar A_{11}z_O,\\
    \dot z_{UO}&=\bar A_{21}z_O+\bar A_{22} z_{UO},\\
    y&= \bar  C z_O. 
$$

Thus, observing the output allows to determine $z_O$ (the observable part of the vector $z$), but not $z_{UO}$ (the unobservable part of $z$). 


### Popov-Belevitch-Hautus Test for Observability

Another important way to 
verify  observability is the 
Popov-Belevitch-Hautus (PBH)
test for observability.

````{prf:theorem}
(PBH Test for Observability)

Consider the system {eq}`eq:system_obsvr`.
Let $\sigma(A)$ denote the set of eigenvalues of $A$.
Then $(A,C)$ is observable if and only if

```{math}
:label: eq:pbh_test

        rank\begin{bmatrix}
            \lambda I_n-A\\
            C
        \end{bmatrix}=n,\text{ for any }\lambda\in\sigma(A).
```
````

Note that for $\lambda\not \in \sigma(A)$, the above rank is always $n$, because $\lambda I_n-A$ is invertible.

```{prf:proof}

Suppose that $(A,C)$ is not observable. Then $n_1:=\text{rank}(\mathcal{O}(A,C))<n$. 
Let $T$ be the invertible matrix in {prf:ref}`thm:from_x_to_z` and let $z(t):=Tx(t)$. Then $z$ satisfies  {eq}`eq:z_obser`. Note that
$\bar A_{22}\in\mathbb{R}^{ (n-n_1)\times(n-n_1)  }$. Let $\lambda  \in \mathbb{C}$ be an eigenvalue of $\bar A_{22}$ 
(and then also an eigenvalue of $A$). Let $v\not =0$ be the corresponding eigenvector so that $\bar A_{22}v=\lambda  v$. Then

$$
  \left(   \lambda I_n- \begin{bmatrix}
        \bar A_{11}&0 \\
        \bar A_{21}&\bar A_{22}
        \end{bmatrix}\right ) 
\begin{bmatrix}
    0\\v
\end{bmatrix} = 
\begin{bmatrix}
    0\\0
\end{bmatrix},
$$

and also

$$
\begin{bmatrix}
    \bar C & 0
\end{bmatrix}\begin{bmatrix}
    0\\v
\end{bmatrix}= \begin{bmatrix}
    0\\0
\end{bmatrix}.
$$

This implies that {eq}`eq:pbh_test` does not hold. Conversely, suppose that $\text{rank}\begin{bmatrix}
            \lambda I_n-A\\
            C
        \end{bmatrix}<n$ for some $\lambda\in\sigma(A)$. Thus, the columns of this matrix are linearly dependent, so   there exists $x_0\neq0$ such that
		
$$
            \begin{bmatrix}
                \lambda I_n-A\\
                C
            \end{bmatrix}x_0=0.
$$

It follows that $x_0$ is an eigenvector of $A$ (as $Ax_0=\lambda x_0$) and $Cx_0=0$. Hence, $e^{At}x_0=e^{\lambda t}x_0$ and therefore $Ce^{At}x_0 = e^{\lambda t} Cx_0 =0$ for all $t\geq0$. This implies  that $(A,C)$ is not observable.
```
 

```{prf:example}
Consider again the system {eq}`eq:unobser_simple` in {prf:ref}`exa:simp_non_obser`. In this case, $n=2$, $p=1$,  $A=\begin{bmatrix}
    1&-1\\ 0& -3
\end{bmatrix}$, and $C=\begin{bmatrix}0 & 1 \end{bmatrix}$. Here $\sigma(A)=\{1,-3\}$. Let $\lambda=1$. The corresponding eigenvector is $v=\begin{bmatrix}
    1\\0
\end{bmatrix}$. Note that   
$            \begin{bmatrix}
                \lambda I_2-A\\
                C
            \end{bmatrix} v  =0,
$
so the PBH test implies that the system is not observable. 
```

## Controllability


Fix an initial condition $x(0)=a$ and a control $u(t)$, $t\in[0,T]$, and let $x(t,u,a)$ be the solution of {eq}`eq:state_space` at time $t$. We then say that the control $u$ 
steers the system from $a$ to $x(t,u,a)$ in time $t$.

Assume   for a moment that $B=0$. Then clearly any control $u$ steers $x(0)=a$ to $x(T,u,a)=e^{AT} a$ in time $T$. In other words, the control  has 
no effect on the evolution of the state vector. What happens in the general case? Is the control input ``rich enough'' to drive the state vector from any initial condition to any desired final condition?

```{prf:Definition}
The system {eq}`eq:state_space` is called controllable if for any $a,b\in\mathbb{R}^n$ there exists a time $T\geq 0$ and a control $u(t)$, $t\in[0,T]$, such that for $x(0)=a$ the solution satisfies $x(T,u,a)=b$. 
```

In other words, it is possible to steer  the state from any initial condition $a$ to any desired final condition $b$ in finite
time. 

````{prf:theorem}
:label: thm:controll

The system {eq}`eq:state_space` is controllable if and only if

```{math}
:label: eq:necc_sugg_cont

 \text{rank}\begin{bmatrix}
     B&AB&\dots&A^{n-1}B
 \end{bmatrix}=n. 
```
````

We will prove this result by transforming it to the observability problem that we already addressed.

## Duality


The dual system of  the system {eq}`eq:state_space` is the control system

```{math}
:label: eq:dual

    \dot{\tilde x} &=A^\top \tilde x+C^\top \tilde u ,\nonumber \\
    \tilde y&= B^\top \tilde x+D^\top \tilde u.

````
Note that the matrix dimensions imply that $\tilde x(t) \in\mathbb{R}^n$, $\tilde u(t)\in\mathbb{R}^p$, and $\tilde y(t)\in\mathbb{R}^m$.

```{prf:theorem}
:label: thm:dula

The system {eq}`eq:state_space` is controllable if and only if the dual system {eq}`eq:dual` is observable. 
```

Note that this reduces the problem of determining controllability to the problem of determining observability. 

````{prf:proof}
First, assume that {eq}`eq:state_space` is not controllable. Fix $T>0$. We may assume that $x(0)=0$, and then

$$
x(T)=\int_0^T e^{A(t-s)}B u(s) ds. 
$$

Define

$$
    R(T)&:= \{z | \text{ there exits a control } u \text{ that steers } x(0)=0 \text{ to }  x(T)=z \}\\
    &= \{z | \text{ there exits a control } u \text{ such that }
    z=\int_0^T e^{A(t-s)}B u(s) ds\}.
$$


It is not difficult to show that $R(T)$ is a linear subspace. 
Since {eq}`eq:state_space`
is not controllable, $R(T) \not =\mathbb{R}^n$, 
so there exists a vector $p\in\mathbb{R}^n$, with $p\not =0$ such that $p^\top z =0 $ for any $z\in\mathbb{R}(T)$. In other words, for any control $u$ we have

$$
    0 &= p^\top \int_0^T e^{A(t-s)}B u(s) ds\\
    &= \int_0^T u^\top(s) B^\top e^{A^\top (t-s)}  ds \;  p. 
$$

Defining a new integration variable $\tau:=T-s$, we have that 
for any control $u$ 

$$
    0  = \int_0^T u^\top(T-\tau) B^\top e^{A^\top \tau}  d\tau  \;  p. 
$$

Consider now the specific  control

$$
u(T-\tau):=B^\top e^{A^\top \tau} p,\quad \tau\in[0,T].
$$

Then

$$
    0  = \int_0^T  (B^\top e^{A^\top \tau} p)^\top  B^\top e^{A^\top \tau} p d \tau, 
$$

that is,

 $$
 B^\top e^{A^\top \tau}p=0  \text{ for any } \tau\in[0,T].
 $$
 
We will show that this implies that the dual system is not observable. It is enough to consider the system

```{math}
:label: eq:dual_short

    \dot{\tilde x} &= A^\top \tilde x,\nonumber\\
    \tilde y &= B^\top \tilde x. 
```
Fix $\tilde x(0)=p$ and recall that $p\not =0$. Then

$$
     \tilde y(t) & = B^\top e^{A^\top t} \tilde x(0)\\
     & = B^\top e^{A^\top t}   p
     \\&=0, \text{ for all } t\in[0,T],
$$

so the dual system is not observable. 
Thus, we showed that: 

system  {eq}`eq:state_space`  is not controllable implies that the dual system  {eq}`eq:dual`  is not observable.


Now assume that the dual system \eqref{eq:dual} is not observable.  Then there exists $p\in\mathbb{R}^n$, with $p\not =0$, such that

$$
B^\top e^{A^\top t} p =0 \text{ for all } t\in [0,T]. 
$$

This implies that for any control $u$, we have

$$
0=\int_0^T u^\top (T-\tau) B^\top e^{A^\top \tau} p d\tau,
$$

and we already saw that this implies that for any control $u$ we have 

$$
0= p^\top \int_0^T 
e^{A  (T-s)} 
 Bu(s) ds .
$$

This implies that {eq}`eq:state_space` is not controllable. Thus, we showed
that:


the dual system  {eq}`eq:dual` is not observable implies that the
system  {eq}`eq:state_space` is not controllable.


This completes the proof of {prf:ref}`thm:dula`.
````

Using duality, we can now prove {prf:ref}`thm:controll`. Indeed, {eq}`eq:state_space` is controllable iff the dual system {eq}`eq:dual` is observable iff the Kalman observability condition holds for {eq}`eq:dual_short`, that is, iff

$$
\text{rank} \begin{bmatrix}
    B^\top \\ B^\top A^\top \\ \vdots\\
    B^\top(A^\top)^{n-1}
\end{bmatrix}=n,
$$

and applying a transpose to this condition implies that {eq}`eq:state_space` is controllable iff {eq}`eq:necc_sugg_cont` holds. 

Using duality and the PBH test for observability yields the following result.

```{prf:proposition}
(PBH test for controllability) The pair $(A,B)$ is controllable if and only if 

$$
     \text{rank}\begin{bmatrix}
         \lambda I_n-A & B
     \end{bmatrix}=n \text{ for any }\lambda\in\sigma(A). 
$$
```


```{prf:example}
Consider the system {eq}`eq:state_space` with $m=p=1$,
 
$$
A=\begin{bmatrix}
    a_1&0&0&\dots&0&0 \\
    0&a_2&0& \dots&0&0 \\
    &&\vdots\\
    0&0&\dots&0&0&a_n
\end{bmatrix},\;B=\begin{bmatrix}
    1\\1\\\vdots\\1
\end{bmatrix},\;C\in \mathbb{R}^{n\times 1}, \;D\in\mathbb{R}^{1\times 1},
$$

and with $a_i\not = a_j$ for any $i\not =j$.

Then $\sigma(A)=\{a_1,\dots,a_n\}$. Note that

$$
     \text{rank}\begin{bmatrix}
         a_1 I_n-A & B
     \end{bmatrix}&=   \text{rank} \begin{bmatrix}0&0&0&\dots&0&0 &1\\
    0&a_1-a_2&0& \dots&0&0 &1\\
    &&\vdots\\
    0&0&\dots&0&0&a_1-a_n&1
\end{bmatrix} =n.
    
$$

A similar argument shows that the PBH test for controllability holds for any $\lambda=a_i$, so the system is controllable. 
```



## Detectability

Observability has nothing to do with stability. For example, the scalar system

$$
    \dot x_1&=a x_1,\\
    y&=x_1
$$

is always observable, but it may be stable or unstable depending on the sign of $a$. We now define a weaker notion than observability, called detectability.  

````{prf:Definition}
:label: def:detectable

The system {eq}`eq:system_obsvr` is called detectable if $y(t)=0$ for all $ t\geq 0$ implies that

```{math}
:label: eq:contoze
 \lim_{t\to\infty}x(t)= 0 .
```
````

Intuitively speaking, a system is detectable if the unobservable modes are stable. 
  
Recall that $y(t)=0$ for all $t\geq0 $ certainly holds when $x(0)=0$ and then also $x(t)=0$ for all $t\geq 0$. 
Thus, detectability implies that when $y(t)=0$ for all $t\geq0 $ we may not be able to uniquely determine the initial condition $x(0)$, but
we will be able to conclude the stability condition {eq}`eq:contoze`.

````{prf:example}
:label: exa:detect

Consider the system

$$
        \dot x&=\begin{bmatrix}
            3&0\\5&-2
        \end{bmatrix}x, \\
        y&=\begin{bmatrix}
            1&0
        \end{bmatrix}x. 
$$

Here $n=2$, $p=1$,  $A=\begin{bmatrix}
            3&0\\5&-2
        \end{bmatrix}$, and $C=\begin{bmatrix}
            1 &0
        \end{bmatrix}$. 
Then

```{math}
:label: eq:xintihse

    x(t)&= e^{At}x(0)\nonumber \\
        &=
\begin{bmatrix}
    e^{3t}& 0\\
    e^{3t}-e^{-2t} &e^{-2t} 
    \end{bmatrix}x(0) \nonumber \\
    &= \begin{bmatrix}
    e^{3t}x_1(0)\\
    (e^{3t}-e^{-2t})x_1(0)+ e^{-2t}x_2(0) 
    \end{bmatrix} , 
```
and

$$
         y(t)&=C  x(t)\\
    &=e^{3t}x_1(0). 
$$

Suppose that $y(t)=0$ for all $t\geq 0$. Then $x_1(0)=0$, and {eq}`eq:xintihse` yields
$x(t)=\begin{bmatrix}
     0\\
     e^{-2t}x_2(0) 
    \end{bmatrix}$,
so $\lim_{t\to\infty} x(t)=0$. Thus, the system is detectable. 
````





The next result is easy to establish.

```{prf:lemma}
If {eq}`eq:system_obsvr` is observable then it is detectable. 
```

An important advantage of the PBH test for observability is that it can be modified to a test for detectability. 



````{prf:theorem}
(PBH Test for Detectability)

Consider the system {eq}`eq:system_obsvr`.
Let $\sigma(A)$ denote the set of eigenvalues of $A$. Then $(A,C)$ is detectable if and only if

```{math}
:label: eq:pbh_test_detect
        rank\begin{bmatrix}
            \lambda I_n-A\\
            C
        \end{bmatrix}=n,\text{ for any }\lambda\in\sigma(A) \text{ with }
        \text{Re}(\lambda)\geq  0.
```
````

```{prf:example}
Consider again  the system in {prf:ref}`exa:detect`. In this case, $\sigma(A)=\{3,-2\}$, so we need to check {eq}`eq:pbh_test_detect` only for $\lambda=3$, that is, to compute
 
$$

\text{rank} \begin{bmatrix}
3 I_2-A\\
C
\end{bmatrix} &=\text{rank} \begin{bmatrix}
0&0\\
-5&1\\1&0 
\end{bmatrix}  
    =2,
$$

so the system is detectable. 
```


## Stabilizability

Consider the system:

```{math}
:label:  eq:stbiliz

\dot x(t)=Ax(t)+Bu(t),
```

with $A\in\mathbb{R}^{n\times n}$ and $B\in\mathbb{R}^{n\times m}$. Suppose that we have access to the entire state-space vector and we design a controller by

$$
u(t)=Fx(t)
$$

with a matrix $F\in\mathbb{R}^{ m\times n}$. The closed-loop system is

$$
    \dot x&= A x+B F x\\
    &=(A+BF)x.
$$


```{prf:definition}
:label: def:stabiliz

The system {eq}`eq:stbiliz` is called stabilizable if there exists a matrix $F\in\mathbb{R}^{ m\times n}$ such that $A+BF$ is stable
(that is, every eigenvalue of $A+BF$ has a negative real part).
    
```

If $A$ is stable then clearly $(A,B)$ is stabilizable (just take $F=0$). If $A$ is not stable then stabilizability implies that there exists  a linear feedback controller
that makes the system's unstable modes stable.

```{prf:example}
Consider {eq}`eq:stbiliz` with $A=\begin{bmatrix}
        -2&3\\5&6
    \end{bmatrix}$ and $B=\begin{bmatrix}
        2\\-1
    \end{bmatrix}$. Let $F:=\begin{bmatrix}
        -116&-222
    \end{bmatrix}$. Then
    $A+BF=\begin{bmatrix}
        -234 & -441\\
   121  & 228
    \end{bmatrix}$, and this is stable, so $(A,B)$
is  stabilizable.
```

```{prf:proposition}
The system {eq}`eq:stbiliz` is stabilizable if and only if for any $x(0)\in\mathbb{R}^n$ there exists a control $u:[0,\infty)\to\mathbb{R}^m$, with $\lim_{t\to\infty}u(t)=0$, such that 

$$
    \lim_{t\to\infty}x(t)=0. 
$$
	
```

In other words, for any initial condition there exists 
a control function that steers the state to zero and, moreover, this control function also goes to zero. 

```{prf:proof}

We prove only one implication. Suppose that the system is 
stabilizable. Then there exists $F\in\mathbb{R}^{m\times n}$ such that $A+BF$ is stable. Fix $x(0)\in\mathbb{R}^n$. 
Define $u(t):=Fx(t)$.
Then $\lim_{t\to\infty}x(t)=0$ and thus

$$
\lim_{t\to\infty}u(t)= \lim_{t\to\infty}Fx(t)=0.
$$

```


Using duality yields  the following result. 

```{prf:theorem}
The pair $(A,C)$ is detectable if and only if the pair $(A^\top,C^\top)$  is stabilizable.  
```

Combining this with {prf:ref}`def:stabiliz` yields the following  result.
 
```{prf:proposition}
Let $A\in\mathbb{R}^{n\times n}$ and $C\in\mathbb{R}^{p\times n}$. The pair $(A,C)$ is detectable if and only if there exists $H\in\mathbb{R}^{n\times p} $ such that $A+HC$ is stable. 
```


```{prf:proof}
    The pair $(A,C) $ is detectable iff the pair $(A^\top,C^\top)$ is stabilizable  iff there exists a matrix $F\in\mathbb{R}^{p\times n}$ such that $A^\top+ C^\top F$ is stable iff there exists a matrix $F\in\mathbb{R}^{p\times n}$ such that $A+F^\top C$ is stable. 
```

## Observers

Consider the system {eq}`eq:state_space`. A (full state)  observer is another system that receives the input $u$
and output $y$ of {eq}`eq:state_space` and computes an estimate $x_e$ of the state $x$ such that

```{math}
:label: eq:zero_err

\lim_{t\to\infty} |x_e(t)-x(t) | =0 
```

for any $u$ and any $x(0)$ (see {numref}`fig:observer`). 

```{figure} images/observer.png
---
width: 90%
name: fig:observer
---
An observer.
```


```{prf:theorem}
The system {eq}`eq:state_space` admits an observer that satisfies {eq}`eq:zero_err` if and only if $(A,C)$ is detectable.
```

````{prf:proof}
Suppose that $(A,C) $ is not detectable. Consider the control $u(t)=0$ for all $t\geq 0$. For $x(0)=0$ we have that $y(t)=Cx(t)=0 $ for all $t\geq 0$. Since $(A,C) $ is not detectable, {prf:ref}`def:detectable` implies that there exists an initial condition $p$ such that for $x(0)=p$ we have $y(t)=0$  for all $t\geq 0$ and 
{eq}`eq:contoze` does not hold. Thus, $p\not =0$. We conclude that there are two cases: (1) $x(0)=0$, $u(t)=0$ for all $t \geq 0 $;
and 
(2) $x(0)=p\not =0 $, $u(t)=0$ for all $t \geq 0 $ and in both cases the output is identically zero. Thus, no observer will be able to distinguish between these two cases, so it is impossible to achieve {eq}`eq:zero_err`.

To prove the converse implication, suppose that $(A,C) $ is detectable. Then there exists $H\in \mathbb{R}^{n\times p}$ such that $A+HC$ is stable. We claim that

```{math}
:label: eq:lun_obser

\dot x_e = (A+HC)x_e +(B+HD)u-Hy
```
is an observer. First note that realizing $x_e$ requires only the signals $u$ and $y$. Second, let $e(t):=x_e(t)-x(t)$, that is, the estimation error. Then

$$
    \dot e& = \dot x_e -\dot x \\
    &= (A+HC)x_e +(B+HD)u-Hy-(Ax+Bu)\\
    &=(A+HC)x_e +(B+HD)u-H(Cx+Du) -(Ax+Bu)\\
    &=(A+HC)(x_e-x)\\
    &=(A+HC)e. 
$$

Since $A+HC$ is stable, this implies that $\lim_{t\to \infty}e(t)=0$, for any $x(0)$, $x_e(0)$,  and control $u$, and this completes the proof. 
````

The observer in {eq}`eq:lun_obser` was invented  by David Gilbert Luenberger who was a professor at Stanford University.
 

## Observer-based Controllers

Consider the system {eq}`eq:state_space`. If $(A,B)$ is stabilizable then there exits a matrix $F$ such that $A+BF$ is stable, so the state-feedback control $u=Fx$ stabilizes the system.  If $x$ is not available   to the controller, and $(A,C)$
is detectable then we can try to replace $u=Fx$ by $u=Fx_e$, where $x_e$ is the output of a state observer. 
This yields the scheme in {numref}`fig:observer_based`. 


```{figure} images/observer_based_control.png
---
width: 90%
name: fig:observer_based
---
Observer-based control.
```

Then

$$
    \dot x & =Ax+Bu\\
    &=Ax + B F x_e \\
    &=(A+BF)x+ BF e,
$$

with $A+BF$ a stable matrix. The closed-loop system is described by

$$
    \begin{bmatrix} \dot x \\
    \dot e \end{bmatrix}& =\begin{bmatrix}
        A+BF&BF\\0&A+HC
    \end{bmatrix}\begin{bmatrix}  x \\
     e \end{bmatrix}.
$$

The block-triangular structure of the matrix implies that

$$
\sigma (\begin{bmatrix}
        A+BF&BF\\0&A+HC
    \end{bmatrix})=\sigma ( 
        A+BF )
    \cup \sigma ( A+HC
     )
$$

and since $A+BF$ and $A+HC$ are stable, the closed-loop system is stable. The above decomposition of the eigenvalues of the closed-loop system eigenvalues into the sets $\sigma ( 
        A+BF )$ and
    $\sigma ( A+HC
     )$ is called the separation principle, and it implies that we can design the controller and the observer independently. 
     