# Linear Algebra and Learning From Data（线性代数与数据学习）· V.2

## 书页 275-283 ｜ PDF 页 277-285 ｜ Probability Distributions（概率分布）

> <span style="color:#7f8c8d;">本节综述概率论中最重要的七种分布——二项、泊松、指数、正态、对数正态、卡方与多元正态，逐一给出其概率密度、均值与方差的推导，并延伸到独立变量的卷积、方差-协方差矩阵，为后续 V.5 节铺路。</span>

---

<!-- page 277 -->
> <span style="color:#7f8c8d;">本页为书页 275，属 V.2 开头，先给出概率、probability density function 与七种核心分布的清单；页眉与印页码不译。</span>

概率论的应用，始于一组给出每个可能结果之概率的数字。对连续概率而言，我们有一个 density function（密度函数）$p(x)$。总概率恒等于 1，即 $\int p(x)\,dx = 1$。

$p$ 有几十种著名而实用的可能选择。我们选出了七种特别重要的：两种是离散概率，五种是连续概率 $p(x)$ 或 $p(x, y)$。

| 分布 | 中文名 | 来源 |
|---|---|---|
| Binomial | 二项分布 | 掷一枚硬币 $n$ 次 |
| Poisson | 泊松分布 | 稀有事件 |
| Exponential | 指数分布 | "遗忘过去" |
| Gaussian = Normal | 高斯分布（正态分布） | 多次试验的平均 |
| Log-normal | 对数正态分布 | 对数服从正态分布 |
| Chi-squared | 卡方分布 | $n$ 维中的距离平方 |
| Multivariable Gaussian | 多元正态分布 | 一个向量的概率（见 V.5） |

其中每一种都有一个 mean（均值）$\mu$ 和一个围绕该均值的 variance（方差）$\sigma^2$。你会想要知道这两个基本数字 $\mu$ 与 $\sigma^2$。在这个主题上，Wikipedia 的编排方式很实用——它给出了 $p(x)$ 的图像及其积分（即 cumulative distribution，累计分布，一直到 $x$ 的总概率），并系统地列出了这七种特殊分布以及其他分布的各种性质。

### 1. 二项分布（Binomial distribution）

每一次 trial（试验），结果要么是 1，要么是 0（success 成功 / failure 失败，heads 正面 / tails 反面）。成功的概率是 $p_{1,1} = p$，失败的概率是 $p_{0,1} = 1 - p = q$。一枚 fair coin（公平硬币）有 $p = \tfrac{1}{2}$。

$n = 2$ 次试验中出现 0、1、2 次成功的概率分别为

```math
p_{0,2} = (1-p)^2,\qquad p_{1,2} = 2p(1-p),\qquad p_{2,2} = p^2 .
```

$n$ 次试验中恰好 $k$ 次成功的概率涉及 binomial coefficient（二项系数）$\binom{n}{k}$：

```math
p_{k,n} = \binom{n}{k} p^k (1-p)^{n-k},\qquad \binom{n}{k} = \frac{n!}{k!(n-k)!}.
```

对 $n=2$，这些二项系数是 $1, 2, 1$，正如式 (1) 所示：

```math
\binom{2}{0} = \frac{2!}{0!\,2!} = 1,\qquad \binom{2}{1} = \frac{2!}{1!\,1!} = 2,\qquad \binom{2}{2} = \frac{2!}{2!\,0!} = 1 .
```

对公平硬币，$n=2$ 次试验中 $k=0,1,2$ 次成功的概率依次为 $p_{0,2} = \tfrac14,\ p_{1,2} = \tfrac12,\ p_{2,2} = \tfrac14$。

> <span style="color:#27ae60;">**译者注**：二项系数 $\binom{n}{k}$ 之所以是"组合数"，是因为它统计的是 $n$ 个位置上挑出 $k$ 个成功位置的方案数。每个具体序列（比如"正反正"）发生的概率都是 $p^k(1-p)^{n-k}$，而这样的序列共有 $\binom{n}{k}$ 个，于是相乘得到总概率。这体现了概率论里"先数组合、再乘单次概率"的基本套路。注意 $p_{0,2}+p_{1,2}+p_{2,2} = (1-p)^2+2p(1-p)+p^2 = (p+q)^2 = 1$，这正是二项展开定理的结论——所以它叫"二项"分布。而 $p_{1,2}=2p(1-p)$ 里的系数 2，恰好就是两次里"哪一次成功"的两种选择。</span>

---

<!-- page 278 -->
> <span style="color:#7f8c8d;">本页为书页 276，属 V.2 第 1-2 小节，先算二项分布的均值与方差，再引入泊松分布作为"稀有事件 + 大量试验"的极限；页眉与印页码不译。</span>

一次试验的 mean value（均值）$= (0)p_0 + (1)p_1 = (0)(1-p) + (1)p = p$：

```math
E[x] = p .
```

$n$ 次试验的均值是 $np$。

一次试验的 variance（方差）$= (1-p)(0-\mu)^2 + p(1-\mu)^2 = (1-p)p^2 + p(1-p)^2 = p(1-p)$：

```math
\sigma^2 = p(1-p) .
```

$n$ 次试验的方差 $\sigma^2$ 是 $n\sigma^2 = np(1-p)$。

