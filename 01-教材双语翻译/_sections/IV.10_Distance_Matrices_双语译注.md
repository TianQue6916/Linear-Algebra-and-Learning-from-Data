# Linear Algebra and Learning From Data（线性代数与数据学习）· IV.10

## 书页 259-262 ｜ PDF 页 261-264 ｜ Distance Matrices（距离矩阵）

> <span style="color:#7f8c8d;">本节说明如何从一个只含"两两距离平方"的矩阵 $D$ 反推出点在空间中的位置 $X$，并引出多维尺度分析（MDS）与 Procrustes 对齐等经典算法。</span>

---

<!-- page 261 -->

> <span style="color:#7f8c8d;">本页为书页 259，属 IV.10 Distance Matrices（距离矩阵）的开篇，提出核心问题"能否从距离矩阵恢复位置"，并列举三类应用；页眉与印页码不译。</span>

### IV.10　Distance Matrices（距离矩阵）

假设有 $n$ 个点，其位置分别为 $x_1,\dots,x_n$（位于 $d$ 维空间中）。$n\times n$ 的 distance matrix（距离矩阵）$D$ 包含了每对点之间的 squared distances（距离的平方）$D_{ij}=\|x_i-x_j\|^2$。因此 $D$ 是 symmetric（对称的）。$D$ 的主对角线上都是零，因为 $\|x_i-x_i\|^2=0$。下面是从 $D$ 中提取信息的关键问题：

**能否从 Euclidean distance matrix（欧氏距离矩阵）$D$ 恢复出各点的位置 $x_1,\dots,x_n$？**

直接的答案是否定的。假设我们找到了一个解——一组可能的位置。那么我们可以把这组位置整体平移一个常向量 $c_0$，也可以用任意 orthogonal matrix（正交矩阵）去乘所有的 $x_i$。这些都属于 rigid motions（刚体运动），它们不会改变距离 $\|x_i-x_j\|$。认识到"一个解会引出一族等价解"之后，关键问题仍然成立（我们也回答了它）：

**是否总存在与距离矩阵 $D$ 相容的位置 $x_i$？是的。**

总存在一个 position matrix（位置矩阵）$X$（其列为 $x_1,\dots,x_n$），能产生 $D$ 中给定的这些距离。当点位于 $d$ 维空间时，矩阵 $X$ 有 $d$ 行（$d=2$ 对应一张地图，$d=3$ 对应我们的世界，$d>3$ 也允许且确实会发生）。问题之一就是确定最小的维数 $d$。

这个"从 $D$ 求 $X$"的问题由来已久。起初这纯粹是一个数学问题，但应用很快就出现了。我们只提其中三个：

1. **Wireless sensor networks（无线传感器网络）**：测量传感器两两之间的 travel times（传播时间）就得到 $D$，然后我们解出传感器的位置 $X$（即网络拓扑）。
2. **Shapes of molecules（分子形状）**：nuclear magnetic resonance（核磁共振）给出原子之间的距离，于是我们知道矩阵 $D$，再解出位置矩阵 $X$。这个例子以及许多其他例子都会涉及 noise（噪声，即 $D$ 中的误差），甚至 missing entries（缺失项）。
3. **Machine learning（机器学习）**：训练集中的样本被转换为高维空间中的 feature vectors（特征向量）。这些向量可能靠近某个维度低得多的平面或曲面。找到那个曲面（近似地）是理解数据、对新样本分类的一大步，然后 kernel trick（核技巧）会降低维度。这一过程同样可能处于非常嘈杂的环境中。

在准备本书这一节时，我们参考了一篇出色的论文 *"Euclidean Distance Matrices"*（欧氏距离矩阵），2015 年发布于 arXiv：1502.07541v2 [cs.OH]。作者是 Ivan Dokmanic、Reza Parhizkar、Juri Ranieri 和 Martin Vetterli。这篇论文充满思想、算法、代码和大量应用，讲解非常清楚！请到网上查找它以了解更多。

---

<!-- page 262 -->

> <span style="color:#7f8c8d;">本页为书页 260，属 IV.10 Distance Matrices（距离矩阵），给出把 $D$ 与 $G=X^TX$ 联系起来的关键恒等式，并从 $D$ 解出 $G$；页眉与印页码不译。</span>

### 由距离 $D$ 求位置 $X$（Positions $X$ from Distances $D$）

