# Chapter 3: What is a Control System

The general structure of a feedback connection  is as follows:

```{figure} images/plant_controller.png
---
width: 90%
name: fig:damp_spring
---

```

In general,  signals can be

- Continuous-time, that is, functions defined on $[0,\infty)$.
- Discrete-time, that is, functions defined on $\{0,1,2,\dots\}$. 


In this course,  all signals are continuous-time.

(section:closed_loop_LTI)=

## The Standard Feedback Connection of Two LTI Systems

We consider only the single input-single output (SISO) case.

```{figure} images/closed_loop1.png
---
width: 70%
name: fig:closed_loop
---
The feedback connection of two SISO linear systems with transfer functions "Plant" and "Controller".
```

We list each element in {numref}`fig:closed_loop`:

- $P$ is the transfer function of the plant.
- $C$ is the transfer function of the controller.
- $d$ is the <b>disturbance</b> acting on the plant.
- $u$ is the <b>input</b> signal of the plant.
- $y$ is the <b>output</b> signal of the plant.
- $r$ is the <b>reference</b> signal.
- $e=r-y$ is the <b>tracking error</b>.
 
We assume zero initial conditions, and denote the transfer function of the Plant by $P$, and the transfer function of the Controller by $C$. Then

$$
    \begin{bmatrix}
        \hat{d}(s)\\\hat{r}(s)
    \end{bmatrix}=\begin{bmatrix}
        1&-C(s)\\
        P(s)&1
    \end{bmatrix}\begin{bmatrix}
        \hat{u}(s)\\\hat{e}(s)
    \end{bmatrix}.
$$

This implies that

```{math}
:label: eq:closed_loop_trasnferfunctions
\begin{bmatrix}
        \hat{u}\\\hat{e}
    \end{bmatrix}&=\begin{bmatrix}
        1&-C\\
        P&1
    \end{bmatrix}^{-1}\begin{bmatrix}
        \hat{d}\\\hat{r}
    \end{bmatrix}\nonumber\\
    &=\begin{bmatrix}
        (1+PC)^{-1}&C(1+PC)^{-1}\\
        -P(1+PC)^{-1}&(1+PC)^{-1}
    \end{bmatrix}\begin{bmatrix}
        \hat{d}\\\hat{r}
    \end{bmatrix}.
```

We call $PC$ the <b>loop gain</b>. We define  $S:=(1+PC)^{-1}$,  and refer to this as the sensitivity function. Note that $S$ is the  transfer function from $r$ to $e$ (or from $d$ to $u$). 

```{prf:remark}
If

$$
    P(s)C(s)=\frac{n(s)}{d(s)},
$$

where $n(s)$ and $d(s)$ are polynomials, then

$$
    S(s)=\Big(1+\frac{n(s)}{d(s)}\Big)^{-1}=\frac{d(s)}{d(s)+n(s)}.
$$

Thus, we see that  the poles of $PC$ become zeros of $S$.
```

We would like to have good tracking in spite of the disturbances, i.e., to make $e$ small. Since

$$
    \hat{e} =-PS\hat{d} +S\hat{r} ,
$$

this can be achieved by making $S$ as small as possible, but  without destroying the stability of the closed-loop system.
 
## Stability of the Feedback System

The feedback connection of $P$ and $C$ is called  <b>stable</b> if the transfer function from $(d,r)$ to $(u,e)$ is stable, i.e., if all four entries of the matrix in {eq}`eq:closed_loop_trasnferfunctions` are stable. Note that two entries are equal, so that we have three different transfer functions  to check. Stability of the feedback connection means that if the inputs $(d,r)$ have finite energy, then all the signals in the diagram have finite energy.

 
In terms of state space systems, the interpretation of the stability concept defined for state-space systems is: If $P$ and $C$ are the transfer functions of a minimal plant and a minimal controller, then also the feedback system is minimal. Hence, if its transfer function $\begin{bmatrix}
        (1+PC)^{-1}&C(1+PC)^{-1}\\
        -P(1+PC)^{-1}&(1+PC)^{-1}
    \end{bmatrix}$ is stable, then also the system is stable. 

