# Linear Algebra and Learning From Data（线性代数与数据学习）· V.3

## 书页 285-293 ｜ PDF 页 287-295 ｜ Moments, Cumulants, and Inequalities of Statistics（矩、累积量与统计不等式）

> <span style="color:#7f8c8d;">本节从 Markov（马尔可夫）与 Chebyshev（切比雪夫）不等式出发，引入生成函数与累积量，进而把这些浓度不等式推广到随机矩阵，最后落到 Erdős–Rényi 随机图的连通性判据上，是全书把概率工具用到数据科学的核心章节。</span>

---

<!-- page 287 -->

> <span style="color:#7f8c8d;">本页为书页 285，属 V.3 开头，给出 Markov 与 Chebyshev 两个基础不等式及其证明；页眉与印页码不译。</span>

V.3. Moments, Cumulants, and Inequalities of Statistics（矩、累积量与统计不等式）

Markov 不等式（Markov's inequality）的证明只消四步。

```math
\bar X = \mathbb E[X] = \sum_{\text{all } s} X(s)\, \Pr[X(s)]
```

将求和拆成两部分：

```math
\mathbb E[X] \ge \sum_{X(s)\ge a} X(s)\, \Pr[X(s)]
\ge a \sum_{X(s)\ge a} \Pr[X(s)]
= a\, \Pr[X(s) \ge a]
```

两边除以 $a$，即得 Markov 不等式：$\Pr[X(s) \ge a] \le \bar X / a$。

第二个有用的不等式是 Chebyshev 的（Chebyshev's）。它对一切 random variable（随机变量）$X(s)$ 都成立，而不只限于非负函数。它给出那些"偏离均值 $\bar X$ 很远"的事件概率的估计——所以我们看的是概率分布的"tail"（尾部）。对于"heavy-tailed"（重尾）分布，较大偏差 $|X(s) - \bar X|$ 出现的概率比通常更高。而 $\Pr[|X-\bar X| \ge a]$ 会随数 $a$ 的增大而减小。

**Chebyshev 不等式（对任意概率分布 $X(s)$）：**

```math
\Pr\big[\,|X(s) - \bar X| \ge a\,\big] \le \frac{\sigma^2}{a^2}
```

证明是：把 Markov 不等式应用到非负函数 $Y(s) = (X(s) - \bar X)^2$ 上。按 variance（方差）的定义，函数 $Y$ 的均值正是 $\sigma^2$！我们关心的是 $|X(s) - \bar X| \ge a$ 的事件。两边平方得 $Y(s) \ge a^2$。再用 Markov：

```math
\Pr\big[Y(s) \ge a^2\big] \le \frac{\mathbb E[Y]}{a^2} = \frac{\sigma^2}{a^2}
\qquad\text{(Chebyshev 由 Markov 而来)}
```

这些都是简单的不等式，但它们可以进一步改进。有时它们已足以确立某个 randomized algorithm（随机算法）能够成功；当它们不够用时，你通常得越过均值和方差，去考察更高阶的"moments"（矩）和"cumulants"（累积量）。其关键思想（如 Chernoff 不等式那样）往往是使用一个 generating function（生成函数），它把所有矩都串联起来。

把一列数连到一个函数，是数学里一个强有力的思想。一个实函数 $f(x)=\sum a_n x^n$（或一个复函数 $F(\theta)=\sum a_n e^{in\theta}$）以另一种形式承载着所有数 $a_n$ 的信息。那些数可以是 probabilities（概率），也可以是"moments"或"cumulants"。此时 $f$ 就是它们的生成函数。

---

<!-- page 288 -->

> <span style="color:#7f8c8d;">本页为书页 286，定义矩与中心矩，并导出 skewness（偏度）与 kurtosis（峰度）这两个归一化高阶量；页眉与印页码不译。</span>

**Moments and Central Moments（矩与中心矩）**

均值和方差是 fundamental numbers（基本量），无论对离散概率集，还是对 probability density function（概率密度函数）$p(x)$ 都成立。但统计学的基本理论走得更远：对每个 $n$，矩是 $m_n$。

- Zeroth moment（零阶矩）$=1$：$\sum p_i = 1$ 或 $\int p(x)\,dx = 1$
- First moment（一阶矩）$=$ mean（均值）$= \mathbb E[x]$：$\sum i\,p_i = m$ 或 $\int x\,p(x)\,dx = m$
- Second moment（around 0，二阶原点矩）：$\sum i^2 p_i$ 或 $\int x^2 p(x)\,dx = \sigma^2 + m^2 = \mathbb E[x^2]$

到目前为止我们知道 $m_0, m_1, m_2$。二阶 central moment（中心矩，绕均值 $m$）为：

```math
\mathbb E\big[(x-m)^2\big] = \sigma^2
\quad\text{或}\quad
\int (x-m)^2 p(x)\,dx = \sigma^2
```

$n$ 阶矩 $m_n$ 是 $\sum i^n p_i$ 或 $\int x^n p(x)\,dx$。但中心矩（绕 $m$）更有用，它们定义为 $(x-m)^n$ 的 expected value（期望值）：

