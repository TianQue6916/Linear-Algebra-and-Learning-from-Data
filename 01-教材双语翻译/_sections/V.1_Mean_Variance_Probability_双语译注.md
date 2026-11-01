# Linear Algebra and Learning From Data（线性代数与数据学习）· V.1

## 书页 263-273 ｜ PDF 页 265-275 ｜ Mean, Variance, and Probability（均值、方差与概率）

> <span style="color:#7f8c8d;">本节是全章（Probability and Statistics，概率与统计）的第一小节，先铺开三个核心词——mean（均值）、variance（方差）、probability（概率），再给出离散样本/离散概率/连续概率三种情形下均值与方差的统一写法，并顺势引出 uniform distribution（均匀分布）、normal distribution（正态分布）、Central Limit Theorem（中心极限定理）与 Monte Carlo（蒙特卡洛）估计，为后续小节做总纲式的铺垫。</span>

---

<!-- page 265 -->

> <span style="color:#7f8c8d;">本页为书页 263，属 V.1 的章首导引，交代本章 10 个主题的清单；页眉与印页码不译。</span>

**第五部分　概率与统计**

这些主题的重要性已经跃升到了前沿。当我们预测一个 output（输出）时，需要知道它的 probability（概率）；当我们度量这个 output 时，需要知道它的 statistics（统计量）。这类计算过去只局限于简单的方程和小样本。如今我们能够求解关于概率分布的微分方程（master equations，主方程），也能计算大样本的 statistics。本章旨在对这些关键思想给出一个基本理解：

1　均值 $m$ 与方差 $\sigma^2$：expected value（期望值）与 sample value（样本值）
2　概率分布与累积分布
3　协方差矩阵与联合概率
4　Normal (Gaussian) distribution（正态／高斯分布）：单变量与多变量
5　Standardized random variable（标准化随机变量）$\sigma^{-1}(x-m)$
6　The Central Limit Theorem（中心极限定理）
7　Binomial distribution（二项分布）与 uniform distribution（均匀分布）
8　Markov 与 Chebyshev 不等式（与均值的距离）
9　Weighted least squares（加权最小二乘）与 Kalman filter（卡尔曼滤波）：及其方差
10　Markov matrix（马尔可夫矩阵）与 Markov chain（马尔可夫链）

---

<!-- page 266 -->

> <span style="color:#7f8c8d;">本页为书页 264，给出 mean、variance、probability 三词的粗略定义，并用新生年龄的样本例子引出「sample mean（样本均值）与 expected value（期望值）两套口径」的关键区分；页眉与印页码不译。</span>

**V.1　均值、方差与概率**

我们从本章三个最基本的词开始：mean、variance 和 probability。在写任何公式之前，先给出它们含义的粗略解释：

- mean 是 average value（平均值）或 expected value（期望值）；
- variance（方差）$\sigma^2$ 度量的是到均值 $m$ 的「平均平方距离」；
- $n$ 个不同 outcome（结果）的 probabilities 是一组非负数 $p_1,\dots,p_n$，加起来等于 1。

均值当然最好理解，我们就从它开始。但立刻要面对两种必须分清的处境：一方面，我们可能有来自一次「已经完成」的 trial（试验）的 results（样本值）；另一方面，我们可能有来自「未来」试验的 expected results（期望值）。各举一例：

**Sample values（样本值）**　五位随机挑选的新生年龄为 $18,17,18,19,17$：

```math
\text{样本均值}=\frac{18+17+18+19+17}{5}=17.8
```

**Probabilities（概率）**　某届新生班中年龄分布为 17 岁（20%）、18 岁（50%）、19 岁（30%）。一位随机新生的 expected age（期望年龄）为

```math
E[x]=(0.2)\cdot 17+(0.5)\cdot 18+(0.3)\cdot 19=18.1
```

这两个数 17.8 与 18.1 都是正确的 averages。sample mean（样本均值）始于一次已完成试验的 $N$ 个样本 $x_1,\dots,x_N$，其均值是这 $N$ 个观测样本的平均：

```math
\text{样本均值}\quad m=\frac{1}{N}\sum_{i=1}^{N}x_i
```

而 $x$ 的 expected value 始于各年龄 $c_1,\dots,c_n$ 对应的 probabilities $p_1,\dots,p_n$：

```math
\text{期望值}\quad m=E[x]=p_1c_1+p_2c_2+\cdots+p_nc_n
```

这正是 $p\cdot c$。注意：$m=E[x]$ 告诉我们「该期待什么」，而 $m=\frac{1}{N}\sum x_i$ 告诉我们「实际得到了什么」。

一枚 fair coin（公平硬币）出现 heads（正面）的概率为 $p_0=\tfrac12$，tails（反面）概率为 $p_1=\tfrac12$。于是

```math
E[x]=\left(\tfrac12\right)\cdot 0+\left(\tfrac12\right)\cdot 1=\tfrac12
```

在 $N$ 次掷硬币中 heads 所占的比例就是 sample mean，它被期待去逼近 $\tfrac12$。只要取很多样本（大 $N$），样本结果就会越来越接近 probabilities。**Law of Large Numbers（大数定律）**说的是：以概率 1，随着样本量 $N$ 增大，sample mean 将收敛到它的期望值 $E[x]$。

这并不意味着：如果我们已经看到 tails 比 heads 多，下一次就更可能出 heads。赔率始终是五五开。前 100 次或 1000 次投掷确实会影响 sample mean，但 1000 次投掷不会影响它的极限——因为你除以的是 $N\to\infty$。

---

