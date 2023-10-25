# Multiplication with booleans, and their utility for integrating discontinuous functions.

<h2>Íntroduction</h2>

If we have some discontinuous function $f(x)$, that we define to be:

$f(x) = \begin{cases} 
f_1(x) : x \in [x_1, x_2] \\
f_2(x) : x \notin [x_1, x_2]
\end{cases}$

One way to handle this function in calculations is to carefully check wether or not your specific x-value that you're working with is inside the domain $[x_1, x_2]$, before choosing which "method" of the function to dispatch. I propose an altarnate notation for this, that I feel provides greater versatility in calculations, and lends itself better towards concepts such as integration, derivation, etc, that we will get into later:

$f(x) = f_1(x)\cdot(x\in[x_1, x_2]) + f_2(x) \cdot (x\notin[x_1,x_2])$

Where $(x\in[x_1, x_2])$ and $(x\notin[x_1, x_2])$ are booleans, with values either $1$ or $0$, reflecting wether they are true or false.

For example: 

$(3 \in [1,2]) = 0$, 

While

$(3 \in [1,5]) = 1$.








<h2>Using it algebraically</h2>

This notation not only makes the function a bit more compact, it also allows us to use common methods such as factoring, multiplication, division, etc on these individual terms, just like when handling any normal function.

For example, if we have some function $g(x)$ that we know the following about:

$\frac{g(x)}{a} = f_1(x)\cdot(x\in[x_1, x_2]) + f_2(x) \cdot (x\notin[x_1,x_2])$

We can use standard algebra to draw conclusions about the statement:

$\Longleftrightarrow g(x) = a\cdot f_1(x)\cdot(x\in[x_1, x_2]) + a \cdot f_2(x) \cdot (x\notin[x_1,x_2]) \;$,  or:

$\Longleftrightarrow \frac{g(x)}{f_1(x)\cdot(x\in[x_1, x_2]) + f_2(x) \cdot (x\notin[x_1,x_2])} = a$

The previous statements could be made using standard notation, but would be a lot more cumbersome, and a lot less intuitive.

This also means that if we want to evaluate the expression at a certain x-value, say $x_p = \frac{x_1+x_2}{2}$, whereby $(x_p \in [x_1, x_2]) = 1$, and $(x_p \notin [x_1, x_2]) = 0$. Then we just evaluate all the boolean terms individually. Say that we want to evaluate the following expression:

$b = \frac{c}{f_1(x_p)\cdot(x_p\in[x_1, x_2]) + f_2(x_p) \cdot (x_p\notin[x_1,x_2])}\;$; Then: 

$b = \frac{c}{f_1(x_p)\cdot 1 + f_2(x_p) \cdot 0} = \frac{c}{f_1(x_p)}$

We can also factor an expression with booleans, for example, if we have the following:

$$\begin{align*} f(x) =&\; \bigl(\;f_1\cdot(x\in[x_1,x_2])\;\bigr)^2 \\ 
&+ 2\bigl(\;f_1\cdot(x\in[x_1,x_2])\;\bigr) \bigl(\;f_2\cdot(x\in[x_3,x_4])\;\bigr)\\ 
&+\bigl(\;f_2\cdot(x\in[x_3,x_4])\;\bigr)^2\;\;\;  \end{align*}$$

$$\Longleftrightarrow f(x) = \bigl(\;f_1\cdot(x\in[x_1,x_2])\; + \;f_2\cdot(x\in[x_3,x_4])\;\bigr)^2$$

This is something that, as far as I'm aware, you cannot do with the standard notation. This often comes in handy, and we'll see an example of that later.






<h2>Integration of expressions containing booleans</h2>


If we have some function $f(x)$ such that:
$$f(x) = f_1(x)\cdot(x\in[x_1, x_2])$$

Where $f_1(x)$ is some other function with a primitive function $F_1(x)$, such that: $\frac{dF_1(x)}{dx} = f_1(x)$.

We will thus proceed to find an expression for the primitive function to $f(x)$ based on this.