```math
\text{n 阶中心矩 } = \sum (i-m)^n p_i
\quad\text{或}\quad
\int (x-m)^n p(x)\,dx
\tag{6}
```

```math
\text{n 阶归一化中心矩 } = \mu_n / \sigma^n
\tag{7}
```

每个关于均值对称的分布，其所有 odd moments（奇阶矩）都为零，因为零点左侧与右侧的项相互抵消。当 $p(x)$ 关于其均值对称时，奇阶中心矩……将全部为零。（最佳例子 = normal distribution，正态分布。）而归一化的三阶中心矩 $\mu_3/\sigma^3$ 称为分布的 skewness（偏度）。

**问题：** 掷一枚 Bernoulli（伯努利）硬币，概率为 $p_0 = 1-p$、$p_1 = p$，其偏度是多少？

**解答：** 首先均值是 $p$。方差为 $\sigma^2 = (1-p)p^2 + p(1-p)^2 = p(1-p)$。三阶中心矩是 $\mu_3$，它取决于到均值 $p$ 的距离：

```math
\mu_3 = (1-p)(0-p)^3 + p(1-p)^3 = p(1-p)(1-2p)
```

```math
\text{skewness} = \frac{\mu_3}{\sigma^3} = \frac{1-2p}{\sqrt{p(1-p)}}
```

离"center"（中心）越远，矩就越大。对一块 seesaw（跷跷板），中心是质心；对概率，中心就是均值 $m$。一个重尾分布会有很大的 $\mu_4$。我们通常以正态分布的四阶矩（它是 $3\sigma^4$）作为比较基准。于是任意分布的 kurtosis（峰度）记作 $\kappa$：

```math
\text{Kurtosis} = \kappa = \frac{\mu_4}{\sigma^4}
\tag{8}
```

---

<!-- page 289 -->

> <span style="color:#7f8c8d;">本页为书页 287，引入四类生成函数与累积量，并指出独立随机变量累积量可加这一关键性质；页眉与印页码不译。</span>

**Generating Functions and Cumulants（生成函数与累积量）**

由概率、矩和累积量造出四个关键函数。我们从离散随机变量 $X$ 出发。事件 $X=n$ 的概率为 $p_n$。这些数 $p_n$ 导出前三个函数，而 $K(t) = \log M(t)$。

```math
\text{Probability generating function（概率生成函数）}\quad G(z) = \sum p_n z^n = \mathbb E[z^X]
\tag{9}
```

```math
\text{Characteristic function（特征函数）}\quad \phi(t) = \sum p_n e^{int} = \mathbb E[e^{itX}]
\tag{10}
```

```math
\text{Moment generating function（矩生成函数）}\quad M(t) = \sum p_n e^{nt} = \mathbb E[e^{tX}]
\tag{11}
```

```math
\text{Cumulant generating function（累积量生成函数）}\quad K(t) = \log M(t) = \log \mathbb E[e^{tX}]
\tag{12}
```

所有概率 $p_n$、矩 $m_n$ 和累积量 $\kappa_n$ 都能由 $G,M,K$ 在 $z=0$ 与 $t=0$ 处的 $n$ 阶导数还原出来：

```math
p_n = \frac{1}{n!}\frac{d^n G}{dz^n}(0),\qquad
m_n = \frac{d^n M}{dt^n}(0),\qquad
\kappa_n = \frac{d^n K}{dt^n}(0)
\tag{13}
```

而且有一个极富启发的办法把这四个生成函数与 expectation（期望）连起来：

```math
G(z)=\mathbb E[z^X],\quad
\phi(t)=\mathbb E[e^{itX}],\quad
M(t)=\mathbb E[e^{tX}],\quad
K(t)=\log \mathbb E[e^{tX}]
\tag{14}
```

当然这四个函数背后必有目的：我们在每个函数里捕捉了一整组（无限多）系数。累积量的关键点是它们导出 $K(t)=\log M(t)$ 的这一性质：

```math
K_{X+Y}(t) = K_X(t) + K_Y(t)
\quad\text{对独立随机变量 } X,Y
```

**例子** 一次掷硬币给出 Bernoulli 分布，概率为 $p_0 = 1-p$、$p_1 = p$，故 $M(t) = 1-p+pe^{t}$，均值 $\mu = p$。于是 $p=\mathbb E[x]=\mathbb E[x^2]=\mathbb E[x^3]=\cdots$。累积量生成函数 $K(t)=\log(1-p+pe^{t})$。第一个累积量是

```math
\kappa_1 = \frac{dK}{dt}\bigg|_{t=0}
= \frac{p e^{t}}{1-p+p e^{t}}\bigg|_{t=0} = p
```

对 binomial distribution（二项分布，$N$ 次独立掷币），每个累积量乘以 $N$。对 Poisson distribution（泊松分布）$p_n = e^{-\lambda}\lambda^n/n!$，函数 $K(t)=\lambda(e^{t}-1)$，所有 $\kappa_n = \lambda$。

---

<!-- page 290 -->

> <span style="color:#7f8c8d;">本页为书页 288，把生成函数推广到连续分布，并给出中心极限定理与 Chernoff 不等式对求和的情境；页眉与印页码不译。</span>

