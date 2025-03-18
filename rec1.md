---
title: Introduction to Control -- Recitation 1
---

# Introduction to Control -- Recitation 1

## Transfer Functions

A general solution of a second-order differential equation with constant coefficients:

```{math}
\ddot{y} + a \dot{y} + b y = 0,
```

is:

```{math}
:label: my_label
y(t) = C_1 e^{\lambda_1 t} + C_2 e^{\lambda_2 t}.
```


Here, $C_1,C_2\in\mathbb{R}$ depend on initial conditions, and $\lambda_1, \lambda_2$ are the roots of:

```{math}
:label: eq:cp
\lambda^2+a\lambda+b=0.
```

The behavior of the solution depends on the roots of {eq}`eq:cp`.

:::{Note} 
The roots of {eq}`eq:cp` can be complex. We generally write $\lambda=a+ib$ where $a,b\in\mathbb{R}$.
:::
Interactive Plot of  $y(t) = e^{(a_1+ib_1)t}+e^{(a_2+ib_2)t}$:

<center>
<a href="https://mybinder.org/v2/gh/Omrid1994/solution-plot/HEAD?urlpath=voila/render/2dtime_solution.ipynb" target="_blank">
    <button style="font-size:18px; padding:10px 20px; background-color:#0078D4; color:white; border:none; border-radius:5px; cursor:pointer;">
        🚀 Click to Open Interactive Plot
    </button>
</a>
</center>

:::{Important} 
If $b_1,b_2\neq0$, then the solution will be oscillatory. $y(t)$ converges only if $a_1<0$ and $a_2<0$, that is, the real part of both roots of {eq}`eq:cp` is negative.
:::






### Important Laplace Transformations

```{math}
\mathcal{L}\{\delta(t-t_0)\}=e^{-st_0},\quad \mathcal{L}\{1(t)\}=\frac{1}{s},\quad \mathcal{L}\{u(t-\tau)\}=U(s)e^{-s\tau},\quad \mathcal{L}\{e^{at}\}=\frac{1}{s-a}.
```

For zero initial conditions:

```{math}
\mathcal{L}\{f^{(n)}(t)\}=s^n\mathcal{L}\{f(t)\}.
```

## Stability Theorems for Transfer Functions

**Frequency Domain Criterion:** A (rational) transfer function is stable if and only if all its poles are on the left-hand side of the complex plane.

**Time Domain Criterion:** The transfer function is stable if and only if for the impulse response $h(t)$:

```{math}
\int_0^{\infty} |h(t)| dt < \infty
```

### Exercise -- Damped and Driven Harmonic Oscillator

Consider the damped and driven harmonic oscillator with mass $m=1$:

```{figure} images/output.png
---
width: 60%
name: fig-mass-spring-damper
---
Diagram of the mass-spring-damper system.

The differential equation representing this system is:

```{math}
:label: eq:spring_damper
\ddot{x}(t) + 2\gamma\dot{x}(t) + \omega^2x(t) = a\dot{u}(t)-bu(t).
```

Let $\gamma=4$, $\omega^2=3$, $a=2$, $b=3$. Define:

```{math}
X(s) = \mathcal{L}\{x(t)\},\quad U(s)=\mathcal{L}\{u(t)\}.
```


1. Find the transfer function $G(s)=\frac{X(s)}{U(s)}$ of the system. What are the poles and zeros of $G(s)$?
2. Find the impulse response of the system:
3. Find the step response of the system.
4. Is the system stable?

### Solution

1. Transfer Function Derivation

Applying the **Laplace Transform**:

```{math}
s^2X(s) + 2\gamma sX(s) + \omega^2 X(s) = asU(s) - bU(s).
```

Factoring:

```{math}
X(s)(s^2 + 2\gamma s + \omega^2) = U(s)(as - b).
```

Thus, the **transfer function** is:

```{math}
\boxed{G(s) = \frac{X(s)}{U(s)} = \frac{as-b}{s^2 + 2\gamma s + \omega^2}}
```
Note that the numerator corresponds to the excitation, and the denominator corresponds to the system itself.

There is a zero at $s = \frac{a}{b}$. The poles are:

```{math}
s^2 + 2\gamma s + \omega^2 = 0 \rightarrow s_{1,2} = -\gamma \pm \sqrt{\gamma^2 - \omega^2}.
```

The solution of {eq}`eq:spring_damper` is:

```{math}
y(t) = c_1 e^{\lambda_1 t} + c_2 e^{\lambda_2 t},
```

where

```{math}
\lambda_{1,2} = -\gamma \pm \sqrt{\gamma^2 - \omega^2}.
```
Note that the poles of~$G(s)$ correspond to the time-domain solution of {eq}`eq:spring_damper`.
Substituting the values, we have:

```{math}
G(s) = \frac{X(s)}{U(s)} = \frac{2(s - 1.5)}{(s + 1)(s + 3)}.
```

The zero is at $s = 1.5$, and the poles are at $s = -1, -3$.

2. Impulse Input

In this case, $u(t) = \delta(t)$, so $U(s) = 1$. We have:

```{math}
\frac{X(s)}{U(s)} = G(s) \rightarrow X(s) = G(s) U(s) \underbrace{=}_{U(s)=1} G(s) = \frac{2(s - 1.5)}{(s + 1)(s + 3)}.
```

The impulse response is:

```{math}
h(t) := \mathcal{L}^{-1} \{ G(s) \}.
```

Partial fraction decomposition gives:

```{math}
G(s) = \frac{2(s - 1.5)}{(s + 1)(s + 3)} = -\frac{2.5}{s + 1} + \frac{4.5}{s + 3}.
```

:::{admonition} Click here for the derivation of the fraction decomposition.
:class: seealso, dropdown

We decompose the function:

```{math}
\frac{2(s - 1.5)}{(s + 1)(s + 3)} = \frac{A}{s + 1} + \frac{B}{s + 3}.
```

Multiplying both sides by $(s + 1)(s + 3)$:

```{math}
2s - 3 = s(A + B) + 3A + B.
```

Comparing coefficients:

```{math}
2 = A + B, \quad -3 = 3A + B.
```

Solving for $A$ and $B$:

```{math}
B = 2 - A, \quad -3 = 3A + (2 - A).
```

Rearranging:

```{math}
-3 = 3A + 2 - A \Rightarrow A = -2.5, \quad B = 4.5.
```
:::
Thus, the inverse Laplace transform is:

```{math}
h(t) &= \mathcal{L}^{-1} \{ G(s) \} \\
&=-2.5\mathcal{L}^{-1}\Big\{\frac{1}{s+1}\Big\}+4.5\mathcal{L}^{-1}\Big\{\frac{1}{s+3}\Big\}\\
&= -2.5 e^{-t} + 4.5 e^{-3t}, \quad t \geq 0.
```

3. Step Input

In this case, $u(t) = 1(t)$, thus $U(s) = \frac{1}{s}$. We have:

```{math}
X(s) = G(s) U(s) = \frac{2(s - 1.5)}{(s + 1)(s + 3)} \cdot \frac{1}{s}.
```

Partial fraction decomposition gives:

```{math}
X(s) = \frac{2.5}{s + 1} - \frac{1.5}{s + 3} - \frac{1}{s}.
```

:::{admonition} Click here for the derivation of the fraction decomposition.
:class: seealso, dropdown

We further decompose:

```{math}
\frac{2(s - 1.5)}{(s + 1)(s + 3)} \cdot \frac{1}{s} = \frac{A}{s + 1} + \frac{B}{s + 3} + \frac{C}{s}.
```

Multiplying both sides by $(s + 1)(s + 3)s$:

```{math}
2s - 3 = A(s^2 + 3s) + B(s^2 + s) + C(s^2 + 4s + 3).
```

Comparing coefficients:

```{math}
0 = A + B + C, \quad 2 = 3A + B + 4C, \quad -3 = 3C.
```

Solving for $C$:

```{math}
C = -1.
```

Substituting into the other equations:

```{math}
0 = A + B - 1, \quad 2 = 3A + B - 4.
```

Solving for $A$ and $B$:

```{math}
A = 2.5, \quad B = -1.5, \quad C = -1.
```
:::
The inverse Laplace transform gives::

```{math}
x(t)&=2.5\mathcal{L}^{-1}\Big\{\frac{1}{s+1}\Big\}-1.5\mathcal{L}^{-1}\Big\{\frac{1}{s+3}\Big\}-\mathcal{L}^{-1}\Big\{\frac{1}{s}\Big\}\\
    &=2.5e^{-t}-1.5e^{-3t}-1,\;t\geq0.
