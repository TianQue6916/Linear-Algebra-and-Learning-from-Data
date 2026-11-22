# Linear Algebra and Learning From Data（线性代数与数据学习）· §IV.7

## 书页 249-254 ｜ PDF 页 251-256 ｜ Clustering by Spectral Methods and k-means（谱方法与 k-means 聚类）

> <span style="color:#7f8c8d;">本节是 §IV.7「Clustering by Spectral Methods and k-means（谱方法与 k-means 聚类）」。正文为 OCR 文本经数学公式还原后的双语译注：英文术语首次出现时附中文括注，之后保留英文；公式按上下文还原为 LaTeX，拿不准处标注待核。页眉（IV.7 Clustering by Spectral Methods and k-means）与印页码不译。原书图表处用 [[FIGURE: …]] 占位。</span>

---

<!-- page 251 -->
> <span style="color:#7f8c8d;">本页为书页 249，属 §IV.7 开头部分：承接 §I.10 的 Rayleigh quotient（瑞利商），引出第二特征向量、Fiedler vector（菲德勒向量）及其归一化约定，并给出 Example 1（20-node 图的 MATLAB 代码）。页眉与印页码不译。</span>

> <span style="color:#1e8449;">**[note] 为什么要在 Rayleigh quotient 里做 $c \to D^{-1/2}y$ 这个代换：**</span> 未经归一化的特征值问题 $A^{T}CAz = \lambda z$（$A$ 是 incidence matrix，$C$ 是权矩阵）在图上并不可靠——度数大的节点会主导特征向量。把变量换成 $y = D^{-1/2}z$（即 $z = D^{1/2}y$）后，原问题 $A^{T}CAz = \lambda Dz$ 就化成了对称的 $D^{-1/2}A^{T}CAD^{-1/2}\,y = \lambda y$。这正是在 §I.10 里见过的对称广义特征值问题，它的第二小特征值 $\lambda_2$ 对应的特征向量 $y$ 就是 Fiedler vector。归一化的好处是让每个节点的度数 $d_i$（进该节点的边权和）都"拉平"到同一尺度，从而改善聚类效果。这里用 Rayleigh quotient $y^{T}A^{T}CAy/y^{T}Dy$ 的极小值来"找到"这第二个特征向量，与直接解 $Lv = \lambda v$ 是同一件事，只是换了个求解视角。

0 (Section I. 10)。通过把 $x$ 换成 $D^{1/2}y$，Rayleigh quotient（瑞利商）将会找到第二个特征向量 $z$：

```math
\frac{y^{T}A^{T}CAy}{y^{T}Dy}
\ \xrightarrow{\ \text{same eigenvalue}\ }\ 
\min\ \frac{y^{T}A^{T}CAy}{y^{T}Dy} = \lambda_2
```

Fiedler（菲德勒）向量 $z = D^{-1/2}v$，且满足 $\mathbf{1}^{T}Dy = 0$：

```math
A^{T}CAz = \lambda_2 Dz \tag{11}
```

在 $Ay$ 中，incidence matrix（关联矩阵）$A$ 给出差分 $y_i - y_j$，而 $C$ 把每个差分量乘以权 $w_{ij}$。

Note：对某些作者，Fiedler vector $v$ 是 $A^{T}CA$ 的一个特征向量；我们更偏好 $D^{-1/2}v$。于是 $A^{T}CAz = \lambda_2 Dz$。实验似乎从 $v$ 和 $z$ 得到相似的聚类。那些 weighted degree（加权度数）$d_i$（进入节点 $i$ 的边权和）把普通的 $A^{T}CA$ 特征值问题做了归一化，以改善聚类。

