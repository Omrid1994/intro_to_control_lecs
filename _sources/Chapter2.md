# Chapter 2: Linear Time-Invariant Control Systems


A linear time-invariant (LTI) control system $\Sigma$ is given  by the
state-space equations:  

$$
		\dot{x}(t)&=Ax(t)+Bu(t),\\
		y(t)&=Cx(t)+Du(t),
$$

where $x(t)\in\mathbb{R}^n$ is the state vector, $u(t)\in\mathbb{R}^m$ is the input, $y(t)\in\mathbb{R}^p$ is the output. The matrices $A,B,C,D$ have suitable dimensions:

$$
    A\in\mathbb{R}^{n\times n},\;B\in\mathbb{R}^{n\times m},\;C\in\mathbb{R}^{p\times n},\;D\in\mathbb{R}^{p\times m}.
$$

The control system $\Sigma$ is called single-input single-output (SISO) if $m=p=1$,  multiple-input single-output (MISO) if $m>1$ and $p=1$, etc.  The value $n$ is called the **order** of $\Sigma$.

## Transfer function

Let $\hat{y}(s)$ denote the Laplace transform of the output of $\Sigma$, that is, $\hat y(s)=\int_0^\infty e^{-st}y(t)dt$.
Let $\hat{u}(s)$ denote the Laplace transform of the input of $\Sigma$.
The transfer function of $\Sigma$ is
  
```{math}
:label: eq:transfer_function
	G(s):= \frac{\hat y(s)}{\hat u(s)}=C(sI_n-A)^{-1}B+D, 
```

and this is well defined for any $s\notin\sigma(A)$, where $\sigma(A)$ denotes the set of eigenvalues of $A$.
 
Recall that the inverse of a square invertible matrix $H$ satisfies $H^{-1}=\frac{1}{\det(H)}\text{adj}(H)$, where $\text{adj}(H)$ is the adjugate matrix of $H$. Every entry of $\text{adj}(H) $ is the determinant  of an $(n-1)\times (n-1)$ submatrix of $H$. Thus, 

```{math} 
:label: eq:GS_adjugate
	G(s)=C \frac{1}{\det(s I_n-A)}\text{adj}(s I_n-A )B+D.
```

A transfer function $Q=Q(s)$ is called  rational if it is the ratio of two polynomials in $s$, so $G$ is rational. A rational transfer function $Q$ is called proper if $\lim_{s\to\infty}Q(s)$ exists and is finite, and strictly proper if this limit is zero. By {eq}`eq:GS_adjugate`, $\lim_{s\to \infty} G(s)=D$, so $G$ is proper. It is strictly proper if $D=0$. 

Write the rational transfer function $G$ as the ratio of two polynomials

$$
G(s)=\frac{N(s)}{D(s)}.
$$

Then the zeros of $G$ are the values $s$ such that $N(s)=0$, and the poles of $G$ are the values $s$ such that $D(s)=0$.

By {eq}`eq:GS_adjugate`, the  poles of $G$ are a subset of $\sigma(A)$.

The system $\Sigma$ is called minimal if there does not exist an LTI system with a smaller order than $n$ that gives the same transfer function. If the system $\Sigma$ is minimal then the  poles of $G$ are  the eigenvalues of $A$. 



````{prf:remark}
Not every transfer function is rational. For example, suppose that a system is described by the input-output relation $y(t)=u(t-\tau)$, with $\tau>0$, that is, the output is equal to the input delayed by $\tau$ seconds. 
Then

$$
    G(s) & = \frac{\hat{y}(s)}{\hat{u}(s) }\\
    &=\frac{e^{-\tau s}\hat{u}(s)}{\hat{u}(s)}\\
    &=e^{-\tau s}.
$$
````


## Stability of the LTI

The system $\Sigma$ is called **stable** if the matrix $A$ is stable (see Chapter 0).
This means that if $u=0$, then starting from an arbitrary initial state $x(0)\in\mathbb{R}^n$, the trajectory $x(t)=e^{At}x(0)$ will tend to zero as $t\to\infty$. 