```

4.We saw that all poles have a negative real part, so the transfer function is stable. Moreover, according to the time domain theorem, the impulse response is a decreasing exponential, so it is easy to confirm that the integral is finite.
### Conclusion

- The time behavior depends on the poles of $G(s)$.
- Since all poles have a **negative real part**, the transfer function is **stable**.
- According to the time domain theorem, the impulse response is a **decreasing exponential**, confirming that the integral is finite.





## Routh-Hurwitz Criterion

We saw in class that the system is stable if the matrix is **Hurwitz**, that is, the real part of every eigenvalue is negative. The **Routh-Hurwitz criterion** helps us determine if a polynomial is stable or not. Consider the following polynomial:

```{math}
P(s) = a_n s^n + a_{n-1} s^{n-1} + \dots + a_1 s + a_0.
```

We build the following table:

```{math}
\begin{array}{c|cccc}
    s^n     & b_n     & b_{n-2} & b_{n-4} & \dots \\
    s^{n-1} & b_{n-1} & b_{n-3} & b_{n-5} & \dots \\
    s^{n-2} & c_1 & c_2 & c_3 & \cdots \\
    s^{n-3} & d_1 & d_2 & \cdots & \cdots \\
    \vdots  & \vdots  & \vdots  & \vdots  & \vdots \\
    s^1 & j_1 \\
    s^0 & k_1
\end{array}
```

If $n$ is even (odd), then the first row consists of the coefficients of all even (odd) powers, and the second row consists of the coefficients of all odd (even) powers. All other values are calculated recursively.

```{math}
c_1 = \frac{b_{n-1} b_{n-2} - b_n b_{n-3}}{b_{n-1}}, \quad
c_2 = \frac{b_{n-1} b_{n-4} - b_n b_{n-5}}{b_{n-1}}, \quad
c_3 = \frac{b_{n-1} b_{n-6} - b_n b_{n-7}}{b_{n-1}}
```

```{math}
d_1 = \frac{c_1 b_{n-3} - b_{n-1} c_2}{c_1}, \quad
d_2 = \frac{c_1 b_{n-5} - b_{n-1} c_3}{c_1}, \quad
d_3 = \frac{c_1 b_{n-7} - b_{n-1} c_4}{c_1}
```

```{admonition} Key Insight
:class: tip
The **number of sign changes in the first column** is the number of right-handed roots.
```

### Properties

- We may multiply all the elements of a row by a **positive constant**.
- If an element in the first column is **zero**, and there are other non-zero elements in the same row, then we can do one of the following:
  
  - Take a small $\epsilon$, obtain a new polynomial, and check its stability.
  - Divide the polynomial by $(s + \epsilon)$ where $\epsilon$ is small, and check its stability.
  - Replace the zero with $\epsilon$, and continue as usual, where we only care about the sign changes.

- If there is a **row in which all elements are zero**, we:
  - Build a polynomial from the row above it.
  - Differentiate it.
  - Substitute its coefficients in place of the row of zeros.

- The polynomial above the row of zeros **divides the original polynomial**; the roots of this polynomial are also the roots of the original polynomial.

### Exercise 1 - zero element in the first column

Consider the polynomial:

```{math}
P(s) = s^5 + s^4+ 2s^3+ 2s^2 + 3s + 15.
```
Find the number of right-handed roots of $P(s)$ using the Routh-Hurwitz table.
The Routh table will be:

```{math}
\begin{array}{c|cccc}
    s^5 & 1 & 2 & 3 \\
    s^4 & 1 & 2 & 15 \\
    s^3 & 0 & -12
\end{array}
```

We replace $0$ by $\varepsilon$, and continue:

```{math}
\begin{array}{c|cccc}
    s^5 & 1 & 2 & 3 \\
    s^4 & 1 & 2 & 15 \\
    s^3 & \varepsilon & -12 \\
    s^2 & d_1 & d_2 \\
    s^1 & e_1 \\
    s^0 & f_1
\end{array}
```

:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown



In this case:

```{math}
d_1 = \frac{2\varepsilon+12}{\varepsilon}>0, \quad
d_2 = \frac{15\varepsilon}{\varepsilon}=15.
```

Moreover,

```{math}
e_1 = \frac{\frac{-24\varepsilon-144}{\varepsilon}-15\varepsilon}{\frac{2\varepsilon+12}{\varepsilon}} = -\frac{15\varepsilon^2+24\varepsilon+144}{2\varepsilon+12}<0.
```

Finally, we have:

```{math}
f_1 = \frac{e_1 d_2 - d_1 \cdot 0}{e_1} = \frac{e_1 d_2}{e_1} = d_2 = 15.
```

To conclude:

```{math}
\begin{array}{c|cccc}
    s^5 & 1 & 2 & 3 \\
    s^4 & 1 & 2 & 15 \\
    s^3 & \varepsilon>0 & -12 \\
    s^2 & d_1>0 & 15 \\
    s^1 & e_1<0 \\
    s^0 & f_1>0