**Generating Functions for Continuous Distributions（连续分布的生成函数）**

我们不能漏掉正态分布！对连续分布，所有生成函数都用含 $p(x)$ 的积分而非含 $p_n$ 的求和：

```math
G(z)=\int p(x) z^x\,dx,\quad
\phi(t)=\int p(x)e^{itx}\,dx,\quad
M(t)=\int p(x)e^{tx}\,dx,\quad
K(t)=\log M(t)
\tag{15}
```

正态分布（均值 $\mu$，方差 $\sigma^2$）的矩生成函数是 $M(t)=e^{\mu t + \sigma^2 t^2/2}$。其累积量生成函数是它的对数 $K(t)=\mu t + \sigma^2 t^2/2$。所以正态分布极不寻常——只有这两个非零累积量：

```math
\kappa_1 = \mu,\quad \kappa_2 = \sigma^2,\quad \kappa_3 = 0,\quad \kappa_4 = 0,\quad\ldots
\qquad\text{(正态分布)}
```

关于累积量的关键事实：$\kappa_1=$ 均值，$\kappa_2=$ 方差，$\kappa_3=$ 三阶中心矩。因为独立过程的累积量可以相加，它们遍布 combinatorics（组合数学）、statistics（统计）和 physics（物理）。高阶累积量比 $\kappa_3$ 更复杂。

**The Central Limit Theorem（中心极限定理）**

寥寥几行，我们就能为概率论中伟大的极限定理给出论证。它关乎 standardized average（标准化均值）$Z_N = \sum (X_k - m)/(\sigma\sqrt N)$，其中 $X_1,\dots,X_N$ 是 $N$ 个均值 $m$、方差 $\sigma^2$ 的独立样本。中心极限定理说：当 $N\to\infty$ 时，$Z_N$ 的分布趋于 standard normal distribution（标准正态分布，均值 0，方差 1）。

证明用到标准化变量 $Y=(X-m)/\sigma$ 的特征函数：

```math
\mathbb E[e^{itY}] = \mathbb E\Big[1 + itY - \tfrac12 t^2 Y^2 + O(t^3)\Big]
\tag{16}
```

当然 $Z_N = (Y_1+Y_2+\cdots+Y_N)/\sqrt N$。所以它的特征函数是 $N$ 个相同函数 $Y/\sqrt N$ 特征函数的乘积（数 $t$ 固定）：

```math
\big[\mathbb E(e^{itY/\sqrt N})\big]^N
= \Big(1 - \frac{t^2}{2N}\Big)^N
\;\longrightarrow\; e^{-t^2/2}
\qquad\text{当 } N\to\infty
\tag{17}
```

而极限 $e^{-t^2/2}$ 正是标准正态分布 $N(0,1)$ 的特征函数。

**Chernoff's Inequality for Sums（和的 Chernoff 不等式）**

和 $X = X_1 + \cdots + X_n$ 的均值总是 $\bar X = \bar X_1 + \cdots + \bar X_n$。若这些变量独立，则 $X$ 的方差 $\sigma^2$ 也是各 $\sigma_i^2$ 之和。本节开头，Chebyshev 不等式给出了"样本 $X_i$ 偏离其均值 $\bar x_i$ 很远"的概率界，它同样适用于它们的和 $X$ 与 $\bar X$。

---

<!-- page 291 -->

> <span style="color:#7f8c8d;">本页为书页 289，给出和的 Chebyshev 界与 Chernoff 的指数界，并以掷币为例展示其巨大差距；页眉与印页码不译。</span>

```math
\sigma^2 = \sigma_1^2 + \cdots + \sigma_n^2
\tag{18}
```

```math
\text{和的 Chebyshev：}\quad
\Pr\big[|X - \bar X| \ge a\big] \le \frac{\sigma^2}{a^2}
```

这个不等式在 $n=1$ 时是 tight（紧的）。对一个和，能否改进？我本会猜"不能"。Chernoff 说"能"。这里有个微妙之处：Chernoff 假设的不只是每对 $X_i,X_j$ 独立，而是所有 $X_i$ 一起 joint independent（联合独立）：

```math
P(x_1,\dots,x_n) = P_1(x_1)\cdots P_n(x_n)
\tag{19}
```

一个对角协方差矩阵只需要 pairwise independence（两两独立），而式 (19) 断言得更多。它导出比 Chebyshev 不等式 (18) 强得多的、关于和的界 (20)。

Chernoff 不等式的关键点是它的 exponential bound（指数界）：远离其均值 $\bar X$ 的和 $X$ 呈指数级不可能。那是因为一个异常的和 $X = X_1+\cdots+X_n$ 通常需要好几个 $X_i$ 同时偏离各自均值 $\bar X_i$。

一个例子是掷 $n$ 枚硬币的正面数。此时每枚硬币 $X_i \in \{0,1\}$，$\Pr[X_i=1]=p_i$。正面总数 $X$ 的均值是 $\bar X = p_1 + \cdots + p_n$。

```math
\text{上 Chernoff：}\quad \Pr\big[X \ge (1+\delta)\bar X\big] \le e^{-\bar X \delta^2/3}
\tag{20}
```