下面是一个简化问题的关键观察。它把 $D$ 中的每个（距离的平方）$\|x_i-x_j\|^2$ 与矩阵 $X^TX$（即所求向量 $x_i$ 与 $x_j$ 的 dot products（点积））中的四个元素联系起来：

```math
\|x_i-x_j\|^2 = \|x_i\|^2 - 2x_i^Tx_j + \|x_j\|^2
```
(1)

第一项产生一个"行恒定"的矩阵（不依赖 $j$）；最后一项 $\|x_j\|^2$ 产生一个"列恒定"的矩阵（不依赖 $i$）。这两个矩阵中位于主对角线上的数，就是 $\|x_i\|^2$ 与 $\|x_j\|^2$——即 $G=X^TX$ 中 column vector（列向量）$\operatorname{diag}(G)$ 里的那些数。

(1) 式中间的项 $-2x_i^Tx_j$ 恰好就是 $-2G$ 中的数。于是我们可以把 (1) 改写成关于矩阵 $D$ 的方程，用符号 $\mathbf{1}$ 表示由 $n$ 个 $1$ 组成的列向量。$\mathbf{1}$ 给出恒定的列，$\mathbf{1}^T$ 给出恒定的行：

```math
D = \mathbf{1}\,\operatorname{diag}(G)^T - 2G + \operatorname{diag}(G)\,\mathbf{1}^T
```
(2)

我们的问题是从 $D$ 恢复 $G$，然后位置 $X$ 就由 $X^TX=G$ 得出。你会发现，一个解 $X$ 可以右乘任意 orthogonal matrix（正交矩阵）$Q$，仍有 $(QX)^T(QX)=G$。由 $Q$ 带来的 rotations（旋转）是意料之中、被允许的。

解 $X^TX=G$ 求出这个 $d\times n$ 矩阵 $X$，就告诉我们这些点 $x_1,\dots,x_n$ 可以被放置在空间 $\mathbb{R}^d$ 中。$G$ 的 rank（秩）就是空间的维数——这是与给定距离矩阵 $D$ 相容的最小维数。

由于 (2) 式中有两项是 rank 1（秩一）矩阵，我们得知 $D$ 的秩至多为 $d+2$。注意，我们的所有点可以整体平移一个常向量而不改变 $D$ 中的距离平方，所以 $D$ 是一个 affine dimension（仿射维数，允许平移）而非 subspace dimension（子空间维数）。

现在解方程 (2) 求 $G=X^TX$。把第一个点放到原点：$x_1=0$。那么每个 $\|x_i-x_1\|^2$ 就只是 $\|x_i\|^2$。$D$ 的第一列 $d_1$（它是给定的）恰好等于 $\operatorname{diag}(X^TX)=\operatorname{diag}(G)=\big(\|x_1\|^2,\|x_2\|^2,\dots,\|x_n\|^2\big)$：

```math
\operatorname{diag}(G) = d_1 \quad\text{且}\quad \operatorname{diag}(G)\,\mathbf{1}^T = d_1\mathbf{1}^T
```
(3)

现在 $G$ 由 $D$ 得出。只要 $D$ 中的距离满足 triangle inequality（三角不等式）（参见 Menger: *Amer. J. Math.* 53; Schoenberg: *Annals Math.* 36），$G$ 就是 positive semidefinite（半正定）的：

```math
X^TX = G = -\tfrac12\big(D - d_1\mathbf{1}^T - \mathbf{1}d_1^T\big)
```
(4)

一旦知道 $G$，我们就能由 $X^TX=G$ 求出 $X$。对 $G$ 用 elimination（消元），或用它的 eigenvalues（特征值）与 eigenvectors（特征向量）。两者都给出一个满足 $x_1=0$ 的位置矩阵 $X$。

- 若 $G=Q\Lambda Q^T$（特征值与特征向量分解），则 $X$ 可取为 $\sqrt{\Lambda}\,Q^T$；
- 若 $G=U^TU$（消元 = Cholesky 分解），则 $X$ 可取为 $U$（upper triangular，上三角）。

两种情况下，我们在 $X$ 中都可以只保留 $\operatorname{rank}(G)$ 行。其余各行全为零，它们来自 $\Lambda$ 中的零特征值，或来自消元的提前终止。

---

<!-- page 263 -->

