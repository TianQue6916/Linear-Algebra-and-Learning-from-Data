# Linear Algebra and Learning From Data（线性代数与数据学习）· V.6

## 书页 311-320 ｜ PDF 页 313-322 ｜ Markov Chains（马尔可夫链）

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
\text{$P$ 的第 $j$ 列：}\quad p_{1j} + p_{2j} + \cdots + p_{Nj} = 1
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
\qquad\text{（其中 $\mathbf{1}$ 是全 1 行向量/列向量）}
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
\quad\text{且 $A$ 的特征值都满足}\ |\lambda| < 1
```

把矩阵 $A$ 隔离出来，我们就得到一个干净、应用广泛的结果：

```math
P^n = X(X^{-1}PX)^n X^{-1} = X\begin{pmatrix} 1 & 0\\ 0 & A^n\end{pmatrix}X^{-1}
\to v_1\mathbf{1}^{T}\quad\text{（$A^n \to 0$）}
```

若 $A$ 的所有特征值都满足 $|\lambda| < 1$，则 $A^n \to 0$（当 $n\to\infty$）。

- **步骤 1** 找一个上三角矩阵 $S = M^{-1}AM$，使其范数 $||S|| < 1$。
- **步骤 2** 于是 $A^n = MS^n M^{-1}$，且 $||A^n|| \le ||M||\,||S||^n\,||M^{-1}|| \to 0$。

<!-- page 319 -->
> <span style="color:#7f8c8d;">本页为书页 317，构造范数小于 1 的三角矩阵 $S$（Schur 定理 + 对角相似缩放），并转入带零元素的经典例「赌徒破产」（Gambler's Ruin）；页眉与印页码不译。</span>

我们需要找到那个三角矩阵 $S$——那样证明就完整了。因为 $S = M^{-1}AM$ 与 $A$ 相似，$S$ 与 $A$ 有相同的特征值，而三角矩阵的特征值就出现在其主对角线上：

```math
S = \begin{pmatrix} \lambda_1 & a & b\\ 0 & \lambda_2 & c\\ 0 & 0 & \lambda_3\end{pmatrix}
\quad\text{若 $a,b,c$ 都很小，则 $||S|| < 1$}
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