<!-- page 267 -->

> <span style="color:#7f8c8d;">本页为书页 265，正式定义 variance（方差）与 sample variance（样本方差），强调除以 $N-1$ 的无偏性，并给出平方和恒等式（4）这一计算捷径；页眉与印页码不译。</span>

**V.1　均值、方差与概率**

**Variance（方差，围绕均值）**

variance $\sigma^2$ 度量的是到 expected mean $E[x]$ 的「期望平方距离」；sample variance $S^2$ 度量的是到 actual sample mean 的「实际平方距离」。其平方根就是 standard deviation（标准差）$\sigma$ 或 $S$。考试之后，我会把 $\bar x$ 和 $S$ 用邮件发给全班。我不知道 expected mean 和 variance，因为我不知道每个分数对应的 probabilities $p_1,\dots,p_n$。（教了 50 年书，我依然不知道该期待什么。）

deviation（偏差）永远指相对均值的偏差——无论是样本均值还是期望均值。我们要度量的是围绕均值 $x=m$ 的「spread（离散程度）」的大小。先从 $N$ 个样本开始：

```math
\text{样本方差}\quad S^2=\frac{1}{N-1}\left[(x_1-m)^2+\cdots+(x_N-m)^2\right]\tag{3}
```

样本年龄 $18,17,18,19,17$ 的均值 $m=17.8$，该样本的方差为 $0.7$：

```math
S^2=\frac{1}{4}\left[(0.2)^2+(-0.8)^2+(0.2)^2+(1.2)^2+(-0.8)^2\right]=\frac{1}{4}(2.8)=0.7
```

一旦算平方，负号就消失了。请务必注意！统计学家除以 $N-1=4$（而不是 $N=5$），是为了让 $S^2$ 成为 $\sigma^2$ 的 unbiased estimate（无偏估计）。有一份 degree of freedom（自由度）已经被 sample mean 占掉了。

一条重要恒等式来自把每个 $(x_i-m)^2$ 拆成 $x_i^2-2mx_i+m^2$：

```math
\sum_{i=1}^{N}(x_i-m)^2
=\left(\sum x_i^2\right)-2m\left(\sum x_i\right)+Nm^2
=\left(\sum x_i^2\right)-2m(Nm)+Nm^2
=\left(\sum x_i^2\right)-Nm^2\tag{4}
```

这给出一个等价算法：先累加 $x_1^2+\cdots+x_N^2$ 再减去 $Nm^2$，就得到 $(x_1-m)^2+\cdots+(x_N-m)^2$。要求 sample variance $S^2$，再除以 $N-1$。

现在改从 probabilities $p_i$（绝不取负！）出发，而不是从样本出发。我们得到的是 expected values 而非 sample values。variance $\sigma^2$ 是统计学里最关键的数：

```math
\text{方差}\quad \sigma^2=E\left[(x-m)^2\right]=p_1(x_1-m)^2+\cdots+p_n(x_n-m)^2\tag{5}
```

我们对到期望值 $m=E[x]$ 的距离取平方。我们没有样本，只有 expectations；我们知道 probabilities，却不知道试验的实际 outcome。

**例 1**　求大学新生年龄的方差 $\sigma^2$。年龄 17、18、19 对应的 probabilities 分别是 $0.2$、$0.5$、$0.3$。

**解**　期望值已算得 $m=18.1$。方差用同一组 probabilities：

```math
\sigma^2=0.2\,(17-18.1)^2+0.5\,(18-18.1)^2+0.3\,(19-18.1)^2=0.242+0.005+0.243=0.49
```

标准差是其平方根 $\sigma=0.7$。这度量了 17、18、19 围绕 $E[x]$ 的 spread，并以 $0.2,0.5,0.3$ 加权。

式（4）给出计算 variance $\sigma^2$ 的另一条途径：

```math
\sigma^2=E[x^2]-(E[x])^2=\sum p_i x_i^2-\left(\sum p_i x_i\right)^2
```

> <span style="color:#27ae60;">**译者注·为什么样本方差要除以 $N-1$ 而不是 $N$：**设想你只用 $N=1$ 个样本来「估」方差。若除以 $N$，则 $(x_1-m)^2$ 中 $m=x_1$，结果恒为 0，仿佛数据毫无波动——这显然是错的，因为单个样本根本无法告诉我们 spread。根源在于 sample mean $m$ 本身就是用同一批数据算出来的，它已经「吃掉」了一个自由度：给定 $m$ 之后，$N$ 个偏差 $x_i-m$ 里只有 $N-1$ 个可以自由变动（它们的和固定为 0）。除以 $N-1$ 正好把这份被用掉的信息补回来，使 $S^2$ 的期望恰好等于真正的 $\sigma^2$，即无偏。这也解释了为什么式（4）里 $\sum x_i^2-Nm^2$ 之后还要除以 $N-1$：$m^2$ 项正是「sample mean 消费掉的那个自由度」的量化体现。</span>

---

<!-- page 268 -->

> <span style="color:#7f8c8d;">本页为书页 266，从离散概率过渡到连续概率，用 17–20 岁的均匀分布引入 cumulative distribution $F(x)$ 与 probability density function $p(x)$ 这一对概念及图 V.1；页眉与印页码不译。</span>

**连续概率分布**

到目前为止，我们允许 $n$ 个可能 outcome $x_1,\dots,x_n$。对于年龄 17、18、19，只有 $n=3$。若改以「天」而非「年」来度量年龄，就会有上千个可能年龄（太多了）。更好的做法是允许 17 到 20 之间的每一个数——一个连续的年龄 continuum（连续统）。于是各年龄 $c_1,c_2,\dots$ 上的 probabilities 就要换成一个覆盖连续区间 $17\le x\le 20$ 的 probability distribution（概率分布）$p(x)$。