> <span style="color:#7f8c8d;">本页为书页 261，属 IV.10 Distance Matrices（距离矩阵），介绍 MDS 算法、中心化，以及用 Procrustes 问题对齐 anchor points（锚点），并给出习题 IV.10；页眉与印页码不译。</span>

我们把 $X$ 中的零行删去，就能看到这些点集 $x$ 的维数 $d$。

如果 $D$ 中的距离平方包含 measurement noise（测量噪声），就把小的特征值置为零。这就是经典的 MDS 算法：**MultiDimensional Scaling（多维尺度分析）**，其中第一个点 = 0。

### 中心化 $X$，或旋转以对齐锚点（Centering $X$ or Rotating to Match Anchor Points）

**Centering（中心化）**：通常我们更愿意把这些 $x$ 的 centroid（质心）放在原点。$x_1,\dots,x_n$ 的质心就是这些向量的平均：

```math
\text{Centroid} = \frac{1}{n}\sum_{i=1}^{n} x_i
```
(5)

只需把任意位置矩阵 $X$ 乘以矩阵 $I-\tfrac1n\mathbf{1}\mathbf{1}^T$，就能把质心放到原点。

**Anchor points（锚点）**：可能有一小部分位置是事先选定好的：把 $N$ 个锚点 $y_i$ 放进一个矩阵 $Y$。这些位置可能与算出的 $x_i$ 不一致。于是我们从算出的位置矩阵 $X$ 中挑出对应的 $N$ 列，再找出那个把这些列旋转到最接近 $Y$ 的正交矩阵 $Q$。

最优的正交矩阵 $Q$ 解的是 Section III.9 中的 Procrustes problem（普洛克路斯忒斯问题）。它由 singular value decomposition（奇异值分解）$X_NY^T=U\Sigma V^T$ 求得。把 $X_N$ 中的 $N$ 个位置移动到最接近 $Y$ 中锚点的正交矩阵是 $Q=VU^T$。

> J. C. Gower, *Properties of Euclidean and non-Euclidean distance matrices*, Linear Algebra and Its Applications **67** (1985) 81–97.

### 习题 IV.10（Problem set IV.10）

1. 若 $\|x_1-x_2\|^2=1$、$\|x_2-x_3\|^2=1$ 且 $\|x_1-x_3\|^2=6$，这组距离将违反 triangle inequality（三角不等式，因为 $1+1<6$）。构造 $G$ 并确认它不是半正定的：$G=X^TX$ 无解。

2. 若 $\|x_1-x_2\|^2=9$、$\|x_2-x_3\|^2=16$ 且 $\|x_1-x_3\|^2=25$，这组距离满足三角不等式 $3+4>5$。构造 $G$ 并找出与这些距离匹配的点 $x_1,x_2,x_3$。

3. 若对 $x_1,x_2,x_3,x_4$ 有 $\|x_i-x_j\|^2=1$（对一切 $i\neq j$），求 $G$ 进而求 $X$。这些点位于 $\mathbb{R}^d$ 中，$d$ 是多少？

---

<!-- page 264 -->

> <span style="color:#7f8c8d;">本页为书页 262，是第五部分 Probability and Statistics（概率与统计）的目录页，列出 V.1–V.6 各节标题，不属于 IV.10 正文；页眉与印页码不译。</span>

### Part V　Probability and Statistics（概率与统计）

- V.1　Mean, Variance, and Probability（均值、方差与概率）
- V.2　Probability Distributions（概率分布）
- V.3　Moments, Cumulants, and Inequalities of Statistics（矩、累积量与统计不等式）
- V.4　Covariance Matrices and Joint Probabilities（协方差矩阵与联合概率）
- V.5　Multivariate Gaussian and Weighted Least Squares（多元高斯与加权最小二乘）
- V.6　Markov Chains（马尔可夫链）

---

### 译者注

> <span style="color:#2e7d32;">**注 1｜为什么 (1) 式是理解本节全部的关键。** 距离 $\|x_i-x_j\|^2$ 本身是"非线性"的——它既含 $x_i$ 又含 $x_j$，还带平方。直接对 $D$ 做线性代数（求秩、求特征值）很难看出点的几何结构。作者的做法是把它拆成三项：$\|x_i\|^2$（只依赖 $i$）、$-2x_i^Tx_j$（同时依赖 $i,j$，且是 $X^TX$ 的线性元素）、$\|x_j\|^2$（只依赖 $j$）。这样一拆，$D$ 与"点积矩阵" $G=X^TX$ 之间的桥就搭起来了——因为 $G$ 正是承载一切线性几何信息的对象。**这一步本质上是"平方差展开"**（$a^2-2ab+b^2$），用线性化的手段把一个二次型的距离问题转成线性方程组，从而可以用熟悉的 Cholesky 分解或谱分解求解。这与 III 章里"从内积反推向量"的思路是同一件事：知道 $G$，就等于知道了点之间的全部相对位置（只差一个整体旋转/平移）。</span>