Let $F(x)$ be a primitive function to $f(x)$, such that $\frac{dF(x)}{dx} = f(x)$:

Let: $$F(x) = \int_{0}^{x}f(x)dx$$

From the definition of an integral as a Riemann-sum we get that:

$$\begin{align*}
\int_{0}^{X}f_1(x)(x\in[x_1,x_2])dx 
=& \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{\frac{X}{\Delta x}}
f_1(\Delta x \cdot i)\cdot(\Delta x \cdot i \in[x_1,x_2])\cdot \Delta x \\
\end{align*}$$

There are now three cases:

1: $X\in(-\infty,x_1)$, 

2: $X\in [x_1,x_2]$,

3: $X\in (x_2,\infty)$

Case 1:

$$\begin{align*}
\int_{0}^{X}f_1(x)(x\in[x_1,x_2])dx 

=& \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{\frac{X}{\Delta x}}
f_1(\Delta x \cdot i)\cdot(\Delta x \cdot i \in[x_1,x_2])\cdot \Delta x \\

&\Bigg|\Delta x \cdot \frac{X}{\Delta x} = X , X\notin[x_1,x_2]\Longleftrightarrow \Delta x\cdot i \notin[x_1,x_2]
\\

=&  \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{\frac{X}{\Delta x}}
f_1(\Delta x \cdot i)\cdot 0 \cdot \Delta x  \\

&= 0
\end{align*}$$

Case 2:

$$\begin{align*}
\int_{0}^{X}f_1(x)(x\in[x_1,x_2])dx 

=& \int_{0}^{x_1}f_1(x)(x\in[x_1,x_2])dx + \int_{x_1}^{X}f_1(x)(x\in[x_1,x_2])dx \\

=& \lim_{\Delta x \rightarrow 0}
\sum_{i=1}^{\frac{x_1-\Delta x}{\Delta x}}
f_1(\Delta x \cdot i)\cdot(\Delta x \cdot i \in[x_1,x_2))\cdot \Delta x \\
&+ \sum_{i=1}^{\frac{X - x_1}{\Delta x}}
f_1(x_1 + \Delta x \cdot i)\cdot(x_1 + \Delta x \cdot i \in[x_1,x_2])\cdot \Delta x \\

&\Bigg|\Delta x \cdot \frac{x_1 - \Delta x}{\Delta x} = x_1 - \Delta x, x_1 - \Delta x \notin[x_1,x_2]\Longleftrightarrow \Delta x\cdot i \notin[x_1,x_2]
\\
&\Bigg|x_1 + \Delta x \cdot \frac{X-x_1}{\Delta x} = x_1 + X - x_1 = X, X\in[x_1,x_2]\Longleftrightarrow x_1 + \Delta x\cdot i \in[x_1,x_2]
\\


=& \lim_{\Delta x \rightarrow 0} 
\sum_{i=1}^{\frac{x_1 - \Delta x}{\Delta x}}
f_1(\Delta x \cdot i)\cdot 0 \cdot \Delta x \\
&+\sum_{i=1}^{\frac{X - x_1}{\Delta x}}
f_1(x_1 + \Delta x \cdot i)\cdot 1\cdot \Delta x \\

=& \lim_{\Delta x \rightarrow 0} 
\sum_{i=1}^{\frac{X - x_1}{\Delta x}}
f_1(x_1 + \Delta x \cdot i)\cdot \Delta x \\

=& \int_{x_1}^{X}f_1(x)dx
  
\end{align*}$$


Case 3:

$$\begin{align*}
\int_{0}^{X}f_1(x)(x\in[x_1,x_2])dx 
=& \int_{0}^{x_1}f_1(x)(x\in[x_1,x_2])dx + \int_{x_1}^{x_2}f_1(x)(x\in[x_1,x_2])dx + \int_{x_2}^{X}f_1(x)(x\in[x_1,x_2])dx\\

