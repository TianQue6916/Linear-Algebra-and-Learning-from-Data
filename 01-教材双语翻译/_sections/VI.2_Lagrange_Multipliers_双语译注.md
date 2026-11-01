# Linear Algebra and Learning From Data（线性代数与数据学习）· VI.2

## 书页 333-338 ｜ PDF 页 335-340 ｜ Lagrange Multipliers = Derivatives of the Cost（拉格朗日乘子 = 代价的导数）

> <span style="color:#7f8c8d;">本节把上一章非结构化的凸优化收束到「强结构化」问题：在线性等式约束 $A^Tc=b$ 下极小化二次型 $F(c)=\tfrac12 c^TSc$。核心结论是——拉格朗日乘子 $\lambda$ 恰恰等于最小代价对约束水平 $b$ 的导数（带负号），并由此引出 saddle point（鞍点）、KKT 矩阵、Schur complement 与 min-max/max-min 对偶。页眉与印页码不译。</span>

---

<!-- page 335 -->

VI.2 **Lagrange Multipliers = Derivatives of the Cost**（拉格朗日乘子 = 代价的导数）

上一节的非结构化（unstructured）问题处理的是 convex set（凸集）$K$ 上的 convex function（凸函数）$F(x)$。本节则从高度结构化（highly structured）的问题入手，观察 Lagrange multipliers（拉格朗日乘子）如何处理约束（constraints）。我们想揭示这些乘子 $\lambda_1,\dots,\lambda_m$ 的含义。引入它们、使用它们之后，再把它们丢弃，是大错特错的。

我们的第一个例子在二维空间。函数 $F$ 是 quadratic（二次的），集合 $K$ 是 linear（线性的）：

> 在直线 $K:\ a_1x_1+a_2x_2=b$ 上极小化 $F(x)=x_1^2+x_2^2$。

在直线 $K$ 上，我们要找的是离 $(0,0)$ 最近的点。代价（cost）$F(x)$ 是距离的平方。在图 VI.4 中，约束直线在最优点 $x^{*}=(\tfrac{a_1b}{a_1^2+a_2^2},\tfrac{a_2b}{a_1^2+a_2^2})$ 处与圆相切。我们把约束方程 $a_1x_1+a_2x_2=b$ 代入函数 $F=x_1^2+x_2^2$ 之后，就能用简单的微积分得到这个结论。

这正是 Lagrange 的巧妙想法。

用一个未知乘子去乘 $a_1x_1+a_2x_2-b$，再加到 $F(x)$ 上：

```math
\text{Lagrangian}\quad L(x,\lambda) = F(x)+\lambda(a_1x_1+a_2x_2-b)=x_1^2+x_2^2+\lambda(a_1x_1+a_2x_2-b)
```

令导数 $\partial L/\partial x_1$、$\partial L/\partial x_2$、$\partial L/\partial\lambda$ 都为零，解这三个方程求出 $x_1,x_2,\lambda$：

```math
\partial L/\partial x_1 = 2x_1+\lambda a_1 = 0
```

```math
\partial L/\partial x_2 = 2x_2+\lambda a_2 = 0
```

```math
\partial L/\partial\lambda = a_1x_1+a_2x_2-b = 0 \qquad(\text{这就是约束！})
```

前两个方程给出 $x_1=-\tfrac12\lambda a_1$、$x_2=-\tfrac12\lambda a_2$。代入 $a_1x_1+a_2x_2=b$ 得：

```math
-\tfrac12\lambda(a_1^2+a_2^2)=b \quad\Rightarrow\quad \lambda=\frac{-2b}{a_1^2+a_2^2}
```

代回 (2a)、(2b) 即得最优点 $(x_1^{*},x_2^{*})$ 与最小代价：

```math
x_1^{*}=\frac{a_1b}{a_1^2+a_2^2},\qquad x_2^{*}=\frac{a_2b}{a_1^2+a_2^2},\qquad
F_{\min}=\frac{b^2}{a_1^2+a_2^2}
```

最小代价对约束水平 $b$ 的导数等于负的拉格朗日乘子：

```math
\frac{d}{db}\left(\frac{b^2}{a_1^2+a_2^2}\right)=\frac{2b}{a_1^2+a_2^2}=-\lambda
```