> <span style="color:#1e8449;">**[note] Fiedler vector 的两种约定与为何选 $D^{-1/2}v$：**</span> 有些作者把 Fiedler vector $v$ 定义为 $A^{T}CA$ 的特征向量（即 $A^{T}CAv = \lambda_2 v$），而本书更偏好归一化版本 $z = D^{-1/2}v$，此时 $A^{T}CAz = \lambda_2 Dz$。两者对应的是同一个广义特征值问题，只是是否左乘 $D^{-1/2}$ 的差别，实验上从 $v$ 和 $z$ 得到的聚类往往相似。这里的关键在于：那些 weighted degree $d_i$（进入节点 $i$ 的边权和）把普通的 $A^{T}CA$ 特征值问题归一化，目的是改善聚类。直观上，度数差异悬殊的图若不归一化，高度数节点会把切割"拖"向自己；归一化后每个节点的贡献按度数平衡，切割边界才落在真正的稀疏处。

为什么我们要解一个特征值问题 $Lv = \lambda v$（通常代价高昂）来作为重排线性系统 $Ac = b$ 的第一步？一个回答是：我们并不需要一个精确的特征向量 $v$。一种"层次化"的 multilevel（多层）方法把节点合并起来，得到更小的 $L$ 和令人满意的 $v$。最快的 k-means 算法逐层 coarsen（粗化）图，然后在 refinement（细化）阶段调整粗聚类。

**Example 1** 一个 20-node 图有两个内置的簇 $P$ 和 $Q$（要从 $z$ 中找出来）。MATLAB 代码在 $P$ 内、$Q$ 内以概率 0.7 创建边；$P$ 与 $Q$ 之间的节点连边概率较小，为 0.1。所有边的权重 $w_{ij} = 1$，故 $C = I$。$P$ 和 $Q$ 从图上一目了然，但从它的 adjacency matrix（邻接矩阵）$W$ 上看不出来。

取 $G = A^{T}A$，特征值命令 `[V, E] = eig(G, D)` 解出 $A^{T}CAc = \lambda Dc$（原文此处 $c$ 应指特征向量，待核）。对 $\lambda$ 排序得到 $\lambda_2$ 及其 Fiedler vector $z$。Des Higham 的第三张图展示了 $z$ 的分量如何分成两簇（正负两组），从而给出一个好的重排。他提供了如下 MATLAB 代码。

```matlab
rand('state', 100)               % Generate 2N nodes in two clusters
for i = 1 : 2*N                  % rand repeats to give the same graph
  for j = i+1 : 2*N              % p = 0.1 when j-i is odd, 0.7 else
    p = 0.7 - 0.6 * mod(j-i, 2); % Insert edges with probability p
    w(i,j) = rand < p;           % The weights are W_ij = 1 (or zero)
  end
end                             % So far W is strictly upper triangular
W = W + W';                     % Adjacency matrix W, degrees in D
D = diag(sum(W));               % Eigenvalues of A^TCA = lambda Dc in E
[V, E] = eig(A'*A, D);          % Fiedler eigenvector z for ...
[a,b] = sort(diag(E)); z = V(:, b(2));
plot(sort(z), '.')              % Show + - groups of Fiedler components
```

> <span style="color:#1e8449;">**[note] 这段 MATLAB 代码的机制：$p$ 的表达式如何造出两个簇：**</span> `p = 0.7 - 0.6*mod(j-i,2)` 是精心设计的：当 $j-i$ 为偶数时 `mod(j-i,2)=0`，得 $p=0.7$；为奇数时 `mod(j-i,2)=1`，得 $p=0.1$。这样"下标同奇偶"的节点对之间以高概率 0.7 连边（对应同一簇内部），"下标异奇偶"的节点对之间以低概率 0.1 连边（对应跨簇），于是奇下标节点自然聚成 $P$、偶下标节点聚成 $Q$。代码先只填 $W$ 的严格上三角部分，再 `W = W + W'` 对称化得到邻接矩阵；`D = diag(sum(W))` 取每行和作为度数矩阵。最后 `[V,E] = eig(A'*A, D)` 解广义特征值问题 $A^{T}CAz = \lambda Dz$，取次小特征值对应的特征向量 $z$，`sort(z)` 后画图就能看到 $z$ 的分量分成正、负两组，据此划分两簇。

