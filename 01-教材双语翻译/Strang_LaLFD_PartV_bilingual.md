# Part V　Probability and Statistics（概率与统计）· §V.1–§V.6

## 书页 262-320 ｜ PDF 页 264-322

---

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

---

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
p_2(s_2) = \int_{0}^{s_2} p_1(s)\,p_1(s_2 - s)\,ds \quad \text{（}p_1\text{ 与自身的卷积）}.
```

于是式 (20) 中 $p_1(s)$ 的公式推出式 (22)——原来 $n=2$ 的卡方就是 exponential distribution（指数分布）！

```math
p_2(s_2) = \int_0^{s_2}\frac{1}{\sqrt{2\pi}}s^{-1/2}e^{-s/2}\cdot\frac{1}{\sqrt{2\pi}}(s_2-s)^{-1/2}e^{-(s_2-s)/2}\,ds = \frac{1}{2}e^{-s_2/2} .
```

这种卷积给出了对每个 $n=3,4,5,\dots$ 求 $\chi_n^2$ 的成功方法。变量 $s_n$ 是 $n$ 个独立标准正态的平方和。我们可以把 $s_n$ 看成 $s_1 + s_{n-1}$，即一个平方加上 $n-1$ 个平方，然后用与式 (21) 相同的想法：

```math
p_n(s_n) = \int_{0}^{s_n} p_1(s)\,p_{n-1}(s_n - s)\,ds \quad \text{（}p_1\text{ 与 }p_{n-1}\text{ 的卷积）}.
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