> <span style="color:#27ae60;">**译者注①｜乘子 $\lambda$ 为何“等于”代价的导数（换什么换到什么）**：约束 $a_1x_1+a_2x_2=b$ 里的右端 $b$ 并不是固定死的东西，它可以理解成“这个约束被允许放松多少”。若把 $b$ 增加一个无穷小量 $db$，可行直线整体外移，最优点和最小代价都会随之改变。式子 $\dfrac{dF_{\min}}{db}=-\lambda$ 说的正是：约束每松一单位，最小代价就下降 $\lambda$ 单位——所以 $\lambda$ 是约束的“影子价格（shadow price）”，衡量这条约束到底有多“贵”。推导的机制就是微积分里的包络定理（envelope theorem）：在最优点，$L$ 对 $b$ 的全导数只剩 $\partial L/\partial b=-\lambda$，因为 $L$ 对 $x$ 的偏导在那里已经等于零。这正是“拉格朗日乘子 = 代价的导数”这句话的数学实质，也是本书刻意强调“用完乘子不要丢掉”的原因。</span>

---

<!-- page 336 -->

### 带线性约束的二次型极小化

我们把那个例子从平面 $\mathbb{R}^2$ 移到空间 $\mathbb{R}^n$。原来对 $x$ 的一条约束，现在变成 $m$ 条约束 $A^Tx=b$。矩阵 $A^T$ 是 $m\times n$ 的，每条约束对应一个拉格朗日乘子 $\lambda_1,\dots,\lambda_m$。代价函数 $F(x)=\tfrac12 x^TSx$ 允许 $S$ 是任意 symmetric positive definite（对称正定）矩阵。

> **问题**：在约束 $A^Tx=b$ 下，极小化 $F=\tfrac12 x^TSx$。 (5)

有 $m$ 条约束，就有 $m$ 个乘子 $\lambda=(\lambda_1,\dots,\lambda_m)$。它们把约束 $A^Tx=b$ 组装进 Lagrangian：

```math
L(x,\lambda)=\tfrac12 x^TSx+\lambda^T(A^Tx-b)
```

$L$ 的 $n+m$ 个导数给出 $n+m$ 个方程，用于求解 $\mathbb{R}^n$ 中的向量 $x$ 与 $\mathbb{R}^m$ 中的向量 $\lambda$：

```math
\text{对 }x\text{ 求导}:\quad Sx+A\lambda=0
```

```math
\text{对 }\lambda\text{ 求导}:\quad A^Tx=b
```

第一个方程给出 $x=-S^{-1}A\lambda$，代入第二个方程给出 $-A^TS^{-1}A\lambda=b$。这确定了最优的 $\lambda^{*}$，进而确定最优的 $x^{*}$：

```math
\lambda^{*}=-(A^TS^{-1}A)^{-1}b,\qquad x^{*}=S^{-1}A(A^TS^{-1}A)^{-1}b
```

```math
\text{最小代价}\quad F^{*}=\tfrac12 x^{*T}Sx^{*}=\tfrac12 b^T(A^TS^{-1}A)^{-1}b
```

这大大简化了！最小代价 $F^{*}$ 正是代价的 gradient（梯度）性质的另一面。

这只是一个 model problem（模型问题）。当约束变成不等式 $A^Tx\le b'$ 时，乘子变为 $\lambda\ge 0$，问题也就更难了。

> <span style="color:#27ae60;">**译者注②｜$A^TS^{-1}A$ 从何而来（消元视角）**：把 $x=-S^{-1}A\lambda$ 代回 $A^Tx=b$，出现的 $A^TS^{-1}A$ 并不是偶然。它有一个更本质的来源——下一段要讲的 Schur complement（舒尔补）。若把 KKT 矩阵 $\begin{bmatrix}S&A\\A^T&0\end{bmatrix}$ 的第一块行左乘 $A^TS^{-1}$ 再从第二块行减去，右下角就“消出”一个 $-A^TS^{-1}A$。也就是说，$A^TS^{-1}A$ 是“把 $x$ 这个变量消掉之后，剩下的关于 $\lambda$ 的约化系数矩阵”，它把原来 $n+m$ 个联立方程压缩成 $m$ 个关于 $\lambda$ 的方程。在物理里它正是 conductance matrix（电导矩阵）与 stiffness matrix（刚度矩阵），其正定性保证了约束问题可解、最优解唯一。</span>