<!-- page 252 -->
> <span style="color:#7f8c8d;">本页为书页 250，属 §IV.7 中部：含三幅图（Graph、Adjacency matrix W、Reordered Matrix W 及 Fiedler components 图），随后进入 Application to Microarray Data（微阵列数据应用）。页眉与印页码不译。</span>

[[FIGURE: 书页 250, Graph（20 节点图，两个簇 P、Q 在图上明显分开）, 左栏上]]

[[FIGURE: 书页 250, Fiedler components（Fiedler 向量 z 的分量，取值分正负两组，对应两个簇）, 左栏下]]

[[FIGURE: 书页 250, Adjacency matrix W（20×20 邻接矩阵，nz = 142，非零元呈两个对角块）, 右栏上]]

[[FIGURE: 书页 250, Reordered Matrix W（按 z 重排后的邻接矩阵，nz = 142，两个对角块清晰分离）, 右栏下]]

## Special Matrices（特殊矩阵）

### Application to Microarray Data（微阵列数据应用）

Microarray（微阵列）数据是一个来自 $m$ 个基因、$n$ 个样本的矩阵 $M$。它的元素 $m_{ij}$ 记录基因 $i$ 在样本 $j$ 中的 activity（表达水平/活性）。$n \times n$ 的权重矩阵 $M^{T}M$ 度量样本（一个 complete graph〔完全图〕中的节点）之间的相似性。

$M^{T}M$ 的非对角元素进入 $W$。$W$ 的行和进入 $D$。于是 $D - W$ 就是 weighted Laplacian matrix（加权拉普拉斯矩阵）$A^{T}CA$。我们解 $A^{T}CAz = \lambda Dz$。

Higham、Kalna 和 Kibble 报告了在三个数据集上的测试。这些涉及 leukemia（白血病，$m = 5000$ 个基因、$n = 38$ 个患者）、brain tumors（脑瘤，$m = 7129$、$n = 40$）和 lymphoma（淋巴瘤）。

> "归一化的谱算法在揭示生物学相关信息方面远优于未归一化版本。"

实验还表明，Fiedler 之后的下一个特征向量如何帮助产生 $k = 3$ 个簇。$k$ 个最低特征值提供特征向量以识别 $k$ 个簇。

> <span style="color:#1e8449;">**[note] 为什么 $M^{T}M$ 度量样本相似、而 $D-W = A^{T}CA$ 是拉普拉斯矩阵：**</span> 微阵列矩阵 $M$ 是 $m\times n$（行=基因，列=样本），$M^{T}M$ 是 $n\times n$，其元素 $(M^{T}M)_{ij} = \sum_{k} m_{ki}m_{kj}$ 正是样本 $i$ 与 $j$ 在全部基因上的内积（表达谱的内积），所以它天然度量样本相似度。把它当作图的加权邻接矩阵 $W$，则度数 $d_i = \sum_j w_{ij}$ 就是 $W$ 的行和。对一般无向加权图，$A^{T}CA$ 恰好等于 $D - W$（$A$ 是 incidence matrix，$C$ 是边权对角阵）——这是图论里"拉普拉斯矩阵 = 度矩阵 − 邻接矩阵"的矩阵版。所以微阵列聚类最终落到解 $A^{T}CAz = \lambda Dz$，与 Example 1 用的是同一套谱聚类框架，只是这里的 $W$ 不再由 0/1 邻接关系给出，而是由表达谱内积连续取值给出。作者引用的结论"归一化优于未归一化"正是上一页归一化代换的价值所在。

<!-- page 253 -->
> <span style="color:#7f8c8d;">本页为书页 251，属 §IV.7：Cuts Connected to Eigenvectors（切割与特征向量的联系），建立 Ncut(P,Q) 与 Rayleigh quotient 的等价关系，并引入 Clustering by k-means（k-means 聚类）的基本问题。页眉与印页码不译。</span>

## Cuts Connected to Eigenvectors（切割与特征向量的联系）

