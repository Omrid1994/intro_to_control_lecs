
```{tableofcontents}
```



# Chapter 0: Matrix Theory 

Control theory uses tools from many fields of mathematics, including matrix theory, complex analysis, and the qualitative theory of dynamical systems. Here, we review some required tools from matrix theory.



Let $x^1, \dots, x^n$ denote $n$ vectors in $\mathbb{R}^n$. The vectors are said to be linearly independent if the equation:

$$
c_1 x^1 + \dots + c_n x^n = 0,
$$

with $c_i \in \mathbb{R}$, holds only for the trivial choice $c_1 = \dots = c_n = 0$. If the vectors are linearly independent, then they span $\mathbb{R}^n$, that is, for any $v \in \mathbb{R}^n$, there exist $d_1, \dots, d_n \in \mathbb{R}$ such that:

$$
d_1 x^1 + \dots + d_n x^n = v.
$$

Let $ \mathbb{R}^{n \times n} $ denote the set of all $n \times n$ real matrices. Let $I_n$ be the $n \times n$ identity matrix. Let $e^i$ denote the $i$-th column of $I_n$.



````{prf:definition}
:label: def:singular_matrix
A matrix $ A \in \mathbb{R}^{n \times n} $ is called <em>invertible (non-singular)</em> if there exists a matrix $ B \in \mathbb{R}^{n \times n} $ such that:
$
AB = I_n.
$
In this case, $ B $ is called the <em>inverse</em> of $ A $ and is denoted by $ A^{-1} $, so that:
$
A A^{-1} = I_n.
$
````

```{admonition} Exercise - Singular Matrix Example
Show that the matrix $
A = \begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix}
$ is not invertible.
```

```{admonition} Solution
:class: dropdown
If $ A $ is invertible, then there exists a matrix $ B $ such that $ AB = I_2 $, that is:

$$
\begin{bmatrix} 0 & 0 \\ b_{21} & b_{22} \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}.
$$

Clearly, this is impossible, so $ A $ is singular.
```


```{prf:proposition}
:label: prop:linear_ind
The matrix $A\in\mathbb{R}^{n\times n}$ is invertible iff the columns of $A$ are linearly independent.
```

````{prf:proof}
Let $e^i\in\mathbb{R}^n$ denote the $i$th column of $I_n$.     Suppose that the columns of $A$, denoted $a^1,\dots,a^n$, are linearly independent. Then the equation $Ar^i=e^i$ admits a solution $r^i\in \mathbb{R}^n$ for any $i\in\{1,\dots,n\}$. Thus,

  $$
  A \begin{bmatrix}
      r^1&r^2&\dots&r^n  \end{bmatrix}=I_n,
  $$
  
  so $A$ is invertible,
  with $A^{-1}=\begin{bmatrix}
      r^1&r^2&\dots&r^n 
  \end{bmatrix}$. 
  
  Now suppose that the columns of $A$ are not linearly independent. Then there exists $v\in \mathbb{R}^n\setminus\{0\}$ such that $Av =0$. Seeking a contradiction, assume that $A$ is invertible. Then 
there exists $A^{-1} $ such that 

$$
A A^{-1} =I_n.   
$$

If the columns of $A^{-1}$ are not linearly independent then there exists $w\in \mathbb{R}^n\setminus\{0\}$ such that $A^{-1} w =0 $, so $A A^{-1} w =0 $, but this is not possible as $AA^{-1}=I_n$. We conclude that the columns of $A^{-1}$ are   linearly independent. Then the equation $A^{-1} z = v$ admits a solution $z\in \mathbb{R}^n\setminus\{0\}$, and $AA^{-1} z =Av =0$. This is a contradiction, as $A A^{-1}=I_n$. This completes the proof of Proposition  {prf:ref}`prop:linear_ind`. 
````
  
   

## Eigenvalues and Eigenvectors