$n$ 次独立试验的答案来得很快：乘以 $n$ 即可。同样的答案也可以更慢地从式 (2) 的二项概率 $p_{k,n}$（$k$ 次成功）推得：$\sum k\,p_{k,n}$ 仍等于 $np$，而 $\sum (k-\mu)^2 p_{k,n}$ 等于 $np(1-p)$。

> <span style="color:#27ae60;">**译者注**：均值 $np$ 与方差 $np(1-p)$ 是二项分布的标志性结论。为什么"独立试验直接乘 $n$"？因为期望是线性的：$E[x_1+\cdots+x_n]=E[x_1]+\cdots+E[x_n]$，每个 $E[x_i]=p$，加起来就是 $np$；方差在变量独立时也可加：$\mathrm{Var}(x_1+\cdots+x_n)=n\,\mathrm{Var}(x_i)=np(1-p)$。这里的"线性可加"是全书反复用到的一条主线，与后文 V.5 中协方差矩阵的对角化是同一件事——独立意味着交叉项消失。方差 $p(1-p)$ 在 $p=\tfrac12$ 时最大（$\tfrac14$），在 $p\to 0$ 或 $p\to 1$ 时趋于 0，直观地说明：结果越确定，方差越小。</span>

### 2. 泊松分布（Poisson Distribution）

泊松分布很迷人，因为逼近它的路径不止一条。一种方式是把它直接与二项分布联系起来（每次试验成功概率为 $p$，$n$ 次试验中 $k$ 次成功的概率为 $p_{k,n}$）。于是泊松解释了这样一种极限情形——稀有事件，但试验次数极多：

- $p \to 0$：每次试验的成功概率 $p$ 很小（趋于零）。
- $n \to \infty$：试验次数 $n$ 很大（趋于无穷）。
- $np = \lambda$：$n$ 次试验中成功次数的 average（期望）是 $\lambda = np$，保持为常数。

那么当 $p \to 0$ 且 $np = \lambda$ 时，$n$ 次试验中出现 $0, 1, 2$ 次成功的概率各是多少？

- $n$ 次失败、0 次成功：$p_{0,n} = (1-p)^n \approx \left(1-\dfrac{\lambda}{n}\right)^n$。
- $n-1$ 次失败、1 次成功：$p_{1,n} = np(1-p)^{n-1} \approx \lambda\left(1-\dfrac{\lambda}{n}\right)^{n-1}$。
- $n-2$ 次失败、2 次成功：$p_{2,n} = \tfrac{1}{2}n(n-1)p^2(1-p)^{n-2} \approx \tfrac{1}{2}\lambda^2\left(1-\dfrac{\lambda}{n}\right)^{n-2}$。

每一步我们都用到了微积分课程里的同一条关键事实：当 $n\to\infty$ 时，$\left(1-\dfrac{\lambda}{n}\right)^n \to e^{-\lambda}$。

---

<!-- page 279 -->
> <span style="color:#7f8c8d;">本页为书页 277，属 V.2 第 2 小节，给出泊松概率 $p_k$ 的闭式、其均值和方差均等于 $\lambda$，并讨论"稀有事件 + 独立同分布"假设的适用边界；页眉与印页码不译。</span>

对 $n$ 次试验、每次成功概率 $p=\lambda/n$ 的情形，二项概率 $p_{n,k}$ 趋近于泊松概率 $p_k$：

```math
p_k = \frac{\lambda^k e^{-\lambda}}{k!} .
```

这些泊松概率之和可验证等于 1：

```math
\sum_{k=0}^{\infty} p_k = e^{-\lambda}\left(1 + \lambda + \frac{\lambda^2}{2!} + \frac{\lambda^3}{3!} + \cdots\right) = e^{-\lambda}e^{\lambda} = 1 .
```

接下来是泊松 mean（均值）与 variance（方差）的计算（二者都等于 $\lambda$）。泊松分布的均值是 $\lambda$。慢的办法是直接求和：

```math
\mu_p = 0p_0 + 1p_1 + 2p_2 + \cdots = e^{-\lambda}\left(0 + \lambda + \frac{2\lambda^2}{2!} + \cdots\right) = \lambda .
```

快办法：泊松均值 $\mu_p$ 是二项均值 $np$ 的极限，故 $\mu_p = \lambda$。方差 $\sigma^2_p$ 是二项方差 $np(1-p)$ 的极限，故 $\sigma^2_p = \lambda$。

#### 泊松分布的应用

我们把泊松分布与稀有事件（$p \to 0$）联系在一起。但我们往往要等很长的时间、或纳入很大的人口，才能产生"确实会发生一次或多次事件"的像样概率。泊松分布不是用来算"你自己会被雷击中"的概率的——那大约是百万分之一（一生之中）。它是用来算"一座 10 万人的城市里会有人被雷击中"的概率的。此时 $\lambda = pn = 100{,}000 / 1{,}000{,}000 = 0.1$，这就是被雷击的期望次数。

泊松分布常被用于统计一段长时间内的稀有事件数量：撞击地球的大流星数目、被美洲狮袭击的露营者人数、大银行倒闭的数目。