解释概率分布最好的方式是给两个例子：uniform distribution 与 normal distribution。前者（均匀）简单，后者（正态）至关重要。

**Uniform distribution（均匀分布）**　假设年龄在 17.0 与 20.0 之间均匀分布。这两个数之间的所有年龄都「同样可能」。当然，任何一个确切的年龄本身都没有机会——恰好命中 $x=17.1$ 或 $x=17+\epsilon$ 的概率为零。你真正能如实给出的（在均匀分布假设下）是一个随机新生的年龄小于 $x$ 的概率 $F(x)$：

- 年龄小于 $x=17$ 的概率是 $F(17)=0$（17 不会发生）
- 年龄小于 $x=20$ 的概率是 $F(20)=1$（20 必然发生）
- 年龄小于 $x$ 的概率是 $F(x)=\frac13(x-17)$，$F$ 从 0 单调升到 1

这个公式 $F(x)=\frac13(x-17)$ 在 $x=17$ 处给出 $F=0$，于是 $x=17$ 不会发生；在 $x=20$ 处给出 $F(x)=1$，于是 20 是必然的。在 17 与 20 之间，cumulative distribution（累积分布）$F(x)$ 的图对这个均匀模型呈线性上升。让我画出 $F(x)$ 及其导数——probability density function（概率密度函数）$p(x)$ 的图像。

[[FIGURE: 书页 266, 图 V.1：上图为累积分布 $F(x)=\frac13(x-17)$（从 17 处的 0 线性升到 20 处的 1），下图为概率密度 $p(x)=dF/dx$（在 17 与 20 之间为常数 $\tfrac13$，其余为 0）。]]

**图 V.1：** $F(x)$ 是 cumulative distribution，其导数 $p(x)=dF/dx$ 是 probability density function (pdf)。对这个均匀分布，$p(x)$ 在 17 与 20 之间为常数。$p(x)$ 图下方总面积即总概率 $F=1$。

你可以说 $p(x)\,dx$ 是样本落在 $x$ 与 $x+dx$ 之间的概率。这在「无穷小」意义下成立：$p(x)\,dx=F(x+dx)-F(x)$。下面是 $F(x)$ 与 $p(x)$ 的完整联系：

```math
F(b)=\int_{-\infty}^{b}p(x)\,dx
```

其中「$x\lt b$ 的概率」$=F(b)$；$F(b)$ 是 $x\le b$ 的概率。我减去 $F(a)$ 以保持 $x\ge a$，于是 $a\le x\le b$ 的概率 $=F(b)-F(a)=\int_a^b p(x)\,dx$。

---

<!-- page 269 -->

> <span style="color:#7f8c8d;">本页为书页 267，给出连续分布下均值（积分 $xp(x)$）与方差（积分 $(x-m)^2p(x)$）的定义，推导均匀分布 $0$ 到 $a$ 的均值 $a/2$、方差 $a^2/12$，并引出正态分布；页眉与印页码不译。</span>

**$p(x)$ 的均值与方差**

一个概率分布的 mean $m$ 与 variance $\sigma^2$ 是什么？之前我们用「求和」得到均值（期望值）；对连续分布，我们改为对 $x\,p(x)$ 积分：

```math
\text{均值}\quad m=\int x\,p(x)\,dx=18.5
```

对这个均匀分布，均值 $m$ 恰好落在 17 与 20 的中点。于是随机值落在这个中点 $m=18.5$ 之下的概率是 $F(m)=\tfrac12$。

在 MATLAB 中，`rand(1)` 均匀地取 0 与 1 之间的随机数。从 0 到 $x$ 的区间有概率 $F(x)=x$；于是期望均值是 $m=\tfrac12$；均值以下的区间恒有概率 $F(m)=\tfrac12$。

variance 是到均值的平均平方距离。对 $N$ 个 outcome，$\sigma^2$ 是 $\sum(x_i-m)^2$ 的求和；对连续随机变量 $x$，求和变为积分：

```math
\text{方差}\quad \sigma^2=E\left[(x-m)^2\right]=\int (x-m)^2 p(x)\,dx\tag{7}
```

当年龄在 $17\le x\le 20$ 均匀时，积分可平移成 $0\le x\le 3$：

```math
\sigma^2=\frac13\int_{0}^{3}(x-1.5)^2\,dx
=\frac13\cdot\frac{(x-1.5)^3}{3}\Big|_0^3
=\frac19\left[(1.5)^3-(-1.5)^3\right]
=\frac{2}{9}(1.5)^3=0.75
```

这是一个典型例子。下面是均匀分布 $p(x)$（$0$ 到 $a$）的完整图景：

```math
\text{累积分布}\quad F(x)=\frac{x}{a},\qquad
\text{密度}\quad p(x)=\frac{1}{a},
\qquad \text{均值}\ m=\frac{a}{2},\qquad
\text{方差}\ \sigma^2=\frac{a^2}{12}
```

均值是 $a$ 的倍数，方差是 $a^2$ 的倍数。对 $a=3$，$\sigma^2=\frac{9}{12}=0.75$。对一个介于 0 与 1 之间的随机数（均值 $\tfrac12$），方差是 $\sigma^2=\frac{1}{12}$。

**Normal Distribution（正态分布）：钟形曲线**