Recall that $A$ is stable if the real part of every eigenvalue of $A$ is negative. Let

$$
    \mathbb{C}_- &: = \{s\in\mathbb{C}\;|\;\text{Re}(s)<0\},\\
    \mathbb{C}_+& :=\{s\in\mathbb{C}\;|\;\text{Re}(s)>0\},\\
    i\mathbb{R}&:=\{i\omega\;|\;\omega\in\mathbb{R}\}.
$$

Clearly, $\mathbb{C}=\mathbb{C}_-\cup i\mathbb{R}\cup \mathbb{C}_+$. Then $\Sigma$ is stable if and only if $\sigma(A)\subset\mathbb{C}_-$.
We mention that the LTI system $\Sigma$ is called marginally stable if $\sigma(A)\subset (\mathbb{C}_-\cup i\mathbb{R})$.

````{prf:example}
:label: example:RLC_circuit
Consider the following electrical circuit:

```{figure} images/RLC_low-pass_pure_white_bg.png
---
width: 70%
name: fig-RLC-circuit
---
RLC Circuit.
```

where $L$ is the inductance of the inductor, $C$ is the capacitance of the capacitor. Let $x_1(t):=i_L(t)$ be the current through the inductor, and let $x_2(t):=v_C(t)$ be the voltage on  the capacitor. The input is $u(t):=V_{in}(t)$, and the output $y(t)=V_{out}(t)$ is the voltage on the resistor $R_{L}$. We derive the  state-space representation of this system. We use the known properties of the electrical components: 

$$
    i_C(t)&=C\frac{d }{dt}v_{C}(t)=C\dot{x}_2(t),\\
    v_L(t)&=L\frac{d }{dt}i_L(t)=L\dot{x}_1(t).
$$

By Kirchhoff's law of voltages, $ V_{in}-v_L+v_C=0$, so $\dot{x}_1=\frac{x_2}{L}+\frac{V_{in}}{L}$.

By Kirchhoff's law of currents: $i_L+i_C+\frac{v_C}{R_L} =0 $, so $\dot x_2=- \frac{x_1}{C}-\frac{x_2}{CR_L}$.
In matrix form, we have 

$$
    \begin{bmatrix}
        \dot{x}_1 \\\dot{x}_2 
    \end{bmatrix}&=\begin{bmatrix}
        0& \frac{1}{L}\\
       - \frac{1}{C}&-\frac{1}{CR_L}
    \end{bmatrix}\begin{bmatrix}
        x_1 \\x_2 
    \end{bmatrix}+\begin{bmatrix}
        \frac{1}{L}\\0
    \end{bmatrix}u,\\
    y &=\begin{bmatrix}0&-1\end{bmatrix}\begin{bmatrix}
        x_1 \\x_2 
    \end{bmatrix}.
$$

This is in the form $\Sigma$ with $n=2$,  

$$
        A=\begin{bmatrix}
        0& \frac{1}{L}\\
        -\frac{1}{C}&-\frac{1}{CR_L}
    \end{bmatrix},\;B=\begin{bmatrix}
        \frac{1}{L}\\0
    \end{bmatrix},\;C=\begin{bmatrix}0&-1\end{bmatrix},\;D=0.
$$

Since the input and output are one-dimensional, the system is SISO. The transfer function is

$$
      G(s) 
        &=C(sI-A)^{-1}B+D\\
        &=\begin{bmatrix}0&-1\end{bmatrix} \begin{bmatrix} s& -\frac{1}{L}\\ 
                         \frac1{C} &s+\frac1{CR_L} \end{bmatrix}^{-1} \begin{bmatrix}
                             \frac1{L}\\0
                         \end{bmatrix} \\

                         &=\begin{bmatrix}0&-1\end{bmatrix} 
                         \frac{ \begin{bmatrix} s+\frac1{CR_L}&  \frac{1}{L}\\ 
                         -\frac1{C} & s \end{bmatrix} }{s^2+\frac{s}{CR_L}+\frac1{LC} } \begin{bmatrix}
                             \frac1{L}\\0
                         \end{bmatrix} \\
                         &= \frac{ \frac1{CL}}{s^2+ \frac{s}{CR_L}+ \frac1{LC}}.
