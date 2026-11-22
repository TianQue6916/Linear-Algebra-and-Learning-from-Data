# Part IV（续）Special Matrices（特殊矩阵）· §IV.7–§IV.10

## 书页 249-262 ｜ PDF 页 251-264

---

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

---

> <span style="color:#7f8c8d;">本节把「补全一个秩一矩阵的缺失元」这个看似纯代数的问题，转译成图论中「行—列二分图是否构成 spanning tree（生成树）」的语言，从而给出一句干净的充要条件：唯一可补全当且仅当 $m+n-1$ 个给定元连成的边构成一棵生成树。</span>

---

<!-- page 257 -->

### IV.8 Completing Rank One Matrices（补全秩一矩阵）

给一个 rank-1 matrix（秩一矩阵）补上缺失元，这件事与「在图中能否找到（或找不到）cycle（回路）」直接相关。这套 rank-1 completion（秩一补全）理论，起源于下面这个问题：

> 在一个 $m\times n$ 矩阵 $A$ 中，我们给定 $m+n-1$ 个非零元。
> 何时要求 $\operatorname{rank}(A)=1$ 就能把其余所有元唯一确定？

答案取决于这 $m+n-1$ 个非零元的**位置**。下面看三个例子：

```math
A_1=\begin{bmatrix}x&x&x\\x&x&?\\x&?&?\end{bmatrix}\quad(\text{success 成功}),\qquad
A_2=\begin{bmatrix}x&x&?\\x&x&?\\?&?&?\end{bmatrix}\quad(\text{failure 失败}),\qquad
A_3=\begin{bmatrix}1&1&1\\1&1&1\\1&2&?\end{bmatrix}\quad(\text{failure 失败})
```

> <span style="color:#7f8c8d;">注：原书 OCR 中三个例子被压成片段，此处按上下文还原——$A_1$ 的第一列全给定（$x$），第二、三列只给首元，故可唯一补全；$A_2$ 给了左上 $2\times2$ 的四个元，成败取决于这四个元；$A_3$ 给了前 $3\times3$ 子阵中 $6$ 个元，多给定一个导致过约束。数学实质见下。</span>

在 $A_1$ 中，第一列（column 1）完全没有零元。若 $A$ 秩为 1，则第二、三列必须是第一列的倍数（multiples）。既然第二、三列的**首元**已给定，这两列就被完全确定了。

这是看 $A_1$ 的另一种思路。在任意秩一矩阵中，每个 $2\times2$ determinant（行列式）必为零。于是 $A_1$ 的 $(2,2)$ 元由 $a_{11}a_{22}=a_{12}a_{21}$ 这个等式决定。

在 $A_2$ 中，前四个元**可能不满足**「行列式 $=0$」这个条件。那样我们就注定失败（doomed to failure）。若那个行列式恰为零，我们便可任取第一列中某个 $a_{31}\neq 0$，把 $A_2$ 补全成秩一矩阵。这就是常见情形：**无解，或无穷多解**。

这个例子说明：只要一个 $2\times2$ 子阵的四个元全被给定，就可能失败。是不是**每次失败都这样发生**？不是——$A_3$ 就是另一种失败。

在 $A_3$ 中，那个前导 $3\times3$ 子阵给了**太多**给定元。它给了 $6$ 个元，而不是 $5$ 个（$m+n-1=3+3-1=5$）。对这 $6$ 个元的大多数取法，$3\times3$ 矩阵的秩为 1 是不可能的。例如

```math
\begin{bmatrix}1&1&1\\1&1&1\\1&1&2\end{bmatrix}\quad\text{的秩是 }2.
```

（此例实际算出：第一、二行完全相同，第三行 $=(1,1,2)$ 不能写成前两行的倍数——因为若 $(1,1,2)=k(1,1,1)$，则 $k=1$ 与 $2=1$ 矛盾——所以行空间维数是 $2$，秩为 $2$。）

### Spanning Trees in a Graph（图中的生成树）