```math
\text{下 Chernoff：}\quad \Pr\big[X \le (1-\delta)\bar X\big] \le e^{-\bar X \delta^2/2}
```

Michel Goemans 在他为 MIT 课程 18.310 写的在线讲义里指出了这有多强。设我们掷一枚 fair coin（公平硬币）$n$ 次，则 $\bar X = n/2$（一半正一半反）。取一个小的 $\delta^2 = (4\log n)/n$，比较 Chernoff 界 (20) 在 $\delta$ 与 $2\delta$ 处的表现。

$X\le(1-2\delta)\bar X$ 的概率远小于 $X\le(1-\delta)\bar X$ 的概率。把 $\delta$ 加倍，Chernoff 指数里的 $\delta^2$ 变成 $4\delta^2$。概率从 $1/n$ 降到 $1/n^4$：

```math
\bar X\delta^2/2 = \log n \;\Rightarrow\; \text{界 } e^{-\log n} = 1/n
```

```math
\bar X(2\delta)^2/2 = 4\log n \;\Rightarrow\; \text{界 } e^{-4\log n} = 1/n^4
```

Chebyshev 给的是 $1/4n$，而 Chernoff 给 $1/n^4$——一个指数级的差别！我们可以指出证明 Chernoff 界的关键一步。先把 $X$ 中心化使 $\bar X = 0$：

```math
\text{通常 Chebyshev：}\quad \Pr[|X|\ge a] = \Pr[X^2 \ge a^2] \le \frac{\mathbb E[x^2]}{a^2}
```

```math
\text{上 Chernoff：}\quad \Pr[X\ge a] = \Pr[e^{sX} \ge e^{sa}] \le \frac{\mathbb E[e^{sX}]}{e^{sa}}
```

```math
\text{下 Chernoff：}\quad \Pr[X \le a] = \Pr[e^{-sX} \ge e^{-sa}] \le \frac{\mathbb E[e^{-sX}]}{e^{-sa}}
```

我们需要两个指数（正、负）。尤其需要 moment generating function（矩生成函数），它给出 $M(s)=\mathbb E[e^{sX}]$ 与 $M(-s)=\mathbb E[e^{-sX}]$。然后 Chernoff 界由对 $s$ 的精心选取而来。它在 randomized linear algebra（随机化线性代数）中有许多应用。

要处理非独立样本，我们既需要方差也需要 covariances（协方差）。此外还需要矩阵版的 Markov–Chebyshev–Chernoff 不等式。这些现在登场。

---

<!-- page 292 -->

> <span style="color:#7f8c8d;">本页为书页 290，把 Markov 与 Chebyshev 不等式推广到随机矩阵，核心是半正定序与迹；页眉与印页码不译。</span>

**Markov and Chebyshev Inequalities for Matrices（矩阵的 Markov 与 Chebyshev 不等式）**

Stochastic gradient descent（随机梯度下降，见 V.1.5 节）是优化神经网络权重的既定算法。"Stochastic"意味着随机——而那些权重进了矩阵。所以深度学习统计中一个关键步骤，就是为随机矩阵的 eigenvalues（特征值）和 trace（迹）建立不等式。

我们不追求穷尽式陈述，只讲基本事实。当 $A-X$ 是 positive semidefinite（半正定，能量 $\ge 0$ 且所有特征值 $\ge 0$）时记 $X \preceq A$；否则 $X \npreceq A$，此时 $A-X$ 有一个负特征值。

**Markov 不等式** 设 $X \succeq 0$ 是一个半正定（或正定）随机矩阵，其均值为 $\mathbb E[X]=\bar X$。若 $A$ 是任一正定矩阵，则

```math
\Pr\{X \npreceq A\} = \Pr\{A-X \text{ 非半正定}\} \le \operatorname{tr}(\bar X A^{-1})
\tag{21}
```

若 $X$、$A$ 是标量 $x$、$a$，对比 Markov 不等式 $\Pr\{x \ge a\} \le \bar x/a$。

**证明** 若 $A^{1/2}$ 是 $A$ 的正定平方根，关键一步是：

```math
\operatorname{tr}(A^{-1/2} X A^{-1/2}) > 1 \quad\text{当 } X \npreceq A
\tag{22}
```

当 $A-X$ 非半正定时，必存在向量 $v$ 具有负能量 $v^T(A-X)v < 0$。令 $w = A^{1/2}v$，于是 $w^T A^{-1/2} X A^{-1/2} w > w^T w$。于是 $A^{-1/2} X A^{-1/2}$ 的最大特征值是 $\lambda_{\max} > 1$：

```math
\lambda_{\max} = \max_{y\ne 0} \frac{y^T (A^{-1/2} X A^{-1/2}) y}{y^T y}
\qquad\text{(Rayleigh quotient，瑞利商)}
```

$A^{-1/2} X A^{-1/2}$ 没有负特征值，故其迹大于 1。这就是 (22)。然后对 (22) 两边取期望即得 Markov 不等式 (21)：

```math
\Pr\{X \npreceq A\} \le \mathbb E\big[\operatorname{tr}(A^{-1/2} X A^{-1/2})\big]
= \operatorname{tr}(A^{-1/2} \bar X A^{-1/2})
= \operatorname{tr}(\bar X A^{-1})
```