泊松假设各事件是 **independent（独立）** 的！上面这些例子未必满足。应用概率中最困难的问题之一，就是估计一个事件对另一些事件的依赖性——一家银行倒闭可能引发更多银行倒闭。所谓 **i.i.d.** 假设（independent and identically distributed，独立同分布）并不总是成立。

> <span style="color:#27ae60;">**译者注**：泊松的"均值 = 方差 = $\lambda$"是一个漂亮的巧合，其根源在于二项分布中 $np=\lambda$ 固定而 $p\to 0$：均值 $\lambda$ 不变，方差 $np(1-p)\to \lambda$（因为 $(1-p)\to 1$）。这也给出了一个实用判据——如果你观察到某计数数据的方差显著大于均值（"过离散"，over-dispersion），就说明独立同分布假设被破坏了，事件之间存在正相关，泊松模型失效，需要更复杂的模型。作者特意点出银行倒闭的例子，正是要提醒：独立性假设一旦不成立，再漂亮的公式也只是一厢情愿。这与 V.5 中协方差非零导致矩阵不再对角化，是同一个数学现象的两种表述。</span>

---

<!-- page 280 -->
> <span style="color:#7f8c8d;">本页为书页 278，属 V.2 第 3 小节，定义指数分布作为泊松过程的等待时间，强调其"无记忆性"，并给出均值与方差；页眉与印页码不译。</span>

### 3. 指数分布（Exponential distribution）

指数分布是连续的（不是离散的）。它描述的是泊松过程中的 waiting time（等待时间）：闪电多久之后会击中你的城市？关键假设是：

> 等待时间与你已经等待的时间无关。

未来独立于过去。这对一台电视机是否会坏成立吗？对一台电脑是否会坏成立吗？如果故障来自一次随机的灾害，那么等待时间服从指数分布——failure rate（故障率）是常数。如果故障来自缓慢的衰变，独立性要求就不成立。

指数分布的 probability density function（概率密度函数，pdf）为

```math
p(x) = \lambda e^{-\lambda x},\qquad x > 0 .
```

cumulative distribution（累计分布，即事件在时刻 $t$ 之前发生的概率）是 $p$ 的积分：

```math
\int_0^t \lambda e^{-\lambda x}\,dx = 1 - e^{-\lambda t} .
```

$p(x)$ 的 mean（均值）是平均等待时间：

```math
\mu = \int_0^{\infty} x\,\lambda e^{-\lambda x}\,dx = \frac{1}{\lambda} .
```

$p(x)$ 的 variance（方差）是 $(x-\mu)^2$ 的期望：

```math
\sigma^2 = \int_0^{\infty} (x - \tfrac{1}{\lambda})^2\,\lambda e^{-\lambda x}\,dx = \frac{1}{\lambda^2} .
```

均值 $= 1/\lambda$ 这个式子并不意外。如果一家餐厅的桌子平均以每小时 3 桌的速率空出来（日夜不停），那么平均等待（期望等待时间）就是 20 分钟（$1/3$ 小时）。

注意：这个数字 $\mu = 1/\lambda$ 常常被反过来用，即用 $\mu$ 本身而不是 $\lambda$ 来写密度：

```math
p(x) = \frac{1}{\mu}\,e^{-x/\mu},\qquad \text{Mean} = \mu .
```

指数分布**没有记忆**：很遗憾，再等 $y$ 小时才有桌子的概率，不会因为你已经等了 $x$ 小时而改变：

```math
\mathrm{Prob}\{t > x+y \mid t > x\} = \mathrm{Prob}\{t > y\} .
```

这归结为对 $p(t)=\lambda e^{-\lambda t}$ 的积分的一个简单事实：

```math
\frac{\displaystyle\int_{x+y}^{\infty} \lambda e^{-\lambda t}\,dt}{\displaystyle\int_{x}^{\infty} \lambda e^{-\lambda t}\,dt}
= \frac{e^{-\lambda(x+y)}}{e^{-\lambda x}} = e^{-\lambda y} .
```

---

<!-- page 281 -->
> <span style="color:#7f8c8d;">本页为书页 279，属 V.2 第 3-4 小节，讨论独立指数变量的最小等待时间、几何分布，以及正态分布的标准形式、拐点与累计分布；页眉与印页码不译。</span>

另一个了不起的事实。假设你的手机和电脑分别有 failure rate（故障率）$\lambda_p$ 与 $\lambda_c$，且它们的故障相互独立。那么首次故障发生的时刻 $t_{\min}$ 的概率分布 $p(t_{\min})$ 是什么？答案是：这个分布也是指数分布，故障率为 $\lambda_p + \lambda_c$。看式 (9) 中的 survival（存活）而不是 failure，然后相乘：

```math
\mathrm{Prob}\{t_{\text{first}} > t\} = \mathrm{Prob}\{t_{\text{phone}} > t\}\cdot\mathrm{Prob}\{t_{\text{computer}} > t\} = e^{-\lambda_p t} e^{-\lambda_c t} = e^{-(\lambda_p+\lambda_c)t} .
```