Alex Postnikov 给出了看待这个 rank-1 completion 问题的正确方式。他构造一个图：用 $m$ 个节点对应 $m$ 行，$n$ 个节点对应 $n$ 列。对每个给定元 $A_{ij}$，图里就连一条边（edge），连接行节点 $i$ 与列节点 $j$。于是上面矩阵中 $x$ 的分布图案，就变成了它们行—列图（row-column graphs）中的边的图案（见下页）。

---

<!-- page 258 -->

$A_1$ 与 $A_3$ 两个例子产生了这样两张图：

[[FIGURE: 书页 256, $A_1$ 与 $A_3$ 的行—列二分图：左图 $A_1$ 的 5 条边连起 6 个节点成一棵树；右图 $A_3$ 的 7 条边在顶部 6 个节点间形成回路]]

这些是 bipartite graphs（二分图），因为它们所有的边都从一边连向另一边。$A_1$ 的成功与 $A_3$ 的失败，都能由这两张图解释。

**图 $A_1$** 这 $5$ 条边构成一棵 spanning tree（生成树）。说它是 tree（树），因为图里没有闭合环（没有 cycle）；说它 spanning（生成），因为它连通了全部 $6$ 个节点。若我们想求出 $A_1$ 的 $(3,3)$ 元（在秩一补全意义下），就加上那条虚线边，补成一个 cycle。于是 $A_{33}$ 由回路中的 $a_{11},a_{13},a_{31}$ 决定——这四个数凑出一个零行列式。

**图 $A_3$** 这 $7$ 条边**不**构成生成树。它不是树，因为（在顶部六条边里）存在一个 cycle。这个 cycle 对 $A_3$ 的那六个元施加了一个约束条件：

```math
\frac{a_{11}a_{22}a_{33}}{a_{12}a_{23}a_{31}}=1.
```

若 $A_3=uv^{T}$ 的秩为 1，其元必须满足这一等式。若该条件恰好成立，那么把 $A_3$ 补全成秩 1 的方式有无穷多种。

**Conclusion（结论）** 部分矩阵 $A$ 有唯一 rank-1 completion，当且仅当这 $m+n-1$ 个给定元 $A_{ij}$ 产生出 $m+n-1$ 条边（行 $i$ 到列 $j$），且这些边在行—列图中构成一棵 spanning tree——这棵树覆盖所有节点，且没有回路。

**Open problem（未解问题）** 可以指定 $A$ 中的哪些 $(m+n-2)^2$ 个元，从而允许唯一补全为一个 rank-2 matrix（秩二矩阵）？本书的 Appendix C（附录 C）确认了 $(m+n-2)^2$ 正是秩 2 矩阵独立参数的**正确个数**。

### Problem Set IV.8（习题集 IV.8）

1. 对示例矩阵 $A_2$，画出含 $3$ 个行节点与 $3$ 个列节点的二分图。$A_2$ 的 $5$ 条边是否构成一棵 spanning tree？
2. 构造一个 $5\times5$ 矩阵 $A_4$，其 $5+5-1=9$ 个非零元落在一个长度为 $8$ 的 cycle 上。
3. 要补全为一个 rank-1 矩阵，必须成立什么形如 $a_{11}a_{22}a_{33}=a_{12}a_{23}a_{31}$ 的等式？
4. 对一张有 $M$ 条边、$N$ 个节点的连通图，「spanning tree」这两个词各自对 $M$ 与 $N$ 提出什么要求？
5. 你如何知道一张有 $N$ 个节点、$N-1$ 条边的图是一棵 spanning tree？

---

> <span style="color:#7f8c8d;">译者注 1（为什么是 $m+n-1$，而不是别的数）：一棵 $m+n$ 个节点的树，恰好有 $m+n-1$ 条边——这是树的基本恒等式（节点数 $=$ 边数 $+1$）。所以 $m+n-1$ 这个给定元的个数不是随意选的：它正好等于「把所有行、列节点都连通、又不产生回路」所需的最少边数。给定元若少于这个数，图必不连通（有节点孤立），对应矩阵有自由度、无法唯一确定；给定元若多于这个数，图必含 cycle，而这个 cycle 就逼出一个行列式为零的约束条件，多数时候直接无解。这正是下节结论的算术来源。</span>

