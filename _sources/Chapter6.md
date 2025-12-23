# Chapter 6: Analysis and Synthesis in the Frequency Domain

If $\Sigma$ is a stable linear system with transfer function $G$ then the response to the  input 

$$
    u(t)=\cos(\omega t),
$$

is the output 

$$
    y(t)=A(\omega)\cos(\omega t+\varphi(\omega))+e(t),
$$

where the transient response $e(t) $ converges to zero, and

$$
    A(\omega)&=\big|G(j\omega)\big|\text{ is the  gain at $\omega$,}\\
    \varphi(\omega)&=\arg\big(G(j\omega)\big)\text{ is the  phase shift at $\omega$}.
$$

If the input is the sum of sinusoidal terms then, by linearity,  the output will be the sum of the responses to each input term. 

## Bode Plot

The Bode plot provides a   graphical representation of the two functions $A(\omega)$ and $\varphi(\omega)$, with a logarithmic $\omega$-axis, and with the gain represented logarithmically by $20\log(A(\omega))$,  and the phase represented linearly in degrees or radians. The two plots together are called the Bode plot of $G$. The logarithmic scales are suitable for looking at several frequency ranges in one glance, and they also make the drawing of the plots easier, because of the appearance of linear asymptotes. The plot with a logarithmic scale in the $x$-axis becomes easier using a semi-logarithmic paper.

Suppose that the transfer function $G$ can be decomposed as $G=G_1G_2$. Then

$$
20\log |G(j\omega)|&= 20\log |G_1(j\omega)G_2(j\omega)|\\
&=20\log |G_1(j\omega)|+20\log|G_2(j\omega)|,   
$$

and

$$
\arg (G(j\omega))&=\arg ( G_1(j\omega)G_2(j\omega))\\ 
&= \arg ( G_1(j\omega) )+\arg ( G_2(j\omega) ).    
$$

Thus, the Bode plot will be   the ``sum'' of the Bode plot of $G_1$ and the Bode plot of $G_2$. 

If $G=G_1/G_2$ then a similar calculation gives

$$
20\log |G(j\omega)|=20\log |G_1(j\omega)|-20\log|G_2(j\omega)|,
$$

and

$$
\arg (G(j\omega))= \arg ( G_1(j\omega) )-\arg ( G_2(j\omega) ).    
$$

We will typically consider
transfer functions in the form $G(s)=\frac{n(s)}{d(s)}$,
where $n,d$ are polynomials with real coefficients, and the ratio is proper.  
Each polynomial can be decomposed as the product of terms in the form $(s-z)$ and $(s^2+2\zeta \omega_ns+\omega^2)$, and the discussion above implies that it is enough to know  the plots  for the 8 basic 
transfer functions listed below. 

[📄 Download the file here](files/BODE_BASIC.pdf)




Generating a Bode plot then reduces to expressing the transfer function using the 8 basic functions described above, and then graphically adding the plots corresponding to each basic function. 
For example, given $G(s)= \frac{s+7}{s-2}$, we write

$$
    G(s)&= \frac{7(1+\frac{s}{7} ) }{-2(1+\frac{s}{-2})}\\
    &=( -3.5) \frac{1+\frac{s}{7}  }{1+\frac{s}{-2}},
$$

and this  is the product of three basic transfer functions in the form: $H(s)=k$, $H(s)=1+\frac{s}{\omega_n}$ with $\omega_n>0$,    and $H(s)=\frac1{1+\frac{s}{\omega_n}}$ with $\omega_n<0$. The Bode plot will thus include the ``graphical sum'' of three basic plots. 

## Nyquist Plot

An important graphic tool for analyzing the stability of closed-loop systems is the Nyquist plot. It builds on the following important result from complex analysis.

````{prf:theorem}
:label: thm:argument