To state a condition for stability, we require the concept of zero-pole cancellation. 
We say that there is  zero-pole cancellation at $z$ in the product $PC$ if $z$ is a pole of $P$ (or $C$) and a zero of $C$ (or $P$).
The pole-zero cancellation is called stable if $z\in\mathbb{C}_-$ and unstable, otherwise.

````{prf:example}
:label: example:zp1
If

$$
    P(s)=\frac{s}{(s+1)(s-2)},\quad  C(s)=5\frac{s+1}{s^2+1},
$$
then there is a pole-zero cancellation at $z=-1$ in the product $PC$. Since $z=-1\in\mathbb{C}_-$, this is a stable cancellation. 
````

````{prf:example}
:label: example:zp2
If

$$
    P(s)=\frac{2s}{s^2+1},\quad
    C(s)=\frac{s^2+1}{(s+2)(s+100)},
$$
then there are unstable pole-zero cancellations at $z=i$ and at $z=-i$. 
````
 

```{prf:proposition}
:label: prop:stable_closed_loop
The feedback connection of $P$ and $C$ is stable if and only if the following two conditions hold:

1. $S=(1+PC)^{-1}$ is stable.
2. There is no unstable pole-zero cancellation in the product $PC$.
```

```{prf:example}
:label: example:zp3
Consider

$$
    P(s)=\frac{3s}{s-1},\quad C(s)=\frac{1}{s-1}.
$$

Obviously, there is no unstable pole-zero cancellation in $PC$ (in fact, there is no pole-zero cancellation at all). We compute

$$
    \big(1+P(s)C(s)\big)^{-1}=\frac{s^2-2s+1}{s^2+s+1},
$$

which is stable, so that the feedback connection is stable. Note that $P$ and $C$ are not stable. Thus, an unstable controller can be used to stabilize an unstable plant. 
```


## W-Stability

````{prf:definition}

The feedback connection of $P$ and $C$ is called  $w$-stable if

$$
    \big|P(\infty)  C(\infty)\big|<1.
$$

````

If this condition does not hold, then a very small change in $P$ and $C$ can cause all signals in the interconnection to tend to $\infty$ very fast. 

```{prf:example}
Consider

$$
    P(s)=\frac{5s}{s+1},\quad C(s)=-\frac{s+2}{s-1}.
$$

We have $P(\infty)=5$, $C(\infty)=-1$, so $\big|P(\infty)C(\infty)\big|=5$ and the feedback connection of $P$ and $C$ is not $w$-stable. It is easy to check that this feedback connection is stable using {prf:ref}`prop:stable_closed_loop`. Indeed, there are no zero-pole cancellations in $PC$ and

$$
    S(s)=-\frac{s^2-1}{4s^2+10s+1},
$$

is stable.
```

```{prf:remark}
When we design a feedback connection, we always require that it should be both stable and $w$-stable.
```

Indeed, in any engineering application, we must take into account that $P$ and $C$ are mathematical models and the real systems may be somewhat different, and we  cannot allow any signal to grow without bound. 

```{prf:remark}
A transfer function is called  strictly proper if $G(\infty)=0$. Equivalently, the degree of the numerator is less than the degree of the denominator. If $P$ or $C$ are strictly proper, then obviously the feedback connection is $w$-stable (as in {prf:ref}`example:zp1`, {prf:ref}`example:zp2`, {prf:ref}`example:zp3`).
```
 
 The stability of $S$ is one condition for stability of the feedback system (see {prf:ref}`prop:stable_closed_loop`).  

(sec:control_first_order)=

### An Example: Control of a First Order System

Suppose that  the plant is given by 

$$
    P(s)=\frac{k}{1+Ts},\quad k,T\in\mathbb{R},\;T\neq0.
$$

We want the control system in {numref}`fig:1order_sys_cont` to be stable,  and the output $y$ of the plant should be close to the reference signal $r$ (i.e., $e$ should be small).

```{figure} images/1order_system.png
---
width: 70%
name: fig:1order_sys_cont
---
Feedback control of a  first order system.
```

The signal $d$ is a disturbance. Since the plant is strictly proper, $w$-stability is not a problem. Usually, $T$ and $k$ are positive, but this need not be the case. The most important class of reference signals are steps (i.e., we would like a constant output $y$).

### Proportional Control

This is one possible type of control, not the best, but very simple:

$$
    C(s)=K,\quad K\in\mathbb{R}.
$$

The controller represents constant gain. We examine the performance of the closed-loop system. We compute its sensitivity: 

$$
    S(s)=\Big(1+\frac{kK}{1+Ts}\Big)^{-1}=\frac{1+Ts}{1+kK+Ts}.
$$

This is the transfer function from $r$ to $e$. For stability (since there are no pole-zero cancellations), we need that $S$ should be stable. Its pole is at

$$
    s_0=-\frac{1+kK}{T}.
$$

The stability condition is $s_0<0$. In particular, if $T>0$ (stable plant) then we need $1+kK>0$ (otherwise, we need $1+kK<0)$. The transfer function from $r$ to $y$ is

$$
    G(s)&=1-S(s)\\\
    &=\frac{kK}{1+Ts}S(s)\\&=\frac{kK}{1+kK}\cdot\frac{1}{1+\tau s},
$$

where $\tau:=\frac{T}{1+kK}$ is called the  time-constant of $G$. From this we can easily compute the step response of $G$ (i.e., the function $y(t)$ when $r(t)=1$):

$$
    y_{step}(t)=\frac{kK}{1+kK}\big(1-e^{-\frac{t}{\tau}}\big).
$$

```{figure} images/1order_step_response.png
---
width: 70%
name: fig:1order_step_res
---
Step response of a first order system with $k=1,\;K=2$.
```

As expected, for large $t$, $y_{\text{step}}(t)$ approaches $G(0)$. The error,

$$
    e_{\text{step}}(t)=\underbrace{1}_{r(t)}-y_{\text{step}}(t),
$$

converges to $1-G(0)=S(0),$ i.e.,

$$
    e_{\text{step}}(\infty)=\frac{1}{1+kK}.
$$

The derivative of $y_{\text{step}}(t)$ at $t=0$ (its slope) is

$$
    \frac{d}{dt}y_{\text{step}}(0)=\frac{G(0)}{\tau}=\frac{1+kK}{T}\cdot G(0)=\frac{kK}{T}.
$$

The smaller the time constant $\tau$, the faster the step response $y_{\text{step}}(t)$ will approach its final value (which is $G(0)$).

Our aim is to make $e_{\text{step}}(\infty)$ small (small stationary error) and $\tau$ small (fast response of the control system). From the formulas, it is clear that both aims can be achieved by choosing $|K|$ large. The correct sign of $K$ depends on the sign of $T$ and $k$, for example, if $T>0$ and $k>0$ then also $K>0$. In the graphs below, we show various graphs of possible $y_{\text{step}}(t)$ as $|K|$ increases.

```{figure} images/1order_step_response_K.png
---
width: 70%
name: fig:1order_K
---
Step response of a first order system with $k=1,\;T=5$.
```

However, there are also disadvantages with a large controller gain $K$:

- The control input $u(t)$ becomes large for small values of $t$. Indeed

$$
    u(0)=Ke(0)=KS(\infty)=K.
$$
	
Often, it is not permissible to apply large $u$ values to the plant (something could be damaged).

- If the transfer function of the plant $\frac{k}{1+Ts}$ is just an approximation, and in reality, there are more poles present (which is almost always the case), then the high gain $K$ can lead to instability of the feedback system. (This phenomenon can be better understood after studying the Nyquist test for stability of feedback systems).

Thus, a sensible compromise should be found between the need to increase $K$ and the need to avoid the two problems above. 

(sec:eliminate_constant)=

## Eliminating the Steady-State Error for Constant Reference and Disturbance 

We saw in Section {ref}`sec:control_first_order` that if we apply proportional control to a first order system and the reference $r$ and/or the disturbance $d$ converge to   non-zero constants, then also the error $e$, given by $\hat{e}(s)=S\hat{r}(s)-PS\hat{d}(s)$ converges (as $t\rightarrow\infty$) to a non-zero value $e_{ss}$ called the  steady-state error. 


Our goal now is to  achieve $e_{ss}=0$ for any $d,r$ that converge to constant values, by using a different controller $C$. If $r$ converges to a constant as $t\rightarrow\infty$, for example, if $r$ is a step and similarly for $d$, then denoting $r_{ss}:=\lim_{t\rightarrow \infty} r(t)$, $d_{ss}:=\lim_{t\rightarrow\infty}d(t)$, and using  the final value theorem gives 