如果故障只发生在整数时刻 $t = 0, 1, 2, 3, \dots$，那么（连续时间的）指数分布就被（离散时间的）geometric distribution（几何分布）所取代。在时刻 $n$ 发生故障的概率是 $p_n = (1-a)a^n$。因子 $1-a$ 的作用是使 $p_0 + p_1 + p_2 + \cdots = 1$，即总概率为 1。

### 4. 正态分布（Normal Distribution，又称高斯分布）

正态分布居于概率论的正中心。它是在我们对来自另一分布的许多结果取平均时产生的。同时，它还引出了我们接下来要看的几种新分布：log-normal（对数正态）、multivariate normal（多元正态）和 chi-squared（卡方）。

漂亮的公式往往仍然可能，尽管 $\int e^{-x^2/2}\,dx$ 不是 elementary function（初等函数）——从 0 到 $x$ 的那个积分无法用 $x$ 的指数与幂表示出来。幸而，从 $-\infty$ 到 $+\infty$ 的积分却有简单的形式。$\int_{-\infty}^{\infty} e^{-x^2/2}\,dx = \sqrt{2\pi}$，于是我们除以这个数来归一化。

**均值 0，方差 1**：standard normal distribution（标准正态分布）$N(0,1)$ 有

```math
p(x) = \frac{1}{\sqrt{2\pi}}\,e^{-x^2/2} .
```

**均值 $\mu$，方差 $\sigma^2$**：分布 $N(\mu, \sigma^2)$ 有

```math
p(x) = \frac{1}{\sqrt{2\pi}\,\sigma}\,e^{-(x-\mu)^2/(2\sigma^2)} .
```

这些分布在点 $x=\mu$ 处是对称的。函数 $p(x)$ 在到达该点之前递增，在 $x>\mu$ 之后递减。二阶导数在 $x=\mu-\sigma$ 与 $x=\mu+\sigma$ 之间为负。这两个点正是 inflection points（拐点），那里 $d^2p/dx^2 = 0$。在该区间之外，函数是 convex（凸，$d^2p/dx^2 > 0$）的。$p(x)$ 下方约 67% 的面积落在这个区间内，所以 $|x-\mu|<\sigma$ 的概率约为 0.67。

$|x-\mu|<2\sigma$ 的概率约为 95%（$x$ 落在距均值 2 个标准差之内）。这就是著名的 bell-shaped curve（钟形曲线，见 Figure V.2）。它不是 heavy-tailed（重尾）的。

**问题**：若 $p(x) = e^{-ax^2+bx+c}$ 是一个概率分布，那么 $a$、$b$、$c$ 各是什么？

**答案**：把这个指数 $-ax^2+bx+c$ 配成完全平方 $-a\left(x - \dfrac{b}{2a}\right)^2 + \text{常数}$。在这个形式里，我们识别出均值是 $b/2a$。括号外的数 $a$ 是 $1/(2\sigma^2)$。常数 $c$ 的作用是使 $\int p(x)\,dx = 1$。

正态分布围绕其中心点 $x=\mu$ 对称，所以它不适合取值永不为负的变量 $x$。此时 log-normal distribution（对数正态分布）也许更合适。

cumulative distribution（累计分布）是 $p(x)$ 从 $-\infty$ 到 $x$ 的积分。当 $p(x)$ 是标准正态（$\mu=0,\ \sigma^2=1$）时，它从 $-\infty$ 起的积分常写作 $\Phi(x)$：

```math
\Phi(x) = \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}}\,e^{-t^2/2}\,dt .
```

> <span style="color:#27ae60;">**译者注**：正态分布的"钟形曲线"与拐点有一个精确的几何对应：曲线从 $-\infty$ 处的 convex（下凸、开口向上）形态，经过拐点 $\mu-\sigma$ 变为 concave（上凸），在峰值 $\mu$ 处达到最大，再经过 $\mu+\sigma$ 变回 convex。这两个拐点恰好落在均值左右各一个标准差处，这也是"68% 的面积落在 $\mu\pm\sigma$ 内"的直观来源——拐点标记了曲线由"加速下降"转为"减速下降"的位置。作者用配平方的技巧，把一般二次型指数 $e^{-ax^2+bx+c}$ 的均值/方差一次性读出来（$a=1/(2\sigma^2)$、$\mu=b/2a$），这其实是把"多元正态的二次型 $\exp(-\tfrac12 x^T\Sigma^{-1}x)$"在一维情形下提前演练了一遍，与 V.5 的协方差矩阵是一脉相承的。</span>

---

<!-- page 282 -->
> <span style="color:#7f8c8d;">本页为书页 280，属 V.2 第 4 小节，引入误差函数 erf、卡方与多元正态的引出，并给出协方差矩阵与多元高斯密度的预告；页眉与印页码不译。</span>

累计分布为

```math
\Phi(x) = \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}}\,e^{-t^2/2}\,dt .
```

这与早已被制成数表的 error function（误差函数）$\mathrm{erf}(x)$ 关系极为密切：

```math
\mathrm{erf}(x) = \frac{2}{\sqrt{\pi}}\int_0^{x} e^{-s^2}\,ds .
```

我们可以把变量 $s$ 换成 $t/\sqrt{2}$，并补上从 $-\infty$ 到 0 的那段积分，于是

```math
\int_{-\infty}^{x} p(t)\,dt = \frac{1}{2} + \frac{1}{2}\,\mathrm{erf}\!\left(\frac{x}{\sqrt{2}}\right),
```