> <span style="color:#2e7d32;">**注 2｜为什么要"把第一个点放到原点"、以及平移自由度。** 距离矩阵 $D$ 只记录两两之差，天然丢失了整体位置信息：把所有点整体平移一个常向量 $c_0$，$D$ 完全不变。这意味着 $D$ 能确定的不是"点的绝对位置"，而是"点的相对构型"，也就是仿射意义下的形状（affine dimension，允许平移）。为了消除这个多余的自由度、让 $G$ 能被唯一解出，作者约定 $x_1=0$。于是 $D$ 的第一列 $d_1$ 就恰好等于 $\operatorname{diag}(G)$（因为 $\|x_i-x_1\|^2=\|x_i\|^2$），从而 (4) 式 $G=-\tfrac12(D-d_1\mathbf 1^T-\mathbf 1 d_1^T)$ 完全由已知的 $D$ 表出。**拿"已知的第一列"换"未知的对角线"**，这是整套推导里最关键的一次"以已知代未知"。而 $-\tfrac12$ 这个系数，正是 (1) 式中间项 $-2x_i^Tx_j$ 里的 $-2$ 解出来的：把 $D$ 里那份"交叉项"除以 $-2$，就还原出真正的点积 $G$。</span>

> <span style="color:#2e7d32;">**注 3｜"秩"在这里的几何含义：为什么 $D$ 的秩至多 $d+2$、$G$ 的秩等于维数。** $G=X^TX$ 是 $n\times n$，但它的秩至多等于 $X$ 的行数 $d$（因为 $G$ 是 $X$ 的列向量的 Gram 矩阵，秩 = 列空间维数 = 点的 span 维数）。所以 $\operatorname{rank}(G)=d$ 就是这些点实际张成空间的最小维数——这正是"从 $D$ 确定最小维数 $d$"的依据。再看 $D$：(2) 式里 $\mathbf 1\operatorname{diag}(G)^T$ 与 $\operatorname{diag}(G)\mathbf 1^T$ 都是秩一矩阵，$-2G$ 的秩至多 $d$，两项秩一矩阵至多再贡献 2 维（一个来自"行恒定"项、一个来自"列恒定"项）。因此 $\operatorname{rank}(D)\le d+2$。这解释了为什么距离矩阵"看起来"比点积矩阵高一两个维度——那多出来的 2 维正是平移（对应 $\mathbf 1$）与整体缩放/对角线信息（对应 $\operatorname{diag}(G)$）留下的痕迹，与注 2 里的仿射自由度是同一件事的两面。</span>

> <span style="color:#2e7d32;">**注 4｜半正定条件就是"三角不等式"，MDS 与 Procrustes 为什么成立。** (4) 式求出的 $G$ 未必半正定；$G\succeq 0$ 当且仅当 $D$ 的距离真的来自某个欧氏空间中的点集。数学上，这一等价由 Menger 与 Schoenberg 的经典结果给出：一组距离能嵌入欧氏空间，当且仅当相应的 $G$ 半正定。而"半正定"在几何上就对应"三角不等式成立"——两段距离之和必须不小于第三段。习题 1 正是反例：$1+1<6$ 违反三角不等式，算出的 $G$ 有负特征值，于是 $X$ 不存在。**MDS 的精髓在于**：当 $D$ 含噪声、$G$ 只是近似半正定时，把小的（甚至负的）特征值置零，只保留前 $d$ 个大的特征值，就得到"在最小二乘意义上最贴近 $D$"的低维构型——这正是降维/可视化的核心手段。而最后的 Procrustes 问题用 SVD 找最优旋转 $Q=VU^T$，与 III.9 节的"旋转对齐"完全一致：给定两组对应的锚点，$VU^T$ 是使 $\|X_NQ-Y\|_F$ 最小的正交矩阵。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么从 $D$ 求 $X$ 的“正确答案”不是唯一，而问题仍然“可解”：**</span> 本节的核心问题——从欧氏距离矩阵 $D$ 还原点的位置矩阵 $X$——初看像是一个“病态”问题：把全体点平移一个常数向量、再乘任意正交矩阵 $Q$，得到的 $(QX)(QX)^T = X^TX$ 不变，于是平方距离 $D$ 也完全不变。换句话说，$D$ 决定不了“绝对位置与绝对朝向”，只能决定“相对形状”。作者并不回避这一点，反而把它变成解题的钥匙：与其去求那个不存在的唯一 $X$，不如求一个**规范化的代表解**——把第一个点放到原点（$x_1=0$），于是第 1 列 $d_1$ 恰好就等于 $G$ 的对角元 $\mathrm{diag}(G)=(\|x_1\|^2,\dots,\|x_n\|^2)$。这一步把“平移自由度”冻结掉；剩下的旋转自由度本来就被 $Q$ 允许，因为任何 $X$ 与 $QX$ 都是合法答案。所以“存在性”问题（总有 $X$ 与 $D$ 一致）与“唯一性”问题（$X$ 不唯一，但形状唯一）被干净地分开：前者由 $G$ 的半正定性保证，后者由“刚性运动群”来描述。这正是 affine 维度（允许平移）而非子空间维度的含义所在。