---

<!-- page 337 -->

请允许我回到方程 (6) 里的那个 “saddle point matrix（鞍点矩阵）”或 “KKT matrix（KKT 矩阵）”：

```math
M=\begin{bmatrix}S&A\\A^T&0\end{bmatrix}\begin{bmatrix}x\\\lambda\end{bmatrix}=\begin{bmatrix}0\\b\end{bmatrix}
```

那个矩阵 $M$ 既非 positive definite（正定）也非 negative definite（负定）。假设你把第一块行 $[S\ \ A]$ 左乘 $A^TS^{-1}$ 得到 $[A^T\ \ A^TS^{-1}A]$，再从第二块行减去它，就看出一个零块：

```math
\begin{bmatrix}S&A\\0&-A^TS^{-1}A\end{bmatrix}\begin{bmatrix}x\\\lambda\end{bmatrix}=\begin{bmatrix}0\\b\end{bmatrix}
```

这只是对 $2\times2$ 分块矩阵 $M$ 做消元。那个出现在 (2,2) 位置的新块，叫做 Schur complement（舒尔补，得名于有史以来最伟大的线性代数学家）。

我们又回到了和之前一样的方程 $-A^TS^{-1}A\lambda=b$。消元不过是求解线性方程的一种有条理的方法。前 $n$ 个主元（pivots）是正的，因为 $S$ 正定；而后面会有 $m$ 个负主元，因为 $-A^TS^{-1}A$ 负定。这正是 Lagrangian $L(x,\lambda)$ 存在 saddle point（鞍点）的明确标志——那个函数 $L=\tfrac12x^TSx+\lambda^T(A^Tx-b)$ 对 $x$ 是凸的，对 $\lambda$ 是凹的。

### Minimax = Maximin（极小极大 = 极大极小）

这个问题还有更多可学之处。方程 (6) 已把 $L$ 对 $x$ 的导数和对 $\lambda$ 的导数同时置零，我们解出了 $x^{*}$ 和 $\lambda^{*}$。那个二元组 $(x^{*},\lambda^{*})$ 就是方程 (7) 中 $L$ 的鞍点。通过求解 (7)，我们在 (8) 里找到了最小代价及其导数。

假设我们把这件事拆成两个问题：一个极小问题和一个极大问题。先对每个固定的 $\lambda$ 极小化 $L(x,\lambda)$，极小点 $x^{*}$ 依赖于 $\lambda$；再去找使 $L(x^{*},\lambda)$ 最大的 $\lambda$。

在 $x^{*}$ 处极小化 $L$ 得到：

```math
\min_x L = -\tfrac12\lambda^TA^TS^{-1}A\lambda-\lambda^Tb
```

再对这个极小值求极大：

```math
\max_\lambda\min_x L = \tfrac12 b^T(A^TS^{-1}A)^{-1}b
```

这个 maximin（极大极小）是先对 $x$、后对 $\lambda$。反过来就是 minimax（极小极大）：先对 $\lambda$、后对 $x$。$L(x,\lambda)=\tfrac12x^TSx+\lambda^T(A^Tx-b)$ 对 $\lambda$ 的最大值是：

```math
\max_\lambda L(x,\lambda)=
\begin{cases}
\tfrac12 x^TSx, & A^Tx=b\\[2pt]
+\infty, & A^Tx\ne b
\end{cases}
```

再对这个最大值对 $x$ 求极小，正是我们的答案：

```math
\min_x\max_\lambda L = \tfrac12 b^T(A^TS^{-1}A)^{-1}b
```

在鞍点 $(x^{*},\lambda^{*})$ 处我们有：

```math
\max_\lambda\min_x L = \min_x\max_\lambda L = L(x^{*},\lambda^{*})
```