````{prf:definition}
:label: def:eigvalue_eigenvector
A pair $ \lambda \in \mathbb{C}, v \in \mathbb{C}^n \setminus \{0\} $ is called an <em>eigenvalue-eigenvector pair</em> of $ A $ if:

```{math}
:label: eq:eigenvalue_equation
Av = \lambda v.
```
````

````{admonition} Exercise
:label: exercise:eigenpairs
Let $A=\begin{bmatrix}0&-1\\1&0\end{bmatrix}$. Show that$\Big(i,\begin{bmatrix}1\\-i\end{bmatrix}\Big)$ and $\Big(-i,\begin{bmatrix}1\\i\end{bmatrix}\Big)$ are a pair of eigenvalue-eigenvectors of $A$. Here $i:=\sqrt{-1}$.
````

````{admonition} Solution
:class: dropdown
   Let $\lambda=i$ and $v=\begin{bmatrix}1\\-i\end{bmatrix}
   $. Then 
   
```{math}
         Av&=\begin{bmatrix}
             0&-1\\1&0 
         \end{bmatrix}
         \begin{bmatrix}
            1\\-i
         \end{bmatrix}
         =\begin{bmatrix}
            i\\1
         \end{bmatrix}
 ```
	
whereas

$$
           \lambda v&= i  \begin{bmatrix}
            1\\-i
         \end{bmatrix}
         =\begin{bmatrix}
            i\\1
         \end{bmatrix}, 
$$

so $A v =\lambda v$. A similar calculation shows that
 $\Big(-i,\begin{bmatrix}1\\i\end{bmatrix}\Big)$ is also an eigenvalue-eigenvector pair. 

````

````{prf:remark}
Note that combining Definitions {prf:ref}`def:singular_matrix` and {prf:ref}`def:eigvalue_eigenvector` with the fact that $\det(A)$ is the product of the eigenvalues of $A$
    implies that 
	
$$	
	A \text{ is singular } \iff A \text{ has a zero eigenvalue } \iff \det(A)=0,
$$	

where $\iff$ stands  for if and only if (iff).
{eq}`eq:eigenvalue_equation` can be written as

```{math}
:label: eq:eigenvalue_equation2
    \big(\lambda I_n-A\big)v=0.
```
Thus, the eigenvalues of $A$ are the values $\lambda$ such that $\lambda I_n-A$ is a singular matrix, i.e. the roots of the equation
```{math}
:label: eq:det(lambda I-A)=0
    \det\big(\lambda I_n-A\big)=0.
```
Note that this equation admits $n$ solutions $\lambda_1,...,\lambda_n\in\mathbb{C}$.
````

```{admonition} Exercise
	:label: exercise:det=0
Solve equation {eq}`eq:det(lambda I-A)=0` for $A=\begin{bmatrix}0&-1\\1&0\end{bmatrix}$.
```

```{admonition} Solution
:class: dropdown
We have

$$
\det(\lambda I_n-A)=\det\begin{bmatrix}
    \lambda&1\\-1&\lambda
\end{bmatrix}=\lambda^2+1,
$$

and the roots are  $\lambda_1= i $, $ \lambda_2=-i $.
```


```{admonition} Exercise
Let $A,B\in\mathbb{R}^{n\times n}$. Show that if $AB=I_n$ then $BA=I_n$. Hint: use the fact that for any $A_1,A_2 \in\mathbb{R}^{n\times n}$, we have $\det(A_1A_2)=\det(A_1)\det(A_2).$
```

```{admonition} Solution
:class: dropdown
 Assume that $AB=I_n$. Then $\det(A)\det(B)= 1$. Thus, $\det(B)\not =0$, so $B$ is invertible, i.e.  there exists a matrix $B^{-1}$ such that $BB^{-1}=I_n$. Now,

$$
 I_n&= B  I_n B^{-1}\\
 &=B( AB)B^{-1}
  \\&= BA, 
$$

and this completes the proof. 
```