(Cauchy's argument principle) Let $\Gamma$ be a simple closed curve in the complex plane oriented in the clockwise direction. Let $H:\mathbb{C}\to\mathbb{C}$ be a complex function such that 

1. $H$ is analytic on $\Gamma$, and
2.$H$ is analytic on the domain inside $\Gamma$ except perhaps on a finite number of points.

Let

- $P$ be the number of poles of $H$ inside $\Gamma$,
- $Z$  be the number of zeros of $H$ inside $\Gamma$,
- $N$ be the number of times that the plot $H(\Gamma)$ encircles the origin in the counter-clockwise direction.

Then

```{math}
:label: eq:N=P_minus_Z

N=P-Z.

```
````

In other words, every pole of $H$ inside $\Gamma$ contributes one counter-clockwise rotation of $H(\Gamma)$ around the origin, and every zero of $H$ inside $\Gamma$ contributes one  clockwise rotation of $H(\Gamma)$ around the origin.

```{prf:example}
:label: exa:pi1

Consider the curve $\Gamma_1=2e^{j\theta}-7$, with $\theta=0^\circ\downarrow -360^\circ$, that is, a circle of radius 2 centered at $-7$ in the complex plane,   in the clockwise direction. Consider $H(s)=\frac1{s+7}$.
Then $H$ has no zeros, and one pole at $-7$, so $Z=0$, $P=1$. To plot $H(\Gamma_1)$, that is, $H(s)$ as $s$ moves along $\Gamma_1$, we calculate 
 
$$
    H(\Gamma_1)& = \frac1{(2e^{j\theta}-7)+7}\\
        &=\frac1{2}e^{-j\theta}.
$$

Since $\theta=0^\circ\downarrow -360^\circ$, we have that $H(\Gamma_1)$ is a circle with radius $1/2$ around the origin in the counter-clockwise direction, so $N=1$. We see that $N=P-Z$.
```



```{prf:example}
:label: exa:pi2

Consider the curve $\Gamma_2=2e^{j\theta}$, with $\theta=0^\circ\downarrow -360^\circ$, that is, a circle of radius 2 centered at $0$ in the complex plane,    in the clockwise direction. Consider $H(s)=\frac1{s+7}$. Then $Z=0$, $P=0$.  To plot $H(\Gamma_2)$, that is, $H(s)$ as $s$ moves along $\Gamma_2$, we calculate  

$$
    H(\Gamma_2)& = \frac1{(2e^{j\theta})+7}\\
    &=\frac{ 2e^{-j\theta} +7}{(2e^{j\theta} +7)(2e^{-j\theta} +7) }\\
    &=\frac{ 2e^{-j\theta} +7}{53+28\cos(\theta) }
$$

The numerator here  is a circle or radius 2 centered at $7$. The denominator is always a positive number larger than $1$. Thus, $N=0$ and we see that $N=P-Z$. 
```


{prf:ref}`thm:argument` implies that by knowing any two out of $N,P,Z$, we can deduce the third value. 

 
Let $G $ be the 
loop gain of a closed-loop system. The sensitivity function is then $\frac{1}{1+G}$. Suppose that
$G(s)=n(s)/d(s)$, so that 

$$
S=\frac{d}{d+n}.
$$

The zeros of $S$ are just the zeros of $d$, which are the poles of $G$. To determine the  stability of $S$, we need to determine how many poles it has in the right-hand side of the complex plane. 

Introduce a special curve, denoted $\Gamma_N$,  that includes three parts:


1. $s=j\omega$ with $\omega =0 \uparrow \infty$,
2. $s=Re^{j\theta}$ with $R\to\infty$ and $\theta =90^\circ \downarrow  -90^\circ$,
3. $s=j\omega$ with $\omega =-\infty \uparrow 0$,

see {numref}`fig:gamman`. Thus, $\Gamma_N$ encircles the right-half plane in the clockwise direction.


## Nyquist Stability Theorem

The Nyquist plot of $G$ is the plot $G(\Gamma_N)$.

```{prf:theorem}
:label: thm:nyq_general

Let $G=n/d$ be the ratio of two polynomials such that $G$ has no poles on the imaginary axis.  Let  

- $P$  be the number of poles of $G$ in the right-half plane,
- $N$ be the number of counter-clockwise rotations of $G(\Gamma_N)$ around the point $-1$ in the complex plane.

Then the number of poles of $S=\frac1{1+G}$ in the right-half plane is $P-N$.
```

Thus, $S$ is stable if and only if $P=N$.

```{admonition} Exercise
Prove  {prf:ref}`thm:nyq_general` based on  {prf:ref}`thm:argument`.
```

```{figure} images/nyquist_contour.png
---
width: 90%
name: fig:gamman
---
The curve $\Gamma_N$ includes three  parts.
```


```{prf:example}
Consider $G(s)=\frac{s^2+100.1s+10}{s^2+5s+100}$. The denominator is a second-order polynomial with positive coefficients, so $P=0$.
The Nyquist plot of  $G$ is depicted in {numref}`fig:nyqui_PL_G`, and we see that $N=0$. Thus, the number of unstable poles of
$S=\frac1{1+G}$ is zero, so $S$ is stable.  
```

```{figure} images/nyquist_1.png
---
width: 90%
name: fig:nyqui_PL_G
---
Nyquist plot $G(\Gamma_N)$ for  $G(s)=\frac{s^2+100.1s+10}{s^2+5s+100}$.
```

```{prf:remark}
:label: rem:modified_nyquist
   
If $G$ has poles on the imaginary  axis then the Nyquist theorem can still be used once  the curve $\Gamma_N$ is modified. Suppose that $G$ has a pole $ja$, with $a\geq 0 $, and then also a pole $-ja$. Then $\Gamma_N$ should be modified to include the following parts: 

1. $s=j\omega$ with $\omega =0 \uparrow a^-$,
2. $s=ja+r e^{j\theta}$ with $r\to 0 $ and $\theta =-90^\circ \uparrow  90^\circ$,
3. $s=j\omega$ with $\omega =a^+ \uparrow \infty$,
4. $s=Re^{j\theta}$ with $R\to\infty$ and $\theta =90^\circ \downarrow  -90^\circ$ ,
5. $s=j\omega$ with $\omega =-\infty \uparrow -a^+$,
6. $s=-ja+r e^{j\theta}$ with $r\to 0 $ and $\theta =-90^\circ \uparrow  90^\circ$,
7. $s=j\omega$ with $\omega =-a^- \uparrow 0$,

see {numref}`fig:modified_nyq`.
```

```{figure} images/nyquist_contour_with_poles.png
---
width: 90%
name: fig:modified_nyq
---
The modified curve $\Gamma_N$ when $G$ has poles at $ja$ and $-ja$.
```

If $G$ is stable then the value $P$ defined  in {prf:ref}`thm:nyq_general` satisfies $P=0$, and this yields the following result. 

```{prf:theorem}
:label: thm:nyq_special

Let $G=n/d$ be the ratio of two polynomials such that $G$ is stable.  Then $S=\frac1{1+G}$ is stable 
if and only if the Nyquist plot $G(\Gamma_N)$ does not encircle (or hit) 
the point $-1$ in the complex plane.
```



## Drawing the Nyquist Plot

There are several ways to draw $G(\Gamma_n)$. Note that to apply the Nyquist stability criterion the plot does not have to be completely  accurate, as the only information we need is the number of rotations around the point $-1$ in the complex plane. 

Recall that when $G$ has no poles on the imaginary axis, $\Gamma_n$ includes three parts:

1. $s=j\omega$ with $\omega =0 \uparrow \infty$,
2. $s=Re^{j\theta}$ with $R\to\infty$ and $\theta =90^\circ \downarrow  -90^\circ$,
3. $s=j\omega$ with $\omega =-\infty \uparrow 0$,

see {numref}`fig:gamman`.


The transfer function $G$ is typicality the proper ratio of two polynomials with real coefficients. This implies that: (1) the arc 
$s=Re^{j\theta}$, with $R\to\infty$ and $\theta =90^\circ \downarrow  -90^\circ$, is mapped by $G$ to a single point; and (2) the plots $G(j\omega)$ for $\omega=-\infty \uparrow 0$ and for $\omega=0\uparrow \infty$ are symmetric with respect to the real axis.  

Consider thus $G(j\omega)$ with $\omega:0\uparrow\infty$. The magnitude and angle of every point on this curve is exactly the information  in the Bode plot of $G$. 
We conclude that one  possibility is to first draw the Bode plot of $G$ and then use this to draw the Nyquist plot. 

```{prf:example}
Consider the transfer function $G(s)=\frac{s^2+100.1s+10}{s^2+5s+100}$. The Bode plot of $G$ is depicted in  {numref}`fig:bode_for_nyquist`.
We will use this to plot the Nyquist curve for $G$. Consider $G(j\omega)$ with $\omega:0\uparrow \infty$. For $\omega=0$, we have $G(j0)=\frac{10}{100}=0.1$. This corresponds to 
$|G(j0)|=-20dB$ and $\arg G(j0)=0^\circ$. As $\omega$ increases,  we see from the Bode plot that first the gain increases and the phase increases to almost $90^\circ$. Then 
the angle decreases to $0^\circ$,   to $\approx -45^\circ $ and then increases again to $0^\circ$. This yields the solid curve in the Nyquist plot of $G$ in  {numref}`fig:nyqui_PL_G`. This curve ends at the point 

$$
\lim_{\omega\to\infty} G(j\omega)=\lim_{\omega\to\infty}\frac{(j\omega)^2}{(j\omega)^2}=1.
$$

The arc $s=Re^{j\theta }$, with $R\to\infty$, is also mapped by $G$ to the point $1$. The part $s=j\omega$, with $\omega:-\infty\uparrow 0$ is mapped to a plot that is symmetric with respect to the real axis to the plot we already generated. This completes the Nyquist plot in {numref}`fig:nyqui_PL_G`.
```

```{figure} images/bode_plot_of_g.png
---
width: 90%
name: fig:bode_for_nyquist
---
Bode plot $G(\Gamma_N)$ for  $G(s)=\frac{s^2+100.1s+10}{s^2+5s+100}$.
```

Another way to draw the Nyquist plot is by substituting the parametric representation of $\Gamma_N$ in $G $. The next example demonstrates this. 

```{prf:example}
Consider again the transfer function $G(s)=\frac{s^2+100.1s+10}{s^2+5s+100}$. To plot $G(\Gamma_N)$, we begin by substituting $s=j\omega$ in $G(s)$. This gives

$$
        G(j\omega)&= \frac{-\omega^2+100.1j\omega+10}
        {100-\omega^2+5j\omega }\\
        &=\frac{\omega^4+395.5\omega^2+1000+j(-96.1\omega^2+10060 )\omega }{(100-\omega^2)^2+(5\omega)^2}.
$$
	
Suppose that $\omega=0\uparrow \infty$. The real part of $G(j\omega )$ is always positive. For $\omega=0$, we get

$$
    G(j0) =\frac{1000}{100^2}=0.1.
$$

As $\omega$ increases from $0$ to $\infty$,  we see that for small values of $\omega$ we have that  $\text{Img}(G(j\omega))$ is positive, so the curve is in the first orthant. For $\omega\approx 10$, we get $\text{Img}(G(j\omega))=0$, so the curve crosses the positive part of the real axis. As $\omega$ further increases, the imaginary part remains negative, and as $\omega\to \infty$, we get

$$
    \lim_{\omega\to\infty}G(j\omega)  =\lim_{\omega\to\infty}\frac{\omega^4  }{ \omega^4}=1.
$$

This yields the solid curve in  {numref}`fig:nyqui_PL_G`.
The part $s=Re^{j\theta}$ with $R\to infty$ is mapped by $G$ to the point $1$. The part $s=j\omega$, with $\omega:-\infty\uparrow 0$ is mapped to a plot that is symmetric with respect to the real axis to the plot we already generated. This completes the Nyquist plot in  {numref}`fig:nyqui_PL_G`.
```

## Stability Margins

So far, we considered stability as a binary problem: the closed-loop system is stable or not. The Nyquist stability theorem allows to derive a notion of stability margins by testing ``how far'' is the Nyquist plot $G(\Gamma_N) $ from encircling the point $-1$.

### Gain Margin

We consider the loop gain $G=PC$. 

```{prf:definition}
Let $\omega_c>0$ be the frequency such that $G(j\omega_c)$ is real and negative. The gain margin (GM) of $G$ is

$$
-20 \log |G(j\omega_c)| \text{ (in dB).}
$$

```

Generally speaking, a larger gain margin implies ``more stability'' of $S=\frac1{1+G}$. To explain this, let $ x:=-G(j\omega_c)$,  so $x>0$. If $x=1$ then $G(j\omega_c)=-1$, so the Nyquist plot $G(\Gamma_N)$ ''touches'' the point $-1$. We would thus like the difference $-x-(-1)$ to be as large as possible, that is,    that the difference $\frac1{|G(j\omega_c)|}-1$ will be large as possible, that is, that the GM will be as large as possible. 

If there is no frequency $\omega_c$ such that $G(j\omega_c)=-180^\circ$ then GM is defined as infinity. 

The GM can be read from the Bode plot of $G$. 

```{prf:example}
Let $G(s)=\frac{10}{s(1+0.2s)(1+0.02s)}$. {numref}`fig:GM` depicts a Bode plot of $G$. From this plot, we first find  the frequency $\omega_c$  where $G(j\omega_c)=-180^\circ$ (this is marked by an arrow in the figure).  Then the 
     GM of $G$ is  the distance  in dB between $G(j\omega_c) $ and the value 0 dB.
```

```{figure} images/bode_plot_of_G1.png
---
width: 90%
name: fig:GM
---
Gain and phase margins of $G(s)=\frac{10}{s(1+0.2s)(1+0.02s)}$.
```


### Phase Margin

Another measure of quantitative   stability of the closed-loop system  is the phase margin.

```{prf:definition}
Let $\omega_g>0$ be the frequency such that $|G(j\omega_g)|=1$. The phase margin of $G$ is

$$
    \arg(G(j\omega_g))-(-180^\circ) \text{ (in degrees)}.
$$
```
To explain this, note that if $\arg(G(j\omega_g))=-180^\circ$ then $G(j\omega_g)=-1$, so the Nyquist plot $G(\Gamma_n)$ ``touches'' the point $-1$. 

Generally speaking, a larger phase  margin implies ''more stability'' of $S=\frac1{1+G}$.

If there is no frequency $\omega_g$ such that $|G(j\omega_g)|=1$ then PM is defined as infinity.

The PM can be read from the Bode plot of $G$.

```{prf:example}
Let $G(s)=\frac{10}{s(1+0.2s)(1+0.02s)}$. {numref}`fig:PM` depicts a Bode plot of $G$. From this plot, we first find  the frequency $\omega_g$  where $G(j\omega_g)$ is 0 dB  (this is marked by an arrow in the figure).  Then the  PM of $G$ is  the distance   between $\arg (G(j\omega_g) )$ and the value $-180^\circ$.
```

```{figure} images/bode_plot_of_G_with_PM.png
---
width: 90%
name: fig:PM
---
Gain and phase margins of $G(s)=\frac{10}{s(1+0.2s)(1+0.02s)}$.
```


```{prf:example}
Suppose that the plant $P(s)=\frac{50}{s(s+1)(s+10)}$ is controlled in a closed-loop system with controller $C(s)=1$. We compute the GM and PM.     In this case, $G(s)=P(s)$, so

$$
G(j\omega) = \frac{50}{j\omega(j\omega+1)(j\omega+10)}=
\frac{1}{\omega}\cdot\frac{-550\omega+(50\omega^2-500)j}{\omega^4+101\omega^2+100}.
$$

We see that $G(j\omega)$ will be real and negative at the frequency $\omega_c=\sqrt{10}\approx 3.16$. At this frequency, we have

$$
G(j\omega_c) =\frac1{\sqrt{10}} \cdot \frac{-550\sqrt{10}}{100+1010+100}=\frac{-55}{121}.
$$

Thus,

$$
GM=-20\log |\frac{-55}{121} |=6.85\; \text{dB}. 
$$

We turn to computing PM. 

$$
|G(j\omega)| & =
\frac{1}{\omega}\cdot\frac{ \sqrt{(550\omega)^2+(50\omega^2-500)^2}}{\omega^4+101\omega^2+100}\\
&=\frac1{\omega}\cdot \frac{50\sqrt{\omega^4+101\omega^2+100} }{\omega^4+101\omega^2+100}\\
&=\frac{1}{\omega}\cdot\frac{50}{\sqrt{\omega^4+101\omega^2+100}}.
$$

We look for a frequency $\omega_g$ such that $|G(j\omega_g)|=1$, that is, 
$50=\omega_g \sqrt{\omega_g^4+101\omega_g^2+100}$, so

$$
2500=\omega_g^6+101\omega_g^4+100\omega_g^2.
$$

Letting $v_g:=\omega_g^2$ gives

$$
2500=(v_g^2+101v_g+100 )v_g,
$$

so $v_g=4.42$ and $\omega_g=2.1$. At this frequency, 

$$
\arg G(j\omega_g)&=\arg (-500\cdot 2.1+(50\cdot 2,1^2-500)j)\\
&= \arg (-1155-279.5 j )\\
&=-90^\circ-\tan^{-1}(\frac{1155}{279.5})\\
&=-166.4^\circ.
$$

Thus,

$$
PM=\arg G(j\omega_j)+180^\circ=13.6^\circ.
$$
```


```{prf:remark}
Usually, $GM\geq 6$ dB and $PM \geq 30^\circ$ are considered to be good. 
```

So far, we  considered the GM and PM as tools to analyze how stable a given  closed-loop system is. But, these can also be used as design specifications. 

## Control Synthesis in the Frequency Domain

We begin with an example.

````{prf:example}
Consider a closed-loop system composed of a plant 

$$
    P(s)=\frac{1}{s(1+s)(1+\frac{s}{80})},
$$
	
and a controller $C$. Design $C$ such that


1. the closed-loop system is stable;
2. the steady-state error for a ramp input is no more than $1\%$, that is, $|e_{ss}(ramp)|\leq 0.01$.

We begin by trying a gain controller $C(s)=k$. The closed-loop transfer function is 

$$
    \frac{\hat y(s)}{\hat r(s)} = \frac{P(s)C(s)}{1+P(s)C(s)}
=\frac{kP(s)}{1+kP(s)}  ,  
$$

so for ramp input 

$$
e_{ss}(ramp)&= \lim_{s\to 0} \frac1{skP(s)}\\
&=
\frac1{k},     
$$

assuming that the limit exists. To satisfy the second requirement, we must take $k\geq 100$. 

Set $k=100$. To analyze the stability of the closed loop system, we draw a Nyquist plot of $100P(s)$. Note that since $P$ has a pole at the origin, we use a modified $\Gamma_N$ as explained in {prf:ref}`rem:modified_nyquist`.
The Nyquist plot of $100P(s)$
is depicted in {numref}`fig:nyq_100`. 

```{figure} images/nyquist100new.png
---
width: 90%
name: fig:nyq_100
---
Nyquist plot of $100P(s)$.
```


To analyze stability of the closed-loop system, we calculate the value $-x$ in the figure. Note that

$$
    100P(j\omega)&=\frac{100}{j\omega(1+j\omega)(1+\frac{j\omega}{80})}\\
    &=\frac{-100j}{ \omega(1+j\omega)(1+\frac{j\omega}{80})}\\
    &=\frac{ -101.25  \omega -100 j( 1-\frac{\omega^2}{80})}
    {\omega(1+\omega^2)(1+(\frac{\omega}{80})^2)}  . 
    %%%%%
$$

Thus, the frequency $\omega_g$ such that $100P(j\omega_g)$  is $\omega_g=\sqrt{80}$, and at this frequency we have


```{math}
:label: eq:8081
    100P(j\omega_g)
    &=\frac{ -101.25  \sqrt{80}  }
    {\sqrt{80} (1+80)(1+(\frac{1}{\sqrt{80} })^2)}\nonumber\\&=-100/81.
```

Thus, $-x=-100/81<-1$ and this implies that the Nyquist plot in {numref}`fig:nyq_100` includes two encirclements of the point $-1$ in the CW direction. We now apply {prf:ref}`thm:nyq_general` (see also {prf:ref}`rem:modified_nyquist`). 
The number of poles   of $100P$ in the right-half plane is zero. The number of   of CCW rotations of $100P(\Gamma_N)$ around the point $-1$ in the complex plane is $-2$, so the number of right-half poles of $S=\frac1{1+100P}$   is $2$ and, in particular, the closed-loop system is unstable. It follows from {eq}`eq:8081` that the closed-loop system is unstable for any $k>81$.
  

The conclusion from this example is that we require a controller in the form $kC$, with $k\geq 100$, 
such that $C$ stabilizes the closed-loop system. 
````

### Phase Lead Compensator

A phase lead compensator is a network that introduces a positive phase shift to a system's frequency response, thereby improving its transient response and increasing its stability margins.

The phase lead compensator has the form

```{math}
:label: eq:plc

C(s)=\frac{1+\tau s}{1+\alpha \tau s} \text{  with  } 0<\tau, \;0<\alpha<1. 
```

Note that this is in normalized form in the sense that $C(0)=1$, so it will not affect the value of the steady state error. 
The  phase lead compensator has a stable zero at $-1/\tau$, and a stable pole at $-1/(\alpha\tau)$.  
An asymptotic Bode plot of $C$ is depicted in {numref}`fig:asym_bode` in blue line. An accurate plot (red dashed line) is also shown.  

```{figure} images/asym_bode.png
---
width: 90%
name: fig:asym_bode
---
Bode plot of the phase lead compensator. Blue line: asymptotic plot; Red dashed line: accurate plot.
```


It may be seen that $C$ always has a positive phase. This implies that for any plant $P$ we have that $PC$ has a higher gain margin than $P$. Furthermore, there is a unique frequency $\omega_M$ such that $\phi_M:=\arg(C(j\omega_M))$ is the maximal   phase   that $C$ can contribute, with

```{math}
:label: eq:bounds_omega_M
0^\circ<\phi_M<90^\circ.
```

Note that $C(j\omega)=\frac{1+\tau j\omega}{1+\alpha\tau j \omega}$, so 

$$
\arg(C(j\omega))=\tan^{-1}(\tau\omega)-\tan^{-1} (\alpha\tau\omega).
$$

Using the formula

$$
\tan(a-b)=\frac{\tan(a)-\tan(b)}{1+\tan(a)\tan(b)}
$$

yields

```{math}
:label: eq:tan_arg
\tan(\arg(C(j\omega)))=\frac{\tau\omega(1-\alpha )}{1+\alpha\tau^2\omega^2}.
```

Differentiating this with respect to $\omega $ and comparing to zero gives

$$
0=1-\alpha \tau^2 \omega^2,
$$

so

```{math}
:label: eq:oemag_M

\omega_M=\frac1{\tau \sqrt{\alpha}}.
```

Note that $\frac{1}{\tau}<\omega_M <\frac{1}{\alpha\tau}$ (see {numref}`fig:asym_bode`). Using {eq}`eq:tan_arg` we get that the maximal phase satisfies

$$
\tan(\phi_M)=\frac{\tau\omega_M(1-\alpha )}{1+\alpha\tau^2\omega_M^2} 
= \frac{1-\alpha}{2\sqrt{\alpha}}.
$$

Using the trigonometric identity $\sin(\theta) =\frac{\tan(\theta)}{\sqrt{1+\tan^2(\theta)}}$ which holds in the range $\theta\in[0^\circ,90^\circ]$ (see {eq}`eq:bounds_omega_M`) gives 

$$
\sin(\phi_M)=\frac{1-\alpha}{1+\alpha}, 
$$

or

```{math}
:label: eq:alpha_and_phi_M

\alpha = \frac{1-\sin(\phi_M)}{1+\sin(\phi_M)}.
```

A calculation shows that

```{math}
:label: eq:c_mag_at_phi_M

20\log(  |C(j\omega_M)|)\approx \frac1{2} 20 \log (\frac1{\alpha})=-10\log(\alpha).
```

We now have all the data needed to design a phase lead compensator $C$ 
as a controller: 

1. Draw Bode plots of the plant $P$ and determine GM and PM;
2. Calculate, according to the design specifications, the needed additional phase, and set $\phi_M$ to be this value;
3. Obtain the parameter $\alpha$ of $C$ from {eq}`eq:alpha_and_phi_M`;
4. Find  a frequency $\omega_1>0$ such that $20\log|P(j\omega_1)|=10\log(\alpha)$, and set $\omega_M=\omega_1$.  Obtain the parameter $\tau$ of $C$ from {eq}`eq:oemag_M`;
5. Since $\alpha,\tau$ have been determined, this completes the design of $C$. Verify that the closed-loop system satisfies the design specifications. 

To explain this procedure, note that

$$
    20\log|P(j\omega_1)C(j\omega_1)| &= 20\log|P(j\omega_1)|+ 20\log|C(j\omega_1)|\\
    &=10\log(\alpha) +20\log|C(j\omega_M)|\\
    &=10 \log(\alpha) -10\log(\alpha)\\&=0.
$$

Thus, the frequency where we compute  the PM of the system is $\omega_1=\omega_M$, and this is the frequency where $C$ provides the maximal phase $\phi_M$.

```{prf:example}
Consider the plant

$$
    P(s)=\frac{100}{s(1+0.04 s)}.
$$

Design a closed-loop controller such that:


1. PM $\geq 45^\circ$; and
2. the steady state error to a ramp input  $\leq 1\%$.

We will design a controller in the form $kC$, with $C$ a phase lead compensator. We first determine the gain $k$ based on the steady state error requirement

$$
    e_{ss}(ramp) &= \lim_{s\to 0}\frac1{s(1+kP(s)C(s))} \\
    &=\frac{0.01}{k}.
$$

 
Thus, it is enough to take $k=1$. {numref}`fig:bode_plot_kp` 
depicts a Bode plot of $kP=P$. 
We see that PM=$28^\circ$, attained at the frequency $\omega_c=47$ (rad/sec), so the PM requirement does not hold.
To meet the requirement PM$\geq 45^\circ$, we design a compensator with $\phi_M=25^\circ$. Now {eq}`eq:alpha_and_phi_M` gives

$$
\alpha=\frac{1-\sin(25^\circ)}{1+\sin(25^\circ)}\approx 0.40586.
$$

The next step is to determine the frequency $\omega_1$ such that
 
$$
|kP(j\omega_1)|_{dB}=10\log(\alpha)=-3.91625. 
$$

From the Bode plot we find that $\omega_1\approx 60$, so we set $\omega_M=60$. Now {eq}`eq:oemag_M` gives

$$
\tau=0.02616.
$$

Summarizing, the designed controller is

$$
k \frac{1+\tau s}{1+\alpha \tau s } = k\frac{1+0.2616 s}{1+0.0106 s},
$$

with $k=1$, and

$$
P(s)C(s)= \frac{100}{s(1+0.04s)}\cdot \frac{1+0.2616 s}{1+0.0106 s}.
$$

{numref}`fig:bode_corrected` shows the Bode plot of $PC$. Now   PM=$47.6^\circ$.

```

```{figure} images/bode_p_k1.png
---
width: 90%
name: fig:bode_plot_kp
---
Bode plot of $kP=P$.
```

```{figure} images/bode_corrected_plc.png
---
width: 90%
name: fig:bode_corrected
---
Bode plot of $PC$.
```