即一个 shifted and scaled（平移并缩放的）误差函数。对一般的正态分布 $N(\mu,\sigma)$，只需把 $x$ 换成 $(x-\mu)/\sigma$ 即可。

接下来的几页将描述另外两种概率分布——它们各自都很重要——它们直接来自这个一元正态分布 $p(x)$：

1. 当 $x$ 服从正态分布时，指数 $e^x$ 服从 log-normal distribution（对数正态分布）。
2. 若 $x$ 服从标准 $N(0,1)$ 分布，则 $x^2$ 服从 chi-squared distribution（卡方分布）。
3. 若 $\xi_1, \dots, \xi_n$ 是均值为零、方差为 1 的独立正态变量，则它们的和 $\xi_1 + \cdots + \xi_n$ 服从均值为零、方差为 $n$ 的正态分布。
4. $\xi_1^2 + \cdots + \xi_n^2$ 服从自由度为 $n$ 的卡方分布 $\chi^2$。

平方和之比服从 F-distribution（$F$ 分布，此处不研究）。

我们最想要的，是允许随机变量彼此**不独立**。在这种情形下，除了 variances（方差）还会有 covariances（协方差）。均值是 $\mu_1, \dots, \mu_n$：

- 方差 $=$ $(x_i - \mu_i)^2$ 的期望值。
- 协方差 $=$ $(x_i - \mu_i)(x_j - \mu_j)$ 的期望值。

这些数字填满了 V.5 节的 variance-covariance matrix（方差-协方差矩阵）$C$。当变量 $\xi_1,\dots,\xi_n$ 独立时，协方差为零，$C$ 是对角阵。当变量不独立（比如股票与债券）时，$C$ 是 symmetric（对称）且 positive definite（正定）的（极端情形下是半正定）。此时高斯变量 $\xi_1,\dots,\xi_n$ 的联合分布就是 "multivariate Gaussian"（多元高斯）：

```math
p(x) = \frac{1}{(2\pi)^{n/2}(\det C)^{1/2}}\,\exp\!\left(-\frac{1}{2}(x-\mu)^T C^{-1}(x-\mu)\right) .
```

对 $n=1$，$1\times 1$ 的协方差矩阵是 $C = [\sigma^2]$，$p(x)$ 就是通常的高斯分布。

---

<!-- page 283 -->
> <span style="color:#7f8c8d;">本页为书页 281，属 V.2 第 5-6 小节，导出对数正态分布（变量代换 $dy=dx/x$）与卡方分布的密度，并引入卷积与 $\Gamma$ 函数；页眉与印页码不译。</span>

### 5. 对数正态分布（Log-normal Distribution）

当 $y = \log x$ 服从正态分布时，$x$ 的分布就是 log-normal（对数正态）。这要求 $x > 0$。对数正态分布只适用于正的随机变量。

正态分布（由 central limit theorem，中心极限定理而来）出现在你对随机变量 $y$ 的许多独立样本取平均之时。你通过 $(\bar{y}-\mu)$ 来中心化并重新缩放，使之逼近标准正态 $N(0,1)$（$\mu=0,\ \sigma^2=1$）。类似地，对数正态分布出现在你对许多正样本值取**乘积**之时。正态的 arithmetic mean（算术平均）与对数正态的 geometric mean（几何平均）相对照。

要看出 $p(x)$ 的公式，先从 $y=\log x$ 的正态分布出发。总概率必须为 1。换元，并记住 $dy = dx/x$。这给对数正态分布 $p(x)$ 带来了一个因子 $1/x$：

```math
p(x) = \frac{1}{x\,\sigma\sqrt{2\pi}}\,\exp\!\left(-\frac{(\log x - \mu)^2}{2\sigma^2}\right),\qquad x > 0 .
```

对数正态分布的应用总是要求 $x > 0$。

### 6. 卡方分布（Chi-squared Distribution）

从一个问题开始：若 $\xi$ 服从标准正态分布（$\mu=0,\ \sigma^2=1$），那么 $s=\xi^2$ 的概率分布是什么？这就是 $s$ 的 $\chi_1^2$ 分布，其中希腊字母 chi（$\chi$）和下标 1 告诉我们：我们正在对一个标准正态变量 $\xi$ 取平方。当然 $s=\xi^2 \ge 0$。

我们需要 $s$ 落在 $y$ 与 $y+dy$ 之间的概率。这有两种方式：要么 $\sqrt{y}$ 落在 $+\sqrt{y}$ 与 $+\sqrt{y+dy}$ 之间，要么落在 $-\sqrt{y+dy}$ 与 $-\sqrt{y}$ 之间。由于标准正态关于零对称，这两种方式等可能。

又因为 $\sqrt{y+dy} = \sqrt{y} + \dfrac{dy}{2\sqrt{y}} + O\big((dy)^2\big)$：

```math
\mathrm{Prob}\{y < s < y+dy\} = 2\,\mathrm{Prob}\left\{\sqrt{y} < \xi < \sqrt{y} + \frac{dy}{2\sqrt{y}}\right\}
= 2\cdot\frac{1}{\sqrt{2\pi}}e^{-y/2}\cdot\frac{dy}{2\sqrt{y}}
= \frac{1}{\sqrt{2\pi}}\,y^{-1/2}e^{-y/2}\,dy .
```