> <span style="color:#27ae60;">**译者注③｜max-min 与 min-max 为什么在这里相等（对偶机制）**：$\max_\lambda$ 里 $L$ 是 $\lambda$ 的线性函数，若 $A^Tx\ne b$，$\lambda^T(A^Tx-b)$ 可以随 $\lambda$ 沿某个方向趋向 $+\infty$，于是 $\max_\lambda L=+\infty$；只有当 $A^Tx=b$ 时线性项为零，最大值才回到 $\tfrac12x^TSx$。这一“惩罚”实际上把硬约束重新编码进了目标：先 max 再 min，等于“在满足约束的前提下找最小代价”。反过来先 min 后 max，则是把 $x$ 消掉后对 $\lambda$ 求最大，得到 $-A^TS^{-1}A\lambda=b$ 的解。两者在同一鞍点处相等，这就是弱对偶与强对偶（strong duality）在二次型情形下的体现——与 VI.3 讲 linear programming 的对偶是同一件事，只不过那里是线性、这里是二次。</span>

---

<!-- page 338 -->

### 科学与工程中的对偶问题

在一条线性约束 $A^Tx=b$ 下极小化二次型 $\tfrac12x^TSx$，并不只是一个抽象练习。当线性微分方程被离散化（made discrete）时，它正是物理应用数学的核心问题。这里有两个主要例子。

**1. 电路的网络方程（Network equations）**
未知量：各节点的电压（voltages）、各边的电流（currents）。
方程：Kirchhoff 定律与 Ohm 定律。
矩阵：$A^TS^{-1}A$ 是 conductance matrix（电导矩阵）。

**2. 结构的有限元方法（Finite element method）**
未知量：各节点的位移（displacements）、结构中的应力（stresses）。
方程：力的平衡与 stress–strain（应力–应变）关系。
矩阵：$A^TS^{-1}A$ 是 stiffness matrix（刚度矩阵）。

完整清单可延伸到工程的每个领域。刚度矩阵与电导矩阵都是对称正定的。通常约束是等式而非不等式，于是数学上对这类物理问题建模有三种途径：

1. （i）带刚度矩阵 / 电导矩阵 / 系统矩阵的线性方程组；
2. （ii）以电流或应力为未知量 $x$ 的极小化；
3. （iii）以电压或位移为未知量的极大化。

最终，线性方程组 (i) 是流行的选择——我们把方程 (9) 约化为方程 (10)。那些网络方程同时表达了 Kirchhoff 定律与 Ohm 定律；结构方程则表达了力的平衡与材料的性质。所有电学与力学定律都被“建进”了最终的方程组。

对于流体流动问题，这个方程组常以鞍点形式出现，未知量 $x$ 与 $\lambda$ 分别是速度（velocities）与压强（pressures）。相关数值分析在 Elman、Silvester 与 Wathen 合著的 *Finite Elements and Fast Iterative Solvers* 一书中有很好的描述。

对于导出电导矩阵与刚度矩阵 $A^TCA$ 的网络方程和有限元方程，可参考我的教材 *Computational Science and Engineering*；18.085 的视频课程见 ocw.mit.edu。

在统计学与 least squares（最小二乘 / 线性回归）中，矩阵 $A^TE^{-1}A$ 包含 $E=$ covariance matrix（协方差矩阵）。我们用方差 $\sigma^2$ 来除，以对噪声做 whiten（白化）。

对非线性问题，能量不再是二次型 $\tfrac12x^TSx$。几何非线性出现在矩阵 $A$ 中；材料非线性（通常更简单）出现在矩阵 $C$ 中。大位移与大应力是非线性的典型来源。

> <span style="color:#27ae60;">**译者注④｜同一个 $A^TS^{-1}A$ 为何贯穿三大领域（同一件事）**：这一页表面在罗列应用，其实是在印证前一页的 Schur complement 结论——无论电路、结构还是统计回归，消掉“内变量”（电流、应力、残差）之后剩下的约化矩阵都长成 $A^T(\cdot)^{-1}A$ 的形式。电路里 $S^{-1}$ 是电阻（欧姆定律的体现），$A$ 是节点-边的关联矩阵，$A^TS^{-1}A$ 就是电导矩阵；结构里 $S^{-1}$ 是柔度，$A$ 是位移-应变的几何关系，$A^TS^{-1}A$ 就是刚度矩阵；统计里 $S^{-1}=\Sigma^{-1}$ 除以方差正是 whitening。三种物理在“能量极小化 + 线性约束”这一数学骨架下是同一件事，这正是作者强调“对偶三途径 (i)(ii)(iii)”的用意。</span>

