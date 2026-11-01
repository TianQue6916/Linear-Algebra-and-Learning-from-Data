# Linear Algebra and Learning From Data（线性代数与数据学习）· V.4

## 书页 293-304 ｜ PDF 页 295-306 ｜ Covariance Matrices and Joint Probabilities（协方差矩阵与联合概率）

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