正态分布也叫「Gaussian」分布，是所有概率密度函数 $p(x)$ 中最重要的一个。它压倒性的重要性来自「重复一个实验并对 outcome 取平均」：实验本身有自己的分布（比如正反面），而它们的平均却逼近正态分布。

---

<!-- page 270 -->

> <span style="color:#7f8c8d;">本页为书页 268，给出标准正态分布 $p(x)=\frac1{\sqrt{2\pi}}e^{-x^2/2}$ 及其三条标准事实（总概率 1、均值 0、方差 1），并借图 V.2 说明 $\pm\sigma$、$\pm2\sigma$ 的覆盖概率与「平移拉伸」得到一般 $N(m,\sigma)$ 的方法；页眉与印页码不译。</span>

**Central Limit Theorem（中心极限定理，非正式表述）**　「任意」概率分布的 $N$ 个样本的平均，当 $N\to\infty$ 时逼近一个正态分布（在 V.3 节证明）。

从 standard normal distribution（标准正态分布）开始。它关于 $x=0$ 对称，故均值 $m=0$；它被选定为方差 $\sigma^2=1$，记作 $N(0,1)$。

```math
\text{标准正态分布}\quad p(x)=\frac{1}{\sqrt{2\pi}}\,e^{-x^2/2}\tag{9}
```

它的图就是图 V.2 中的钟形曲线。标准事实是：

```math
\text{总概率}=\int_{-\infty}^{\infty}p(x)\,dx=1,\qquad
\text{均值}\ E[x]=\int x\,p(x)\,dx=0,\qquad
\text{方差}\ E[x^2]=\int x^2\,p(x)\,dx=1
```

零均值很好理解，因为我们在积分一个 odd function（奇函数）：把 $x$ 换成 $-x$ 就表明「积分 = −积分」，故该积分必为 $m=0$。另外两个积分用第 12 题的思想即可得到 1。图 V.2 画出了正态分布 $N(0,1)$ 的 $p(x)$ 以及它的累积分布（$p(x)$ 的积分）。从 $p(x)$ 的对称性可见 mean 为零；从 $F(x)$ 则可读出一条对 opinion polling（民意调查）极其实用的近似：

随机样本落在 $-x$ 与 $x$ 之间的概率是 $F(x)-F(-x)$。

```math
\int_{-x}^{x}p(x)\,dx=F(x)-F(-x)
```

同理，随机 $x$ 落在 $-2\sigma$ 与 $2\sigma$ 之间（「距均值不到两个标准差」）的概率是 $F(2\sigma)-F(-2\sigma)\approx 0.95$。若你的实验结果偏离均值超过 $2\sigma$，那几乎可以断定不是偶然：chance $=0.05$。drug tests（药物检验）可能要求更严格的确认，比如概率 0.001。寻找 Higgs boson（希格斯玻色子）时用的是偏离纯偶然 $5\sigma$ 的超严格标准。

任何均值 $m$、标准差 $\sigma$ 的正态分布，都可通过对标准 $N(0,1)$ 做平移与拉伸得到：把 $x$ 平移成 $x-m$，再把 $x-m$ 拉伸成 $(x-m)/\sigma$。

```math
\text{正态分布}\ N(m,\sigma),\qquad
\text{高斯密度}\quad p(x)=\frac{1}{\sqrt{2\pi}\,\sigma}\,e^{-(x-m)^2/2\sigma^2}\tag{10}
```

---

<!-- page 271 -->

> <span style="color:#7f8c8d;">本页为书页 269，说明累积分布 $F(x)$ 无法用初等公式写出故需查表，并借「掷硬币输出 $\pm1$」与「输出 $0/1$」两个例子演示 sample average 的均值与方差如何随 $N$ 缩放（线性律）；页眉与印页码不译。</span>

$p(x)$ 的积分是 $F(x)$——一个随机样本落在 $x$ 之下的概率。其微分 $p(x)\,dx=F(x+dx)-F(x)$ 是样本落在 $x$ 与 $x+dx$ 之间的概率。对 $\int e^{-x^2/2}dx$ 没有简单的初等公式，所以这个 cumulative distribution $F(x)$ 只能非常仔细地数值计算并制成表。

[[FIGURE: 书页 269, 图 V.2：标准正态分布 $p(x)$ 的钟形曲线（均值 $m=0$、$\sigma=1$），并在 $-2\sigma$、$0$、$2\sigma$ 处标出累积概率 0.02、0.16、0.84、0.98。]]

**图 V.2：** 标准正态分布 $p(x)$ 有均值 $m=0$ 与 $\sigma=1$。

**$N$ 次掷硬币与 $N\to\infty$**

**例 2**　设 $x$ 取 1 或 $-1$，概率各为 $p_1=p_{-1}=\tfrac12$。均值 $m=\frac12(1)+\frac12(-1)=0$，方差 $\sigma^2=\frac12(1^2)+\frac12((-1)^2)=1$。

关键问题是 average $A_N=(x_1+\cdots+x_N)/N$。这些 $x_i$ 独立且取值 $\pm1$，我们把它们的和除以 $N$。$A_N$ 的期望均值仍为零。大数定律说：这个样本平均以概率 1 趋近于零。

$A_N$ 趋近零的速度有多快？它的方差 $\sigma^2$ 是多少？

由 linearity（线性性），

```math
\sigma^2_{A_N}=\frac{1}{N^2}(\sigma^2+\cdots+\sigma^2)=\frac{N\sigma^2}{N^2}=\frac{\sigma^2}{N}=\frac{1}{N},\qquad\text{因}\ \sigma^2=1\tag{11}
```