---

<!-- page 339 -->

### Problem Set VI.2（习题集 VI.2）

**1.** 在约束 $A^Tx=x_1+3x_2=4$ 下极小化 $F(x)=x_1^2+x_2^2$。

（a）此问题的 Lagrangian $L(x,\lambda)$ 是什么？
（b）“$L$ 的导数 = 零”的三个方程是什么？
（c）解这些方程求出 $x^{*}=(x_1^{*},x_2^{*})$ 与乘子 $\lambda$。
（d）画出此问题的图 VI.4，约束直线与代价圆相切。
（e）验证最小代价的导数为 $\dfrac{dF_{\min}}{db}=-\lambda$，并算出 $\dfrac{dF_{\min}}{db}=10b^{-1}$ 是否成立。

**2.** 在约束 $2x_1+x_2=5$ 下极小化 $F(x)=\tfrac12(x_1^2+4x_2^2)$。求出并解三个方程 $\partial L/\partial x_1=0$、$\partial L/\partial x_2=0$、$\partial L/\partial\lambda=0$。画出约束直线 $2x_1+x_2=5$ 与椭圆 $\tfrac12(x_1^2+4x_2^2)=F_{\min}$ 在极小点处相切的情形。

**3.** 第 1 题的鞍点矩阵是

```math
M=\begin{bmatrix}2&0&1\\0&2&3\\1&3&0\end{bmatrix}
```

用消元把 $M$ 约化为上三角矩阵 $U$，并验证右下角块为 $0=-A^TS^{-1}A$。$M$ 有多少个正主元？有多少个正特征值？

**4.** 对任意可逆对称矩阵 $S$，正主元的个数等于正特征值的个数。主元出现在 $S=LDL^T$（$L$ 为下三角）中，特征值出现在 $S=Q\Lambda Q^T$（$Q$ 正交）中。一个漂亮的证明是把 $L$ 和 $Q$ 连续地变形到 $I$ 或 $-I$，途中不经过奇异状态（见习题集 III.2）；特征值保持实数且不穿越零，因此它们在 $D$ 与 $\Lambda$ 中符号相同。试证明对任意 $2\times2$ 可逆对称矩阵 $S$ 的这条 “Law of Inertia（惯性定律）”：当 $S$ 有 0、1 或 2 个正主元时，它有 0、1 或 2 个正特征值。

1. 取 $LDL^T=Q\Lambda Q^T$ 的行列式，说明 $\det D$ 与 $\det\Lambda$ 同号。若行列式为负，则 $S$ 在 $\Lambda$ 中有一个正特征值、在 $D$ 中有一个正主元。
2. 若行列式为正，则 $S$ 可能正定也可能负定。证明当两个特征值都为正时，两个主元也都为正。

**5.** 求 $F(x)=\tfrac12(x_1^2+x_2^2+x_3^2)$ 在一条约束 $x_1+x_2+x_3=3$ 下的最小值；再加入一条约束 $x_1+2x_2+3x_3=12$ 后，求新的最小值。第二个最小值应小于第一个最小值，为什么？（第一个问题对应 $\mathbb{R}^3$ 中与球相切的一条直线；第二个问题对应与球相切的一个点。）

---

<!-- page 340 -->

### VI.3 Linear Programming, Game Theory, and Duality（线性规划、博弈论与对偶）

本节讨论高度结构化的优化问题。Linear programming（线性规划）先登场——线性代价与线性约束（含不等式）。它在历史上也是最先出现的：Dantzig 发明了 simplex algorithm（单纯形算法）来寻找最优解。我们这里的方法，是观察一个极小问题与一个极大问题之间的 “duality（对偶）”——两个线性规划被同时求解。

