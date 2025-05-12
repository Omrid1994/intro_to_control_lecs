# Chapter 5: Root Locus Plots

Consider the standard feedback configuration with plant $P$ and controller $C$, with sensitivity $S=(1+PC)^{-1}$. We often want to know how the poles of $S$ would change if we changed one of the gain parameters in the controller. 

To investigate this problem, write:

$$
    P(s)C(s)=k\frac{n(s)}{d(s)}.
$$

with

$$
    n(s)&=s^w+b_{w-1}s^{w-1}+\dots+b_1s+b_0,\\
    d(s)&=s^m+a_{m-1}s^{m-1}+\dots+a_1s+a_0,
$$

where $b_j$ and $a_j$ are real coefficients,  and $m\geq w$. Note that we assume that both $n$ and $d$ are monic polynomials. Then

```{math}
:label: eq:sasdandn
    S(s)=\frac{d(s)}{d(s)+kn(s)},
```

so the problem described earlier is equivalent to plotting the roots of 

```{math}
:label: eq:dkns
d(s)+kn(s)=0
```

as a function of $k$. Such a plot, for either   all $k>0$ or  for  all $k<0$ is called  **the root locus of $\frac{n}{d}$**. 
A key point is the fact that the roots of {eq}`eq:dkns` in the complex plane  are continuous functions of $k$.

We begin with a simple example where we have a closed-form expression for the location of the roots.

````{prf:example}
:label: exa:canonic_RL

Consider the case where 

```{math}
:label: eq:lec5_ex1
        \frac{n(s)}{d(s)}=\frac{s+3}{s(s+2)}.
```

Then $d(s)+kn(s)=s^2+(2+k)s+3k$, so the poles of $S$ are

$$
  s_{1}(k)=\frac{-(2+k) +  \sqrt{k^2-8k+4}}{2},\quad 
  s_{2}(k)=\frac{-(2+k) -  \sqrt{k^2-8k+4}}{2}.
$$

The Root Locus plot for $k>0$ is:

```{figure} images/rec5_ex1_positivek.png
---
width: 90%
name: fig:RLEX1POSITIVE
---
Root locus of {eq}`eq:lec5_ex1` for $k>0$.
```

The Root Locus plot for $k<0$ is:

```{figure} images/rec5_ex1_negativek.png
---
width: 90%
name: fig:RLEX1NEGATIVE
---
Root locus of {eq}`eq:lec5_ex1` for $k<0$.
```

````


## Rules for Plotting the Root Locus