```{math}
:label: eq:limess
    e_{ss}&=\lim_{t\rightarrow\infty}e(t)\\
          &=\lim_{s\rightarrow0}s\hat{e}(s)
          \nonumber \\ &=\lim_{s\rightarrow0}S(s)s\hat{r}(s)-\lim_{s\rightarrow0}P(s)S(s)s\hat{d}(s)\nonumber \\
          &=S(0)r_{ss}-P(0)S(0)d_{ss}.\nonumber
```

In order to obtain $e_{ss}=0$ (for all $r_{ss},\;d_{ss}$), we need $S(0)=0$. It is easy to see that the zeros of $S$ are the poles of the loop gain $PC$. Thus, for $e_{ss}=0$, $C$ should have a pole at $s=0$.

```{prf:remark}
In the above discussion, we had in mind the first order system. However, the arguments and conclusions remain valid for any rational transfer function $P$.
```

There is a little problem that has to be clarified if $P$ has a pole at $s=0$. In this case, $PC$ will have a higher order pole at $s=0$, and we still have

$$
    \lim_{s\rightarrow0}P(s)S(s)=0,
$$

so that scheme will work also in this case.

Naturally, the other requirements for a controller must be satisfied as well: stability (as otherwise the limit in {eq}`eq:limess` may not exist) and also $w$-stability. This implies the following: If $P(0)=0$, then we cannot achieve $e_{ss}=0$.
Indeed, in this case  there would be a pole-zero cancellation at $s=0$ in the product $PC$, and according to {prf:ref}`prop:stable_closed_loop` the feedback connection of $P$ and $C$ would not be stable in this case.

````{prf:example}
Consider the circuit below, with input $u$ (a voltage) and output $y$ (also a voltage).

```{figure} images/circuit_for_example.png
---
width: 70%
name: fig:circuit
---

```

The transfer function $P(s):=\frac{\hat y(s)}{\hat u(s)}$ is

$$
    P(s)=\frac{RCs}{1+RCs}.
$$

Since $P(0)=0,$ we cannot achieve $e_{ss}=0$ for constant $r\neq0$. We also give a physical explanation: to obtain $e_{ss}=0$ we would need $\lim_{t\rightarrow\infty}y(t)=r$. Denoting the input current of the circuit by $j$ we would then have

$$
    \lim_{t\rightarrow\infty}j(t)=\frac{r}{R}\neq0.
$$

Such a current would cause the voltage on the capacitor $v_c(t)=\frac{1}{C}\int_0^t j(\sigma)d\sigma$ to tend (linearly) to $\infty$. Hence, $\lim_{t\rightarrow \infty}u(t)=\infty$, which shows that the control system would need to be unstable.
````

```{prf:remark}
If $P$ is such that $P(0)=\infty$ (i.e, $P$ has a pole at $s=0$) and $C$ does not have a pole at $s=0$, and if the feedback system is stable, then with $\lim_{t\rightarrow\infty}r(t)=r_{ss}$ and $\lim_{t\rightarrow\infty}d(t)=0$ we obtain again $e_{ss}=0$. 
```

## Integral Control and  Second Order Systems

This is a particular controller that eliminates the steady-state error. Consider

$$
    P(s)=\frac{k}{1+Ts},\quad C(s)=\frac{K_i}{s}.
$$

We compute the sensitivity transfer function

$$
    S(s)=\frac{Ts^2+s}{Ts^2+s+kK_i}.
$$

Note that $S(0)=0$. We see that $S$ is stable if $T>0$ and $kK_i>0$. The first condition means that the plant must be stable. The second condition can be satisfied by choosing correctly the sign of $K_i$ (should be the same as the sign of $k$). There are no pole-zero cancellations between $P$ and $C$, so that if $S$ is stable, then also the feedback system is stable. $w$-stability is not a problem at all, since $P(\infty)=C(\infty)=0$.

We now calculate the system response   in more detail. The transfer function from $r$ to $y$ is 

$$
    G(s)=1-S(s)=\frac{kK_i}{Ts^2+s+kK_i}.
$$

Let