&=  \lim_{\Delta x \rightarrow 0}
\sum_{i=1}^{\frac{x_1 - \Delta x}{\Delta x}}
f_1(\Delta x \cdot i)\cdot(\Delta x \cdot i \in[x_1,x_2])\cdot \Delta x \\
&+ \sum_{i=1}^{\frac{x_2 - x_1}{\Delta x}}
f_1(x_1 + \Delta x \cdot i)\cdot(x_1 + \Delta x \cdot i \in[x_1,x_2])\cdot \Delta x \\
&+ \sum_{i=1}^{\frac{X - x_2}{\Delta x}}
f_1(x_2 + \Delta x \cdot i)\cdot(x_2 + \Delta x \cdot i \in[x_1,x_2])\cdot \Delta x \\

&\Bigg|x_1 + \Delta x \cdot \frac{x_2-x_1}{\Delta x} = x_1 + x_2 - x_1 = x_2,  x_2 \in[x_1,x_2]\Longleftrightarrow x_1 + \Delta x\cdot i \in[x_1,x_2]
\\

&\Bigg|x_2 + \Delta x \cdot \frac{X-x_2}{\Delta x} = x_2 + X - x_2 = X,  X \notin[x_1,x_2]\Longleftrightarrow x_1 + \Delta x\cdot i \notin[x_1,x_2]
\\

=& \lim_{\Delta x \rightarrow 0}
\sum_{i=1}^{\frac{x_1 - \Delta x}{\Delta x}}
f_1(\Delta x \cdot i)\cdot 0 \cdot \Delta x \\
&+ \sum_{i=1}^{\frac{x_2 - x_1}{\Delta x}}
f_1(x_1 + \Delta x \cdot i)\cdot 1\cdot \Delta x \\
&+ \sum_{i=1}^{\frac{X - x_2}{\Delta x}}
f_1(x_2 + \Delta x \cdot i)\cdot 0 \cdot \Delta x \\

=&  \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{\frac{x_2 - x_1}{\Delta x}}
f_1(x_1 + \Delta x \cdot i)\cdot \Delta x \\

=& \int_{x_1}^{x_2}f_1(x)dx
\end{align*}$$


We thus get the following:

$$\int_{0}^{X}f_1(x)(x\in[x_1,x_2])dx  = \begin{cases} \begin{align*}
0 &: X \in (-\infty, x_1) \\
\int_{x_1}^{X}f_1(x)dx &: X \in [x_1, x_2] \\ 
\int_{x_1}^{x_2}f_1(x)dx &: X \in (x_2, \infty) \\
\end{align*}
\end{cases}$$

Which can be written neatly in boolean-multiplication form as:

$$\begin{align*}
\int_{0}^{X}f_1(x)(x\in[x_1,x_2])dx  =& \biggl[\int_{x_1}^{X}f_1(x)dx \biggr]\cdot (X \in [x_1, x_2])\\
&+ \biggl[\int_{x_1}^{x_2}f_1(x)dx \biggr]\cdot (X \in [x_2, \infty))\\
=& (F_1(X)-F_1(x_1))(X\in[x_1,x_2]) -(F_1(x_2)-F_1(x_1))(X\in[x_2,\infty)) 
\end{align*}$$





If we want to find the integral to the function from a lower bound to an upper bound, say $[X_1, X_2]$ (not necessarily the same as $x\in[x_1, x_2]$), we can now do that:


From the fundamental theorem of calculus we know that:

$$\int_{X_1}^{X_2}f(x)dx = F(X_2) - F(X_1) = \int_{0}^{X_2}f(x)dx - \int_{0}^{X_1}f(x)dx$$


We thus get:

$$\begin{align*} \int_{X_1}^{X_2}f(x)dx =& \int_{0}^{X_2}f(x)dx - \int_{0}^{X_1}f(x)dx \\
=& \int_{0}^{X_2}f_1(x)(x\in[x_1,x_2])dx - \int_{0}^{X_1}f_1(x)(x\in[x_1,x_2])dx \\
=& \biggl[\int_{x_1}^{X_2}f_1(x)dx \biggr]\cdot (X_2 \in [x_1, x_2])\\
&+ \biggl[\int_{x_1}^{x_2}f_1(x)dx \biggr]\cdot (X_2 \in (x_2, \infty)) \\
&- \biggl[\int_{x_1}^{X_1}f_1(x)dx \biggr]\cdot (X_1 \in [x_1, x_2])\\
&- \biggl[\int_{x_1}^{x_2}f_1(x)dx \biggr]\cdot (X_1 \in (x_2, \infty))
\end{align*}$$


We can use these expressions to also get some useful short-hands:

$$\begin{align*}\int_{0}^{X}f(x-x_1)(x\in[x_1,x_2])dx =& \biggl[\int_{x_1}^{X}f_1(x-x_1)dx \biggr](X \in [x_1, x_2])\\
&+ \biggl[\int_{x_1}^{x_2}f_1(x-x_1)dx \biggr](X \in [x_2, \infty))\\
\end{align*}$$

Using u-substitution:
$$\begin{cases} let: u = x-x_1 \\
x\in [x_1,x_2] \Longleftrightarrow u\in[0,x_2-x_1]\\
x\in [x_2,\infty) \Longleftrightarrow u\in[x_2-x_1,\infty)\\
\frac{du}{dx} = 1 \Longleftrightarrow du = dx
\end{cases}$$

Whereby:

$$\begin{align*} &\biggl[\int_{x_1}^{X}f_1(x-x_1)dx \biggr](X \in [x_1, x_2]) + \biggl[\int_{x_1}^{x_2}f_1(x-x_1)dx \biggr](X \in [x_2, \infty)) \\
&= \biggl[\int_{0}^{X-x_1}f_1(u)du \biggr](X \in [x_1, x_2]) + \biggl[\int_{0}^{x_2-x_1}f_1(u)du \biggr](X \in [x_2, \infty)) \\
&= F(X-x_1)(X \in [x_1, x_2]) + F(x_2-x_1)(X \in [x_2, \infty))
\end{align*}$$

While this is not native to discrete functions, it will come in very handy later for some of our later derivations. Thus:

$$\begin{align*}\int_{0}^{X}f_1(x-x_1)(x\in[x_1,x_2])dx = F_1(X-x_1)(X\in[x_1,x_2]) + F_1(x_2-x_1)(X\in[x_2,\infty))
\end{align*}$$


With this in mind, finding the double-integral becomes trivial:

$$\begin{align*}
{\int\int}_{0}^{X}f_1(x)(x\in[x_1, x_2])dx^2 &= 
\int_{0}^{X} (F_1(x) - F_1(x_1))(x\in[x_1,x_2]) + (F_1(x_2) - F_1(x_1))(x\in(x_2,\infty)) dx\\
\end{align*}$$

Let: $\mathbb{F}_1(x)$ be the primitive function to $F_1(x)$, such that: $\frac{d\mathbb{F}_1(x)}{dx} = F_1(x)$

$$\begin{align*}
=& (\mathbb{F}_1(x)-\mathbb{F}_1(x_1) - F_1(x_1)x + F_1(x_1)x_1)(x\in[x_1,x_2])\\
&+(\mathbb{F}_1(x_2)-\mathbb{F}_1(x_1) - F_1(x_1)x_2 + F_1(x_1)x_1)(x\in(x_2,\infty))\\
&+ (F_1(x_2)x - F_1(x_2)x_2 - F_1(x_1)x + F_1(x_1)x_2)(x\in(x_2,\infty))\\
&+ (F_1(x_2)\infty - F_1(x_2)x_2 - F_1(x_1)\infty + F_1(x_1)x_2)(x\in(x_2,\infty))\\


\end{align*}$$



As $(x\in(\infty, \infty))$ never occours, this term will be 0. This does however lead us to note something important: 