## Diagonalizable Matrices

````{prf:definition}
A matrix $A\in\mathbb{R}^{n\times n}$ is called <em>diagonalizable</em> if it is similar to a diagonal matrix, that is, if there exists an invertible matrix $T\in\mathbb{C}^{n\times n}$   such that $ T^{-1}AT$ 
is diagonal.
````

````{prf:example}
Suppose that $A$ admits $n$ linearly independent eigenvectors $v^1,\dots,v^n\in\mathbb{C}^n$. 
Let $T:=\begin{bmatrix}
    v^1 &v^2 &\dots& v^n
\end{bmatrix}$. Then

$$
A T= T \text{diag}(\lambda_1,\dots,\lambda_n),
$$

and thus $T^{-1} A T $ is diagonal, so $A$ is diagonalizable. 
````

Fix $A\in\mathbb{R}^{n\times n}$   and denote  its eigenvalue-eigenvector pairs by $(\lambda_i,v^i)$, $i=1,\dots,n$. Suppose that $A $ is diagonalizable, that is, there exists a matrix $T$ such that $T^{-1}AT$ is diagonal. Then
\begin{align*}
    T^{-1}AT (T^{-1} v^i)&= T^{-1}A  v^i \\&= \lambda_i (T^{-1} v^i) ,
\end{align*}
so $T^{-1} v^i$ is an eigenvector of $T^{-1}AT$ corresponding to the eigenvalue $\lambda_i$. Thus, $A $ and $ T^{-1}AT $ have the same eigenvalues. Since $T^{-1}AT$ is diagonal,  these eigenvalues are just the diagonal entries of $T^{-1}AT$.


````{admonition} Exercise
Show that the matrix $A=\begin{bmatrix}
       0&1\\0&0
   \end{bmatrix}$ is not diagonalizable.
````

````{admonition} Solution
:class: dropdown
If $A$ is diagonalizable then there exits an invertible matrix $T$ such that $T^{-1}AT $ is diagonal and has the same eigenvalues as $A$, so

$$ 
  T^{-1}AT=\begin{bmatrix}0&0\\0&0\end{bmatrix}. 
$$
Multiplying this equation by $T$ from the left and $T^{-1}$ on the right gives $A=0$, and this is a contradiction.
````

The fact that not every matrix is diagonalizable is sometimes referred to as the ``main nuisance   of linear algebra''.
However, every matrix is arbitrarily close to a matrix that can be diagonalized. To explain this, define the distance between two matrices $A,B\in\mathbb{R}^{n\times n}$ by

$$
\|A-B\|:=(\sum_{i,j}(a_{ij}-b_{ij})^2)^{1/2}. 
$$

````{prf:proposition}
:label: prop:B_close_diagonalizbe
Let $A\in\mathbb{R}^{n\times n}$. Fix $\varepsilon>0$. Then there exits a matrix $B$ such that $B$ is diagonalizable and $\|A-B\|\leq \varepsilon$. 
````

````{admonition} Exercise 
Consider again the matrix $A=\begin{bmatrix}
       0&1\\0&0
   \end{bmatrix}$. Fix $\varepsilon>0$. Find a matrix $B$ such that $B$ is diagonalizable and $\|A-B\|\leq \varepsilon$. 
````


## The Cayley-Hamilton Theorem


````{prf:definition}
The <em>characteristic polynomial</em> of an $n\times n$ matrix $A$ is 
```{math}
:label: eq:def_char_poly
    p_A(\lambda) : =\det(\lambda I_n-A).
```
````

 Note that $p_A(\lambda)$ is a polynomial of degree $n$  in $\lambda$, so it can be written as
 
$$
    p_A(\lambda)=\lambda^n+c_{n-1}\lambda^{n-1}+...+c_1 \lambda+c_0.
$$
In particular, $p_A(0)=c_0$ and using {eq}'eq:def_char_poly' gives $c_0=\det(-A)=(-1)^n\det(A)$.
    