> <span style="color:#7f8c8d;">译者注 2（一个 cycle 凭什么「决定」一个未知元）：秩一矩阵的每个 $2\times2$ 行列式为零，等价于「相邻两列成比例」。若图中有回路，沿回路走一圈，比例系数首尾必须自洽，于是最后一个未知元被前几个元唯一锁定。反过来，若图中没有回路（是树），从任意一个非零元出发，沿树逐步「传播」比例关系，就能到达每个节点，且每个位置只被访问一次、不会发生冲突——这就是树能「唯一确定全部元」的机制。无解/无穷多解的根源，也在于「回路约束」与「树传播」这两种结构之争。</span>

> <span style="color:#7f8c8d;">译者注 3（与谱聚类/图 Laplacian 的暗合）：本节用图来编码矩阵的非零元位置，这个「行—列二分图」的 idea 在书的后半部分会反复出现——例如谱聚类里把数据看成图的节点、用边权衡量相似度，Laplacian matrix（拉普拉斯矩阵）的第二小特征值判定连通性。这里的 spanning tree 是「连通且无回路」的极值结构，而 Laplacian 的零特征值重数恰好等于图的连通分支数，二者是同一件事的代数面与组合面。理解了本节「回路=约束、树=唯一解」，对后面「图连通性决定可补全性/可分块性」会更顺。</span>

> <span style="color:#7f8c8d;">译者注 4（第 2 题的数值算例）：题 2 要一个 $5\times5$、$9$ 个非零元落在长度 8 的 cycle 上的矩阵。例如取 $A_4=(1,1,1,1,1)^{T}(1,1,1,1,1)$（全 1 矩阵，秩为 1），再沿一个 $8$ 元回路标记非零位置即可满足「9 个非零元构成 cycle」的结构要求；对应二分图中，$5$ 行节点与 $5$ 列节点连成一个 $8$ 边环，第 $9$ 条边则作为「弦」落到树之外、恰好逼出一个秩约束。这正是第 3 题那个等式要表达的：沿回路的奇数位置乘积 $=$ 偶数位置乘积。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么秩一补全的成败能用一个「生成树」来判定：**</span> 秩一矩阵的本质是 $A = uv^{\mathsf T}$，即所有列都是同一列 $u$ 的倍数、所有行都是同一行 $v^{\mathsf T}$ 的倍数。于是给定 $m+n-1$ 个非零元之后，能不能唯一地把其余位置补出来，取决于这些已知元是否在「行—列」之间形成了一条不会自相矛盾的链。把 $m$ 个行当作 $m$ 个节点、$n$ 个列当作 $n$ 个节点，每个给定元 $A_{ij}$ 画一条从行节点 $i$ 到列节点 $j$ 的边，就得到一个二分图（bipartite graph）。若这些边恰好连成树，则任意两个节点之间只有唯一一条路径——这意味着从任意一个已知元出发，沿着这条唯一路径不断用「两列成比例」把未知元逐一推出，每一步都没有歧义，故补全是唯一的。反之，若图里出现了环（cycle），环上每个节点的值就受到一条约束方程的牵制，多给一个元就多一个要满足的条件；一旦环上的已知元不满足这个条件，就无解，满足时又因为少了一个约束而得到无穷多解。所以「$m+n-1$ 条边是否构成生成树（spanning tree）」这一纯图论条件，精确刻画了秩一补全「唯一可补」的边界，这正是 Alex Postnikov 引入图的动机所在。

