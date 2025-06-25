# Chapter 4: PID Controllers

In this chapter, we discuss PID (proportional-integral-derivative) controllers.

## PI  Controllers

We have seen   that  in order to eliminate the steady-state error for a constant reference $r$ (or constant disturbance $d$), the controller $C$ should have a pole at $s=0$. A PI  (proportional-integral) controller has the transfer function

\begin{align*}
    C(s)=K_p+\frac{K_i}{s},\quad K_p,K_i\in\mathbb{R},
\end{align*}

where $K_p$ is the proportional term, and $\frac{K_i}{s}$ is the integral term. The constants $K_p$ and $K_i$ must be tuned according to the plant and the control objectives. In the time domain, if $e(t)$ denotes the error signal and $v(t)$ denotes the controller output, then

\begin{align*}
    v(t)=K_pe(t)+K_i\int_0^t e(\tau)d\tau.
\end{align*}

Such controllers are used to combine the advantages of proportional and of integral controllers. Since there are two parameters to tune, we have more freedom of choice and can achieve better performance.
Since $C$ has a pole at zero, if the feedback system is stable then the  steady-state error corresponding to step reference and disturbance signals will be  zero. 

For concreteness, we now study in detail the case where  the plant is a first order system:

\begin{align*}
    P(s)=\frac{k}{1+Ts} . 
\end{align*}

Then the loop-gain is

\begin{align*}
    P(s)C(s)=\frac{k(K_i+K_ps)}{s(1+Ts)},
\end{align*}

```{figure} images/PI_CLOSED_LOOP.png
---
width: 90%
name: fig:1order
---
Closed-loop system for PI controller and a first order plant.
```
and the sensitivity $S=(1+PC)^{-1}$ is  

```{math}
:label: eq:sense_p1p2
    S(s)=\frac{s(1+Ts)}{Ts^2+(1+kK_p)s+kK_i}.
```

As expected, we have $S(0)=0$, so that the steady state error is zero. Note that, compared to integral control of a first-order system, the difference is the appearance of the term $kK_p$ in the coefficient of $s$ in the denominator.

We now analyze  stability. If $K_p$ and $K_i$ are of the same sign (usually they are both positive), then there cannot be an unstable pole-zero cancellation in $PC$. Thus, the feedback system is stable if $S$ is stable, which is the case if

$$
    \boxed{\frac{1+kK_p}{T}>0,\quad \frac{kK_i}{T}>0}
$$

Introduce the parameters

$$
    \omega_n^2:=\frac{kK_i}{T},\quad\xi:=\frac{1+kK_p}{2\sqrt{kK_iT}}.
$$

Then

```{math}
:label: eq:S_PI
    S(s)=\frac{s^2+\frac{1}{T}s}{s^2+2\xi\omega_n s+\omega_n^2}.
```

```{prf:remark}
Note that here we can easily achieve $\xi=1$ and large $\omega_n$, as we have more freedom than with an integral controller only.
```

The transfer function from $r$ to $y$ is

$$
    G(s)=1-S(s).
$$

Denoting $z:=\frac{K_i}{K_p}$, this can be written  as

$$
    G(s)=\frac{s+z}{s^2+2\xi\omega_n s+\omega_n^2}\cdot\frac{\omega_n^2}{z}.
$$

Note that $G(0)=1$, and $G$ has a zero at $-z$. The presence of this zero makes the formula for the step response $y_{step}(t)$  more complicated, so we omit to write it. Compared to the step response which we would have if there were no zero, i.e., compared to

$$
    G_0(s)=\frac{\omega_n^2}{s^2+2\xi\omega_ns+\omega_n^2}.
$$

(which corresponds to $z\rightarrow\infty$, $K_p\rightarrow0$, i.e. just integral control)
the step response raises more quickly, and has a higher overshoot, as shown below:

```{figure} images/step_response_PI.png
---
width: 90%
name: fig:1order
---
Step response of $G$ and $G_0$.
```

It is important to understand how the poles of $S$ (which are also the poles of $G$) depend on the parameters $K_p$ and $K_i$. Denote the poles by $p_1,p_2\in \mathbb{C}$. 
From {eq}`eq:sense_p1p2` and {eq}`eq:S_PI`,  we see that
 
$$
    p_1+p_2&=-2\xi \omega_n = -\frac{1+kK_p}{T},\\ p_1p_2&=\omega_n^2 = \frac{kK_i}{T}.
$$

Thus, the average of the poles is always $-\frac{1+kK_p}{2T}$.

- If $\xi>1$ then the poles are real and located symmetrically left and right  to the average. 
- If $\xi=1$ then $p_1=p_2=-\omega_n$. 
- If $\xi<1$ then the poles are complex conjugate and located symmetrically above and below the average in the complex plane (see Fig. {ref}`fig:1order`).