图的切割把 $P$ 从 $Q$ 分开，它与 $A^{T}CAz = \lambda Dz$ 中的 Fiedler eigenvector 有何联系？关键的连接来自把 (5) 式中的 $\mathrm{Ncut}(P,Q)$ 与 (11) 式中的 Rayleigh quotient $y^{T}A^{T}CAy/y^{T}Dy$ 作比较。一个切割的完美 indicator（指示向量）应是一个所有分量只取 $p$ 或 $-q$（仅两个值）的向量 $y$：

> Two values（两个值）：节点 $i$ 若 $y_i = p$ 则归入 $P$；节点 $i$ 若 $y_i = -q$ 则归入 $Q$。

$\mathbf{1}^{T}Dy$ 会把一组 $d_i$ 乘以 $p$、另一组乘以 $-q$。第一组 $d_i$ 相加得到 $\mathrm{size}(P) = \sum w_{ij}$（$i \in P$）$= \sum d_i$（$i \in P$）。第二组 $d_i$ 相加得到 $\mathrm{size}(Q)$。约束 $\mathbf{1}^{T}Dy = 0$ 就变成 $p\,\mathrm{size}(P) = q\,\mathrm{size}(Q)$。

当我们把这个 $y$ 代入 Rayleigh quotient，正好得到 $\mathrm{Ncut}(P,Q)$！差分 $y_i - y_j$ 在 $P$ 内和 $Q$ 内都是零，跨切割处为 $p+q$：

```math
\text{分子：}\quad y^{T}A^{T}CAy = \sum \sum (y_i - y_j)^{2} = (p+q)^{2}\,\mathrm{links}(P,Q)
```

```math
\text{分母：}\quad y^{T}Dy = \frac{q}{p}\,\mathrm{size}(Q)\,(p+q)\,p = (p+q)\,q\,\mathrm{size}(Q) = p\,(p+q)\,\mathrm{size}(P)
```

最后一步用了 $p\,\mathrm{size}(P) = q\,\mathrm{size}(Q)$。在商中约去 $p+q$：

```math
\text{Rayleigh quotient} = \frac{(p+q)^{2}\,\mathrm{links}(P,Q)}{(p+q)\,q\,\mathrm{size}(Q)} = \frac{p\,\mathrm{links}(P,Q)}{p\,\mathrm{size}(P)} + \frac{q\,\mathrm{links}(P,Q)}{q\,\mathrm{size}(Q)} \tag{12}
```

```math
= \mathrm{Ncut}(P,Q) \tag{13}
```

```math
\mathrm{Ncut}(P,Q) = \frac{\mathrm{links}(P,Q)}{\mathrm{size}(P)} + \frac{\mathrm{links}(P,Q)}{\mathrm{size}(Q)} \tag{14}
```

Ncut 问题与特征值问题是同一个问题，只是额外加上了"$y$ 只有两个值"的约束。（这个问题是 NP-hard 的：$P$ 与 $Q$ 的选择实在太多。）Fiedler vector $z$ 不会满足这个双值条件，但在这个特别好的例子中它的分量清楚地分成了两组。如果能高效地实现，用 $z$ 聚类就是成功的。

> <span style="color:#1e8449;">**[note] 为什么"双值指示向量代入 Rayleigh quotient 恰得 Ncut"这条链是谱聚类成立的核心：**</span> 这段推导是全书谱聚类部分的枢纽。若允许 $y$ 取任意实数，$y^{T}A^{T}CAy/y^{T}Dy$ 的最小值就是 $\lambda_2$、取到它的是 Fiedler vector $z$；若限制 $y$ 只取 $p$ 与 $-q$ 两个值，则同一个 Rayleigh quotient 精确等于 Ncut。这意味着 **Ncut 的离散最优化是连续特征值问题的一个"离散约束版本"**——连续问题（可多项式时间求解）给出了离散问题（NP-hard）的一个连续松弛。把 Fiedler vector $z$ 的分量按正负切成两半，就是把这个松弛解"舍入"回一个切割，从而得到一个虽非全局最优但通常很好的近似切割。这正是"用第二特征向量做图二分"的数学依据：$z$ 的分量在 $P$ 内趋同、跨切割反号，符号就是簇标签。