> <span style="color:#1e8449;">**[note] 环条件 $A_{11}A_{22}A_{33}=A_{12}A_{23}A_{31}$ 的来源：**</span> 这一节里反复出现的等式，其实只是「$2\times2$ 子式为零」在任意长度环上的推广。秩一矩阵 $A=uv^{\mathsf T}$ 有一个基本特征：任意 $2\times2$ 子式
>
> ```math
> \det\begin{pmatrix} A_{ij} & A_{ik}\\ A_{lj} & A_{lk}\end{pmatrix}
> = A_{ij}A_{lk}-A_{ik}A_{lj} = u_i v_j u_l v_k - u_i v_k u_l v_j = 0
> ```
>
> 把 $A_{ij}=u_i v_j$ 代入，$u_i u_l v_j v_k$ 与 $u_i u_l v_k v_j$ 完全抵消，故每一对「行 $i,l$、列 $j,k$」形成的子式必为零。若把这些已知元按环 $A_{11}\to A_{13}\to A_{23}\to A_{22}\to A_{21}\to A_{31}$（对应 $u_1 v_1, u_1 v_3, u_2 v_3, u_2 v_2, u_2 v_1, u_3 v_1$）排列，逐个消去公共的 $u_i$、$v_j$ 因子，就得到环上乘积相等：$A_{11}A_{22}A_{33} = A_{12}A_{23}A_{31}$。它其实是把「两个行乘以两个列」的 $2\times2$ 条件沿环「转了一圈」后所得的循环乘积恒等式。对一个 $3\times3$ 的 $A$，若已知其 6 个元构成这样一个环，这个等式就是补全到秩一之前必须满足的一致性条件（consistency condition）：它不成立则无解，成立则因少一个约束而有无穷多解。

> <span style="color:#1e8449;">**[note] 与附录 C 及前文的联系——参数个数的呼应：**</span> 本节结论中「$m+n-1$ 个给定元对应一个生成树」与全书反复出现的「秩一矩阵的自由参数个数」是同一件事的两面。秩一矩阵 $A=uv^{\mathsf T}$ 中 $u\in\mathbb{R}^m$、$v\in\mathbb{R}^n$ 一共给出 $m+n$ 个参数，但把 $u$ 乘一个非零常数、$v$ 除以同一常数并不改变 $A$，故真正的自由度是 $m+n-1$——这正是生成树边数的来源，也是本节「给定 $m+n-1$ 个元」这一假设的来历。举一个具体数值例子：$A_1$ 的第一列已知为 $u=(1,2,3)^{\mathsf T}$，若第 2、3 列的首元分别是 $4$、$5$，则由「各列是 $u$ 的倍数」立刻得到 $v^{\mathsf T}=(1,4,5)$，于是 $A_3$ 的 $(3,3)$ 元 $A_{33}=u_3 v_3=3\cdot5=15$ 被唯一确定——这正是图中由生成树补上虚线边、闭合成一个环后，用 $A_{11},A_{13},A_{31}$ 推出 $A_{33}$ 的过程。文末把此推广到秩二，问「哪些 $(m+n-2)^2$ 个元可唯一补成一个秩二矩阵」，其数目 $mn$ 中的自由参数 $(m+n-2)^2$ 同样出自秩二矩阵 $A=UV^{\mathsf T}$（$U\in\mathbb{R}^{m\times2}$、$V\in\mathbb{R}^{n\times2}$）在列变换 $GL(2)$ 下的不变性，附录 C 将给出这一计数的确认。

---

> <span style="color:#7f8c8d;">本节说明：IV.9 用 SVD 解决一个「用正交矩阵 $Q$ 把一组向量 $y$ 尽量旋转到另一组向量 $x$」的经典问题（正交 Procrustes 问题）。核心结论是 $Q = V^T U$（由 $Y^T X = U\Sigma V^T$ 得到）最小化 $\|X - YQ\|_F$，并给出基于 trace（迹）性质的完整证明。末尾附一组习题。</span>

---

<!-- page 259 -->

> <span style="color:#7f8c8d;">本页为书页 257，属 IV.9 正交 Procrustes 问题的引言、神话背景、求解步骤与证明的三个小引理；页眉与印页码不译。</span>

IV.9 正交 Procrustes 问题

下面是 SVD 一个漂亮（而且实用）的应用。它从两组向量 $x_1,\dots,x_n$ 与 $y_1,\dots,y_n$ 出发：哪个 orthogonal matrix（正交矩阵）$Q$ 去乘那些 $y$，能让结果尽可能靠近那些 $x$？这个问题在数量惊人地多的应用中都会出现。