---

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
\mathbb E[\lambda_{\min}(Y)] \;\ge\; \Big(1-\frac{1}{e}\Big)\mu_{\min} - C\log n
\tag{24}
```

```math
\mathbb E[\lambda_{\max}(Y)] \;\le\; (e-1)\,\mu_{\max} + C\log n
\tag{25}
```

和 $Y$ 的特征值远离其均值是 index（指数）级不可能的：

```math
\Pr\{\lambda_{\min}(Y) \le t\,\mu_{\min}\} \le n\, e^{-(1-t)^2\mu_{\min}/2C}
\tag{26}
```

```math
\Pr\{\lambda_{\max}(Y) \ge t\,\mu_{\max}\} \le n\Big(\frac{e}{t}\Big)^{t\mu_{\max}/C} \quad\text{当 } t \ge e
\tag{27}
```

Joel Tropp 的在线教材是对矩阵不等式的出色陈述。他的书为 (24–27) 中的期望与指数界证明了更精确的估计：

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

---

> <span style="color:#7f8c8d;">本节承接 V.3 的矩、累积量与不等式，从「多个实验并行测量」切入，用联合概率把方差推广为协方差矩阵，证明协方差矩阵半正定，并给出均值/方差在线性变换 $Z=AX$ 下的传播规则，最后引出相关系数与多元高斯。</span>

---

<!-- page 295 -->
> <span style="color:#7f8c8d;">本页为书页 293，属 V.3 末尾的 Problem Set（习题），是本节的题前铺陈；页眉与印页码不译。</span>

### V.3 Moments, Cumulants, and Inequalities of Statistics（统计量的矩、累积量与不等式）· 习题集

1. 求 Poisson distribution（泊松分布）$p_n = e^{-\mu}\mu^n/n!$ 的 probability generating function（概率生成函数）$G(z)$。

2. 独立随机变量 $x$ 与 $y$ 有 $p(x,y)=p(x)p(y)$。试推导它们 cumulant generating function（累积量生成函数）的特殊性质 $K_{X+Y}(t)=K_X(t)+K_Y(t)$。

3. 一枚公平硬币的投掷结果 $X=0$ 或 $X=1$，二者概率各为 $\tfrac12$。问 $X\ge\tfrac12$ 的概率是多少？试说明在此情形下 Markov inequality（马尔可夫不等式）给出精确概率 $X\ge\tfrac12$。

4. 掷两枚普通骰子，结果 $X$ 介于 $X=2$ 与 $X=12$ 之间（两个 1 或两个 6）。均值是 7。问 $X\ge 12$ 的实际概率 $p$ 是多少？试说明在 $a=12$ 时 Markov 界 $X/12$ 高估了这个概率 $p$。

5. 下面给出非负变量 $X$ 的 Markov 基本不等式的另一个证明。对 $a>0$，定义随机变量

```math
Y=\begin{cases}0, & \text{若 } X<a\\ a, & \text{若 } X\ge a\end{cases}
```

且有 $Y\le X$。为什么？试解释最后一步 $a\operatorname{Prob}[X\ge a]=E[Y]\le E[X]$ 如何导向 Markov 界 $E[X]/a$。

6. 证明随机对称矩阵 $Y=Y^{T}$ 的最大特征值 $\lambda_{\max}$ 是 $Y$ 的 convex function（凸函数）：

```math
\lambda_{\max}(Y)=\lambda_{\max}(p_1Y_1+\cdots+p_nY_n)\le p_1\lambda_{\max}(Y_1)+\cdots+p_n\lambda_{\max}(Y_n)
```

7. 证明 $A\succeq B$ positive semidefinite（半正定），但 $A^2-B^2$ 未必半正定。

8. 当随机样本 $0<\xi_1<\xi_2<\cdots<\xi_n$ 具有概率 $p_1$ 到 $p_n$ 时，证明这个惊人的恒等式：

```math
\operatorname{mean}=E[\xi]=\sum_i p_i\xi_i=\int_0^{\infty}\operatorname{Prob}(\xi>t)\,dt.
```

> 提示：该概率在 $t<\xi_1$ 时等于 1，之后到 $t=\xi_2$ 之前等于 $1-p_1$。

---

<!-- page 296 -->
> <span style="color:#7f8c8d;">本页为书页 294，是 V.4 节的开篇，引入「协方差」与「联合概率」两个核心概念，并以两枚硬币作例；页眉与印页码不译。</span>

### V.4 协方差矩阵与联合概率

当我们同时进行 $M$ 个不同实验时，linear algebra（线性代数）就登场了。我们可以同时测量年龄、身高与体重（对 $N$ 个人做 $M=3$ 个测量）。每个实验都有自己的 mean（均值），于是我们有一个向量 $m=(m_1,m_2,m_3)$，它包含 $M$ 个均值。这些可以是年龄、身高、体重的 sample mean（样本均值）；$m_1,m_2,m_3$ 也可以是基于已知概率的年龄、身高、体重的 expected value（期望值）。

当我们关注 variance（方差）时，矩阵就介入了。每个实验都有一个 sample variance（样本方差）$s^2$ 或期望方差 $\sigma^2=E[(x_i-\bar x_i)^2]$，基于其到自身均值的平方距离。这 $M$ 个数 $\sigma_1^2,\dots,\sigma_M^2$ 将落在「variance-covariance matrix（方差–协方差矩阵）」的主对角线上。至此，我们尚未在这 $M$ 个并行实验之间建立任何联系——它们测量不同的随机变量，但这些实验**未必独立**！

如果我们测量儿童的年龄、身高与体重 $(a,h,w)$，结果将是 strongly correlated（强相关）的：年纪大些的儿童通常更高、更重。假设均值 $m_a,m_h,m_w$ 已知，则 $\sigma_a^2,\sigma_h^2,\sigma_w^2$ 分别是年龄、身高、体重的各自方差。新的数是像 $\sigma_{ab}$ 这样的 covariance（协方差），它度量年龄与身高的关联。

```math
\text{Covariance}=E\big[(\text{age}-\text{mean age})(\text{height}-\text{mean height})\big]. \tag{1}
```

这个定义需要仔细审视。要计算 $c_{ah}$，仅知道每个年龄的概率和每个身高的概率是不够的，我们必须知道每一对（年龄与身高）的**联合概率**。这是因为年龄与身高是相连的。

- $p_{ah}$ = 随机儿童同时具有「年龄 $=a$ 且身高 $=h$」的概率；
- $p_{ij}$ = 实验 1 产生 $x_i$ 且实验 2 产生 $y_j$ 的概率。

假设实验 1（年龄）均值为 $m_1$，实验 2（身高）均值为 $m_2$。式 (1) 中实验 1 与实验 2 之间的协方差考察所有年龄 $x_i$ 与身高 $y_j$ 的组合，并乘以该组合的联合概率 $p_{ij}$。

```math
\text{Covariance } \sigma_{12}=\sum_{\text{all }i,j}(x_i-m_1)(y_j-m_2)\,p_{ij}. \tag{2}
```

为抓住「联合概率 $p_{ij}$」这一思想，我们从两个小例子开始。

**例 1** 分别抛两枚硬币。以 1 表示正面、0 表示反面，结果可以是 $(1,1)$、$(1,0)$、$(0,1)$ 或 $(0,0)$。这四种结果各有概率 $\tfrac14$。对独立实验，我们把概率相乘：

```math
p_{ij}=\operatorname{Prob}(i,j)=\operatorname{Prob}(i)\times \operatorname{Prob}(j).
```

---

<!-- page 297 -->
> <span style="color:#7f8c8d;">本页为书页 295，通过「粘连硬币」例 2、例 3 展示联合概率矩阵、边缘概率与完美相关，说明独立 ⇒ 协方差为 0，粘连 ⇒ 协方差矩阵奇异；页眉与印页码不译。</span>

**例 2** 把两枚硬币粘在一起，朝向相同。唯一可能的结果是 $(1,1)$ 与 $(0,0)$，二者概率各为 $\tfrac12$；概率 $p_{10}$ 与 $p_{01}$ 均为零。$(1,0)$ 与 $(0,1)$ 不会发生，因为硬币粘在一起：要么都是正面，要么都是反面。

联合概率矩阵对例 1 与例 2 分别为

```math
P_1=\begin{pmatrix}\tfrac14&\tfrac14\\ \tfrac14&\tfrac14\end{pmatrix},\qquad
P_2=\begin{pmatrix}\tfrac12&0\\ 0&\tfrac12\end{pmatrix}.
```

让我在 $P$ 上多停留一会儿，用良好的矩阵记号展示它。矩阵给出每一对 $(x_i,y_j)$ 的概率 $p_{ij}$——从 $(x_1,y_1)=(\text{正面},\text{正面})$ 与 $(x_1,y_2)=(\text{正面},\text{反面})$ 开始。注意行和 $p_1,p_2$ 与列和 $p^1,p^2$ 以及总和 $=1$。

```math
\text{概率矩阵 } P=\begin{pmatrix}p_{11}&p_{12}\\ p_{21}&p_{22}\end{pmatrix},
\quad
\begin{aligned}
p_{11}+p_{12}&=p_1 \quad \text{（第一枚硬币）}\\
p_{21}+p_{22}&=p_2 \\
\text{列和 } p^1,\ p^2 & \quad \text{（第二枚硬币）}\\
\text{4 个元素相加 }&=1
\end{aligned}
```

这些和 $p_1,p_2$ 与 $p^1,p^2$ 是联合概率矩阵 $P$ 的**边缘概率**（marginals）：

```math
\begin{aligned}
p_1&=p_{11}+p_{12}=\text{硬币 1 出现正面的机会（硬币 2 可为正或反）},\\
p^1&=p_{11}+p_{21}=\text{硬币 2 出现正面的机会（硬币 1 可为正或反）}.
\end{aligned}
```

例 1 展示了独立随机变量：每个概率 $p_{ij}$ 都等于 $p_i\times p^j$（该例中 $\tfrac12\times\tfrac12$ 给出 $p_{ij}=\tfrac14$）。此时协方差为零——第一枚硬币的正反不提供任何关于第二枚硬币的信息。

独立试验的零协方差：因为式 (2) 中每个 $p_{ij}$ 都等于 $p_i p^j$，故 $\sigma_{12}=0$。

```math
\sigma_{12}=0,\qquad \text{协方差矩阵 } V=\begin{pmatrix}\sigma_1^2&0\\0&\sigma_2^2\end{pmatrix} \text{ 为对角阵}.
```

**例 3** 粘连硬币展示**完全相关**：一枚为正意味着另一枚也为正。协方差 $\sigma_{12}$ 从 0 移动到 $\tfrac14=\tfrac12\sigma_1\cdot\tfrac12\sigma_2$ 的乘积形式，即 $\sigma_{12}=\sigma_1\sigma_2$。这是 $\sigma_{12}$ 所能取的最大值，如下面的独立计算所证实：

```math
\begin{aligned}
\text{均值}&=\tfrac12,\quad m_1=m_2=\tfrac12,\\
\sigma_{12}&=p_{11}(1-m_1)(1-m_2)+p_{22}(0-m_1)(0-m_2)\\
&=\tfrac12\cdot\tfrac12\cdot\tfrac12+\tfrac12\cdot(-\tfrac12)(-\tfrac12)=\tfrac18+\tfrac18=\tfrac14=\sigma_1\sigma_2.
\end{aligned}
```

硬币 1 的正反给出关于粘连硬币 2 正反的**完整信息**：

```math
V_{\text{glue}}=\begin{pmatrix}\sigma_1^2&\sigma_1\sigma_2\\ \sigma_1\sigma_2&\sigma_2^2\end{pmatrix},
\qquad \text{奇异协方差矩阵：}\det=0.
```

---

<!-- page 298 -->
> <span style="color:#7f8c8d;">本页为书页 296，给出核心结论：协方差矩阵 $V$ 半正定，并由秩一矩阵 $u_{ij}u_{ij}^{T}$ 的加权和构造出来；页眉与印页码不译。</span>

恒有 $\sigma_1^2\sigma_2^2\ge(\sigma_{12})^2$，故 $\sigma_{12}$ 介于 $-\sigma_1\sigma_2$ 与 $\sigma_1\sigma_2$ 之间。矩阵 $V$ 是正定的（或在粘连硬币这一奇异情形，$V$ 半正定）。这些是关于 $M$ 个实验的任意 $M\times M$ 协方差矩阵 $V$ 的重要事实。

注意，由 $N$ 次试验得到的 sample covariance matrix（样本协方差矩阵）$S$ 必然是半正定的。每个新样本 $X=(\text{年龄},\text{身高},\text{体重})$ 都对样本均值 $\bar X$（一个向量）作出贡献。每个 rank-one（秩一）项 $(X_i-\bar X)(X_i-\bar X)^{T}$ 都是 positive semidefinite（半正定）的，我们把它们相加即得到矩阵 $S$。$S$ 中不含概率，只有实际结果：

```math
S=\sum_{i=1}^{N}(X_i-\bar X)(X_i-\bar X)^{T}. \tag{3}
```

### 协方差矩阵 $V$ 是半正定的

回到两个实验（两枚硬币）之间的期望协方差 $\sigma_{12}$：

```math
\sigma_{12}=\text{期望值}\big[(\text{输出 1}-\text{均值 1})\times(\text{输出 2}-\text{均值 2})\big] \tag{4}
```

```math
\sigma_{12}=\sum_{\text{all }i,j}p_{ij}(x_i-m_1)(y_j-m_2). \tag{4'}
```

$p_{ij}\ge 0$ 是「实验 1 看到 $x_i$ 且实验 2 看到 $y_j$」的概率。某一对输出必然出现，因此这 $N^2$ 个联合概率 $p_{ij}$ 之和为 1。

```math
\text{总概率（所有组合）}=1:\quad \sum_{\text{all }i,j}p_{ij}=1. \tag{5}
```

我们还需要另一个事实。固定实验 1 中某个特定输出 $x_i$，允许实验 2 出现所有输出 $y_j$，把 $(x_i,y_1),(x_i,y_2),\dots$ 的概率相加。

```math
P \text{ 的行和 } p_i=\sum_j p_{ij}=\text{实验 1 中 } x_i \text{ 的概率}. \tag{6}
```

实验 2 中某个 $y_j$ 必然发生！无论两枚硬币是完全分开还是粘连，硬币 1 为正的概率 $p_H=p_{HH}+p_{HT}$ 都相同：

```math
\text{(分开)}\quad p_{HH}+p_{HT}=\tfrac14+\tfrac14=\tfrac12;\qquad
\text{(粘连)}\quad p_{HH}+p_{HT}=\tfrac12+0=\tfrac12.
```

这一基本推理使我们能够写出一个包含协方差 $\sigma_{12}$ 以及实验 1、实验 2 各自方差 $\sigma_1^2,\sigma_2^2$ 的矩阵公式。我们把每一对 $(i,j)$ 的矩阵 $V_{ij}$ 相加，得到整个协方差矩阵 $V$：

```math
V=\sum_{\text{all }i,j}p_{ij}
\begin{pmatrix}(x_i-m_1)^2&(x_i-m_1)(y_j-m_2)\\ (x_i-m_1)(y_j-m_2)&(y_j-m_2)^2\end{pmatrix},\qquad V=\sum_{\text{all }i,j}V_{ij}. \tag{7}
```

---

<!-- page 299 -->
> <span style="color:#7f8c8d;">本页为书页 297，说明式 (7) 如何同时给出对角线上的方差与非对角线上的协方差，并把 $V_{ij}$ 写成 $p_{ij}$ 乘秩一矩阵 $u_{ij}u_{ij}^{T}$，由此证明 $V$ 半正定；页眉与印页码不译。</span>

非对角线上，这正是式 (2) 的协方差 $\sigma_{12}$；对角线上，我们得到普通方差 $\sigma_1^2$ 与 $\sigma_2^2$。我将详细展示如何用式 (6) 得到 $V_{11}=\sigma_1^2$：让所有 $j$ 相加，只剩下实验 1 中 $x_i$ 的概率 $p_i$。

```math
V_{11}=\sum_{\text{all }i,j}p_{ij}(x_i-m_1)^2=\sum_{\text{all }i}(\text{概率 } p_i)(x_i-m_1)^2=\sigma_1^2. \tag{8}
```

请把这个看两遍。它是用一条公式 (7) 产生整个协方差矩阵的关键。这条公式之美在于它把 $2\times 2$ 矩阵 $V_{ij}$ 组合起来。而式 (7) 中每一对结果 $i,j$ 的矩阵 $V_{ij}$ 都是半正定的：$V_{ij}$ 的对角元素 $(x_i-m_1)^2\ge 0$ 与 $(y_j-m_2)^2\ge 0$，且 $\det(V_{ij})=0$。

该矩阵 $V_{ij}$ 秩为 1。式 (7) 把 $p_{ij}$ 乘以「列 $u$ 乘行 $u^{T}$」：

```math
V_{ij}=p_{ij}\begin{pmatrix}x_i-m_1\\ y_j-m_2\end{pmatrix}
\begin{pmatrix}x_i-m_1 & y_j-m_2\end{pmatrix}=p_{ij}\,u_{ij}u_{ij}^{T}. \tag{9}
```

每个矩阵 $uu^{T}$ 都是半正定的，因此整个矩阵 $V$（这些秩一矩阵之和）至少是半正定的——而且很可能 $V$ 是正定的。

除非实验之间相关，否则协方差矩阵 $V$ 是正定的。

现在我们从两个变量 $x$ 与 $y$ 推进到 $M$ 个变量，如年龄–身高–体重。每次试验的输出是含 $M$ 个分量的向量 $X$（每个儿童有一个含 3 个分量的年龄–身高–体重向量 $X$）。协方差矩阵 $V$ 现在是 $M\times M$。矩阵 $V$ 由输出向量 $X$ 及其均值 $\bar X=E[X]$ 构造：

```math
\text{Covariance matrix } V=E\big[(X-\bar X)(X-\bar X)^{T}\big]. \tag{10}
```

记住 $XX^{T}$ 与 $X\bar X^{T}=(\text{column})(\text{row})$ 都是 $M\times M$ 矩阵。对 $M=1$（一个变量），可见 $X$ 是均值 $m$，$V$ 是方差 $\sigma^2$。对 $M=2$（两枚硬币），可见 $\bar X=(m_1,m_2)$ 且 $V$ 与式 (7) 相符。期望总是「输出乘其概率」相加。对年龄–身高–体重，输出可以是 $X=(5\text{ 岁},31\text{ 英寸},48\text{ 磅})$，其概率为 $p_{ahw}$。

现在出现一个新思想。取任意线性组合 $c^{T}X=c_1X_1+\cdots+c_MX_M$。以 $c=(6,2,5)$ 为例，即 $c^{T}X=6\times\text{年龄}+2\times\text{身高}+5\times\text{体重}$。由线性性，我们知道其期望 $E[c^{T}X]$ 是 $c^{T}E[X]=c^{T}\bar X$：

```math
E[c^{T}X]=c^{T}E[X]=6\,(\text{期望年龄})+2\,(\text{期望身高})+5\,(\text{期望体重}).
```

---

<!-- page 300 -->
> <span style="color:#7f8c8d;">本页为书页 298，用「能量检验」$c^{T}Vc\ge0$ 给出 $V$ 半正定的新证明，并说明 $V=Q\Lambda Q^{T}$ 的对角化对应着寻找独立的实验组合；页眉与印页码不译。</span>

除了 $c^{T}X$ 的均值，我们还知道它的方差 $\sigma^2=c^{T}Vc$：

```math
\text{Variance of } c^{T}X=E\big[(c^{T}X-c^{T}\bar X)(c^{T}X-c^{T}\bar X)^{T}\big]=c^{T}E\big[(X-\bar X)(X-\bar X)^{T}\big]c=c^{T}Vc. \tag{11}
```

现在关键点来了：$c^{T}X$ 的方差绝不可能为负，故 $c^{T}Vc\ge 0$。

> 新证明：由能量检验 $c^{T}Vc\ge 0$，协方差矩阵 $V$ 是半正定的。

协方差矩阵 $V$ 打开了概率与线性代数之间的联系：$V$ 等于 $Q\Lambda Q^{T}$，其中特征值 $\ge 0$，orthonormal（正交归一）特征向量为 $q_1$ 到 $q_M$。对协方差矩阵 $V$ 做 diagonalize（对角化），意味着找到 $M$ 个独立的实验，作为原 $M$ 个实验的组合。

**坦白**：我对这个基于 $c^{T}Vc\ge 0$ 的证明并不完全满意。期望符号 $E$ 隐藏了联合概率这一关键思想。请允许我直接展示协方差矩阵 $V$ 是半正定的（至少对年龄–身高–体重这个例子）。证明很简单：$V$ 是每种组合（年龄、身高、体重）的联合概率 $p_{ahw}$ 乘以半正定矩阵 $uu^{T}$ 之和。这里 $u=X-\bar X$：

```math
V=\sum_{\text{all }a,h,w}p_{ahw}\,uu^{T},\qquad
u=X-\bar X=\begin{pmatrix}\text{age}-\text{mean age}\\ \text{height}-\text{mean height}\\ \text{weight}-\text{mean weight}\end{pmatrix}. \tag{12}
```

这与式 (7) 中的 $2\times 2$ 抛硬币矩阵 $V$ 完全一样，只是现在 $M=3$。

期望符号 $E$ 的价值在于它也允许 pdf（probability density function，概率密度函数）：像 $p(x,y,z)$ 这样的概率密度函数，用于连续随机变量 $x$ 与 $y$ 与 $z$。如果我们允许年龄、身高、体重的所有数值（而非离散的 age $i=0,1,2,3,\dots$），那就需要 $p(x,y,z)$ 而非 $p_{ijk}$。本书本节的和式都将变为积分，但我们仍有 $V=E[uu^{T}]$：

```math
V=\iiint p(x,y,z)\,uu^{T}\,dx\,dy\,dz,\qquad u=\begin{pmatrix}x-m_x\\ y-m_y\\ z-m_z\end{pmatrix}. \tag{13}
```

恒有 $\iiint p=1$。例 1–2 强调了 $p$ 如何给出对角的 $V$ 或奇异的 $V$：

- 独立变量 $x,y,z$：$p(x,y,z)=p(x)p(y)p(z)$。
- 相关变量 $x,y,z$：$p(x,y,z)=0$，除非 $cx+dy+ez=0$。

---

<!-- page 301 -->
> <span style="color:#7f8c8d;">本页为书页 299，推导 $z=x+y$ 的均值与方差：「均值之和等于和的均值」恒成立，而和的方差还需加上协方差项 $2\sigma_{xy}$；页眉与印页码不译。</span>

### $z=x+y$ 的均值与方差

先从 sample mean（样本均值）开始。我们有 $N$ 个 $x$ 的样本，其均值（= 平均）是数 $m_x$；我们也有 $N$ 个 $y$ 的样本，其均值是 $m_y$。$z=x+y$ 的样本均值显然为 $m_z=m_x+m_y$。

```math
\text{和的均值}=\text{均值之和}: \quad m_z=m_x+m_y. \tag{14}
```

看到这么简单的事真好。$z=x+y$ 的期望均值看起来不那么简单，但它必然得出 $E[z]=E[x]+E[y]$。下面是一种理解方式。

对 $(x_i,y_j)$ 的联合概率是 $p_{ij}$。其值取决于实验是否独立，这一点我们并不知道。但对和 $z=x+y$ 的期望而言，$x$ 与 $y$ 是否相关无关紧要——期望值仍然相加：

```math
E[z]=E[x+y]=\sum_i\sum_j(x_i+y_j)p_{ij}=\sum_i\sum_j x_i p_{ij}+\sum_i\sum_j y_j p_{ij}. \tag{15}
```

所有的和都从 1 到 $N$，我们可以任意顺序相加。对右端第一项，沿概率矩阵 $P$ 的第 $i$ 行把 $p_{ij}$ 相加得到 $p_i$，这个双重和给出 $E[x]$：

```math
\sum_i\sum_j x_i p_{ij}=\sum_i x_i\Big(\sum_j p_{ij}\Big)=\sum_i x_i p_i=E[x].
```

对最后一项，沿矩阵第 $j$ 列把 $p_{ij}$ 相加得到 $y_j$ 的概率 $p_j$。那些组合 $(x_1,y_j),(x_2,y_j),\dots,(x_N,y_j)$ 是产生 $y_j$ 的所有方式：

```math
\sum_i\sum_j y_j p_{ij}=\sum_j y_j\Big(\sum_i p_{ij}\Big)=\sum_j y_j p_j=E[y].
```

于是式 (15) 说明 $E[x+y]=E[x]+E[y]$：和的均值 = 均值之和。

那么 $z=x+y$ 的方差呢？联合概率 $p_{ij}$ 与协方差将参与进来。让我把 $x+y$ 的方差拆成三个简单部分：

```math
\begin{aligned}
\sigma_z^2&=\sum_i\sum_j p_{ij}(x_i+y_j-m_x-m_y)^2\\
&=\sum_i\sum_j p_{ij}(x_i-m_x)^2+\sum_i\sum_j p_{ij}(y_j-m_y)^2+2\sum_i\sum_j p_{ij}(x_i-m_x)(y_j-m_y).
\end{aligned}
```

第一块是 $\sigma_x^2$，第二块是 $\sigma_y^2$，最后一块是 $2\sigma_{xy}$。故 $z=x+y$ 的方差为

```math
\sigma_z^2=\sigma_x^2+\sigma_y^2+2\sigma_{xy}. \tag{16}
```

---

<!-- page 302 -->
> <span style="color:#7f8c8d;">本页为书页 300，把 $z=x+y$ 写成 $Z=AX$，得到协方差矩阵传播的核心公式 $V_Z=AV_XA^{T}$，并引入「相关系数 $\rho$」；页眉与印页码不译。</span>

### $Z=AX$ 的协方差矩阵

这是看清 $z=x+y$ 的好方法。把 $(x,y)$ 看作列向量 $X$，把 $1\times 2$ 矩阵 $A=[1\ 1]$ 乘以向量 $X=(x,y)$，则 $AX$ 就是和 $z=x+y$。式 (16) 的方差 $\sigma_z^2$ 写成矩阵记号即

```math
\sigma_z^2=[1\ 1]\begin{pmatrix}\sigma_x^2&\sigma_{xy}\\ \sigma_{xy}&\sigma_y^2\end{pmatrix}\begin{bmatrix}1\\1\end{bmatrix}=A V_X A^{T}. \tag{17}
```

可见式 (17) 中的 $\sigma_z^2=AV_XA^{T}$ 与式 (16) 中的 $\sigma_x^2+\sigma_y^2+2\sigma_{xy}$ 一致。

现在说要点。向量 $X$ 可以含来自 $M$ 个实验的 $M$ 个分量（而非只有 2 个）。这些实验有一个 $M\times M$ 协方差矩阵 $V_X$。矩阵 $A$ 可以是 $K\times M$，则 $AX$ 是一个含 $K$ 个「$M$ 个输出之组合」的向量（而非 2 个输出的一种组合 $x+y$）。

这个长度为 $K$ 的向量 $Z=AX$ 有一个 $K\times K$ 协方差矩阵 $V_Z$。于是协方差矩阵的伟大法则——式 (17) 只是其 $1\times 2$ 的例子——就是这条漂亮的公式：**$AX$ 的协方差矩阵是 $A$（$X$ 的协方差矩阵）$A^{T}$**。

```math
Z=AX \text{ 的协方差矩阵是 } V_Z=A V_X A^{T}. \tag{18}
```

对我而言，这条简洁公式展示了矩阵乘法的美。我不证明这条公式，只欣赏它——它在应用中被不断使用。

### 相关系数 $\rho$

Correlation（相关系数）$\rho_{xy}$ 与 covariance（协方差）$\sigma_{xy}$ 密切相关。二者都度量相关或独立。先对随机变量 $x$ 与 $y$ 重新缩放或「standardize（标准化）」：新的 $X=x/\sigma_x$ 与 $Y=y/\sigma_y$ 的方差为 1。这就像把向量 $v$ 除以它的长度以产生 unit vector（单位向量）$v/\|v\|$，其长度为 1。

$x$ 与 $y$ 的相关系数是 $X$ 与 $Y$ 的协方差。若 $x$ 与 $y$ 的原协方差为 $\sigma_{xy}$，则重新缩放到 $X$ 与 $Y$ 时除以 $\sigma_x$ 与 $\sigma_y$：

```math
\text{Correlation } \rho_{xy}=\operatorname{Cov}\!\Big(\frac{x}{\sigma_x},\frac{y}{\sigma_y}\Big)=\frac{\sigma_{xy}}{\sigma_x\sigma_y}.
```

恒有 $-1\le\rho_{xy}\le 1$，且 $\rho_{xy}\neq 0$ 一般不为零。零协方差给出零相关，独立随机变量产生 $\rho_{xy}=0$。

我们知道恒有 $(\sigma_{xy})^2\le\sigma_x^2\sigma_y^2$（协方差矩阵 $V$ 至少半正定），于是 $(\rho_{xy})^2\le 1$。相关接近 $p=+1$ 意味着同方向的强相关：经常投同样的票。负相关意味着当 $x$ 高于其均值时 $y$ 倾向于低于其均值：当 $\rho$ 接近 $-1$ 时投相反的票。

---

<!-- page 303 -->
> <span style="color:#7f8c8d;">本页为书页 301，以例 4（$y=-x$）给出 $\rho_{xy}=-1$ 与奇异相关矩阵，例 5 给出独立变量的相关矩阵为单位阵，并给出相关矩阵的标准化公式 $R=DVD$；页眉与印页码不译。</span>

**例 4** 假设 $y$ 就是 $-x$。一枚硬币的抛掷结果 $x=0$ 或 $1$，同一抛掷结果 $y=0$ 或 $-1$。对公平硬币，均值 $m_x=\tfrac12$，而 $m_y=-\tfrac12$。$x$ 与 $y$ 的协方差为 $\sigma_{xy}=-\sigma_x\sigma_y$。相关系数除以 $\sigma_x\sigma_y$ 得 $\rho_{xy}=-1$。此时相关矩阵 $R$ 行列式为零（奇异、仅半正定）：

```math
\text{Correlation matrix } R=\begin{pmatrix}1&\rho_{xy}\\ \rho_{xy}&1\end{pmatrix}=\begin{pmatrix}1&-1\\ -1&1\end{pmatrix},\qquad \text{当 } y=-x.
```

$R$ 的对角线上恒为 1，因为我们归一化到 $\sigma_x=\sigma_y=1$。$R$ 是 $x$ 与 $y$ 的相关矩阵，也是 $X=x/\sigma_x$ 与 $Y=y/\sigma_y$ 的协方差矩阵。这个数 $\rho_{xy}$ 也称为 Pearson 系数（Pearson coefficient）。

**例 5** 假设随机变量 $x,y,z$ 独立。$R$ 是什么矩阵？答案是单位矩阵。由定义，三个自相关 $\rho_{xx},\rho_{yy},\rho_{zz}$ 均为 1；由独立性，三个互相关 $\rho_{xy},\rho_{xz},\rho_{yz}$ 均为零。

相关矩阵 $R$ 来自协方差矩阵 $V$，当我们对每一行每一列重新缩放时——把第 $i$ 行与第 $i$ 列各除以第 $i$ 个标准差 $\sigma_i$：

1. $R=DVD$，其中对角矩阵 $D=\operatorname{diag}[1/\sigma_1,\dots,1/\sigma_M]$，则每个 $R_{ii}=1$。
2. 若协方差 $V$ 正定，则相关矩阵 $R=DVD$ 也正定。

#### 例题

假设 $x$ 与 $y$ 是均值 0、方差 1 的独立随机变量，则 $X=(x,y)$ 的协方差矩阵 $V_X$ 是 $2\times 2$ 单位矩阵。问 3 分量向量 $Z=(x,y,ax+by)$ 的均值 $m_z$ 与协方差矩阵 $V_Z$ 是多少？

**解**：$Z$ 与 $X$ 通过 $A$ 联系：$Z=\begin{bmatrix}x\\y\\ax+by\end{bmatrix}=\begin{bmatrix}1&0\\0&1\\a&b\end{bmatrix}\begin{bmatrix}x\\y\end{bmatrix}=AX$。

向量 $m_X$ 含 $X$ 的 $M$ 个分量的均值，向量 $m_Z$ 含 $Z=AX$ 的 $K$ 个分量的均值。$X$ 与 $Z$ 均值之间的矩阵联系必须是线性的：$m_Z=A m_X$。$ax+by$ 的均值是 $a m_x+b m_y$。

---

<!-- page 304 -->
> <span style="color:#7f8c8d;">本页为书页 302，完成例题（$V_Z=AA^{T}$、秩仅 2 的奇异矩阵），并以差分 GPS 作为 $V_Z=AV_XA^{T}$ 降方差的应用实例收尾；页眉与印页码不译。</span>

当 $V_X$ 是 $2\times 2$ 单位矩阵时，$Z$ 的协方差矩阵为 $V_Z=AA^{T}$：

```math
V_Z=AA^{T}=\begin{pmatrix}1&0\\0&1\\a&b\end{pmatrix}
\begin{pmatrix}1&0&a\\0&1&b\end{pmatrix}
=\begin{pmatrix}1&0&a\\0&1&b\\a&b&a^2+b^2\end{pmatrix}.
```

**解释**：$x$ 与 $y$ 独立，协方差 $\sigma_{xy}=0$。于是 $x$ 与 $ax+by$ 的协方差是 $a$，$y$ 与 $ax+by$ 的协方差是 $b$。它们正好来自 $ax+by$ 的两个独立部分。最后，式 (18) 给出 $ax+by$ 的方差：

```math
\sigma_{ax+by}^2=a^2\sigma_x^2+b^2\sigma_y^2+2ab\,\sigma_{xy}=a^2+b^2+0=a^2+b^2.
```

这个 $3\times 3$ 矩阵 $V_Z$ 是奇异的，其行列式为 $a^2+b^2-(a^2+b^2)=0$。第三分量 $z=ax+by$ 完全依赖于 $x$ 与 $y$，$V_Z$ 的秩仅为 2。

#### GPS 例子

GPS 卫星的信号包含其发射时刻，接收机时钟给出到达时刻。接收机把传播时间乘以光速，就知道到该卫星的距离。来自四颗或更多卫星的距离（用最小二乘法！）将精确定位接收机位置。

一个问题：光速在电离层中会改变。但这一修正对所有附近的接收机几乎相同。如果一台接收机停在已知位置，我们可以对其取差分。差分 GPS（Differential GPS）通过固定一台接收机来减小误差方差：

```math
\text{Difference matrix } A=[1\ -1],\qquad
V_Z=A V_X A^{T}=[1\ -1]\begin{pmatrix}\sigma_1^2&\sigma_{12}\\ \sigma_{12}&\sigma_2^2\end{pmatrix}\begin{bmatrix}1\\-1\end{bmatrix}
=\sigma_1^2-2\sigma_{12}+\sigma_2^2.
```

光速的误差消失了，于是厘米级定位精度是可达到的。（关键思想见 Borre 与 Strang 的 *Algorithms for Global Positioning* 第 320 页。）

GPS 的世界关乎时间与空间与惊人的精度。

### 习题 V.4

1. (a) 当硬币抛掷概率为 $p$ 与 $1-p$（反面 = 0，正面 = 1）时，计算方差 $\sigma^2$。
   (b) $N$ 次独立抛掷（0 或 1）之和是 $N$ 次尝试后正面的次数。用和的方差规则 (16–17–18) 给出 $\sigma^2$。

2. 实验 3 的结果 $x_1,\dots,x_m$ 与实验 5 的结果 $y_1,\dots,y_n$ 之间的协方差是什么？你的公式应形如式 (2) 中的 $\sigma_{12}$。于是协方差矩阵 $V$ 的 $(3,5)$ 与 $(5,3)$ 元素是 $\sigma_{35}=\sigma_{53}$。

3. 对 $M=3$ 个实验，方差–协方差矩阵 $V$ 将是 $3\times 3$。存在一个概率 $p_{ijk}$，表示三个输出分别为 $x_i,y_j,z_k$。写出一个形如式 (7) 的矩阵 $V$ 的公式。

---

<!-- page 305 -->
> <span style="color:#7f8c8d;">本页为书页 303，续习题：独立实验的协方差矩阵、线性变换的线性性解释，以及条件概率的记号与和式法则、乘积法则、贝叶斯定理；页眉与印页码不译。</span>

4. $M=3$ 个独立实验、均值为 $m_1,m_2,m_3$、方差为 $\sigma_1^2,\sigma_2^2,\sigma_3^2$ 时的协方差矩阵 $V$ 是什么？

5. 当输出 $X$ 的协方差矩阵为 $V$ 时，输出 $Z=AX$ 的协方差矩阵是 $A V A^{T}$。用线性性解释这条简洁公式：

```math
V_Z=E\big[(AX-A\bar X)(AX-A\bar X)^{T}\big]=A\,E\big[(X-\bar X)(X-\bar X)^{T}\big]A^{T}=A V A^{T}.
```

习题 6–10 关于「已知 $X=x_i$ 时 $Y=y_j$」的条件概率。记号：$\operatorname{Prob}(Y=y_j\mid X=x_i)=$ 在 $X=x_i$ 已知条件下结果 $y_j$ 的概率。

- 例 1：硬币 1 粘在硬币 2 上，则 $\operatorname{Prob}(Y=\text{正面}\mid X=\text{正面})=1$。
- 例 2：独立抛硬币，$X$ 不提供关于 $Y$ 的信息，知道 $X$ 无用，则 $\operatorname{Prob}(Y=\text{正面}\mid X=\text{正面})$ 与 $\operatorname{Prob}(Y=\text{正面})$ 相同。

6. 解释条件概率的和式法则：

```math
\operatorname{Prob}(Y=y_j)=\sum_{\text{all }x_i}\operatorname{Prob}(Y=y_j\mid X=x_i)\,\operatorname{Prob}(X=x_i).
```

7. $n\times n$ 矩阵 $P$ 含联合概率 $p_{ij}=\operatorname{Prob}(X=x_i\text{ 且 }Y=y_j)$。解释为何条件概率 $\operatorname{Prob}(Y=y_j\mid X=x_i)$ 等于

```math
\frac{p_{ij}}{p_{i1}+\cdots+p_{in}}=\frac{p_{ij}}{p_i}.
```

8. 对这个联合概率矩阵，其中 $\operatorname{Prob}(x_1,y_2)=0.3$，求 $\operatorname{Prob}(Y=y_2\mid X=x_1)$ 与 $\operatorname{Prob}(X=x_1)$：

```math
P=\begin{pmatrix}p_{11}&p_{12}\\p_{21}&p_{22}\end{pmatrix}=\begin{pmatrix}0.1&0.3\\0.2&0.4\end{pmatrix},
\qquad \text{元素 } p_{ij} \text{ 相加为 } 1.
```

> 某些 $i,j$ 必然发生。代入计算：
>
> ```math
> \operatorname{Prob}(Y=y_2\mid X=x_1)=\frac{p_{12}}{p_{11}+p_{12}}=\frac{0.3}{0.1+0.3}=\frac{0.3}{0.4}=0.75,
> ```
>
> ```math
> \operatorname{Prob}(X=x_1)=p_{11}+p_{12}=0.1+0.3=0.4.
> ```

9. 解释条件概率的乘积法则：

```math
p_{ij}=\operatorname{Prob}(X=x_i\text{ 且 }Y=y_j)=\operatorname{Prob}(Y=y_j\mid X=x_i)\,\operatorname{Prob}(X=x_i).
```

10. 由习题 8 的乘积法则推导这个关于 $p_{ij}$ 的 Bayes 定理：

```math
\operatorname{Prob}(X=x_i\mid Y=y_j)=\frac{\operatorname{Prob}(Y=y_j\mid X=x_i)\,\operatorname{Prob}(X=x_i)}{\operatorname{Prob}(Y=y_j)}.
```

> 「贝叶斯派」使用先验信息，「频率派」只使用抽样信息。

---

<!-- page 306 -->
> <span style="color:#7f8c8d;">本页为书页 304，进入 V.5 节：多元高斯与加权最小二乘，介绍一元正态分布、标准化变量与二维高斯；页眉与印页码不译。</span>

### V.5 多元高斯与加权最小二乘

Normal probability density（正态概率密度）$p(x)$（the Gaussian，高斯分布）只依赖两个数：均值 $m$ 与方差 $\sigma^2$。

```math
p(x)=\frac{1}{\sqrt{2\pi}\,\sigma}\,e^{-(x-m)^2/2\sigma^2}. \tag{1}
```

$p(x)$ 的图形是一条 centered at（中心在）$x=m$ 的 bell-shaped curve（钟形曲线）。连续变量 $x$ 可在 $-\infty$ 到 $\infty$ 之间任意取值。以接近 $\tfrac23$ 的概率，该随机变量 $x$ 将落在 $m-\sigma$ 与 $m+\sigma$ 之间（距其均值 $m$ 不到一个 standard deviation（标准差）$\sigma$）。

```math
\int_{m-\sigma}^{m+\sigma}p(x)\,dx=\int_{-1}^{1}\frac{1}{\sqrt{2\pi}}\,e^{-x^2/2}\,dx. \tag{2}
```

该积分做了一个从 $x$ 到 $X=(x-m)/\sigma$ 的变量替换。这把指数简化为 $-X^2/2$，把积分限简化为 $-1$ 与 $1$。连 $p(x)$ 中的 $1/\sigma$ 也消失了，因为 $dX$ 等于 $dx/\sigma$。该积分做了一个从 $x$ 到 $X=(x-m)/\sigma$ 的 change of variables（变量替换）。这把指数简化为 $-X^2/2$，把积分限简化为 $-1$ 与 1。连 $p(x)$ 中的 $1/\sigma$ 也消失了，因为 $dX$ 等于 $dx/\sigma$。每个高斯都变成一个均值 $m=0$、方差 $\sigma^2=1$ 的 standard Gaussian（标准高斯）：

```math
\text{标准正态分布 } N(0,1):\quad p(x)=\frac{1}{\sqrt{2\pi}}\,e^{-x^2/2}. \tag{3}
```

把 $p(x)$ 从 $-\infty$ 积分到 $x$ 得到 cumulative distribution（累积分布函数）$F(x)$：随机样本低于 $x$ 的概率。在 $x=0$（均值）处该概率为 $F(0)=\tfrac12$。

### 二维高斯

现在我们有两个 Gaussian（高斯）随机变量 $x$ 与 $y$，它们有均值 $m_1$ 与 $m_2$，方差 $\sigma_1^2$ 与 $\sigma_2^2$。若它们独立，则其 probability density（概率密度）$p(x,y)$ 就是 $p_1(x)$ 乘 $p_2(y)$。变量独立时概率相乘：

```math
p(x,y)=\frac{1}{2\pi\sigma_1\sigma_2}\,e^{-(x-m_1)^2/2\sigma_1^2-(y-m_2)^2/2\sigma_2^2}. \tag{4}
```

$x$ 与 $y$ 的协方差将是 $\sigma_{12}=0$，协方差矩阵 $V$ 将是对角的。方差 $\sigma_1^2$ 与 $\sigma_2^2$ 总在 $V$ 的主对角线上。$p(x,y)$ 中的指数正是 $x$ 指数与 $y$ 指数之和。注意两个指数可以合并为 $-\tfrac12(x-m)^{T}(x-m)$，中间夹着逆协方差矩阵。该指数为 $-\tfrac12[x-m]^{T}V^{-1}[x-m]$：

```math
-\frac12\begin{bmatrix}x-m_1 & y-m_2\end{bmatrix}
\begin{pmatrix}1/\sigma_1^2&0\\0&1/\sigma_2^2\end{pmatrix}
\begin{bmatrix}x-m_1\\ y-m_2\end{bmatrix}
=-\frac{(x-m_1)^2}{2\sigma_1^2}-\frac{(y-m_2)^2}{2\sigma_2^2}. \tag{5}
```

---

## 译者注

> <span style="color:#27ae60;">**注 1 · 为什么协方差矩阵「半正定」而非只是「正定」？** 式 (7)/(9) 把 $V$ 写成 $\sum p_{ij}u_{ij}u_{ij}^{T}$。每个 $u_{ij}u_{ij}^{T}$ 是秩一的外积，对任意向量 $c$ 有 $c^{T}(u_{ij}u_{ij}^{T})c=(c^{T}u_{ij})^2\ge 0$，故每个都是半正定；半正定矩阵的非负加权和仍是半正定，所以 $V$ 至多到「半」正定。它能否升到「正定」取决于这些 $u_{ij}$ 是否张满整个空间：粘连硬币例子里两个 $u_{ij}$ 都落在同一条直线 $x=y$ 上（共线），故 $V$ 奇异、$\det=0$，能量 $c^{T}Vc$ 在某个非零方向（垂直于 $x=y$）上严格为零。这正是「正定 ↔ 各变量不能由其他变量的线性组合完全确定」这一几何解释的雏形——$V$ 的零特征方向就是变量之间存在的精确线性依赖。</span>

> <span style="color:#27ae60;">**注 2 · $V_Z=AV_XA^{T}$ 到底「换」掉了什么？** 这条法则并不新，它只是把两条已知事实合写成一个矩阵等式。第一，期望是线性的：$m_Z=E[Z]=E[AX]=AE[X]=Am_X$，均值按 $A$ 前向传播；第二，方差/协方差本质是「二次型」。把中心化后的 $Z-m_Z=A(X-m_X)$ 代入 $E[(Z-m_Z)(Z-m_Z)^{T}]$，因子 $A$ 从左侧、$A^{T}$ 从右侧各提出一次，中间剩下 $V_X$。所以「拿方差换什么」的答案是：一个变量的二阶矩 $V_X$ 在坐标变换 $A$ 下，按张量规则 $V\mapsto A V A^{T}$ 变换——这正是线性代数中二次型在基变换下的协变规律。式 (17) 的标量情形 $\sigma_z^2=[1\ 1]V_X[1\ 1]^{T}$ 与式 (16) 的 $\sigma_x^2+\sigma_y^2+2\sigma_{xy}$ 逐项对应：两个对角项来自各自方差，交叉项 $2\sigma_{xy}$ 正是矩阵乘开时的两个非对角项之和。差分 GPS 用 $A=[1\ -1]$ 把公共误差「做差抵消」，得到的 $\sigma_1^2-2\sigma_{12}+\sigma_2^2$ 当 $\sigma_{12}$ 接近 $\sigma_1\sigma_2$ 时趋近于 $(\sigma_1-\sigma_2)^2$，误差方差被大幅压低——这是 $V_Z=AV_XA^{T}$ 在工程上最漂亮的实例。</span>

> <span style="color:#27ae60;">**注 3 · 协方差 $\sigma_{xy}$、相关系数 $\rho_{xy}$、内积 $\langle u,v\rangle$ 是同一件事的三个化身。** 协方差的定义 $\sigma_{xy}=E[(x-m_x)(y-m_y)]$ 把「偏离均值的乘积」取期望，与线性代数里两个中心化向量的内积结构完全一致；只要把期望 $E$ 看作随机变量空间上的内积 $\langle u,v\rangle=E[uv]$，$\sigma_{xy}$ 就是 $\langle x-m_x,\,y-m_y\rangle$。于是 Cauchy–Schwarz 不等式直接给出 $(\sigma_{xy})^2\le\sigma_x^2\sigma_y^2$，即 $|\rho_{xy}|\le 1$——这跟本书前面「协方差矩阵半正定 ⇒ 其 $2\times 2$ 主子式 $\det\ge 0$」是同一件事，等号 $\rho=\pm1$ 当且仅当 $y-m_y$ 是 $x-m_x$ 的常数倍（完全线性相关），正是例 4 中 $y=-x$ 的 $\rho=-1$。而 $\rho_{xy}=\dfrac{\sigma_{xy}}{\sigma_x\sigma_y}=\dfrac{\langle x-m_x,y-m_y\rangle}{\|x-m_x\|\,\|y-m_y\|}$ 正是两个「标准化向量」夹角的余弦，所以 $R=DVD$ 中 $D=\operatorname{diag}(1/\sigma_i)$ 的角色等价于把每个向量除以其范数化成单位向量——这与正文把 $v$ 除以 $\|v\|$ 得到单位向量的类比逐字对应。</span>

> <span style="color:#27ae60;">**注 4 · 「独立 ⇒ 协方差为零」为何不可逆？** 正文反复强调独立变量给出 $\sigma_{12}=0$，但反过来「零协方差 ⇒ 独立」并不成立。协方差只捕捉**线性**关系：若 $y=x^2$ 且 $x$ 关于原点对称分布，则 $\sigma_{xy}=E[x(x^2-m_{x^2})]=E[x^3]-m_x m_{x^2}$ 可以为零，但 $y$ 完全由 $x$ 决定，绝非独立。只有对联合高斯（V.5 节）这个特殊情形，$\sigma_{xy}=0$ 才等价于独立，因为高斯的 $p(x,y)$ 完全由 $m$ 与 $V$ 这两个量决定，而 $V$ 对角时式 (4) 的指数自动分离为 $p_1(x)p_2(y)$。这提醒我们：协方差矩阵 $V$ 只是二阶信息，它无法描述三阶及以上（偏度、峰度、非线性依赖）——这正是 V.3 引入 cumulant（累积量）去刻画高阶结构的动机所在。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 协方差矩阵为什么要引入"联合概率"：**</span> 本节（V.4 Covariance Matrices and Joint Probabilities）真正的转折点，不在"方差写在主对角线上"，而在作者反复强调的一句话：要算协方差 $c_{ah}=\mathrm{E}[(age-\text{mean age})(height-\text{mean height})]$，光知道每个年龄的边缘概率、每个身高的边缘概率是**不够的**，必须知道每一对 $(age, height)$ 同时出现的**联合概率** $p_{ah}$。这是因为"年龄与身高相关"这件事，恰恰藏在"哪些 $(a,h)$ 配对更常一起出现"里，而它无法从两个边缘分布还原出来——同一对边缘分布可以对应完全不同的联合结构。作者用"分开抛的两枚硬币"（Example 1）与"粘在一起的两枚硬币"（Example 2）来演示：两例的边缘概率完全相同（每枚硬币出正面的概率都是 $\tfrac12$），但联合概率矩阵 $P$ 一个是 $\begin{smallmatrix}\tfrac14&\tfrac14\\\tfrac14&\tfrac14\end{smallmatrix}$，一个是 $\begin{smallmatrix}\tfrac12&0\\0&\tfrac12\end{smallmatrix}$，协方差 $c_{12}$ 一个为 $0$、一个为 $\tfrac14$。所以协方差矩阵 $V$ 不只是一张方差表，它把"线性代数"与"联合概率"两条线接在了一起：矩阵的每个元素都由 $P_{ij}$ 加权而来，这也正是后文 $V=\sum P_{ij}\,uu^{\mathsf T}$ 这种写法的动机——先把"相关性"翻译成"联合概率"，再用矩阵把这种关系表达并运算。

> <span style="color:#1e8449;">**[note] 公式 $V=\sum_{ij}P_{ij}uu^{\mathsf T}$ 为什么等价于"正半定"：**</span> 本节最有分量的一条公式是 (7)：整个协方差矩阵可以写成 $V=\sum_{i,j} P_{ij}\,u_{ij}u_{ij}^{\mathsf T}$，其中 $u_{ij}=(c_i-m_1,\ y_j-m_2)^{\mathsf T}$，$P_{ij}\ge 0$ 且 $\sum_{ij}P_{ij}=1$。这条式子同时干了两件事：它在**非对角元**上给出了协方差的定义式 (2) $c_{12}=\sum_{ij}P_{ij}(c_i-m_1)(y_j-m_2)$，又在**对角元**上（利用行和公式 (6) $\sum_j P_{ij}=P_i$ 把 $j$ 消掉）回到普通方差 $v_{11}=\sum_i P_i(c_i-m_1)^2$。真正的价值在于它给出的结构信息：每一项 $uu^{\mathsf T}$ 都是一个 **rank-1 的半正定矩阵**（其行列式 $\det(uu^{\mathsf T})=0$，两个对角元 $\ge 0$），而 $V$ 是这些半正定矩阵的**非负加权和**，于是 $V$ 自动半正定。这与下一段用"能量测试"$c^{\mathsf T}Vc\ge 0$ 的证法其实是**同一件事的两面**——后者把 $c^{\mathsf T}Vc=\sum_{ij}P_{ij}(c^{\mathsf T}u_{ij})^2$ 展开成平方和，前者则直接看矩阵结构。作者也承认他更喜欢 $V=\mathrm{E}[uu^{\mathsf T}]$ 这个"直接"版本，因为期望符号 $\mathrm{E}$ 会把联合概率的真实来源隐藏起来；写开成 (7) 后，"半正定"就不再是抽象的代数结论，而是"每个可能结果贡献一个 rank-1 半正定块"这一朴素事实的直接推论。

> <span style="color:#1e8449;">**[note] $V_Z=AV_XA^{\mathsf T}$ 与前文及全书 "能量/二次型" 视角的联系：**</span> 公式 (18) $V_Z=AV_XA^{\mathsf T}$ 是本节乃至全书的高潮——它说线性变换 $Z=AX$ 把协方差矩阵按"双线性"方式搬过去。要理解它为什么成立，看 $z=c+y$ 这个一维情形（$A=[1\ 1]$）：$AV_XA^{\mathsf T}=[1\ 1]\begin{smallmatrix}c_1^2&c_{12}\\c_{12}&c_2^2\end{smallmatrix}\begin{smallmatrix}1\\1\end{smallmatrix}=c_1^2+c_2^2+2c_{12}$，与 (16) 式 $\sigma_z^2=\sigma_1^2+\sigma_2^2+2c_{xy}$ 完全吻合。这条规则在全书里反复出现：它正是"方差是二次型、均值是线性"这一普遍原则的矩阵版——均值按线性搬移 $m_Z=Am_X$，而方差（二阶量）按二次型 $A(\cdot)A^{\mathsf T}$ 搬移。Worked Example 与 GPS Example 都直接用它：GPS 中取差分矩阵 $A=[1\ -1]$，得 $v_Z=c_1^2-2c_{12}+c_2^2$，把公共的传播误差（两接收器相同的电离层改正量）**抵消掉**，从而把定位误差降到厘米级——这正是"差分消除公共误差"这一思想的协方差表述。一个可手算的数值例：设 $X=(c,y)$ 独立、方差均为 1，取 $A=[1\ 1]$，则 $V_Z=1+1+0=2$；若换 $A=[1\ -1]$，则 $V_Z=1+1-0=2$，但 $Z=AX$ 为三分量 $Z=(c,\ y,\ ax+by)$ 时（Worked Example），$\det V_Z=a^2b^2-a^2b^2=0$，说明 $V_Z$ 奇异、rank 只有 2——因为第三个分量被前两个完全决定。这条"降秩"现象正是"独立实验个数"与"矩阵秩"之间联系的入口，为下一节 V.5 用特征分解对角化 $V=Q\Lambda Q^{\mathsf T}$（找出 $M$ 个相互独立的组合）埋下伏笔。

---

> <span style="color:#7f8c8d;">本节把最小二乘从"误差独立同方差"的假设推广到"误差相关且方差不齐"的一般情形：用协方差矩阵 $V$ 定义多元高斯分布，用 $V^{-1}$ 作为权重把异方差噪声"白化"，得到加权最小二乘（weighted least squares）正规方程，并引出估计量的协方差、BLUE 定理与卡尔曼滤波（Kalman filter）的递推更新。</span>

---

<!-- page 307 -->

> <span style="color:#7f8c8d;">本页为书页 305，属 V.5 开篇，讲多元高斯分布如何由协方差矩阵 $V$ 刻画变量间的相关性，并用特征分解把多维积分化为一维积分之和；页眉与印页码不译。</span>

## Non-independent $x$ and $y$（不再独立的 $x$ 与 $y$）

我们准备好放弃独立性了。即使 $V$ 不再是对角矩阵，指数中的项 (5)（连同 $\frac12$ 因子）依然正确。现在这个 Gaussian（高斯分布）同时依赖一个向量 $m$ 和一个矩阵 $V$。

当 $M=2$ 时，第一个变量可能给出关于第二个变量 $y$ 的部分信息（反之亦然）。也许 $y$ 的某一部分由 $x$ 决定，而另一部分是真正独立的。正是这个 $M\times M$ 的协方差矩阵（covariance matrix）$V$ 刻画了 $M$ 个变量 $x=(x_1,\dots,x_M)$ 之间的相互依赖。协方差矩阵的逆 $V^{-1}$ 进入 $p(x)$：

```math
p(x) = \frac{1}{(2\pi)^{M/2}\sqrt{\det V}}\,\exp\!\Big(-\tfrac12 (x-m)^{T} V^{-1} (x-m)\Big)
```

Multivariate Gaussian（多元高斯） probability distribution（概率分布）

向量 $x=(x_1,\dots,x_M)$ 与 $m=(m_1,\dots,m_M)$ 分别包含随机变量及其均值。分子里的 $2\pi$ 的 $M$ 个平方根（即 $(2\pi)^{M/2}$）与 $\det V$ 的平方根，都是为了让总概率等于 1。让我用线性代数来验证。我利用对称矩阵 $V=Q\Lambda Q^{T}$ 的特征值 $\lambda$ 与标准正交特征向量 $q$，于是 $V^{-1}=Q\Lambda^{-1}Q^{T}$：

```math
(x-m)^{T} V^{-1}(x-m) = X^{T}Q\Lambda^{-1}Q^{T}X = Y^{T}\Lambda^{-1}Y
```

注意！组合 $Y=Q^{T}X=Q^{T}(x-m)$ 是统计上独立的，它们的协方差矩阵 $\Lambda$ 是对角阵。

用 $V$ 的特征向量矩阵 $Q$ 把 $V$ 对角化这一步，等同于把随机变量"去相关"（uncorrelating）。对于新变量 $Y_1,\dots,Y_M$，协方差全部为零。这正是线性代数帮助微积分计算多维积分的切入点。

把变量 $x$ 减去 $m$ 平移到 $X$，再旋转到 $Y=Q^{T}X$，$p(x)$ 的积分不会改变。矩阵 $\Lambda$ 是对角的！于是我们要的积分拆成 $M$ 个我们已知的一维积分之积：

```math
\int e^{-Y^{T}\Lambda^{-1}Y/2}\,dY
= \int e^{-Y_1^2/2\lambda_1}\,dY_1\ \cdots\ \int e^{-Y_M^2/2\lambda_M}\,dY_M
= (2\pi\lambda_1)^{1/2}\cdots(2\pi\lambda_M)^{1/2}
```

且 $ (2\pi)^{M/2}\sqrt{\det V} = \prod_{i=1}^{M}(2\pi\lambda_i)^{1/2}$（由 (7) 得）。

$V$ 的行列式（也是 $\Lambda$ 的行列式）等于特征值之积 $\lambda_1\cdots\lambda_M$。于是 (7) 给出了正确的除数，使得 (6) 式中的 $p(x_1,\dots,x_M)$ 的积分 $=1$，如我们所愿。

$p(x)$ 的均值与方差同样是 $M$ 维积分。用 $V$ 的特征向量 $q_1$ 到 $q_M$ 把 $V$ 对角化、并引入 $Y=Q^{T}X$ 的同一思路，可以求出这些积分：

```math
\int x\,p(x)\,dx = (m_1, m_2, \dots, m_M) = m
\qquad
\text{Covariance matrix } V
```

Vector $m$ of means（均值向量） ｜ Covariance matrix $V$（协方差矩阵）

---

<!-- page 308 -->

> <span style="color:#7f8c8d;">本页为书页 306，属 V.5 第二节，引出加权最小二乘：当误差不独立或方差不齐时，正确度量是 $E=(b-Ax)^{T}V^{-1}(b-Ax)$，正规方程为 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$；页眉与印页码不译。</span>

## Probability and Statistics（概率与统计）

**结论**：概率密度 $p(x)$ 的公式 (6) 具备我们想要的全部性质。

## Weighted Least Squares（加权最小二乘）

在第 4 章，最小二乘从一个无解方程组 $Ax=b$ 出发。我们选择最小化误差 $\lVert b-Ax\rVert^2$，这引导我们得到最小二乘方程 $A^{T}A\hat x=A^{T}b$。最优的 $\hat x$ 是 $b$ 在 $A$ 的列空间上的投影。但问题在于：这个平方距离 $E=\lVert b-Ax\rVert^2$ 真的是该最小化的正确误差度量吗？

如果 $b$ 中的测量误差是独立随机变量，均值为 0、方差 $\sigma^2=1$ 且服从正态分布，Gauss（高斯）会说：是的，用最小二乘。

如果误差不独立、或它们的方差彼此不等，Gauss 会说：不，用加权最小二乘。

本节将说明，好的误差度量是 $E=(b-Ax)^{T}V^{-1}(b-Ax)$。最优 $\hat x$ 的方程用到了协方差矩阵 $V$：

```math
A^{T}V^{-1}A\hat x = A^{T}V^{-1}b .
```

Weighted least squares（加权最小二乘） (10)

最重要的例子是 $b$ 中有 $m$ 个独立误差，这些误差的方差为 $\sigma_1^2,\dots,\sigma_m^2$。由独立性，$V$ 是对角矩阵。好的权重 $1/\sigma_1^2,\dots,1/\sigma_m^2$ 来自 $V^{-1}$。我们是在给 $b$ 中的误差加权，使其方差变为 1（且协方差 $=0$）：

```math
\text{Minimize } E = \sum_{i=1}^{m} \frac{(b_i - A_i x)^2}{\sigma_i^2}
\qquad
\text{Independent errors in } b
```

Weighted least squares（加权最小二乘） (11) ｜ Independent errors in $b$（$b$ 中的独立误差）

通过给误差加权，我们在"白化"（whitening）噪声。White noise（白噪声）是对基于标准高斯 $N(0,1)$（均值零、$\sigma^2=1$）的独立误差的简洁描述。

让我写下得到最优 $\hat x$ 的方程 (10) 与 (11) 的步骤：

- 从 $Ax=b$ 出发（$m$ 个方程、$n$ 个未知数，$m>n$，无解）
- 每个右端项 $b_i$ 均值零、方差 $\sigma_i^2$，各 $b_i$ 相互独立
- 把第 $i$ 个方程除以 $\sigma_i$，使每个 $b_i/\sigma_i$ 的方差 $=1$

这一除法把 $Ax=b$ 变成 $V^{-1/2}Ax=V^{-1/2}b$，其中 $V^{-1/2}=\operatorname{diag}(1/\sigma_1,\dots,1/\sigma_m)$。

对这些加权后的方程做普通最小二乘，即 $A\to V^{-1/2}A$、$b\to V^{-1/2}b$，得到

```math
(V^{-1/2}A)^{T}(V^{-1/2}A)\,\hat x = (V^{-1/2}A)^{T} V^{-1/2}b
\quad\Longrightarrow\quad
A^{T}V^{-1}A\hat x = A^{T}V^{-1}b .
```

(12)

由于 $V^{-1}$ 中的 $1/\sigma_i^2$，更可靠的方程（$\sigma_i$ 更小）得到更重的权重。这是加权最小二乘的核心要点。

那些对角权重（方程之间不耦合）是最常见、也最简单的。它们适用于 $b_i$ 中的独立误差。当这些测量误差不独立时，$V$ 不再对角——但 (12) 仍然是正确的加权方程。实际中，找出全部协方差可能是繁重的工作，而对角的 $V$ 要简单得多。

---

<!-- page 309 -->

> <span style="color:#7f8c8d;">本页为书页 307，属 V.5 第三节，讲估计量的方差-协方差矩阵 $W=(A^{T}V^{-1}A)^{-1}$ 及其最优性（BLUE），并给出心率测量三次数值例；页眉与印页码不译。</span>

## The Variance in the Estimated $\hat x$（估计量 $\hat x$ 的方差）

还有一点：通常重要的问题并不是针对某个特定 $b$ 的最优 $\hat x$——那只是一个样本！真正的目标是了解整个实验的可靠性。这（一如可靠性总是如此）由估计量 $\hat x$ 的方差来度量。

首先，$b$ 的零均值给出 $\hat x$ 的零均值。然后，把输入 $b$ 的方差 $V$ 与输出 $\hat x$ 的方差 $W$ 联系起来的公式，结果十分优美：

```math
\text{Variance-covariance matrix for } \hat x = (A^{T}V^{-1}A)^{-1} .
```

(13)

这一最小可能的方差来自最优的加权，也就是 $V^{-1}$。这个关键公式正是 V.4 节的完美应用。若 $b$ 的协方差矩阵为 $V$，则 $\hat x=Lb$ 的协方差矩阵为 $LVL^{T}$。矩阵 $L$ 是

```math
L = (A^{T}V^{-1}A)^{-1}A^{T}V^{-1},
```

因为 $\hat x=Lb$ 解加权方程 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$。把它代入 $LVL^{T}$，就能看到 (13) 出现：

```math
LVL^{T}
= (A^{T}V^{-1}A)^{-1}A^{T}V^{-1}\; V\; V^{-1}A\,(A^{T}V^{-1}A)^{-1}
= (A^{T}V^{-1}A)^{-1}.
```

这就是输出 $\hat x$ 的协方差 $W$。是时候看一个例子了。

**例 1** 假设一位医生三次测量你的心率 $x$（$m=3,n=1$）：即 $Ax=b$，其中

```math
A = \begin{bmatrix}1\\1\\1\end{bmatrix},
\qquad
V = \begin{bmatrix}\sigma_1^2 & 0 & 0\\ 0 & \sigma_2^2 & 0\\ 0 & 0 & \sigma_3^2\end{bmatrix}.
```

方差可能是 $\sigma_1^2=1/9$、$\sigma_2^2=1/4$、$\sigma_3^2=1$。权重于是依次是 3、2、1。随着测量进行你越来越紧张：$b_3$ 不如 $b_2$ 和 $b_1$ 可靠。三次测量都含有一些信息，所以它们都进入最优（加权）估计：

```math
V^{-1/2}A\hat x = V^{-1/2}b \quad\Longleftrightarrow\quad
\begin{cases} 3\hat x = 3b_1\\ 2\hat x = 2b_2\\ 1\hat x = 1b_3 \end{cases}
```

进而 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$：

```math
\begin{bmatrix}1&1&1\end{bmatrix}
\begin{bmatrix}9&0&0\\0&4&0\\0&0&1\end{bmatrix}
\begin{bmatrix}1\\1\\1\end{bmatrix}\hat x
=
\begin{bmatrix}1&1&1\end{bmatrix}
\begin{bmatrix}9&0&0\\0&4&0\\0&0&1\end{bmatrix}
\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}
```

```math
14\,\hat x = 9b_1 + 4b_2 + b_3
\quad\Longrightarrow\quad
\hat x = \frac{9b_1 + 4b_2 + b_3}{14}
```

即 $b_1,b_2,b_3$ 的最优加权平均。

---

<!-- page 310 -->

> <span style="color:#7f8c8d;">本页为书页 308，属 V.5 第四节，收束加权最小二乘（BLUE 定理与 $\ell_1$ 范数的动机），并转入卡尔曼滤波：动态最小二乘与新数据到来时的递推更新思想；页眉与印页码不译。</span>

权重最大落在 $b_1$ 上，因为它的方差最小。$\hat x$ 的方差有优美的公式：

```math
W = (A^{T}V^{-1}A)^{-1} = \frac{1}{14}.
```

这个方差 $W=\frac{1}{14}$，因为纳入了 $b_2$ 与 $b_3$，从单独用 $b_1$ 时的 $\frac{1}{9}$ 下降了：

```math
\frac{1}{14} < \frac{1}{9}.
```

Gauss 的 BLUE 定理（证明见网站）断言：我们的 $\hat x=Lb$ 是 $Ax=b$ 之解的最佳线性无偏估计（Best Linear Unbiased Estimate）。对任何其他无偏选择 $\hat x^{*}=L^{*}b$，其方差 $W^{*}=L^{*}V L^{*T}$ 将大于我们的 $W=LVL^{T}$。

注意："更大"意味着 $W^{*}-W$ 将是正半定矩阵（positive semidefinite）。"无偏"意味着 $L^{*}A=I$，这样精确的 $Ax=b$ 会产生正确答案 $\hat x=L^{*}b=x$。

我必须补充：也有理由从一开始就不最小化平方误差。理由之一：$\hat x$ 往往有很多小分量，小数的平方非常小，而它们会在最小化时出现。更容易理解的是稀疏向量（sparse vectors）——只有少数非零元。统计学家常常更愿意最小化非平方误差：$\sum |b_i-(Ax)_i|$ 之和。这一误差度量是 $\ell_1$ 范数而非 $\ell_2$ 范数。由于绝对值的缘故，用 $\ell_1$ 范数求 $\hat x$ 的方程变成非线性的。

新出现的快速算法正在计算稀疏的 $\hat x$，未来属于 $\ell_1$。IV.4 节的压缩感知（compressive sensing）正是 $\ell_1$ 回归的一个令人印象深刻的应用。

## The Kalman Filter（卡尔曼滤波）

"Kalman filter"（卡尔曼滤波）是动态最小二乘中的伟大算法。"动态"一词意味着新的测量值 $b_k$ 不断到来，于是最优估计不断改变（基于全部的 $b_0,\dots,b_k$）。不仅如此，矩阵 $A$ 也在改变。于是 $\hat x_k$ 将是我们对"全部历史观测方程与更新方程（状态方程）的最新解"的最佳最小二乘估计。截至时间 2，共有 3 个观测方程和 2 个状态方程：

```math
A_0x_0 = b_0,\qquad
A_1x_1 = b_1,\qquad
A_2x_2 = b_2
```

```math
x_1 = F_0x_0,\qquad
x_2 = F_1x_1
```

(14)

卡尔曼的思想是一次引入一个方程。每个方程都会有误差。每来一个新方程，我们就更新当前 $x_k$ 的最优估计。但历史不会被遗忘！这个新估计用到了所有过去的观测 $b_0$ 到 $b_{k-1}$，以及所有状态方程 $x_{new}=F_{old}\,x_{old}$。这是一个不断增大的最小二乘问题。

关于 (14) 还有更重要的一点。每个最小二乘方程都用 $b_k$ 中误差的协方差矩阵 $V_k$ 加权。更新方程 $x_{k+1}=F_kx_k$ 中的误差甚至还有一个协方差矩阵 $C_k$。于是最优 $\hat x_k$ 依赖 $b_0,b_1$ 与 $F_1$，以及 $V_0,V_1$ 与 $C_1$。把它写成对前一个 $\hat x_{k-1}$ 的更新，才是好的写法。

---

<!-- page 311 -->

> <span style="color:#7f8c8d;">本页为书页 309，属 V.5 第五节，给出卡尔曼滤波的核心——用增益矩阵 $K_1$ 与协方差更新 $W_1^{-1}=W_0^{-1}+A_1^{T}V_1^{-1}A_1$ 把旧估计递推到新估计；页眉与印页码不译。</span>

让我集中处理一个简化问题：不含矩阵 $F_k$ 与协方差 $C_k$。我们在每一步估计同一个真实的 $x$。如何从 $\hat x_0$ 得到 $\hat x_1$？

$b_0$ 引出加权方程 $A_0^{T}V_0^{-1}A_0\hat x_0=A_0^{T}V_0^{-1}b_0$：

```math
\text{OLD } A_0\hat x = b_0
```

(15)

下面的旧问题引出如下的新加权方程：

```math
\text{NEW } \begin{bmatrix}A_0\\A_1\end{bmatrix}\hat x = \begin{bmatrix}b_0\\b_1\end{bmatrix}
\quad\text{with}\quad
V = \begin{bmatrix}V_0 & 0\\0 & V_1\end{bmatrix}
```

(16)

是的，我们可以直接解这个新问题、忘掉旧问题。但旧解 $\hat x_0$ 花了功夫，我们希望能在 $\hat x_1$ 中复用。我们寻找的是对 $\hat x_0$ 的一个更新：

```math
\hat x_1 = \hat x_0 + K_1(b_1 - A_1\hat x_0).
```

Kalman update gives $\hat x_1$ from $\hat x_0$（卡尔曼更新：由 $\hat x_0$ 得 $\hat x_1$） (17)

更新修正量是旧状态与新测量 $b_1$ 之间的失配 $b_1-A_1\hat x_0$，再乘以卡尔曼增益矩阵（Kalman gain matrix）$K_1$。$K_1$ 的公式来自比较 (15) 与 (16) 两式的解 $\hat x_0$ 与 $\hat x_1$。而且当我们基于新数据 $b_1$ 把 $\hat x_0$ 更新到 $\hat x_1$ 时，也要把协方差矩阵 $W_0$ 更新到 $W_1$。

记得 $W_0=(A_0^{T}V_0^{-1}A_0)^{-1}$，来自方程 (13)。把它的逆从 $W_0^{-1}$ 更新到 $W_1^{-1}$：

```math
W_1^{-1} = W_0^{-1} + A_1^{T}V_1^{-1}A_1
```

Covariance $W_1$ of errors in $\hat x_1$（$\hat x_1$ 误差的协方差） (18)

```math
K_1 = W_1 A_1^{T}V_1^{-1}
```

Kalman gain matrix $K_1$（卡尔曼增益矩阵） (19)

这就是卡尔曼滤波的核心。注意协方差矩阵 $W_k$ 的重要性：这些矩阵度量整个过程的可靠性，其中向量 $\hat x_k$ 基于特定的测量 $b_0$ 到 $b_k$ 估计当前状态。

当状态 $x_k$ 也在变化（基于矩阵 $F_k$）时，解释动态卡尔曼滤波需要整章整本书。它先有一步用 $F$ 对 $x_k$ 的预测（prediction），再有一步用新数据 $b$ 的修正（correction）。也许最好到此为止！

本页讲的是递推最小二乘（recursive least squares）：加入新数据 $b_k$，基于全部数据更新最优的当前估计，并更新它的协方差矩阵 $W_k$。

这个更新思想始于 III.1 节的 Sherman–Morrison–Woodbury 公式（关于 $(A-UV^{T})^{-1}$）。数值上，这是卡尔曼成功的钥匙——把大小为 $n$ 的逆矩阵换成大小为 $k$ 的逆矩阵。

---

<!-- page 312 -->

> <span style="color:#7f8c8d;">本页为书页 310，属 V.5 习题集（Problem Set V.5），共 6 题，练习加权估计、独立性下的积分分解、卡尔曼更新与动态最小二乘；页眉与印页码不译。</span>

## Problem Set V.5（习题集 V.5）

**1.** 对同一变量 $x$ 的两次测量给出两个方程 $x=b_1$ 和 $x=b_2$。设均值皆为零，方差为 $\sigma_1^2$ 与 $\sigma_2^2$，误差独立：$V$ 为对角阵，对角元为 $\sigma_1^2,\sigma_2^2$。把这两个方程写成 $Ax=b$（$A$ 是 $2\times1$）。如正文例 1，求基于 $b_1,b_2$ 的最优估计：

```math
\hat x = \frac{b_1/\sigma_1^2 + b_2/\sigma_2^2}{1/\sigma_1^2 + 1/\sigma_2^2}.
```

**2.** (a) 在第 1 题中，设第二次测量 $b_2$ 变得极其精确，其方差 $\sigma_2^2\to 0$。当 $\sigma_2^2$ 趋于零时，最优估计 $\hat x$ 是多少？

(b) 相反的情形是 $\sigma_2^2\to\infty$，$b_2$ 不含任何信息。此时基于 $b_1,b_2$ 的最优估计又是多少？

**3.** 若 $x$ 与 $y$ 独立，概率分别为 $p_1(x)$ 与 $p_2(y)$，则 $p(x,y)=p_1(x)\,p_2(y)$。通过把二重积分拆成一元积分之积（从 $-\infty$ 到 $\infty$），证明

```math
\iint p(x,y)\,dx\,dy = 1
\qquad\text{且}\qquad
\iint (x+y)\,p(x,y)\,dx\,dy = m_1 + m_2 .
```

**4.** 续第 3 题对独立 $x,y$，证明 $p(x,y)=p_1(x)p_2(y)$ 满足

```math
\iint (x-m_1)^2 p(x,y)\,dx\,dy = \sigma_1^2,
\qquad
\iint (x-m_1)(y-m_2)\,p(x,y)\,dx\,dy = 0 .
```

于是 $2\times2$ 协方差矩阵 $V$ 是对角的，其对角元为 $\sigma_1^2,\sigma_2^2$。

**5.** 设 $\hat x_k$ 是 $b_1,\dots,b_k$ 的平均。一个新的测量 $b_{k+1}$ 到来。卡尔曼更新方程 (17) 给出新平均：

```math
\hat x_{k+1} = \hat x_k + \frac{1}{k+1}(b_{k+1}-\hat x_k).
```

验证 $\hat x_{k+1}$ 确实是 $b_1,\dots,b_{k+1}$ 的正确平均。

再验证平均值的方差更新方程 (18)：在假设 $W_k=\sigma^2/k$ 且 $b_{k+1}$ 的方差 $V=\sigma^2$ 下，得到

```math
W_{k+1} = \frac{\sigma^2}{k+1}.
```

**6.** （稳态模型）第 5 题是静态最小二乘，所有样本平均都是对同一个 $x$ 的估计。要让卡尔曼滤波动态化，还需加入一个带自身误差方差 $s^2$ 的状态方程 $x_{k+1}=Fx_k$。动态最小二乘问题允许 $x$ 随 $k$ 增大而"漂移"：

```math
\begin{cases}
b_0 = x_0 \\
b_1 = x_1 \\
b_2 = x_2
\end{cases}
\qquad
\begin{cases}
x_1 = F x_0 \\
x_2 = F x_1
\end{cases}
```

各方程带方差 $s^2,\sigma_1^2,\sigma_2^2$。取 $F=1$，把这三个方程两边除以相应的 $s,\sigma_1,\sigma_2$，用最小二乘求 $x_0$ 与 $x_1$，这会给更近期的 $b_1$ 更大权重。卡尔曼滤波在《Algorithms for Global Positioning》（Borre 与 Strang）中展开。

---

## 译者注

<span style="color:#27ae60;">**注 1：为什么"除以 $\sigma_i$"能把方程"白化"？** 加权最小二乘的全部技巧，在于用协方差矩阵的逆 $V^{-1}$ 去"消掉"误差的异质性。设第 $i$ 个方程 $b_i$ 的方差是 $\sigma_i^2$。若把它除以 $\sigma_i$，新右端 $b_i/\sigma_i$ 的方差就是 $\operatorname{Var}(b_i/\sigma_i)=\sigma_i^2/\sigma_i^2=1$。于是所有加权后的方程都变成方差为 1、彼此（因独立）协方差为 0 的"标准噪声"，即正文说的 white noise。这一步等价于作线性变换 $b\mapsto V^{-1/2}b$，其中 $V^{-1/2}=\operatorname{diag}(1/\sigma_1,\dots,1/\sigma_m)$；对 $A$ 也做同样变换 $A\mapsto V^{-1/2}A$，再套用普通最小二乘 $A^{T}A\hat x=A^{T}b$，把 $V^{-1/2}$ 代进去、合并，正好得到 (12) 的 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$。所以"白化→普通最小二乘"与"直接写加权正规方程"是同一件事的两种说法——这正是 V.4 节协方差在线性变换下按 $LVL^{T}$ 传播的直接推论。</span>

<span style="color:#27ae60;">**注 2：估计量方差 $W=(A^{T}V^{-1}A)^{-1}$ 为什么是"最小的"？** 一旦取定 $\hat x=Lb$（线性）且要求无偏 $LA=I$，那么 $\hat x$ 的协方差就是 $W=LVL^{T}$。关键恒等式 $LVL^{T}=(A^{T}V^{-1}A)^{-1}$ 只有在 $L=(A^{T}V^{-1}A)^{-1}A^{T}V^{-1}$（即加权正规方程的解）时才成立。任何别的无偏线性估计 $\hat x^{*}=L^{*}b$（$L^{*}A=I$）都有 $L^{*}V L^{*T}-W\succeq 0$（正半定），也就是说：无论沿哪个方向看，$W$ 都给出不更大的方差——这就是 Gauss–Markov/BLUE 定理。直观上，$V^{-1}$ 把可靠（方差小）的方程权重放大、不可靠的权重压低，从而"榨取"出最小方差。注意 (13) 里的 $W$ 与 $b$ 无关，只由 $A$ 和 $V$ 决定：它描述的是整个实验的可靠性，而非某一次样本的好坏，这正是本节"关心的不是某个 $b$ 的最优 $\hat x$，而是可靠性"那句话的落点。</span>

<span style="color:#27ae60;">**注 3：卡尔曼更新 (17)–(19) 与 III.1 节的关系。** 递推最小二乘想避免每来一个新数据就重解一个大方程组，而希望"在旧解上做一次小修正"。以两个数据块为例，新问题的正规方程是 $(A_0^{T}V_0^{-1}A_0+A_1^{T}V_1^{-1}A_1)\hat x_1=A_0^{T}V_0^{-1}b_0+A_1^{T}V_1^{-1}b_1$。记 $W_0^{-1}=A_0^{T}V_0^{-1}A_0$，则新协方差的逆是 $W_1^{-1}=W_0^{-1}+A_1^{T}V_1^{-1}A_1$（这就是 (18)）。要由 $\hat x_0$ 得到 $\hat x_1$，需要用 $W_1=(W_0^{-1}+A_1^{T}V_1^{-1}A_1)^{-1}$ 去求逆。而 III.1 节的 Sherman–Morrison–Woodbury 公式正是给出"秩一（或低秩）修正下的逆更新"：它把对一个 $n\times n$ 矩阵求逆，换成对一个小得多的修正子块求逆。这里 $A_1^{T}V_1^{-1}A_1$ 的秩不超过新数据数 $k$，于是每步只需对 $k\times k$ 的矩阵求逆，而非重解 $n\times n$ 系统——这是卡尔曼滤波在数值上高效、能在线实时运行的根本原因。正文末句"把大小为 $n$ 的逆矩阵换成大小为 $k$ 的逆矩阵"说的正是这个交换。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么要用协方差矩阵的逆 $V^{-1}$ 来刻画「依赖」：**</span> 一元高斯 $p(x)\propto e^{-(x-m)^2/(2\sigma^2)}$ 里，方差 $\sigma^2$ 出现在分母，控制着钟形曲线「有多宽」；推广到多个变量时，自然的猜测是把指数里的平方写成二次型 $(\mathbf{x}-\mathbf{m})^{\mathsf T}W(\mathbf{x}-\mathbf{m})$，而问题就变成了：那个对称正定矩阵 $W$ 该是什么？如果只是想让各分量独立（diagonal 情形），$W$ 应取对角元 $1/\sigma_i^2$；一旦变量之间相关，就必须让 $W$ 承担「同时度量每个方向的离散程度与彼此之间的耦合」的任务。答案是 $W=V^{-1}$，其中 $V$ 是协方差矩阵（covariance matrix），其元 $V_{ij}=\mathbb{E}[(x_i-m_i)(x_j-m_j)]$ 直接度量 $x_i$ 与 $x_j$ 的同涨同落。取逆的原因在归一化里看得最清楚：常数因子里出现的是 $\det V$（的平方根），而只有 $W=V^{-1}$ 才能让 $\int e^{-(\mathbf{x}-\mathbf{m})^{\mathsf T}V^{-1}(\mathbf{x}-\mathbf{m})/2}\,d\mathbf{x}$ 这个 $M$ 维积分恰好等于 $\sqrt{(2\pi)^M\det V}$，使总概率归一为 $1$。也就是说，$V$ 描述「协方差」，$V^{-1}$（常被称为精度矩阵，precision matrix）才进入概率密度的指数——这正是为什么后文加权最小二乘里权重取的也是 $V^{-1}$ 而非 $V$：可靠的信息（方差小的分量）在 $V^{-1}$ 中权重反而大。

> <span style="color:#1e8449;">**[note] 对角化 $V=Q\Lambda Q^{\mathsf T}$ 为什么能把 $M$ 维积分「拆成 $M$ 个一维积分」：**</span> 这是全书「线性代数帮微积分算积分」这一主题在概率上的又一次现身。指数里的二次型 $(\mathbf{x}-\mathbf{m})^{\mathsf T}V^{-1}(\mathbf{x}-\mathbf{m})$ 一般不是平方和的形式，因为 $V^{-1}$ 非对角；但 $V$ 是对称正定矩阵，可写成 $V=Q\Lambda Q^{\mathsf T}$，其中 $Q$ 的列是标准正交特征向量，$\Lambda=\operatorname{diag}(\lambda_1,\dots,\lambda_M)$。于是 $V^{-1}=Q\Lambda^{-1}Q^{\mathsf T}$，代入并令 $\mathbf{Y}=Q^{\mathsf T}\mathbf{X}=Q^{\mathsf T}(\mathbf{x}-\mathbf{m})$，二次型就变成 $\mathbf{Y}^{\mathsf T}\Lambda^{-1}\mathbf{Y}=\sum_i y_i^2/\lambda_i$——交叉项全部消失。这一步的统计含义是：新变量 $Y_1,\dots,Y_M$ 的协方差矩阵恰是 $\Lambda$，对角线外全为零，即它们是**相互独立**的，作者说的「去相关（uncorrelating）」正是这个意思。由于 $\mathbf{Y}=Q^{\mathsf T}\mathbf{X}$ 是正交变换，其 Jacobi 行列式的绝对值为 $1$，体积元不变，于是 $M$ 重积分 $\int e^{-\sum_i y_i^2/(2\lambda_i)}\,d\mathbf{y}$ 按 Fubini 定理拆成 $\prod_i \int e^{-y_i^2/(2\lambda_i)}\,dy_i$ 这 $M$ 个已知的一维高斯积分，各自等于 $\sqrt{2\pi\lambda_i}$，乘起来就是 $\sqrt{(2\pi)^M\det\Lambda}=\sqrt{(2\pi)^M\det V}$，与式 (7) 吻合。式 (7) 的归一化常数之所以是 $\det V$，根子就在这里：$\det V=\det\Lambda=\lambda_1\cdots\lambda_M$ 恰是各独立方向方差的乘积。

> <span style="color:#1e8449;">**[note] 加权最小二乘与 §IV、§III.1 及卡尔曼滤波的呼应：**</span> 本节式 (10) 的加权正规方程 $A^{\mathsf T}V^{-1}A\hat{x}=A^{\mathsf T}V^{-1}b$，就是 §IV 中普通最小二乘 $A^{\mathsf T}A\hat{x}=A^{\mathsf T}b$ 在「噪声不独立、方差不等」时的推广：先把 $A\mathbf{x}=b$ 左乘 $V^{-1/2}=\operatorname{diag}(1/\sigma_1,\dots,1/\sigma_m)$ 得到 $V^{-1/2}A\mathbf{x}=V^{-1/2}b$，让每个方程 $b_i/\sigma_i$ 都具有方差 $1$——这就是作者说的「白化（whitening）」噪声，使标准高斯 $N(0,1)$ 的假设重新成立，再套普通最小二乘即得式 (12)。举 §例 1 的数值：医生三次测心率，方差为 $1/9,1/4,1$，对应权重 $3,2,1$，最佳加权平均 $\hat{x}=(9b_1+4b_2+b_3)/14$，方差 $W=(1/9+1/4+1)^{-1}=1/14$——比只信 $b_1$ 时的 $1/9$ 更小，说明「多一次测量即使不可靠也仍降低总方差」。而末节卡尔曼滤波式 (17)–(19) 的更新 $\hat{x}_1=\hat{x}_0+K_1(b_1-A_1\hat{x}_0)$，其增益 $K_1$ 与协方差更新 $W_1^{-1}=W_0^{-1}+A_1^{\mathsf T}V_1^{-1}A_1$ 正是式 (13) $W=(A^{\mathsf T}V^{-1}A)^{-1}$ 的递归版本：每来一个新观测，就把它的精度 $A_1^{\mathsf T}V_1^{-1}A_1$ 累加到旧的逆协方差上，而不用重解整个增长中的最小二乘问题。作者点明这背后的数值关键是 §III.1 的 Sherman–Morrison–Woodbury 公式——用低维求逆替换高维求逆，这与 §IV.4 压缩感知（compressive sensing）改用 $\ell_1$ 范数求稀疏解一样，都是本书「同一条思想在不同章节反复现身」的例子。

---

> <span style="color:#7f8c8d;">本节以租车为例引入 Markov matrix（马尔可夫矩阵），讲清正矩阵的 Perron-Frobenius Theorem（佩龙–弗罗贝尼乌斯定理）如何保证概率向量收敛到稳态；随后把离散的 Markov chain 推广到连续的 master equation（主方程）$dp/dt = Ap$，用矩阵指数 $e^{At}$ 统一两类过程。文末给出习题集 V.6 与第六部分的目录。</span>

---

<!-- page 313 -->
> <span style="color:#7f8c8d;">本页为书页 311，属 V.6 的引子——用 100 辆车在芝加哥与丹佛之间流动的例子，展示 Markov matrix 的特征值与幂 $P^n$ 如何解释稳态分布；页眉与印页码不译。</span>

## V.6 马尔可夫链

马尔可夫链的关键事实，用一个租车（rental cars）的例子就能讲清楚。假设开始时 100 辆车都在芝加哥，每个月这些车会在芝加哥与丹佛之间移动：

- 芝加哥的车有 80% 留在芝加哥；丹佛的车有 30% 移向芝加哥
- 芝加哥的车有 20% 移向丹佛；丹佛的车有 70% 留在丹佛

用矩阵语言写，车从第 $n$ 个月到第 $n+1$ 个月的移动就是 $y_{n+1} = Py_n$：

```math
y_{n+1} = \begin{pmatrix} \text{芝加哥的车}\\ \text{丹佛的车} \end{pmatrix}_{n+1}
= \underbrace{\begin{pmatrix} 0.8 & 0.3\\ 0.2 & 0.7 \end{pmatrix}}_{P}
  \begin{pmatrix} \text{芝加哥的车}\\ \text{丹佛的车} \end{pmatrix}_{n}