**例 3**　把输出从 1 或 $-1$ 改成 $x=1$ 或 $x=0$，保持 $p_1=p_0=\tfrac12$。新均值 $m$ 落在 0 与 1 的中点：

```math
m=\frac12(1)+\frac12(0)=\frac12,\qquad
\sigma^2=\frac12\left(1-\frac12\right)^2+\frac12\left(0-\frac12\right)^2=\frac14
```

于是 average $A_N$ 现在有均值 $\frac12$、方差

```math
\sigma^2_{A_N}=\frac{1}{4N}\tag{12}
```

这个 $\sigma^2_{A_N}$ 是例 2 中 $\frac1N$ 的一半。这必然正确，因为新范围 $0$ 到 $1$ 的长度是 $-1$ 到 $1$ 的一半。例 2–3 展示了一条 linearity 定律。

---

<!-- page 272 -->

> <span style="color:#7f8c8d;">本页为书页 270，给出仿射变换 $x_{\text{new}}=ax_{\text{old}}+b$ 下均值与方差的线性律，并用三项数值试验与 $N=3$、$N=4$ 的二项分布演示「二项逼近正态」的过程及标准化 $X=(x-m)/\sigma$；页眉与印页码不译。</span>

新的 $0$–$1$ 变量 $x_{\text{new}}=\frac12(x_{\text{old}}+1)$，于是均值 $m$ 增至 $\frac12$，方差乘上 $\left(\frac12\right)^2$。平移改变 $m$，重标则改变 $\sigma^2$：

```math
\text{线性性}\quad x_{\text{new}}=a\,x_{\text{old}}+b
\quad\Longrightarrow\quad
m_{\text{new}}=a\,m_{\text{old}}+b,\qquad
\sigma^2_{\text{new}}=a^2\,\sigma^2_{\text{old}}\tag{13}
```

下面是三次数值试验的结果：对随机 0 或 1 做 $N$ 次平均。

- 48 个 1（来自 $N=100$）
- 5035 个 1（来自 $N=10000$）
- 19967 个 1（来自 $N=40000$）

标准化量 $X=(A_N-m)/\sigma=\left(A_N-\frac12\right)\big/\!\frac{1}{2\sqrt{N}}$ 依次为 $[-0.40]$、$[0.70]$、$[-0.33]$。

中心极限定理说：多次掷硬币的平均会逼近一个正态分布。让我们看看这是如何发生的：binomial（二项）逼近 normal。

「binomial」概率 $p_0,\dots,p_N$ 统计 $N$ 次掷硬币中 heads 的次数。对每次（公平）投掷，heads 概率为 $\tfrac12$。对 $N=3$ 次投掷，三次全是 heads 的概率是 $\left(\tfrac12\right)^3=\tfrac18$；两次 heads、一次 tails 的概率是 $\tfrac38$（来自 HHT、HTH、THH 三个序列）。这些数 $\tfrac18$ 与 $\tfrac38$ 是 $(p+q)^3$ 展开的碎片，总和 $\frac18+\frac38+\frac38+\frac18=1$。3 次投掷中 heads 的平均次数为 1.5：

```math
m=(3\ \text{heads})\frac18+(2\ \text{heads})\frac38+(1\ \text{head})\frac38+0\cdot\frac18=\frac38+\frac68+\frac38=\frac{12}{8}=1.5
```

对 $N$ 次投掷，例 3（或常识）给出均值 $m=N/2$ 个 heads。variance $\sigma^2$ 基于到该均值 $N/2$ 的平方距离。对 $N=3$，方差为 $\sigma^2=\frac34$（即 $N/4$）。为求 $\sigma^2$，以 $m=1.5$ 累加 $(x_i-m)^2$：

```math
\sigma^2=(3-1.5)^2\frac18+(2-1.5)^2\frac38+(1-1.5)^2\frac38+(0-1.5)^2\frac18=\frac{9+3+3+9}{32}=\frac{24}{32}=\frac34
```

对任意 $N$，binomial distribution 的方差是 $\sigma^2_N=N/4$，故 $\sigma_N=\sqrt{N}/2$。

图 V.3 显示 $N=4$ 次投掷中 0、1、2、3、4 个 heads 的概率如何贴近一条钟形 Gaussian。那条 Gaussian 以均值 $m=N/2=2$ 为中心。为得到标准 Gaussian（均值 0、方差 1），我们对该图做平移与重标。若 $x$ 是 $N$ 次投掷中的 heads 数——即 $N$ 个零一 outcome 之和——则把它平移其均值 $m=N/2$、重标其标准差 $\sigma=\sqrt{N}/2$，就得到标准 $X$：

```math
X=\frac{x-N/2}{\sqrt{N}/2}\qquad(N=4\ \text{时}\ X=(x-2))
```

减去 $m$ 叫 centering（中心化）或 detrending（去趋势），使 $X$ 的均值为零；除以 $\sigma$ 叫 normalizing（归一化）或 standardizing（标准化），使 $X$ 的方差为 1。

---

<!-- page 273 -->

> <span style="color:#7f8c8d;">本页为书页 271，在钟形曲线中心点核验中心极限定理的精确度：用二项系数与 Stirling 公式证明中心概率 $p_{N/2}\approx\sqrt{2/\pi N}$，与 Gaussian 中心高度一致；页眉与印页码不译。</span>

看到中心极限定理在中心点 $x=0$ 给出正确答案是件趣事。在那一点，因子 $e^{-x^2/2}$ 等于 1。我们知道 $N$ 次掷硬币的方差是 $\sigma^2=N/4$，钟形曲线的中心高度为 $\sqrt{2/\pi N}$。