注意这里的限制是只允许一个正交矩阵 $Q$。这不包含平移，也不包含放缩。若 $y$ 各向量的 mean（均值）等于 $x$ 各向量的均值，就无需平移；否则大多数程序会先减去这些均值，从而得到新的 $x$ 与 $y$，满足 $\sum x_i = \sum y_i = \mathbf{0}$（零向量）。这样两组向量就都被居中（centered）、均值为零了。而如果我们事先允许对向量做 rescaling（重新放缩）来把它们的长度先拉平，那就得到所谓「generalized Procrustes problem（广义 Procrustes 问题）」。

我得给你讲讲 Procrustes 与那段神话。Procrustes 本人正是以放缩闻名。他邀请过路的陌生人到他那张特制的床上舒舒服服睡一晚，声称这张床会自己调整长度去适配来客。可真相是：Procrustes 调整的是来客的长度，好让客人去适配那张床。（矮个子客人被放到刑架上拉长，高个子客人被砍掉双腿。我不确定这神话透露出希腊人的什么，但肯定不是什么好事。）Theseus 迎难而上，把 Procrustes 反过来「调整」去适配他自己的床——结果不幸致命。

他们解决了广义问题，而我们解决标准问题：正交的 $Q$。

**解法：**
1. 构造矩阵 $X$ 与 $Y$，其列分别是 $x_1,\dots,x_n$ 与 $y_1,\dots,y_n$；
2. 形成方阵 $Y^T X$；
3. 求奇异值分解 $Y^T X = U\Sigma V^T$；
4. 正交矩阵 $Q = V^T U$ 最小化 $\|X - YQ\|_F$。

**Discussion（讨论）**

第 $k$ 列与 $Y$ 的第 $k$ 列 $y_k Q$ 之间的距离，就是通常的 Euclidean length（欧氏长度）$\|x_k - y_k Q\|$。对于「所有 $x$ 到所有 $yQ$」的（平方）距离，很自然的做法是把这些列长度平方加起来。这就得到（平方）Frobenius norm（Frobenius 范数）$\|X - YQ\|_F^2$。我们必须证明第 4 步的 $Q = V^T U$ 使这个范数最小——它是最优的 $Q$。

证明中有三个小观察会有帮助：

(i) 平方 Frobenius 范数 $\|A\|_F^2$ 是 $A^T A$ 的 trace（迹）。
(ii) $A^T B$ 的迹等于 $B^T A$ 的迹，也等于 $BA^T$ 的迹。
(iii) 平方范数与 $\|AQ\|_F^2$、$\|A^T\|_F^2$ 相同。

---

<!-- page 260 -->

> <span style="color:#7f8c8d;">本页为书页 258，属 IV.9 正文，解释三个观察并给出 $Q = V^T U$ 最小化 $\|X - YQ\|_F^2$ 的完整证明，随后交代历史出处与一组习题；页眉与印页码不译。</span>

方阵的 trace（迹）是主对角线上各元素之和，它同时也是各 eigenvalue（特征值）之和。于是上面三个观察就很好解释了：

(i) $A^T A$ 的对角元素是各列的平方长度——所以它们加起来等于 $\|A\|_F^2$。
(ii) $A^T B$ 与其转置 $B^T A$ 有相同的对角——因此有相同的迹。$A^T B$ 与 $BA^T$ 有相同的非零特征值。它们的对角包含了全部 $a^T b$ 的内积。
(iii) $AQ$ 与 $A$ 有相同的列长度，因为 $Q$ 是正交矩阵。$\|A\|_F^2$ 与 $\|A^T\|_F^2$ 都把 $A$ 所有元素的平方加起来，所以二者相等。

**证明 $Q = V^T U$ 是使 $\|X - YQ\|_F^2$ 最小的正交矩阵**

我们要最小化

```math
\operatorname{trace}\big((X - YQ)^T (X - YQ)\big)
= \operatorname{trace}(X^T X) + \operatorname{trace}(Y^T Y) - 2\,\operatorname{trace}(Q^T Y^T X).
```

$X^T X$ 与 $Y^T Y$ 是固定的，所以我们要最大化最后那一项 trace。这正是引入 $Y^T X = U\Sigma V^T$ 的时刻：