## Clustering by k-means（k-means 聚类）

最基本的问题从 $d$ 维空间中的 $n$ 个点 $a_1, \dots, a_n$ 开始。目标是把这些点划分成 $k$ 个簇。簇 $P_1, \dots, P_k$ 有 centroid（质心）$c_1, \dots, c_k$。每个质心 $c$ 最小化到其簇内点 $a_j$ 的总距离 $\sum \|c - a_j\|^2$。质心就是那 $n_j$ 个点的 mean（均值/平均）：

```math
c_j = \frac{\sum a_i}{n_j}\ \text{（对其簇 } P_j \text{ 内所有 } a_i \text{ 求和，} n_j = |P_j| \text{）}
```

$c_j = \dfrac{\sum a}{n}$（簇 $P_j$ 内 $a$ 的均值）最小化 $\sum \|c - a\|^2$。

目标：找到划分 $P_1, \dots, P_k$，使得到质心的总距离 $D$ 最小：

```math
\text{Clustering（聚类）：}\quad \text{最小化}\ D = D_1 + \cdots + D_k = \sum_{j} \sum_{a_i \in P_j} \|c_j - a_i\|^2 \tag{15}
```

> <span style="color:#1e8449;">**[note] 为什么质心一定取均值、且总距离 $D$ 分解为 $D_1 + \cdots + D_k$：**</span> 对单个簇 $P_j$，$\sum_{a_i\in P_j}\|c - a_i\|^2$ 是 $c$ 的二次函数，求导令其为零得到 $\sum (c - a_i) = 0$，即 $c = \frac{1}{n_j}\sum a_i$——这正是算术平均，也是"最小二乘解是均值"这一结论。总距离 $D$ 之所以能按簇拆成 $D_1 + \cdots + D_k$，是因为每个点只属于一个簇、$\|c_j - a_i\|^2$ 只涉及它所属簇的质心，各簇项互不耦合。这个可加性正是 k-means 两步迭代能保证 $D$ 单调下降的基础：先固定划分优化质心（每个 $D_j$ 单独下降），再固定质心优化划分（每个点归到最近质心，$D$ 不增）。

<!-- page 254 -->
> <span style="color:#7f8c8d;">本页为书页 252，属 §IV.7：阐述 k-means 的 key idea（两步迭代）与收敛性，随后引入 Weights and the Kernel Method（加权与核方法）。页眉与印页码不译。</span>

## Special Matrices（特殊矩阵）

**Key idea（核心思想）** 把节点聚类成 $P_1, \dots, P_k$，会产生 $k$ 个质心（步骤 1）。每一组质心又产生一个聚类（步骤 2），其中 $a$ 若 $c_j$ 是离 $a$ 最近的质心，则 $a$ 移入 $P_j$。（若出现距离相等的质心，则任选其一。）

经典的 "batch k-means algorithm（批量 k-means 算法）" 从一个聚类迭代到它的质心、再到一个新的聚类。在式 (1) 中，这正是通过 alternating least squares（交替最小二乘）做的分解 $A = CR$！

> k-means（两步）：1. 求（旧）聚类 $P_1, \dots, P_k$ 的质心 $c_j$；2. 求（新）聚类——若 $c_j$ 是最近质心，则把 $a$ 放入 $P_j$。

每一步都减小总距离 $D$。我们为每个 $P_j$ 重置质心 $c_j$，然后围绕这些 $c_j$ 改进出新的 $P_j$。由于 $D$ 在两步中都下降，k-means 算法收敛。但它可能不收敛到全局最小值。

很难对极限簇了解太多。非最优划分可能给出局部极小值。更好的划分来自加权距离。