那么掷硬币分布 $p_0$ 到 $p_N$（二项分布）在中心的高度是多少？对 $N=4$，0、1、2、3、4 个 heads 的概率来自 $\left(\frac12+\frac12\right)^4$：

```math
\text{中心概率}=\frac{6}{16}
```

各概率依次为 $\frac{1}{16},\frac{4}{16},\frac{6}{16},\frac{4}{16},\frac{1}{16}$。

[[FIGURE: 书页 271, 图 V.3：$N=4$ 次投掷中 heads 数的概率 $p=(1,4,6,4,1)/16$ 的直方图，其轮廓逼近一条以 $m=N/2=2$ 为中心、方差 $\sigma^2=N/4$ 的 Gaussian。]]

**图 V.3：** 4 次投掷中 heads 数的概率 $(1,4,6,4,1)/16$。这些 $p_i$ 逼近方差 $\sigma^2=N/4$、中心在 $m=N/2$ 的 Gaussian 分布。对 $X$，中心极限定理给出向 $N(0,1)$ 的收敛。

第 8 题的 binomial theorem（二项式定理）告诉我们任意偶数 $N$ 的中心概率：

```math
\text{中心概率}=\binom{N}{N/2}\left(\frac12\right)^{N/2}\left(\frac12\right)^{N/2}=\frac{N!}{(N/2)!\,(N/2)!}\,\frac{1}{2^N}
```

对 $N=4$，这些 factorial 给出 $4!/2!\,2!=24/4=6$。对大 $N$，Stirling's formula（斯特林公式）是 $N!$ 的极好近似：

```math
N!\approx\sqrt{2\pi N}\,\left(\frac{N}{e}\right)^{N}
```

对 $N$ 用一次、对 $N/2$ 用两次，得到：

```math
p_{N/2}\approx\frac{\sqrt{2\pi N}\,(N/e)^N}{\left[\sqrt{\pi N}\,(N/2e)^{N/2}\right]^2}\cdot\frac{1}{2^N}
=\sqrt{\frac{2}{\pi N}}
```

最后一步用到了掷硬币的方差 $\sigma^2=N/4$。结果 $\sqrt{2/\pi N}$ 与上面 Gaussian 的中心值一致。中心极限定理成立：中心化的二项分布在 $N\to\infty$ 时逼近正态分布 $p(x)$。

> <span style="color:#27ae60;">**译者注·为什么「中心概率 $\sqrt{2/\pi N}$」是理解中心极限定理的最佳核验点：**标准正态密度在 $x=0$ 处的值恰为 $\frac1{\sqrt{2\pi}}$，而钟形曲线的高度要反比于其标准差——标准差 $\sigma_N=\sqrt{N}/2$，故中心高度 $\propto 1/\sigma_N=\sqrt{2/\pi N}$。二项分布在中心那一格的「离散概率」与 Gaussian 在该点的「密度」能对得上，靠的是两件事：一是 Stirling 公式把阶乘的指数增长精确到常数前因子，二是中心极限定理保证的不只是「极限存在」，而是带正确 normalization 的逐点收敛。这里作者故意选 $x=0$，因为 $e^{-x^2/2}=1$ 最简，能把「概率质量如何随 $N$ 以 $1/\sqrt N$ 摊薄」这件事看得最干净。</span>

---

<!-- page 274 -->

> <span style="color:#7f8c8d;">本页为书页 272，转入 Monte Carlo（蒙特卡洛）估计：用样本平均逼近期望 $E[x]$，误差量级 $1/\sqrt N$；并介绍 Quasi-Monte Carlo 与 Multilevel Monte Carlo 两种降方差/降成本的改进；页眉与印页码不译。</span>

**Monte Carlo Estimation Methods（蒙特卡洛估计方法）**

科学计算必须处理数据中的误差，金融计算必须处理不确定的数与预测。于是大量应用数学都遇到同一个问题：接受输入中的不确定性，并估计输出中的方差。

怎样估计那个方差？概率分布 $p(x)$ 常常未知。我们能做的是：尝试不同的输入 $b$，计算 output，再取平均。这是 Monte Carlo 方法（因 Riviera 的赌场得名，我曾在那一带见过一场关于「下注是否及时」的争执）的最简单形式。

Monte Carlo 用样本平均 $(x_1+\cdots+x_N)/N$ 来逼近期望值 $E[x]$。请理解：每一个 $x_k$ 都可能算起来很昂贵——我们不是在掷硬币。每个样本来自一组数据 $b_k$。Monte Carlo 随机地选取这个数据 $b_k$，计算 output $x_k$，再对这些 $x_k$ 取平均。要对 $E[x]$ 取得像样的精度，往往需要大量样本 $b$ 和巨大的计算代价。用 $(x_1+\cdots+x_N)/N$ 逼近 $E[x]$ 的误差通常为 $1/\sqrt{N}$ 量级——随 $N$ 增大改善得很慢。

那个 $1/\sqrt N$ 估计在式（11）中已对掷硬币出现过：把 $N$ 个方差为 $\sigma^2$ 的独立样本取平均，方差降为 $\sigma^2/N$。

「Quasi-Monte Carlo（拟蒙特卡洛）」有时能把方差降到 $\sigma^2/N^2$——这是巨大的差别！其输入 $b_k$ 是精心选取的，而非单纯随机。这种 QMC 方法在期刊 *Acta Numerica* 2013 有综述。更新的「Multilevel Monte Carlo（多层蒙特卡洛）」由 Michael Giles 在 *Acta Numerica* 2015 概述。其思路如下。