$$
    \omega_n^2:=\frac{kK_i}{T},\quad \xi:=\frac{1}{2\sqrt{kK_iT}}.
$$

Then

$$
    G(s)=\frac{\omega_n^2}{s^2+2\xi\omega_n s +\omega_n^2}.
$$

We have $\omega_n,\;\xi>0$. Usually, $K_i$ is chosen such that $\xi\leq 1$. If this is the case, then $G(s)$ has two complex conjugate poles, $s_0$ and $s_0^*$. If we denote by $\varphi$ the angle between these poles and the negative real axis ($\varphi\in[0,\pi/2)$), then

$$
    \omega_n=|s_0|,\quad\xi=\cos\varphi.
$$

```{figure} images/2ordersystempoles.png
---
width: 70%
name: fig:1order_pole
---
Pole location of second order system.
```

If $\xi=1$, then $s_0=s_0^*$ and

$$
    G(s)=\frac{\omega_n^2}{(s+\omega_n)^2},
$$

that is, a double real pole at $-\omega_n$. For $\xi>1$ we have two distinct real poles. 


We return to the case $\xi<1$. The impulse response corresponding to $G$ is 

$$
    g(t)=\frac{\omega_n}{\sqrt{1-\xi^2}}e^{-\xi\omega_n t}\sin\big(\sqrt{1-\xi^2}\omega_n t\big).
$$

$\xi$ is called the  damping ratio of $G$. The corresponding step response is

```{math}
:label: eq:freq_step_resp
    y_{\text{step}}(t)&=
    \int_0^t g(\sigma)d\sigma
   \nonumber  \\&=
    1-\frac{e^{-\xi\omega_n t}}{\sqrt{1-\xi^2}}\sin\big(\sqrt{1-\xi^2}\omega_n t+\varphi\big).
```

```{figure} images/second_order_step_response.png
---
width: 70%
name: fig:1order_step_res
---
Second order step response for $\omega_n=2,\;\xi=0.2$.
```

If we denote by $t_p,\;t'_p,\;t''_p,\cdots$ the times of the peaks (local maximums) of $y_{\text{step}}(t)$, then

$$
    t_p=\frac{\pi}{\omega_n\sqrt{1-\xi^2}},\quad t'_p=\frac{3\pi}{\omega_n\sqrt{1-\xi^2}},\quad t''_p=\frac{5\pi}{\omega_n\sqrt{1-\xi^2}},\cdots.
$$

the peak values are

