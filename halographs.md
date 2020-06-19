# Halo Optimizations and Constructing Graphs of Elliptic Curves

These are the accompanying notes for my ZK Study Club talk on 25th June 2020.

We use the notation $E_{p \rightarrow q}$ for an elliptic curve over $\mathbb{F}_p$ of (assumed prime) order $q$.

## Proof that CM curves form cycles

Consider the elliptic curve $E_{p \rightarrow q}$ as above, with $j$-invariant $j$, and complex multiplication with positive discriminant $D$. Let $E_q$ be another curve over $\mathbb{F}_q$ with the same $D$.

### Case for $j \neq 0$

Theorem: One of the two possible orders for $E_q$ is $p$.

Proof:
The CM norm equation for $E_{p \rightarrow q}$ is $4p = |D|V^2 + T_p^2$ for integers $V$ and $T_p$.

For a CM curve with $j \neq 0$ we have $q = p + 1 \pm T_p$, so

$4q = 4p + 4 \pm 4T_p$
$\phantom{4q} = |D|V^2 + T_p^2 \pm 4T_p + 4$
$\phantom{4q} = |D|V^2 + (T_p \pm 2)^2$

This is a norm equation for $E_q$, with the same $V$ and $T_q = T_p \pm 2$.

In the positive case we have $T_q = T_p + 2$ and $q + 1 - T_q = (p + 1 + T_p) + 1 - (T_p + 2) = p$. 

In the negative case we have $T_q = T_p - 2$ and $q + 1 + T_q = (p + 1 - T_p) + 1 + (T_p - 2) = p$. 

That is, one of the possible orders of $E_q$, specifically $q + 1 \mp T_q$, is $p$ in both cases. $\square$

### Case for $j = 0$

In this case we have $|D| = 3$. The CM norm equation for $E_{p \rightarrow q}$ is $4p = 3V_p^2 + T_p^2$ for integers $V_p$ and $T_p$.

For a CM curve with $j = 0$ we have $q \in \left\{p + 1 \pm T_p, p + 1 \color{red}{\pm} \frac{3V_p}{2} \color{blue}{\pm} \frac{T_p}{2}\right\}$.

The $p + 1 \pm T_p$ cases are the same as for $j \neq 0$. For the four remaining cases,

$4q = 4p + 4\left(1 \color{red}{\pm} \frac{3V_p}{2} \color{blue}{\pm} \frac{T_p}{2}\right)$
$\phantom{4q} = 3V_p^2 + T_p^2 + 4 \color{red}{\pm} 6V_p \color{blue}{\pm} 2T_p$
$\phantom{4q} = 3(V_p^2 \color{red}{\pm} 2V_p + 1) + (T_p^2 \color{blue}{\pm} 2T_p + 1)$
$\phantom{4q} = 3(V_p \color{red}{\pm} 1)^2 + (T_p \color{blue}{\pm} 1)^2$

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

## Compression of two random curve points to three field elements

Suppose we are given two random points $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$ on a curve $E / \mathbb{F}_p: y^2 = x^3 + b$ with a large number of points $\#E$.

We will check in the circuit that $x_1^3 \neq x_2^3$ and $x_1^3 + b \neq 0$ and $x_2^3 + b \neq 0$ and $y_1 + y_2 \neq 0$, and absorb $(x_1, x_2, y_1 + y_2)$ into the Fiat--Shamir sponge, instead of $(x_1, y_1, x_2, y_2)$.

(Strictly speaking we might not even need to do the checks since, as proven below, they fail with negligible probability. However, it's cheap to do so.)

----

Lemma: $\left(y_1 \neq \pm y_2 \text{ and } y_1 \neq 0 \text{ and } y_2 \neq 0 \text{ and } y_1 + y_2 \neq 0\right)$ implies that $\left\{ a_1 y'_1 + a_2 y'_2 : a_1, a_2 \in \{-1,+1\} \right\}$ are all distinct.

Proof. Add $y'_1 + y'_2$ to each element; since this is a bijection, the statement is equivalent to:
"$\left(y_1 \neq \pm y_2 \text{ and } y_1 \neq 0 \text{ and } y_2 \neq 0 \text{ and } y_1 + y_2 \neq 0\right)$ implies that $\{ 0, 2y'_1, 2y'_2, 2(y'_1 + y'_2) \}$ are all distinct.", which is clearly true. $\square$

----

Theorem: Except with negligible probability over random choices of $P_1$ and $P_2$, $x_1^3 \neq x_2^3$ and $x_1^3 + b \neq 0$ and $x_2^3 + b \neq 0$ and $y_1 + y_2 \neq 0$, and in that case $(x_1, x_2, y_1 + y_2)$ determines $P_1$ and $P_2$.

Proof (sketch). For a given $P_1$, there can be at most $6$ points $P_2$ on the curve that give the same $x^3$, and at most $3$ points $P_2$ for which $y_1 + y_2 = 0$. There are also at most $3$ points on the curve with $y = 0$. Therefore, if $P_1$ and $P_2$ are random, we expect that $\left(x_1^3 \neq x_2^3 \text{ and } x_1^3 + b \neq 0 \text{ and } x_2^3 + b \neq 0 \text{ and } y_1 + y_2 \neq 0\right)$ with probability at least $1 - \frac{6 + 3 + 2 \cdot 3}{\#E} = 1 - \frac{15}{\#E}$. In that case, $y_1^2 \neq y_2^2$, and so $y_1 \neq \pm y_2$. Also $y_1 \neq 0$ and $y_2 \neq 0$.

Let $y'_1$ be an arbitrary square root of $x_1^3 + b$, and similarly for $y'_2$. We have $y_1 = \pm y'_1$ and $y_2 = \pm y'_2$. Therefore $y_1 + y_2 = a_1 y'_1 + a_2 y'_2$ where $a_1, a_2 \in \{-1,+1\}$.

By the lemma, knowing $y'_1$, $y'_2$, and $y_1 + y_2$ tells you $a_1$ and $a_2$, hence $P_1$ and $P_2$. $\square$