假设模拟另一个接近 $x(b)$ 的变量 $y(b)$ 更便宜。那么用 $N$ 次 $y(b_k)$ 的计算、只用 $N^*\lt N$ 次 $x(b_k)$ 的计算，来估计 $E[x]$：

```math
\text{2 层蒙特卡洛}\quad E[x]\approx\frac{1}{N}\sum_{k=1}^{N}y(b_k)+\frac{1}{N^*}\sum_{k=1}^{N^*}\left[x(b_k)-y(b_k)\right]
```

想法是 $x-y$ 的方差 $\sigma^*$ 比原 $x$ 的更小，于是 $N^*$ 可以小于 $N$ 而仍对 $E[x]$ 达到同样精度。我们做 $N$ 次廉价模拟求 $y$（每次成本 $C$），只做 $N^*$ 次涉及 $x$ 的昂贵模拟（每次成本 $C^*$），总计算成本为 $NC+N^*C^*$。

微积分在固定总成本下最小化总体方差：最优比 $N^*/N$ 为 $\sigma^*/\sigma$。三层蒙特卡洛会模拟 $x$、$y$、$z$：

```math
E[x]\approx\frac{1}{N}\sum z(b_k)+\frac{1}{N^*}\sum\left[y(b_k)-z(b_k)\right]+\frac{1}{N^{**}}\sum\left[x(b_k)-y(b_k)\right]
```

Giles 优化 $N,N^*,N^{**}$ 以使 $E[x]$ 固定为 $E_0$，并提供了一份 MATLAB 代码。

> <span style="color:#27ae60;">**译者注·为什么「$x-y$ 的方差更小」能省钱，这是 variance reduction（方差缩减）的核心：**直接估计 $E[x]$，误差由 $\sigma_x/\sqrt N$ 控制，要减半误差就得把样本量翻四倍。多层蒙特卡洛换了个思路——用一个「相关且便宜」的代理 $y$ 把 $E[x]$ 写成 $E[y]+E[x-y]$。第二项 $E[x-y]$ 是对「校正量」的估计，只要 $y$ 与 $x$ 高度相关，$x-y$ 的方差 $\sigma^*$ 就远小于 $\sigma_x$，于是用很少的昂贵样本即可把它估准；而廉价的 $E[y]$ 部分尽管样本多，单次成本低。等价地说，这是拿「相关性」去换「方差」：$y$ 承担了 $x$ 的绝大部分波动，剩余残差的方差才是真正决定成本的东西。它与第 3 小节的协方差矩阵、第 9 小节 Kalman filter 的「用可测的低维量去逼近不可测的高维量」是同一类思想。</span>

---

<!-- page 275 -->

> <span style="color:#7f8c8d;">本页为书页 273，作 V.1 小节总结：用一张表并列「样本值 / 离散期望 / 连续期望」三种情形下均值与方差的三套公式，随后是 Problem Set V.1（习题 1–7）；页眉与印页码不译。</span>

**回顾：均值与方差的三套公式**

$m$ 与 $\sigma^2$ 的公式是整个概率与统计的起点。有三种必须分清的情形：sample values（样本值 $x_i$）、expected values（离散期望，$m$）、expected values（连续期望，$p(x)$）。下面列出各情形的均值 $m$ 与方差 $S^2$ 或 $\sigma^2$：

| 情形 | 均值 $m$ | 方差 $S^2$ 或 $\sigma^2$ |
|---|---|---|
| 样本 $x_1$ 到 $x_N$（输出之和） | $\displaystyle\frac{1}{N}\sum_{i=1}^{N}x_i$ | $\displaystyle\frac{1}{N-1}\sum_{i=1}^{N}(x_i-m)^2$ |
| 输出 $c_i$ 乘概率 $p_i$（求和） | $\displaystyle\sum_{i} p_i c_i$ | $\displaystyle\sum_{i} p_i(c_i-m)^2$ |
| 输出 $x$ 带概率密度 $p(x)$（积分） | $\displaystyle\int x\,p(x)\,dx$ | $\displaystyle\int (x-m)^2p(x)\,dx$ |

**习题集 V.1**

1. 上表第 1 行没有 probabilities $p$，那这些公式如何平行？答：我们期待样本中恰有比例为 $p_i$ 的样本取值 $X=c_i$。若这一点精确成立，则 $X$ 被重复 $p_iN$ 次，于是第 1 行与第 2 行给出相同的 $m$。

2. 当我们处理样本时，只是把每个 output $X$ 按其出现次数原样计入，于是得到「empirical（经验）」均值（第 1 行）而非 expected mean。

3. 把每个 output $x$ 都加 7，均值与方差会怎样？新的 sample mean、新的 expected mean、新的 variance 各是什么？

4. 我们知道：所有整数中有 $\frac13$ 能被 3 整除、$\frac17$ 能被 7 整除。能被 3 或 7（或同时被两者）整除的整数占多大比例？

5. 假设你以相等的概率 $1/1000$ 从数 1 到 1000 中抽样。样本末位数字是 $0,\dots,9$ 的概率 $p_0$ 到 $p_9$ 各是多少？该末位数字的 expected mean $m$ 是多少？其 variance $\sigma^2$ 是多少？

6. 再次从 1 到 1000 抽样，但看样本末位数字的平方。该平方的末位可为 $0,1,4,5,6,9$。概率 $p_0,p_1,p_4,p_5,p_6,p_9$ 各是多少？该数 $x$ 的（期望）均值 $m$ 与方差 $\sigma^2$ 是多少？

