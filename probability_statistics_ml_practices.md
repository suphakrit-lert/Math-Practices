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


**Example 3. Hypothesis Testing**

Say you flip a coin 10 times and observe only one heads. What would be your null hypothesis and $p$-value for testing whether the coin is fair or not?

Let $X$ be the random variable of the number of heads obtained from tossing ten coins
$H_0$ : The coin is fair with $X=5$ from tossing 10 coin
$H_a$ : The coin is unfair with $X \neq 5$ from tossing 10 coin
Let's find the expected value and variance of $X$ where is binomial distribution or $X \sim \operatorname{Bin}(n, p)=\operatorname{Bin}(10,0.5)$

$$
\begin{gathered}
\mathbb{E}[X]=n p=10 \cdot 0.5=5 \\
\operatorname{Var}(X)=n p(1-p)=10 \cdot 0.5 \cdot(1-0.5)=2.5
\end{gathered}
$$


To test if the coin is fair or not, we need to first calculate the test statistics.
Since we observe only one head from ten toss, we have $X=1$

$$
Z_0=\frac{X-\mathbb{E}[X]}{\sqrt{\operatorname{Var}(X)}}=\frac{1-5}{\sqrt{2.5}}=2.53
$$


Calculate the p -value, p -value $=P\left(|Z|>Z_0\right)$

$$
\begin{aligned}
P(|Z|>2.53) & =P(Z>2.53 \text { or } Z<-2.53) \\
& =2 P(Z<-2.53) \\
& =2 \cdot \Phi(-2.53) \\
& =2 \cdot 0.0057 \\
& =0.011
\end{aligned}
$$

Set the confidence to be $95 \%$; hence, $\alpha=1-0.95=0.05$. Since p -value $=0.011$ is lesser than $\alpha=0.05$, we reject the null hypothesis that the coin is fair.


**Example 4. Law of Total Probability**

Suppose $80 \%$ of Netflix users rate movies thumbs up $60 \%$ of the time, and thumbs down $40 \%$ of the time. However, $20 \%$ of Netflix users are "lazy": they rate $100 \%$ of the movies they watch as good! Given that someone gives 3 movies IN A ROW a thumbs up, what's the probability they are a "lazy" rater?

$$
\begin{aligned}
& P(\text { Lazy } \mid 3 \text { up's }) \\
& =\frac{P(3 \text { up's } \mid \text { Lazy }) \cdot P(\text { Lazy })}{P(3 \text { up's })} \\
& =\frac{P(3 \text { up's } \mid \text { Lazy }) \cdot P(\text { Lazy })}{P(3 \text { up's | Lazy }) \cdot P(\text { Lazy })+P(3 \text { up's I Not Lazy }) \cdot P(\text { Not Lazy })} \\
& =\frac{1^3 \cdot 0.20}{1^3 \cdot 0.20+0.60^3 \cdot 0.80} \\
& =0.536
\end{aligned}
$$