> <span style="color:#1e8449;">**[note] 关键恒等式 $D = 1\,\mathrm{diag}(G)^T - 2G + \mathrm{diag}(G)\,1^T$ 在拿什么换什么：**</span> 展开 $\|x_i-x_j\|^2=\|x_i\|^2-2x_i^Tx_j+\|x_j\|^2$，得到三块：第一块 $\|x_i\|^2$ 只依赖 $i$，写成矩阵是“每行相同”的常数行，即 $1\,\mathrm{diag}(G)^T$；第三块 $\|x_j\|^2$ 只依赖 $j$，是“每列相同”的常数列，即 $\mathrm{diag}(G)\,1^T$；中间一块 $-2x_i^Tx_j$ 恰好就是 $-2G=-2X^TX$。于是 $D$ 被写成“两个秩 1 矩阵加一个 $-2G$”。这里真正的价值在于**可逆**：给定 $D$，用 $(3)$ 式 $G=-\tfrac12\big(d_1 1^T + 1 d_1^T - D\big)$ 就能把 $G$ 解回来。两个秩 1 项（常数行、常数列）所携带的信息，本质是“每个点的范数平方”，而它们与 $D$ 的交界处恰恰由对角元 $d_{11}=0$ 与第一列 $d_1$ 唯一确定。这也直接解释了“$D$ 的秩至多 $d+2$”：$-2G$ 的秩 $\le d$，再加两个秩 1 项，至多 $d+2$。

> <span style="color:#1e8449;">**[note] 半正定性与三角形不等式、以及经典 MDS 与 Cholesky 的联系：**</span> $G=X^TX$ 必须是半正定的，这对 $D$ 施加了约束，而该约束正是三角形不等式——这一点可追溯到 Menger（Amer. J. Math. 53）与 Schoenberg（Annals Math. 36）的工作，是“哪些距离矩阵能嵌入欧氏空间”的经典刻画。数值例子见习题 IV.10：若 $\|c_1-c_2\|^2=1$、$\|c_2-c_3\|^2=1$ 而 $\|c_1-c_3\|^2=6$，则边长 $1,1,\sqrt6$ 违反三角形不等式，此时按 $(4)$ 式构造出的 $G$ 非半正定，故 $G=X^TX$ 无解；反之 $\|c_1-c_2\|^2=9$、$\|c_2-c_3\|^2=16$、$\|c_1-c_3\|^2=25$ 对应 $3,4,5$，满足 $3+4>5$，可还原出三点。有了 $G$ 后，求 $X$ 有两条等价路径，正好对应书前半部分的两种分解：$G=Q\Lambda Q^T$ 取 $X=\sqrt{\Lambda}Q^T$（特征分解），或 $G=U^TU$ 取 $X=U$（消元即 Cholesky 分解，$U$ 上三角）；两者都能只保留 $\mathrm{rank}(G)$ 行，其余行因零特征值或消元提前结束而全为零，从而读出最小维度 $d$。带噪声时把小特征值置零，就是经典 MDS（MultiDimensional Scaling，多维标度）算法。