现在转向 Chebyshev 不等式 $\Pr\{|X-\bar X| \ge a\} \le \sigma^2/a^2$。对对称矩阵 $A = Q\Lambda Q^T$，我们要用它的绝对值 $|A| = Q|\Lambda| Q^T$ 的一个事实：

> 若 $A^2 - B^2$ 半正定，则 $|A| - |B|$ 也半正定。

证明不完全简单，而且其逆命题不成立。我们把例子留到 Problem Set，现在先用这个事实：

**Chebyshev 不等式（对均值为 0 的随机矩阵 $X$）：**

```math
\text{若 } A \text{ 正定，则 } \Pr\{|X| \npreceq A\} \le \operatorname{tr}\big(\mathbb E[X^2]\, A^{-2}\big)
\tag{23}
```

若 $A-|X|$ 非半正定，则（如上）$A^2 - X^2$ 也非半正定：

```math
\Pr\{|X| \npreceq A\} = \Pr\{X^2 \npreceq A^2\} \le \operatorname{tr}\big(\mathbb E[X^2]\, A^{-2}\big)
```

最后一步正是对半正定矩阵 $X^2$ 的 Markov 不等式。

---

<!-- page 293 -->

> <span style="color:#7f8c8d;">本页为书页 291，引入矩阵 Chernoff 不等式，并开始定义 Erdős–Rényi 随机图与其 Laplacian 矩阵；页眉与印页码不译。</span>

Wikipedia 给出一个多维 Chebyshev 不等式，用于 $\mathbb R^n$ 中的随机向量 $x$。设其均值为 $\mathbb E[x]=m$，协方差矩阵为 $V=\mathbb E[(x-m)(x-m)^T]$。若 $V$ 正定且 $t>0$，则

```math
\Pr\big\{(x-m)^T V^{-1}(x-m) > t^2\big\} \le n/t^2
```

**Matrix Chernoff Inequalities（矩阵 Chernoff 不等式）**

Chernoff 不等式处理的是随机变量 $X_k$ 的和 $Y$——先前是标量，现在是 $n\times n$ 的 positive semidefinite（或正定）矩阵。我们看这个和的最小与最大特征值。Chernoff 的关键点是：一个和要偏离其均值很远，通常需要和里若干项都相当偏离——而这种不寻常事件的组合是指数级不可能的。于是我们得到 tail probability（尾部概率，即到均值的距离）的指数小界。

**矩阵 Chernoff** 设 $Y=\sum X_k$ 中每个矩阵 $X_k$ 的特征值满足 $0 \le \lambda \le C$。设 $\mu_{\min}$、$\mu_{\max}$ 为平均和 $\bar Y=\sum \bar X_k$ 的极端特征值。则

```math
\frac{1}{C}\log n \;\le\; \mathbb E[\lambda_{\min}(Y)] \;\le\; \mathbb E[\lambda_{\max}(Y)] \;\le\; \mu_{\max}(e-1) + C\log n
\tag{24}
```

```math
\Pr\{\lambda_{\min}(Y) \le t\mu_{\min}\} \le n\, e^{-t/2C} \quad\text{当 } t \le \frac12
\tag{25}
```

```math
\Pr\{\lambda_{\max}(Y) \ge t\mu_{\max}\} \le n\, e^{-t\mu_{\max}/C} \quad\text{当 } t \ge e
\tag{26}
```

```math
\Pr\{\lambda_{\max}(Y) \ge t\mu_{\max}\} \le n\left(\frac{e}{t}\right)^{t\mu_{\max}/C} \quad\text{当 } t \ge e
\tag{27}
```

和 $Y$ 的特征值远离其均值是 index（指数）级不可能的。Joel Tropp 的在线教材是对矩阵不等式的出色陈述。他的书为 (24–27) 中的期望与指数界证明了更精确的估计：

> Joel Tropp, *An Introduction to Matrix Concentration Inequalities*, arXiv:1501.01591.

Chernoff 之后还有多得多的不等式！我们以一个应用收尾：把不等式 (26) 用于"边随机出现的图是否连通"的概率。

**Erdős–Rényi Random Graphs（Erdős–Rényi 随机图）**

这是定义随机图的好机会。从 $n$ 个节点出发，每条边以概率 $p$ 出现。问题是：对怎样的 $p$，图很可能连通？

$n\times n$ 的 adjacency matrix（邻接矩阵）在节点 $j$、$k$ 相连时取 $M_{jk}=M_{kj}=1$。那条双向边的随机变量是 0 或 1，概率分别为 $1-p$ 与 $p$：

```math
\text{邻接矩阵 } M = \sum_{j<k} c_{jk}(E_{jk} + E_{kj})
\tag{28}
```

$E_{jk}$ 是只在位置 $(j,k)$ 有单个 1 的矩阵。Laplacian matrix（拉普拉斯矩阵）是 $L = D - M$：

```math
\text{行和减 } M:\quad L = \sum_{j<k} c_{jk}(E_{jj} + E_{kk} - E_{jk} - E_{kj})
\tag{29}
```