In 1942, W. R. Evans worked out an ingenious  list of  rules  that enable an engineer to construct the root locus plots, based on the polynomials $n$ and $d$, without using a computer. Learning and applying all these rules requires a lot of effort and training, but it is   less relevant today, because a computer can plot the root locus of $\frac{n}{d}$ quickly  and accurately (all the plots in this chapter were generated using Matlab's ``rlocus'' command). Thus, we shall present here only $6$ rules and some examples, which would enable the student to draw  the shape of the root locus plot for simple systems. 
We first describe  these $6$ rules and demonstrate each one using {prf:ref}`exa:canonic_RL`.

 
### Rule $1$: Number of branches

The root locus of $\frac{n}{d}$ has $m$ branches, where $m$ is the degree of the polynomial $d$. In other words, for each value of $k$, $S$ has $m$ poles. These poles are distributed symmetrically with respect to the real axis $\mathbb{R}$. 

Indeed this is clear from

$$
    S=\frac{d}{d+kn},
$$

which shows that the poles of $S$ are the zeros of the polynomial $d+kn$ and the fact that $m\geq w$.

In {prf:ref}`exa:canonic_RL` we have  $w=1$ and $m=2$, so the plot includes two branches. 

### Rule $2$: Locus on real axis

For $k>0$, a real point $s\in\mathbb{R}$ is included in the root locus plot if and only if the number of real poles and zeros of $n/d$ to the right of $s$ is odd. 

For $k<0$, a real point $s\in\mathbb{R}$ is included in the root locus plot if and only if the number of real poles and zeros of $n/d$ to the right of $s$ is even. 
    
A double pole (or a double zero) is counted as two poles (or zeros). 

We will explain this rule for the case $k>0$ (the case $k<0$ is similar).  If $s $ is on the plot then $d(s )+kn(s  )=0$ or

```{math}
:label: eq:-knd
    -k=\frac{d(s)}{n(s)}.
```

This is equivalent to

```{math}
:label: eq:180cond
 180^\circ = \angle \frac{d(s)}{n(s)}=  \angle \frac{(s-p_1)\dots(s-p_m)}{(s-z_1)\dots(s-z_m)},  
```

where $z_1,\dots,z_m$ are the roots of $n$, and $p_1,\dots,z_w$ are the roots of $d$. Now suppose that $s$ is a real point. Then any  complex zero of $n$ or $d$ appears with a complex conjugate and together they contribute zero degrees to $\angle \frac{d(s)}{n(s)}$. A real $p_i$ gives

$$
\angle (s-p_i)= \begin{cases} 
 0 ^\circ , & p_i \text{ is on the left of } s ,\\
 180^\circ , & p_i \text{ is on the right of } s ,
 \end{cases}
$$

and similarly for any real $z_i$. We conclude that {eq}`eq:180cond` holds if and only if there is an odd number of poles or zeros of $\frac{n}{d}$ to the right of $s$. 

Note that every real point is on the root locus of $\frac{n}{d}$, either on the plot for $k>0$ or on the plot for $k<0$. 

In {prf:ref}`exa:canonic_RL` the real poles and zeros of $\frac{n}{d}$ are: $-3$, $-2$, and $0$. For $k>0$, the RL plot includes the points in $(-2,0)\cup (-\infty,-3)$. For $k<0$, the RL plot includes the points in $(-3,-2)\cup (0,\infty)$.

### Rule $3$: Starting and ending points of root locus

The root locus starts for $k=0$ at the poles of $\frac{n}{d}$. For $|k|\to \infty$ it ends either at zeros of $n/d$ or at an infinite distance from the origin. 

To explain this rule, note that for $k=0$, $d(s)+kn(s)=0$ becomes $d(s)=0$, so the roots are the roots to $d$.

When $|k|\to \infty$, Eq. {eq}`eq:-knd` implies that $s$ is a zero of $n$  but if the number of branches $m$ is larger than $w $ then we must also have $m-w$ branches such that $|s|\to\infty$. Consider

```{math}
:label: eq:lim_s_inf
    \lim_{|s|\to \infty }\frac{n(s)}{d(s)} & =
    \lim_{|s|\to \infty }\frac{\prod_{i=1}^w (s-z_i) }{\prod_{j=1}^m (s-p_j)}\nonumber  \\
    &\approx \frac{1}{s^{m-w}}.
```

Thus, {eq}`eq:-knd` becomes

$$
-k\approx s^{m-w}. 
$$

When $k\to \infty$ this gives

$$
|s^{m-w}|\to \infty, \quad \angle s^{m-w}= 180^\circ  (1+2 h) \text{ with } h=0,\pm1,\pm2,\dots,
$$

that is, $|s|\to \infty$, with angles $ \angle s=\frac{ 180^\circ  (1+2 h) }{m-w}$, with $h=0,\pm1,\pm2,\dots$. 

When $k\to -\infty$, we get 

$$
|s^{m-w}|\to \infty, \quad \angle s^{m-w}= 180^\circ  ( 2 h  )\text{ with } h=0,\pm1,\pm2,\dots,
$$

that is, $|s|\to \infty$, with angles $ \angle s=\frac{ 180^\circ   ( 2 h)  }{m-w}$, with $h=0,\pm1,\pm2,\dots$. 

 
In {prf:ref}`exa:canonic_RL` this rule implies that the plot starts for $k=0$ at the poles $0$, $-2$,  and ends at the single zero $-3$ and at $-\infty$ for $k\to \infty $ [$+\infty$ for $k\to-\infty$].

### Rule $4$: Angle of asymptotes

The $m-w$ poles of $S$ that tend to $\infty$ do so along $m-w$ straight asymptotes. The angles of these asymptotes are

$$
    \frac{  180^\circ}{m-w}\ell,
$$

where $\ell$ are odd numbers if $k>0$, and $\ell$ are even numbers if $k<0$.

For example, if $m-w=1$ and $k>0$, then there will be only one asymptote, the negative real axis. If $m-w=3$ and $k>0$, then the angles of the asymptotes will be $60^\circ$, $180^\circ$, and $300^\circ$. Note that the angle between two adjacent asymptotes is always $\frac{360^\circ}{m-w}$.

In {prf:ref}`exa:canonic_RL` we have $w=1$ and $m=2$, so $m-w=1$ and there will be a single asymptote with angle

$$
\begin{cases}
    180^\circ, &\text{if } k>0,\\
    0^\circ, &\text{if } k<0.
\end{cases}
$$
 
### Rule $5$: Centroid of asymptotes

All the asymptotes of the root locus meet in one point $\gamma$ on the real axis, given by

$$
    \gamma=\frac{\sum_{j=1}^m p_j-\sum_{j=1}^wz_j}{m-w},
$$

where $p_1,p_2,...,p_m$ are the poles of $\frac{n}{d}$, and $z_1,z_2,...,z_w$ are the zeros of $\frac{n}{d}$.

To derive this rule, we improve the accuracy of the calculation in {eq}`eq:lim_s_inf` as follows: 

```{math}
:label: eq:nudpo
    \lim_{|s|\to \infty }\frac{n(s)}{d(s)} & =
    \lim_{|s|\to \infty }\frac{\prod_{i=1}^w (s-z_i) }{\prod_{j=1}^m (s-p_j)}\nonumber  \nonumber\\
    &\approx \frac{s^w-s^{w-1}\sum_{i=1}^w z_i}{s^m-s^{m-1}\sum_{j=1}^m p_j}\nonumber \\
    &=  \frac{1-s^{-1}\sum_{i=1}^w z_i}{s^{m-w}-s^{m-w-1}\sum_{j=1}^m p_j}.
```

Using the identity $1-x=\frac1{1+x}-\frac{x^2}{1+x}$, we get   that for $x\approx 0$ we have $1-x\approx\frac1{1+x}$. Applying this to the numerator of {eq}`eq:nudpo` yields 

$$
	\lim_{|s|\to \infty }\frac{n(s)}{d(s)} \approx  \frac1{(s^{\beta }-s^{\beta -1}\sum_{j=1}^m p_j)(1+s^{-1}\sum_{i=1}^w z_i)}.
$$

where $\beta:=m-w$. Keeping only the two higher-order terms in the dominator gives

$$
    \lim_{|s|\to \infty }\frac{n(s)}{d(s)} 
    \approx  \frac1{s^{\beta}-\alpha s^{\beta -1} }.
$$

where $\alpha:=\sum_{j=1}^m p_j-\sum_{i=1}^w z_i$. Using the fact that

$$
(s-\sigma)^\beta=s^\beta-\beta \sigma s^{\beta -1}+...
$$

yields

$$  
    \lim_{|s|\to \infty }\frac{n(s)}{d(s)} 
    \approx  \frac1{ (s-\frac{\alpha}{\beta})^\beta}.
$$

Thus, for $|s|\to\infty$, Eq. {eq}`eq:-knd` becomes

$$
-k\approx (s-\frac{\alpha}{\beta})^\beta . 
$$

This is the equation for a set of vectors that intersect the real axis at the point $ \frac{\sum_{j=1}^m p_j-\sum_{i=1}^w z_i}{m-w}$.

### Rule $6$: Location of break points

If $z\in\mathbb{C}$ is a point on the root locus where two or more branches  come together, then

```{math}
:label: eq:dnzero
  0=  d'(z)n(z)-n'(z)d(z).
```

In {prf:ref}`exa:canonic_RL`, we have $n(s)=s+3$, $d(s)=s(s+2)$, so $n'(s)=1$,  $d'(s)=2s +2$ and {eq}`eq:dnzero` yields

$$
0=(2s+2)(s+3)- s(s+2)=s^2+6s+6. 
$$

Thus,   break points (if they exist) must be  located at $-3+\sqrt{3} \approx    -1.268 $ and $-3-\sqrt{3}\approx  -4.732$ (see {numref}`fig:RLEX1POSITIVE`).

To derive an intuitive explanation of this rule, note that differentiating {eq}`eq:-knd` with respect to $s$ gives

$$
-\frac{dk}{ds}=\frac{d'(s)n(s)-n'(s)d(s)}{n^2(s)},
$$

so

$$
-n^2(s)=(d'(s)n(s)-n'(s)d(s))\frac{ds}{dk}.
$$

At a point $s\in\mathbb{C}$ where two or more branches meet, we have that $ds/dk$ is not well-defined, so we must have that $d'(s)n(s)-n'(s)d(s)=0$.
 
Usually we apply rule $6$ for two poles meeting on the real axis. We have two possible situations: 

```{figure} images/break_in_point.png
---
width: 90%
name: fig:P_D
---
Break-in point.
```

```{figure} images/break_out_point.png
---
width: 90%
name: fig:P_D
---
Break-out point.
```

```{prf:remark}
The root locus curves never intersect each other. In other words, if a point $z$ is on the root locus curves for some $k\in\mathbb{R}$, then this point cannot belong to the root locus curves for any other value $k\in\mathbb{R}$. This is clear from the formula $k=-\frac{d(z)}{n(z)}$, which determines a unique $k$ for $z$. Thus we cannot have loops or intersections. 
```

## Examples of Root Locus Plots

````{prf:example}

Consider

```{math}
:label: eq:exa1rl
    \frac{n(s)}{d(s)}=\frac{1}{(s-p_1)(s-p_2)}, \text{ with }  p_2<p_1<0.
``` 
	
We generate a root locus plot for $k>0$.

```{figure} images/RL_example_1.png
---
width: 90%
name: fig:P_D
---
Root locus of {eq}`eq:exa1rl` for $k>0$.
```

Note that the meeting point of the asymptotes $\gamma=\frac{p_1+p_2}{2} $ coincides with the break-away point.
````

````{prf:example}
Consider

```{math}
:label: eq:rk12
    \frac{n(s)}{d(s)}=\frac{1}{s(s-p_1)(s-p_2)} \text{ with } p_2<p_1<0.
```

We generate a root locus plot for $k>0$.

```{figure} images/RL_example_2.png
---
width: 90%
name: fig:P_D
---
Root locus of {eq}`eq:rk12` for $k>0$.
```

According to Rule $5$:

$$
    \gamma=\frac{p_1+p_2}{3}.
$$

In this case

$$
    d(s)=s^3-(p_1+p_2)s^2+p_1p_2s,\quad n(s)=1.
$$

By Rule 6,  break-away point is the solution of $d'(s)=0$, that is, 

$$
 3s^2-2(p_1+p_2)s+p_1p_2=0,
$$

and this  lies in the interval $[p_1,0]$. (The other solution of this equation is in the interval $[p_2,p_1]$ and it represents the break-away point of the root locus curve for $k<0$.)
````

````{prf:example}

Consider

```{math}
:label: eq:exa3rl
    \frac{n(s)}{d(s)} =     \frac{s-z}{s(s-p)} \text{ with } z<p<0. 
```

We generate a root locus plot for $k>0$.

```{figure} images/RL_example_3.png
---
width: 90%
name: fig:P_D
---
Root locus of {eq}`eq:exa3rl` for $k>0$.
```

Note that there is only one asymptote, one break-away point and one break-in point. We remark that the non-real part of the root locus is a circle.
````

````{prf:example}
Consider

```{math}
:label: eq:rlanexa
        \frac{n(s)}{d(s)}=\frac{s}{s^2+a^2} \text{ with } a>0 . 
```
	
We generate a root locus plot for $k>0$.

```{figure} images/RL_example_4.png
---
width: 90%
name: fig:P_D
---
Root locus of {eq}`eq:rlanexa` for $k>0$.
```
````

The root locus plot can also be used to derive  theoretical results. The next exercise demonstrates this. 

````{admonition} Exercise
Consider a plant with transfer function

$$
    P(s)=\frac{m}{s^2(s-p)} \text{ with } p<0,\; m>0.
$$
	
Show, using root locus techniques, that we cannot stabilize this plant with a P or with a PI controller, no matter how we choose the coefficients. However, we can stabilize the plant with a PD controller,

$$
    C(s)=K_p(s-z),
$$
	
where $p<z<0,\;k_p>0$. Draw the root locus plot for the feedback connection of $P$ and $C$, using $k=K_pm$ as the parameter of the curves. Apply the six rules to approximate the root-locus plot. 
````


## Root locus with  Several Parameters

If the controller has several parameters and we only want to investigate the change of the poles of $S$ as one of these parameters changes, we can usually reduce this to a standard root locus problem by rearranging the block diagram. For example, if $C$ is a PI controller,

$$
    C(s)=K_p+\frac{K_i}{s},
$$

and we want to see the effect of $K_i$ on the poles of $S$, then we can rearrange our feedback system like this:

```{figure} images/RL_sys1.png
---
width: 90%
name: fig:P_D
---
Possible pole locations for $G(s)$
```

Here we took $d=0$, and defined $\tilde{P} : =\frac{P}{1+K_p P}$. This system is not equivalent to the previous one in the sense that its sensitivity $\tilde{S}(s)=\big(1+\tilde{P}(s)\frac{K_i}{s}\big)^{-1}$ is not equal to $S$. However, the poles of $\tilde{S}$ and $S$ are the same (verify this!).