一条不等式约束 $x_k\ge 0$ 有两种状态——active（起作用的）与 inactive（不起作用的）。若极小化解最终落在 $x_k^{*}>0$，则该约束是不起作用的——它没有改变任何东西，其拉格朗日乘子满足 $\lambda_k=0$，最小代价不受这条关于 $x_k$ 的约束影响。但若约束 $x_k\ge 0$ 主动迫使最优的 $x^{*}$ 落在 $x_k^{*}=0$，则乘子满足 $\lambda_k>0$。于是最优性条件为：

```math
\lambda_k^{*}\,x_k^{*}=0 \qquad\text{对每个 }k
```

关于线性规划还有一点：它求解所有二人零和博弈（2-person zero-sum games）——一方的收益就是另一方的损失，最优策略产生一个 saddle point（鞍点）。

不等式约束在 quadratic programming（二次规划，QP）与 semidefinite programming（半正定规划，SDP）中依然存在。SDP 的约束涉及对称矩阵：不等式 $S\succeq 0$ 表示矩阵 positive semidefinite（半正定，或正定）。若最优的 $S$ 实际上是正定的，则约束 $S\succeq 0$ 并不起作用，此时拉格朗日乘子（现在也是一个矩阵）将为零。

#### Linear Programming（线性规划）

线性规划从代价向量 $c=(c_1,\dots,c_n)$ 出发。问题是要极小化代价 $F(x)=c^Tx$。约束是 $m$ 个线性方程 $Ax=b$ 和 $n$ 个不等式 $x_1\ge0,\dots,x_n\ge0$。我们写 $x\ge0$ 来涵盖全部 $n$ 个分量：

> **Linear Program（线性规划）**：在 $Ax=b$ 且 $x\ge0$ 下，极小化 $c^Tx$。 (1)

若 $A$ 是 $1\times3$ 的，$Ax=b$ 在三维空间中给出一个平面，如 $x_1+x_2+2x_3=4$。这个平面被约束 $x_1\ge0$、$x_2\ge0$、$x_3\ge0$ 切掉一部分，剩下平面上一个 triangle（三角形），其三个角（corner）在 $(x_1,x_2,x_3)=(4,0,0)$、$(0,4,0)$、$(0,0,2)$。我们的问题是找出这个三角形内使代价 $c^Tx$ 最小的点 $x^{*}$。因为代价是线性的，其最小值必在这些角中的某一个处达到。

线性规划必须找到那个最小代价角。当 $m$、$n$ 很大时，枚举所有角在指数意义上是不可行的。于是 simplex method（单纯形法）先找到一个满足 $Ax=b$ 且 $x\ge0$ 的起始角，然后沿约束集 $K$ 的一条边移动到另一个（代价更低的）角。代价 $c^Tx$ 在每一步都下降。找出最陡的边、以及这条边终止的下一个角，是一个线性代数问题。单纯形法从角到角地重复这一步骤很多次。

> <span style="color:#27ae60;">**译者注⑤｜$\lambda_kx_k=0$ 是“导数=零”的对偶说法（互补松弛）**：本节末尾转入 VI.3 的铺垫，其实是在把 VI.2 的等式约束结论推广到不等式。等式约束下乘子 $\lambda$ 可正可负，而加了 $x_k\ge0$ 之后，只有“把解顶在边界上”的约束才配拥有非零乘子，于是得到 complementary slackness（互补松弛）条件 $\lambda_k^{*}x_k^{*}=0$。它的机制仍是包络定理：$\lambda_k$ 度量的是“把边界 $x_k\ge0$ 放松一丁点能省多少代价”，若解本来就在内部（$x_k^{*}>0$），放松毫无收益，$\lambda_k=0$；若解被边界卡住（$x_k^{*}=0$），放松就能降代价，$\lambda_k>0$。这与 VI.2 的 $\dfrac{dF_{\min}}{db}=-\lambda$ 是同一个导数思想，也是理解线性规划对偶（dual variables）与 SDP 中“矩阵乘子”的关键。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 乘子为什么是「最小成本的导数」：**</span> 本节标题点明 Lagrange multiplier 就是 cost 的导数，这并非一句口号，而是乘子最本质的读法。把带约束的极小化问题写成 Lagrangian $L(c,\lambda)=F(c)+\lambda(a_1c_1+a_2c_2-b)$，其中 $b$ 是约束线的「水平」。若把最优成本 $F^*(b)$ 看成 $b$ 的函数，则一阶最优性条件给出的恰好是 $\mathrm{d}F^*/\mathrm{d}b=-\lambda^*$：约束每放松一个单位，最小成本按乘子的负值下降。这回答了一个自然的动机问题——乘子到底在度量什么？它度量的是「约束的边际价格」，即约束资源的稀缺程度。正文中的两维例子是最干净的示范：$F=\frac12(c_1^2+c_2^2)$ 在 $a_1c_1+a_2c_2=b$ 上取最小，代入解出 $c^*$ 后 $F^*=\frac{b^2}{2(a_1^2+a_2^2)}$，对 $b$ 求导恰得 $-\lambda^*$。正因为乘子携带了「放松约束能省多少成本」这一信息，正文才反复警告：引进并用完乘子后把它扔掉，是「一个很大的错误」。在工程上这个导数就是灵敏度（sensitivity），它让决策者知道该往哪个方向松弛约束才划算。