这回答了我们的第一个问题。$s=\xi^2$ 的概率分布（记作 $\chi_1^2$ 分布）是

```math
p_1(s) = \frac{1}{\sqrt{2\pi}}\,s^{-1/2}e^{-s/2} .
```

注意：我们提一下，$s=\xi^2$ 的累计分布与式 (16) 的标准正态累计分布直接相关：

```math
\mathrm{Prob}\{s < y\} = \mathrm{Prob}\{-\sqrt{y} < \xi < \sqrt{y}\} = \Phi(\sqrt{y}) - \Phi(-\sqrt{y}) = 2\Phi(\sqrt{y}) - 1 .
```

由定义，它在 $y=s$ 处的导数就是 $\chi_1^2$ 概率分布，与式 (20) 一致：

```math
p_1(s) = \frac{d}{dy}\big[2\Phi(\sqrt{y})-1\big]\Big|_{y=s} = \frac{1}{\sqrt{2\pi}}s^{-1/2}e^{-s/2} .
```

> <span style="color:#27ae60;">**译者注**：卡方分布的本质是"对标准正态变量取平方后的分布"，其推导的核心动作是**换元与概率守恒**：区间 $[y, y+dy]$ 在 $\xi$ 轴上对应两段（正、负各一段，因为平方丢掉了符号信息），而每一段的长度是 $dy/(2\sqrt{y})$（这是 $d\sqrt{y} = dy/(2\sqrt{y})$ 的几何意义），两段加起来再乘上标准正态的密度值 $e^{-y/2}/\sqrt{2\pi}$，就得到 $p_1(s)$。这里的 $s^{-1/2}$ 因子正是 Jacobian（雅可比行列式）$ds/d\xi = 2\xi = 2\sqrt{s}$ 的倒数。这种"平方变换引入 $s^{-1/2}$ 权因子"的现象，与第 5 节对数正态里"取对数变换引入 $1/x$ 因子"是同一个机制——变量代换时，概率密度要乘上导数绝对值的倒数。</span>

---

<!-- page 284 -->
> <span style="color:#7f8c8d;">本页为书页 282，属 V.2 第 6 小节，通过卷积把卡方从 $n=1,2$ 推广到任意自由度，引入 $\Gamma$ 函数给出通式，并举例样本方差的自由度；页眉与印页码不译。</span>

现在转向两个平方之和。这是 $s_2 = \xi_1^2 + \xi_2^2$。两个标准正态变量 $\xi_1,\xi_2$ 相互独立。我们须考察所有满足 $s = \xi_1^2$ 与 $s_2 - s = \xi_2^2$、加起来等于 $s_2$ 的组合。$s_2$ 的概率分布 $p_2$ 是对所有这些组合的积分：

```math
p_2(s_2) = \int_{0}^{s_2} p_1(s)\,p_1(s_2 - s)\,ds \quad \text{（$p_1$ 与自身的卷积）}.
```

于是式 (20) 中 $p_1(s)$ 的公式推出式 (22)——原来 $n=2$ 的卡方就是 exponential distribution（指数分布）！

```math
p_2(s_2) = \int_0^{s_2}\frac{1}{\sqrt{2\pi}}s^{-1/2}e^{-s/2}\cdot\frac{1}{\sqrt{2\pi}}(s_2-s)^{-1/2}e^{-(s_2-s)/2}\,ds = \frac{1}{2}e^{-s_2/2} .
```

这种卷积给出了对每个 $n=3,4,5,\dots$ 求 $\chi_n^2$ 的成功方法。变量 $s_n$ 是 $n$ 个独立标准正态的平方和。我们可以把 $s_n$ 看成 $s_1 + s_{n-1}$，即一个平方加上 $n-1$ 个平方，然后用与式 (21) 相同的想法：

```math
p_n(s_n) = \int_{0}^{s_n} p_1(s)\,p_{n-1}(s_n - s)\,ds \quad \text{（$p_1$ 与 $p_{n-1}$ 的卷积）}.
```

这个积分 $p_n$ 具有 $C\,s_n^{(n-2)/2}e^{-s_n/2}$ 的形式。常数 $C$ 必须使总概率 $\int p_n\,ds_n$ 等于 1。integration by parts（分部积分）会稳步地把指数 $(n-2)/2$ 降下来，直到降到 $-1/2$ 或 0——这正是我们已经完成的两个情形（$n=1$ 与 $n=2$）。于是我们知道如何求 $C$，也就得到了 $s_n = \chi_n^2$（$n$ 个标准正态的平方和）的概率分布：

```math
p_n(s_n) = \frac{1}{2^{n/2}\,\Gamma(n/2)}\,s_n^{n/2-1}e^{-s_n/2} .
```

其中 Gamma function（$\Gamma$ 函数）定义为

```math
\Gamma(n) = \int_0^{\infty} t^{n-1}e^{-t}\,dt .
```

且 $\Gamma(n) = (n-1)!$，对 $n=\tfrac12$ 有 $\Gamma(\tfrac12) = \sqrt{\pi}$。