Boolean 0 is, in lack of a better word, "stronger" than infinity, which makes intuitive sense, since it's meant to represent true or false, and thus wether or not a term should be included at all or not. We will thus use the bold-notation $\mathbf{0}$ and $\mathbf{1}$ instead of $0$ and $1$ to symbolise this:

Def:

$\mathbf{0}: \infty\cdot \mathbf{0} = 0, \;\; k\cdot\mathbf{0} = 0 \; \forall \; k\in\mathbb{R}$

$\mathbf{1}: \mathbf{1} = 1$

Thus:

$$\begin{align*}
{\int\int}_{0}^{X}f_1(x)(x\in[x_1, x_2])dx^2 
=&  (\mathbb{F}_1(x)-\mathbb{F}_1(x_1) - F_1(x_1)(x - x_1))(x\in[x_1,x_2])\\
&+(\mathbb{F}_1(x_2)-\mathbb{F}_1(x_1) - F_1(x_1)(x_2 - x_1))(x\in(x_2,\infty))\\
&+ (F_1(x_2) - F_1(x_1))(x-x_2)(x\in(x_2,\infty))\\

\end{align*}$$


But we can go further.

Let's say that we want to find the n'th integral:

$$\begin{align*}
\int\int\int {}_{\dots}^{\;n} \int_{X}^{0}f_1(x)(x\in[x_1,x_2])dx^n = \dots =\int\int\int {}_{\dots}^{n-2} \int_{X}^{0}& (\mathbb{F}_1(x)-\mathbb{F}_1(x_1) - F_1(x_1)(x - x_1))(x\in[x_1,x_2])\\
&+ (\mathbb{F}_1(x_2)-\mathbb{F}_1(x_1) - F_1(x_1)(x_2 - x_1))(x\in(x_2,\infty))\\
&+ (F_1(x_2) - F_1(x_1))(x-x_2)(x\in(x_2,\infty)) dx^{n-2}
\end{align*}$$

Let $F_1^m(x)$ be the m'th primitive function to $f_1(x)$, such that: $\frac{d^mF_1^m(x)}{dx^m} = f_1(x)$:

Continuing the pattern, we get:

$$\begin{align*}
\int\int\int {}_{\dots}^{\;n} \int_{X}^{0}f_1(x)(x\in[x_1,x_2])dx^n = \dots 

=\int\int\int {}_{\dots}^{n-3} \int_{X}^{0}& 

(F_1^3(x)-F_1^3(x_1) - F_1^2(x_1)(x - x_1) - \frac{1}{2}F_1(x_1)(x - x_1)^2)(x\in[x_1,x_2])\\
&+ (F_1^3(x_2)-F_1^3(x_1) - F_1^2(x_1)(x_2 - x_1) - \frac{1}{2}F_1(x_1)(x_2 - x_1)^2)(x\in(x_2,\infty))\\
&+ (\mathbb{F}_1(x_2)-\mathbb{F}_1(x_1) - F_1(x_1)(x_2 - x_1))(x-x_2)(x\in(x_2,\infty))\\
&+ (F_1(x_2) - F_1(x_1))\frac{1}{2}(x-x_2)^2(x\in(x_2,\infty)) 

dx^{n-3} \\

= \int\int\int {}_{\dots}^{n-4} \int_{X}^{0}& 

(F_1^4(x) - F_1^4(x_1) -F_1^3(x_1)(x-x_1) - \frac{1}{2}F_1^2(x_1)(x - x_1)^2 - \frac{1}{6}F_1(x_1)(x - x_1)^3)(x\in[x_1,x_2])\\
&+ (F_1^4(x_2) - F_1^4(x_1) -F_1^3(x_1)(x_2-x_1) - \frac{1}{2}F_1^2(x_1)(x_2 - x_1)^2 - \frac{1}{6}F_1(x_1)(x_2 - x_1)^3)(x\in(x_2,\infty))\\
&+ (F_1^3(x_2)-F_1^3(x_1) - F_1^2(x_1)(x_2 - x_1) - \frac{1}{2}F_1(x_1)(x_2 - x_1)^2)(x-x_2)(x\in(x_2,\infty))\\
&+ (\mathbb{F}_1(x_2)-\mathbb{F}_1(x_1) - F_1(x_1)(x_2 - x_1))\frac{1}{2}(x-x_2)^2(x\in(x_2,\infty))\\
&+ (F_1(x_2) - F_1(x_1))\frac{1}{6}(x-x_2)^3(x\in(x_2,\infty)) 