7. （略难）再从 1 到 1000 以等概率抽样，令 $x$ 为首位数字（若数是 15，则 $x=1$）。$x=1,\dots,9$ 的概率 $p_1$ 到 $p_9$（和为 1）各是多少？$x$ 的均值与方差是多少？

8. 假设你在第 5 题中有 $N=4$ 个样本 $157,312,696,602$。这些数平方后的首位数字 $x_1$ 到 $x_4$ 各是什么？sample mean 是多少？sample variance $S^2$ 是多少？记住要除以 $N-1=3$ 而非 $N=4$。

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么先分清 sample mean 与 expected value：**</span> 本节一开篇就反复强调要"keep straight"两种均值——已完成的试验给出的 sample value（$m=\frac{1}{N}\sum x_i$），与基于概率给出的 expected value（$m=E[x]=\sum p_i x_i$）。这不是文字游戏，而是全书概率统计的方法论分水岭：前者是"事后描述"，你手里只有一摞已经发生的观测值，均值是对它们做算术平均；后者是"事前预测"，你手里是一组概率 $p_i$（它描述的是"未来会以多大比例出现"），均值是对可能取值做加权平均。两者数值可以很接近（新生年龄例子里 $17.8$ 与 $18.1$），但来源完全不同：$E[x]$ 不依赖任何一次具体抽样的运气，只依赖概率结构；而 sample mean 会随抽样波动。全书后面所有内容——variance、covariance matrix、Central Limit Theorem、Monte Carlo——都建立在这个区分之上：凡是"已知概率"就走期望路线，凡是"只有样本"就走经验（empirical）路线。第 1 节的 Problem 1 正是追问这一点：第一行公式里没有 $p_i$，为什么能和第二行"平行"？答案是"当样本比例恰好等于概率 $p_i$ 时二者一致"——理解了这个等价条件，就理解了经验量与理论量的全部关系。

> <span style="color:#1e8449;">**[note] 关于方差除以 $N-1$ 与恒等式 $\sum(x_i-m)^2=\sum x_i^2-Nm^2$：**</span> 书里 Sample variance 定义成 $S^2=\frac{1}{N-1}\sum(x_i-m)^2$，并特别提醒"除以 $N-1$ 而不是 $N$，好让 $S^2$ 成为 $\sigma^2$ 的无偏估计"。这背后的机制是：样本均值 $m$ 本身是从这 $N$ 个数据里"用掉了一个自由度"算出来的，它已经被强行拉到了数据中心，所以每个偏差 $x_i-m$ 不是完全独立的 $N$ 个量，而只有 $N-1$ 个独立方向——直观说，若已知 $m$，前 $N-1$ 个 $x_i$ 一旦确定，第 $N$ 个就被 $\sum(x_i-m)=0$ 锁定。除以 $N$ 会系统性偏小（低估真实方差），除以 $N-1$ 恰好把这个偏差补回来。与之配套的是恒等式（4）：$\sum(x_i-m)^2=\sum x_i^2-Nm^2$，它把"先减均值再平方求和"换成"先平方求和再减掉 $Nm^2$"，这是一条单趟扫描就能算方差的捷径（只需累加 $x_i$ 与 $x_i^2$，不必先求出 $m$ 再回头算一遍），在数值计算里既省内存又减误差。注意这条恒等式对期望版同样成立，即 $\sigma^2=E[x^2]-(E[x])^2$——"方差等于平方的期望减期望的平方"，这正是 Example 1 里 $0.49$ 的另一种算法，也是全书反复出现的最重要的方差等价形式。

> <span style="color:#1e8449;">**[note] 与全书的联系：标准化与中心极限定理的伏笔：**</span> 本节末尾通过"抛硬币"这个贯穿全章的例子埋下了两条主线。第一是 linearity：把输出从 $\pm 1$ 换成 $0/1$（Example 2 到 Example 3），或一般地做变换 $x_{\text{new}}=ax_{\text{old}}+b$，则均值按 $m_{\text{new}}=a m_{\text{old}}+b$ 平移、方差按 $\sigma^2_{\text{new}}=a^2\sigma^2_{\text{old}}$ 缩放——"移位改均值、缩放平方改方差"这条规律，正是后面（V.3）把任意正态分布 $N(m,\sigma)$ 化成标准正态 $N(0,1)$ 的工具，也是本节的标准化变量 $X=(x-m)/\sigma$（"centering 再 normalizing"）的由来。第二是 $1/\sqrt{N}$ 收敛速率：$N$ 次独立样本的均值 $A_N$ 方差恰为 $\sigma^2/N$，标准差 $\sim 1/\sqrt{N}$，这既解释了 Law of Large Numbers 里样本均值"以概率 1"收敛到期望（因为波动被 $\sqrt N$ 压下去），又直接预告了 Monte Carlo 一节中"估计 $E[x]$ 的误差约 $1/\sqrt{N}$、改进极慢"这一痛点，以及 quasi-Monte Carlo 想把它压到 $1/N$ 的动机。再给一个具体数值呼应本节：五个新生年龄 $18,17,18,19,17$，$m=17.8$，用（4）式 $\sum x_i^2=18^2+17^2+18^2+19^2+17^2=1587$，$Nm^2=5\times17.8^2=1584.2$，相减得 $2.8$，除以 $N-1=4$ 正是 $S^2=0.7$——与书中的 $0.7$ 完全一致。