\tag{1}
```

每个月我们都乘以这个「Markov matrix（马尔可夫矩阵）」$P$。它的两列之和都是 1。经过 $n$ 个月，车的分布就是 $y_n = P^n y_0$。本例中 $y_0 = (100, 0)$，因为所有车都从芝加哥出发：

```math
\begin{pmatrix}100\\0\end{pmatrix},\ 
\begin{pmatrix}80\\20\end{pmatrix},\ 
\begin{pmatrix}70\\30\end{pmatrix},\ 
\begin{pmatrix}65\\35\end{pmatrix}
```

假设改为所有 100 辆车都从丹佛出发：

```math
\begin{pmatrix}0\\100\end{pmatrix},\ 
\begin{pmatrix}30\\70\end{pmatrix},\ 
\begin{pmatrix}45\\55\end{pmatrix},\ 
\begin{pmatrix}52.5\\47.5\end{pmatrix}
```

两条路径都收敛到同一个 $60$–$40$ 的极限分布。车从哪里出发无关紧要。因为我们研究的是矩阵 $P$ 的幂 $P^n$，这本质上是一个关于 $P$ 的 eigenvalues（特征值）与 eigenvectors（特征向量）的问题：

```math
\det\begin{pmatrix}0.8-\lambda & 0.3\\ 0.2 & 0.7-\lambda\end{pmatrix}
= \lambda^2 - 1.5\lambda + 0.5 = (\lambda - 1)(\lambda - 0.5)
```

特征值 $\lambda_1 = 1$、$\lambda_2 = 0.5$，对应特征向量为：

```math
v_1 = \begin{pmatrix}0.6\\0.4\end{pmatrix},\qquad
v_2 = \begin{pmatrix}1\\-1\end{pmatrix}
```

它们解释了一切。那个 $60$–$40$ 的极限分布就是 steady state（稳态）$(60,40)$。因为 $\lambda_1 = 1$，所以 $y_n \to (60,40)$ 给出 $y_{n+1} = (60,40)$；每个月到稳态的距离都乘以 $\tfrac12$（即 $\lambda_2 = 0.5$）。

你可以在上面的数字里看到这一点：芝加哥的 $100, 80, 70, 65$，每个月都把到稳态 60 的距离减半；同样地，丹佛的 $0, 20, 30, 35$，把到稳态 40 的距离减半。用矩阵记号，$P$ 通过其特征向量与特征值对角化为 $X\Lambda X^{-1}$：

```math
P^n = (X\Lambda X^{-1})\cdots(X\Lambda X^{-1}) = X\Lambda^n X^{-1}
```

```math
P^n = \begin{pmatrix}1 & 1\\ 1 & -1\end{pmatrix}
\begin{pmatrix}1 & 0\\ 0 & (0.5)^n\end{pmatrix}
\begin{pmatrix}0.6 & 0.4\\ 0.4 & -0.4\end{pmatrix}
```

<!-- page 314 -->
> <span style="color:#7f8c8d;">本页为书页 312，正式定义 transition probabilities（转移概率）与 transition matrix（转移矩阵），并陈述三类状态空间——有限、无限可数、连续；页眉与印页码不译。</span>

当 $n=1$ 时我们得到 $P$ 本身；当 $n \to \infty$ 时，极限矩阵 $P^{\infty}$ 的两列都是 $(0.6,\ 0.4)$。100 辆车无论从「芝加哥列」还是「丹佛列」出发，随着 $n\to\infty$ 都总是 $60$–$40$ 的分配。这正是正 Markov matrix（positive Markov matrix，即 $P>0$）的突出特征。

一个正 Markov matrix 需要满足：

- 所有元素 $p_{ij} > 0$，且 $P$ 的每一列之和为 1（因此没有车「丢失」）。这时有 $\mathbf{1}^{T}P = \mathbf{1}^{T}$。

矩阵 $P$ 有最大的特征值 $\lambda_1 = 1$，且对应的特征向量 $v_1 > 0$（正特征向量）。正是针对正矩阵的 Perron-Frobenius Theorem（佩龙–弗罗贝尼乌斯定理）保证了 $\lambda_1 > 0$ 且 $v_1 > 0$。而「各列之和为 1」这一事实又告诉我们 $P^{T}\mathbf{1} = \mathbf{1}$、$\lambda_1 = 1$。于是便产生了稳态 $y_{\infty}$，它是 $v_1$ 的某个倍数。记住，$\mathbf{1}^{T}$ 这一行就是左特征向量（left eigenvector）。

**收敛性（Convergence）**

```math
P^n = X\Lambda^n X^{-1}
```

随着 $n\to\infty$，对角矩阵 $\Lambda^n$ 中只有那个 1 能存活下来。于是「列乘行」的形式变成 $X$ 的某一列乘以 $[\,1\ \ 1\,]$。极限矩阵 $P^{\infty}$ 的每一列都相同！稳态 $y_{\infty} = P^{\infty} y_0$ 必定是那个列向量 $v_1$ 的某个倍数。

在我们的例子中这个倍数是 $(60,40)$，因为我们开始时是 100 辆车。马尔可夫链既不销毁旧车也不增添新车——它最终把车按照 $P$ 的主特征向量（leading eigenvector）来分配。

现在我们把 $P$ 看成概率矩阵，然后引出 Perron-Frobenius。

**转移概率（Transition Probabilities）**

马尔可夫链是概率论中线性代数的绝佳范例。最基本的一批数是概率 $p_{ij}$，表示在时刻 $n$ 处于状态 $j$、在时刻 $n+1$ 转移到状态 $i$ 的概率：

```math
\text{转移概率}\quad p_{ij} = \operatorname{Prob}\{\, c(n+1) = i \mid c(n) = j \,\}
\tag{2}
```

这句简单陈述里藏着两个关键点。第一，概率 $p_{ij}$ 不依赖 $n$——规则在任何时刻都相同。第二，新状态 $c(n+1)$ 的概率 $y_{n+1}$ 只依赖当前状态，而与更早的历史无关。

还有一个问题待回答：马尔可夫链可能的「状态」是什么？在本例中状态是芝加哥和丹佛（抱歉，是城市）。这里给出三种选择：

- **有限马尔可夫链（Finite Markov Chain）**：每个状态 $c(n)$ 是 $1,2,\dots,N$ 中的一个数。
- **无限可数状态马尔可夫链（Infinite State Markov Chain）**：每个状态 $c(n)$ 是一个整数 $n = 0,1,2,\dots$
- **连续状态马尔可夫链（Continuous Markov Chain）**：每个状态 $c(n)$ 是一个实数。

<!-- page 315 -->
> <span style="color:#7f8c8d;">本页为书页 313，把转移矩阵的列和条件写成 $\mathbf{1}^{T}P=\mathbf{1}^{T}$ 与 $P^{T}\mathbf{1}=\mathbf{1}$，并给出例题 1 的特征向量与特征值；页眉与印页码不译。</span>

我们大多选取 $N$ 个状态的有限链。初始状态 $c(0)$ 可以是给定的，也可能我们只知道那个初始状态的概率向量 $y_0$。与微分方程不同，$c(0)$ 并不能决定 $c(1)$。若 $c(0)=j$，那只能决定新状态 $c(1)$ 的 $N$ 个概率，即 $y_1$。这个新状态是 $1$ 到 $N$ 中的一个数。这些新状态的概率就是 $p_{1j}, p_{2j}, \dots, p_{Nj}$，它们的和必须为 1：

```math
P\text{ 的第 }j\text{ 列：}\quad p_{1j} + p_{2j} + \cdots + p_{Nj} = 1
\tag{3}
```

这些数自然组成一个 $N\times N$ 的概率矩阵 $P$，元素为 $p_{ij}$。它们被称为 transition probabilities（转移概率），$P$ 就是 transition matrix（转移矩阵）。它告诉我们关于「从状态 $c(n)=j$ 转移到状态 $c(n+1)=i$」这件事所能知道的一切（只有概率，没有确定事实！）。同一个矩阵 $P$ 也适用于每个未来时刻从 $c(n)$ 到 $c(n+1)$ 的转移。

```math
\underbrace{\begin{pmatrix} \operatorname{Prob}\{c(n+1)=1\}\\ \vdots\\ \operatorname{Prob}\{c(n+1)=N\} \end{pmatrix}}_{y_{n+1}}
= \underbrace{\begin{pmatrix} p_{11} & \cdots & p_{1N}\\ \vdots & & \vdots\\ p_{N1} & \cdots & p_{NN} \end{pmatrix}}_{P}
\underbrace{\begin{pmatrix} \operatorname{Prob}\{c(n)=1\}\\ \vdots\\ \operatorname{Prob}\{c(n)=N\} \end{pmatrix}}_{y_n}
\tag{4}
```

矩阵 $P$ 的所有元素满足 $0 \le p_{ij} \le 1$。由方程 (3)，每一列之和为 1：

```math
\mathbf{1}^{T}P = \mathbf{1}^{T}\quad \text{且}\quad P^{T}\mathbf{1} = \mathbf{1}
\qquad\text{（其中 }\mathbf{1}\text{ 是全 1 行向量/列向量）}
```

所以 $P^{T}$ 是一个以 $\lambda = 1$ 为特征值、以 $\mathbf{1} = (1,1,\dots,1)$ 为特征向量的非负矩阵。而 $P$ 本身也是一个以 $\lambda = 1$ 为特征值的非负矩阵，但我们必须找出满足 $Pv = v$ 的特征向量：

```math
\text{例题 1}\quad P = \begin{pmatrix}0.8 & 0.3\\ 0.2 & 0.7\end{pmatrix}
\quad \Rightarrow\quad
P\begin{pmatrix}0.6\\0.4\end{pmatrix} = \begin{pmatrix}0.6\\0.4\end{pmatrix}
```

于是 $v = (0.6, 0.4)$。其 trace（迹）为 $0.8 + 0.7 = 1.5$，故第二个特征值为 $\lambda_2 = 0.5$。$P$ 的第二个特征向量 $v_2$ 总是与 $P^{T}$ 的第一个特征向量 $(1,1)$ 正交。

回到概率的转移方程 $y_{n+1} = Py_n$。向量 $y_n$ 与 $y_{n+1}$ 分别包含 $N$ 个状态在时刻 $n$ 与 $n+1$ 的概率。在任何时刻，$P^n$ 的各列之和都是 1（$y_n$ 中的概率之和亦然）：

```math
\mathbf{1}^{T}y_{n+1} = \mathbf{1}^{T}(Py_n) = (\mathbf{1}^{T}P)\,y_n = \mathbf{1}^{T}y_n = 1
\tag{5}
```

这里是马尔可夫链的基本问题。转移矩阵 $P$ 固定且已知；起始状态 $c(0)$ 或该状态的概率向量 $y_0$ 可能已知也可能未知。**关键问题：概率向量 $y_n = P^n y_0$ 在 $n\to\infty$ 时是否有极限？** 我们期望 $y_{\infty}$ 与 $y_0$ 中的初始概率无关。我们会看到 $y_{\infty}$ 常常存在，但并非对每个 $P$ 都如此。当它存在时，$y_{\infty}$ 告诉我们「期望在多久之后处于每个状态」。

<!-- page 316 -->
> <span style="color:#7f8c8d;">本页为书页 314，用例题 2（switching matrix）与例题 3 对比「正 $P$」与「非负 $P$」的收敛差异，引出 Perron 部分的证明思路；页眉与印页码不译。</span>

**例题 2** 转移矩阵可以是 $P = \begin{pmatrix}0 & 1\\ 1 & 0\end{pmatrix}$，即 switching matrix（交换矩阵）。这意味着系统在每个时间步都切换状态。时刻 $n$ 的状态 1 在时刻 $n+1$ 变为状态 2。若初始概率是 $y_0 = \begin{pmatrix}1/2\\1/2\end{pmatrix}$，则 $y_1 = Py_0 = \begin{pmatrix}1/2\\1/2\end{pmatrix}$。概率就在这两个向量之间来回震荡，没有稳态。

我们的矩阵 $P$ 总是有特征值 $\lambda = 1$，其特征向量本应是稳态（乘上 $P$ 后什么都不变）。但这个特定的 $P$ 还有特征值 $\lambda = -1$，它的影响在 $n\to\infty$ 时不会消失。唯一的「稳定」只体现在 $y_0 = y_2 = y_4 = \cdots$ 以及另单独的 $y_1 = y_3 = y_5 = \cdots$ 上。这个矩阵 $P$ 的幂在 $P$ 与 $I$ 之间震荡。

其他矩阵 $P$ 确实有稳态：$P^n \to P^{\infty}$ 且 $y_n \to y_{\infty}$。注意，实际状态 $c$ 仍在变化——依据 $P$ 中的概率 $p_{ij}$。向量 $(y_{1\infty},\dots,y_{N\infty})$ 告诉我们系统最终处于每个状态的时间比例。

**正 $P$ 还是非负 $P$（Positive P or Nonnegative P）**

我们的两个例子之间有明显区别：$P_1 > 0$ 而 $P_2 \ge 0$。

```math
P_1 = \begin{pmatrix}0.8 & 0.3\\ 0.2 & 0.7\end{pmatrix}
\ \text{特征值为}\ 1\ \text{和}\ \tfrac12\text{；幂}\ (\tfrac12)^n\ \text{趋于零。}
```

```math
P_2 = \begin{pmatrix}0 & 1\\ 1 & 0\end{pmatrix}
\ \text{特征值为}\ 1\ \text{和}\ -1\text{；幂}\ (-1)^n\ \text{不趋于零。}
```

$P$ 的每一列之和为 1，于是 $\lambda = 1$ 是一个特征值，因为 $P - I$ 的各行相加为零行。而且 $P$ 没有负元素。这两个性质合在一起保证：没有特征值的绝对值 $|\lambda| > 1$。但 $P_1$ 与 $P_2$ 之间有个重要差别：$P_2$ 有零元素，这就给「某个 $\lambda$ 的绝对值等于 1」留下了可能；而 $P_1$ 的元素严格为正，这就保证 $|\lambda_2| < 1$。

针对 $P_1 > 0$（元素严格为正）的 Perron-Frobenius Theorem 保证成功：

1. $P$ 的最大特征值及其特征向量 $v_1$ 严格为正。
2. 其余所有特征值 $\lambda_2, \dots, \lambda_N$ 满足 $|\lambda_i| < \lambda_1$。而马尔可夫矩阵有 $\lambda_1 = 1$。

第三个例子 $P_3$ 表明，$P$ 中的零元素并不总是破坏趋向稳态的过程：

```math
\text{例题 3}\quad P_3 = \begin{pmatrix}1 & 1\\ 0 & 0\end{pmatrix}
\ \text{有}\ \lambda_1 = 1\ \text{与}\ v_1 = \begin{pmatrix}1\\0\end{pmatrix},\
\lambda_2 = 0\ \text{与}\ v_2 = \begin{pmatrix}1\\-1\end{pmatrix}
```

尽管 $P_3$ 中有那个零元素，$(P_3)^n$ 的所有列仍趋向第一个特征向量 $v_1$：

```math
(P_3)^n \to \begin{pmatrix}1 & 1\\ 0 & 0\end{pmatrix}
\tag{6}
```

这正是我们想要并期待的稳态。于是 $y_n = (P_3)^n y_0$ 也趋向那个相同的特征向量 $v_1 = \begin{pmatrix}1\\0\end{pmatrix}$。这个马尔可夫链随着 $n\to\infty$ 把所有人都移到状态 1。

<!-- page 317 -->
> <span style="color:#7f8c8d;">本页为书页 315，用对角化 $P = X\Lambda X^{-1}$ 展示 $P^n$ 收敛到秩一矩阵 $v_1\mathbf{1}^{T}$，并开始陈述、证明 Perron-Frobenius Theorem；页眉与印页码不译。</span>

**当 $n\to\infty$ 时向稳态收敛**

对于元素严格为正的马尔可夫矩阵，看清收敛 $P^n \to P^{\infty}$ 的最佳方式是对角化 $P$。暂且假设 $P$ 有 $n$ 个线性无关的特征向量。

特征值矩阵 $\Lambda$ 以 $\lambda_1 = 1$ 开头，特征向量矩阵 $X$ 的第一列是主特征向量 $v_1$。随着 $n$ 增大，这个 $v_1$ 会出现在 $P^n$ 的每一列中。

$P = X\Lambda X^{-1}$ 意味着：

```math
P^n = (X\Lambda X^{-1})\cdots(X\Lambda X^{-1}) = X\Lambda^n X^{-1}
```

$X$ 的列是 $P$ 的特征向量 $v_1,\dots,v_n$；$X^{-1}$ 的行是 $P^{T}$ 的特征向量（第一行是全 1 向量 $\mathbf{1}^{T}$）。因为 $\lambda_1 = 1$ 而其余特征值 $|\lambda_i| < 1$，对角矩阵 $\Lambda^n$ 将趋向只在左上角有一个 1 的 $\Lambda^{\infty}$：

```math
P^n = X\Lambda^n X^{-1}\ \to\ v_1 \mathbf{1}^{T}
```

这里给出 $P, P^2, P^3, \dots$ 收敛到以 $v_1$ 填满各列的秩一矩阵 $P^{\infty}$ 的过程：

```math
\begin{pmatrix} .80 & .30\\ .20 & .70\end{pmatrix},\
\begin{pmatrix} .70 & .45\\ .30 & .55\end{pmatrix},\
\begin{pmatrix} .65 & .525\\ .35 & .475\end{pmatrix},\ \dots
\to \begin{pmatrix} .60 & .60\\ .40 & .40\end{pmatrix}
```

至此我们陈述并证明 Perron-Frobenius Theorem。实际上我们证明的是 Perron 的部分（严格正矩阵）；随后 Frobenius 允许 $P$ 中出现零元素，这带来「$|\lambda_2| = \lambda_1$」的可能，此时 $P^n$ 将不收敛（除非 $P = I$）到通常的 $P^{\infty} = v_1\mathbf{1}^{T}$。

**Perron-Frobenius 定理（Perron-Frobenius Theorem）**

有一条矩阵定理统领整个主题。Perron-Frobenius Theorem 适用于所有 $a_{ij} \ge 0$ 的情形，并不要求各列之和为 1。我们证明其中最简洁的形式：当所有 $a_{ij} > 0$ 时，最大特征值 $\lambda_{\max}$ 及其特征向量都是正的。

**针对 $A>0$ 的 Perron-Frobenius**：$A$ 的最大特征值 $\lambda_{\max}$ 及其特征向量 $c$ 的所有分量严格为正。

**证明** 从 $A > 0$ 开始。核心想法是考察所有满足 $Ac \ge tc$（对某个非负向量 $c \ne 0$）的数 $t$。我们允许 $Ac \ge tc$ 中的不等号，是为了获得许多小的正候选值 $t$。对于最大的那个值 $t_{\max}$（它是可达到的），我们将证明等式成立：$Ac = t_{\max} c$。那时 $t_{\max}$ 就是特征值 $\lambda_{\max}$，$c$ 就是特征向量——下面给出证明。

<!-- page 318 -->
> <span style="color:#7f8c8d;">本页为书页 316，完成 Perron 证明（用「$A>0$ 把不等号变严格」+ 三角不等式两条论证），并处理马尔可夫理论的两点精细之处；页眉与印页码不译。</span>

若 $Ac \ge t_{\max} c$ 不是等式，就在两边同乘 $A$。因为 $A > 0$，这会产生一个严格不等式 $A^2 c > t_{\max} Ac$。因此正向量 $y = Ac$ 满足 $Ay > t_{\max} y$，这意味着 $t_{\max}$ 还可以再增大。这一矛盾迫使我们得到等式 $Ac = t_{\max} c$，于是我们就有了一个特征值。其特征向量 $c$ 是正的，因为在该等式左边，$Ac$ 一定是正的。

为说明没有特征值的模能超过 $t_{\max}$，假设 $Az = \lambda z$。由于 $\lambda$ 与 $z$ 可能含负数或复数，我们取绝对值：

```math
|\lambda|\,|z| = |\lambda z| = |Az| \le A|z|
\qquad\text{（由三角不等式）}
```

这个 $|z|$ 是一个非负向量，所以这个 $|\lambda|$ 就是可能的候选值 $t$ 之一。因此 $|\lambda|$ 不能超过 $t_{\max}$——而 $t_{\max}$ 正是 $\lambda_{\max}$。

**马尔可夫理论的精细之处（Finer Points of Markov Theory）**

回到马尔可夫，我们在证明 $P^n \to P^{\infty} = v_1\mathbf{1}^{T}$ 时留下了两个未解决的情形：

1. $P > 0$ 可能严格为正，但未必有 $n$ 个线性无关的特征向量。
2. $P \ge 0$ 可能含有零元素，此时 $|\lambda_2| = 1$ 成为一种可能（而非必然）。

情形 1 是技术问题。重要的事实 $P^n \to P^{\infty}$ 即便在我们没有可逆特征向量矩阵 $X$ 时仍然成立。我们确实在 $\lambda_1 = 1$ 与其余所有特征值之间存在着分离。只要把满足 $Pv_1 = v_1$ 的那个特征向量放在 $X$ 的第一列，$X^{-1}PX$ 的第一列就仍是 $(1, 0, \dots, 0)$。$X^{-1}PX$ 最后那些行与列构成的子矩阵 $A$ 拥有 $P$ 的其余特征值，它们由 Perron-Frobenius 都满足 $|\lambda| < 1$。我们将证明 $A^n \to 0$。

**来自代数的要点**：$X^{-1}PX$ 总可以被化成上三角形式（通常是对角形式）。

若 $|\lambda_2| < 1$，则 $P^n \to P^{\infty}$。

我们想证明：只要 $|\lambda_2| < 1$，就有 $P^n \to P^{\infty} = v_1\mathbf{1}^{T}$。矩阵 $P \ge 0$ 可能含零（如例题 3），也可能没有 $n$ 个线性无关的特征向量，因而无法对角化。但我们仍能把 $\lambda_1 = 1$ 与矩阵其余部分（$|\lambda| < 1$）分离开，这就足以证明 $P^n \to P^{\infty}$。

```math
X^{-1}PX = \begin{pmatrix} 1 & 0\\ 0 & A\end{pmatrix}
\quad\text{且 }A\text{ 的特征值都满足}\ |\lambda| < 1
```

把矩阵 $A$ 隔离出来，我们就得到一个干净、应用广泛的结果：

```math
P^n = X(X^{-1}PX)^n X^{-1} = X\begin{pmatrix} 1 & 0\\ 0 & A^n\end{pmatrix}X^{-1}
\to v_1\mathbf{1}^{T}\quad\text{（}A^n \to 0\text{）}
```

若 $A$ 的所有特征值都满足 $|\lambda| < 1$，则 $A^n \to 0$（当 $n\to\infty$）。

- **步骤 1** 找一个上三角矩阵 $S = M^{-1}AM$，使其范数 $||S|| < 1$。
- **步骤 2** 于是 $A^n = MS^n M^{-1}$，且 $||A^n|| \le ||M||\,||S||^n\,||M^{-1}|| \to 0$。

<!-- page 319 -->
> <span style="color:#7f8c8d;">本页为书页 317，构造范数小于 1 的三角矩阵 $S$（Schur 定理 + 对角相似缩放），并转入带零元素的经典例「赌徒破产」（Gambler's Ruin）；页眉与印页码不译。</span>

我们需要找到那个三角矩阵 $S$——那样证明就完整了。因为 $S = M^{-1}AM$ 与 $A$ 相似，$S$ 与 $A$ 有相同的特征值，而三角矩阵的特征值就出现在其主对角线上：

```math
S = \begin{pmatrix} \lambda_1 & a & b\\ 0 & \lambda_2 & c\\ 0 & 0 & \lambda_3\end{pmatrix}
\quad\text{若 }a,b,c\text{ 都很小，则 }||S|| < 1
```

**要点：最大特征值不是范数！** 若 $a,b,c$ 很大，则幂 $S^2, S^3, \dots$ 一开始会增长；最终 $\lambda_1^n, \lambda_2^n, \lambda_3^n$ 发挥作用，$S^n$ 又落回零矩阵。若我们想保证一开始就不增长，就要让 $S$ 的范数 $||S|| < 1$；那时 $||S^n||$ 将保持在 $||S||^n$ 之下并直接趋于零。

我们知道 $|\lambda_1| < 1,\ |\lambda_2| < 1,\ |\lambda_3| < 1$。若 $a,b,c$ 很小，范数就小于 1：

```math
||S|| \le ||\text{对角部分}|| + ||\text{非对角部分}|| < 1
```

我们分两步达到这个三角 $S = M^{-1}AM$。第一步，每个方阵 $A$ 都相似于某个上三角矩阵 $T = Q^{-1}AQ$，这是带正交矩阵 $Q$ 的 Schur's Theorem（舒尔定理），其证明直接，见《Introduction to Linear Algebra》第 343 页。第二步，用一个对角矩阵 $D$ 缩小 $T$ 中的 $A,B,C$，从而在 $S$ 中得到很小的 $a,b,c$：

```math
D^{-1}TD = \begin{pmatrix} 1 & & \\ & 1/d & \\ & & 1/d^2 \end{pmatrix}
\begin{pmatrix} \lambda_1 & A & B\\ 0 & \lambda_2 & C\\ 0 & 0 & \lambda_3\end{pmatrix}
\begin{pmatrix} 1 & & \\ & d & \\ & & d^2 \end{pmatrix}
= \begin{pmatrix} \lambda_1 & dA & d^2 B\\ 0 & \lambda_2 & dC\\ 0 & 0 & \lambda_3\end{pmatrix}
```

对很小的 $d$，非对角数 $dA$、$d^2 B$ 与 $dC$ 会小到我们想要的程度。于是 $S = M^{-1}AM$ 如步骤 1、步骤 2 所需。

若 $P \ge 0$ 并非严格为正，一切取决于 $P$ 的特征值。我们面对「$|\lambda_2| = 1$ 且 $P^n$ 不收敛」的可能。这里给出例子：

```math
P = \begin{pmatrix} 0 & 0.5 & 0.5\\ 0 & 0.5 & 0.5\\ 0 & 0 & 1\end{pmatrix}
\qquad\text{或}\qquad
P = \begin{pmatrix} 1 & 0 & 0\\ 0 & 1 & 0\\ 0 & 0 & 1\end{pmatrix}
```

**「赌徒破产」（Gambler's Ruin）**

这个矩阵 $P$ 是一个经典的马尔可夫例子。两个赌徒一共有 \$3。系统有四个状态：$(3,0),\ (2,1),\ (1,2),\ (0,3)$。吸收态（absorbing states）是 $(3,0)$ 与 $(0,3)$，即当某个玩家赢了所有钱时——游戏结束，且无法离开这两个状态中的任何一个。有这两个稳态，我们必定得到两次 $\lambda = 1$。

瞬态（transient states）是 $(2,1)$ 与 $(1,2)$，此时进行一场 \$1 的对局——玩家 1 获胜的概率是 $p$，玩家 2 获胜的概率是 $q = 1-p$。$4\times 4$ 的转移矩阵 $P$ 在其中间的列含有这些数 $p$ 与 $q$，对应玩家 1 持有 \$2 或 \$1 的情形。

<!-- page 320 -->
> <span style="color:#7f8c8d;">本页为书页 318，先回答赌徒破产的三个问题（特征值、永远继续的概率、获胜概率 $p^*$），再引入连续的 master equation $dp/dt = Ap$ 与矩阵指数 $e^{At}$；页眉与印页码不译。</span>

**问题：$P$ 的四个特征值是什么？**

**答案：** $\lambda = 1,\ 1,\ \sqrt{pq},\ -\sqrt{pq}$。所以（转移矩阵形如）

```math
P = \begin{pmatrix} 1 & p & 0 & 0\\ 0 & 0 & p & 0\\ 0 & q & 0 & 0\\ 0 & 0 & q & 1\end{pmatrix}
```

$\lambda_1 = 1$ 出现两次，因而没有唯一的稳态。

**问题：游戏永远继续下去、没有赢家的概率是多少？**

**答案：** 零。以概率 1 这个游戏会结束。

**问题：若游戏从 $(2,1)$ 开始，玩家 1 获胜的概率 $p^*$ 是多少？**

**答案：** 好问题！玩家 1 在第一轮立即获胜的概率是 $p$。玩家 2 赢得第一轮、使状态变为 $(\$1,\$2)$ 的概率是 $q = 1-p$。接着玩家 1 赢得第二轮、使状态回到 $(\$2,\$1)$ 的概率是 $p$。从那里开始，玩家 1 最终以概率 $p^*$ 获胜。由此可以解出 $p^*$：

```math
p^* = p + q p\, p^*
\quad\Longrightarrow\quad
p^* = \frac{p}{1-qp}
```

**主方程：连续马尔可夫过程（Master Equations: Continuous Markov Processes）**

Master equation（主方程）拥有一个响亮的名字。它们是关于概率向量 $p(t)$（分量非负、总和为 1）的线性微分方程 $dp/dt = Ap$。矩阵 $A$ 很特殊：对角线上为负或零，非对角线上为正或零，各列之和为零。这个连续马尔可夫过程的概率为 $e^{At}p(0)$。

在时刻 $t$ 处于状态 $j$ 的概率是 $p_j(t)$。在一个很小时段 $dt$ 内，状态从 $j$ 变到 $i$ 的概率是 $a_{ij}\,dt$。给定 $p(0)$，解来自矩阵指数 $p(t) = e^{At}p(0)$。那个矩阵 $e^{At}$ 将是一个马尔可夫矩阵。

**证明** 若 $n$ 很大，$I + (tA/n)$ 是一个普通马尔可夫矩阵，其各列之和为 1。于是

```math
\Big(I + \frac{tA}{n}\Big)^n \ \text{收敛到}\ P = e^{At}\ \text{（也是马尔可夫矩阵）}
```

并且随着 $t\to\infty$，$e^{At}$ 以通常的方式收敛到极限 $P^{\infty}$。

一个例子是矩阵 $A$，其对角线为 $-1,-2,\dots,-1$（即 $-1,-2,\dots,-2,-1$），只是 $A_{11} = A_{NN} = -1$。这就是一条节点线上的图 Laplacian（graph Laplacian）的相反数。热方程在 Neumann boundary conditions（诺伊曼边界条件）下的有限差分近似就用到这个矩阵。

这个 $A$ 也出现在双分子反应 $A + B \to C$ 的 master equation 中：一个 $A$ 分子与一个 $B$ 分子化学结合，形成一个 $C$ 分子。

```math
A = \begin{pmatrix} -1 & 1 & 0 & 0\\ 1 & -2 & 1 & 0\\ 0 & 1 & -2 & 1\\ 0 & 0 & 1 & -1\end{pmatrix}
\quad
I + \frac{t}{n}A = \begin{pmatrix} 1-\frac{t}{n} & \frac{t}{n} & 0 & 0\\ \frac{t}{n} & 1-\frac{2t}{n} & \frac{t}{n} & 0\\ 0 & \frac{t}{n} & 1-\frac{2t}{n} & \frac{t}{n}\\ 0 & 0 & \frac{t}{n} & 1-\frac{t}{n}\end{pmatrix}
```

$A$ 的各列之和为零；$I + \frac{t}{n}A$ 的各列之和为 1。于是 $P = e^{At}$ 是马尔可夫矩阵。

<!-- page 321 -->
> <span style="color:#7f8c8d;">本页为书页 319，为习题集 V.6 的第 1–6 题；页眉与印页码不译。</span>

**习题集 V.6（Problem Set V.6）**

1. 找出一个 Markov matrix $P > 0$，它含有一个零元素，但 $P^2$ 严格为正。
2. $P$ 的各列之和为 1，所以 $\lambda_{\max} = 1$。你如何知道 $P$ 的其余特征值满足 $|\lambda| < 1$？于是 $P^n$ 趋近于以 $v_1$ 填满每一列的 $P^{\infty}$。
3. 若 $A$ 的所有元素为正，则 $A^{T}A$ 与 $AA^{T}$ 的所有元素为正。用 Perron 定理证明：最接近 $A$ 的秩一矩阵 $\sigma_1 u_1 v_1^{T}$ 也是正的。
4. 这些矩阵满足 $||A|| > 1$ 且 $||M|| > 1$。找出矩阵 $B$ 与 $C$，使得 $||BAB^{-1}|| < 1$ 且 $||CMC^{-1}|| < 1$。这之所以肯定可能，是因为 $A$ 与 $M$ 的特征值的绝对值都小于 1。若 $M$ 是马尔可夫矩阵，为什么不可能？

```math
A = \begin{pmatrix} 0 & 1\\ 0 & 0\end{pmatrix}\qquad
M = \begin{pmatrix} 1 & 1\\ 0 & 0\end{pmatrix}
```

5. 为什么 $||BZB^{-1}|| \le 1$ 对任何 $B$ 都不可能，而 $||CYC^{-1}|| \le 1$ 却可能？

```math
Z = \begin{pmatrix} 0 & 1\\ 0 & 0\end{pmatrix}\qquad
Y = \begin{pmatrix} 1 & 1\\ 0 & 1\end{pmatrix}
```

6. 若对 $A$ 取幂，$A^n$ 在 $n\to\infty$ 时的极限是什么？

```math
A = \begin{pmatrix} 2/3 & 1/3\\ 1/3 & 2/3\end{pmatrix}
\qquad\text{以及}\qquad
A = \begin{pmatrix} 2 & 1 & 1\\ 1 & 2 & 1\\ 1 & 1 & 2\end{pmatrix}
```

另：假设每年纽约和佛罗里达各有 99% 的人迁往佛罗里达与纽约——但有 1% 的人死亡（对这个问题我表示抱歉）。你能构造一个对应「纽约–佛罗里达–死亡」三态的 $3\times 3$ Markov matrix $P$ 吗？矩阵 $P^n$ 在 $n\to\infty$ 时的极限是什么？

<!-- page 322 -->
> <span style="color:#7f8c8d;">本页为书页 320，是第六部分「Optimization（最优化）」的目录页，列出 VI.1–VI.5 五节的标题；页眉与印页码不译。</span>

**第六部分　Optimization（最优化）**

- VI.1　Minimum Problems: Convexity and Newton's Method（最小值问题：凸性与牛顿法）
- VI.2　Lagrange Multipliers = Derivatives of the Cost（拉格朗日乘子 = 代价函数的导数）
- VI.3　Linear Programming, Game Theory, and Duality（线性规划、博弈论与对偶性）
- VI.4　Gradient Descent Toward the Minimum（走向最小值的梯度下降）
- VI.5　Stochastic Gradient Descent and ADAM（随机梯度下降与 ADAM）

---

<span style="color:#27ae60;">**【译者注 1 · 为什么马尔可夫矩阵「列和为 1」必然给出特征值 $\lambda=1$？】** 这是理解本节一切收敛现象的起点。矩阵 $P$ 的每一列之和为 1，等价于全 1 行向量满足 $\mathbf{1}^{T}P = \mathbf{1}^{T}$——也就是说 $\mathbf{1}^{T}$ 是 $P$ 的**左**特征向量，对应特征值 1。而矩阵与其转置有相同的特征值，所以 $P$ 也必有特征值 1，其对应的**右**特征向量 $v_1$ 才是我们关心的稳态。左、右特征向量在这里扮演不同角色：左特征向量 $\mathbf{1}^{T}$ 表达「总概率守恒」（$\mathbf{1}^{T}y_n$ 恒为 1，见式 (5)），右特征向量 $v_1$ 表达「长期分布的形状」（$y_\infty$ 是 $v_1$ 的倍数）。这两者由 Perron-Frobenius 定理连成闭环：正矩阵保证 $v_1$ 的各分量严格为正，于是稳态是一个合法的概率分布而非带负分量的「伪概率」。这就是为什么列和为 1 加上正元素，能同时保证「有稳态」且「稳态有意义」。</span>

<span style="color:#27ae60;">**【译者注 2 · 收敛速度为什么是 $|\lambda_2|$，而不是别的？】** 把 $P$ 对角化后 $P^n = X\Lambda^n X^{-1}$，$y_n$ 中除主特征方向外的一切都随 $\lambda_2^n$ 衰减。Strang 在开头用「距离到稳态每月减半」直观说明了这一点：$\lambda_2 = 0.5$ 就是衰减因子。更精细地说，收敛速度由 $|\lambda_2|/\lambda_1$ 这个比值决定——这里 $\lambda_1=1$ 所以简化为 $|\lambda_2|$。这解释了例题 2 为何不收敛：其 $\lambda_2 = -1$，$|\lambda_2| = 1 = \lambda_1$，衰减因子等于 1，误差永不缩小，只能在 $P$ 与 $I$ 之间震荡。因此 $|\lambda_2| < 1$（严格小于）是马尔可夫链收敛的充要条件——它衡量的正是「第二大的特征方向要以多快的速度被磨平」。这与前文对角化、后文「最大特征值不是范数」的讨论是同一件事：特征值决定长期行为，而范数决定短期行为，二者不可混为一谈。</span>

<span style="color:#27ae60;">**【译者注 3 · 离散马尔可夫链与连续 master equation 如何统一在 $e^{At}$ 下？】** 离散链的更新是 $y_{n+1} = Py_n$，连续过程的更新是 $dp/dt = Ap$，看起来一阶差分与导数差了「一个时间步」。统一的桥梁是证明里那一步：$e^{At} = \lim_{n\to\infty}(I + tA/n)^n$。每个因子 $I + tA/n$ 在 $n$ 很大时就是一个合法的（列和为 1 的）马尔可夫矩阵——因为 $A$ 各列之和为零，所以 $I + tA/n$ 各列之和恰好为 1；又因 $A$ 的非对角元素非负、对角元素非正，$n$ 足够大时 $I + tA/n$ 的各元素都落在 $[0,1]$。于是连续过程被看成「无限多步极小时间步的离散链」的极限，矩阵指数把离散的 $P^n$ 与连续的 $e^{At}$ 纳入了同一个框架。这也呼应了本书始终贯彻的一个观点：矩阵指数之于连续系统，正如矩阵幂之于离散系统。</span>

<span style="color:#27ae60;">**【译者注 4 · 赌徒破产里 $p^* = p/(1-qp)$ 是怎么解出来的？】** 关键是用「马尔可夫性」把问题递归化。设从状态 $(\$2,\$1)$ 出发玩家 1 最终获胜的概率为 $p^*$。看第一轮之后的三种去向：玩家 1 直接赢（概率 $p$），玩家 2 赢（概率 $q$，状态变为 $(\$1,\$2)$），然后玩家 1 又赢回（概率 $p$）回到原点 $(\$2,\$1)$——但过程无记忆，回到原点后获胜概率仍是 $p^*$。于是 $p^* = p + q\cdot p\cdot p^*$，即获胜 = 首轮直接赢，或首轮输掉但随后又回到原点再重新计算。解这个一次方程得 $p^* = p/(1-qp)$。注意 $1-qp = 1-(1-p)p = 1-p+p^2$，恒大于零，故分母不会为零，$p^*$ 总有意义。这一「拆第一轮、其余递归」的技巧，正是全概率公式在马尔可夫链上的典型用法，与正文「距离减半」背后同一个思想——只依赖当前状态。</span>

[[FIGURE: 书页 311, 100 辆车在芝加哥与丹佛之间每月流动的转移示意图，标出 0.8/0.2 与 0.3/0.7 四条转移概率]]
[[FIGURE: 书页 315, $P, P^2, P^3,\dots$ 逐步逼近 $P^\infty$ 的矩阵数值序列示意]]

---

## 本节译者注

> <span style="color:#1e8449;">**[note] Markov 矩阵为什么要求「每列相加为 1」：**</span> 这一约束并非数学上的随意装饰，而是「汽车不凭空产生、也不凭空消失」这一物理守恒的直接翻译。设第 $j$ 列表示「从状态 $j$ 出发、下一时刻去向各个状态的概率」，那么第 $j$ 列的全体元素 $p_{1j}+p_{2j}+\cdots+p_{Nj}=1$ 说的正是：从 $j$ 出发的 100 辆车（或一份总概率 1），无论如何移动，下一时刻仍被完整地分配到 $N$ 个状态里。用行向量全 1 表示 $\mathbf{1}^{T}=(1,\dots,1)$，这一约束可紧凑地写成 $\mathbf{1}^{T}P=\mathbf{1}^{T}$，即 $\mathbf{1}$ 是 $P^{T}$ 的（左）特征值为 $1$ 的特征向量。这一式子在逻辑上「一箭三雕」：它同时保证了 $P$ 有特征值 $\lambda_1=1$（因为 $P^{T}$ 与 $P$ 有相同特征值）、保证了每步迭代后 $y_{n+1}=Py_n$ 的分量和仍为 1（$\mathbf{1}^{T}y_{n+1}=\mathbf{1}^{T}Py_n=\mathbf{1}^{T}y_n=1$），也为「稳态分布」的存在埋下伏笔——$Pv=v$ 的那个特征向量 $v$，正是每列相加为 1 时自动被锁定在 $\lambda=1$ 上的。理解这一点，本节后文所有关于 $\lambda=1$ 的讨论才有一个共同出发点。

> <span style="color:#1e8449;">**[note] $P^n=X\Lambda^nX^{-1}$ 是「幂的收敛」如何由「特征值的模」决定：**</span> 本节反复出现的对角化 $P^n=X\Lambda^{n}X^{-1}$，本质是在做一次「换坐标、在主轴上看、再换回来」的操作：把状态向量投影到特征向量张成的坐标系里，在每一根主轴上独立地乘 $\lambda_k^{n}$，最后再合回原坐标。于是极限行为只取决于对角阵 $\Lambda^{n}$ 的对角元 $\lambda_k^{n}$ 的走势。以书中的例子 $P=\begin{bmatrix}0.8&0.3\\0.2&0.7\end{bmatrix}$，特征值为 $1$ 与 $0.5$，故 $\Lambda^{n}\to\begin{bmatrix}1&0\\0&0\end{bmatrix}$：$\lambda_1=1$ 的幂恒为 1「存活」下来，而 $0.5^{n}\to 0$「衰减归零」。代入后 $P^{n}\to X\begin{bmatrix}1&0\\0&0\end{bmatrix}X^{-1}$，其几何意义是「把整个空间投影到最大特征向量 $v_1=(0.6,0.4)$ 所在的一维直线上」，这正是 $P^{\infty}$ 每一列都变成 $v_1$ 的原因——秩一矩阵 $P^{\infty}=v_1\,(1,1)$，两列完全相同。这也解释了为何 $100\to80\to70\to65$ 每步都在「距离 60 的差」上乘 $\tfrac12$：这个衰减因子正是第二个特征值 $0.5$。换言之，收敛速度由「次大特征值的模」决定，模越小，趋近稳态越快。

> <span style="color:#1e8449;">**[note] 与全书别处及一个数值例子的联系：Perron–Frobenius 是「正矩阵版」的谱半径定理：**</span> 本节把 Markov 链的收敛归结为 Perron–Frobenius Theorem（正/非负矩阵的 Perron–Frobenius 定理），它与全书前文「特征值、对角化、幂 $A^n$」的主线是同一件事的升华：普通的谱分析只保证「若可对角化则 $A^n=X\Lambda^nX^{-1}$」，却不能保证 $\lambda_1$ 是正的、且其余特征值严格更小；而正矩阵定理额外地告诉我们——只要 $a_{ij}>0$，最大特征值 $\lambda_{\max}>0$ 及其特征向量 $v_1$ 全为**正**，其余特征值满足 $|\lambda|< \lambda_1$。对一个 Markov 矩阵而言 $\lambda_1=1$，于是其余 $|\lambda|<1$ 自动成立，$P^{n}\to P^{\infty}$ 就水到渠成。一个具体数值例子：对 $P=\begin{bmatrix}0.8&0.3\\0.2&0.7\end{bmatrix}$，若初始 $y_0=(100,0)$，则 $y_1=Py_0=(80,20)$、$y_2=(70,30)$、$y_3=(65,35)$，逐项核对「距离 60」依次为 $40,20,10,5$，恰好每步乘 $\tfrac12$（即 $\lambda_2=0.5$）；而初始 $y_0=(0,100)$ 则得到 $(30,70)\to(45,55)\to(52.5,47.5)$，两条路径最终都收敛到同一个 $(60,40)$。这正是定理的核心承诺：**只要 $P$ 严格为正，稳态唯一、且与起点无关**；而一旦出现零元素（如切换矩阵 $P_2=\begin{bmatrix}0&1\\1&0\end{bmatrix}$，特征值 $1,-1$），$\lambda=-1$ 的幂不衰减，$P^n$ 只在 $P$ 与 $I$ 之间振荡、永无稳态——恰与 Perron–Frobenius 允许零元素时「$\lambda$ 的模可等于 $\lambda_1$」的警告一一对应。