```math
\operatorname{trace}(Q^T Y^T X)
= \operatorname{trace}(Q^T U \Sigma V^T)
= \operatorname{trace}(V^T Q^T U \Sigma)
= \operatorname{trace}(Z\Sigma). \tag{1}
```

矩阵 $Z = V^T Q^T U$ 是若干正交矩阵的乘积，因而也是正交矩阵。$\Sigma$ 是由正数 $\sigma_1,\dots,\sigma_r$ 构成的对角矩阵。于是矩阵 $Z\Sigma$ 的迹是 $z_{11}\sigma_1 + \cdots + z_{rr}\sigma_r$。要使这个数最大化，最佳选择是 $Z = I$（此时 $z_{ii}=1$ 全部取到，迹达到 $\sum_i \sigma_i$）。

由 $Z = V^T Q^T U = I$ 即得 $Q = U V^T$，这就解决了 Procrustes 问题。

在原来的 $X$ 与 $Y$ 是正交矩阵的情形，要得到零误差（$X - YQ$ 为零）的完美旋转，$Q = Y^T X$ 显然成立。这与答案 $Q = U V^T$ 一致：正交矩阵的奇异值全为 $1$，所以式 (1) 中的分解 $Y^T X = U\Sigma V^T$ 恰为 $U V^T$（即 $\Sigma = I$）。

**Notes（注）**

Procrustes 问题最初在 Schönemann 1964 年的博士论文中解决。Gower 与 Dijksterhuis 的《Procrustes Problems》（Oxford University Press, 2004）展开了它的许多应用。我们上面借用的证明取自 Golub 与 Van Loan（《Matrix Computations》第 4 版，第 328 页）。那一页还开启了 SVD 在子空间夹角问题上的一批重要应用。

**Problem Set IV.9（习题 IV.9）**

1. 哪个正交矩阵 $Q$ 最小化 $\|X - YQ\|_F$？分别用上面的解 $Q = UV^T$，以及把该范数当作 $\theta$ 的函数来最小化（令对 $\theta$ 的导数为零）两种方法：

```math
Q =
\begin{pmatrix}
\cos\theta & -\sin\theta \\[2pt]
\sin\theta & \cos\theta
\end{pmatrix}.
```

---

> <span style="color:#27ae60;">【译者注 1】为什么用「正交矩阵」而非任意矩阵？这正是本问题的精髓。若允许 $Q$ 是任意矩阵，那么「把 $Y$ 旋转/变形去靠近 $X$」就退化为普通的最小二乘，解就是伪逆，几乎等于直接解 $YQ \approx X$，太「自由」、太平凡。限定 $Q$ 为正交，等于要求变换只做**旋转（可能带反射）**，保持每列的欧氏长度不变、保持列间的内积不变。这对应一个极其常见的实际设定：两组点云代表同一个刚体在不同姿态下的坐标，你只被允许整体旋转对齐，不能拉伸或剪切。所以正交 Procrustes 问题几乎就是「刚体配准 / 点云对齐（point-set registration）」的数学内核，也是后来 Kabsch 算法、ICP 迭代最近点算法乃至结构生物学、计算机视觉中姿态估计的共同基础。</span>

> <span style="color:#27ae60;">【译者注 2】关键的一步是 $\operatorname{trace}(V^T Q^T U \Sigma) = \operatorname{trace}(Z\Sigma)$，以及「$Z$ 是正交矩阵」。为什么正交的 $Z$ 在对角矩阵 $\Sigma$ 面前只能靠 $Z=I$ 取到最大迹？看 $Z\Sigma$ 的对角元：第 $i$ 个是 $z_{ii}\sigma_i$。因为 $Z$ 正交，它的每个列向量是单位向量，故每个对角元 $|z_{ii}|\le 1$（这是 Cauchy–Schwarz 直接给的：$\sum_j z_{ji}^2 = 1$ 蕴含 $z_{ii}^2 \le 1$）。于是 $z_{ii}\sigma_i \le \sigma_i$，且要全部同时取等，必须 $z_{ii}=1$ 对每个 $i$ 成立，再结合正交性迫使所有非对角元为 $0$，即 $Z=I$。这就是「拿一项一项的乘积求和，用正交性把每一项都压到上界」的典型最优化手法——和 IV.7 里用奇异值上下界、以及凸组合求极值时「放缩系数和为 1 时线性项在端点取到」是同一件事：都是把目标函数写成 $\sum_i c_i z_i$ 的形式，再逐项求极大。</span>