#### $\chi^2$ 的一个典型应用

我们制造某种东西，然后检验它。我们得到它厚度的样本值 $\xi_1,\dots,\xi_n$，算出平均厚度 $\bar{\xi}$ 与 sample variance（样本方差）$S^2$：

```math
\bar{\xi} = \frac{1}{n}\sum_{i=1}^n \xi_i,\qquad S^2 = \frac{1}{n-1}\sum_{i=1}^n (\xi_i - \bar{\xi})^2 .
```

$S^2$ 是自由度为 $n-1$ 的平方和。有一个自由度被均值 $\bar{\xi}$ 用掉了。对 $n=1$，$\bar{\xi}=\xi_1$ 而 $S^2=0$。对 $n=2$，$\bar{\xi}=\tfrac12(\xi_1+\xi_2)$，而 $S^2=\tfrac12(\xi_1-\xi_2)^2$。$S^2$ 服从式 (23) 给出的、自由度为 $n-1$ 的 $\chi^2_{n-1}$ 概率分布 $p_{n-1}$。

> <span style="color:#27ae60;">**译者注**：把卡方从 1 个平方推广到 $n$ 个平方，靠的是**卷积**这一核心运算。两个独立随机变量之和的密度，等于它们各自密度的卷积：$p_{X+Y}(z)=\int p_X(t)p_Y(z-t)\,dt$。这是因为要得到总和 $z$，$X$ 取 $t$、$Y$ 取 $z-t$ 的所有组合都要累加（并乘上各自的概率密度）。这里 $n=2$ 的卡方恰好算出是指数分布 $e^{-s/2}/2$，是个漂亮的巧合。样本方差 $S^2$ 除以 $n-1$ 而非 $n$，是因为用样本均值 $\bar\xi$ 代替了真实均值，损失了一个自由度——$n$ 个偏差 $(\xi_i-\bar\xi)$ 满足线性约束 $\sum(\xi_i-\bar\xi)=0$，只有 $n-1$ 个是独立的。这与线性代数里"约束条件降低秩"是同一个道理，也预示了 V.5 中协方差矩阵秩与正定性之间的关系。</span>

---

<!-- page 285 -->
> <span style="color:#7f8c8d;">本页为书页 283，属 V.2 的 Problem Set（习题集），考察两个正态分布乘积、卷积及傅里叶变换，并以掷两枚骰子的卷积作例；页眉与印页码不译。</span>

### Problem Set V.2（习题集 V.2）

**1.** 若 $p_1(x) = \dfrac{1}{\sqrt{2\pi}\,\sigma_1}\,e^{-x^2/(2\sigma_1^2)}$ 且 $p_2(x) = \dfrac{1}{\sqrt{2\pi}\,\sigma_2}\,e^{-x^2/(2\sigma_2^2)}$，证明 $p_1 p_2$ 也是一个正态分布：均值为零、方差为 $\sigma^2 = \dfrac{\sigma_1^2\sigma_2^2}{\sigma_1^2+\sigma_2^2}$。

**2.** 高斯之积仍是高斯。若 $p_1$ 与 $p_2$ 的均值分别为 $m_1$ 与 $m_2$，则 $p_1 p_2$ 的均值将是 $\dfrac{m_1\sigma_2^2 + m_2\sigma_1^2}{\sigma_1^2+\sigma_2^2}$。

**3.** 重要：这两个高斯 $p_1(x)$ 与 $p_2(x)$ 的卷积也是高斯的：

```math
(p_1 * p_2)(x) = \int_{-\infty}^{\infty} p_1(t)\,p_2(x - t)\,dt
= \frac{1}{\sqrt{2\pi(\sigma_1^2+\sigma_2^2)}}\,e^{-x^2/[2(\sigma_1^2+\sigma_2^2)]} .
```

一个漂亮的证法是取 Fourier transform（傅里叶变换）$F$ 并用 convolution theorem（卷积定理）：

```math
\widehat{p_1 * p_2} = \widehat{p_1}\,\widehat{p_2} .
```

之所以能成功，是因为这些变换 $F$ 都是 $\exp(-\sigma_i^2 k^2/2)$ 的倍数。把这些变换相乘，就得到如第 1 题那样的一个乘积，其中含有 $\sigma_1^2+\sigma_2^2$。然后再做 inverse Fourier transform（逆傅里叶变换），就把 $p_1 * p_2$ 变回另一个高斯。

**问题**：$n$ 个相同高斯 $N(0,\sigma^2)$ 的卷积，其方差是多少？

**4.** 验证卷积 $p(x) = \int p(t)\,p(x-t)\,dt$ 满足 $\int p(x)\,dx = 1$。

**5.** 解释为什么两个随机变量之和的概率分布 $P(x)$，就是它们各自概率分布 $p_1, p_2$ 的卷积。

**6.** 一个例子来自掷两枚骰子并把点数相加。和从 2 到 12 的概率分别为

```math
\frac{1}{36},\ \frac{2}{36},\ \frac{3}{36},\ \frac{4}{36},\ \frac{5}{36},\ \frac{6}{36},\ \frac{5}{36},\ \frac{4}{36},\ \frac{3}{36},\ \frac{2}{36},\ \frac{1}{36} .
```