> <span style="color:#1e8449;">**[note] 最优解的闭式与 Schur complement：**</span> 从一维约束推广到 $m$ 个约束时，正文得到方程组（6）：$Sc+A\lambda=0$ 与 $A^Tc=b$。消去 $c$ 得 $c=-S^{-1}A\lambda$，代回即 $-A^TS^{-1}A\,\lambda=b$，于是 $\lambda^*=-(A^TS^{-1}A)^{-1}b$，$c^*=S^{-1}A(A^TS^{-1}A)^{-1}b$。这里出现的块 $A^TS^{-1}A$ 不是巧合：在分块矩阵 $M=\begin{bmatrix}S&A\\A^T&0\end{bmatrix}$ 上做一次消元，第二行减去第一行左乘 $A^TS^{-1}$ 后，右下角正是 $-A^TS^{-1}A$，这就是所谓的 Schur complement。这说明「乘子方程」与「KKT 矩阵的消元」是同一件事的两副面孔：前者直接解线性方程组，后者是把消元组织起来。而 $S$ 正定给出 $n$ 个正主元、$-A^TS^{-1}A$ 负定给出 $m$ 个负主元，主元符号的这组正负号正是 $L(c,\lambda)$ 在 $c$ 方向凸、在 $\lambda$ 方向凹的鞍点结构的代数印记——这也是下一小节讲 saddle point 时要用到的「Law of Inertia」的铺垫。

> <span style="color:#1e8449;">**[note] 与全书、与工程的联系及一个数值例子：**</span> 本节的模型远非抽象习题：当把线性微分方程离散化后，「带线性约束的二次型极小化」就是物理应用数学的中心问题。电路中 $A^TS^{-1}A$ 是导纳矩阵（conductance matrix），结构有限元里同一个块是刚度矩阵（stiffness matrix），最小二乘/线性回归中 $\Sigma$ 取协方差矩阵时 $A^T\Sigma^{-1}A$ 正是「除以方差 $\sigma^2$ 白化噪声」后的法方程系数。这些矩阵都对称正定，且通常约束是等式而非不等式，于是便有三种等价建模途径：解系统矩阵的线性方程、以电流/应力为未知量做极小化、以电压/位移为未知量做极大化——三者殊途同归。一个具体数值例子可看正文 Problem Set VI.2 的第 1 题：极小化 $F(c)=\frac12 c_1^2+\frac12 c_2^2$（原文 $-\frac12c_1^2+2c_2^2$ 疑为 OCR 之误），约束 $c_1+3c_2=b$，解得 $c_1^*=\frac{b}{10}$、$c_2^*=\frac{3b}{10}$、$\lambda^*=-\frac{b}{10}$，最小成本 $F^*=\frac{b^2}{20}$，而 $\mathrm{d}F^*/\mathrm{d}b=\frac{b}{10}=-\lambda^*$，与第一条注的结论完全吻合。最小二乘回归中乘子即残差与回归系数的关系、以及 $A^T\Sigma^{-1}A$ 正是参数协方差之逆，也都是同一块矩阵在不同领域换个名字而已。