---

<!-- page 294 -->

> <span style="color:#7f8c8d;">本页为书页 292，分析拉普拉斯矩阵次小特征值与连通性的关系，并用矩阵 Chernoff 导出连通所需的阈值 $p$；页眉与印页码不译。</span>

对每条边（即 $c_{jk}=1$），degree matrix（度矩阵）$D$ 从 $E_{jj}+E_{kk}$ 得到两个 1，邻接矩阵 $M$ 从 $E_{jk}+E_{kj}$ 得到两个 1。合起来这四个条目使 $L$ 的那一部分特征值为 $2$ 与 $0$。所以 $L$ 半正定，且 $\lambda=0$ 有特征向量 $\mathbf 1 = (1,\dots,1)$。

当图连通时，$L$ 的 second smallest eigenvalue（次小特征值）为正。若图分成两块，我们可以把一组的节点排在另一组之前编号，则 $L$ 出现来自两块的分离 block（分块）。每个分块各有一个全 1 特征向量，故 $L$ 有 $\lambda_1=\lambda_2=0$（两个零特征值，分别对应两组的全 1 特征向量）。

我们需要一个 $n-1$ 阶随机矩阵 $Y$，其最小特征值 $\lambda_{\min}(Y)=\lambda_2(L)$。于是连通的图将有 $\lambda_{\min}(Y)>0$。一个合适的 $Y$ 是 $ULU^T$，其中 $U$ 的 $n-1$ 行是正交单位向量，且都垂直于全 1 向量 $\mathbf 1$。$Y$ 就像 $L$，但去掉了那个全 1 特征向量及其零特征值。

现在应用矩阵 Chernoff 定理，去发现何时 $\lambda_{\min}(Y)>0$、图何时连通。$Y$ 是随机矩阵 $X_{jk}$（对所有 $j\lt k$）之和：

```math
Y = ULU^T = \sum_{j<k} c_{jk}\, U(E_{jj}+E_{kk}-E_{jk}-E_{kj})U^T = \sum_{j<k} X_{jk}
\tag{30}
```

每个 $X_{jk}$ 是半正定的，且如上所述特征值为 $2$ 与 $0$（因为 $\|U\|=\|U^T\|=1$）。故 Chernoff 定理中 $C=2$。我们还需要平均矩阵 $\bar Y$ 的最小特征值。每个随机数 $c_{jk}$ 的期望值是 $p$——即包含该边的概率。于是 $\bar Y = \mathbb E[\sum X_{jk}] = p\, n\, I_{n-1}$：

```math
\bar Y = p\, U\Big(\sum_{j<k}(E_{jj}+E_{kk}-E_{jk}-E_{kj})\Big) U^T = p\, n\, I_{n-1}
\tag{31}
```

其中 $(n-1)I_n$ 那一项来自把所有对角矩阵 $E_{jj}$、$E_{kk}$ 相加；非对角矩阵 $E_{jk}$、$E_{kj}$ 加起来是 $\mathbf 1\mathbf 1^T - I$（对角为零的全 1 矩阵）。再由 $UU^T = I_{n-1}$ 即得 $p\, n\, I_{n-1}$，且我们已求出最小特征值。

现在把 Chernoff 定理中的不等式 (26) 以 $C=2$ 应用：

```math
\Pr\{\lambda_2(L) \le t p n\} = \Pr\{\lambda_{\min}(Y) \le t p n\} \le (n-1)\, e^{-(1-t)^2 p n/4}
\tag{32}
```

当 $t\to 0$ 时，关键量是 $(n-1)e^{-pn/4}$。若其对数为负，它就小于 1：

```math
\log(n-1) - \frac{p n}{4} < 0 \quad\text{或}\quad p > \frac{4\log(n-1)}{n}
\tag{33}
```

随机图的边以概率 $p$ 被包含。若 $p$ 大到满足 (33)，图就很可能连通。更精细的论证可去掉因子 4，得到随机图连通所需 $p$ 的最优 cutoff（阈值）。

[[FIGURE: 书页 292, 随机图的连通阈值示意——$p$ 高于 $4\log(n-1)/n$ 时图以高概率连通，低于阈值时以高概率不连通]]

---

<!-- page 295 -->

> <span style="color:#7f8c8d;">本页为书页 293，为 V.3 的 Problem Set（习题集），共 8 题，覆盖生成函数、累积量可加、Markov 界与矩阵迹、特征值凸性、随机图等；页眉与印页码不译。</span>

**Problem Set V.3**

1. 求 Poisson 分布 $p_n = e^{-\lambda}\lambda^n/n!$ 的概率生成函数 $G(z)$。

2. 独立随机变量 $x$、$y$ 有 $p(x,y)=p(x)p(y)$。推导其累积量生成函数的特殊性质 $K_{X+Y}(t)=K_X(t)+K_Y(t)$。

3. 一次公平掷币的结果是 $X=0$ 或 $X=1$，概率各 $\tfrac12$、$\tfrac12$。$X>\tfrac12$ 的概率是多少？证明此时 Markov 不等式给出精确概率 $\bar X/\tfrac12$。