Replacing the scalar variable $\lambda$ with the matrix $A$, one can define an analogous \emph{matrix polynomial} expression,

$$
    p_A(A)=A^n+c_{n-1}A^{n-1}+...+c_1 A+c_0 I_n.
$$

````{prf:theorem} The Cayley-Hamilton Theorem
:label: thm:cayley_hamilton
Let $A\in\mathbb{R}^{n\times n}$. Then
	
$$
    p_A(A)=0.
$$
Note that here $''0''$ is the zero $n\times n$ matrix.
````

````{admonition} Exercise
Prove the Cayley-Hamilton Theorem for diagonal  matrices, and then for diagonalizable matrices. 
````

One implication of the Cayley-Hamilton Theorem is that 

```{math}
:label: eq:expressan
A^n=-c_{n-1}A^{n-1}-...-c_1 A-c_0 I_n,
```
that is, we can express $A^n$ as a weighted sum of matrices in the set $\mathcal A:=\{A^0,\dots,A^{n-1}\}$. Multiplying {eq}`eq:expressan` by $A$ gives 

```{math}
:label: eq:recurrence
\begin{aligned}
A^{n+1} &= -c_{n-1}A^{n} - ... - c_1 A^2 - c_0 A,
\end{aligned}
```

and since we can express $A^n$ as a weighted sum of matrices in $\mathcal{A}$, we conclude that we can express $A^{n+1}$ a as weighted sum of matrices in $\mathcal{A}$. 
Continuing in this fashion we conclude that we can express any $A^k$, $k\geq n$, as a weighted sum of matrices in $\mathcal{A}$.

## Matrix Exponential



````{prf:definition}
The matrix exponential of $A\in\mathbb{R}^{n\times n}$, denoted $e^A$ or $\exp(A)$,  is the $n\times n$ matrix defined by
```{math}
:label: eq:def_exp_matrix
    e^A=\sum_{k=0}^\infty \frac{A^k}{k!}, 
```
where $A^0:=I_n$.
````
Consider the following linear time-invariant (LTI) system
```{math}
:label: eq:homo_lti
    \dot{x}(t)&=Ax(t),\\
     x(0)&=x_0,\nonumber
```
where $x_0\in\mathbb{R}^n$, $A\in\mathbb{R}^{n\times n}$. The solution of {eq}`eq:homo_lti` at time $t$ 
is
$$
    x(t)=e^{At}x_0.
$$

To prove this, define $z(t):=e^{At}x_0$.  Then

$$
    z(0)=e^{A0}x_0=I_nx_0=x_0.
$$

Also, differentiating $z(t)$ gives 

$$
        \dot{z}(t)&=\frac{d}{dt}\Big(I_n+\frac{At}{1!}+\frac{A^2t^2}{2!}+\mathbb{C}dots\Big)x_0\\
        &=\Big(0+\frac{A}{1!}+\frac{2A^2t}{2!} +\frac{3A^3t^2}{3!}+\mathbb{C}dots\Big)x_0\\
        &=A\Big(I_n+\frac{At}{1!}+\frac{A^2t^2}{2!}+\mathbb{C}dots\Big)x_0\\
        &=Az(t).
$$

Thus, $z(t)$ satisfies the same differential equation as $x(t)$, with the same initial condition. By uniqueness of the solution of the LTI, this implies that $x(t)=z(t)=e^{At}x_0$.

Let $D=\text{diag}(\lambda_1,\dots,\lambda_n)$ denote the $n\times n$ diagonal matrix with diagonal entries $\lambda_i$. Its exponential is given by:

```{math}
:label: eq:exp_diag
e^D=\text{diag}(e^{\lambda_1}, e^{\lambda_2}, \dots, e^{\lambda_n}).
```

(prove this).