步骤 1 代价更高：要计算所有距离 $\|c_j - a_i\|^2$。复杂度通常每次迭代 $O(n^2)$。当算法稍后扩展为 kernel k-means（核 k-means）时，从数据生成 kernel matrix（核矩阵）$K$ 可能要 $O(n^2 d)$。

步骤 2 是寻找离每个质心最近的点集这一 "Voronoi（维诺）思想"。

> <span style="color:#1e8449;">**[note] k-means 与矩阵分解 $A = CR$ 为什么是同一件事：**</span> 把数据点排成矩阵 $A$ 的各行，把 $k$ 个质心排成 $C$ 的各行，$R$ 是一个 $k\times n$ 的 0/1 指示矩阵（每列恰有一个 1，表示该点属于哪个簇），则 $A \approx CR$：每个数据点被它所属簇的质心"代表"。k-means 的两步交替——固定 $R$ 求最优 $C$（取均值）、固定 $C$ 求最优 $R$（最近质心）——正是 alternating least squares（ALS）在秩-$k$ 分解 $A = CR$ 上的两个交替最小化子问题。这个对应解释了 k-means 的收敛性与"非凸、易陷局部极小"的根源：$A=CR$ 的秩约束最优化本身是非凸的，ALS 只保证目标不增并收敛到某个驻点，而非全局最优。

## Weights and the Kernel Method（加权与核方法）

当我们在距离中引入权重时，它们会出现在质心中：

```math
\text{质心 } c_j = \frac{\sum_{a_i \in P_j} w_i\, a_i}{\sum_{a_i \in P_j} w_i} \tag{16}
```

```math
\text{加权距离 } D_j = \sum_{a_i \in P_j} w_i\, \|c - a_i\|^2
```

加权距离 $D_j = \sum w_i\|c - a_i\|^2$（$a_i \in P_j$）在步骤 1 中由 $c = c_j$ 最小化。为减小总 $D = D_1 + \cdots + D_k$，步骤 2 重置各簇。每个 $a_i$ 归到最近的质心。然后迭代步骤 1（新质心）与步骤 2（新簇）。

一个关键点是：到质心的距离只需要点积 $a_i \cdot a_j$：

```math
\sum_{a_i \in P_j} \|c_j - a_i\|^2 = c_j \cdot c_j \sum_{a_i\in P_j} 1 - 2\,c_j \cdot \sum_{a_i\in P_j} a_i + \sum_{a_i\in P_j} a_i \cdot a_i \tag{17}
```

> <span style="color:#1e8449;">**[note] 为什么"到质心的距离只需点积"是核方法得以成立的前提：**</span> 把 $\|c_j - a_i\|^2$ 展开成 $c_j\cdot c_j - 2c_j\cdot a_i + a_i\cdot a_i$，三项都只依赖点积（内积）：$c_j$ 本身是 $a_i$ 的均值，故 $c_j\cdot c_j$、$c_j\cdot a_i$ 最终都化成 $a_i\cdot a_k$ 的组合。这意味着 k-means 全程无需知道 $a_i$ 的具体坐标，只要知道所有内积 $a_i\cdot a_j$ 组成的核矩阵 $K$ 即可。于是可以把 $a_i$ 换成任意 feature map $\phi(x_i)$ 在高维特征空间中的像——只要核 $K_{ij} = \phi(x_i)\cdot\phi(x_j)$ 能算，就无需显式构造 $\phi$。这就是 kernel trick（核技巧）在聚类里的应用：数据点可以不是空间中的真实位置，而只是"以自己规则"映射出的向量。

**Kernel method（核方法）** 加权核矩阵 $K$ 的元素是 $a_i \cdot a_j$。那些向量 $a_i$ 不必是空间中的真实位置。每个应用可以按自己的规则把图的节点线性或非线性地映射到向量 $a_i$。当节点是输入空间中的点 $x_i$ 时，它们的 representing vector（表示向量）$a_i = \phi(x_i)$ 可以是高维 feature space（特征空间）中的点。常用的核有三种：