4. 掷两颗普通骰子，结果介于 $X=2$ 到 $X=12$ 之间（两个 1 或两个 6）。均值为 7。$X>12$ 的实际概率 $p$ 是多少？证明 Markov 的 $\bar X/12$ 在 $a=12$ 这一情形下高估了该概率 $p$。

5. 这是对非负变量 $X$ 的 Markov 基本不等式的另一种证明。对 $a>0$，随机变量

```math
Y = \begin{cases} 0 & \text{若 } X < a\\ a & \text{若 } X \ge a\end{cases}
```

满足 $Y \le X$。为什么？解释最后一步 $a\,\Pr[X\ge a] = \mathbb E[Y] \le \mathbb E[X]$ 如何得到 Markov 界 $\mathbb E[X]/a$。

6. 证明随机 $Y=Y^T$ 的最大特征值是 $Y$ 的凸函数：

```math
\lambda_{\max}\Big(\sum p_i Y_i\Big) \le p_1\lambda_{\max}(Y_1) + \cdots + p_n\lambda_{\max}(Y_n)
```

7. 证明 $A-B$ 半正定但 $A^2-B^2$ 不（即找出反例）。

8. 当随机样本 $0 < x_1 < x_2 < \cdots$ 的概率为 $p_1$ 到 $p_n$ 时，证明这个惊人的恒等式：

```math
\text{mean} = \mathbb E[x] = \sum p_i x_i = \int_0^\infty \Pr[x > t]\,dt
```

提示：该概率在 $t$ 直到 $x_1$ 前为 1，之后到 $t=x_2$ 前为 $1-p_1$，依此类推。

---

> <span style="color:#27ae60;">**译者注一：Markov 不等式的实质是"用均值给尾部分布盖一个上限"。** 它的证明只有两步：先把期望 $\mathbb E[X]=\sum_s X(s)\Pr(s)$ 这一和式截断，只保留 $X(s)\ge a$ 的那些项，这一步丢掉非负项所以不增；再把这些项里的 $X(s)$ 统一下压成 $a$，这一步也不增。于是 $\mathbb E[X]\ge a\,\Pr[X\ge a]$，即 $\Pr[X\ge a]\le \mathbb E[X]/a$。它之所以"弱"，是因为它把全部质量都压缩成一个数——均值，完全丢弃了分布的 spread（离散程度）信息。这也正是 Chebyshev 改进它的方式：不对 $X$ 用 Markov，而对 $(X-\bar X)^2$ 用 Markov，把二阶信息（方差）也纳进来，得到 $\Pr[|X-\bar X|\ge a]\le \sigma^2/a^2$，衰减从 $1/a$ 提升到 $1/a^2$。Chernoff 则更进一步：对 $e^{sX}$ 用 Markov，把任意高阶矩都压进一个可调的 $s$ 里，从而得到指数衰减 $e^{-sa}M(s)$。这三者是一个连续的谱系——Markov 用一阶、Chebyshev 用二阶、Chernoff 用"全部阶"。</span>

> <span style="color:#27ae60;">**译者注二：为什么累积量要定义成 $\log$ 而不是别的？** 关键在独立可加性。若 $X,Y$ 独立，则 $\mathbb E[e^{t(X+Y)}]=\mathbb E[e^{tX}]\mathbb E[e^{tY}]$，矩生成函数是相乘的；取对数后相乘变相加，$K_{X+Y}=K_X+K_Y$。这正是我们希望一个"可加的尺度量"具备的性质——就像熵、方差（独立时）一样。于是 $K(t)$ 的 Taylor 系数（即累积量 $\kappa_n$）就是一组"独立时可加"的分布不变量。正态分布只有 $\kappa_1=\mu,\kappa_2=\sigma^2$ 非零，这解释了它在中心极限定理里的特殊地位：独立同分布样本均值标准化后，其累积量 $\kappa_3,\kappa_4,\dots$ 按 $N^{-1/2},N^{-1},\dots$ 消失，只留下前两阶，故极限只能是正态。累积量是"把分布的正态性偏差逐阶拆开"的工具——$\kappa_3$ 管偏度、$\kappa_4$ 管峰度。</span>