$$
    y_{\text{step}}(t_p)=1+\sigma,\quad y_{\text{step}}(t'_p)=1+\sigma^3,\quad y_{\text{step}}(t''_p)=1+\sigma^5,\cdots.
$$

where $\sigma$ is the  overshoot of the step response $y_{\text{step}}$, given by

$$
    \sigma=e^{-\frac{\pi\xi}{\sqrt{1-\xi^2}}}.
$$

Note that if $\xi$ is close to zero, then $\sigma$ is close to $1$ and the oscillations die very slowly, i.e., $y_{\text{step}}(t'_p)$ is almost as high as $y_{\text{step}}(t_p)$, etc.  As $\xi$ gets bigger, $\sigma$ gets smaller and the oscillations die more quickly. 


The  logarithmic decrement of $y_{\text{step}}$ is

$$
   \log( \frac{y_{\text{step}}(t_p)-1}{y_{\text{step}}(t'_p)-1})&=-2\log(\sigma)\\&=2\pi\xi/\sqrt{1-\xi^2}.
$$

This  can be measured experimentally with relative ease, and permits the computation of $\xi$. 

By {eq}`eq:freq_step_resp`, the frequency of the oscillations is

$$
\omega_d:=\omega_n\sqrt{1-\xi^2}.
$$

This is called the damped natural frequency of $G$. As $\xi$ gets bigger, the frequency decreases. 

### The critically damped case
  
This is the case when $\xi=1$.  We then have the impulse response

$$
    g(t)=\omega_n^2 te^{-\omega_n t},
$$

and the step response

$$
    y_{\text{step}}(t)&= \int_0^t g(\sigma)d\sigma\\
    &=1-(1+\omega_n t)e^{-\omega_n t}.
$$

```{figure} images/2order_system_crit_damped.png
---
width: 70%
name: fig:1order_crit
---
Second order system with $\xi=1$ (critically damped) for different values of $\omega_n$.
```

In this case, there is no overshoot ($\sigma=0$) and sometimes this is considered the most desirable situation.

For $\xi>1$ there is also no overshoot, but the response becomes slower (the step response rises slower at the beginning). In practical designs, we usually choose $0.7\leq\xi\leq1$.

 
## Eliminating the Steady-State Error for Ramp  Inputs

Sometimes it is required to achieve $e_{ss}=\lim_{t\rightarrow\infty}e(t)=0,$ where $r$ and $d$ are of the form

$$
    r(t)=at+b.
$$

For this, it will be enough to solve the problem corresponding to $r(t)=t$ (this is called the ramp input) and $d=0$. Note that in this case $\hat{r}(s)=\frac{1}{s^2}$. By the final value theorem,

$$
    e_{ss}=\lim_{s\rightarrow 0}s\hat{e}(s)=\lim_{s\rightarrow0}sS(s)\frac{1}{s^2} = \lim_{s\rightarrow0} S(s)\frac{1}{s}.
$$

To obtain $e_{ss}=0$, $S$ should have a double zero at $s=0$. Assuming that $P(0)\neq0$, this is possible if $C$ has a double pole at $s=0$. Thus,  to eliminate the steady-state error  for a ramp input, $C$ should have a double (or higher) pole at $s=0$. If $P(0)=0$, then the steady state error for ramp input cannot be eliminated. 

## Eliminating the Steady-State Error for Sinusoidal Inputs


Now consider the problem to achieve $e_{ss}=0$ when $r$ and $d$ are of the form 

$$
    r(t)=R\cos(\omega_0 t+\psi),
$$

where $\omega_0>0$ is known, and $R,\;\psi$ can be any real numbers, not known in advance. For this, it will be enough to solve the problem corresponding to $r(t)=\cos(\omega_0 t)$ and $d=0$. Note that since $S$ represents a  stable LTI system, $e$ will converge to 

$$
    e(t)=A (\omega_0) \cos(\omega_0 t+\varphi (\omega_0) ), 
$$

where 

$$
    A ( \omega_0 ) =\big|S( i \omega_0)\big|,\;\varphi ( \omega_0 ) =\arg\big(S( i \omega_0)\big).
$$

Hence, to obtain $\lim_{t\rightarrow\infty}e(t)=0$, we need $S( i \omega_0)=0$. For this,  $C$ should have a pole at $i \omega_0$. By symmetry, $C$ must have a pole also at $-j\omega_0$. It will not work if $P( i \omega_0)=0$.

```{prf:example}
Suppose that  

$$
    P(s)=\frac{k}{1+Ts},\quad C(s)=\frac{Ks}{s^2+\omega_0^2},
$$
	
with $k,\;T,\;K,\;\omega_0$ all positive. Then the feedback system of $P$ and $C$ is stable (check this!) and $e_{ss}=0$ for $r,\;d$ sinusoidal signals of angular frequency $\omega_0$ (check this!).
```

## Internal Model Principle

The following table summarizes our findings in this chapter.

```{table} Controllers needed to achieve zero steady-state error
:label: tab-my_label
:align: center

| Input $r$    | Laplace Transform of Input $\hat{r}$           | Structure Needed in Controller $C(s)$     |
|:--------------|:-------------------------------------------------|:-------------------------------------------|
| Step          | $\hat{r}(s) = \dfrac{1}{s}$                    | $\dfrac{1}{s}$                           |
| Ramp          | $\hat{r}(s) = \dfrac{1}{s^2}$                  | $\dfrac{1}{s^2}$                         |
| Sinusoidal    | $\hat{r}(s) = \dfrac{1}{s^2+\omega_0^2}$        | $\dfrac{1}{s^2+\omega_0^2}$               |
```


We conclude that the controller must encapsulate the form of the input for which we require zero steady state error. This is known as the internal model principle {cite:p}`internal-sontag_2022`. 


This raises interesting questions. For example, if we apply a reverse engineering  process to  decipher a biological controller in our cells, can we determine for what types of inputs/disturbances this controller was designed? 

 ## References

```{bibliography} references.bib