> <span style="color:#27ae60;">【译者注 3】三个观察中，(i) 是「Frobenius 范数 = 迹」这一桥梁的由来：$\|A\|_F^2 = \sum_{i,j} a_{ij}^2 = \operatorname{trace}(A^T A)$。它把「距离平方」这个几何量翻译成了「迹」这个可线性拆分的代数量，于是原问题 $\|X-YQ\|_F^2$ 展开后能把不含 $Q$ 的两项 $\operatorname{trace}(X^T X)$、$\operatorname{trace}(Y^T Y)$ 直接丢掉，问题浓缩成最大化一项 $\operatorname{trace}(Q^T Y^T X)$。(ii) 的 $\operatorname{trace}(A^T B)=\operatorname{trace}(BA^T)$ 靠的是迹的循环不变性 $\operatorname{trace}(AB)=\operatorname{trace}(BA)$。这两个「小观察」其实都是迹的循环置换性质，是让 SVD 能「穿」进 trace 里、把 $Q$ 单独挤到 $Z$ 位置的关键。末尾「正交矩阵奇异值全为 1」的特例，也正是本页习题 1 用 $\theta$ 求导能得到与 $Q=UV^T$ 一致答案的原因——二维旋转矩阵本身就是正交矩阵，两种解法殊途同归。</span>

> <span style="color:#27ae60;">【译者注 4】「Procrustes」一词后来在统计学里演化成一个更广的比喻——Procrustes analysis（Procrustes 分析）泛指「把一组形状/构型通过平移、旋转、放缩对齐到另一组，再比较形状差异」的方法族，这正是神话里「把来客削足适履塞进床」的数学化身。标准正交 Procrustes 问题只允许旋转（本页情形）；广义 Procrustes 问题再加放缩与平移，对应「相似变换」。读者若往后接触主成分对齐、形状分析（shape analysis，如 Bookstein 坐标）、或机器学习里对嵌入/表征做旋转对齐（如 ICA、去相关、衡量两个词向量空间是否一致），本质上都是同一个 $Q = V^T U$ 的解在起作用。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么必须限定正交矩阵 $Q$：**</span> 这个问题的全部价值都押在「$Q$ 正交」这一条上。Procrustes 神话里床只允许调整长度（伸缩），而数学里我们只允许旋转与反射——不许平移、不许缩放。为什么偏偏要这么苛刻？因为一旦放开成任意矩阵 $A$，问题立刻退化为平凡的最小二乘：$\|X-YA\|_F$ 对 $A$ 求导置零，直接得到 $A=(Y^TY)^{-1}Y^TX$（伪逆解），SVD 根本用不上。正是「$Q^TQ=I$」这个非线性约束，让解不再是一个显式线性系统，而变成一个约束优化问题，SVD 才成为那把合适的钥匙。同时这个约束本身是有物理/几何意义的：正交变换保持长度与夹角，所以它描述的是刚体旋转（rigid rotation）——这正是计算机视觉里点集配准（point-set registration）、因子分析里旋转载荷（rotate loadings）、分子构象对齐等场景共同的需求：我们只想「转」一组点去对齐另一组，而不是把它任意拉扯变形。正交限制还顺带解决了解的唯一性困境：若 $Y^TX$ 的奇异值有重根，$U,V$ 有自由度，但 $Q=V^TU$ 可能不唯一，此时通常再用 $\det Q=+1$ 排除反射、强制取真正的旋转。所以「正交」既是对问题做了合理瘦身，也是让解有意义的前提。