即 $1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1$ 除以 36。

> <span style="color:#27ae60;">**译者注**：第 3 题展示了"高斯卷积仍是高斯"这一深刻性质，它正是正态分布能成为概率论中心的根本原因——你反复把独立随机变量相加（等价于不断做卷积），只要各分量方差有限，结果就不断"高斯化"，这就是中心极限定理的直观版本。而**卷积定理**（时域卷积 = 频域相乘）让这件事变得几乎平凡：高斯在傅里叶变换下仍是高斯（$\exp(-x^2/2\sigma^2)\leftrightarrow \sigma\exp(-\sigma^2k^2/2)$），相乘时方差 $\sigma_1^2+\sigma_2^2$ 直接相加。第 6 题两枚骰子之和的三角形分布（$1,2,3,4,5,6,5,4,3,2,1$）是离散卷积的最直观例子——它正是两个均匀分布 $\{1,\dots,6\}$ 的卷积，从"每个结果等可能"变成了"中间值更可能"，呼应了"和的分布比单个更集中"这一核心直觉。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么需要概率分布这个“总目录”：**</span> 本节把七个分布——Binomial（二项）、Poisson（泊松）、Exponential（指数）、Gaussian/Normal（正态）、Log-normal（对数正态）、Chi-squared（卡方）——并列摆在一起，并不是随手罗列，而是给出全书处理随机变量的**统一坐标系**。任何一个随机变量，本质上都可以被它的概率函数 $p(x)$ 完全描述；而“描述”这件事真正需要被记住的两个数字，就是均值 $\mu$ 和方差 $\sigma^2$。作者反复强调“每个分布都有均值、以及围绕均值的方差”，正是想告诉读者：与其背下几十条公式，不如先建立一种**以矩为中心**的直觉——分布只是“形状”，$\mu$ 定位置、$\sigma^2$ 定量散度。这一层铺垫直接服务于后面 V.5 节的协方差矩阵 $C$：当从单个变量推广到多个变量时，标量 $\sigma^2$ 自然升级成矩阵，而本节这七个分布就是日后多元高斯、卡方检验、对数正态收益模型的“原料库”。理解这一点，就不会把本节当成公式手册，而是把它当作通往全书其余统计内容的入口。

> <span style="color:#1e8449;">**[note] 指数分布“无记忆性”等价于一个积分恒等式：**</span> 指数分布最反直觉、也最核心的性质，是它的无记忆性：已经等待了 $x$ 小时，并不会缩短继续等待的时间，即 $\mathrm{Prob}\{t>x+y \mid t>x\}=\mathrm{Prob}\{t>y\}$。这条性质并非凭空假设，而等价于指数密度 $p(t)=\lambda e^{-\lambda t}$ 的一个代数事实——条件概率写成积分之比，分子分母中的 $e^{-\lambda x}$ 恰好约掉：

```math
\frac{\int_{x+y}^{\infty}\lambda e^{-\lambda t}\,dt}{\int_{x}^{\infty}\lambda e^{-\lambda t}\,dt}
= \frac{e^{-\lambda(x+y)}}{e^{-\lambda x}}
= e^{-\lambda y}
= \mathrm{Prob}\{t>y\}.
```

也就是说，指数分布的“过去不影响未来”，正是由 $e^{-\lambda(x+y)}=e^{-\lambda x}e^{-\lambda y}$ 这一**指数函数的乘性结构**所保证的。反过来说，如果你要求“无记忆性”成立，那么在连续情形下解出来的唯一分布就是指数分布——这是它区别于其他所有连续分布的本质原因，也解释了为什么只有指数分布适合描述“纯随机灾难”导致的等待时间（电视机因雷击而非老化而坏），而描述缓慢衰变老化时必须放弃这条假设。

> <span style="color:#1e8449;">**[note] 卡方与指数、泊松的连接及一个具体数值：**</span> 本节最具“结构美感”的一环，是卡方分布如何一层层搭出来。当 $n=2$ 时，两个独立标准正态的平方和 $s_2=x_1^2+x_2^2$ 经卷积得到 $p_2(s_2)=\tfrac{1}{2}e^{-s_2/2}$——这正是指数分布 $\lambda e^{-\lambda s}$ 在 $\lambda=\tfrac12$ 时的特例；而指数分布又是泊松过程里“首次事件等待时间”的分布。于是同一条链把 Poisson（离散计数）、Exponential（等待时间）、Chi-squared（平方和）串在了一起，读者会看到看似无关的分布其实是**同一几何对象在不同坐标下的投影**。落在一个具体数值上更直观：标准正态 $N(0,1)$ 落在 $[-1,1]$ 内的概率约为 $0.68$，其平方 $x^2$ 落在 $[0,1]$ 内的概率也是约 $0.68$；再如泊松例中，若某城市 $100{,}000$ 人被闪电击中的概率是百万分之一，则期望击中数 $\lambda=p n=100{,}000/1{,}000{,}000=0.1$，代入 $P_k=e^{-\lambda}\lambda^k/k!$，可得无人被击中的概率约为 $e^{-0.1}\approx 0.905$——这个“从参数到具体概率”的换算，正是本节所有公式真正被使用的样子。