\end{array}
```
:::
There are **two sign variations** in the first column, so we have **two right-handed roots**. A system with $P(s)$ as its denominator is **not stable**.

### Exercise - row of zeros

Consider the polynomial:

```{math}
P(s) = s^6 + s^5 - 2s^4 - 3s^3 - 7s^2 - 4s - 4.
```

We find the number of right-handed roots of $P(s)$.

The Routh table will be:

```{math}
\begin{array}{c|cccc}
    s^6 & 1 & -2 & -7 & -4 \\
    s^5 & 1 & -3 & -4 & 0 \\
    s^4 & c_1 & c_2 & c_3 \\
    s^3 & d_1 & d_2
\end{array}
```

:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown
Here:

```{math}
c_1 &= \frac{b_5b_4 - b_6b_3}{b_5} = \frac{1 \cdot -2 - (1 \cdot -3)}{1} = \frac{1}{1} = 1, \\
c_2 &= \frac{b_5b_2 - b_6b_1}{b_5} = \frac{1 \cdot -7 - (1 \cdot -4)}{1} = \frac{-3}{1} = -3, \\
c_3 &= \frac{b_1b_0 - b_6 \cdot 0}{b_5} = \frac{-4}{1} = -4, \\
d_1 &= \frac{c_1b_3 - b_6c_2}{c_1} = \frac{1 \cdot -3 - (1 \cdot -3)}{1} = 0, \\
d_2 &= \frac{c_1b_1 - b_5c_2}{c_1} = \frac{1 \cdot -4 - (1 \cdot -4)}{1} = 0.
```
:::
We have:

```{math}
\begin{array}{c|cccc}
    s^6 & 1 & -2 & -7 & -4 \\
    s^5 & 1 & -3 & -4 & 0 \\
    s^4 & 1 & -3 & -4 & 0 \\
    s^3 & 0 & 0
\end{array}
```

Since we obtained a row of zeros, we use the coefficients of the row $s^4$ to generate a new polynomial:

```{math}
p(s) = s^4 - 3s^2 - 4s^0.
```

Differentiating with respect to $s$:

```{math}
p'(s) = 4s^3 - 6s.
```

We replace the coefficients of $p'(s)$ with the zeros in the Routh table:

```{math}
\begin{array}{c|cccc}
    s^6 & 1 & -2 & -7 & -4 \\
    s^5 & 1 & -3 & -4 & 0 \\
    s^4 & 1 & -3 & -4 & 0 \\
    s^3 & 4 & -6 \\
    s^2 & e_1 & e_2 \\
    s^1 & f_1 \\
    s^0 & g_1
\end{array}
```
:::{admonition} Click here for the derivation of the table elements
:class: seealso, dropdown
Here,

```{math}
e_1 &= \frac{d_1c_2 - c_1d_2}{d_1} = \frac{4 \cdot -3 - (1 \cdot -6)}{4} = -\frac{6}{4}, \\
e_2 &= \frac{d_1c_3 - c_1d_3}{d_1} = \frac{-4 \cdot 4}{4} = -4, \\
f_1 &= \frac{e_1d_2 - e_2d_1}{e_1} = \frac{-(6/4) \cdot -6 - (4 \cdot -4)}{-6/4} = -\frac{50}{3}, \\
g_1 &= \frac{f_1e_2 - f_2e_1}{f_1} = \frac{-50/3 \cdot -4}{-50/3} = -4.
```

Thus, the final Routh table is:

```{math}
\begin{array}{c|cccc}
    s^6 & 1 & -2 & -7 & -4 \\
    s^5 & 1 & -3 & -4 & 0 \\
    s^4 & 1 & -3 & -4 & 0 \\
    s^3 & 4 & -6 \\
    s^2 & -6/4 & -4 \\
    s^1 & -50/3 & 0 \\
    s^0 & -4
\end{array}
```
:::
Here we have **one sign variation** in the first column, so there is **one right-handed root**. A system with $P(s)$ as its denominator is **not stable**.