| 领域 | 核 | 公式 |
|---|---|---|
| 视觉 | Polynomial（多项式） | $K_{ij} = (x_i \cdot x_j + c)^{d}$ |
| 统计 | Gaussian（高斯） | $K_{ij} = \exp\big(-\|x_i - x_j\|^2 / 2\sigma^2\big)$ |
| 神经网络 | Sigmoid | $K_{ij} = \tanh(c\,x_i \cdot x_j + \theta)$ |

(17) 式中的距离因为质心公式 (16)，只需核矩阵即可。

<!-- page 255 -->
> <span style="color:#7f8c8d;">本页为书页 253，属 §IV.7 结尾：给出核 k-means 的总距离公式 (18)，介绍两类加速途径（随机采样、Dhillon 的 graclus 多层聚类），并以 Applications of Clustering 的应用清单收尾。页眉与印页码不译。</span>

对 $P_j$ 中的节点求和：

```math
\sum_{a_i \in P_j} \|c_j - a_i\|^2 = \sum_{a_i \in P_j} K_{ii} - \frac{1}{n_j}\sum_{a_i, a_k \in P_j} K_{ik} + \sum_{a_i \in P_j} K_{ii} \tag{18}
```

（注：式 (18) 右端第 1、3 项依 OCR 原样均为 $\sum_{a_i \in P_j} K_{ii}$，可合并为 $2\sum K_{ii} - \frac{1}{n_j}\sum K_{ik}$；本书此处排版将 $+\sum K_{ii}$ 独立成行。公式结构与 (17) 一致：第一项对应 $c_j\cdot c_j$，第二项对应 $-2c_j\cdot a_i$，第三项对应 $a_i\cdot a_i$，均以核 $K_{ik} = a_i\cdot a_k$ 表示。此处 $a_k$ 遍历 $P_j$，待核。）

kernel batch k-means（核批量 k-means）算法用矩阵 $K$ 来计算这个总距离。

对大规模数据集，k-means 和 `eig(A'*C*A, D)` 都会很昂贵。这里有两种途径可生成一系列更易处理的问题。**Random sampling（随机采样）** 找到节点样本的最佳划分，用其质心按"归到最近质心"来划分所有节点。采样已成为一个重要研究方向，目标是证明以 high probability（高概率）得到的划分是好的。

Dhillon 的 graclus 代码使用 multilevel clustering（多层聚类）：先 graph coarsening（图粗化），再在底层聚类，最后 refinement（细化）。Coarsening 把节点合并成 supernode（超节点），边权求和。对于底层的 small supergraph（小超图），spectral clustering（谱聚类）或递归 2-means 都很快。这种多层途径类似于 algebraic multigrid（代数多重网格）。

## Applications of Clustering（聚类的应用）

这一节存在的理由是其应用极其广泛。这里是一份远超聚类的清单。应用数学的这一部分发展非常迅速。

1. 学习理论、训练集、神经网络、Hidden Markov Models（隐马尔可夫模型）
2. 分类、回归、模式识别、Support Vector Machines（支持向量机）
3. 统计学习、maximum likelihood（最大似然）、Bayesian statistics（贝叶斯统计）、spatial statistics（空间统计）、kriging（克里金法）、time series（时间序列）、ARMA 模型、平稳过程、预测
4. 社交网络、small world networks（小世界网络）、six degrees of separation（六度分隔）、组织理论、heavy tails（重尾）概率分布
5. 数据挖掘、document indexing（文档索引）、semantic indexing（语义索引）、word-document matrix（词-文档矩阵）、image retrieval（图像检索）、kernel-based learning（基于核的学习）、Nystrom method（尼斯特勒姆方法）、low rank approximation（低秩逼近）
6. 生物信息学、microarray data（微阵列数据）、systems biology（系统生物学）、protein homology detection（蛋白质同源性检测）
7. 化学信息学、drug design（药物设计）、ligand binding（配体结合）、pairwise similarity（两两相似度）、decision trees（决策树）
8. 信息论、vector quantization（向量量化）、rate distortion theory（率失真理论）、Bregman divergences（布雷格曼散度）
9. 图像分割、computer vision（计算机视觉）、texture（纹理）、min cut（最小割）、normalized cuts（归一化割）
10. Predictive control（预测控制）、feedback samples（反馈样本）、robotics（机器人学）、adaptive control（自适应控制）、Riccati equations（黎卡提方程）

