# Halo Optimizations and Constructing Graphs of Elliptic Curves

These are the accompanying notes for my ZK Study Club talks on [25th June](https://www.youtube.com/watch?v=q7bAYgxkHUE) and [2nd July](https://www.youtube.com/watch?v=IQVGIqcdxL4) 2020. The slides are [here](https://github.com/daira/halographs/raw/master/halographs.pdf).

We use the notation $E_{p \rightarrow q}$ for an elliptic curve over $\mathbb{F}_p$ with large prime-order subgroup of order $q$. For curves that form cycles, $q$ is the order of the curve (i.e. it has cofactor $1$).

## Proof that CM curves form cycles

Consider the elliptic curve $E_{p \rightarrow q}$ with $j$‑invariant $j_p$, and complex multiplication with positive discriminant $|D|$. Let $E_q$ be another CM curve over $\mathbb{F}_q$. Assume that if $j_p = 0$ then the $j$‑invariant of $E_q$ is also $0$.

The CM norm equation of $E_{p \rightarrow q}$ is $4p = |D|V^2 + T_p^2$ for integers $V$ and $T_p$.

*Theorem: One of the possible orders for $E_q$ is $p$.*

#### Case for $q = p + 1 \pm T_p$

We have

\begin{array}{rl}
4q\!\!\!&= 4p + 4 \pm 4T_p \\
        &= |D|V^2 + T_p^2 \pm 4T_p + 4 \\
        &= |D|V^2 + (T_p \pm 2)^2
\end{array}

This is a norm equation for $E_q$, with the same $|D|$ and $V$, and with $T_q = T_p \pm 2$.

In the positive case we have $T_q = T_p + 2$ and $q + 1 - T_q = (p + 1 + T_p) + 1 - (T_p + 2) = p$. 

In the negative case we have $T_q = T_p - 2$ and $q + 1 + T_q = (p + 1 - T_p) + 1 + (T_p - 2) = p$. 

That is, one of the possible orders of $E_q$, specifically $q + 1 \mp T_q$, is $p$ in both cases. $\square$

#### Otherwise

*Fact: if $q \neq p + 1 \pm T_p$ then $j \in \{0, 1728\}$. Furthermore if $q$ is prime then $|D| = 3$ and $j_p \neq 1728$ (see [[SS2011]](https://arxiv.org/abs/0912.1831) for details).*

So, the CM norm equation of $E_{p \rightarrow q}$ is $4p = 3V_p^2 + T_p^2$ for integers $V_p$ and $T_p$.

For a CM curve with $j_p = 0$ we have $q \in \left\{p + 1 \pm T_p, p + 1 \color{red}{\pm} \frac{3V_p}{2} \color{blue}{\pm} \frac{T_p}{2}\right\}$. (See [[IEEE Std 1363-2000]](https://perso.telecom-paristech.fr/guilley/recherche/cryptoprocesseurs/ieee/00891000.pdf), section A.14.2.3, item 6.)

The $p + 1 \pm T_p$ cases were covered above. For the four remaining cases,

\begin{array}{rl}
4q\!\!\!&= 4p + 4\left(1 \color{red}{\pm} \frac{3V_p}{2} \color{blue}{\pm} \frac{T_p}{2}\right) \\
        &= 3V_p^2 + T_p^2 + 4 \color{red}{\pm} 6V_p \color{blue}{\pm} 2T_p \\
        &= 3(V_p^2 \color{red}{\pm} 2V_p + 1) + (T_p^2 \color{blue}{\pm} 2T_p + 1) \\
        &= 3(V_p \color{red}{\pm} 1)^2 + (T_p \color{blue}{\pm} 1)^2
\end{array}

This is a norm equation for $E_q$, with $V_q = V_p \color{red}{\pm} 1$ and $T_q = T_p \color{blue}{\pm} 1$.

Then one of the possible orders of $E_q$, specifically $q + 1 \color{red}{\mp} \frac{3V_q}{2} \color{blue}{\mp} \frac{T_q}{2}$, is equal to $p$.

In case this is not clear we write out the four cases:

\begin{array}{|c|c|c|}
\hline
V_q                  & T_q                   & \#E_q\\\hline
V_p \color{red}{+} 1 & T_p \color{blue}{+} 1 & q + 1 \color{red}{-} \frac{3V_q}{2} \color{blue}{-} \frac{T_q}{2} = \left(p + 1 \color{red}{+} \frac{3V_p}{2} \color{blue}{+} \frac{T_p}{2}\right) + 1 \color{red}{-} \frac{3(V_p \color{red}{+} 1)}{2} \color{blue}{-} \frac{T_p \color{blue}{+} 1}{2} = p \\\hline
V_p \color{red}{+} 1 & T_p \color{blue}{-} 1 & q + 1 \color{red}{-} \frac{3V_q}{2} \color{blue}{+} \frac{T_q}{2} = \left(p + 1 \color{red}{+} \frac{3V_p}{2} \color{blue}{-} \frac{T_p}{2}\right) + 1 \color{red}{-} \frac{3(V_p \color{red}{+} 1)}{2} \color{blue}{+} \frac{T_p \color{blue}{-} 1}{2} = p \\\hline
V_p \color{red}{-} 1 & T_p \color{blue}{+} 1 & q + 1 \color{red}{+} \frac{3V_q}{2} \color{blue}{-} \frac{T_q}{2} = \left(p + 1 \color{red}{-} \frac{3V_p}{2} \color{blue}{+} \frac{T_p}{2}\right) + 1 \color{red}{+} \frac{3(V_p \color{red}{-} 1)}{2} \color{blue}{-} \frac{T_p \color{blue}{+} 1}{2} = p \\\hline
V_p \color{red}{-} 1 & T_p \color{blue}{-} 1 & q + 1 \color{red}{+} \frac{3V_q}{2} \color{blue}{+} \frac{T_q}{2} = \left(p + 1 \color{red}{-} \frac{3V_p}{2} \color{blue}{-} \frac{T_p}{2}\right) + 1 \color{red}{+} \frac{3(V_p \color{red}{-} 1)}{2} \color{blue}{+} \frac{T_p \color{blue}{-} 1}{2} = p \\\hline
\end{array} $\square$


## 2-adicity

We want both curves in a Halo cycle to have $2$-adicity at least $c$.

We can freely choose $V_p$ and $T_p$. So choose $\frac{V_p-1}{2}$ and $\frac{T_p-1}{2}$ as multiples of $2^c$. Then

\begin{array}{rl}
4p\! &= (3(V_p-1)^2 + 6(V_p-1) + 3) + ((T_p-1)^2 + 2(T_p-1) + 1) \\
     &= 3(V_p-1)^2 + 6(V_p-1) + (T_p-1)^2 + 2(T_p-1) + 4 \\
 p\! &= 3\left(\frac{V_p-1}{2}\right)^2 + 3\frac{V_p-1}{2} + \left(\frac{T_p-1}{2}\right)^2 + \frac{T_p-1}{2} + 1
\end{array}

So $p-1$ will be a multiple of $2^c$, and so will $q-1$ for $q \in \left\{ p+1-T_p,\, p+1-\frac{3V_p}{2}+\frac{T_p}{2} \right\}$.


## Compression of two random curve points to three field elements

(This is not implemented yet, and we have not decided whether to use it.)

Suppose we are given two random points $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$ on a curve $E / \mathbb{F}_p: y^2 = x^3 + b$ with a large number of points $\#E$.

We can check in the circuit that $x_1^3 \neq x_2^3$, and absorb $(x_1, x_2, y_1 + y_2)$ into the Fiat--Shamir sponge, instead of $(x_1, y_1, x_2, y_2)$.

----

*Lemma: Suppose that $v_1, v_2 \in \mathbb{F}_p$ are such that $v_1 \neq \pm v_2$ and $v_1 \neq 0$ and $v_2 \neq 0$. Then $\left\{ a_1 v_1 + a_2 v_2 : a_1, a_2 \in \{-1,+1\} \right\}$ are all distinct in $\mathbb{F}_p$.*

Proof. Add $v_1 + v_2$ to each element; since this is a bijection, the statement is equivalent to:

$$\left(v_1 \neq \pm v_2 \text{ and } v_1 \neq 0 \text{ and } v_2 \neq 0\right) \Rightarrow \{ 0, 2v_1, 2v_2, 2(v_1 + v_2) \} \text{ are all distinct.}$$

Since multiplication by $2$ in $\mathbb{F}_p$ is an injection, the LHS implies that $2v_1 \neq \pm 2v_2$ and $2v_1 \neq 0$ and $2v_2 \neq 0$, from which we can also infer that $2(v_1 + v_2)$ is none of $\{ 0, 2v_1, 2v_2 \}$. $\square$

----

Let $QR_p = \{u \in \mathbb{F}_p : u \text{ is a square in } \mathbb{F}_p \}$

*Theorem: Let $E / \mathbb{F}_p: y^2 = x^3 + b$ be an elliptic curve with $\#E$ points.*
1. *Suppose that $x_1, x_2 \in \mathbb{F}_p$ are such that $x_1^3 \neq x_2^3$ and $x_i^3 + b \in QR_p$. Then there exist points $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$ on $E$ uniquely determined by $(x_1, x_2, y_1 + y_2)$.*
2. *For exponentially large $\#E$, the conditions of part 1 hold except with negligible probability for $(x_1, x_2)$ given by the $x$-coordinates of random points $P_1$ and $P_2$ on $E$.*

Proof (Part 1).
From $x_1^3 \neq x_2^3$ we have $x_1^3 + b \neq x_2^3 + b$ and so $y_1^2 \neq y_2^2$, therefore $y_1 \neq \pm y_2$.

If $x_i^3 + b = 0$ then $y_i = 0$ and $y_{3-i} = y_1 + y_2$, so Part 1 holds. Hence we only need to consider the remaining case in which $y_1 \neq 0$ and $y_2 \neq 0$.

For $i \in \{1, 2\}$, let $v_i$ be an arbitrary square root of $x_i^3 + b$ (which must exist). We have $y_i = a_i v_i$ for $a_i \in \{-1, +1\}$. Therefore $y_1 + y_2 = a_1 v_1 + a_2 v_2$.

Since $y_1 \neq \pm y_2$ and $y_i = \pm v_i$, we have $v_1 \neq \pm v_2$ and $v_1 \neq 0$ and $v_2 \neq 0$. Therefore, by the lemma, there is an injective map from $(x_1, x_2, y_1 + y_2, v_1, v_2)$ to $(a_1, a_2)$, hence there is an injective map from $(x_1, x_2, y_1 + y_2)$ to $(P_1, P_2)$.

Proof (Part 2).
For a given $P_1 = (x_1, y_1)$ on $E$, there are up to three $x_2$ with $x_1^3 = x_2^3$, and up to two points on $E$ with a given $x_2$, so there can be at most six points $P_2 = (x_2, y_2)$ on $E$ for which $x_1^3 = x_2^3$. Therefore, over random choices of $P_1$ and $P_2$ we have $x_1^3 \neq x_2^3$ with probability at least $1 - \frac{6}{\#E}$. 
$\square$

This technique appears to be a reinvention of [[Xinxin Fan, Adilet Otemissov, Francesco Sica, and Andrey Sidorenko 2016]](https://sci-hub.tf/10.1007%2Fs10623-016-0251-2) for the case of two points, except that we exclude exceptional cases rather than using an extra bit to handle them. Also note that in the Fiat–Shamir setting we do not need to decompress the points.