dx^{n-4} \\

\end{align*}$$

While this process doesn produce a lot of residual terms, if we look close enough we can see a pattern emerge. Sumarizing this pattern, we get:

$$\begin{align*}
\int\int\int {}_{\dots}^{\;n} \int_{X}^{0}&f_1(x)(x\in[x_1,x_2])dx^n = \dots \\

=& F_1^n(x)(x\in[x_1, x_2]) - \sum_{i=1}^{n} \frac{1}{(n-i)!}F_1^{i}(x_1)(x-x_1)^{n-i}(x\in[x_1, x_2]) \\

&+ F_1^n(x_2)(x\in(x_2, \infty)) - \sum_{i=1}^{n} \frac{1}{(n-i)!}F_1^{i}(x_1)(x_2-x_1)^{n-i}(x\in(x_2, \infty)) \\

&+ \bigg[F_1^{n-1}(x_2)(x\in(x_2, \infty)) - \sum_{i=1}^{n-1} \frac{1}{(n-i-1)!}F_1^{i}(x_1)(x_2-x_1)^{n-i-1}(x\in(x_2, \infty))\bigg](x-x_2) \\

&+ \bigg[F_1^{n-2}(x_2)(x\in(x_2, \infty)) - \sum_{i=1}^{n-2} \frac{1}{(n-i-2)!}F_1^{i}(x_1)(x_2-x_1)^{n-i-2}(x\in(x_2, \infty))\bigg]\frac{1}{2}(x-x_2)^2 \\
\vdots\\

&+ \bigg[F_1^{n-2}(x_2)(x\in(x_2, \infty)) - \sum_{i=1}^{1} \frac{1}{(n-i - (n-1))!}F_1^{i}(x_1)(x_2-x_1)^{n-i - (n-1)}(x\in(x_2, \infty))\bigg]\frac{1}{(n-1)!}(x-x_2)^{(n-1)} \\

=& F_1^n(x)(x\in[x_1, x_2]) - \sum_{i=1}^{n} \frac{1}{(n-i)!}F_1^{i}(x_1)(x-x_1)^{n-i}(x\in[x_1, x_2]) \\
&+ \sum_{m=0}^{n-1} 
\bigg[F_1^{n-m}(x_2)(x\in(x_2, \infty)) - \sum_{i=1}^{n-m} \frac{1}{(n-i - m)!}F_1^{i}(x_1)(x_2-x_1)^{n-i - m}(x\in(x_2, \infty))\bigg]\frac{1}{m!}(x-x_2)^{m}
\end{align*}$$


Thus, we get the final formula:

$$\begin{align*}
\int\int\int {}_{\dots}^{\;n} \int_{X}^{0}&f_1(x)(x\in[x_1,x_2])dx^n \\
=& F_1^n(x)(x\in[x_1, x_2]) - \sum_{i=1}^{n} \frac{1}{(n-i)!}F_1^{i}(x_1)(x-x_1)^{n-i}(x\in[x_1, x_2]) \\
&+ \sum_{m=0}^{n-1} 
\bigg[F_1^{n-m}(x_2) - \sum_{i=1}^{n-m} \frac{1}{(n-i - m)!}F_1^{i}(x_1)(x_2-x_1)^{n-i - m}\bigg]\frac{1}{m!}(x-x_2)^{m}(x\in(x_2, \infty))
\end{align*}$$

While clunky, this sum only requires as much integration as integrating $F_1(x)$ under normal circumstances, when it's domain is not constrained to $x\in[x_1,x_2]$. The rest of the terms are just lower order integrals and constants.