Suppose that we fix $K_p$ and change $K_i$ from $0$ to $\infty$. For $K_i=0$ (this corresponds to $\xi=\infty$, i.e. unstable system) one pole is at $0$ and the other is at $-\frac{1+kK_p}{T}$. As we increase $K_i$, the two poles move closer, until they meet for $K_i=\frac{(1+kK_p)^2}{4kT}$
(this corresponds to $\xi=1$). As we further increase $K_i$ 
the eigenvalues become complex conjugate. 

```{figure} images/LEC4PIC.png
---
width: 90%
name: fig:1order
---
Pole locations of $G(s)$ as we increase $K_i$ from $0$ to $\infty$.
```

This behavior is summarized in the diagram in Fig. {ref}`fig:1order`. The center point of this diagram is the average $-\frac{1+kK_p}{2T}$. It can be shifted  to the left by increasing $K_p$ making the poles ``more stable''. However, we cannot increase $K_p$ arbitrarily much, because for a step reference signal (and $d=0$), we have 

$$
    u(0)=C(\infty)e(0)=K_p, 
$$
  
and we   cannot impose too large $u(0)$. After choosing $K_p$ we can choose $K_i$ such that $\xi=1$.

 

## PD Controllers

A PD (proportional-derivative) controller has the transfer function

$$
    C(s)=K_p+K_ds,\quad K_p, K_d\in\mathbb{R},
$$

where $K_p$ is the proportional term, and $K_ds$ is the derivative term. The coefficients $K_p,K_d$ must be tuned to achieve the desired performance of the feedback system. In the time domain, if $e(t)$ is the error signal and $v(t)$ is the controller output, then

$$
    v(t)=K_pe(t)+K_d\dot{e}(t).
$$

Note that the gain $|C(j\omega)|=\sqrt{K_p^2+\omega^2K_d^2}$ tends to infinity as $\omega\rightarrow\infty$ (this controller is not proper). Such a behavior is difficult (or impossible) to achieve in practice, so that we often use an approximate realization of the PD controller:

$$
    C(s)=K_p+\frac{K_ds}{1+Ts},
$$

where $T>0$ is small. Then for low frequencies (i.e., for $|s|\ll\frac{1}{T}$) we have $C(s)$ approximately equal to $K_p+K_ds$.

If the measurement of $e$ includes noise (which is typically a high frequency signal) then calculating $\dot e$ may increase the noise.
Sometimes we have access to a measurement in the plant that makes it unnecessary to calculate  $\dot{e}$. For example, if  the plant $P$ can be factored as $P(s)=P_0(s)\frac{m}{s+p}$

```{figure} images/P_decompose.png
---
width: 90%
name: fig:P_decom
---

```

and we can measure both $y$ and $q$, then we can compute $\dot{y}$ without having to differentiate, from $\dot{y}+py=mq$. If $\dot{r}$ is given (this is reasonable, since we generate $r$) then 

$$
\dot{e}=\dot{r}-\dot{y}=\dot{r}+py-mq.
$$

Thus, we can build the equivalent of a PD controller as follows:

```{figure} images/PD_controller.png
---
width: 90%
name: fig:P_D
---

```

For example, if $q$ represents a speed that can be measured directly, and $y$ is the corresponding position, then we can use this arrangement with $p=0$ and $m=1$.

```{prf:remark}
Note that if in the block diagram we replace $\dot{r}$ with $0$ (i.e., we do not supply $\dot{r}$), then this will have no effect on the location of the poles of the feedback system.
```

Consider now a second-order plant controlled with a PD controller:

```{figure} images/PD_closed_loop.png
---
width: 90%
name: fig:P_D
---

```

It is easy to check that the closed-loop transfer function from $r$ to $y$ is

$$
    G(s)=1-S(s)=\frac{kK_ds+kK_p}{s^2+(a_1+kK_d)s+(a_0+kK_p)}.
$$

We see that by changing $K_p$ and $K_d$, we can move the two poles of $G$ anywhere we want (the only restriction being that if the poles are non-real, they must be complex conjugate). As explained before, to have a small overshoot and a small settling time, a good choice is to take the poles equal and of large absolute value. Thus, we would choose $K_p$ large and then $K_d$ such that

$$
    a_1+kK_d=2\sqrt{a_0+kK_p}.
$$

PD controllers are a good choice   when the plant can be approximated well by a second-order plant. This means that

$$
    P(s)=\frac{k}{s^2+a_1s+a_0}+Q(s),
$$

where $|Q(j\omega)|$ is small in the frequency range of interest. Usually, $Q(s)$ contains the poles with large negative real part. ``Small''  is a relative concept, of course. If $P$ can be decomposed as above, then the poles of the first term (i.e., the zeros of $s^2+a_1s+a_2$) are called the  dominant poles of $P$. We mention that in industry we often encounter  PID controllers  (an obvious combination of PI and PD described in this chapter).