> <span style="color:#27ae60;">**译者注三：矩阵版不等式的核心是把标量的"序"换成半正定序（Loewner 序）。** 标量里 $x\ge a$ 是平凡的比较；矩阵没有自然的全序，于是用 $X\preceq A$（即 $A-X$ 半正定）代替。证明矩阵 Markov 不等式 (21) 的关键一步 (22)，本质上是在做一次"变换到 $A$ 的范数下再取迹"：$\operatorname{tr}(A^{-1/2}XA^{-1/2})>1$ 当且仅当 $X\npreceq A$。因为若 $A-X$ 有负能量方向 $v$，令 $w=A^{1/2}v$，则 $w^T A^{-1/2}XA^{-1/2}w > w^Tw$，说明该矩阵的 Rayleigh 商在某方向超过 1，故最大特征值 $>1$；又它半正定，迹必 $>1$。这一步和标量里"$x>a$ 则 $x/a>1$"是同一个思想，只是"除以 $a$"换成了"共轭乘以 $A^{-1/2}$"。后面随机图连通性那一整段，就是把这条矩阵 Chernoff 界套到 $Y=ULU^T$ 上，用"去掉全 1 特征向量"的技巧把 $\lambda_2(L)$ 翻译成 $\lambda_{\min}(Y)$，从而把"连通性"这个图论性质变成可套不等式的问题。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么要把一串数"变成"一个函数：生成函数背后的动机：**</span> 本节反复出现一句话——"connecting a list of numbers to a function is a powerful idea"。它的动机值得说透：一个离散随机变量 $X$ 的全部信息，本来是一列无穷多个数，比如概率列 $p_n = \Pr(X=n)$，或矩列 $m_n = E[X^n]$，或累积量列 $\kappa_n$。这列数各自为政，很难整体操作；但如果用一个幂级数 $G(z)=\sum p_n z^n$ 把它们"打包"成一个函数，那么"取第 $n$ 个系数"这种局部信息，就统一变成了"在 $z=0$ 求 $n$ 阶导数"这一个全局动作。于是三个本来看似不同的问题——求概率、求矩、求累积量——被同一个机制（式 (13) 的求导）统一起来。更关键的是，独立随机变量相加在概率空间里对应"卷积"，而在函数空间里卷积变成普通乘法：$M_{X+Y}(t)=M_X(t)M_Y(t)$，取对数后更退化成简单的加法 $K_{X+Y}=K_X+K_Y$。这就是为什么"加性"这个对独立和最有用的性质，只有在累积量生成函数 $K(t)=\log M(t)$ 上才变得如此干净。换言之，生成函数不是记号的炫技，而是把"无穷序列"和"卷积"这两种难操作的对象，翻译成"求导"和"乘法/加法"这两种好操作的对象。

> <span style="color:#1e8449;">**[note] 累积量"加性"的等价刻画：为什么定义 $K(t)=\log M(t)$：**</span> 矩(moments)和累积量(cumulants)其实是同一批信息的两种"基底"。矩生成函数 $M(t)=E[e^{tX}]$ 的泰勒系数给出各阶矩 $m_n$；而累积量生成函数 $K(t)=\log M(t)$ 的泰勒系数给出累积量 $\kappa_n$。为什么要取对数？答案就在式 $K_{X+Y}(t)=K_X(t)+K_Y(t)$（$X,Y$ 独立）。因为 $M_{X+Y}=M_X M_Y$，取对数后乘法化为加法，于是**独立变量之和的每一阶累积量都等于各自累积量之和**：$\kappa_n(X+Y)=\kappa_n(X)+\kappa_n(Y)$。而矩并不具备这个性质——$m_n(X+Y)$ 会纠缠出交叉项。这正是累积量被称为 cumulant（"累积量"）的缘由：它是"随独立求和而线性累积"的那个量。书中紧接着用伯努利分布 $K(t)=\log(1-p+pe^t)$ 验证：其一阶累积量 $\kappa_1=p$（均值），而二项分布由 $N$ 次独立抛硬币构成，故所有累积量都乘上 $N$，$\kappa_n^{\rm binomial}=N\kappa_n^{\rm Bernoulli}$，一行都不用重新算。正态分布更是极端：$M(t)=e^{\mu t+\sigma^2 t^2/2}$ 取对数得 $K(t)=\mu t+\frac{\sigma^2}{2}t^2$，只有 $\kappa_1=\mu,\ \kappa_2=\sigma^2$ 两个非零累积量，其余高阶全为零——这正是中心极限定理的代数根源，见下一条。

> <span style="color:#1e8449;">**[note] 与中心极限定理的联系：正态分布"只有两个累积量"这件事的分量：**</span> 本节对正态分布有一句看似轻描淡写的话：它的累积量生成函数是 $K(t)=\mu t+\sigma^2 t^2/2$，除 $\kappa_1,\kappa_2$ 外全部为零。这句话其实是全书最重的一步，因为它直接给中心极限定理(Central Limit Theorem)一个"三行证明"。把标准化变量 $Y=(X-m)/\sigma$ 代入特征函数，得 $E[e^{itY}]=1-\frac12 t^2+O(t^3)$；对 $N$ 个独立样本的标准化平均 $Z_N=\frac{1}{\sqrt N}\sum Y_k$，其特征函数是 $[E(e^{itY/\sqrt N})]^N \approx \left(1-\frac{t^2}{2N}\right)^N\to e^{-t^2/2}$，而 $e^{-t^2/2}$ 恰是标准正态 $N(0,1)$ 的特征函数。这个极限之所以成立，本质在于：求和平均时，一阶项 $\kappa_1$ 被"标准化"消掉，二阶项 $\kappa_2$ 保留并规整成 $t^2/2$，而三阶以上累积量随 $\frac1{\sqrt N}$ 的幂次衰减殆尽——这正是"正态只有前两个累积量"的另一种说法。所以读者会看到：累积量的加性（第二条）与"正态仅有两项"（本条的常数形式）合起来，就自动"长"出了中心极限定理。这也解释了为什么累积量贯穿组合数学、统计与物理——凡是"独立元相加"的模型，其极限行为都被前两阶累积量锁定。