<!-- page 256 -->
> <span style="color:#7f8c8d;">本页为书页 254，属 §IV.7 的 Problem Set（习题集）：共 11 题，前 7 题围绕 4-node 直线图与 k-means 的手算练习，第 8-11 题关于 5 个节点的图聚类与最小生成树。页眉与印页码不译。</span>

## Problem Set IV.7（习题集 IV.7）

**1.** 若图是一条 4 节点的线，且所有权重为 1（$C = I$），最佳切割是从中间切开。从 Fiedler vector $z$ 的 ± 分量找到这个切割：

```math
A^{T}CA z =
\begin{pmatrix}
1 & -1 & 0 & 0 \\
-1 & 2 & -1 & 0 \\
0 & -1 & 2 & -1 \\
0 & 0 & -1 & 1
\end{pmatrix}
z = \lambda_2 D z
,\quad
D = \operatorname{diag}(1, 2, 2, 1)
```

用手求出 $z$，并验证 $\mathbf{1}^{T}Dz = 0$。这里 $\lambda_2$（原文 OCR 作 `.X2`，应为此）为次小特征值。

**2.** 对同一个 4-node 树，计算从中间切开的 $\mathrm{links}(P)$、$\mathrm{size}(P)$ 和 $\mathrm{Ncut}(P,Q)$。

**3.** 从同样的四个点 $1, 2, 3, 4$ 出发，求簇 $P = \{1,2\}$ 与 $Q = \{3,4\}$ 的质心 $c_P$、$c_Q$ 与总距离 $D$。当 k-means 把四个点赋给最近质心时，$P$ 和 $Q$ 不会改变。

**4.** 以 $P = \{1,2,4\}$、$Q = \{3\}$ 启动 k-means 算法。求两个质心，并把点重新赋给最近质心。

**5.** 对簇 $P = \{1,2,3\}$ 与 $Q = \{4\}$，质心为 $c_P = 2$ 且 $c_Q = 4$。以错误的方式打破平局会留下这个无改进的划分，但请算出它的总距离 $D$。

**6.** 若图是一个 8 节点的 2×4 mesh（网格），权重 $C = I$，用 `eig(A'*A, D)` 求 Fiedler vector $z$。incidence matrix（关联矩阵）$A$ 是 10×8，且 $D = \operatorname{diag}(\operatorname{diag}(A^{T}A))$。$z$ 的 ± 分量会给出什么簇？

**7.** 用概率从 $p = 0.1$ 与 $0.7$ 收窄到 $p = 0.5$ 与 $0.6$ 运行 Fiedler 代码。计算 $z$ 并画出图及其划分。

**8-11 题**关于节点为 $(0,0), (1,0), (3,0), (0,4), (0,8)$ 的图。

**8.** 哪些簇 $P$ 与 $Q$ 最大化它们之间的最小距离 $D^{*}$？

**9.** 用 greedy algorithm（贪心算法）找到那些最佳簇。从五个簇开始，合并两个最近的簇。$k = 4, 3, 2$ 时各自的最佳 $k$ 簇是什么？

**10.** minimum spanning tree（最小生成树）是连接所有节点的最短边组。它将有 $n-1$ 条边且无环，否则总长度不会最小。**Dijkstra 算法**：从任一节点（如 $(0,0)$）开始。每一步，加入把新节点连到已建部分树的最短边。

**11.** 最小生成树也可由 greedy inclusion（贪心纳入）求得。把边按长度递增排序，保留每条边，除非它构成回路。