Suppose that $A$ is diagonalizable,
that is, there exists an invertible matrix $T\in\mathbb{C}^{n\times n}$   such that $ D:=T^{-1}AT=\text{diag}(\lambda_1,\dots,\lambda_n)$. Then $A=TDT^{-1}$ yields $A^2=TD^2T^{-1}$, and continuing in this way gives $A^k=TD^k T^{-1}$ for any integer $k\geq 0$. Now Eq. {eq}`eq:def_exp_matrix` yields
 
$$
    e^{At}&= Te^{Dt}T^{-1}\\
    &=T\text{diag}(e^{\lambda_1 t},\dots,e^{\lambda_n t})T^{-1} . 
$$ 

This can be used to calculate 
the matrix exponential. 

````{prf:example}
Let $A=\begin{bmatrix}
         -7&4\\-12&7
    \end{bmatrix}$.
Our goal is to compute $e^{At}$ by first diagonalizing $A$. We begin by computing the eigenvalues of $A$:

$$
       \det( \lambda I_2-A)=\det ( \begin{bmatrix}
        \lambda+7&-4\\12&\lambda-7
    \end{bmatrix} )= \lambda^2-1,
$$

so the eigenvalues of $A$ are $\lambda_1=1$, $\lambda_2=-1$. To obtain the corresponding eigenvalues $v^1$ and $v^2$, we solve the equations

$$
 Av^i=\lambda_i v^i,\quad i=1,2.
$$

This gives $v^1=\begin{bmatrix} 1\\ 2 \end{bmatrix}$, and $v^2=\begin{bmatrix} 2\\3 \end{bmatrix}$. Let
$
 T:=\begin{bmatrix}
     v^1&v^2
 \end{bmatrix} = \begin{bmatrix}
     1 & 2\\ 2 &3 
 \end{bmatrix}.
$ 
 Then $AT=D T$, with $D=\text{diag}(\lambda_1,\lambda_2)=\text{diag}(1,-1)$, so
$
 A=T^{-1}DT.
$
Now,

$$
     e^{At}&= T^{-1} e^{Dt} T \\
       &= \begin{bmatrix}
     -3 & 2\\ 2 &-1 
 \end{bmatrix}      \text{diag}(e^t,e^{-t}) \begin{bmatrix}
     1 & 2\\ 2 &3 
 \end{bmatrix}  \\
 &= \begin{bmatrix} -3e^t +4e^{-t} 
 & - 6 e^{ t}+6e^{-t}\\
2e^t - 2e^{-t} &
4e^t - 3e^{-t}
\end{bmatrix}
 .
$$
````


### Matrix stability

A matrix $A\in\mathbb{C}^{n\times n}$ is called stable if $\lim_{t\to\infty}e^{At}=0$.


````{prf:example}
Let $\lambda=\alpha+i\beta$, with $\alpha,\beta\in \mathbb{R}$. 
Then

$$
 e^{\lambda t}=e^{(\alpha+i\beta )t}
 =e^{\alpha t} (\cos(\beta t)+i \sin(\beta t)).
$$

Thus, $\lim_{t\to\infty} e^{\lambda t}=0$ iff $\alpha<0$, that is, iff the real part of $\lambda$ is negative. Now let $D=\text{diag}(\lambda_1,\dots,\lambda_n)$, with $\lambda_i\in \mathbb{C}$. 
Since

$$
 e^{D t}=
 \text{diag}(e^{\lambda_1t}, \dots,e^{\lambda_n t}),
$$
we conclude that $D$ is stable iff the real part of every $\lambda_i$ is negative. 
````

````{admonition} Exercise
Let $A\in\mathbb{R}^{n\times n}$. Denote the eigenvalues of $A$ by $\lambda_k$, $k=1,\dots,n$. Prove that $A$ is stable iff every eigenvalue has a negative real part. Hint: first prove this when $A$ is diagonalizable. Then complete the proof using Proposition {prf:ref}`prop:B_close_diagonalizbe`.
````