$$
````

````{Admonition} Exercise
For the system in {prf:ref}`example:RLC_circuit`, what is the relation between the  poles of $G$ and $\sigma(A)$? Is the system $\Sigma$ stable?
```` 

## Routh Stability Test

The eigenvalues of $A$ can be computed numerically using  various software packages, for example MATLAB. Nevertheless, it is useful to have   simple criteria to check if $\sigma(A)\subset\mathbb{C}_-$. Recall that $\sigma(A)$ consist of the zeros of the characteristic polynomial:

$$
    p(s):=\det(sI_n-A) =s^n+a_{n-1}s^{n-1}+a_{n-2}s^{n-2}+\dots+a_1s+a_0.
$$

Since $A$ is real, the coefficients $a_j$ are real. 

A necessary (but not sufficient) condition for stability is

```{math}
:label: eq:nece_cond
  \text{If $A$ is stable, then $a_j>0$   for } j=0,\dots,n-1.
```
````{prf:remark}
If $A$ is of order $n=1$ or $n=2$, then this condition is also sufficient.    
````
 

What happens when $n>2$?  Luckily, Routh and Hurwitz worked out algorithms that are simple and can determine the stability of $A$ without computing its eigenvalues. 

Generate the following table:

$$
\begin{array}{c|cccc}
    s^n     & a_n     & a_{n-2} & a_{n-4} & \dots \\
    s^{n-1} & a_{n-1} & a_{n-3} & a_{n-5} & \dots \\
    s^{n-2}&c_1&c_2&c_3&\dots\\
    s^{n-3}&d_1&d_2&\dots&\dots\\
    \vdots  & \vdots  & \vdots  & \vdots  & \vdots\\
    s^1&j_1\\
    s^0&k_1
\end{array}
$$

If $n$ is even [odd] then the first row consists of the coefficients of all even [odd] powers, and the second row consists of the coefficients of all odd [even] powers. All other values are calculated recursively.

$$
c_1 = \frac{a_{n-1} a_{n-2} - a_n a_{n-3}}{a_{n-1}}; \quad
c_2 = \frac{a_{n-1} a_{n-4} - a_n a_{n-5}}{a_{n-1}}; \quad
c_3 = \frac{a_{n-1} a_{n-6} - a_n a_{n-7}}{a_{n-1}},
$$

$$
d_1 = \frac{c_1 a_{n-3} - a_{n-1} c_2}{c_1}; \quad
d_2 = \frac{c_1 a_{n-5} - a_{n-1} c_3}{c_1}; \quad
d_3 = \frac{c_1 a_{n-7} - a_{n-1} c_4}{c_1}.
$$

We carry on in this way, computing new rows, which get shorter and shorter. Note that the table has in total $n+1$ rows. The last row will contain only one element that is possibly non-zero.

````{prf:proposition}
:label: prop:stab_rou_necen_suff
$A$ is stable if and only if:
1. the necessary condition {eq}`eq:nece_cond` holds, and
2. all the numbers in the first column of the Routh table are positive.
````

````{prf:example}
Consider the polynomial

$$
        p(s)=s^3+a_2s^2+a_1s+a_0.
$$

The Routh table looks like:

$$
\begin{array}{c|cccc}
    s^3&1&a_1\\
    s^2&a_2&a_0\\
    s^1&b_1\\
    s^0&c_1
\end{array}
$$

with

$$
    b_1&=-\frac{a_0-a_1a_2}{a_2},\\
    c_1&=-\frac{-a_0b_1}{b_1}=a_0.
$$

Thus, we conclude that if $n=3$ then $A$ is stable if and only if

$$
    a_2>0,\;a_0>0\text{ and }a_1a_2>a_0.
$$

(Note that this implies that $a_1>0$, so the necessary condition holds).
````

If $A$ is not stable, then the Routh table gives us some information in addition to instability:

````{prf:proposition}
If $A$ is unstable and all the numbers in the first column of the Routh table are non-zero, then the number of unstable eigenvalues of $A$ (i.e. the eigenvalues in $ \mathbb{C}_+$) is equal to the number of sign variations in the first column of the Routh table.
````

````{prf:example}
Let $A=\begin{bmatrix}
        -1 &0 &0\\ 0&4&0\\0&0&3
    \end{bmatrix}$.
Note that $A$ has two unstable eigenvalues. The characteristic polynomial of $A$ is

$$
        p(s)&=\det(sI_3-A)\\
        &=(s+1)(s-4)(s-3)\\
        &=s^3-6s^2+5s+12.
$$

The Routh table in this case is

$$
\begin{array}{c|cccc}
    s^3&1& 5 \\
    s^2&-6&12\\
    s^1&7\\
    s^0&12
\end{array}
$$

so the first column includes two sign variations, as expected. 
````

For an intuitive proof of the Routh stability test, see {cite:p}`margaliot_langholz_Routh`.


## Stability of the transfer function

A transfer function $G$ is called stable if it is bounded and analytic on $\mathbb{C}_+$.
 

````{prf:proposition}
:label: prop:G_rational_Stable
If $G$ is rational, then $G$ is stable if and only if it is proper and all its poles are in $\mathbb{C}_-$.
````

````{Admonition} Exercise
Show that if $G$ has a pole on $i\mathbb{R}$, then $|G(s)|$ tends to $\infty$ if $s$ tends to this pole from the right, hence $G$ is not stable in this case.    
````

 

````{prf:proposition}
:label: prop:stable_lop
If $\Sigma$ is a stable finite-dimensional LTI system, then its transfer function is stable.
````
This follows from the fact that any pole of $G$ is an eigenvalue of the matrix $A$. 


The converse of {prf:ref}`prop:stable_lop` is not true. For example, if $A$ is unstable and $C=0$ (or $B=0$) then $G(s)=D$, so  $G(s)$ is  stable.
 
````{prf:example}
The following are stable transfer functions:
       $ \frac{s-1}{s+1}$,
       $\frac{s}{s^2+5s+7}$,
       $e^{-3s}$,
       $\frac{2s-7}{s^3+3s^2+2s+5}$,
        $\frac{(s-7)(s+3)}{(s+1)(s+7)}$,
        $\frac{1}{2s-e^{-2s}}$.
````

Here are some unstable transfer functions:

$$
        s,\;\frac{2s}{s-7},\;\frac{s+3}{s(s+7)},\;e^{2s},\;\frac{s^2+2s+2}{s+5},\;\frac{2s}{s^2+9}.
$$

Stability of $G$ has some important consequences. To explain this, recall that $u(t):\mathbb{R}_+\rightarrow\mathbb{R}^m$ has finite energy if

$$
        \int_0^\infty\big|u(t)\big|^2dt<\infty.
$$

This integral is then called the energy of $u(t)$. 

````{prf:theorem}
If $G(s)$ is a stable transfer function, $u$ is a signal with finite energy, and $y$ is a signal defined via its Laplace transform by

$$
        \hat{y}(s)=G(s)\hat{u}(s),
$$

then $y$ has finite energy. Conversely, if $G(s)$ is a transfer function with the above property, then $G(s)$ is stable.
````

````{prf:theorem}
Suppose that $\Sigma$ is SISO and that $G$ is stable. Then for $u(t)=\cos(\omega t) $ the output will converge to

$$
y_{\text{steady-state}}(t)= c \cos(\omega t+\phi ),
$$

where $c =|G(i\omega)|$, and $\phi =\text{arg}(G(i\omega))$.
````

This implies that the system <em>entrains</em> to the periodic excitation.

In particular, if we take $\omega=0$ then for the input $u(t)=\cos(\omega t)\equiv 1$ the output converges to 

$$
y_{\text{steady-state}}(t)= c \cos(\omega t+\phi )\equiv c \cos( \phi ),
$$

where $c =|G(0)|$, and is  called the <em>DC gain</em> of the system. 
 
 ## References

```{bibliography} references.bib