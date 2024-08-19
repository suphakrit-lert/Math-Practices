**Example 1. Assumption of Linear Regression**
1. The error terms i.i.d, normal distribution
2. Homoskedasticity
3. Linearity
4. No multicollinearity

**Example 2. Tossing to Get Consecutive 5's**

Say you're rolling a fair six-sided die. What is the expected number of rolls until you get two consecutive 5 s?

Let 

$V\left(S_i\right)$ be the function to find the \# of rolls from state $S_i$ to $S_2$ and $a$ be the number obtained from tossing the die

$\mathrm{S}_0$ : State 0 where there is no 5 's yet

$S_1$ : State 1 where there is a first 5

$S_2$ : State 2 where there is a second consecutive 5 's

Let's calculate the $V\left(S_1\right)$ first,

$$
\begin{aligned}
V\left(S_1\right) & =1+\mathbb{E}_{S_i}\left[V\left(S_i\right)\right] \\
& =1+P\left(S_1 \rightarrow S_2\right) V\left(S_2\right)+P\left(S_1 \rightarrow S_0\right) V\left(S_0\right) \\
& =1+\frac{1}{6} V\left(S_2\right)+\frac{5}{6} V\left(S_0\right) \\
V\left(S_1\right) & =1+\frac{1}{6} \cdot 0+\frac{5}{6} \cdot V\left(S_0\right)
\end{aligned}
$$


Then, let's calculate the $V\left(S_0\right)$

$$
\begin{aligned}
V\left(S_0\right) & =1+\mathbb{E}_{S_i}\left[V\left(S_i\right)\right] \\
& =1+P\left(S_0 \rightarrow S_1\right) V\left(S_1\right)+P\left(S_0 \rightarrow S_0\right) V\left(S_0\right) \\
V\left(S_0\right) & =1+\frac{1}{6} V\left(S_1\right)+\frac{5}{6} V\left(S_0\right)
\end{aligned}
$$


Solve (1) \& (2), $V\left(S_0\right)=42$ and $V\left(S_1\right)=36$