> <span style="color:#1e8449;">**[note] $\operatorname{trace}(Q^TY^TX)=\operatorname{trace}(Z\Sigma)$ 这条不等式在拿什么换什么：**</span> 证明的核心是一处「迹的不变性 + 正交性收拢」的代换。先把目标展开为 $\|X-YQ\|_F^2=\operatorname{trace}(X^TX)+\operatorname{trace}(Y^TY)-2\operatorname{trace}(Q^TY^TX)$，前两项不含 $Q$，所以极小化目标等价于极大化 $\operatorname{trace}(Q^TY^TX)$。代入 $Y^TX=U\Sigma V^T$，令 $Z=V^TQ^TU$：因为 $V,U,Q$ 全正交，$Z$ 也正交；而 $\Sigma$ 是对角阵 $\operatorname{diag}(\sigma_1,\dots,\sigma_r)$，于是由迹的循环性质 $\operatorname{trace}(Q^TU\Sigma V^T)=\operatorname{trace}(V^TQ^TU\,\Sigma)=\operatorname{trace}(Z\Sigma)=\sum_{i} z_{ii}\sigma_i$。这里就出现了关键的不等式：对正交矩阵 $Z$，其对角元满足 $|z_{ii}|\le 1$（每行模长为 $1$），而 $\sigma_i\ge 0$，所以 $\sum z_{ii}\sigma_i\le\sum\sigma_i$，等号当且仅当 $z_{ii}=1$（对所有 $i$）时取到。由于正交矩阵对角元全为 $1$ 只能是对角元为 $\pm1$ 的对角阵，而取 $\pm1$ 只会让对应项变号（不增加和），故最优是 $Z=I$，即 $V^TQ^TU=I\Rightarrow Q=UV^T$。一句话：这条式子把「在所有正交矩阵里找最大」这个抽象问题，收拢成了「一个正交矩阵的对角元被奇异值加权求和」的有限问题，$Z=I$ 的自然最优性一眼可见——这就是 SVD 在这里的威力，它把 $Q$ 与 $Y^TX$ 的关系解耦成了对 $\Sigma$ 的对角加权。

> <span style="color:#1e8449;">**[note] 与 §IV.7（$2$-范数下 SVD 的极小秩近似）是同一件事的两种范数：**</span> 若读者已读过 §IV.7 关于 SVD 给出矩阵最佳低秩近似的讨论（$\min_{\operatorname{rank}(B)\le k}\|A-B\|=\sigma_{k+1}$），会发现 Procrustes 解与其同源。二者都是「在约束族里找一个矩阵，使它与给定矩阵的某种范数距离最小」：Procrustes 问题可重述为 $\min_{Q^TQ=I}\|Y^TX-Q\|$ 的某种等价形式——把「旋转 $Q$ 去贴合」翻译成「用正交矩阵族去逼近 $Y^TX$」。区别只在于所用的范数与约束：低秩近似用 $\sigma_1\ge\sigma_2\ge\dots$ 截断来逼近（谱范数意义），而 Procrustes 是在正交群 $\mathrm{O}(n)$ 上、用 Frobenius 范数做投影，答案是「把 $Y^TX$ 的奇异值全部替换成 $1$，再还原」——即 $Q=UIV^T=UV^T$。这揭示了一个漂亮的直觉：对任何矩阵，它到正交群的最近点就是「抹掉奇异值大小、只保留左右奇异方向」所得的矩阵，因为正交矩阵的奇异值全是 $1$。具体数值例：设 $Y^TX=\begin{pmatrix}2&0\\0&\frac12\end{pmatrix}$，其 SVD 本身就是 $U=V=I,\Sigma=\operatorname{diag}(2,\frac12)$，于是最优旋转 $Q=UV^T=I$；而若 $Y^TX=\begin{pmatrix}0&3\\0&0\end{pmatrix}$（秩 $1$），SVD 为 $U=I,\ V=\begin{pmatrix}0&1\\1&0\end{pmatrix}$，则 $Q=UV^T=\begin{pmatrix}0&1\\1&0\end{pmatrix}$，恰是把坐标轴对调的旋转——即把秩亏的方向「掰正」过来。这些例子说明 $Q$ 只取决于奇异向量的方向，与奇异值的大小无关。

---

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
