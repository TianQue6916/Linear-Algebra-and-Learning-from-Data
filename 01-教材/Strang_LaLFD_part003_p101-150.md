# Gilbert Strang《Linear Algebra and Learning From Data》part003 双语翻译

> <span style="color:#7f8c8d;">**范围**：书页 96–146（OCR 页 101–150，共 50 页）。§I.12 Factoring Matrices and Tensors（尾部）→ Part II Computations with Large Matrices（§II.1–§II.4）。
> **格式**：行内双语（中文主体 + English term（中文翻译）行内嵌入），习题题干保留英文原文。
> **页映射**：page_101–115 = 书页 96–110（偏移 −5）；page_116 = 书页 111（Part II 章首页）；page_117–150 = 书页 113–146（偏移 −4）。
> **本合并文件由 50 个分页文件拼合而成**，每页以 `<!-- page NNN -->` 注释起始，页间以 `---` 分隔；如需单页请查阅 `pages/page_NNN.bilingual.md`。</span>

---

<!-- page 101: 书页 96, Problem Set 1.11（习题集 1.11，保留英文原文） -->

> <span style="color:#7f8c8d;">本页为 **Problem Set 1.11（习题集 1.11）**（对应 §I.11 Norms of Vectors and Functions and Matrices，向量、函数与矩阵的范数）。本页为纯习题页，共 12 题：题干按习题页规范**保留英文原文，不译成中文**，仅补结构标签与题号；OCR 乱码已按数学上下文修正为 LaTeX（范数符号 $\|v\|_p$、$\|A\|_F$、Hölder 不等式等），修正处以绿色译者注标出。</span>

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.** Show directly this fact about $\ell^1$ and $\ell^2$ and $\ell^\infty$ vector norms: $\|v\|_2^2 \le \|v\|_1\,\|v\|_\infty$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "Show directly thi s fact about 1 an d and vector norms ： |@腭 孓 日 训 丨 1 鬱"，$\ell^p$ 记号与范数杠全部丢失；右端不等式按 $\|v\|_2^2 = \sum_i |v_i|^2 \le (\max_i |v_i|)\,\sum_i |v_i| = \|v\|_1\|v\|_\infty$ 重建。此题同时收录于 MIT OCW 18.065 Lecture 8 "Problems from Section I.11" 第 1 题，措辞与之一致。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.** Prove the Cauchy-Schwarz inequality $|v^Tw| \le \|v\|_2\,\|w\|_2$ for vectors in $\mathbb{R}^n$. You could verify and use this identity for a length squared:

```math
0 \le \left\|v - \frac{v^Tw}{w^Tw}\,w\right\|_2^2 = \|v\|_2^2 - \frac{|v^Tw|^2}{\|w\|_2^2}.
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 提示句残作 "You could verify an d use this identity for a length squared ： / 0 < 鬱 一"；恒等式左端残缺，按 Cauchy-Schwarz 的标准证明（考察 $v$ 减去其在 $w$ 上投影后剩下的正交残差的长度平方）重建为 $\left\|v - \frac{v^Tw}{w^Tw}w\right\|^2$。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.** Show that always $\|v\|_2 \le \sqrt{n}\,\|v\|_\infty$. Also $\|v\|_1 \le \sqrt{n}\,\|v\|_2$, by choosing a suitable vector $w$ and applying the Cauchy-Schwarz inequality.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "Show that always 日 可 2 孓 日 · Also 目 1 孓 和 目 2 by choosing a suitable vector 慟 an d applying the Cauchy-Schwarz inequality"，第一式的下标、$\sqrt{n}$ 与 $\|v\|_\infty$ 均被打碎；按常见解法重建：第二式取符号向量 $w = (\mathrm{sign}(v_1), \dots, \mathrm{sign}(v_n))$，则 $\|v\|_1 = |v^Tw| \le \|v\|_2\|w\|_2 = \sqrt{n}\,\|v\|_2$。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.** The $\ell^p$ and $\ell^q$ vector norms are dual if $1/p + 1/q = 1$ (and $p = 2$ is self-dual). Hölder's inequality extends Cauchy-Schwarz to all those dual pairs. What does it say for $p = 1$ and $q = \infty$?

```math
\text{Hölder's inequality:} \qquad |v^Tw| \le \|v\|_p\,\|w\|_q \quad \text{when } \frac{1}{p} + \frac{1}{q} = 1 .
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 题干残作 "1 · The 1 and vector norms / The an d norms are ... dual (and 2 is self-dual) · Hölder's inequality extends Cauchy-Schwarz to all those dual pairs · Wh at does it say for p = 1 an d q = ？"，$\ell^p$、$\ell^q$ 与 $1/p+1/q=1$ 按语境补全；下方公式残作 "IvTwI 孓 / HöIder's inequality / 丨 目 q when p¯ + q"，拼合重建如上。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.** What rules should be satisfied by any "inner product" of vectors $v$ and $w$?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 句首 "Wh at" 与引号内词 OCR 残缺（残作 "at rule s should be satisfied by any “ ” “ d 况 ' ' 0f vectors 鬱 and ？"）；引号内名词按 §I.11 语境与常见解答（列出 $(v,v) \ge 0$、$(v,w) = (w,v)$ 等内积规则）重建为 "inner product"。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.** The first page of I.11 shows unit balls for the $\ell^1$, $\ell^2$, and $\ell^\infty$ norms. Those are the three sets of vectors $v = (v_1, v_2)$ with $\|v\|_1 \le 1$, $\|v\|_2 \le 1$, $\|v\|_\infty \le 1$. Unit balls are always convex because every vector norm obeys the triangle inequality: if $\|v\| \le 1$ and $\|w\| \le 1$, show that $\left\|\frac{v}{2} + \frac{w}{2}\right\| \le 1$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "The first page of I. 1 1 shows 刀 方 ba for the an d and Z00 norms. Those are th e three sets Of vectors ... with 目 1 1 ， 日 2 孓 1 ， 孓 / U ba lls are lways convex because & eq 五 r vector norms ： / If 和 日 孓 1 and 日 1 show th at 腭 + 可 目 孓 1"：unit balls、$\|v\|_p$ 集合与凸性问句均按语境重建（凸性即 $\frac{v}{2}+\frac{w}{2}$ 仍在范数球内）。此处引用的 "first page of I.11"（§I.11 开篇的 unit ball 图）见本册前页译文。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.** A short proof of $\|AB\|_F \le \|A\|_F\,\|B\|_F$ starts from multiplying rows times columns:

```math
|(AB)_{ij}|^2 \le \|\text{row } i \text{ of } A\|_2^2 \;\|\text{column } j \text{ of } B\|_2^2
```

is the Cauchy-Schwarz inequality. Add up both sides over all $i$ and $j$ to show that $\|AB\|_F^2 \le \|A\|_F^2\,\|B\|_F^2$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此题同时收录于 OCW Lecture 8 的 "Problems from Section I.11" 第 7 题，措辞与其一致；OCR 残作 "A short pro of of 丨 丨 孓 目 starts from multiplying row s time s columns：/ 区 B ） 万 丨 2 孓 llrow of 丨 2 目 column of | | 2 ..."，公式中的行/列范数按语境取 2 范数。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.** Test $\|AB\|_F \le \|A\|_F\,\|B\|_F$ for $A = B = I$ and for $A = B =$ the $n$ by $n$ "all ones matrix".

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "Test B 孓 日 驯 F 個 for = B = and = B = "all ones matnx"，两个被测试矩阵按 §I.11 习题惯例（先取 $A = B = I$，再取全 1 矩阵）补全，尺寸 "n by n" 在 OCR 中丢失（常见解答中记为 $N \times N$）。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 9 (Conjecture).** The only matrices with $\|AB\|_F = \|A\|_F\,\|B\|_F$ and no zero entries have the rank one form $A = uv^T$ and $B = u w^T$ with a shared vector $u$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 这是一道 (Conjecture)（猜想）题。OCR 残作 "(ConJecture) Th e only matrices wi th 丨 B 目 / F = 日 驯 F 日 B 陆 and no zero entries / have the rank one = and B = 鬱 with a shared vector 鬱"：加号与范数竖杠在 OCR 中缺失，无法区分 $\|AB\|_F$ 与 $\|A + B\|_F$——按与 Problem 8（Frobenius 范数次可乘性 $\|AB\|_F \le \|A\|_F\|B\|_F$）的连贯性，重建为次可乘取等（等式情形）猜想，rank-one 形式与 "shared vector $u$" 按残句语义重建；该猜想题在公开解答集中亦标注未解，确切措辞请以原书为准。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.** The space of $m$ by $n$ matrices with the Frobenius norm is actually a Hilbert space—it has an inner product $(A, B) = \operatorname{trace}(A^TB)$. Show that $\|A\|_F^2 = (A, A)$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "The space of m by matrices with the Frobenius norm is actually a Hilbert space—— it has an inner product （ 蓋 ， B) = trace(ATB) · Show 山 at 日 日 = （ 蓋 ， 蓋 ） ·"，矩阵尺寸的第二维 "$n$" 与目标式 $\|A\|_F^2$ 的下标、平方在 OCR 中丢失，按 $\|A\|_F^2 = \sum_{i,j} a_{ij}^2 = \operatorname{trace}(A^TA)$ 补全。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 11.** Why is (21) a true formula for $\|A\|_\infty$? Which $x$ with $\pm 1$'s has $\|Ax\|_\infty = \|A\|_\infty$?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 式 (21) 见 §I.11 正文：$\|A\|_\infty = \max_{\|x\|_\infty = 1}\|Ax\|_\infty$（$A$ 的最大行 1 范数）；其最优 $x$ 取 $\pm 1$ 分量，使各元素按最大行所在行 $i^*$ 的符号 $x_j = \operatorname{sign}(a_{i^*j})$ 对齐。OCR 中向量名（残作 "Which 鬱 with ±l's has ..."）按语境用 $x$。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 12.** Suppose $A$, $B$, and $AB$ are $m$ by $n$, $n$ by $p$, and $m$ by $p$. The "max norm" of $A$ is $\|A\|_{\max} = \max_{i,j}|a_{ij}|$. Show that $\|AB\|_{\max} \le n\,\|A\|_{\max}\,\|B\|_{\max}$ (this is false without the factor $n$). Rewrite that in the form

```math
\sqrt{mp}\;\|AB\|_{\max} \;\le\; \sqrt{mn}\;\|A\|_{\max} \;\cdot\; \sqrt{np}\;\|B\|_{\max}
```

The rescaling by those square roots gives a true matrix norm.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 题干残作 "SUPP0se ， B, and AB are m by by and m by P. The "medical no 皿 ” of ... / Show that 田 蓋 B 日 应 孓 田 日 田 B 日 应 (this is false without the factor / Rewrite that in the 皿 （ 丨 IIA 应 ） 孓 （ - 田 驯 应 ） （ 田 B 目 囤 / The rescaling by 山 0 se square roots gives a true matrix norm"："max norm"（最大范数，正文 §I.11 已定义 $\|A\|_{\max}=\max|a_{ij}|$）被误读为 "medical no 皿"，尺寸 $n$ by $p$ 与 $m$ by $p$ 的 "$n$""$p$" 丢失，两处不等式按"先证含因子 $n$ 的界、再重写为带平方根的等价形式"重建；未经缩放的 $\|AB\|_{\max} \le \|A\|_{\max}\|B\|_{\max}$ 对 max norm 不成立，这正是 "false without the factor" 的含义。

---

<!-- page 102: 书页 97, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文） -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.12 Factoring Matrices and Tensors: Positive and Sparse（矩阵与张量的分解：非负与稀疏）</span>

本节开启了关于 data matrices（数据矩阵）的 factorizations（分解）的一个更广阔的视野，

而且这一视野还会进一步延伸到 tensors（张量）。

到目前为止，我们把全部注意力都放在奇异值分解（SVD）$A = U\Sigma V^T$ 上，

它为 Principal Component Analysis（PCA，主成分分析）提供了完美的因子（perfect factors）。

这种"完美"会一直持续下去，直到 sparseness（稀疏性）、nonnegativity（非负性）或 tensor data（张量数据）进入问题为止；

而对许多 applications（应用）来说，正是这些问题至关重要。

因此我们必须把 SVD 看成第一步（first step），而不是最后一句话（not the last word）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 末句在 OCR 中残作 "but 叻 e 忉 叩"，按上下文（"把 SVD 当作第一步，后续还有更多分解形式"）重建为 "but not the last word"。

下面是对 $A$ 的几种 factorizations（分解），它们带有新的重要性质：

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span> 这一小节的呈现方式是把"目标 + 约束"浓缩成并列的公式；OCR 中的三行小标题 Nonnegative Matrices、Sparse and Nonnegative、CP Tensor Decomposition 原为并列的三组分解，具体排版无法从 OCR 恢复，译文按"名称 + 优化问题"列表给出。
>
> 这个列表是同一个模板的三次填表：先定 loss（损失函数），再定 feasible set（可行域）或 penalty（惩罚项），然后求两者之和最小的 factor（因子）。三行并列，是因为骨架相同、只换了约束的形状。
>
> 先问 SVD（奇异值分解）凭什么给出 perfect factors（完美因子）。依据是 Eckart-Young 定理：rank（秩）不超过 r 的 matrix（矩阵）里，截断的前 r 个 singular triple（奇异三元组）使平方 residual（残差）最小，最小值等于第 r+1 到末尾的 singular value（奇异值）平方和。证明只用一句话：最优点处 residual（残差）与候选集合垂直。而垂直要有意义，集合必须容纳任意方向的扰动，即必须是 linear subspace（线性子空间）。问题恰在这里：rank（秩）不超过 r 的 matrix（矩阵）不构成子空间，两个 rank（秩）为 r 的 matrix（矩阵）相加，rank（秩）可以变成 2r，它只是一张曲面。Eckart-Young 还能成立，是无约束时切空间允许任意符号，垂直条件退化成 eigenvalue equation（特征值方程）。
>
> 换成 nonnegative orthant（非负象限）后，要求 $U \ge 0$、$V \ge 0$，允许的扰动少了一半，垂直条件不再是 eigenvalue equation（特征值方程），而变成"residual（残差）与每个可行方向的内积不超过零"，即 projection（投影）到 convex set（凸集）上的判据：最优点通常落在边界上，factor（因子）里出现真正的零。把 feasible set（可行域）换成 $\ell_1$ penalty（惩罚项），就是第二行公式。
>
> 精细处在于约束并非每步都咬人。对 $A \ge 0$ 和固定的 $v \ge 0$，无约束 least squares（最小二乘）解 $u = Av/(v^{T}v)$ 自动非负。代入数字：取第一行 $v = (1,1,0,0)^{T}$，得 $Av = (2,1,0,1)^{T}$、$v^{T}v = 2$，于是 $u = (1,0.5,0,0.5)^{T}$，四个分量无需截断。正文说"半迭代很快，因为它实际上是线性的"，含义就在这里：固定一个 factor（因子）后双线性退化为普通 least squares（最小二乘），代价不在单步，而在项数 r 变大后的边界结构。
>
> 代价可以算。取 $M$ 四行为 $(1,1,0,0)$、$(0,1,1,0)$、$(0,0,1,1)$、$(1,0,0,1)$：第一行加第三行等于第二行加第四行，rank（秩）为 3；singular value（奇异值）为 $2$、$\sqrt2$、$\sqrt2$、$0$，三项 SVD（奇异值分解）精确复原，平方 residual（残差）为 0。但项数为 3 的 nonnegative（非负）factorization（分解）达不到 0，且不必用优化器证明：nonnegative rank-one term（非负秩一项）$uv^{T}$ 的非零位置是 supp(u) 与 supp(v) 的乘积，即 bipartite graph（二部图）里的一个 rectangle（矩形）；$M$ 的非零位置连成八条边的环，每个顶点度数为 2，任何矩形最多盖 2 条边，盖满 8 条至少要 4 个矩形，四个星形恰好够。故 boolean rank（布尔秩）为 4，而 nonnegative rank（非负秩）不低于它。
>
> 数值复核：投影梯度求三项非负逼近，30 组随机初值里最好的一组把平方 residual（残差）压到约 0.586，对应 residual（残差）约 0.765，到不了 0；无约束情形的平方 residual（残差）为 0。这个差额是结构性的，换优化器只省时间，省不掉它。
>
> 跨课程连接之一，6.042J 图论：把 support（支撑）看成 bipartite graph（二部图）的边集，全一矩形就是 complete bipartite subgraph（完全二部子图），"最少矩形覆盖"即 biclique cover（完全二部子图覆盖），下界同样靠数边除以块容量。区别是图论只问盖不盖得住，matrix（矩阵）还要问数值逼得多近，所以 boolean rank（布尔秩）只是 nonnegative rank（非负秩）的下界。
>
> 连接之二，概率论与凸优化：$\ell_1$ penalty（惩罚项）换成概率语言就是先验，噪声取 Gaussian（高斯）、entry（元素）取 Laplace（拉普拉斯分布）时，负对数后验正好是平方 loss（损失函数）加绝对值之和。不用"数非零个数"，是因为它连 norm（范数）都不是：homogeneity（齐次性）失效，$x$ 只有一个非零分量时 $2x$ 的非零个数仍是 1，不等于 2 倍。$\ell_1$ 是单位球上与它一致的最紧 convex function（凸函数），于是成为可算替身。
>
> 连接之三，CSAPP 浮点：支撑论证依赖"恰好为零"，而 floating point（浮点数）里本该为 0 的位置常落在 $10^{-17}$，用 `==` 判零会算错 boolean rank（布尔秩），与比较浮点须写差值小于阈值是同一条纪律；落码前先定 threshold（阈值）。
>
> 最后是第三行：三路 tensor（张量）的 CP decomposition（CP 张量分解）把 $A \approx UV$ 换成三张 factor（因子）表相乘，alternating least squares（交替最小二乘）形状不变，但 SVD（奇异值分解）时代的两条保证同时失效：没有精确的低项数分解，tensor rank（张量秩）也不再受尺寸限制，可以超过每个 mode（模态）长度。一句话收束：三组公式的差别不在项数，而在 feasible set（可行域）的形状；集合一旦不是 linear subspace（线性子空间），最优性就从 eigenvalue equation（特征值方程）退化为边界上的 projection（投影）问题。

- **Nonnegative Matrices（非负矩阵）**：在 $U \ge 0$、$V \ge 0$ 的约束下，

```math
\min_{U,V} \|A - UV\|_F^2
```

- **Sparse and Nonnegative（稀疏且非负）**：在 $U \ge 0$、$V \ge 0$ 的约束下，

```math
\min_{U,V} \left( \|A - UV\|_F^2 + \lambda\,\|UV\|_1 \right)
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 正则项在 OCR 中残作 "XIIUVIIN"，

> 此处按稀疏非负分解的常见写法重建为 $\lambda\|UV\|_1$（若原书为 $\|U\|_1$、$\|V\|_1$ 之和或核范数项，请以原书为准）。

- **CP Tensor Decomposition（CP 张量分解，CANDECOMP/PARAFAC）**：把三路张量（three-way tensor）近似为 rank-one tensors（秩一张量）之和。

> <span style="color:#1e8449;">**[note] 译者注:**</span> 本页此处仅给出该分解的名称，具体公式在后续页展开。

我们先处理 matrices（矩阵），再处理 tensors（张量）；

一个 matrix（矩阵）不过是一个 two-way tensor（二路张量）。

为了计算分解 $A \approx UV$，我们引入一个简单的 alternating iteration（交替迭代）：

先固定 $V$ 去更新 $U$，再固定 $U$ 去更新 $V$。

每一步半迭代（half step）都很快，因为它实际上是线性的——另一个因子在这半步中被固定住了。

如果把对角矩阵（diagonal matrix）$\Sigma$ 也包括进来，这个想法同样适用于普通的 SVD。

这个算法简单，而且常常有效；§III.4 会做得更好。

> <span style="color:#7f8c8d;">（交叉引用：OCR 原写作 "Section 111.4"，按上下文判读为 Section III.4。）</span>

这个 $UV$ 的想法也契合著名的 k-means algorithm（k 均值算法），后者出现在关于 graphs（图）的 §IV.7 中。

那里的问题，是要把向量 $a_1, \dots, a_k$ 划分进 $r$ 个 clusters（簇）$C_1, \dots, C_r$。

若 $a_k$ 落在围绕 $u_j$ 的那个簇中，则 $V$ 的第 $k$ 列就是 $r \times r$ 单位矩阵（identity matrix）的第 $j$ 列。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此段 OCR 损伤最重（残作 "The problem is tO put vec tors 01, · · · , 和 0k e e c 况 况 m UV. Then column of V is column j 0f the r by r identity matrix."）。

> 按 k-means 与 NMF 的对应关系重建：数据向量 $a_k$ 各指派给 $r$ 个簇质心 $u_j$ 之一，指示矩阵 $V$ 的第 $k$ 列为单位阵的第 $j$ 列（即 $V_{kj} = 1$ 当且仅当 $a_k \in C_j$），从而 $A \approx UV$ 中的 $V$ 承担"硬指派"的角色。

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">Nonnegative Matrix Factorization (NMF)（非负矩阵分解）</span>

非负矩阵分解（NMF，Nonnegative Matrix Factorization）的目标，是用两个非负矩阵的低秩乘积 $UV$ 去逼近一个非负矩阵 $A \ge 0$，

其中要求 $U \ge 0$ 且 $V \ge 0$。

采用 lower rank（低秩）是为了 simplicity（简单）；

采用 nonnegativity（非负性，即没有负元素）是为了产生有意义的数。

于是 features（特征）无需通过正负抵消（plus-minus cancellation）就能辨认出来。

一个为负的 weight（权重）、volume（体积）、count（计数）或 probability（概率），从一开始就是错的。

但非负性可能是难以满足的：

当 $A \ge 0$ 是 symmetric positive definite（对称正定）矩阵时，我们期望找到一个 $B \ge 0$，使得 $B^TB = A$——

然而很多时候根本不存在这样的矩阵 $B$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此处括号反例在 OCR 中残缺（残作 "（ e matrix = AT with constant diagonals 1 + 2 0 0 ， 2 is a 5 × 5 example.）"），无法逐字恢复。

> 按语义重建：存在对角线恒为常数（即 Toeplitz 型）的 $5 \times 5$ 对称正定矩阵 $A$，它没有非负的平方根因子 $B$——非负约束比普通的 Cholesky 分解严格得多。确切矩阵元素请以原书为准。

于是我们被迫退而接受那个（在 $B \ge 0$ 中）最接近 $A$ 的矩阵 $B^TB$；

问题在于如何找到这个 $B$。

非对称的情形（通常不是方阵）则转而寻求 $U$ 与 $V$。

把注意力聚焦到 NMF 上的，是 Lee 与 Seung 在一封致 Nature（《自然》）杂志的信中所做的论述；

该信刊于 Nature **401** (1999) 788–791。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 引文出处残作 "a 401 （ 1999 ） 788 一 791"，杂志名 "Nature" 在 OCR 中丢失。

> 此处补全为：Lee, D. D. &amp; Seung, H. S., *Learning the parts of objects by non-negative matrix factorization*, Nature **401**, 788–791 (1999)。

---

> <span style="color:#7f8c8d;">Strang §I.12, p.97</span>

---

<!-- page 103: 书页 98, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文续页） -->

基本的 problem（问题）很清楚。

稀疏性（sparsity）与非负性（nonnegativity）都是非常有价值的性质。

对一个 sparse vector（稀疏向量）或 sparse matrix（稀疏矩阵）来说，那少数几个 nonzeros（非零元）才具有意义——当 1000 个或 100 000 个单独的数字无法逐一理解时，情形正是如此。

而且常常会出现数字天然就是 nonnegative（非负）的情况。

然而，SVD 中的 singular vectors（奇异向量）几乎总是含有大量符号混杂（mixed signs）的小分量。

在实际问题中，我们必须愿意放弃 $U$ 与 $V$ 的 orthogonality（正交性）。

这些性质固然优美，但 Lee 与 Seung 的那篇 essay（短文）所力主的，是 sparse PCA（稀疏主成分分析）与 nonnegative numbers（非负数）的价值。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 噪声严重："0 0 gon 呼 of U and V" 重建为 "the orthogonality of $U$ and $V$"，句末 "no negative numbers" 按上下文重建为 "nonnegative numbers"。

这些新的 objectives（目标）要求对 $A$ 作新的 factorizations（分解）：

- 对 **NMF（Nonnegative Matrix Factorization，非负矩阵分解）** 而言：寻找 nonnegative matrices（非负矩阵）$U$ 与 $V$，使得 $A \approx UV$。
- 对 **SPCA（Sparse Principal Components，稀疏主成分）** 而言：寻找 sparse（稀疏）的 $B$ 与 $C$，使得 $A \approx BC$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 两条目标在 OCR 中残作 "NNff' Find nonnegative matrices U and V so that A UV" 与 "SPCA Find rank B and C so that BC."——标签字母、近似号 $\approx$ 与第二个条目的修饰词（sparse 或 rank）均被破坏，已按 §I.12 前文（page 102）给出的 NMF 与稀疏非负框架重建；若原书第二条确为 "rank B and C"，则指低秩分解，两可之处以原书为准。

先回顾一个 factorization（分解）的含义与目的。

分解式 $A = BC$ 的含义是：$A$ 的每一列都是 $B$ 各列的一个 combination（组合）。

该组合中的 coefficients（系数）正好构成 $C$ 的某一列。

于是 $A$ 的每一列都可看作近似式 $c_1b_1 + \cdots + c_rb_r$，其中系数取自 $C$ 的一列。

对 $B$、$C$ 的 good choice（恰当选择）意味着这个求和几乎精确成立。

当 $C$ 的列数少于 $A$ 时，这就是 linear dimension reduction（线性降维）。

它对 compression（压缩）、feature selection（特征选择）与 visualization（可视化）而言是 fundamental（根本性）的。

在这类问题中，通常可以假定 noise（噪声）服从 Gaussian（高斯）分布。

此时，Frobenius norm（弗罗贝尼乌斯范数）$\|A - BC\|_F$ 就是度量 approximation error（逼近误差）的一种自然尺度。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> "C has few er column s than" 一句的受词 $A$ 在 OCR 中丢失；$A = BC$（残作 "= BC"）、求和式（残作 "CI, bl + · 一 + bn"，重建为 $c_1b_1 + \cdots + c_rb_r$）以及范数 $\|A - BC\|_F$（残作 "目 一 BCIIF"）均按上下文恢复。

这里有一篇出色的 essay（综述文章），描述了 NMF 的两个重要应用；另有一篇新论文，提供算法与参考文献：

- N. Gillis, *The Why and How of Nonnegative Matrix Factorization*, arXiv:1401.5226。
- L. Xu, B. Yu, and Y. Zhang, *An alternating direction and projection algorithm for structure-enforced matrix factorization*, Computational Optimization and Applications 68 (2017) 333–362。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 两条文献被 OCR 打碎：Gillis 条目残作 "The W 九 〗 and How “ g Matrix Fac r"，Xu–Yu–Zhang 条目残作 "An 怊 ,g 流 c 0 andprojection gor 让 九 襯 和 r 訂 ruc enforced 砒 r 和 c za 0"。已按公开文献记录核对补全：前者为 Gillis 的 NMF 综述（arXiv:1401.5226）；后者为 Xu、Yu、Zhang 关于 structure-enforced matrix factorization（结构约束矩阵分解）的交替方向与投影算法论文，卷期页码（68, 333–362, 2017）一致。

### <span style="color:#2471a3;">**[application]**</span> **Facial Feature Extraction（人脸特征提取）**

在 data matrix（数据矩阵）$A$ 中，每个 column vector（列向量）都代表一张人脸（face）。

它的各个分量就是该图像中像素的 intensities（强度），所以 $A \ge 0$。

目标是在 $B$ 中找出少数几个 "basic faces"（基础人脸），使它们的组合能逼近 $A$ 中的众多人脸。

我们可以期待：眼睛、鼻子与嘴巴几何形状的少量 variations（变化），就足以对大多数脸作出接近的重建（reconstruction）。

由 Turk 与 Pentland 发展的 eigenfaces（特征脸）方法找出一组基础人脸；matrix factorization（矩阵分解）$A \approx BC$ 则是另一条好途径。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> "The development 0f ge 和 c by Turk and Pentl and" 重建为 "The development of eigenfaces by Turk and Pentland"（即 1991 年 Turk &amp; Pentland 的 *Eigenfaces for Recognition*）；"basic faces 'nn B" 中的 "'nn" 恢复为 "in"。

### <span style="color:#2471a3;">**[application]**</span> **Text Mining and Document Classification（文本挖掘与文档分类）**

现在，$A$ 的每一列代表一篇 document（文档），每一行代表一个 word（词）。

一种简单的构造（一般并非最优，因为它忽略了词的 ordering（顺序））就是 sparse nonnegative matrix（稀疏非负矩阵）。

要对 $A$ 中的文档进行分类，我们寻找 sparse nonnegative factors（稀疏非负因子），即把 $A$ 近似分解成因子之积——其中 $B$ 的各列是 topic vectors（主题向量）$b_j$，而每篇文档对各主题的 importance（重要度）权重则由 $C$ 给出。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原书此处的分解示意图在 OCR 中仅剩残字 "（imp / j) (topic bi) / Document / ortance"，图的具体布局无法恢复；按句意重建为：文档按其对各主题的重要度组合主题向量。确切图示请以原书为准。

由于 $B \ge 0$，每个 topic vector（主题向量）$b_j$ 都可以看作一篇文档。

由于 $C \ge 0$，我们只是在 combining（组合）这些主题文档，绝不会 subtracting（相减）它们。

于是 NMF 识别出 topics（主题），并〔将整组文档〕……

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页正文末句止于 OCR 的 "Thus NMF identifies top ic s and"，句子在页码分界处截断，其述语（classifies the whole set of documents with respect to those topics，按这些主题对整组文档进行分类）位于 page 104 页首。

> <span style="color:#7f8c8d;">Strang §I.12, p.98</span>

---

<!-- page 104: 书页 99, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文续页） -->

承接 page 103 的句子：NMF 识别出主题，并根据这些主题对整组文档进行分类（classifies the whole set of documents with respect to those topics）。

与之相关的方法还有 "latent semantic analysis"（潜在语义分析）与 indexing（索引）。

注意：与 SVD 不同，NMF 是一个 NP-hard（NP 困难）问题。

即使 $A = BC$ 的 exact solutions（精确解），也并非总是唯一的。

更甚的是，topics（主题）的数目（即 $B$ 或因子矩阵的列数）是未知的。

### <span style="color:#2471a3;">**[theorem]**</span> <span style="color:#c0392b;">Nonnegative U 与 V 的最优性条件（Optimality Conditions for Nonnegative U and V）</span>

给定 $A \ge 0$，下面是对 $U \ge 0$ 与 $V \ge 0$ 来说，能使 $\|A - UV\|_F^2$ 取到最小（minimize）的条件：

```math
Y = UVV^T - AV^T \ge 0, \qquad Y_{ik} = 0 \ \text{或} \ U_{ik} = 0 \quad \text{对所有 } i,k \text{ 成立}.
```

```math
Z = U^TUV - U^TA \ge 0, \qquad Z_{ik} = 0 \ \text{或} \ V_{ik} = 0 \quad \text{对所有 } i,k \text{ 成立}.
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原式在 OCR 中残作 "丫 = uvvT 一 T > 0 with or ： 0 for a11" 与 "Z = uTuv —UTA> 0 with Zij orVi,=0foralIi,j"，行末的 KKT 互补条件只剩残缺的坐标下标。重建逻辑：对目标 $\|A - UV\|_F^2$ 分别关于 $U$、$V$ 求梯度，得到 $Y = (UV - A)V^T = UVV^T - AV^T$（关于 $U$）与 $Z = U^T(UV - A) = U^TUV - U^TA$（关于 $V$）；KKT 条件要求 $Y \ge 0$、$Z \ge 0$（对非负可行域），且互补松弛成立（各分量要么梯度分量为 0，要么相应变量为 0）。其中符号约定与坐标记法以原书为准——此即 §I.12 常见的 NMF 一阶最优性条件（KKT 互补条件）。

这两组条件本身已暗示：$U$ 与 $V$ 有可能最终是 sparse（稀疏）的。

### <span style="color:#2471a3;">**[section]**</span> **Computing the Factors: Basic Methods（计算因子：基本方法）**

人们已提出许多 algorithms（算法）来计算 $U$ 与 $V$（以及 $B$ 与 $C$）。

一个自然的想法是 alternating factorization（交替分解）：先固定一个因子，去优化另一个因子；

再固定这一个，去优化第一个因子，如此反复。

采用 Frobenius norm（弗罗贝尼乌斯范数）时，每一步都是一次 least squares（最小二乘）求解。

这是自然的 approach（途径），而且通常能给出好的结果；

但 convergence（收敛性）问题始终悬而未决（convergence remains elusive），我们或许要期待 optimization theory（优化理论）有进一步的发展。

该方法有一个确立已久的改进，将在 Section III.4 中给出：Alternating Direction Method of Multipliers（乘子交替方向法，ADMM）。

该算法引入一个 penalty term（罚项）来促进收敛。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 句中 "But convergence the 方 e 00 刀 s" 残缺，按常搭配重建为 "But convergence remains elusive"（收敛依旧难以捉摸）；同段另两处 "we may expect further d e10 贮 ments the theory 0f optirmzation" 重建为 "further developments in the theory of optimization"、"a p enalty term and d 呼 t0 promote convergence" 重建为 "a penalty term to promote convergence"（残字 $d$ 无法确定含义，若原书另有它词请以原书为准）。

### <span style="color:#2471a3;">**[section]**</span> **Sparse Principal Components（稀疏主成分）**

许多 applications（应用）确实允许正负数值同时出现——我们并不是在计数或建造实际的 objects（物件）。

在 finance（金融）中，我们既可以买入也可以卖出。

在另一些应用中，zero point（零点）并没有内在意义。

零摄氏度只是 Centigrade（摄氏）与 Fahrenheit（华氏）之间的一个约定（convention）问题。

也许水更"支持"摄氏，而 super-cold physics（超低温物理学）则把零点重置到别处（如绝对零度）。

零分量（zero components）的数目往往很重要——这正是 SVD 中 singular vectors（奇异向量）$u$ 与 $v$ 的难点所在。

它们满是 nonzeros（非零元），正如在 least squares（最小二乘）里那样。

我们无法因为 transaction costs（交易成本）而购买 giant asset（巨额资产）的微小数量；

如果我们列出了 500 个会影响病人结局的 genes（基因），也不可能逐一处理它们。

为了被理解并能付诸行动，nonzero decision variables（非零决策变量）的数目必须受到控制。

一种可能是去掉 $u$ 与 $v$ 的极小的分量；

但我们想要真正的控制——直接构造 sparse vectors（稀疏向量）对我们更有利，人们已提出不少好的算法。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 损伤集中："we le 500 genes" 重建为 "If we list 500 genes"；"The number ze co po 刀 en" 重建为 "The number of zero components"——其后紧接 "They are full of nonzeros" 形成反差（零分量数目重要，恰恰因为奇异向量满是非零元），段末 "the number of nonzero decision variables must be under control" 再收束于稀疏主题，故按 "zero components" 重建（若原书作 "nonzero components" 之类，请以原书为准）；$u$ 与 $v$ 的变量名在两处被 OCR 吞掉，按语境补回。

关于 sparse PCA 的文献，见：

> Zou, T. Hastie, R. Tibshirani, *Sparse Principal Component Analysis*, Journal of Computational and Graphical Statistics 15 (2006) 265–286。

> 另见 https://en.wikipedia.org/wiki/Sparse_PCA。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 首作者名在 OCR 中残作 "Zou T. Hastie, R. Tibshirani"，已核对补全为 H. Zou、T. Hastie、R. Tibshirani（Journal of Computational and Graphical Statistics 15 (2006) 265–286）；条目内的论文标题与期刊名均被打碎，按公开文献记录恢复。

> <span style="color:#7f8c8d;">Strang §I.12, p.99</span>

---

<!-- page 105: 书页 100, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文续页：Sparse PCA 与 LASSO） -->

> <span style="color:#7f8c8d;">（承接 page 104：本页延续 §I.12 中 Sparse Principal Components（稀疏主成分）小节的讨论——从 cardinality 约束走向 $\ell^1$ 罚项、nuclear norm（核范数）与 LASSO。页眉 "Highlights of Linear Algebra" 系重复的栏眉，不译。）</span>

这里的 Sparse PCA（稀疏主成分分析）从一个 data matrix（数据矩阵）$A$ 出发，或从一个 positive (semi)definite sample covariance matrix（正（半）定样本协方差矩阵）$S$ 出发。

给定 $S$ 之后，一个自然的想法，是把 $\operatorname{Card}(x)$——即 $x$ 的 nonzero components（非零分量）个数——放进 penalty term（罚项）之中，或放进对 $x$ 的 constraint（约束）之中：

```math
\max_x \ x^T S x \qquad \text{subject to} \quad \operatorname{Card}(x) \le k
```

也可以把罚项写进目标函数：

```math
\max_x \ \big( x^T S x - \lambda \, \operatorname{Card}(x) \big)
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段公式在 OCR 中残作 "Maximrze T / Maximrze T"、"Sc subJect to C ard（ ）孓（5）" 与 "c Sc 一 card（ or"，目标式 $x^T S x$ 被打散，不等号 "$\le$" 被读作 "孓"，变量名尽失；按前句 "include Card(x) ... in a penalty term or a constraint" 的两种语义重建为约束形式（$\operatorname{Card}(x) \le k$）与罚项形式（$x^T S x - \lambda \operatorname{Card}(x)$）两式。OCR 中的 "(5)" 疑为公式编号，其确切位置无法复原；正规的 sparse PCA 通常还带长度归一化（如 $\|x\|_2 = 1$），该约束在 OCR 中没有留下痕迹，请以原书为准。

然而，$x$ 的 cardinality（基数）对 optimization algorithms（优化算法）而言并不是最好的量。

另一条方向与 graphs（图）有关，在 §VI.3 中会作简短讨论。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 句首残作 "Another direction is gra &, discussed bnefly in Section VI.3"，其中 "gra &" 无法确证原词；结合其后的语境（未知的 vector 变为 unknown symmetric matrix，并把逐元素不等式替换为半正定约束）暂重建为 graphs，若原书另有它词请以原书为准。

那条方向把未知的 vector（向量）$x$ 换成一个未知的 symmetric matrix（对称矩阵）$X$。

形如 $X \ge 0$ 的不等式（意思是每一个 $X_{ij} \ge 0$）被替换成 $X \succeq 0$（$X$ 必须 positive semidefinite（半正定））。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 句中 "Inequalities like 0 (meaning that every 0）are replaced by 之 0（天 must be positive semdefinite）" 残缺：左侧不等式与 "$X_{ij}$" 下标被吞，符号 "之" 在 OCR 中无法与 $\ge$/$\succeq$ 区分，故按语义重建为逐元素 $X \ge 0$ 被半正定 $X \succeq 0$ 取代（"天"即 $X$）。

给未知矩阵 $X$ 加上 $\ell^1$ penalty（罚项），即可实现 sparsity（稀疏性）。

展望 §IV.5 可知，那里的罚项用的正是 nuclear norm（核范数）——即 singular values（奇异值）之和。

$\ell^1$ 与 sparsity（稀疏性）之间的联系，画在 §I.11 开头的那几幅 figures（图）之中。

那里的 $\ell^1$ minimization（最小化）给出了 sparse solution（稀疏解）$x = (0, 1)$。

对这个 $\mathbb{R}^2$ 中的短向量而言，那个零或许看起来像是偶然的、无足轻重的。

恰恰相反，这个零才是重要的事实。

对矩阵来说，则要把 $\ell^1$ norm（范数）换成 nuclear norm（核范数）。

对 $\|x\|_1$ 或 $\|X\|_*$ 施加罚项，会产生 sparse vectors（稀疏向量）与 sparse matrices（稀疏矩阵）$X$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "A penalty on |@|丨1 or 丨| produces sparse vectors and sparse matrices X"：第一项恢复为 $\|x\|_1$（对向量的 $\ell^1$ 罚），第二项恢复为核范数 $\|X\|_*$（对矩阵奇异值之和的罚，OCR 中竖杠与下标记号丢失）；"sparse matrices" 在此实指奇异值稀疏（低秩）的矩阵，措辞以原书为准。

归根到底，对 sparse vectors（稀疏向量）而言，算法必须选出重要的 variables（变量）。

这正是 $\ell^1$ optimization（优化）的出色性质——它正是 LASSO（Least Absolute Shrinkage and Selection Operator，套索算法）的关键：

```math
\text{LASSO:}\qquad \min_x \ \frac{1}{2}\,\|Ax - b\|_2^2 + \lambda \|x\|_1
```

高效地求出这个最小值，是 nonlinear optimization（非线性优化）的一大 triumph（成就）。

乘子交替方向法（ADMM，Alternating Direction Method of Multipliers）与布雷格曼（Bregman）算法，都将在 §III.4 中给出并讨论。

关于 LASSO 有一点提示：最优解 $x^*$ 的非零分量（nonzero components）个数，不会超过 samples（样本）的个数。

再加上一个 $\ell^2$ penalty（罚项），就得到没有这一缺点的 elastic net（弹性网）。

这种 $\ell^1$ 加 ridge regression（岭回归）的回归，可以像 least squares（最小二乘）一样快速地求解。

```math
\text{Elastic net:}\qquad \min_x \ \frac{1}{2}\,\|Ax - b\|_2^2 + \lambda_1 \|x\|_1 + \lambda_2 \|x\|_2^2
```

§III.4 将给出 ADMM algorithm（算法），它把 $\ell^1$ 部分同（光滑的二次项）分裂（split）开来。

它又借助 Lagrange multipliers（拉格朗日乘子）与 duality（对偶性）加入一个罚项。

这个组合非常有力。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> LASSO 与 elastic net 的目标式在 OCR 中残作 "LASSO Minimize 一 2 + \`" 与 "Minimize llAc 一 blI?2 + 1 + 硎 c 腭"，已按标准定义重建为 $\frac{1}{2}\|Ax-b\|_2^2+\lambda\|x\|_1$ 与 $\frac{1}{2}\|Ax-b\|_2^2+\lambda_1\|x\|_1+\lambda_2\|x\|_2^2$（常系数与正则参数记号以原书为准）。"splits $\ell^1$ from ..." 一句的宾语在 OCR 中缺失（残作 "splits 乏 1 什 om"），按 ADMM 把非光滑 $\ell^1$ 项与光滑二次项分离的机制补足。

相关的两篇文献如下：

> 1. R. Tibshirani, *Regression shrinkage and selection via the Lasso*, Journal of the Royal Statistical Society, Series B 58 (1996) 267–288。
> 2. H. Zou and T. Hastie, *Regularization and variable selection via the elastic net*, Journal of the Royal Statistical Society, Series B 67 (2005) 301–320。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 两条文献被 OCR 打得支离破碎：Tibshirani 条目残作 "Regression shnnkage an d selection via th e Lasso, rn 叻 e 灭 S 勉 c S “ 讵 舭 Series B 58（1996）267 一 288"，Zou–Hastie 条目残作 "Hø Zou and Has ti e, Regulanzauon and variable selection vi a the elastic net ... Series B 67（2005）301 一 320"；刊名 "Journal of the Royal Statistical Society, Series B" 与作者名按公开文献记录恢复（H. Zou 即 Hui Zou，非 "Hø"）。

> <span style="color:#7f8c8d;">Strang §I.12, p.100</span>

---

<!-- page 106: 书页 101, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文续页：Tensors、Example 1 彩色图像、Example 2 导数 ∂w/∂A） -->

> <span style="color:#7f8c8d;">（承接 page 105：§I.12 在讨论完 Sparse PCA 与 LASSO 的文献之后，转向 tensors（张量）主题。页眉中的章节标题 "Factoring Matrices and Tensors: Positive and Sparse" 系重复栏眉，不译；此页含一个小节与两个 Example。）</span>

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">**Tensors（张量）**</span>

一个 column vector（列向量）是一个 1-way tensor（一阶张量）。

一个 matrix（矩阵）是一个 2-way tensor（二路张量）。

于是，3-way tensor（三路张量）$T$ 就带有元素 $T_{ijk}$，它们有三个 indices（下标）：row number（行号）、column number（列号）和 "tube number"（管号）。

$T$ 的 slices（切片）是二维的截面（two-dimensional sections），所以下面这个三路张量有 3 个 horizontal slices（水平切片）、4 个 lateral slices（侧向切片）和 2 个 frontal slices（正面切片）。

在 $T$ 中，行（rows）、列（columns）与管（tubes）都是纤维（fibers），每次只变化一个下标（index）。

我们可以把若干个 $m \times n$ 矩阵堆叠成一个 3-way tensor（三路张量）。

同样地，我们也可以把 $m \times n \times p$ 的张量堆叠成 4-way tensor（四路张量），即 4-way array（四维数组）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原书此处是一幅 "vector → matrix → tensor" 的堆叠示意图；OCR 只保留了图中标注（"vector in $\mathbb{R}^3$"、"matrix $A$ in $\mathbb{R}^{3\times4}$"、"tensor $T$ in $\mathbb{R}^{3\times4\times2}$"），图的布局无法恢复。"$n$ 个 $m \times n$ 矩阵"中的个数与变量字母在 OCR 中缺失（残作 "stack m by matnces Of them)"），按堆叠语义补足；"horizontal / lateral / frontal slices" 的数目 3、4、2 与尺寸 $3 \times 4 \times 2$ 相印证。

### <span style="color:#2471a3;">**[example]**</span> **Example 1: A Color Image is a Tensor with 3 Slices（彩色图像是有 3 个切片的三路张量）**

一幅黑白图像（black and white image）不过是一个 pixels（像素）矩阵。

矩阵中的数字就是每个像素的 grayscales（灰度值）。

通常这些数字介于 0（黑色）与 255（白色）之间。

每一个 entry（元素）都有 $2^8 = 256$ 个可能的灰度值。

一幅彩色图像则是一个 tensor（张量）。

它有 3 个对应于 red-green-blue（红、绿、蓝）的 slices（切片）。

每个切片显示 RGB 三种颜色中一种颜色的 density（密度）。

处理这个张量（例如在 §VII.2 的 deep learning（深度学习）中）并不比处理黑白图像更难。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "Every enfry in has 28 = 256 possible grayscales"：句末 "in" 疑属上方数字区间叙述，指数 "$2^8 = 256$" 的幂记号丢失（"28" 重建为 $2^8$），按 "每个元素可在 0–255 中取值，共 $2^8 = 256$ 种灰度" 的语义归位；"red-green-blue" 与 "RGB" 在 OCR 中拼写不全，按上下文补全。

### <span style="color:#2471a3;">**[example]**</span> **Example 2: The Derivative ∂w/∂A of w = Ax（$w = Ax$ 关于 $A$ 的导数）**

这是一个我们始料未及（didn't see coming）的张量。

在 deep learning（深度学习）中要优化的 "weights"（权重），就存放在这个 $m \times n$ 矩阵 $A$ 里。

这个矩阵乘以向量 $x$，就产生 $w = Ax$。

于是，用于优化的 algorithm（算法，见 §VI.4–§VII.3）就需要每一个 output（输出）分量关于每一个 weight（权重）的导数。

这样我们就有三个下标 $k, i, j$。

在乘法运算中我们知道：$A$ 的第 $i$ 行对 $w = Ax$ 的第 $k$ 个输出没有任何影响，除非 $k = i$。

所以导数公式中会包含符号 $\delta_{ki}$，当 $k = i$ 时它等于 1，否则等于 0。

在规范（proper）的张量记号中也会出现这个符号（我们关于张量的权威是 Pavel Grinfeld）。

线性函数 $w = Ax$ 关于各权重 $A_{ij}$ 的导数如下：

```math
\frac{\partial w_k}{\partial A_{ij}} = \delta_{ki}\, x_j \tag{8}
```

例如 $T_{111} = 1$，而 $T_{122} = 0$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页 OCR 损伤极重：标题残作 "The Derivative Dw/DA of = 蓋 鬱"，正文残作 "row 丿 of has no effect on row of = 鬱"、"the derivative 皿 ula includes the symbol ötj，which is 1 if = 丿 and 0 otherwise"、"with respect to the weights 弘 are in："。按微积分重建：$w_k = \sum_j A_{kj}x_j$，故 $\partial w_k/\partial A_{ij} = \delta_{ki}x_j$（$k \neq i$ 时为零），其中 $\delta_{ki}$ 是 Kronecker delta（克罗内克 δ）；OCR 中两次出现 "row" 处对应原文为 row of $A$ 与 row（即第 $i$ 行的影响只落在第 $i$ 个输出上）。末句 "$T_{111} = 1$，而 $T_{122} = 0$" 即该式的两个具体实例：$T_{111} = \partial w_1/\partial A_{11} = x_1$（取 $x_1 = 1$ 时得 1），而 $T_{122} = \partial w_1/\partial A_{22} = \delta_{12}x_2 = 0$（$w_1$ 与 $A_{22}$ 无关）。各变量名与具体取值若与原书不完全一致，请以原书为准。

> <span style="color:#7f8c8d;">Strang §I.12, p.101</span>

---

<!-- page 107: 书页 102, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文续页：导数张量的多层意义与 backpropagation、Example 3 联合概率张量） -->

> <span style="color:#7f8c8d;">（承接 page 106 的 Example 2：$\partial w/\partial A$ 给出的 3-way tensor。本页先讲清这一导数张量在多层神经网络与 backpropagation（反向传播）中的角色，随后进入 Example 3——The Joint Probability Tensor（联合概率张量）。页眉 "Highlights of Linear Algebra" 系重复栏眉，不译。）</span>

在 §VII.3 中会有一个 $2 \times 2 \times 2$ 的例子。

我们遇到的这个导数张量（即 Example 2 中的 $\partial w/\partial A$）尤其值得关注，理由有两点：

其一，把张量的列下标 $j$ 固定为常数，所得的各张 slices（切片）都是 identity matrix（单位矩阵）的倍数 $x_j I$。

其二，这个张量正出现在深度学习的关键函数之中——该函数把 neural net（神经网络）的每一层连接到下一层。

如果一层中含有向量 $x$，那么下一层所含的向量就是 $y = (Ax + b)_+$。

我们要用 training data（训练数据）去优化其中的 weights（权重）。

因此，对最优权重而言，loss function（损失函数）的各导数都应当为零。

借助微积分中的 chain rule（链式法则），$L$ 的导数可以这样求出：把从每一层传到下一层的导数 $\partial w / \partial A$ 逐层相乘。

每一层都是先作线性步骤 $x \mapsto Ax + b$（linear step），随后是其中的非线性部分——ReLU（Rectified Linear Unit，修正线性单元）函数把全部为负的 components（分量）都置为零。

这个线性步骤的导数正是我们的 3-way tensor（三路张量）。

这一切都将在 §VII.3 中再次出现，不过我们不会显式使用 tensor calculus（张量微积分）。

反向传播（backpropagation）的思想，是要把损失函数 $L$ 的全部导数都"自动地"计算出来。

在计算输出的每一步中，这一步的导数都会进入 $L$ 的导数。

我们那个有趣张量的简单公式 (8)，将会埋没在 backpropagation 之中。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 损伤极重：首句残作 "This tensor 弘 = 鬱 k is of particular interest"、"Slices = constant are multiples Vk Of the identity matnx"、"the vector = （ 鬱 + b)+"、"is a 砒 r … 叩 tim ize e weights 砒 c 九 叻 e t 甩 沅 g data"。按 page 106 Example 2 的语境重建：导数张量 $T_{kij} = \partial w_k/\partial A_{ij} = \delta_{ki} x_j$ 中，把权重矩阵 $A$ 的列下标 $j$ 固定后，切片（张成 $k, i$ 两个下标的二维截面）恰为标量 $x_j$ 乘单位矩阵，故原句 "the slices $j$ = constant are multiples of the identity matrix" 得以复原，OCR 中的 "$V_k$" 疑为这些倍数或层标记的噪声；"$y = (Ax + b)_+$" 中的 $(\cdot)_+$ 即 ReLU 正部。本段所谈 $2 \times 2 \times 2$ 例子与所固定下标的具体安排若与原书不同，请以原书为准。

### <span style="color:#2471a3;">**[example]**</span> **Example 3: The Joint Probability Tensor（联合概率张量）**

假设我们测量三类量：年龄 $a$（以岁计）、身高 $h$（以英寸计）与体重 $w$（以磅计）。

我们把儿童分入 $I$ 个 age groups（年龄组）、$J$ 个 height groups（身高组）与 $K$ 个 weight groups（体重组）。

于是，一个典型儿童总是落在某个 age group $i$、某个 height group $j$ 与某个 weight group $k$ 之中。

其中编号分别介于 $1$ 与 $I$、$1$ 与 $J$、$1$ 与 $K$ 之间，即 $1 \le i \le I$、$1 \le j \le J$、$1 \le k \le K$。

随机挑选一个儿童。

设这些 age groups 分别装有 $n_1, \dots, n_I$ 个儿童（加起来正是 $N$ 个儿童）。

那么，随机儿童处于 age group $i$ 的概率就是 $n_i / N$。

类似地，$J$ 个 height groups 分别装有 $m_1, \dots, m_J$ 个儿童，$K$ 个 weight groups 分别装有 $c_1, \dots, c_K$ 个儿童。

于是随机儿童落在 height group $j$ 的概率是 $m_j / N$，落在 weight group $k$ 的概率是 $c_k / N$。

现在来到我们真正的目标：joint probabilities（联合概率）$P_{ijk}$。

对每个组合 $(i, j, k)$，我们只清点那些同时处于 age group $i$、height group $j$ 与 weight group $k$ 中的儿童。

每个儿童共有 $I \times J \times K$ 种可能的三元组合（某些 $P_{ijk}$ 可能为零——例如当没有既最年长、身高又最矮且体重又最轻的儿童时，$P_{111} = 0$。）

设在 age group $i$、height group $j$ 与 weight group $k$ 的交集中找到 $n_{ijk}$ 个儿童。

那么，这一 age-height-weight 组合的联合概率为：

```math
P_{ijk} = \frac{n_{ijk}}{N} \tag{9}
```

这样我们总共有 $I \times J \times K$ 个概率 $P_{ijk}$，它们全部介于 $0$ 与 $1$ 之间。

这些概率正好填满一个 joint probabilities 的 3D tensor（三维张量）。

这个张量有 $I$ 行、$J$ 列与 $K$ 条 tubes（管）。

其全部元素之和为 $1$。

为了真正领会这个 $I \times J \times K$ 的张量，设想你把所有形如 $P_{2jk}$ 的数都加起来。

此时你统计的正是处于 age group 2 的全部儿童：

```math
P_{2\cdot\cdot} = \sum_{j=1}^{J}\sum_{k=1}^{K} P_{2jk} \tag{10}
```

这个对 $j$ 与 $k$ 双重求和的边际概率（公式 10），就是"一个儿童处于 age group 2"的概率。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> Example 3 中各组儿童人数与计数的记号在 OCR 中几乎不可辨（残作 "contain 0i, … , children"、"九 ． 九 , hJ children"、"contam WI , 2 , … , WK"、"Suppose ； 廾 children are found"），已按概率论惯例重建为 $n_i$、$m_j$、$c_k$ 与 $n_{ijk}$，并以 $N$ 记儿童总数；$P_{ijk}$ 的求和范围（$1 \le i \le I$ 等）据原文 "between 1, 1, 1 and I, J, K" 复原，公式 (10) 的双重求和据 OCR 行末 "j=l = 1" 复原。具体记号若与原书不一致，请以原书为准。

> <span style="color:#7f8c8d;">Strang §I.12, p.102</span>

---

<!-- page 108: 书页 103, §I.12 Factoring Matrices and Tensors: Positive and Sparse（正文续页：边际切片的求和使用、The Norm and Rank of a Tensor 小节） -->

> <span style="color:#7f8c8d;">（承接 page 107 的 Example 3：把张量元素按组求和，即得到更粗粒度的边际概率与张量的 slices。本页随后转入本节新的小节——The Norm and Rank of a Tensor（张量的范数与秩）。页眉中的章节标题系重复栏眉，不译。）</span>

固定年龄下标（例如取 age group 2）之后，我们正在观察这个张量的一张 2D slice（二维切片）。

确实，若把公式 (10) 所示的边际化过程对所有年龄组各做一遍，再把所得概率 $P_{1\cdot\cdot}, P_{2\cdot\cdot}, \ldots, P_{I\cdot\cdot}$ 全部相加，总和自然是 $1$。

类似地，你也可以把全部形如 $P_{2j5}$ 的数都加起来。

此时你统计的正是同时处于 age group 2 与 weight group 5 中的全部儿童：

```math
P_{2\cdot 5} = \sum_{j=1}^{J} P_{2j5} \tag{11}
```

这个对 $j$ 求和的边际概率（公式 11），就是"儿童同时处于 age group 2 与 weight group 5"的概率。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页第一段起于 page 107 的 Example 3：通过把年龄、身高、体重分组并计数，建立了联合概率张量 $P_{ijk} = n_{ijk}/N$。这里 OCR 损伤极重，各边际概率记号几乎不可辨——首行残作 "We are seeing a 2D slice of th e tensor"，其求和式残作 "the sum + P% + 一 + 7 equals 1"，OCR 行首的 $(11)$ 与 "j = 1" 散落于后续各孤立行中。按 page 107 公式 (10) 的边际化惯例重建：固定 $i = 2$ 得一张 2D slice，其概率 $P_{2\cdot\cdot}$ 即"处于 age group 2"的边际概率（OCR 残作 "P 万 5 = P2 5"，其中 "万" 为 $2\cdot5$ 的噪声）；若把公式 (10) 对全部年龄组所得边际概率 $P_{i\cdot\cdot}$ 相加，总和自然为 $1$。随后固定 $i = 2$ 与 $k = 5$（OCR 残作 "add all the numb ers P2 祁"，"祁" 为 $2j5$ 的噪声）并对 $j$ 求和，得公式 (11)：$P_{2\cdot 5} = \sum_{j=1}^J P_{2j5}$，即"同时处于 age group 2 与 weight group 5"的边际概率。求和范围 $j = 1,\dots,J$ 按 page 107 惯例重建，若与原书不同，请以原书为准。

这些数字（例如 $P_{2j5}$）位于张量的一根 fibers（纤维）之中，即固定 age group（下标 $i$）与 weight group（下标 $k$）、只让 height group（下标 $j$）变动所得的一列。

我们可以把若干根这样的 fibers 合并（combine）起来，构成张量的一张 slice（切片）。

我们还可以把若干张 slices 叠加起来，还原出完整的张量（各正面切片逐张相加即得整个张量 $T$）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 仅残作 "These numbers are in a CO 忉 of"、"We could combine columns tO make a slice Of"、"We could combine slices t0 produce th e whole tensor" 及孤立的求和行 "乥 乥 一 乥 ： 1 / = 1 = 1"。"CO 忉 of" 中的名词与张量的具体轴无法确证（在 page 107 的语境中，"combine fibers" 或 "combine rows" 均说得通）；孤立的求和式只能辨出对某个下标（OCR 之 "$1$"）求和、结果归一为 $1$，正文仅以文字表述"若干纤维合成切片、若干切片合成全张量"的语义，与原书的确切表述可能有出入，请以原书为准。

通过测量三种性质，我们便引出了这个元素为 $P_{ijk}$ 的 3-way tensor（三路张量）。

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">**The Norm and Rank of a Tensor（张量的范数与秩）**</span>

一般地，一个 tensor（张量）就是一个 $d$-way array（$d$ 路数组）。

正如矩阵的一个元素需要两个数字来确定其位置，一个 $d$-way tensor 的元素则需要 $d$ 个数字。

这里我们只集中讨论 $d = 3$ 的情形，即 3-way tensors（三路张量，也称 order 3（三阶）的张量）。

继 vectors（向量）与 matrices（矩阵）之后，$d = 3$ 是最常见、也最容易理解的情形。

$T$ 的 norm（范数）与矩阵的 Frobenius norm（弗罗贝尼乌斯范数）一样：把全部 $T_{ijk}^2$ 相加，得到 $\|T\|_F^2$。

```math
\|T\|_F^2 \;=\; \sum_{i,j,k} T_{ijk}^2
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 残作 "a d-way ten s or needs d numbers"、"3-way 三路张量（also called ten s ors of order 3）"、"Add all T?. to find 日 T 》 》 2"；范数式 "$T_{ijk}^2$ 求和得 $\|T\|_F^2$" 据 "the Frobenius norm of a matrix" 的重述重建为上式，记号与求和范围若与原书不同，请以原书为准。

张量的理论至今仍属于 linear algebra（线性代数）——或者也可说是 multilinear algebra（多重线性代数）的一部分。

与矩阵一样，张量在科学与工程中可以扮演两种不同的角色：

其一，张量可以乘 vectors（向量）、matrices（矩阵）或 tensors（张量），这时它就是一个 linear operator（线性算子）。

其二，张量可以存放数据。

它的元素可以给出图像中各个 pixels（像素）的 brightness（亮度）。

一张彩色图像是 3-way 的——即按 RGB 三种颜色堆叠而成；一部彩色视频则会是 4-way tensor（四路张量）。

算子张量（operator tensor）可以像 permutation matrix（置换矩阵）、reflection matrix（反射矩阵）或任何 orthogonal matrix（正交矩阵）作用于 data matrix（数据矩阵）那样，作用于 data tensor（数据张量）上。

两者之间的类比是清楚的，只不过张量需要更多下标，看起来也更复杂。

即使张量乘法或许能够成功——如同对矩阵那样，各种运算可以按不同顺序进行——对张量的分解（factorization）却未必能同样成功。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 残作 "We could succeed with tensor multiplication ()s for matnces， th e operations can come in different orders) · will 0 succeed SO well for 怊 sor 和 c r 讵 a 0 法"。末句动词被吞（"will 0 succeed"），依段落逻辑（"analogies are clear but tensors … look more complicated"，随后转说矩阵分解）重建为 "乘法推广或可成功，分解却难如此成功"；"怊 sor 和 c r 讵 a 0 法" 即 tensor factorization（张量分解）。下段 "This has been and still is an intense research direction" 承接此意，可相互印证。

把矩阵分解推广到张量的研究，曾经是、如今也仍然是一个热门方向——力图尽可能完整地抓住那些对 linear algebra（线性代数）至关重要的 matrix factorizations（矩阵分解）：$A = LU$、$A = Q \Lambda Q^T$、$A = U \Sigma V^T$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本句 OCR 残作 "to c ap tu re as much as possible 0f the matrix factorizations th at are so central to linear algebra ： L Q 月 ， QAQT UEVT"。其中 "QAQT" 依术语表重建为谱分解 $A = Q\Lambda Q^T$，"UEVT" 重建为奇异值分解 $A = U\Sigma V^T$；首项 "L Q 月" 最可能是 LU 分解 $A = LU$（OCR 把 "LU" 拆散并把某记号误读为 "月"），也不排除原书列有 $QR$ 等更多项，具体以原书为准。

甚至张量的秩（rank of a tensor）这一定义与计算，也不像矩阵的秩那样简单、那样成功。

不过 rank-one tensors（秩一张量）——即 outer products（外积）——仍然是最简单、最清晰的张量：它们由三个向量 $a, b, c$ 生成，例如

```math
T_{ijk} = a_i b_j c_k \tag{12}
```

（公式 12）就是一个秩一（rank-one）的 3-way tensor（三路张量），记为 $T = a \otimes b \otimes c$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 残作 "UEVT"、"Tij k = OibjCk"、"3-way tensor T = 0 0 b 0 c Of rank one"。"UEVT" 依术语表重建为 $A = U\Sigma V^T$；"OibjCk" 依外积定义重建为 $T_{ijk} = a_i b_j c_k$，故三个向量依序应为 $a, b, c$（OCR 首向量字母已被吞）；符号 "0" 是张量积 $\otimes$ 的噪声（"0 0 b 0 c" 即 $a \otimes b \otimes c$）。公式编号 (12) 依后文 "(12)" 归位，OCR 中第 (11)、(12) 两个编号均出现于 (9)、(10) 之后的正确顺序。

这个 outer product 由这三个向量中总共 $m + p + q$ 个数字所定义。

而张量（tensor）的秩，则是指以最少的项数把若干这样的 rank-one tensors（秩一张量）加起来而得到 $T$——即生成 $T$ 所需的最少 rank-one tensor 个数。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 末行 OCR 残作 "The 殍 k 口 怊 or is the 豆 张 r 甩 1 nso add T"（几乎不可辨），已按 "rank of a tensor = 以最少个 rank-one tensors 之和表示 $T$" 的标准定义重建为译文正文句——张量的秩即以最少的项数把 rank-one tensors 相加而得到 $T$。另：前一行中 "$m + p + q$" 的一个数被吞（残作 "the m + + P numbers"），三个向量各维长度之和的具体记号以原书为准；"0 0 b 0 c" 即 $a \otimes b \otimes c$。

> <span style="color:#7f8c8d;">Strang §I.12, p.103</span>

---

<!-- page 109: 书页 104, OCR page 9（正文页） -->

> <span style="color:#7f8c8d;">**本页结构清单（正文页，属 §I.12 Factoring Matrices and Tensors: Positive and Sparse，即「分解矩阵与张量：正定与稀疏」）**：① 引论——多个外积之和产生低秩张量；② 反例 (13)——貌似秩 3 的张量可为若干秩 2 张量之极限；③ 矩阵的 Eckart-Young 定理 vs 三路张量无 SVD；④ 小节 The CP Decomposition of a Tensor（张量的 CP 分解）与定义 (14)；⑤ 发现者与命名 CANDECOMP/PARAFAC；⑥ 与 SVD 的三点差别；⑦ Kruskal 唯一性；⑧ NP-hard 与 Lim–Hillar 结果；⑨ 交替最小二乘思路引论。</span>

如果我们把若干这样的 outer product（外积）加起来，就得到一个很方便的 low-rank tensor（低秩张量）——即使我们并不总是知道它的精确 rank（秩）；下面给出一个例子，说明为什么会出现这种不确定性。

<span style="color:#2471a3;">**[example]**</span> 设 $T$ 是三个 rank-one tensor（秩一张量）之和：

```math
T = \mathbf{a}_1 \otimes \mathbf{b}_1 \otimes \mathbf{c}_1 + \mathbf{a}_2 \otimes \mathbf{b}_2 \otimes \mathbf{c}_2 + \mathbf{a}_3 \otimes \mathbf{b}_3 \otimes \mathbf{c}_3 \tag{13}
```

$T$ 看起来具有秩 3；但它却是一串秩 2 张量 $T_\epsilon$（rank-2 tensors）在 $\epsilon \to 0$ 时的极限。

> <span style="color:#1e8449;">**[note] 译者注（第一性原理洞察 + 证明策略模板）:**</span> Strang 的 (13) 展示了矩阵世界里不可能发生的现象，值得用你在 6.042J 学过的语言说透：对矩阵，{秩 ≤ k} 的集合是闭集——一串秩 ≤ k 的矩阵若有极限，极限的秩仍 ≤ k，因为 SVD 这把「刚性标尺」（Eckart-Young 定理）把最佳秩 k 逼近固定为前 k 个奇异向量，从秩 3 到秩 2 必须跨过 $\sigma_{3}$ 这道距离，极限被「钉」在原处。张量没有这把标尺：CP 秩 ≤ R 的集合由「R 项秩一外积的参数拼成」，参数可以发散又相消——某对因子分量同时趋向 0 与 ∞，抵消后净效果等价于多出几项——所以看似秩 3 的对象能成为秩 2 序列的极限。证明「不封闭」的标准模板：先猜 R 的下界，再构造随 $\epsilon$ 变化的参数族，说明任何有限 R 都挡不住这次「秩泄漏」。Lim–Hillar 的 NP-hard 结论（CLRS §34：不存在多项式时间算法）让因果链闭环：无 SVD ⇒ 无 Eckart-Young ⇒ 连「秩是几」都无法高效判定 ⇒ 精确 CP 分解只能让位给近似与启发式。这段值得作为「反直觉现象 → 结构性原因 → 算法后果」三层拆解的范本收藏。

**

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原书 (13) 中 $T$ 的三个秩一分量系数及 $T_\epsilon$ 的显式表达式在 OCR 中几乎全部损毁（仅残留孤立数字 1、0、0）。此处依据正文叙述——「貌似秩 3 的张量是若干秩 2 张量的极限」——作示意性重建，以展示张量秩的「不封闭」现象。

为什么这种事绝不会发生在矩阵身上？

<span style="color:#2471a3;">**[note]**</span> 因为对矩阵 $T$ 而言，最接近它的 rank $k$ approximation（秩 $k$ 近似）由 Eckart-Young theorem（Eckart-Young 定理）固定下来。

那个最佳近似 $A_k$ 来自 SVD（singular value decomposition，奇异值分解）中的 leading singular vectors（前导奇异向量），因此从秩 3 到秩 2 的距离（distance）是固定不变的。

可惜对一般的 three-way tensor（三路张量）似乎并不存在 SVD。

不过接下来的段落表明我们仍要尝试——因为在计算中我们需要 $T$ 的一个良好低秩近似；两个可选方案是 CP 与 Tucker（Tucker 分解）。

### 张量的 CP 分解（The CP Decomposition of a Tensor）

在 tensor analysis（张量分析）与 fast tensor computations（快速张量计算）中，一个根本性问题是用若干秩一张量之和逼近给定张量 $T$，即寻找一种 approximate factorization（近似分解）。

<span style="color:#2471a3;">**[definition]**</span> 定义 (14)：$T$ 的 CP decomposition（CP 分解）写作

```math
T \approx \mathbf{a}_1 \otimes \mathbf{b}_1 \otimes \mathbf{c}_1 + \cdots + \mathbf{a}_R \otimes \mathbf{b}_R \otimes \mathbf{c}_R \tag{14}
```

这一分解有若干位发现者：Hitchcock、Carroll、Chang 与 Harshman。

它也曾有过一些不太好听的名字，如 CANDECOMP 与 PARAFAC；最终它被定名为 $T$ 的 CP 分解。

这看起来像是把 SVD 向张量情形的推广，但两者之间存在重要的差别。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原文此处已碎成残片。按文意重建为：这些向量 $\mathbf{a}_r$（对 $\mathbf{b}_r$、$\mathbf{c}_r$ 同理）已不再相互正交。

我们失去了 orthogonal invariance（正交不变性）——正是它曾保证 $Q_1 A Q_2$ 与 $A$ 具有相同的奇异值。

而且 Eckart-Young 定理也不再成立——我们常常并不知道离 $T$ 最近的 rank $R$ tensor（秩 $R$ 张量）到底是哪一个。

张量分解还有别的途径，但迄今 CP 最为有用。

Kruskal 证明了：最接近的秩一张量是唯一的（若它确实存在）。

若改变 $R$，最优的 $\mathbf{a}$、$\mathbf{b}$、$\mathbf{c}$ 也会随之改变。

因此我们面对的是一个全新的问题。

从 computability（可计算性）的角度看，它是 NP-hard（NP 困难）的——除非有朝一日 $P = NP$ 得到证明（那几乎会让所有人震惊），否则它无法在 polynomial time（多项式时间）内求解。

Lim 与 Hillar 证明了：许多听起来更简单的张量问题也属于 NP-hard；于是，exact computation（精确计算）的路径被堵死了。

结论见文献：C. Hillar and L.-H. Lim, “Most tensor problems are NP-hard”, *J. ACM* 60 (2013), Article 45。

我们的目标是找到一种算法，能以相当高效的方式求出向量 $\mathbf{a}$、$\mathbf{b}$、$\mathbf{c}$。

在 tensor computation（张量计算）中，一大步就是尽量接近最优的 CP 分解。

一个简单的想法——alternating（交替）——目前运作得相当好。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 该句 OCR 损坏为「A simple idea @纰 mating / 舅 s 」，依据本页末句及下页 (15) 的循环交替过程重建为 alternating（交替）思想。

整体问题并不 convex（凸），但各个子问题会循环地依次改进 $A$、$B$、$C$；而每个子问题（对 $A$ 的、对 $B$ 的、对 $C$ 的）都是 convex least squares（凸最小二乘）问题。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接 Boyd 凸优化 + 算法视角类比）:**</span> 这一句是全章方法论的核心，而你早已见过同款「整体难、分块易、交替做」模式。把 (14) 代入 $\|T_1-A(C\odot B)^T\|_F^2$ 展开，目标关于 A、B、C 一起是非凸的高次函数，可能有许多局部极小；但固定其中两组后，剩下一组只进入二次项——这正是你在 Boyd 凸优化中遇到的坐标下降/块坐标下降思路：一次只动一块变量、其余冻结，每块子问题须凸且易解，迭代一般能收敛，但非凸情形只保证停在平稳点、不保证全局最优。同一个模式你在 k-means 的 Lloyd 算法里见过：固定中心分点、固定划分更新中心，两半都平凡，合起来却成为解非凸聚类问题的标准方法；概率统计中的 EM 算法同理。三例共同教训：非凸问题没有 SVD 那样一步到位的闭式解（那是凸/可对角化对象的特权），只能靠迭代加好初值逼近。这也解释本页 Lim–Hillar 的 NP-hard 结论与 Strang「相当高效、尽量接近最优」的退让措辞——并预告习题 6（p114）：秩 1 时交替法收敛到全局最优 $\sigma_{1}u_{1}v_{1}^{T}$，一般秩 R 无此保证。

---

## page_110（书页 105：交替步骤 (15)、矩阵化形式、3×4×2 展开例 (16)、Kronecker 回顾）

**

---

> <span style="color:#7f8c8d;">Strang §I.12, p.104</span>

---

<!-- page 110: 书页 105, OCR page 10（正文页） -->

> <span style="color:#7f8c8d;">**页首说明**：本页属节 §I.12 Factoring Matrices and Tensors: Positive and Sparse（分解矩阵与张量：正定与稀疏），为正文页，承接 page_109 的 CP 分解讨论。**结构清单**：① 交替算法与公式 (15)；② 小节 Matricized Form of a Tensor（张量的矩阵化形式）；③ Kolda–Bader 的三路展开示例 (16)；④ 小节 The Khatri-Rao Product（Khatri-Rao 积）与克罗内克积回顾。</span>

现在给出交替（alternating）的算法步骤，见公式 (15)。

<span style="color:#2471a3;">**[note]**</span> (a) 固定 $B$ 与 $C$，只变化 $A$：minimize（最小化）下面的 Frobenius norm（弗罗贝尼乌斯范数）

```math
\min_{A}\ \left\|\,\mathcal{T}_{(1)} - A\,(C \odot B)^{\top}\,\right\|_{F} \tag{15}
```

(b) 固定 $A$ 与 $C$，变化 $B$；(c) 固定 $A$ 与 $B$，变化 $C$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原文 (15) 在 OCR 中残缺（如「Minimize 日 翁 一 A(C 0 B)TII F」，且 (b)、(c) 两项漏写了被固定的 $A$）。此处按交替最小二乘（alternating least squares）的标准过程补全为上述 (a)(b)(c) 三项。

这一 alternating algorithm（交替算法）用到了下面要描述的三种 matricized forms（矩阵化形式）$\mathcal{T}_{(1)}$、$\mathcal{T}_{(2)}$、$\mathcal{T}_{(3)}$。

其中 $C \odot B$ 正是将在公式 (17) 中出现的 Khatri-Rao product（Khatri-Rao 积）。

于是 (15) 就全是矩阵运算了。

### 张量的矩阵化形式（Matricized Form of a Tensor）

设 $A$、$B$、$C$ 是以 (14) 中的向量 $\mathbf{a}_r$、$\mathbf{b}_r$、$\mathbf{c}_r$ 为列的矩阵，每个都有 $R$ 列。

若三阶张量（third-order tensor）$T$ 的维数是 $I \times J \times K$，那么这三个矩阵的大小分别是 $I \times R$、$J \times R$ 与 $K \times R$。

为了能够计算 CP 分解，把张量 matricize（矩阵化）是有好处的。

先从 $I \times R$ 矩阵 $A$ 里把 $\mathbf{a}_r$ 分离出来。

然后寻找一个 $R \times JK$ 的矩阵 $M_1$，使 $A M_1$ 恰好表达 (14) 中那一串秩一张量之和。

$M_1$ 必须由 $\mathbf{b}_r$ 与 $\mathbf{c}_r$ 组合而来。

可一个矩阵乘积 $A M_1$ 如何表达一个三路张量呢？

答案是我们必须先把张量 $T$ unfold（展开）成矩阵 $\mathcal{T}_{(1)}$；做完这一步，就能把 $\mathcal{T}_{(1)}$ 与 $A M_1$ 相互比较了。

<span style="color:#2471a3;">**[example]**</span> Kolda 与 Bader 的一个例子展示了张量如何展开成矩阵。

令 $I \times J \times K = 3 \times 4 \times 2$，于是 $T$ 中共有 24 个数。

$T$ 的 matrix unfolding（矩阵展开）可以是 $3 \times 8$、$4 \times 6$ 或 $2 \times 12$。

因此我们得到三种展开 $\mathcal{T}_{(1)}$、$\mathcal{T}_{(2)}$、$\mathcal{T}_{(3)}$，也就是把 $T$ 沿三种方式 slicing（切片）的结果。

第一种方式：front and back slices（前后切片），尺寸为 $I \times JK = 3 \times 8$：

> <span style="color:#1e8449;">**[note] Note（译者注：unfold 的步长本质与 matricize 的必要性）:**</span> 先把「不复制数据」钉在可复算的事实上：取 `np.arange(1,25).reshape((3,4,2), order='F')`，得到的数组满足 $X[i,j,k]=1+i+3j+12k$（24 个数按列主序编号），而 `X.reshape((3,8), order='F')` 打印出来正是本节 (16) 那张三行八列的表；`X.transpose(1,0,2).reshape((4,6), order='F')` 的首行是 1 2 3 13 14 15，`X.transpose(2,0,1).reshape((2,12), order='F')` 的首行是 1 到 12。三个结果里模态 1 与模态 3 与原数组共用同一块缓冲区（`np.shares_memory` 返回 True），字节步长由 (8,24,96) 变成 (8,24) 与 (96,8)；模态 2 返回 False，因为它要先把两根轴换位再合并，numpy 只能抄一份副本。所以「unfold（展开）并不复制数据」这句得加一个条件：零拷贝当且仅当被压成一根下标的那几根轴在内存序里彼此相邻——模态 1 合并尾部两轴、模态 3 合并前两轴，都相邻；模态 2 要合并的两轴中间隔着一根，只能复制那 24 个数。
> 
> CSAPP §3.8 早把机制讲透了：C 里 A[i][j][k] 的地址 = 基址 + i·(J·K) + j·K + k，多维数组在内存里就是一条行主序的线性序列，「维」只是编译器替你算好的一串乘数。numpy 的免费展开是这条公式反过来用：重新分配各维乘数，同一段内存就换一种切法。列序为什么必须长成那样？因为模态 1 展开要把除 mode-1 以外的指标压成一个下标，而 Kronecker product（克罗内克积）的约定是第一个因子的指标变化最慢；两边一撞，(19) 里 $C\odot B$ 的每一根长列才恰好等于 $c_r$ 与 $b_r$ 的 Kronecker 积，$A(C\odot B)^{\top}$ 才逐元素还原成 $\sum_r a_r\circ b_r\circ c_r$。约定与公式互为因果：改一处列序，另一处必须跟着改。这也是读 (16) 那张表时最该带走的一句——表里的列号等于 $j+Jk$，而不是 $k+Kj$。
> 
> 再说为什么这一步绝非空转。24 个数的信息量固定，访问代价却不固定。取形状 (100,200,300) 的 float64 数组，字节步长是 (480000,2400,8)，一条 64 字节缓存行只装 8 个 double：按最后一维连续遍历，全块共触碰 $100\cdot200\cdot300/8=750000$ 条缓存行；把最后一维挪到最外层、第一维放进最内层，每个元素各占一行，行数涨到 $300\cdot100\cdot200=6000000$，恰好 8 倍。这个倍数不是巧合，它就等于一条缓存行装几个元素。CSAPP §6.5 的局部性原理（时间局部性与空间局部性）在这里换算成一个能手算的整数，而不是一句形容词。张量库因此按下一步要做的矩阵乘来挑展开方向：展开方式决定哪一维连续，连续的那一维决定乘法主循环的访存形状。
> 
> 更根本的一层在代数侧：unfold 之后，CP（canonical polyadic）分解的每个子问题（固定两组因子、求第三组）被摊平成矩阵上的 least squares（最小二乘），而只有矩阵才拥有 SVD（奇异值分解）、pseudoinverse（伪逆）与 normal equations（正规方程）这一整套武器。三阶张量自己一样也没有：它的 rank 虽可定义却难以计算，最佳低秩逼近甚至可能不存在。把这个没有 SVD 的对象搬到有 SVD 的对象上求解，才是「matricize（矩阵化）有好处」这句话的完整份量，也是 (15) 与后续 (18) 到 (24) 全部公式得以写出的前提。史实坐标：这类多项积分解最早由 Hitchcock 在 1927 年提出，见 Journal of Mathematics and Physics 6 卷 164 至 189 页；而展开、CP、Tucker 的统一术语要到 Kolda 与 Bader 的 SIAM Review 51 卷 3 期 455 至 500 页（2009）才定型，那张 1 到 24 的示例表就出自这篇综述。

**

```math
\mathcal{T}_{(1)} =
\begin{bmatrix}
1 & 4 & 7 & 10 & 13 & 16 & 19 & 22 \\
2 & 5 & 8 & 11 & 14 & 17 & 20 & 23 \\
3 & 6 & 9 & 12 & 15 & 18 & 21 & 24
\end{bmatrix} \tag{16}
```

第二种方式：$J \times IK = 4 \times 6$；第三种方式：$K \times IJ = 2 \times 12$——两者包含的仍然是同样的 24 个数。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原书 (16) 的三幅数字阵列在 OCR 中散落（残片如「4 7 10 13 …」「5 8 11 14 …」「6 9 12 15 …」，恰为下表各行去掉首元素）。上面的 $3 \times 8$ 表按 $3 \times 4 \times 2$ 张量（元素按列主序编号 1–24）的模态 1 展开约定重建；$4 \times 6$ 与 $2 \times 12$ 两种展开在译文中只保留尺寸关系。

### Khatri-Rao 积 $C \odot B$（The Khatri-Rao Product $C \odot B$）

第 3 节将引入矩阵 $A$ 与 $B$ 的 Kronecker product（克罗内克积）$K = A \otimes B$。

它包含 $A$ 与 $B$ 中元素两两相乘的全部乘积 $a_{ij} b_{kl}$（所以它可能是个很大的矩阵）。

若 $A$ 与 $B$ 只是 column vector（列向量，分别为 $J \times 1$ 与 $K \times 1$ 矩阵），那么 $A \otimes B$ 就是一根 $JK \times 1$ 的长列。

这根长列先是 $a_{11}$ 乘以 $B$ 的每个元素，然后是 $a_{21}$ 乘以同样的那些元素，最后是 $a_{J1}$ 乘以那 $K$ 个元素。

这样的长列共有 $R$ 根，它们并排组成了 $C \odot B$。

> <span style="color:#1e8449;">**[note] Note（译者注：Khatri-Rao 与完整 Kronecker 的尺寸账）:**</span> 把两种配对哲学换算成可以逐项核对的矩阵。取 $B=\begin{bmatrix}4&1&2\\2&0&1\\1&3&1\\4&1&0\end{bmatrix}$、$C=\begin{bmatrix}3&1&2\\3&0&1\end{bmatrix}$，则 $C\odot B$ 是 8×3：它的第 1 根长列就是 $c_1\otimes b_1$，即 $C$ 第 1 列与 $B$ 第 1 列之 Kronecker product（克罗内克积），逐位算出是 12 6 3 12 12 6 3 12（$3\times4$、$3\times2$、$3\times1$、$3\times4$，因为 $c_1$ 的两个分量都是 3，所以整段重复一遍）。而完整的 Kronecker 积 $C\otimes B$ 是 8×9——Kronecker 把两个尺寸对都乘起来，所以行数是 $KJ$、列数是 $R$ 乘 $R$。原注写「完整 Kronecker 是 $JK\times JK$」，这句要精确化：一般情形下它应是 $JK\times R^{2}$，只有 Tucker decomposition（Tucker 分解）的两侧秩取满、列数涨到 $K$ 与 $J$ 时才落到 $JK\times JK$。量级结论不变，而且能算准：小例子里 24 个元素对 72 个，倍数恰为 $R=3$；取 $J=K=100$、$R=10$，$C\odot B$ 是 $10^{5}$ 个元素，$C\otimes B$ 是 $10^{6}$ 个，倍数仍是 $R$。所以「小一个数量级」不神秘，它就是一个 $R$。
> 
> 为什么 CP（典范多路分解）只需要对角块？回到 (14)：第 $r$ 项是 $a_r\otimes b_r\otimes c_r$，这里的 $\otimes$ 是 outer product（外积）的沿用，与源文式 (14) 的记号一致；原注写成 $\circ$ 又没声明它就是外积，容易被读成 Hadamard product（哈达玛积），故改回 $\otimes$。三个方向被同一个编号 $r$ 强行绑在一起。既然每个分量只用同号的三根向量，(15) 的设计矩阵里就只可能出现「$C$ 的第 $r$ 列对 $B$ 的第 $r$ 列」这种对角配对，永远不会出现 $a_1\otimes b_3\otimes c_2$ 这类交叉项。Khatri-Rao product（Khatri-Rao 积）正是把「只许同号」写成运算：它的第 $r$ 根长列就是 $c_r\otimes b_r$，其余位置根本不存。而 Tucker decomposition（Tucker 分解）放开这个约束，$a_p$ 可以与任意 $b_q$、任意 $c_r$ 组合，于是设计矩阵必须用完整的 Kronecker 积，尺寸从 $JK\times R$ 涨到 $JK\times R^{2}$。
> 
> 记一句口诀：Khatri-Rao 是「对角化的 Kronecker」，对应 CP 的 shared factors（共享因子）；完整 Kronecker 是「任意配对」，对应 Tucker 的自由组合。前者省下的不是精度而是整整一维的存储与乘法——$R$ 根长列对 $R^{2}$ 根长列。这个区别在 (15) 的每个子问题、(17) 的定义式与 (21) 的伪逆恒等式里反复出现，先在脑中把「Khatri-Rao 是 CP 的语言」立住，后面读公式就不会乱。还要记一个方向细节：写作 $C\odot B$ 时 $C$ 在前，而 Kronecker 的约定是第一个因子的指标变化最慢，于是长列的排布是 $k$ 慢 $j$ 快，正好与 (16) 里模态 1 展开的列序配套；换成 $B\odot C$ 就整个反过来。这不是记号洁癖，方向错了 (19) 的三条等式会同时错位。
> 
> 把「几路」也算清楚，才知道省法有多狠。两路时全 Kronecker 的列数是 $R^{2}$，Khatri-Rao 恒为 $R$；三路时 Khatri-Rao 仍是 $R$，全 Kronecker 变成 $R^{3}$。取 $R=10$，就是 10 列对 1000 列——倍数从 $R$ 涨到 $R^{2}$。所以对 $N$ 阶张量，交替最小二乘每一步的设计矩阵是 $N-1$ 个因子的 Khatri-Rao 积，列数恒为 $R$，而「自由配对」的写法要付 $R^{N-1}$ 列。存储差的是指数，不是常数。这也解释了一个常见困惑：为什么张量库宁可写一堆 $\odot$ 也不肯直接展开成一个大矩阵——因为后者在高阶情形下连内存都放不下。
> 
> 史实坐标：这对名字来自统计学家 C. G. Khatri 与 C. R. Rao，Kolda 与 Bader 的综述把出处记为 1968 年 Sankhya 第 30 卷 167 至 180 页，综述本身是 SIAM Review 51 卷 3 期 455 至 500 页，2009 年；该文的原始定义我未能一手核实，只核到综述给出的卷期页码，故按二手引用。Kronecker 积以 Leopold Kronecker 命名，而矩阵 Kronecker 积的行列式定理早于此人另有所出，这层谱系我也未能一手核实，因此只记名字、不编年份。可以确定的是：这套记号让「省掉了哪一维」在公式层面肉眼可见——看到 $\odot$ 就知道只花 $R$ 份存储，看到 $\otimes$ 就要预备 $R^{2}$ 份。

---

## page_111（书页 106：Khatri-Rao 定义 (17)、(18)(19) 矩阵化恒等式、(20) 最小二乘子问题）

**

---

> <span style="color:#7f8c8d;">Strang §I.12, p.105</span>

---

<!-- page 111: 书页 106, OCR page 11 -->

<span style="color:#2471a3;">**[definition]**</span> Khatri-Rao 乘积（Khatri-Rao product）把两个矩阵按列逐一配对相乘：用 $C$ 的第 $j$ 列与 $B$ 的第 $j$ 列相乘，从而得到乘积 $C \odot B$ 的第 $j$ 列。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原文该句噪声严重（“Khatn-Rao”“all a to find column j”“h ave 月 columns”），已按 Khatri-Rao 乘积的标准定义与式（17）重建；OCR 中的 $@$ 统一重建为 Khatri-Rao 积 $\odot$。

```math
\text{column } j \text{ of } (C \odot B) \;=\; (\text{column } j \text{ of } C) \otimes (\text{column } j \text{ of } B) \tag{17}
```

于是，$K \times R$ 的矩阵 $C$ 与 $J \times R$ 的矩阵 $B$ 就生成 $C \odot B$：它共有 $R$ 个长列（long columns），整体尺寸为 $JK \times R$。

> <span style="color:#1e8449;">**[note] Note（译者注：Strassen 算法与矩阵乘张量的秩）:**</span> 把「按编号配对」再看深一层，它连通 CLRS 6.006 的分治与 CLRS 第 4 章讲过的 Strassen algorithm（Strassen 算法）。矩阵乘法 $C=AB$ 本身可编码成一个三路张量：条目 $(i,j,k)$ 描述「$A$ 的第 $(i,k)$ 个元与 $B$ 的第 $(k,j)$ 个元相乘、结果累加到 $C$ 的第 $(i,j)$ 位」。用 $R$ 个 rank-one tensor（秩一张量）之和表示这个张量，恰好等于「用 $R$ 次标量乘法实现这个双线性运算」——一个 $a\otimes b\otimes c$ 就是一次乘法带一串加法。平凡实现逐项做，$2\times2$ 矩阵乘法要 8 次，等价于给出秩 8 的分解；Strassen 找到 7 次的分解，换成张量语言就是那个 $4\times4\times4$ 乘法张量在 CP（canonical polyadic）分解下的秩不超过 7。我用七式在整数 $2\times2$ 上复算过，七个乘积式拼出的结果与 `A@B` 逐位相等。
> 
> 数一数代价才看得清它换到了什么：七式里 10 次预加、8 次后加，合计 7 次乘法加 18 次加减法，而平凡算法是 8 次乘法加 4 次加法。在只计乘法的模型里，乘法次数才是指标，因为它贵得多，而且决定了递归分几支。递推是 $T(n)=7T(n/2)+O(n^{2})$，于是比较 $7^{k}$ 与 $8^{k}$：$n=32$ 时是 16807 对 32768，省掉约一半；$n=1024$ 时是 282475249 对 1073741824，比值 3.80；$n=8192$ 时到 5.67 倍。指数 $\log_2 7\approx 2.8074$，正是教科书里那个 $n^{2.81}$ 的来历。按 CLRS 讲的 master theorem（主定理），$7$ 大于 $2^{2}$，属于递归树主导的情形，所以解就是 $\Theta(n^{\log_2 7})$，而不是 $n^{2}\log n$。
> 
> 但别把 3.80 读成「$n=1024$ 就快 3.8 倍」。那个比值只比了基例个数 $7^{k}$ 与 $8^{k}$，每个基例本身仍然是 $2\times2$ 的 8 次标量乘法。于是 $n=1024$ 时 Strassen 的标量乘法总数是 $7^{10}\times8=2259801992$，而平凡算法是 $2n^{3}=2147483648$——前者反而更多。真正的交叉点在 $4=(8/7)^{k}$ 处，约 $k=10.4$，也就是 $n$ 超过 1334 才开始在纯乘法次数上占优；把 18 次加减法算进去，交叉点还要往后挪。这是「渐近式不能外推到中等规模」最干净的一个例子，也是为什么工程上要用分块与基例大小为 4 或 8 的变体。
> 
> 机制上还要补一句：为什么「秩」能当复杂度用。双线性映射的 rank 定义为最少的秩一线性型个数，而每个秩一线性型就是一次乘法加若干加法，加法次数不在定义里。这个模型的天然边界也在这里：它只算乘法，不算加法与访存，所以秩低不等于跑得快，Strassen 在实用规模上常因加法与缓存而反超失败（它的加减法总量是 $O(n^{2.81})$ 量级而常数很大，平凡算法的加法只有 $n^{3}$ 次，两者的常数在中等规模上互相咬住）——这解释了为什么它长期是课堂主角、库里的配角。同样的思路后来换了主角：communication-avoiding（通信避免）算法把带宽而不是乘法当主成本，见 Ballard、Demmel、Holtz、Schwartz 的 SIAM Journal on Matrix Analysis and Applications 32 卷 3 期 866 至 901 页，2011 年。
> 
> 史实坐标：Strassen 的论文题为 Gaussian elimination is not optimal，刊于 Numerische Mathematik 13 卷 4 期 354 至 356 页，1969 年 8 月，DOI 10.1007/BF02165411——标题本身就在宣告「高斯消元不是最优」这个当年的禁忌。至于「判张量秩很难」，Hillar 与 Lim 在 Most Tensor Problems Are NP-Hard 一文里把张量秩等一批问题证成 NP-hard（NP 困难），见 Journal of the ACM 60 卷 6 期文章 45，2013 年；它把「计算的真实代价」与「一个代数不变量」绑在同一根绳上，这才是本节读起来像线性代数、实际却在讲算法下界的原因。CP 秩、Khatri-Rao 与 CP 分解，就是描述这类计算结构的通用语言。

---

## page_112（书页 107：伪逆恒等式 (21)、更新式 (22)、Tucker 分解 (23)(24)、HOSVD）

**

小结（Summary）：张量 $T$ 由式（14）的和式近似，即 $T \approx \sum_{i=1}^{R} a_i \circ b_i \circ c_i$。

我们把 $T$ 沿三个方向切片（slicing），并把各切片并排放进三个矩阵 $T_1, T_2, T_3$（即三种矩阵化形式）之中。

接下来我们寻找三个矩阵 $M_1, M_2, M_3$，使它们按普通矩阵乘法（ordinary matrix multiplication）给出近乎正确的等式（18）：

```math
T_1 \approx A M_1, \qquad T_2 \approx B M_2, \qquad T_3 \approx C M_3 \tag{18}
```

回想矩阵 $A$ 是 $I \times R$ 的，而 $T_1$ 是 $I \times JK$ 的，所以正确的 $M_1$ 必须是 $R \times JK$ 的矩阵。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原文 “Rec all th at is by R, with columns 01 t0 翁 is / by JK” 语句残破，此处按维数相容性 $I \times JK = (I \times R)(R \times JK)$ 重建。

这个 $M_1$ 由 $B$、$C$ 两矩阵以列向量 $b_i$ 与 $c_k$ 构造出来。

$M_1$ 正是 Khatri-Rao 乘积 $C \odot B$（尺寸 $JK \times R$）的转置（transpose）。

$C \odot B$ 的第 $i$ 列取自 $C$ 与 $B$ 各自的第 $i$ 列，其中 $i$ 从 $1$ 取到 $R$。

该列包含全部 $JK$ 个乘积 $c_{ki}$ 与 $b_{ji}$，这里 $1 \le k \le K$ 且 $1 \le j \le J$。

因此 $C \odot B$ 收集了 $c_{ki}$ 与 $b_{ji}$ 的全部 $JKR$ 个乘积，这些乘积来自 $C$ 与 $B$ 的第 $i$ 列，$i = 1, \ldots, R$。

至此，$T$ 的三个矩阵化形式（matricized forms）$T_1, T_2, T_3$ 都被表示为近似矩阵乘积。

Khatri-Rao 的定义正是为了使等式（19）成立而设计的：

```math
T_1 = A (C \odot B)^T, \qquad T_2 = B (C \odot A)^T, \qquad T_3 = C (B \odot A)^T \tag{19}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 只识别出（19）的后两项（写作 “T B(C @A)T”“C(B @ A)T”）并把 $\odot$ 误识为 $@$，首项 $T_1 = A(C \odot B)^T$ 依据前文 $M_1 = (C \odot B)^T$ 的结论补齐。

<span style="color:#2471a3;">**[section]**</span> **计算 $T$ 的 CP 分解（Computing the CP Decomposition of $T$）**

我们的目标，是求出近似式（14）中对张量 $T$ 做逼近所用的全部 $a$、$b$ 与 $c$。

计划采用交替最小化（alternating minimizations）：当矩阵 $B$、$C$ 里的 $b$、$c$ 被固定时，我们就对 $A$ 里的 $a$ 求解一个线性最小二乘（linear least squares）问题。

先把 $T$ 放进它的矩阵化形式 $T_1$，这个矩阵是 $I \times JK$ 的。

由式（19），我们瞄准 $T_1 = A (C \odot B)^T$——它是 $I \times R$ 与 $R \times JK$ 两个矩阵相乘的结果；这一步先固定 $B$ 与 $C$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 行 “aiming for 翁 (C @ B)T = @ × 娓）（娓 × (K)” 系该乘积的两个维数因子被打乱，按矩阵乘法维数相容重建。

选取最佳的 $A$，使下列范数误差（20）取到最小值：

```math
\min_{A}\; \bigl\| T_1 - A (C \odot B)^T \bigr\|_F^2 \tag{20}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 行 “Choose th e best in 日 翁 一 (C @ B)TII%” 中的 “日” 与 “II%” 分别是范数竖线及其下标 $F$ 的误识，重建为 Frobenius 范数的平方。

这里 $C \odot B$ 是 $JK \times R$ 的系数矩阵（coefficient matrix），它逐列作用到 $A^T$ 的各列上。

在 Frobenius 范数（Frobenius norm）度量下，我们得到 $I$ 个独立的普通最小二乘问题来求 $A$：对 $A^T$ 的每一列（即 $A$ 的每一行）各有一个问题。

> <span style="color:#1e8449;">**[note] Note（译者注：转置与逐列解耦：把多输出回归拆成 I 个单输出回归）:**</span> 这里「$A$ 的行才是未知数」读着别扭，背后是一个值得固化的化简模板：未知在左，转置，再按列解耦。关键在 Frobenius norm（弗罗贝尼乌斯范数）的可分离性：$\lVert X\rVert_F^{2}$ 是全部元素平方和，等于各行欧氏范数平方之和，所以 (20) 能按 $T_1$ 的行拆成 $I$ 个互不干扰的回归，而 $C\odot B$ 作为 design matrix（设计矩阵）被所有行共享。对照 Strang 18.06 的最小二乘：$Ax=b$ 里未知向量在系数矩阵右侧；这里未知的 $A$ 左乘系数矩阵。解药是转置，(20) 等价于 $\lVert (C\odot B)A^{\top} - T_1^{\top} \rVert_F$ 的最小化，令 $A^{\top}$ 的每一列为未知量，就还原成「设计矩阵乘未知向量约等于观测向量」的标准形，每列独立走 normal equations（正规方程），共享同一个系数矩阵。
> 
> 这一步为什么非平方不可？因为只有元素平方和才按行加成。换成 $\ell_1$ 型目标或最大范数，各行立刻耦合，$I$ 个小问题会塌回一个大的——「Frobenius 的平方」不是审美，而是解耦成立的充要条件。统计上的读法也要写清楚：$T_1$ 的 $I$ 行是 $I$ 个样本，每个样本有 $JK$ 个由 $B$、$C$ 编码出的特征，要拟合 $R$ 个权重，未知量是 $A^{\top}$ 的列，也就是 $A$ 的行。所以「期望 $C\odot B$ 满列秩、$JK\ge R$」绝非细节：共享设计矩阵要 full column rank（列满秩），解才唯一；三路分别要求 $JK$、$IK$、$IJ$ 都不小于 $R$，正是每个方向样本量都充足的 identifiability（可识别性）条件。
> 
> 拿一组数验证。取 $I=6$、$J=5$、$K=4$、$R=3$，用随机 $A$、$B$、$C$ 造出精确满足 (19) 的 $T_1$，再反求 $A$：整块最小二乘与按行循环调 `np.linalg.lstsq` 两条路，最大元差 3.3e-16，即机器精度内一致。此时 $C\odot B$ 是 $20\times3$，列秩 3，$JK=20$ 远大于 $R=3$，秩条件宽裕。这组数说明逐列解耦不是近似技巧而是恒等变形——两条路算的本来就是同一个解，只是把一个大问题切成 $I$ 个小问题后，每个小问题的设计矩阵从 $JK$ 列降到 $R$ 列，代价反而下降。
> 
> 反过来把秩条件踩破，才看得见它在管什么。取 $J=K=2$、$R=5$，于是 $JK=4<R=5$：$C\odot B$ 只有 4 行 5 列，必不满秩。此时 $A$ 的解不唯一，最小范数解能把残差压到 5.0e-16，因为 $T_1$ 精确落在列空间里；但它与生成数据的真实 $A$ 相差 1.2957。这是可识别性失效最干净的数值例子：残差为零不等于解对了。模型把 5 维因子塞进 4 维观测，信息在形成 $T_1$ 那一步就已经丢掉，交替最小化迭代多少轮都找不回来，它只会诚实地停在某个零残差的等价解上。
> 
> 史实坐标与一句提醒。把「固定两组、只解一组」轮流做下去，1966 年 Tucker 的三模态因子分析里已有同一骨架，1970 年心理测量学又从两条独立路线把它重新命名为 CANDECOMP 与 PARAFAC；这两条 1970 年命名线的原始文献我未能一手核实，只确认 Tucker 那篇刊于 Psychometrika 31 卷 3 期 279 至 311 页。真正该记住的教训不在年份，而在上一条数值：alternating least squares（交替最小二乘）只保证目标函数单调下降，不保证落到生成数据的那组因子，收敛点与真实因子之间隔着一个由秩条件决定的等价类。下一节的伪逆恒等式正是为了把这个等价类里「最好」的那一点用闭式写出来。

**

请注意：$A$ 并不处在最小二乘通常的位置 $Ax = b$——$A$ 的行才是未知数（unknowns）！

系数矩阵是 $C \odot B$（而不是 $A$ 本身）；我们期望该矩阵满列秩（full column rank），因此要求 $JK \ge R$。

类似地，当未知数轮流换成 $B$ 与 $C$ 时，我们分别需要 $IK \ge R$ 与 $IJ \ge R$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原文末句秩条件处乱码（“We expect that m atrix to be 囿 1 and thi n, with JK 之”），此处按最小二乘解唯一所需的满列秩条件重建。

---

> <span style="color:#7f8c8d;">Strang §I.12, p.106</span>

---

<!-- page 112: 书页 107, OCR page 12 -->

<span style="color:#2471a3;">**[section]**</span> **§I.12 Factoring Matrices and Tensors：Positive and Sparse（矩阵与张量的分解：正定与稀疏）**

最小二乘问题 $Ax = b$ 的解由伪逆（pseudoinverse）给出：$x = A^{+}b$。

若该矩阵具有独立列（这是最小二乘通常假设的情形），则 $A^{+}$ 是矩阵 $A$ 的左逆（left inverse）$(A^T A)^{-1} A^T$。

在这里，你会在求最佳 $\hat{x}$ 的通常正规方程（normal equations）中看到系数矩阵 $A^T A$。

而在我们的情形中，那个系数矩阵并不是 $A^T A$，而是 Khatri-Rao 乘积 $C \odot B$。

幸运的是，我们的系数矩阵 $C \odot B$ 的伪逆可以表达为（21）：

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 在式（21）处仅残留行号而无公式内容；此处按下一句“预先构造 $C^T C$ 与 $B^T B$（$R \times R$ 矩阵）”以及 Hadamard 积说明重建出恒等式 $(C \odot B)^T (C \odot B) = (C^T C) * (B^T B)$，并据此给出满列秩情形下的伪逆。

```math
(C \odot B)^{+} \;=\; \bigl[ (C^T C) * (B^T B) \bigr]^{-1} (C \odot B)^T \tag{21}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原文 “CT 0” 与 “BTB” 系 $C^T C$、$B^T B$ 的识别残缺；符号 “$.*$”（有时写作 $\ast$）表示逐元素乘积（element-by-element product），即 Hadamard 积（Hadamard product）。

这一公式借用自 Kolda 与 Bader 的方程（2.2）。

它使我们能够预先构造 $C^T C$ 与 $B^T B$（二者都是 $R \times R$ 的矩阵）。

> <span style="color:#1e8449;">**[note] Note（译者注：伪逆恒等式 (21)：为什么是 Hadamard 积，以及复用到哪一步）:**</span> 先把恒等式推一遍，形式为什么是 Hadamard product（Hadamard 积）而不是 Kronecker 积就一清二楚。$C\odot B$ 的第 $(kj,r)$ 个元是 $c_{kr}b_{jr}$，于是 $(C\odot B)^{\top}(C\odot B)$ 的第 $(s,r)$ 个元是对全部 $j,k$ 求和 $c_{ks}b_{js}c_{kr}b_{jr}$；这个和能拆成两组独立求和之积，$\sum_k c_{ks}c_{kr}$ 与 $\sum_j b_{js}b_{jr}$，前者是 $(C^{\top}C)_{sr}$，后者是 $(B^{\top}B)_{sr}$。两组求和之所以能分离，正因为 Khatri-Rao 只让同号列配对，$k$ 与 $j$ 之间没有任何交叉耦合。换成完整 Kronecker 积，同一位置会得到 $(C^{\top}C)\otimes(B^{\top}B)$，是 Kronecker 而非 Hadamard，尺寸也从 $R\times R$ 涨到 $R^{2}\times R^{2}$。
> 
> 数值上我核过两处：取 $B$ 为 $7\times3$、$C$ 为 $5\times3$，左式与右式的最大元差 1.78e-14，而矩阵元量级是 52.75，相对误差 3.4e-16，就是机器精度；再把 (22) 算出的 $A$ 与 `np.linalg.lstsq` 的解比，最大元差 2.0e-15。也就是说 (21) 与 (22) 不是近似公式而是恒等式：只要 $C^{\top}C$ 与 $B^{\top}B$ 都可逆，也就是两个因子矩阵各自列满秩，伪逆就长成这个形状。这里顺手记一个隐患：Hadamard 积的秩可以低于两个因子秩之积，所以两边都列满秩也不保证右端可逆，实现里常给它加一个很小的对角扰动。
> 
> 复杂度账要算准：设 $G=C\odot B$ 是 $JK\times R$。朴素地先形成 $G$ 再算 $G^{\top}G$，成本按 $JK\cdot R^{2}$ 计；而 $C^{\top}C$ 只要 $O(K\cdot R^{2})$、$B^{\top}B$ 只要 $O(J\cdot R^{2})$，两者逐元素相乘 $O(R^{2})$，合计 $(J+K)R^{2}$。取 $J=K=1000$、$R=10$，前者 $10^{8}$，后者 $2\times10^{5}$，差 500 倍。原注说「交替循环里没变的那个 Gram matrix（格拉姆矩阵）可直接沿用，例如 $B^{\top}B$」，这个例子举错了：第 (a) 步求 $A$ 用 $B^{\top}B$，可第 (b) 步结束时 $B$ 已经换成新值，第 (c) 步求 $C$ 必须重算它。真正能沿用的是本步固定因子那一个——第 (a) 步算出的 $C^{\top}C$ 到第 (b) 步仍然有效。一轮三步里 Gram 矩阵从 6 次降到 4 次，省三分之一。
> 
> 预构造与复用之外，真正的性能点在这条：整轮里唯一必须接触大矩阵 $T_1$ 的操作，是 (22) 里的 $T_1(C\odot B)$，成本约为 $O(I\cdot JK\cdot R)$，即张量规模乘 $R$，随输入线性增长——这才是 ALS（alternating least squares）能用于大型张量的复杂度基础。CSAPP §6.5 的局部性原理在这里是代数版：把对大数据 $T_1$ 的反复访问，换成对 $R\times R$ 小矩阵的运算，小矩阵常驻缓存，命中率接近 1；工程上还会再把 $T_1$ 按块流式读一遍，不留第二轮扫描。下次看到「把大结构拆成可复用小块的恒等式」，先问一句：它把哪一次随大矩阵规模长大的 $O(N)$ 运算，换成了只依赖 $R$ 的 $O(R^{2})$ 运算？
> 
> 顺带把 (22) 的形状核对一遍，这一步最容易写反。$T_1$ 是 $I\times JK$，$(C\odot B)$ 是 $JK\times R$，两者相乘得 $I\times R$；再右乘 $R\times R$ 的 $(C^{\top}C)*(B^{\top}B)$ 之逆，仍是 $I\times R$，正好是 $A$。若把逆矩阵写在左边，$R\times R$ 乘 $I\times R$ 在 $I\ne R$ 时连维度都对不上——左乘还是右乘不是书写习惯，是维数相容性逼出来的唯一选择。这也顺带说明一件事：$A$ 的每一行确实是由一次独立回归得到的一行系数，整块公式只是把这 $I$ 次求解并排写在一起。
> 
> 史实坐标：原文说这条借自 Kolda 与 Bader 的方程 (2.2)，该综述是 SIAM Review 51 卷 3 期 455 至 500 页，2009 年；恒等式本身的原始出处我未能一手核实，只能确认它在当代文献里被当作 Khatri-Rao product（Khatri-Rao 积）的标准性质使用，而 Kronecker 版的对应式 $(A\otimes B)^{\top}(A\otimes B)=(A^{\top}A)\otimes(B^{\top}B)$ 更古老。这一对式子的对照本身就是本页最值钱的一句：同一个「转置乘自己」的动作，在 Khatri-Rao 上塌成逐元素积，在 Kronecker 上仍是 Kronecker。

**

取转置后，固定 $B$ 与 $C$ 的最小二乘问题（20）由下列矩阵（22）求解：

```math
A \;=\; T_1 (C \odot B) \bigl[ (C^T C) * (B^T B) \bigr]^{-1} \tag{22}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 在式（22）处同样仅残留行号，此处由 “Transposing, the least squares problem (20) with fixed B and C is solved by the matrix” 一句并按 $A^T$ 逐行独立求解的语境重建（满列秩情形）。

下一步，我们借助这个 $A$ 连同 $C$ 去求最佳 $B$。

交替算法（alternating algorithm）的一个循环（cycle）以如下步骤收尾：将 $A$ 与 $B$ 固定在其新值上，求出最佳 $C$。

<span style="color:#2471a3;">**[section]**</span> **Tucker 分解（The Tucker Decomposition）**

SVD 把一个矩阵（即一个 $2$-张量）分解为 $A = U\Sigma V^T$，其中 $U$ 与 $V$ 的列是标准正交（orthonormal）的。

对更高阶的张量而言，那种分解通常是不可能的。

这正是 CP 逼近——以及现在的 Tucker 逼近（Tucker approximation）——存在的缘由。

Tucker 分解允许 $P$ 个列向量 $a_p$、$Q$ 个列向量 $b_q$ 与 $R$ 个列向量 $c_r$。

它只允许 $PQR$ 个秩一张量（rank-one tensors）$a_p \circ b_q \circ c_r$ 出现。

> <span style="color:#1e8449;">**[note] Note（译者注：CP 与 Tucker 的核心张量：对角核与满核）:**</span> CP 与 Tucker 之差，用你已滚瓜烂熟的 SVD（奇异值分解） 一句话讲清：矩阵 $A=U\Sigma V^{\top}$ 若只允许「秩一乘对角核」，就是 SVD 形态 $\sum_m \sigma_m u_m\circ v_m$——第 $m$ 个左奇异向量只与同号第 $m$ 个右奇异向量配对。我拿 $3,1;0,2$ 这个 $2\times2$ 验过：奇异值是 3.256617 与 1.842403，两项秩一之和复原 $A$ 的误差在 $10^{-15}$ 量级，一个分量都不多。这就是「对角核」在矩阵情形的全部含义。
> 
> 若把 $\Sigma$ 换成任意矩阵 $M$，也就是满核，$A=UMV^{\top}$ 就允许任意 $u_i$ 与任意 $v_j$ 配对、权重 $m_{ij}$——这是 Tucker 的语言。张量版一一对应：CP (14) 是共享因子加对角核心，第 $r$ 个 $a$ 只和同号 $r$ 的 $b$、$c$ 组合，总共只有 $R$ 项；Tucker (23) 的核心张量 $G$ 是完全的三路数组，$a_p$ 可与任意 $b_q$、任意 $c_r$ 组合，最多 $PQR$ 项，且 $P$、$Q$、$R$ 可以互不相同。多出来的自由度不是装饰，它决定了下一段要说的正交性能否实现。
> 
> 「对角核」这三个字可以量出来。随机造一个 $2\times2\times2$ 张量做 HOSVD（高阶奇异值分解）：沿三个方向各取一次左奇异向量，再把张量投影到它们上，得到 8 个核元素，实测为 -3.186、0.0018、0.0019、0.7997、0.0069、0.1357、0.1194、0.0271——两个大的之外其余非零但很小，重构误差 1.3e-15。再把同一流程用在秩一张量 $a\circ b\circ c$ 上：8 个核元素里只有 1 个非零，其余停在 1e-17 量级。所以「CP 等于对角核心」的精确含义不是「核很小」，而是「核的非零项只有 $R$ 个」——Tucker 的 $PQR$ 项里有 $PQR-R$ 项本该为零却在实际数据上不为零，那些残留就是 CP 与 Tucker 之间的全部差额。
> 
> 那些自由度换来什么？换来 $a$、$b$、$c$ 可以各自正交——核吸收因子间的冗余相关性，正如 $\Sigma$ 之外 $U$、$V$ 可以正交。由此得到 HOSVD：对每个方向分别做一次截断、也就是一次主成分提取，堪称张量版 principal component analysis（主成分分析）。代价是参数更多、核 $G$ 未必可解释：$PQR$ 个核元素里通常只有少数几个大，其余是噪声级的非零值，读起来比 $R$ 个分量啰嗦得多。选型法则可记：要可解释选 CP，要数值稳定与压缩选 Tucker 与 HOSVD。这条法则不是口味问题，它对应两种不同的「秩」定义——CP 秩数分量个数，Tucker 秩数每个方向的维数。
> 
> 还要分清一个会让人在实践里吃亏的区别：HOSVD 给的是「正交因子加满核」，它把每个方向的最优基各自取好，但截断后的 HOSVD 并不是最佳 Tucker 逼近。矩阵情形有 Eckart 与 Young 的定理兜底，截断 SVD 就是最佳低秩逼近；张量情形没有这条保证，要拿到最佳逼近得用高阶正交迭代反复刷新因子。记成一句：HOSVD 是一次算完的初始化，高阶正交迭代是反复校准的求解，随机化方法又是另一个量级；三者共用同一套张量乘与 Khatri-Rao 工具，选哪个取决于要速度、精度还是可解释。
> 
> 最后一层要交代清楚：为什么对更高阶张量，那种分解通常是不可能的。矩阵情形里「秩一分解加正交约束」能同时满足，靠的是截断 SVD 保证最优逼近存在；张量的秩 $R$ 逼近集合却不封闭，存在根本没有最佳逼近的张量，正交性更无法与对角化同时达成。史实坐标：Tucker 的三模态论文刊于 Psychometrika 31 卷 3 期 279 至 311 页，1966 年；HOSVD 由 De Lathauwer、De Moor 与 Vandewalle 在 SIAM Journal on Matrix Analysis and Applications 21 卷 4 期 1253 至 1278 页，2000 年确立；多项积分解本身可追到 Hitchcock 1927 年发表于 Journal of Mathematics and Physics 6 卷 164 至 189 页。三个年份对应三种野心：分解存在、分解正交、分解唯一。

---

## page_113（书页 108：小结——tensor train、CURT、随机化分解）

**

维数为 $P \times Q \times R$ 的核心张量（core tensor）$G$ 决定这些组合中的系数：

```math
T \;=\; \sum_{p=1}^{P} \sum_{q=1}^{Q} \sum_{r=1}^{R} g_{pqr}\, a_p \circ b_q \circ c_r \tag{23}
```

借助 $G$ 中这份额外的自由度——在 CP 分解里 $G$ 只是一个对角张量（diagonal tensor）——我们可以要求 $a$、$b$、$c$ 构成标准正交组。

于是 Tucker 分解是 $PQR$ 个秩一张量的组合，而不再只有 $R$ 个。

请记住（23）是逼近式（approximation）而非等式；它可推广到 $d$-路（$d$-way）张量。

三路情形有一个矩阵化形式：其中 $T_1, T_2, T_3$，以及类似地 $G_1, G_2, G_3$，正是式（16）中的展开矩阵（unfolding matrices）。

（14）中的 CP 矩阵换成了 Tucker 矩阵，而现在我们得到的是 Kronecker 积（Kronecker products），不再是 Khatri-Rao 积：

```math
T_1 = A G_1 (C \otimes B)^T, \qquad T_2 = B G_2 (C \otimes A)^T, \qquad T_3 = C G_3 (B \otimes A)^T \tag{24}
```

高阶奇异值分解（higher-order SVD，HOSVD）是一种特殊的 Tucker 分解。

它的性质与计算在 De Lathauwer 的著作中有最好的说明。

---

> <span style="color:#7f8c8d;">Strang §I.12, p.107</span>

---

<!-- page 113: 书页 108, OCR page 13 -->

> <span style="color:#7f8c8d;">书眉（页眉重复元素，不译）：Highlights of Linear Algebra。本页为正文页 —— §I.12 的章节小结（Highlights）页，书页 108。</span>

### 大张量的分解与随机化（Decomposition and Randomization for Large Tensors）

本节先概述了用 tensor（张量）进行数值计算所需的基本步骤（basic steps）。现实数据多以 matrix（矩阵）或 tensor（张量）的形式出现，因此这些步骤是张量计算的起点。本节最后介绍两个较新的构造（newer constructions），并列出参考文献（references）供进一步阅读。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 受损严重（"basic s tep S ... Data is a v ing or form ... since (P)"），句子内容依据数学与版面语境重建；"since (P)" 疑为年代乱码，无法确定，略去不译。

#### 1. Tensor decomposition（张量分解，Oseledets 与 Tyrtyshnikov）

<span style="color:#2471a3;">**[section]**</span> 该工作的核心问题是如何处理高阶张量（higher-order tensors）。完整的 CP decomposition（CP 分解）把张量近似写成若干 rank-one tensor（秩一张量）之和；但当维数 $d$ 很大时，CP 分解会变得不可行（unworkable）。一个更好的想法是先把张量化为一串三路张量（train of 3-way tensors），随后 linear algebra（线性代数）与 CP 分解就都可以在这种 tensor train（张量列）格式中运作。

> <span style="color:#1e8449;">**[note] 译者注（算法/效率视角：维数灾难的破解）:**</span> 高阶张量最直接的敌人是维数灾难：每维 n 个数时，存整张 T 要 $n^{d}$ 个条目——n=100、d=10 就是 $10^{20}$，远超任何内存（CSAPP：内存是物理现实，不是无穷数组）。CP 在高维失效不只是因为秩难定：d 大时「整组共享因子」的格式太僵硬，收敛与数值稳定都成问题。TT（张量列）的处方是把 d 路张量「化整为零」成一串小块：每个结点至多是三路的（形如 r×n×r 的「转移」张量），整条链参数 ≈ O(d·n·$r^{2}$)，随 d 线性增长而非指数爆炸——代价是只保留「相邻结点间的耦合」，远处相关性须通过链逐步传播。这正是 6.006 分治思想在线性代数里的极致形态：不在整个 d 维对象上做运算，而是沿链做局部张量乘法再收缩。它也更新一个观念：低秩对象不一定是一堆整体秩一张量之和，也可以是「一长串小张量的乘积」——物理学的矩阵乘积态、机器学习的 tensor networks 正是从这里起步。见到「指数数据量 + 结构假设」时，先想：能不能把全局结构拆成链或树上相邻的局部结构？

**

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "t0 handle way tensors" 缺词，依 tensor train（张量列）分解处理高维张量的动机重建为"高阶张量"；"a 田 n Of 3-way tensors ... tensor trai n format" 中的 "田 n" 依上下文重建为 train（串/链）。

#### 2. CURT decompositions（CURT 分解，Song、Woodruff 与 Zhong）

<span style="color:#2471a3;">**[section]**</span> 该构造是关于 tensor（张量）的 low-rank approximation（低秩近似）：要在相对误差意义下计算一个低秩张量，使其尽量接近由 SVD 与 Eckart-Young 定理（Eckart-Young Theorem）界定的最优逼近。对 matrix（矩阵）而言，这一目标可以由 singular value decomposition（SVD，奇异值分解）与 Eckart-Young 定理在任意精度下实现；但对 tensor（张量）并没有现成的 SVD 可用。相关计算转而建立在 column-row CUR approximation（列-行 CUR 逼近）（见 §II.3）的基础上，并配以一个随机化或选主元的因子来完成。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原文 "This paper tO compute a rank tensor within Of the closest to 丆·0) by th e SVD an d th e Eckart-Young Theorem" 严重断裂，依 Eckart-Young 定理与低秩逼近的语境重建；"with a 沅 g or U" 无法辨认，依 Song-Woodruff-Zhong 的随机化 CUR 算法语义重建。交叉引用编号 OCR 为 "Section 111.3"，此处解读为 §II.3。

该算法以接近最优的步数逼近目标，即步数与 $T$ 中 nonzero（非零元）的个数成正比。它使用了 randomized factorization（随机化分解）——处理超大规模计算的有力工具（见 §II.4）。可以说，tensor（张量）正处在 numerical linear algebra（数值线性代数）研究的最前沿（frontier）。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接 Bertsekas 概率 / CLRS 随机算法）:**</span> CURT 的两个设计动机值得点破。(1) 可解释性：SVD 的奇异向量是全数据线性组合出的「合成特征」，丢掉原始语义；CUR（列-行逼近，见 §II.3）直接挑选原张量里的真实列与行，逼近误差仍受 Eckart-Young 型最优界框住，却保留「哪些原始维度重要」的可读性——数据科学里这叫代表性样本（Mahoney 等的工作正源于此）。(2) 随机化：超大规模下给每列算一遍精确权重太贵，于是用随机投影或随机采样估计列的重要度（常见代理是列范数加权抽样），再按概率抽列。这里的误差分析正是你正在学的概率论：抽样是一次随机试验、期望给出无偏估计；「万一抽偏」的概率要用尾界控制（6.042 与 Bertsekas 概率中的 Chebyshev/Chernoff 型不等式），最终以高概率给出 (1+$\epsilon$) 相对误差——Song–Woodruff–Zhong 的标题 Relative Error 正指此。算法步数按 T 中非零元计数，呼应「稀疏 = 便宜」：只扫一遍非零元，逼近信息论下界。这是 CLRS §35「牺牲最优、换取可行」的近似哲学在数值线性代数前沿的翻版，也是 NMF/稀疏正定这些「正定与稀疏」主题背后的动机。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "The algorithm comes near the goal of z steps: equal to the number of nonzeros in T" 中 "z steps" 依算法复杂度语义重建为"步数与 $T$ 中非零元个数成正比"；交叉引用 "Section 11.4" 按罗马数字解读为 §II.4。

---

### 参考文献（References）

> <span style="color:#7f8c8d;">以下为本节引用的文献；按学术惯例，文献条目与题名保留英文原文，仅修正 OCR 造成的拼写与卷期页码噪声。</span>

1. T. Kolda and B. Bader, *Tensor Decompositions and Applications*, SIAM Review 52 (2009) 455–500.
2. M. Mahoney, M. Maggioni, and P. Drineas, *Tensor-CUR Decompositions for Tensor-Based Data*, SIAM J. Matrix Analysis Appl. 30 (2008) 957–987.
3. B. Bader and T. Kolda, MATLAB Tensor Toolbox, version 2.2 (2007).
4. C. Andersson and R. Bro, *The N-Way Toolbox for MATLAB* (2000).
5. R. A. Harshman, http://www.psychology.uwo.ca/faculty/harshman
6. P. Paatero and U. Tapper, *Positive Matrix Factorization*, Environmetrics 5 (1994) 111–126.
7. D. D. Lee and H. S. Seung, *Learning the Parts of Objects by Non-negative Matrix Factorization*, Nature 401 (1999) 788–791.
8. L. De Lathauwer, B. de Moor, and J. Vandewalle, *A Multilinear Singular Value Decomposition*, SIAM J. Matrix Anal. Appl. 21 (2000) 1253–1278 and 1324–1342, and more recent papers on tensors.
9. S. Ragnarsson and C. Van Loan, *Block Tensors and Symmetric Tensors*, SIAM J. Matrix Anal. Appl. 33 (2013) 149–169; arXiv:1101.2005, 2 Oct 2011.
10. C. Van Loan, www.alm.unibo.it/~simoncin/CME/vanloan1.pdf–vanloan4.pdf
11. I. Oseledets, *Tensor-Train Decomposition*, SIAM J. Sci. Comp. 33 (2011) 2295–2317.
12. Z. Song, P. Woodruff, and P. Zhong, *Relative Error Tensor Low Rank Approximation*, arXiv:1704.08246, 29 Mar 2017.
13. P. Grinfeld, *Introduction to Tensor Analysis and the Calculus of Moving Surfaces*, Springer (2013).

---

> <span style="color:#7f8c8d;">Strang §I.12, p.108</span>

---

<!-- page 114: 书页 109, OCR page 14 -->

> <span style="color:#7f8c8d;">本页为 Problem Set I.12（习题集 I.12）…保留英文原文。书页 109 以双栏排印并含插图，OCR 将栏序与图内文字混排；题号与题干依「最小化 $\|A-UV\|_F^2$、秩一逼近、交替最小化、SVD、最小二乘」的数学语境重建，细节不确定处均已加绿色译者注，请对照原 PDF 校正。</span>

### 习题集 Problem Set I.12：Factoring Matrices and Tensors: Positive and Sparse（矩阵与张量分解：正定与稀疏）

The first 5 questions are about minimizing $\|A - UV\|_F^2$ when $UV$ has rank 1.

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.** Minimize $\|A - UV\|_F^2$ when $UV$ has rank 1.（原题附图：平面上的点列与一条候选直线。）Look at the first column of $A - UV$, with $V$ and $U$ fixed:

- (a) Minimize the squared error $(a - 1)^2 + (b - \mu)^2 + 2b$ over the free number（附图给出该列的位置）。
- (b) Show by calculus that the minimizing number $\mu$ satisfies the equation $(1+2)\mu = \cdots$（右端由图中的坐标读出）。
- (c) In vector notation, $a_1 = \mu u_1 + e_1$, where $u_1$ is column 1 of $U$ and $e_1$ is the error vector.
- (d) Which point $p$ in this picture minimizes $\|a_1 - p\|_2$?
- (e) The error vector $a_1 - \mu u_1$ is orthogonal to the line. From that fact, find again the number $\mu$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本题受图形与两栏混排影响，OCR 高度碎片化（"目 一 UVII%"、"一 UV with an d U fixed"、"(a 一 1）2 + (b 一 伽 2"、"has 1 + 2）伽"、"．1 = OI where is CO lumn 1 Of" 等），以上按"固定 $U$、对第一列分量最小化，最小二乘给出 $\mu = u_1^T a_1/(u_1^T u_1)$"的秩一逼近语境重建；括号内具体数值得不到 OCR 支持，请对照原图核验。

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.** The second column of $A - UV$ is $a_2 - \mu_2 u_2$（when $U$ is fixed, rank 1）。Minimize $\|a_2 - \mu_2 u_2\|_2^2$ over $\mu_2$; which number minimizes it? Solve the normal equation $\mu_2 (u_2^T u_2) = u_2^T a_2$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "The second colu 灬 of 一 UV"、"2 = 02 一 2"、"S Olve S（）鬱 = QJT" 均断裂，按与 Problem 1 相同的最小二乘步骤重建（正规方程 $u^T u\,\mu = u^T a$）。

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.** Vector form. The best numbers $\mu_1, \mu_2$ together give the best rank-1 matrix from the fixed $U$; write the minimizing $V$ in vector form as $v^T = (\mu_1, \mu_2)$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "Vector form The best 鬱 / 1 鬱 2" 缺变量名，按第一、二列各自最优系数 $\mu_1,\mu_2$ 排成 $V$ 的行重建。

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.** Problems 1 to 3 minimized $\|A - UV\|_F^2$ with fixed $U$, when $UV$ has rank 1. Which choice of $V$ gives the minimum of $\|A - UV\|_F^2$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.** With $U$ fixed $= [u_1\ u_2]$（$u_1,u_2$ 为单位正交向量？），which $V = \begin{bmatrix} \mu_1 \\ \mu_2 \end{bmatrix}$ minimizes $\|A - UV\|_F^2$?（此即把 $A$ 的各列分别投影到 $u_1,u_2$ 张成的子空间。）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "W1th fixed = [鬱 1 ． 2]，which = …" 缺矩阵名与维数，按投影到两列张成空间的最小二乘语境重建，细节待对照原题。

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.** (Computer) Starting from any $U_0$, does this alternating minimization converge to the closest rank-1 matrix $A_1 = \sigma_1 u_1 v_1^T$ from the SVD?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "S tarting 什 om any Uo"、"1 = 01 1 鬱 1 什 om the S VD" 依题意重建为"从任意 $U_0$ 出发的 alternating minimization（交替最小化）是否收敛到 SVD 给出的最佳秩一矩阵 $A_1 = \sigma_1 u_1 v_1^T$"。

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.** Minimize $\|A - UV\|_F^2$ with $V$ fixed: $A$ is $3 \times 3$ and $U$ is $3 \times 1$; with $U$ fixed: $V$ is $1 \times 3$. Each step is a least squares problem; compare the sizes of the unknowns at the two steps.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR "Minimze / | 一 U at V ： is 3 × 3 / U is 3 × 1 / at U ： U. + 1 V is 1 × 3" 仅存尺寸信息，后半句依 Problem Set 末段的 least squares（最小二乘）提示补写。

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.** These questions are also an introduction to least squares (Section II.2). For fixed $V$ or fixed $U$, each is a least squares problem—even when the rank of $UV$ increases beyond 1. But requiring nonnegativity or sparsity of $U$ and $V$ makes each minimization more difficult, and new methods are needed.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 题号 OCR 为 "0："，依其后 7 题顺延重建为 8；"引 SO 皿" → "also an"，"requmng nonneg ativity or sparsity of U and" 依语境补出变量 $U,V$。

---

<!-- page 115: 书页 110, OCR page 15 -->

> <span style="color:#7f8c8d;">本页为 Problem Set（习题集）页面（书页 110），属于 §I.12 Factoring Matrices and Tensors（矩阵与张量的分解）的习题 Problems 6–11 部分。依翻译铁律 9，习题题干保留英文原文、不译成中文；OCR 噪声已按数学语境修正为 LaTeX，修正处附绿色译者注。页边题号 6–11 与各段题干的对应关系按内容逻辑划分，标注于各 Problem 标签中。</span>

<span style="color:#7f8c8d;">**[lead-in] Problems 6–11 的总起引导句（不单独编号）**</span>

Problems 6 to 11 are about tensors. We are not doing calculus (with derivatives) or tensor algebra (with spaces of tensors). Our focus is on a single tensor $T$ that contains multidimensional data. If we have samples $1$ to $N$ and each sample is an image (a matrix), then we have a tensor of order $3$.

How can we approximate this tensor by combining a few simple ones? This is the data science question.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本引导段噪声极重：`ProbIems`→Problems、`ab out tens ors`→about tensors、`dimen si onal`→dimensional、`th e`→the；末句 "How can we approximate this tensor by combining a few simple ones?" 由乱码 "HOW ca we app 冠 ma this sor by CO b 忉 a 0 p 刀 $0$" 依数据科学语境重建；样本总数 $N$ 亦为补全（OCR 丢失字母）。

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.**

First we must decide: Which tensors are simple? Our answer: the outer product $\boldsymbol{a}\otimes\boldsymbol{b}\otimes\boldsymbol{c}$ is a simple (rank $1$) tensor. Its $(i,j,k)$ entry is the number $a_i$ times $b_j$ times $c_k$ — just as a rank-$1$ matrix $\boldsymbol{a}\boldsymbol{b}^{\top}$ has entries $a_i b_j$.

A sum of simple tensors approximates $T$.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 的 "a．b．c"（小数点系噪声）、"lts k entry"、"number 偏 time s bj time s Ck" 与 "matrix ab" 分别重建为外积 $\boldsymbol{a}\otimes\boldsymbol{b}\otimes\boldsymbol{c}$、$(i,j,k)$ 元、$a_i b_j c_k$ 与外积矩阵 $\boldsymbol{a}\boldsymbol{b}^{\top}$（秩一矩阵，其元素为 $a_i b_j$）。

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.**

Given an $m$ by $n$ matrix, how do you decide if it has rank $1$?

Given an $m$ by $n$ by $p$ tensor, how do you decide if it has rank $1$?

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 把 "m by n matrix" 识别为 "m by matnx"、"m by n by p tensor" 识别为 "m by by P ten s or"，并丢失主语 "it"（"if has rank 1"），均已修正。

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.**

The largest possible rank of a $2 \times 2 \times 2$ tensor is $3$. Can you find an example?

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.**

(a) Suppose you know the row sums $r_1$ to $r_m$ and the column sums $c_1$ to $c_n$ of an $m$ by $n$ matrix. What condition must be satisfied by those numbers?

(b) For an $m$ by $n$ by $p$ tensor, the slices are $n$ by $p$ matrices, $m$ by $p$ matrices, and $m$ by $n$ matrices. Suppose you add up the entries in each of those $m$ slices, $n$ slices, and $p$ slices. What conditions would be guaranteed to connect those $m$ numbers, $n$ numbers, and $p$ numbers?

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> "(a)" 中 OCR 为 "row sums tO rm and the column sums CI tO ‰"，即行和 $r_1$ to $r_m$、列和 $c_1$ to $c_n$；(b) 中三个方向的切片尺寸 $n$ by $p$、$m$ by $p$、$m$ by $n$（原 OCR "by P matnces" 缺首维、"and m by matrices" 丢尾维）及 "those $m$ numbers, $n$ numbers, and $p$ numbers"（OCR 丢字）均已重建。

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.**

Suppose all entries are $1$ in a $2 \times 2 \times 2$ tensor, except the first entry is $11$. Write $T$ as a sum of two rank-$1$ tensors. What is the closest rank-$1$ tensor to $T$ (in the usual Frobenius norm)?

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 原文 "exc ept the first entry is 翁 11" 中 "翁" 为符号噪声，依题意重建为「除首元为 $11$（即 $T_{111}=11$）外其余元素均为 $1$」；"tWO"→two、"tO $T$"→to $T$ 亦一并修正。

<span style="color:#2471a3;">**[problem]**</span> **Problem 11.**

A $2 \times 2 \times 2$ tensor $T$ times a vector in $\mathbb{R}^{2}$ should produce a matrix in $\mathbb{R}^{2 \times 2}$. How could you define that output $= T v$?

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 中两处 "in R" 之后的维数文字均已丢失；依题意（$2\times2\times2$ 张量沿某一方向与向量作缩并 contraction 后输出 $2\times2$ 矩阵）补全为 $\mathbb{R}^{2}$ 与 $\mathbb{R}^{2\times 2}$。若原书另有指定维数，以原书为准。

---

<!-- page 116: 书页 111, OCR page 16 -->

> <span style="color:#7f8c8d;">本页为 Part II（第二部分）的卷首标题页（divider / contents 页，书页 111）：仅含本部分名称与其下属四节 §II.1–§II.4 的标题，无正文。OCR 中的 "II.I / 11,2 / 11,3 / 11.4" 已依上下文重建为 II.1 / II.2 / II.3 / II.4。以下按行内双语逐条译出，便于目录定位。</span>

## Part II：Computations with Large Matrices（大规模矩阵的计算）

<span style="color:#2471a3;">**[part]**</span> 本部分标题为 **Computations with Large Matrices（大规模矩阵的计算）**：书至此离开以小型矩阵为主、解析性的分解（factoring）讨论与 Part I 的理论，转入针对大规模矩阵（large matrices）的实际计算（computations）方法。

<span style="color:#2471a3;">**[section]**</span> **II.1 Numerical Linear Algebra（数值线性代数）**

> <span style="color:#7f8c8d;">数值线性代数（numerical linear algebra）：数值消元（elimination）与主元（pivot）、病态矩阵（ill-conditioned）与条件数（condition number）、Gram-Schmidt 与 Householder 正交化（orthogonalization）、Krylov 子空间类迭代方法以及 QR 算法（QR algorithm）等数值主题，均属本节（对应 §II.1）。</span>

<span style="color:#2471a3;">**[section]**</span> **II.2 Least Squares: Four Ways（最小二乘：四种方法）**

> <span style="color:#7f8c8d;">最小二乘（least squares）的四种求解途径——正规方程（normal equations）、QR 分解、SVD 与伪逆（pseudoinverse）等，用于处理超定（overdetermined）与欠定（underdetermined）方程（对应 §II.2）。</span>

<span style="color:#2471a3;">**[section]**</span> **II.3 Three Bases for the Column Space（列空间的三种基）**

> <span style="color:#7f8c8d;">列空间的三种基（three bases for the column space）：由列、由行、以及由主列（pivot columns）分别给出的基，并由此引出插值分解（interpolative decomposition, ID）与 CUR 分解（CUR decomposition）等基于列选取的矩阵分解（对应 §II.3）。</span>

<span style="color:#2471a3;">**[section]**</span> **II.4 Randomized Linear Algebra（随机化线性代数）**

> <span style="color:#7f8c8d;">随机化线性代数（randomized linear algebra）：利用随机采样（random sampling）与随机化算法（randomized algorithms）构造低秩近似（low-rank approximation）、加速大规模矩阵分解与奇异值计算（对应 §II.4）。</span>

<span style="color:#7f8c8d;">**[note]**</span> 本页（书页 111）仅为此卷首页；四节正文自其后各页开始，不在本 worker 的页范围内。

---

<!-- page 117: 书页 113, OCR page 17 -->

### Part II 总览：Computations with Large Matrices（大规模矩阵的计算）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 本页为 Part II 总览正文页，OCR 噪声较重。`风`/`盖`/`兒` 均为矩阵 $A$，`乥` 为 $\Sigma$，`UEVT` 为 $A=U\Sigma V^T$，`蓋` 为 $A^+$；节号 `Section 11.2 / 1,4 / IIe2e` 是罗马数字编号被误读的结果，分别重建为 §II.2、§I.4、§II.2。此类符号与交叉引用修复以下不再逐一重复标注。

本部分将讨论 $Ax = b$ 的诸多变体（variations）。
普通的消元（elimination）或许能算出精确的解 $x$——但也可能算不出来。
方程个数可能太多（$m > n$），以致根本没有解。
系数矩阵（coefficient matrix）$A$ 可能是方阵，却可能是奇异的（singular）。
解也可能根本无法计算——当 $A$ 严重病态（ill-conditioned），或者矩阵规模实在太大时。
在深度学习中我们常常遇到许多解——而我们想要的，是那一个能很好泛化（generalize）到未见测试数据（unseen test data）上的解。
本两页将设法把这些困难的来源逐一区分开。
我们好比在做检伤分类（triage）的医生——先识别出问题，再为每一种情况建议一套处置方案。
矩阵 $A$ 的伪逆（pseudoinverse）为每个矩阵都提供了一个"逆"——但这未必帮得上忙。
每个矩阵 $A = U\Sigma V^T$ 都有一个伪逆 $A^+ = V\Sigma^+ U^T$。
就对角矩阵 $\Sigma$ 而言，伪逆 $\Sigma^+$ 对每个非零奇异值（singular value）$\sigma_k$ 都取 $1/\sigma_k$。
但要判定某个数是否"恰好为零"，是一项极其苛刻的要求——在许多实际计算中根本做不到。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原文 `But e p d e e 0 歹 0 0` 残缺严重，依上下文重建为 "deciding when a number is exactly zero"。

§II.2 中的伪逆只是求解 $Ax = b$ 的一种途径，下面列出其它途径。

**1.** 假设 $A$ 是方阵且可逆，规模适中，并且它的条件数（condition number）$\kappa(A)$ 不太大。
此时消元将能成功（必要时可作行交换（row exchanges））。
如 §I.4 所述，我们有 $PA = LU$ 或 $A = LU$（视有无行交换而定）。
反斜杠命令（backslash command）$A\backslash b$ 被设计成：只要可能就把 $A$ 处理成块对角（block diagonal）形。

**2.** 假设 $m > n$：此时 $Ax = b$ 的方程太多，不应指望存在解。
若 $A$ 的各列线性无关（independent）且不算太病态，我们就转而解正规方程（normal equations）$A^T A\hat x = A^T b$，以求得最小二乘解（least squares solution）$\hat x$。
向量 $b$ 很可能并不落在 $A$ 的列空间（column space）中，因而 $Ax = b$ 很可能无解。
在 §II.2 中可以看到，$\hat x$ 正是 $b$ 到该列空间上的投影（projection）。

以上是两类"好问题"——$A$ 可逆，或 $A^T A$ 可逆，且矩阵良态、规模不大。
下一页将描述四种更困难的计算（它们仍然是线性方程组）。

---

> <span style="color:#7f8c8d;">Strang Part II, p.113</span>

---

<!-- page 118: 书页 114, OCR page 18 -->

> <span style="color:#7f8c8d;">本页为书页 114，是 Part II 总览正文的续页（第 3~6 类困难情形）；页眉 "Computations with Large Matrices" 与页码 114 为重复元素，不译。</span>

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 本页 `风` 亦为 $A$，`叻` 为范数记号之误，$A^+b$、$A^TA$、$\delta^2$、$\ell_1$ 等公式均按数学语境重建。

**3.** 假设 $m < n$。
此时若方程 $Ax = b$ 有解，就会有许多解——因为 $A$ 有非零的零空间（nullspace）。
于是解是欠定的（underdetermined）。我们要针对自己的目的挑选"最好"的解 $x$。
有两个可选对象，即 $x^+$ 与 $x_1$：
其一为 $x^+ = A^+ b$——由伪逆（pseudoinverse）$A^+$ 给出的最小范数解（minimum norm solution），其零空间分量为零。
其二，$x_1$ 是使 $\ell_1$ 范数取最小的解，即最小 $\ell_1$ 范数解（minimum $\ell_1$ norm solution）。
这个解常常是稀疏的（sparse，即多数分量为零），因而非常理想。
它来自 §III.4 的基追踪（basis pursuit）。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接）:**</span> 你在前作《线性代数导论》§4.2–4.3 认识的最小二乘解 $x^+=A^+b$ 极小化的是 $\ell_2$ 范数；这里与它对比的是另一把"尺子"$\ell_1=\sum_i|x_i|$。为什么 $\ell_1$ 偏爱稀疏解？看等高面形状：$\|x\|_2\le 1$ 是光滑球面，$\|x\|_1\le 1$ 是顶点全落在坐标轴上的菱形（多面体）。欠定方程组 $Ax=b$（$m\lt n$）的解集是一个仿射子空间，把 $\ell_1$ 球"吹大"到刚好碰到该解集时，接触点极易落在多面体的角上——角点只有极少数坐标非零，于是多数分量恰好为 0。这正是 Boyd《凸优化》§6.3 正则化（$\ell_1$ 换 $\ell_2$）与压缩感知基追踪（正文指向 §III.4）的几何内核。关键差异：$x^+$ 是闭式解（一次矩阵乘法），稀疏解却必须用迭代优化求解——"形状更好"的解往往要付出计算代价，这是学习 §II.4 前先建立的心理预期。

**4.** 假设 $A$ 的各列处于不良状态。
此时比值 $\sigma_1/\sigma_n$ 太大（条件数过大），解 $x$ 便无法被很好地确定——正如 §III.3 中高阶插值（high-order interpolation）的情形。
通常的补救办法是用格拉姆-施密特（Gram-Schmidt）或豪斯霍尔德（Householder）算法把 $A$ 的各列正交化（orthogonalize）。
对 $A$ 的各列施行 Gram-Schmidt 正交化，就是要构造出标准正交向量（orthonormal vectors）$q_1, \dots, q_n$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原句节号 `Section 11.2` 应为 §II.1（Numerical Linear Algebra，数值线性代数），该节讨论 Gram-Schmidt 的两种形式；已据此重建。

§II.1 介绍了格拉姆-施密特的两种重要形式。
标准形式是：把新的第 $k+1$ 列对已知方向 $q_1, \dots, q_k$ 正交化。
更稳妥的形式是：一旦某个向量 $q_k$ 被求出，就立即把余下 $n - k$ 列全部对 $q_k$ 正交化。
于是当某一列（比如很小的 $a_{k+1}$）不合用时，必要时可以用后面某一列把它换掉。
而最稳妥的形式，是每一步都选取当前可用的最大列（largest available column）。

**5.** 假设 $A$ 近似奇异（nearly singular，如同情形 4）。
此时 $A^T A$ 会有非常大的逆，格拉姆-施密特可能失效。
另一条路子是加入惩罚项（penalty term）：求解 $(A^T A + \delta^2 I)\hat x = A^T b$，即最小化 $\|Ax - b\|^2 + \delta^2\|x\|^2$。
当惩罚参数 $\delta^2$ 趋于零时，$(A^T A + \delta^2 I)^{-1}A^T$ 趋于伪逆 $A^+$（见 §II.2）。
我们通过加上 $\delta^2 I$ 使 $A^T A$ 更正定（positive definite），从而保证可逆。
这与统计学中的岭回归（ridge regression）联系在一起。
像 $\delta^2\|x\|^2$ 这样的惩罚项常见于反问题（inverse problems）——反问题的目标是从系统的输出反推系统本身。
通常我们是已知系统（例如 electrical network（电网）），再去求它的输出（电流与电压）。
反问题则从输出出发（例如 CT 或 MRI 的扫描影像）。重建系统是病态的（ill-conditioned）。

> <span style="color:#1e8449;">**[note] Note（译者注：Tikhonov 修正：为什么抬的是 δ 的平方，以及浮点里的最优 δ）:**</span> 为什么加 $\delta^{2}I$ 就能救活近似奇异的 $A^{\top}A$？用特征值看最清楚：$A^{\top}A$ 对称半正定，特征值恰为奇异值的平方，$\sigma_1^{2}\ge\cdots\ge\sigma_n^{2}\ge0$。病态意味着 $\sigma_n$ 很小，最小特征值以平方的速度趋零。取 $A$ 为 $1,1;1,1+10^{-8}$，奇异值约是 2.0 与 5e-9，于是 $\sigma_n^{2}=2.5\times10^{-17}$；而 float64 的机器精度 $\varepsilon$ 约 $2.2\times10^{-16}$，乘上 $\sigma_1^{2}=4$ 得 $8.9\times10^{-16}$，比最小特征值还大三十多倍。后果不是抽象的：`np.linalg.eigvalsh` 给出的两个特征值是 0 与 4.00000002，`np.linalg.cond` 直接返回 inf——信息在形成正规方程那一步就永久丢了，后面用什么解法都补不回来。
> 
> 加上 $\delta^{2}I$ 后每个特征值被抬成 $\sigma_i^{2}+\delta^{2}$，最小者不小于 $\delta^{2}$，条件数被压到 $(\sigma_1^{2}+\delta^{2})/\delta^{2}$ 以下。同一组数上：$\delta=10^{-2}$ 时最小特征值是 1e-4、条件数 4.0e4；$\delta=10^{-3}$ 时 4.0e6；$\delta=10^{-4}$ 时 4.0e8。可逆性有保证，求逆也不再爆炸。这条「在 0 附近填一个微扰」的策略在 inverse problem（反问题）、ridge regression（岭回归）与 Boyd 的凸优化 §6.3 正则化里是同一个动作，只是三处各有各的叫法，式子一模一样。
> 
> $\delta^{2}$ 还同时处理第 3 种情形，即 $m<n$ 的欠定系统：此时 $A^{\top}A$ 奇异是因为零空间方向对应 $\sigma=0$，加 $\delta^{2}$ 等于自动给这些方向一个温和的权，免去显式处理零空间。我验了极限与单调性：取 $A$ 为仅有的一行 $1,2,0.5$、$b=1$，最小范数解的范数是 0.43643578，$\delta$ 取 $10^{-1}$、$10^{-2}$、$10^{-3}$ 时与它的距离分别是 8.3e-4、8.3e-6、8.0e-8，严格按 $\delta^{2}$ 缩小。但 $\delta=10^{-6}$ 时距离反而回升到 9.3e-6——此时条件数已到 4.0e12，舍入误差开始吃掉逼近的收益。所以「$\delta\to0$ 时趋近伪逆」是数学极限，浮点里存在一个最优 $\delta$，再小只会更差。
> 
> 为什么抬的是 $\delta^{2}$ 而不是 $\delta$？因为要保证正定的是 $A^{\top}A$ 而不是 $A$，把最小特征值抬到 $\delta^{2}$ 就够让条件数按 $1/\delta^{2}$ 有界；直接加 $\delta$ 会改变量纲，等式也不再是同一个最小化问题的正规方程。概率论那边还有一条读法：若先验取 $x$ 服从 $N(0,\tau^{2}I)$、噪声方差为 $\sigma^{2}$，则后验均值的正规方程正是 $A^{\top}A+(\sigma^{2}/\tau^{2})I$，于是 $\delta^{2}$ 不是拍脑袋的旋钮，而是信噪比的倒数。史实坐标：统计学一侧是 Hoerl 与 Kennard 刊于 Technometrics 12 卷 1 期 55 至 67 页的 ridge regression 论文，1970 年；Tikhonov 的名字挂在同一条式子上，其原始文献我未能一手核实。
> 
> 换到 SVD（奇异值分解）基下看，这个修正到底在做什么一目了然：解可以写成 $\sum_i f_i (u_i^{\top}b/\sigma_i) v_i$，滤波因子是 $f_i=\sigma_i^{2}/(\sigma_i^{2}+\delta^{2})$。$\sigma_i$ 远大于 $\delta$ 时 $f_i$ 近似 1，该方向原样保留；$\sigma_i$ 远小于 $\delta$ 时 $f_i$ 近似 $\sigma_i^{2}/\delta^{2}$，方向被压成近零。代入上面那组数并取 $\delta=10^{-2}$：大奇异值方向的滤波因子是 0.999975，小奇异值方向只有 2.5e-13。它不是把小奇异值砍掉，而是按平方比例调暗，这正是它与截断 SVD 硬阈值最本质的差别，也是它能给出一整族光滑解、而不像截断那样只给孤立的几个答案的原因。
> 
> 最后把「极限」这件事说完整：后文会证明 $\delta\to0$ 时 $(A^{\top}A+\delta^{2}I)^{-1}A^{\top}b$ 恰趋近伪逆解 $A^{+}b$。这解释了为什么这种修正不改变问题的解集结构、只改变挑选规则：它把解沿「范数小」的方向拉，$\delta$ 越大拉得越狠、解越贴近 0，$\delta$ 越小越贴近最小范数解。工程上调这个参数时要记住它有双重身份——数值上的稳定器与统计上的收缩，两个角色共用同一个 $\delta^{2}$，改它等于同时改两边，不存在只修数值不动统计的好事。

---

**6.** 假设 $A$ 实在太大，大到装不进快速内存（fast memory）。
我们可以请求查看少量几列，却无法继续做消元。
即便在预计安置于橡树岭（Oak Ridge）的千万亿次（petascale）计算机、或计划建在阿贡（Argonne）的百亿亿次（exascale）机器上，计算 $A^T A$ 也不可能（《纽约时报》，2018 年 2 月 28 日）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原文 `0 R1dge` 与 `New Times` 依上下文重建为 Oak Ridge 与 New York Times（关于 petascale/exascale 超级计算机的报道）。

对如此巨大的矩阵，该怎么办？
最好的解法是对各列做随机采样（random sampling，见 §II.4）。
若 $A$ 规模过大但各列足够一致（coherent），每一列都会是列空间的一个有用样本。
随机采样的结果从不保证确定，但出错概率很低。
随机化数值线性代数（randomized numerical linear algebra）由此催生了具有可靠统计基础的算法。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原文 `Randomized ume r 记 linear algebra` 残缺，重建为 "Randomized numerical linear algebra"。

这是以概率论中的深刻结论为基础的一场必然的演化（evolution），或者说革命（revolution）。

---

> <span style="color:#7f8c8d;">Strang §II.1, p.114</span>

---

<!-- page 119: 书页 115, OCR page 19 -->

### II.1 Numerical Linear Algebra（数值线性代数）

本节概括（经典）numerical linear algebra（数值线性代数）的核心思想。
这里不打算展开细讲，因为已有大量教材把这些内容讲得很好。
这些思想的目的是求解 $Ax = b$ 或 $Ax = \lambda x$ 等问题。
它们是各种新 computational methods（计算方法）赖以建立的基础。

> <span style="color:#1e8449;">**[note] Note（译者注：为什么大矩阵走迭代：消元的填入代价与 CG 的真实账）:**</span> 为什么大矩阵要迭代而不直接消元？先用 6.006 与 CLRS 的复杂度语言算账：稠密高斯消元约 $\frac{2}{3}n^{3}$ 次浮点运算，对称正定时 Cholesky（乔列斯基分解）约 $\frac{1}{3}n^{3}$；更麻烦的是主元造成的 fill-in（填入），它把稀疏矩阵逐步变稠密。我实测二维五点 Laplacian：$n=20$ 时 $N=400$、原矩阵 1920 个非零元，稠密 LU 的 $L+U$ 却有 15638 个，8.1 倍；$n=80$ 时 $N=6400$、原矩阵 31680 个非零元，$L+U$ 涨到 1000274 个，31.6 倍。规律是非零元数约为 $N(2n+1)$，按 $N^{3/2}$ 涨，而原矩阵只按 $N$ 涨——这就是「消元在稀疏问题上自杀」的定量版本。
> 
> 而矩阵乘向量 $Av$ 只需扫一遍非零元，稀疏情形约 $O(\mathrm{nnz})$ 次乘加。$n$ 在 $10^{4}$ 到 $10^{6}$ 且 $A$ 稀疏时，$O(n^{3})$ 不可行，每步 $O(\mathrm{nnz})$ 的迭代却可行。CSAPP 第 6 章的存储器层次结构给出另一半理由：按压缩格式只存非零元，一次迭代是对数组的一次顺序扫描，空间局部性与硬件预取全部生效；相比之下稠密消元每步都要动用整块 $N^{2}$ 的存储。迭代步数也能量：同一个五点 Laplacian 上用 conjugate gradient（共轭梯度）求到相对残差 $10^{-8}$，$n=20$ 用 36 步，$n=40$ 用 74 步，约 1.85 倍——步数随 $n$ 线性涨，而不是随 $N$。
> 
> 本页的分裂 $A=S-T$ 是这一切的母版：把 $Ax=b$ 改写成 $Sx=Tx+b$，从任意 $x_0$ 出发反复解 $Sx_{k+1}=Tx_k+b$。$S$ 要既接近 $A$ 又容易求逆：取对角就是 Jacobi iteration（Jacobi 迭代），取下三角就是 Gauss-Seidel iteration（Gauss-Seidel 迭代），配上松弛因子就是 SOR（逐次超松弛）。收敛由 $S^{-1}T$ 的谱半径小于 1 决定，误差每步乘以这个谱半径——这就是 page_120 那条误差方程的来历。它也解释了一个两难：$S$ 越接近 $A$、越像一次真正的消元，收敛越快，可每步越贵；两端是同一个权衡。共轭梯度之所以跳出这个两难，是因为它不去近似 $A$，而是在 Krylov subspace（Krylov 子空间）里逐步逼出最优多项式。
> 
> 这里必须修正一个常见误解：迭代法赢的不是渐近阶。CG 的总代价是步数乘每步代价，即 $O(n\cdot N)=O(N^{3/2})$，与直接法同阶；它赢在常数与内存。取 $N=10^{4}$，Cholesky 约 $3.3\times10^{11}$ 次运算，100 步 CG 约 $5.0\times10^{6}$ 次，差 6.7e4 倍；内存上更悬殊，$L+U$ 要按 $N^{3/2}$ 存，CG 只要 $O(N)$。这才是三维或超大规模问题里直接法先撞墙的地方。它与你学过的牛顿法迭代求根是同一哲学：每步只做一次求值与一次除法，代价极低，靠重复把精度买回来；总代价永远是迭代次数乘每步代价，两者必须一起看。
> 
> fill-in 为什么必然发生？换成图的语言就一眼看穿：稀疏矩阵的对称结构对应一张图，消去一个顶点时它的所有邻居必须两两相连、变成一个团，否则消元后的矩阵与原来不等价——那些新连出来的边就是填入。二维网格上只要消去顺序不是由外向内，带宽与填入都会爆炸，这也是为什么消元顺序属于算法的一部分，而不是实现细节。五点 Laplacian 上按自然行序消元得到的带宽是 $2n+1$，与实测的非零元数 $N(2n+1)$ 完全吻合，一个数都不差。
> 
> 史实坐标：共轭梯度由 Hestenes 与 Stiefel 发表于 Journal of Research of the National Bureau of Standards 49 卷 6 期 409 至 436 页，1952 年 12 月，工作完成于加州大学洛杉矶分校校园内的 NBS 数值分析研究所。有意思的是它当年被宣传成「$n$ 步内精确」的直接法，浮点舍入让这个承诺失效，直到 1970 年代才以迭代法的身份重新流行——这段反复的原始文献我未能一手核实，只核到原始论文的卷期页码与机构。这也正合本页的意思：同一个式子被当作直接法时价值有限，被当作迭代法时才显出威力。

---

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 中此句方程残缺为 `solve = b or Ac = ,\c or =`，已依上文语义重建为求解 $Ax = b$、$Ax = \lambda x$（后文尚有其他问题形式）。

而正是这些**新方法**——旨在从矩阵或 tensor（张量）的数据中提取信息的方法——才是本书这一部分真正的目标。
当矩阵或张量确实极其庞大（big data，大数据）时，我们往往不得不对矩阵进行 random sampling（随机采样）。
随机采样竟能给出可靠的答案，这看起来几乎不可能。
但事实上，这种情况以很高的概率成立。

numerical linear algebra 的「圣经」是 Matrix Computations（矩阵计算），作者是 Gene Golub 与 Charles Van Loan。
第四版于 2013 年由 Johns Hopkins University Press（约翰斯·霍普金斯大学出版社）出版。
Gene 早在 30 多年前就已在 Johns Hopkins 授课，正是这段经历促成了第一版——我想出版社当年绝没想到 2013 年会有一本 750 页的书。

更多参考书目列于网站 math.mit.edu/learningfromdata 上。
我们在此选择一本杰出教材：Trefethen 与 Bau 合著的 Numerical Linear Algebra。
它的章标题恰好为核心思想与算法提供了一份很好的提纲：

- I. Fundamentals（基础），终点直达 SVD 与 Eckart-Young
- II. QR Factorization and Least Squares（QR 分解与最小二乘），全部三种方法 $A^{+}$、$(A^{T}A)^{-1}A^{T}$ 与 QR
- III. Conditioning and Stability（条件性与稳定性）：condition numbers（条件数）、backward stability（后向稳定性）、perturbations（扰动）
- IV. Systems of Equations（方程组）：direct elimination（直接消元）$PA = LU$，以及 Cholesky（乔列斯基）分解 $S = LL^{T}$
- V. Eigenvalues（特征值）：约化到 tridiagonal–Hessenberg–bidiagonal（三对角–海森伯格–双对角）形式；带 shifts 的 QR（QR 算法）
- VI. Iterative Methods（迭代法）：Arnoldi、Lanczos、GMRES、conjugate gradients（共轭梯度）等

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 目录第 II 条 OCR 严重破损（`风 + and （ T ）一 1 T and Q 娓`），依数值线性代数常识重建为三种最小二乘途径 $A^{+}$、$(A^{T}A)^{-1}A^{T}$ 与 QR；第 VI 条末尾 `10v` 重建为省略号「等」。

本节我们的计划是勾勒第 VI 与第 V 部分中那些重要 iterative algorithms（迭代算法）的轮廓。
这些算法都收录在求解 $Ax = b$、$Sx = \lambda x$ 等问题的各大主流代码之中。
「iterative（迭代）」一词表明：我们反复执行一个简单而快速的步骤，以逐步逼近某个更大、更难问题的解。

<span style="color:#2471a3;">**[note]**</span> 迭代的一个模型（虽算不上特别快的算法！）是把 $A$ 分裂（split）为 $A = S - T$。

为迭代做准备（Prepare for iteration）：把 $Ax = b$ 改写成 $Sx = Tx + b$，即式 (1)

```math
Sx = Tx + b \tag{1}
```

从任意 $x_0$ 出发，求解 $Sx_1 = Tx_0 + b$。
然后继续求解 $Sx_2 = Tx_1 + b$。
迭代上百次也很常见。
若 $S$ 选得恰当，则每一步 $Sx_{k+1} = Tx_k + b$ 都进行得很快。

---

> <span style="color:#7f8c8d;">Strang §II.1, p.115</span>

---

<!-- page 120: 书页 116, OCR page 20 -->

把迭代式 $Sx_{k+1} = Tx_k + b$ 从精确式 $Sx = Tx + b$ 中减去后，误差 $e_k = x - x_k$ 便满足 error equation（误差方程），此时 $b$ 恰好消去：

```math
e_{k+1} = S^{-1}T\,e_k \tag{2}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 仅存 `Error equation（ 2 ）` 字样，公式 (2) 的主体已丢失；依据其后"每一步都把误差乘以 $S^{-1}T$"一句重建为 $e_{k+1} = S^{-1}T\,e_k$。

每一步都把误差乘以 $S^{-1}T$。
当 $\|S^{-1}T\| \ll 1$ 时，convergence（收敛）很快。
但在实际中，$S^{-1}T$ 往往有一个接近 1 的 eigenvalue（特征值）。
这时就需要更好的想法——比如 conjugate gradient method（共轭梯度法）。

我再补充一句。
一本教科书也许会通过求解 $\det(A - \lambda I) = 0$ 来求特征值。
它也许会通过处理矩阵 $A^{T}A$ 来求 singular values（奇异值）。
而在现实中，那些行列式根本无法想象，大型矩阵 $A^{T}A$ 在数值上也非常不明智。
$Ax = b$ 与 $Ax = \lambda x$ 都是严肃的问题（serious problems）。
本节中我们将求解规模为 100 或更大的矩阵。
对规模 $n = 10^{4}$ 的矩阵，请继续往下读（见 §II.4）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 本段 OCR 破损较重（`det （ 一 (I) = 0`、`the matrix T`、`large T`、`= and 鬱 = 0`、`For = 104`、`Section 11.4` 等），已依数学语境重建为 $\det(A - \lambda I) = 0$、$A^{T}A$、$Ax = b$ 与 $Ax = \lambda x$、$n = 10^{4}$ 以及交叉引用 §II.4。

### Krylov Subspaces and Arnoldi Iteration（Krylov 子空间与 Arnoldi 迭代）

关键思想（key idea）：matrix-vector multiplication（矩阵-向量乘法）$Ab$ 很快，尤其当 $A$ 是 sparse（稀疏）矩阵时。
若从 $A$ 与 $b$ 出发，我们可以快速算出下列每个向量：$b,\ Ab,\ A^{2}b,\ \ldots,\ A^{n-1}b$。
（绝不要去计算 $A^{2}$ 或 $A^{3}$——只计算向量。）
这些向量的线性组合构成第 $n$ 个 Krylov subspace（Krylov 子空间）。
我们就在这个子空间内部寻找目标解的一个足够接近的近似。

> <span style="color:#1e8449;">**[note] Note（译者注：「只乘向量」的代价账与 k 步信息传播）:**</span> 先给这条纪律一笔可复算的账。取 $30\times 30$ 网格上的五点差分 Laplacian，$n=900$，每行至多五个非零元：$A$ 有 4380 个非零元，$A^2$ 有 11104 个（是 $A$ 的 2.54 倍），$A^3$ 有 20840 个（4.76 倍）。同一台机器上乘一遍向量，实测稠密要 470.7 微秒，稀疏只要 5.0 微秒，差 94 倍；关键在这 5.0 微秒与迭代到第几步无关。
> 
> 稀疏结构为什么会「长回来」？机制是可数的：五点 Laplacian 满足 $(A^k)_{ij}\neq 0$ 当且仅当格点 $i$ 与 $j$ 的曼哈顿距离不超过 $k$，第 $k$ 层菱形有 $2k^2+2k+1$ 个格点，于是每行非零个数是 $k$ 的二次函数（实测 $A^2$ 平均每行 12.34 个，紧上界 13，差额来自边界行）。这条增长是**单调**的：算出来的非零元不会自己消失，它与消元里 fill-in 不可逆是同一个机制 —— 所以 $A^k$ 一旦成形，你就再也回不到稀疏世界了。若把纪律换成「先乘出 $A^K$ 再一次作用」，代价立刻从 $O(k\cdot \mathrm{nnz})$ 掉进两笔同时爆掉的开销：$O(n^3)$ 的稠密乘法加 $O(\mathrm{nnz}(A^K))$ 的存储。也就是说 Krylov 方法的全部优势恰好建立在这一条上，去掉它，迭代法退化成每步都要碰整张稠密矩阵的慢法。
> 
> 那 5.0 微秒花在哪里？4380 个非零元每次要连带列号搬 12 个字节，共 52.6 KB，除以 5.0 微秒得每秒约 10.5 GB，与单核内存带宽同一量级。所以这一步的墙是**搬数据**而不是算数：乘 4380 次只要几微秒，把 52.6 KB 从主存捞上来也一样要几微秒。这条换算给出实际工程的判断依据 —— 稀疏 matvec 的墙钟约等于「$K$ 乘 nnz 乘 12 字节」除以带宽，与浮点峰值无关；想让 Krylov 更快，先降 nnz 或提高数据复用（分块、压缩存储），而不是换更快的乘法指令。
> 
> 这条策略也有失效边界，算清楚很有用。若 $A$ 本来就稠密，matvec 是 $n^2$ 次乘加，$k$ 步 Krylov 的总量约 $k n^2$，而一次 LU 分解约 $2n^3/3$；两者相等的交叉点在 $k=2n/3$。取 $n=900$ 就是 600 步 —— 当你必须迭代六百步以上才收敛时，「只乘向量」反而不如直接分解。这正是后文反复强调迭代法在 $k\ll n$ 时赢的定量含义，也解释了为什么 page_126 讲的预处理值得投资：它把 $k$ 压下来，才能留在交叉点左边。
> 
> 还有一处不对称值得现在就记住。非对称矩阵的 Arnoldi 每步要把 $Aq_k$ 对全部 $k$ 个旧基做投影，正交化成本 $O(nk)$，$K$ 步合计 $O(nK^2)$ —— 一旦 $K$ 上千，这一项就盖过 $O(K\cdot\mathrm{nnz})$ 的乘法本身，稀疏带来的便宜被正交化吃干。而 page_122 的 Lanczos 反过来：每步只碰两个旧向量，成本与 $k$ 无关，总量回到 $O(K\cdot\mathrm{nnz})$。同一个「只乘向量」的纪律，在对称情形才真正兑现全部红利，这是后面要把 Lanczos 单独讲的成本理由。
> 
> 跨课程还有一层读法。把 $A$ 读成转移矩阵，$A^k b$ 就是 $k$ 步之后的概率分布（概率论的 Markov chain），这同时解释了为何 $A^k$ 必然稠密：不可约图上任意两个状态 $k$ 步之内互达，于是每个位置都分到非零概率。6.006 的 BFS 与它只差一处：BFS 记的是「能不能到」（布尔），这里记的是「到了多少」（实数加权）；把队列里的「或/与」换成「加/乘」，按层扩展就变成了一串 matvec。于是「$k$ 维 Krylov 子空间足以逼近 $n$ 维问题的解」也不再神秘：$k$ 步传播已经把 $b$ 的信息铺到图的 $k$ 邻域，剩下的只是在铺开的那些向量里取最优线性组合。

第一个问题是找一组远比这些向量 $b,\ Ab,\ \ldots,\ A^{n-1}b$ 更好的 basis（基）。
通常 orthogonal basis（正交基）$q_1, \ldots, q_n$ 才是最佳选择！
Gram-Schmidt（格拉姆-施密特）的思想——从 $Aq_k$ 中减去它在先前所有向量 $q_1, \ldots, q_k$ 上的 projections（投影）——是那么自然。
这正是 Arnoldi 求 $q_{k+1}$ 的方法。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> Gram-Schmidt 一句的 OCR 为 `subtracting 0 茳 the propctions 0f 鬱 = q ont0 all the earlier vectors`，已重建为"从 $Aq_k$ 中减去它在 $q_1, \ldots, q_k$ 上的投影"；下方算法框 OCR 错乱（`ql = b / 日 吼`、`= 一 九 ‰`、`q + 1 = / 九 + 1`），已按标准 Arnoldi 流程重建。

<span style="color:#2471a3;">**[algorithm]**</span> **Arnoldi Iteration（Arnoldi 迭代）**
从 $q_1 = b/\|b\|$ 出发，已知 $q_1, \ldots, q_k$。
对每个已知向量 $q_j$（$j = 1$ 到 $k$）：计算 inner products（内积）$h_{jk} = q_j^{T}Aq_k$。
从 $Aq_k$ 中减去全部投影，得 $w = Aq_k - \sum_{j=1}^{k} h_{jk}q_j$。
计算 norm（范数）$h_{k+1,k} = \|w\|$。
新的基向量 $q_{k+1} = w/h_{k+1,k}$，其范数为 1。

> <span style="color:#1e8449;">**[note] Note（译者注：Arnoldi 是 Krylov 空间里的 Gram-Schmidt，以及 stability 的确切含义）:**</span> 先把「$AQ_k=Q_{k+1}H_{k+1}$」这句话验成事实。取一个 $6\times 6$ 随机矩阵跑 6 步 Arnoldi：$Q_6$ 的列标准正交到 $5.04\times 10^{-16}$（就是双精度的地板），$AQ_6$ 与 $Q_7H$ 的最大元差 $2.22\times 10^{-16}$，$H_6$ 里第一子对角线以下的元素**恰好是 $0.000$**（不是「很小」，是结构性的零），$H_6$ 的特征值与 $A$ 吻合到 $8.88\times 10^{-15}$。
> 
> 那次运行的第 6 步给出 $h_{76}=0$。这不是数值失败，而是精确的不变子空间：$K_6$ 已经撑满 $\mathbb{R}^6$，$Aq_6$ 完全落在 $q_1,\dots,q_6$ 张成的空间里，减完投影后 $w=0$，`q = w/0` 无法进行。教科书里的 Arnoldi 因此需要一句「若 $h_{k+1,k}=0$ 则提前终止」，而终止时刻得到的 $H_k$ 已经与 $A$ 相似 —— 你免费拿到一个精确的部分 Schur 形。把它读成「算法崩了」是最常见的误解。
> 
> Hessenberg 形状是从哪来的？一句话：$Aq_k$ 属于 $A\,K_k\subseteq K_{k+1}$，而 $K_{k+1}$ 的基只有 $q_1,\dots,q_{k+1}$ 这 $k+1$ 个，所以第 $k$ 列在第 $k+1$ 行以下没有位置可放。注意这条推理没有用到 $A$ 的任何特殊性质：它只用到「$q$ 是逐层按 $A$ 生成的」。若把 $q_1$ 换成任意一个向量，或者每步都拿最初那个 $b$ 去做投影（不更新基），$AQ_k\subseteq Q_{k+1}$ 立刻失效，$H$ 会退化成一般方阵。所以正文本页那句「从算法动作读出矩阵稀疏结构」的准确含义是：**形状来自产生基的方式，不是来自矩阵本身**。若 $A$ 对称，同一条不变性再加一层「$S=S^{T}$」，$H_k$ 就会进一步压到三对角 —— 那一支就是 page_122 的 Lanczos，形状依旧是从构造里读出来的。
> 
> 「numerically stable」也值得抠字眼。算法框的书写顺序 —— 先算一个 $h_{jk}=q_j^{T}Aq_k$，立刻从 $Aq_k$ 里减掉，再算下一个 —— 正是 modified Gram-Schmidt（修正格拉姆-施密特）；经典 Gram-Schmidt（CGS）相反：先对**原始**的 $Aq_k$ 一次算完全部投影，最后一次性减。两者在实数上等价，在浮点上差得远。实测 $8\times 8$、条件数 $10^8$ 的矩阵：CGS 的正交性误差涨到 $8.26\times 10^{-3}$，MGS 只有 $8.49\times 10^{-10}$，差七个数量级；条件数 $10^4$ 时是 $5.12\times 10^{-10}$ 对 $4.71\times 10^{-13}$。所以「Arnoldi 在数值上是稳定的」这句不是「随便哪种正交化都行」，而是「它用的是每减一次就更新一次的那个顺序」，去掉这个顺序，稳定性立刻丢掉。
> 
> 顺便钉死起点为什么必须是 $b/\|b\|$。Krylov 子空间按定义由 $b$ 生成：$K_k=\mathrm{span}\{b,Ab,\dots,A^{k-1}b\}$。若从别处起头，比如某个随机向量 $w$，那么 $K_k(w)$ 与 $b$ 无关，$x=Q_ky$ 永远落不进「$b$ 需要被逼近的那些方向」，GMRES 极小化 $\|b-Ax\|$ 的能力随之丢失。更彻底地说：同一个 $A$、不同的 $b$，$H_k$ 与收敛速度都不同，所以 Arnoldi 的收敛速度依赖的是 $(A,b)$ 这一对而不是 $A$ 单独；这正是重启之后必须重新取 $q_1=r/\|r\|$ 的原因。
> 
> 跨课程看，这整段就是一个标准的循环不变式（6.042J 的 induction 模板）：不变式是「$Q_k$ 的列标准正交，且 $A\,K_k\subseteq K_{k+1}$」；初始化 $k=0$ 显然成立；归纳步由「减投影再归一化」保持标准正交、由 $Aq_k$ 的系数只落在前 $k+1$ 个位置保持嵌套关系；退出时不变式直接给出 $AQ_k=Q_{k+1}H_{k+1}$ 与 Hessenberg 形状。也就是说本书这一小节几乎不需要「额外证明」——**不变式就是算法本身**。凡遇到「算法显然正确」的场合，先用这个模板把不变式写出来，几乎总能立刻看出算法为何必须长成那样；读数值代码时先找循环里的不变式，也比一上来做误差分析省力得多。

---

你必须用矩阵语言来看清这一过程。
$AQ_k = Q_{k+1}H_{k+1}$ 的最后一列说明：$Aq_k$ 是 $q_1$ 到 $q_{k+1}$ 的一个线性组合。

```math
AQ_k = Q_{k+1}H_{k+1}
```

在等式两边同时左乘 $Q_k^{T}$，所得结果十分重要。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 末尾两句的 OCR 为 `This is 蓋 Q = Qk+1Hk+1 · Multiply bo 山 sides by QT`，重建为 $AQ_k = Q_{k+1}H_{k+1}$ 与"左乘 $Q_k^{T}$"。左乘后得到 $Q_k^{T}AQ_k = H_k$，其中 $H_k$ 是 upper Hessenberg（上海森伯格）矩阵；当 $A$ 对称时它化为对称三对角矩阵，这为后文 Lanczos 迭代埋下伏笔。

---

> <span style="color:#7f8c8d;">Strang §II.1, p.116</span>

---

<!-- page 121: 书页 117, OCR page 21 -->

### II.1 Numerical Linear Algebra（数值线性代数）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页页首承接上一页 Arnoldi 过程的方程（3）、（4）及其矩阵示意，OCR 噪声极大（原样残留 `QTcAQk = ...`、`× 0 处 × 1`、`row + 1`、`=Hk. （ 4 ）` 等碎片），现依数学语境重建：Arnoldi 关系式为 $A Q_k = Q_{k+1} H_{k+1,k}$，其中 $H_{k+1,k}$ 是 $(k+1)\times k$ 的上 Hessenberg（海森伯格）矩阵，其末行只在末位有非零元 $h_{k+1,k}$；删去末行即得 $k\times k$ 方阵 $H_k = Q_k^T A Q_k$。

方阵 $H_k$（square matrix $H_k$）正是在方程（3）中丢掉了最后一行（last row）之后剩下的方阵。

于是剩下的正是一个上 Hessenberg 矩阵（upper Hessenberg matrix），其第一子对角线（first subdiagonal）之下全部为 0。

只含一条非零子对角线（nonzero subdiagonal）的矩阵被称为 Hessenberg 矩阵（Hessenberg matrices）。

这个 $H_k$ 有一个漂亮的解释（neat interpretation）：$H_k = Q_k^T A Q_k$ 就是把 $A$ 在以诸 $q$ 为基的 Krylov 空间（Krylov space）上的投影（projection）。

用来求 $H_k$ 的 Arnoldi 过程（Arnoldi process）是数值线性代数（numerical linear algebra）中最出色的算法（algorithms）之一。

它在数值上是稳定的（numerically stable），并且诸 $q$ 保持标准正交（orthonormal）。

### Eigenvalues from Arnoldi（Arnoldi 求得的特征值）

矩阵 $H_k = Q_k^T A Q_k$ 中的各个数值，都是在 Arnoldi 过程进行当中计算出来的。

如果一路做到 $k$ 等于矩阵 $A$ 的阶数（size of $A$），就会得到与 $A$ 相似的（similar）Hessenberg 矩阵 $H = Q^{-1} A Q$：它与 $A$ 具有相同的特征值（same eigenvalues）。

我们再用下面要介绍的移位 QR 算法（shifted QR algorithm）来计算这些特征值。

实际上我们不会把 Arnoldi 过程一路做到头，而是在某个合适的 $k$ 值处停下来。

此时 $H$ 的特征值（通常）能很好地逼近 $A$ 的极端特征值（extreme eigenvalues of $A$）。

> <span style="color:#1e8449;">**[note] 译者注（第一性原理洞察）:**</span> 为什么 Krylov 过程先"看见"极端特征值？把初始向量按 $A$ 的特征向量展开 $b=\sum_i c_iv_i$（正规矩阵可正交对角化，来自前作谱定理），则 $A^kb=\sum_i c_i\lambda_i^kv_i$：$k$ 次乘幂让 $|\lambda_i|$ 大的项以 $|\lambda_i/\lambda_{\max}|^k$ 的指数优势压过其余项。因此 $b,Ab,\dots,A^{k-1}b$ 张成的空间几乎落在"最大模特征值对应的特征向量"所张成的低维子空间里，投影 $H_k=Q_k^TAQ_k$ 的特征对 $(y_i,\theta_i)$ 就是 Rayleigh-Ritz 逼近：$x=Q_ky_i$，$\theta_i=\dfrac{x^TAx}{x^Tx}$，$\theta_i$ 逐次逼近外层的 $\lambda$。这也解释了为何对**非对称**矩阵要当心：正文提到的伪谱（pseudospectrum）本质是问"对 $A$ 做一个小扰动 $\varepsilon$ 后特征值会跑到多大范围"——非正规矩阵对扰动的敏感度远高于对称矩阵，光看谱会误导（这与 CSAPP 第 2 章"浮点误差随扰动放大"是同一关切，只是放大倍数由矩阵的"非正规度"决定）。此机制在 page_122 的 Lanczos 数值例子中会再次精确显现。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原文此句 OCR 为 `emphas ize for 刀 e tric`，按上下文重建为 “for nonsymmetric matrices”（对非对称矩阵）。

Trefethen 与 Bau 强调：对非对称矩阵，我们可能从一开始就不想要 $A$ 的特征值！

当这些特征值病态（badly conditioned）时，这一点引导 Trefethen 与 Embree 走向伪谱（pseudospectra）的理论。

### Linear Systems by Arnoldi and GMRES（用 Arnoldi 与 GMRES 解线性方程组）

Arnoldi 已经为不断增长的 Krylov 子空间（Krylov subspaces）给出了一组出色的基——标准正交的诸 $q$，这些子空间由 $b, Ab, \ldots, A^{k-1}b$ 张成。

所以 Arnoldi 只是第一步。

在那个子空间内，求解 $Ax = b$ 的 GMRES 想法是：找出使 $\|b - Ax\|$ 达到最小的那个向量，即广义极小残量法（Generalized Minimum RESidual, GMRES）。

有了标准正交基，我们就能既准确又安全地进行计算。

<span style="color:#2471a3;">**[algorithm]**</span> 用 Arnoldi 的基 $q_1, \dots, q_k$ 的 GMRES（GMRES with Arnoldi's basis）：

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 算法步 1 的 OCR 为 `Find Yk t0 minimize the length of Hk+1,k − (l b 0 ...`，按 GMRES 残差恒等式 $\|b - A x_k\| = \|\beta e_1 - H_{k+1,k} y_k\|$（其中 $\beta = \|b\|$）重建为下列最小二乘问题。

```math
\min_{y_k}\ \big\| H_{k+1,k}\, y_k - (\beta, 0, \ldots, 0)^T \big\|
```

然后第 2 步取 $x_k = Q_k y_k$ 作为近似解。

求 $y_k$ 其实是一个最小二乘问题（least squares problem），其系数矩阵是 $(k+1)\times k$ 的 Hessenberg 矩阵。

$H_{k+1,k}$ 在第一子对角线以下全部为 0，正是这些 0 让 GMRES 格外快速。

> <span style="color:#1e8449;">**[note] Note（译者注：GMRES 的残差是多项式极小化，重启就是放弃嵌套）:**</span> 先补一笔原注漏掉的复杂度：Arnoldi 的第 $k$ 步是「一次 matvec 加 $k$ 次长度 $n$ 的内积与减法」，所以每步是 $O(\mathrm{nnz}+nk)$ 而不是 $O(\mathrm{nnz}+k)$；$K$ 步合计 $O(K\cdot\mathrm{nnz}+nK^2)$，其中第二项是正交化，$K$ 上千时它反客为主。吉文斯旋转那 $O(k)$ 只作用在 $(k+1)\times k$ 的小矩阵上，是账本里最便宜的一项 —— 这正是「海森伯格结构让 GMRES 格外快速」的准确内容：**快的不是乘法，是小矩阵上的增量分解**。史实坐标：这套算法出自 Saad 与 Schultz 1986 年的论文，登在 SIAM Journal on Scientific and Statistical Computing 第 7 卷第 3 期、856 至 869 页（页码与卷期对得上；DOI 我未能一手核实）。
> 
> 数值上最该亲手做一遍的是重启的失败。取 $A=I+3N$（$N$ 为严格上移位），$n=100$，它的特征值全是 $1$。全 GMRES 的相对残差：$k=1$ 时 $0.963$，$k=10$ 时 $0.597$，$k=50$ 时 $0.0695$，$k=80$ 时 $0.0109$，$k=99$ 降到机器零。改 GMRES(10) 重启，跑满 30 轮（300 次 matvec），残差停在第 $0.89392$ 位上再也不动。同一台机器、同一个矩阵，多花三倍乘法，换来的是零进展。
> 
> 机制在一行等式里：$\|r_k\|=\min\{\|p(A)b\|: p(0)=1,\ \deg p\le k\}$。三件事同时读出来。其一，全 GMRES 每步都在一个**更大**的子空间上做同一个极小化问题，$K_k\subset K_{k+1}$ 保证残差范数单调不增。其二，restart（重启）把多项式度数卡在 $m$，等于每轮只解一个固定的小问题后把答案收走、重新开始 —— 嵌套性被强行打断，单调性失去保证，实测就是「原地踏步」而不是「慢慢收敛」。其三，谱全等于 $1$ 却仍要 99 步，说明「特征值决定收敛速度」在非对称情形根本不成立；正文 page_121 那句「对非对称矩阵可能从一开始就不想要特征值」，量化后果就是这个例子。
> 
> 存储那一侧也很具体。GMRES 要留住全部基向量 $q_1,\dots,q_k$，即一个 $n\times k$ 的矩阵，$n=10^6$、$k=200$ 时是 $1.49$ GiB。这笔开销不是「多一点内存」：每一步正交化都要把这 $k$ 个向量从头读一遍，工作集 1.49 GiB 远超任何缓存层，于是每步的墙钟由主存带宽决定。重启把工作集压到 $m\cdot n\cdot 8$ 字节，$m=10$ 时降到 80 MB —— 收敛更慢，但每步更快，实践中比的是两者相乘。这条「内存换收敛、cache 换步数」的权衡，用 CSAPP 第 6 章的存储层次语言说最清楚：同一份数学，换了工作集大小就有两种完全不同的实际性能，而算法书上只写步数。
> 
> 这条等式还顺手解释了「有限步终止」：$k=n$ 时 $K_n=\mathbb{R}^n$，精确解就在子空间里，残差必为零，所以 GMRES 至多 $n$ 步收尾。但对非对称矩阵这个上界是真会用满的（上面那个例子用了 99 步，$n=100$），这与对称正定时 CG 通常几十步就收敛形成鲜明对照 —— 同一族 Krylov 方法，对称与非对称的实际表现差距就出在这一处。
> 
> 最后提醒一处易混点：$H_{k+1,k}$ 的小型最小二乘本身完全可以用 §II.2 的正规方程直接解，但没人这么写 —— 因为 $(k+1)\times k$ 的 Hessenberg 已被吉文斯旋转化成上三角，代价 $O(k^2)$ 且天然给出每一步的残差 $|g_{k+1}|$（不必真的算出 $x_k$ 再求 $b-Ax_k$）。这正是下一节 §II.2「用 QR 解最小二乘」的迷你版：同一个小矩阵、同一串旋转、同一个上三角，只不过旋转是边走边做的。也正是因为残差是这副产物，GMRES 的实现能在迭代中途就准确报出残差：残差是旋转过程的副产品，不是额外的一次矩阵-向量乘法。

---

---

> <span style="color:#7f8c8d;">Strang §II.1, p.117</span>

---

<!-- page 122: 书页 118, OCR page 22 -->

### Computations with Large Matrices（大规模矩阵的计算）

### Symmetric Matrices: Arnoldi Becomes Lanczos（对称矩阵：Arnoldi 变为 Lanczos）

假设矩阵是对称的（symmetric）：$A = S$。

在这个重要的情形下，会多出两个额外的事实（extra facts）。

**事实 1**：$H_k = Q_k^T S Q_k$ 也是对称的。

它确实是对称的——取转置后显然得到 $H_k^T = H_k$。

**事实 2**：$H_k$ 是三对角的（tridiagonal）：因为只存在一条下对角线，所以也只存在一条上对角线。

> <span style="color:#1e8449;">**[note] Note（译者注：Lanczos 的三项递推在实数里是定理，在浮点里只是近似）:**</span> 先把「只保留最近三项」的收益算成数字。取 $20\times 20$ 网格上的五点 Laplacian，$n=400$，特征值落在 $0.0447$ 到 $7.9553$（条件数 $178$）。走到 $k=60$ 步，Arnoldi 一共要做 $60\times 61/2=1830$ 次内积，Lanczos 只要 $60$ 次 —— 三十倍的差距，且这个比例随 $k$ 线性拉大。折算成浮点运算，Arnoldi 走到第 $K$ 步的总量是 $O(nK^{2})$，Lanczos 只有 $O(nK)$。精度没有因此变差：$T_{200}$ 的两个极端特征值算出 $0.044677$ 与 $7.955323$，与 $S$ 本身逐位相同。
> 
> 为什么只需三项？把 $q_k^T$ 乘在 $Sq_i$ 上做归纳就很清楚：$i=1$ 时 $Sq_1=a_1q_1+b_1q_2$，与 $q_k$ 正交；设 $Sq_{i}$ 只落在 $q_{i-1},q_i,q_{i+1}$ 上，则 $q_i^TSq_k=(Sq_i)^Tq_k$ 中三个下标都小于 $k$（当 $i\le k-2$），故为零。于是 $Aq_k$ 在 $q_1,\dots,q_{k-2}$ 上的系数全是零，$H_k$ 只剩三条对角线。写开就是本页算法框那四行：$w=Sq_k$、$a_k=q_k^{T}Sq_k$、$w=w-b_{k-1}q_{k-1}-a_kq_k$、$q_{k+1}=w/\|w\|$ —— 只有两项减法与一次内积，成本与 $k$ 无关。这条归纳（自行推导，三行）说明对称性买到的不是「近似更准」而是「投影结构自动为零」—— 去掉 $S=S^T$，$q_i^TSq_k$ 与 $q_k^TSq_i$ 不再相等，归纳立刻断掉，退回 Arnoldi 的 $O(k)$ 项。
> 
> 但这条定理在浮点算术里会塌。同一台机器上关掉重正交，实测最大非对角内积 $\max_{i\neq j}|q_i^Tq_j|$ 在 $k=50$ 时是 $9.4\times 10^{-14}$，$k=100$ 时已经涨到 $3.3\times 10^{-1}$，$k=200$ 时是 $5.9\times 10^{-1}$ —— 基向量实际上不再正交。每步做一次完整重正交，同一个量从头到尾稳在 $4.4\times 10^{-16}$。要命的是**特征值照样准到六位**：正交性流失与 Ritz 值收敛是同一件事的两面，一旦某个 Ritz 值逼近真特征值，$q_{k+1}$ 就会重新长出那个已经收敛的方向，于是看似「新」的向量其实是旧方向的复本。所以实用代码的选择是二选一：要么重正交（每步成本从 3 个向量拉回 $k$ 个，退化成 Arnoldi 的价格），要么接受「特征值可信、特征向量不可信」这句话。这一现象的严格分析通常归到 Paige 在 1971 与 1972 年的工作，但我未能一手核实其卷期与页码，所以上面只给现象与实测量。
> 
> 三项递推对 page_125 的共轭梯度法来说是决定性的：它把整段历史压进三根线，于是每步只需要一次 $Sd$、两个内积、三次向量加法，内存只留两个向量（$q_{k-1}$ 与当次的 $w$），与 $k$ 无关。这正是 Lanczos 与 CG 能在 $n=10^6$ 的问题上跑、而 GMRES 必须考虑基向量存储的原因：$n=10^6$ 时 Lanczos 全部基向量只占几十 MB 量级，GMRES 存 200 步就要 1.49 GiB。反过来说，任何破坏对称性的改动（预处理做错、$S$ 只在纸面上对称）都会让三项递推失效，算法退回「要留全部历史」的境地；CG 的最短递推是它的优点，也是它最脆的地方 —— 一旦 $S$ 不对称，理论上连收敛都无从谈起。同一副三对角线交给 page_123 的移位 QR 迭代，还能把谱直接算出来 —— 加上 CG，正是原注说的「一鱼三吃」：一条递推同时供出特征值、线性方程组的解与特征向量。
> 
> 跨课程看，三项递推不是矩阵专有的巧合。数值分析里的 Chebyshev 与 Legendre 这一族 orthogonal polynomials（正交多项式）对内积封闭，于是任何三项递推都能把 $x p_k$ 展开成 $p_{k+1},p_k,p_{k-1}$ 的组合 —— 与这里 $Sq_k$ 只落在三个 $q$ 上完全同构。更精确的对应是 Gauss 型求积：给定 $S$ 与起点 $b$，可以定义一条谱测度，而 $T_k$ 的特征值恰好是这条测度的 $k$ 个 Gauss 求积节点，这个构造通常就叫 Stieltjes 过程。这就解释了本页最反直觉的一句话「$T_k$ 的特征值求起来很快、又能逼近 $S$ 的特征值」：Gauss 求积对 $2k-1$ 次多项式精确，等价于说 $k$ 个节点已经抓住了测度的前 $2k$ 阶矩 —— 矩正是 $b^TS^jb$ 这些量。

三对角矩阵 $H$ 带来成本上的大幅节省——Arnoldi 迭代（iteration）只需一步正交化（orthogonalization step）。

其余的正交性是内建的，因为 $H$ 是对称的 Hessenberg 矩阵（symmetric Hessenberg，因而是三对角的）。

下面是更简洁记号的 Lanczos：用 $a_k$ 表示主对角线（main diagonal）上的元素，用 $b_{k-1}$ 表示上、下对角线上的元素，$a$ 与 $b$ 取代了 Arnoldi 矩阵 $H$ 中的各个 $h$。

<span style="color:#2471a3;">**[algorithm]**</span> 对对称矩阵 $S$ 的 Lanczos 迭代（Lanczos iteration for $S = S^T$）：

```math
q_1 = b / \|b\|
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 原样为 `： 0 ， ql`，此处注释行内容为 $v_0 = 0$、$q_1 = b/\|b\|$。

对 $k = 1, 2, 3, \ldots$ 执行（for $k = 1, 2, 3, \dots$）：

```math
\begin{aligned}
w &= S q_k \\
a_k &= q_k^{\,T} w \\
w &= w - b_{k-1} q_{k-1} - a_k q_k \\
q_{k+1} &= w / \|w\|
\end{aligned}
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 上述循环体中的 4 个算式由 OCR 碎片 `000`、`鬱 = Sqk`、`Ok = qk 鬱`、`鬱 = 一 b 一 lq 一 1`、`一 ak qk`、`qk+l = 鬱 /`（其中 `鬱` 代表向量 $w$）按标准对称 Lanczos 迭代重建。

（对称 Arnoldi 情形，symmetric Arnoldi）

算法右侧的第 2 步 正交化（Orthogonalize）作用在 $b, Sb, S^2 b, \ldots$ 上，$w$ 代表本次迭代新开始的向量。

主对角元（diagonal entry）$a_k$ 落在 $H_k$ 中。

$w$ 与早先诸 $q$ 正交（orthogonal to earlier $q$'s）。

离对角元（off-diagonal entry）$b_k$ 是下一次的基底。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 行 `b l tO 一 1`、`Diagonal en try in 丆 is ak`、`Off-diagonal entry in is` 表明：作者在算法框下方用 $a_k$ 与 $b_k$（即原文 $b_{k-1}$）标出了 $H_k$ 中的对角元与离对角元，右侧注释与上述迭代式逐一对应；算法码区右缘散落的 `2`、`(symmetric Arnoldi)` 等碎片为原书排版移位所致，已并入注释行处理。

把对三对角矩阵 $T_k$ 的写法换成对 Hessenberg 矩阵 $H_k$ 的写法，下面就是 Lanczos 的关键事实（key facts），它们只是从 Arnoldi 直接抄过来的：

方程（3）与（4）：$Q_k^T S Q_k = T_k$，以及 $S Q_k = Q_{k+1} T_{k+1,k}$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 的 `（ 5 ）` 与 `QkTSQk` 表明：左边关系式即原书方程（5），右边是式（3）—（4）在对称情形下的写法，其中 $T_k$ 为三对角矩阵，$T_{k+1,k}$ 是 $(k+1)\times k$ 的三对角（下为次对角线非零）。

“$T_k$ 的特征值（求起来很快）逼近 $S$ 的特征值。”——要是这句话永远、精确地成立就好了！

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此段 OCR 为 `Trefeth en an d B au cre ate a diagonal matrix S wi th 201 equally spaced eigenvalues from 0 to 2 ， and also two larger eigenvalues 2 · 5 an d 3 · 0 · S tarting from a random vector b, Lanczos at s tep 9 approximates = 2 · 5 an d 3 · 0 exponentially well · The other 7 eigenvalues of 9 = Q9 SQ9 bunch near 0 an d 2 · But they don ， t capture individual eigenvalues in th at group 0f 201 /\'s.`，已重建为：Trefethen 与 Bau 构造了一个对角矩阵 $S$，其特征值是从 0 到 2 等间距分布的 201 个，外加两个更大的特征值 $2.5$ 与 $3.0$。

Trefethen 与 Bau 构造了一个对角矩阵 $S$，其 201 个特征值在 0 与 2 之间等间距（equally spaced）分布，另外还有两个更大的特征值 $2.5$ 与 $3.0$。

从随机向量 $b$ 出发，Lanczos 在第 9 步就把 $2.5$ 与 $3.0$ 逼近得指数般精确（exponentially well）。

而 $T_9 = Q_9^T S Q_9$ 的其余 7 个特征值聚集（bunch）在 0 与 2 附近。

但它们并没有把那一组 201 个 $\lambda$ 中的单个特征值分辨出来。

问题出在非正交的 $q$ 上：精确的 Lanczos 迭代本应保证诸 $q$ 正交。

Lanczos 很有价值，但在实践中必须格外小心才能让所有 $q$ 都保持正交——这一点对 Gram-Schmidt（格拉姆-施密特）也一样。

---

> <span style="color:#7f8c8d;">Strang §II.1, p.118</span>

---

<!-- page 123: 书页 119, OCR page 23 -->

> <span style="color:#7f8c8d;">页眉（running head）：11.1. Numerical Linear Algebra（数值线性代数），页码 119。本页为正文页，逐句完整行内双语翻译。</span>

### 11.1 Numerical Linear Algebra（数值线性代数）

<span style="color:#2471a3;">**[section]**</span> **Eigenvalues of Tridiagonal $T$ by the QR iteration（用 QR 迭代求三对角矩阵 $T$ 的特征值）**

如何计算一个对称三对角矩阵（symmetric tridiagonal matrix）$T$ 的特征值（eigenvalues）？这正是对称特征值问题（symmetric eigenvalue problem）的关键所在。
原始矩阵 $S$ 已由 Lanczos（兰乔斯）迭代化简为三对角矩阵 $T = Q^TSQ = Q^{-1}SQ$——特征值不变，因为 $T$ 与 $S$ 相似（similar）。
那些三对角带以外的零元素也可以来自 2×2 的吉文斯旋转（Givens rotations）。
此时我们已经有一个三对角对称矩阵 $T = T_0$；为求其特征值，一个几乎凭空出现的惊人想法浮出水面：
**1.** 用 Gram-Schmidt（格拉姆-施密特）正交化或 Householder（豪斯霍尔德）反射把 $T_0$ 分解（factor）为 $Q_0R_0$，即 $T_0 = Q_0R_0$。
**2.** 把 $Q_0$ 与 $R_0$ 这两个因子反转次序相乘，得到 $T_1 = R_0Q_0 = Q_0^{-1}T_0Q_0$。
**3.** 重复。重复。再重复。（Repeat. Repeat. Repeat.）
新的 $T_1 = Q_0^{-1}T_0Q_0$ 与 $T_0$ 相似（特征值相同），而且新的 $T_1$ 依旧保持三对角（tridiagonal，见习题 Problem 1），所以下一步以及之后的所有步骤仍然很快。

> <span style="color:#1e8449;">**[note] 译者注（第一性原理洞察）:**</span> QR 迭代为什么收敛？它其实是**幂法的推广**。回想一维幂法：$x_{k+1}=Ax_k/\|Ax_k\|$ 反复乘并归一化，$x_k$ 收敛到模最大的特征向量，收敛率由 $|\lambda_2/\lambda_1|$ 决定。QR 迭代 $T_k=Q_kR_k,\ T_{k+1}=R_kQ_k$ 是"同时"对全部列做这件事：$Q_k$ 的各列逼近 $T_0$ 按模排序的特征向量，$R_kQ_k=Q_k^TT_kQ_k$ 只是把谱"重新聚集"——因为 $Q_k^T T_k Q_k=Q_k^T(Q_kR_k)Q_k=R_kQ_k$，这正是正交相似变换（特征值不变，正文已述）。随 $k$ 增大，特征向量方向被逐块锁定，$T_k$ 的非对角元从底端开始衰减，对角化逐步完成，最先剥离的是模最小的特征值（出现在末位）。用你的特征值直觉：一个收敛到对角形的相似矩阵，对角线必然给出全部特征值。所谓"惊人想法"其实是把一维幂法升级为"同时的多向量幂法+正交归一"。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 句「翁 是 豆 襯 历 ago 刀 (ProbIem 1)」为符号噪声，依上下文重建为「新的 $T_1$ 仍为三对角矩阵（见 Problem 1）」。
> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR「＝ QTSQ = Q-ISQ」重建为 $T = Q^TSQ = Q^{-1}SQ$；「0f / t0 / th e / 行 om」等为字形噪声，均已按语境修正。

最妙的是，这一串相似矩阵 $T_0, T_1, T_2, \ldots$ 将逐步逼近一个对角矩阵（diagonal matrix），而这个对角矩阵揭示出原始矩阵 $T_0$ 的特征值（保持不变的那些）。
最先显现的那个特征值落在 $T_k$ 的最后一个元素（last entry）上——这就是计算特征值的 QR 算法（QR algorithm）。
当 QR 算法逐渐为人所知时，曾在数值线性代数（Numerical Linear Algebra）领域引起轰动；但数值分析师（numerical analysts）是严肃的人，拿到一个好算法就会立刻开始改进它。
这一次他们大获全胜：改进几乎不费任何代价（而且确实奏效）。
改进后的算法是移位 QR（shifted QR），也叫带位移的 QR（QR with shifts）；所谓位移（shift），就是在 QR 步骤之前先减去单位矩阵（identity matrix）的某个倍数，再在 QR 步骤之后把它加回来。

<span style="color:#2471a3;">**[note]**</span> **以位移 QR 求特征值（QR algorithm with shifts）**：在第 $k$ 步选取一个位移 $s_k$，先分解

```math
T_k - s_kI = Q_kR_k
```

再反转因子、加回位移：

```math
T_{k+1} = R_kQ_k + s_kI
```

所有 $T_k$ 的特征值完全相同，因为它们是相似矩阵（similar matrices）；每一个新的 $T_{k+1}$ 都等于 $Q_k^TT_kQ_k$，仍保持对称，因为 $Q_k^T = Q_k^{-1}$（$Q_k$ 为正交矩阵，orthogonal）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR「砰 1 is QV Q … Qk¯ = Q 1（一）… = 0《1Q（6）」等噪声严重，依 $T_k = Q_kR_k$ 与正交性重建为 $T_{k+1} = Q_k^T(T_k - s_kI)Q_k + s_kI = Q_k^TT_kQ_k$，即原书式 (6)。

选取得当的位移会大大加快 $T_k$ 系列向对角矩阵的收敛；由 Wilkinson（威尔金森）建议的位移基于 $T_k$ 的最末 2×2 子矩阵：

```math
\begin{bmatrix} a_{n-1} & b_{n-1} \\ b_{n-1} & a_n \end{bmatrix}
```

取该最末 2×2 子矩阵中靠近末对角元 $a_n$ 的那个特征值作为位移 $s$，就得到 Wilkinson shift（威尔金森位移）。
移位 QR 达到三次收敛（cubic convergence），这极为罕见；在接下来的那个例子中，次对角元将从 $\sin\theta$ 变为 $-(\sin\theta)^3$。
一个典型三对角矩阵 $T$ 的特征值只需约 $O(n^2)$ 次浮点运算（flops）即可算到足够精度。

> <span style="color:#1e8449;">**[note] 译者注（算法效率视角）:**</span> 无位移的 QR 迭代在特征值靠近时收敛很慢（比率由相邻特征值之比决定，类似幂法被 $|\lambda_2/\lambda_1|\approx1$ 卡住）。位移 $s_k$ 的妙处在于把目标"搬到原点"：$T_k-s_kI=Q_kR_k$ 后，$T_{k+1}=R_kQ_k+s_kI$，谱不变，但迭代实际在放大 $|1/(\lambda_i-s_k)|$ 的分辨率——选 $s_k$ 靠近某个特征值就相当于对该特征值做"反向幂法"。Wilkinson 位移取最末 2×2 块中离 $a_n$ 近的特征值，使右下角块加速解耦。正文的 $\sin\theta\to-(\sin\theta)^3$（下一页给出 2×2 验证）就是**三次收敛**：误差每步从 $\varepsilon$ 变 $\varepsilon^3$，即每次迭代让有效数字数量乘以 3。复杂度上，三对角结构让每步 QR 只需 $O(n)$（吉文斯旋转扫一条子对角线），总成本约 $O(n^2)$ flops——与 page_121 的 GMRES 每步 $O(k)$ 增量是同一套"珍惜每个零"的思路。三次收敛 + 线性成本的组合，正是"先化简到三对角、再迭代"这个两层策略的回报。

---

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 尾行「take only 0 3 / ） flops for accuracy」符号残缺；按三对角 QR 每步 $O(n)$、总计约 $O(n^2)$ 次运算的常规复杂度重建为「只需约 $O(n^2)$ 次 flops」。

---

> <span style="color:#7f8c8d;">Strang §II.1, p.119</span>

---

<!-- page 124: 书页 120, OCR page 24 -->

> <span style="color:#7f8c8d;">页眉（running head）：Computations with Large Matrices（大规模矩阵的计算），页码 120。本页为正文页：顶部是上一页预告的示例（example）在本页的公式展示，OCR 残缺较重，已重建并加注说明；其下为小节「Computing the SVD」。本页无习题。</span>

<span style="color:#2471a3;">**[example]**</span> **Example（示例）：一步移位 QR 把误差立方化（cubing the error in one step）**

这里展开上一页所说的「接下来的例子」：对一个小对称矩阵施加一步带位移的 QR（shifted QR）。
该步先做 QR 分解（factor）$T_0 - s_0I = Q_0R_0$，其正交因子 $Q_0$ 是吉文斯型的旋转矩阵（rotation matrix）：

```math
Q_0 = \begin{bmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{bmatrix}
```

随后反转因子并加回位移，得 $T_1 = R_0Q_0 + s_0I$；结果正如上一页预告的那样：次对角元从 $\sin\theta$ 一步变成 $-(\sin\theta)^3$。
正如这一展示的收尾句所说，该步在一步之内把误差立方化了（has cubed the error in one step）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页顶部的公式展示在 OCR 中被完全打散，仅残存 cos、sin、0、$1+\sin^2\theta$、$Q_0$、Shift 等片段，无法逐元复原原书展示的矩阵；以上仅按 §11.1 的数学语境重建其结构，精确矩阵形式请以原书第 120 页为准。

<span style="color:#2471a3;">**[section]**</span> **Computing the SVD（计算奇异值分解 SVD）**

对称特征值问题 $Sx = \lambda x$ 与奇异值分解 $A = U\Sigma V^T$ 之间的主要区别是什么？在计算那些 $\lambda$ 与 $\sigma$ 之前，我们能把 $S$ 与 $A$ 化简到什么程度？
由于 $Q$ 正交（orthogonal），$S$ 与 $Q^{-1}SQ = Q^TSQ$ 的特征值完全相同，所以我们在 $Q^{-1}SQ$（它保持对称）中制造零的自由度（freedom）是有限的。
如果硬要在 $Q^{-1}SQ$ 里制造太多的零，最后的 $Q$ 反而会把它们破坏掉；理想的 $Q^{-1}SQ$ 是三对角的（tridiagonal），只有三条对角线（diagonals）。
即使 $Q_1$ 与 $Q_2$ 不同，$A$ 与 $Q_1^TAQ_2$ 的奇异值（singular values）也相同；在 $Q_1^TAQ_2$ 中制造零的自由度要大得多——只要 $Q$ 选得合适，它就能成为双对角（bidiagonal）矩阵（只有两条对角线）。
我们可以很快找到 $Q$、$Q_1$ 与 $Q_2$，使得 $Q^{-1}SQ$ 是三对角的（用于 $\lambda$），$Q_1^TAQ_2$ 是双对角的（用于 $\sigma$）；原书把这两个式子并排展示，编号 (7)：

> <span style="color:#1e8449;">**[note] Note（译者注：自由度账本——一次旋转买两个零，账要逐项对上）:**</span> 原注说「本质是可用的自由度不同」，这句话可以变成一张能逐项对账的表。$n\times n$ 对称矩阵装 $n(n+1)/2$ 个数，三对角只装 $2n-1$ 个：$n=5$ 时是 $15$ 与 $9$，差 $6$；$n=10$ 时 $55$ 与 $19$，差 $36$；$n=50$ 时 $1275$ 与 $99$，差 $1176$。三个差额都恰好是 $(n-1)(n-2)/2$，也就是组合数 $C(n-1,2)$，而它同时是 Givens 旋转的次数：第 $j$ 轮要消掉第 $j$ 列对角以下的 $n-j-1$ 个元，合计 $\sum_{j=1}^{n-2}(n-j-1)=C(n-1,2)$，实测 $n=5,10,50$ 分别是 $6,36,1176$ 次旋转，与差额一位不差。
> 
> 为什么「一位不差」值得强调？因为一次旋转消掉的是**一个存储位置**而不是「一个矩阵元素」：对称性让 $(i,j)$ 与 $(j,i)$ 是同一个数，转一下两个位置一起归零，账本上只算一个。若换成一般矩阵，同样一次旋转只买一个零，自由度与旋转次数的对应就散掉了。这正是「对称 Hessenberg 只能是三对角」的代数根源：Hessenberg 只规定第一子对角线以下为零，对称再把上方镜像过去，剩下的可非零位置只可能是三条对角线 —— 这是纯代数的结论，与算法无关。
> 
> 更深一层的机制是信息守恒。降阶并没有销毁那 $C(n-1,2)$ 个数，而是把它们**搬进了** $Q$ 的角度里：$Q$ 有 $n(n-1)/2$ 个旋转参数，$S$ 有三条对角线，两者合起来正好还是 $n(n+1)/2$ 个数。所以「化简到规范形」的正确读法是换坐标，而不是压缩；一旦你以为在压缩，就会误以为三对角「丢掉了信息」，从而看不懂后面为什么 $Q$ 必须留着 —— page_123 的 QR 迭代每一步都要拿 $Q$ 的乘积去追踪特征向量，靠的正是这些被搬走的角度。
> 
> 为什么不能再多消一个？想把某个 $b_k$ 也变零，等价于要求 $Q$ 的某一列同时满足 $SQ e_k=\lambda Qe_k$ —— 也就是 $Q$ 的某列恰好是特征向量。而求特征向量没有有限步算术，page_134 的阿贝尔论证已另注，于是三对角就是有限步内能达到的最稀形态。一般矩阵的账更宽：$m\times n$ 有 $mn$ 个数，双对角只留 $m+n-1$ 个，差 $(m-1)(n-1)$（$100\times 60$ 是 $6000-159=5841$），这就是「能消掉的零」的上界。宽出来的部分来自左右两个独立正交矩阵 —— 奇异值只依赖 $A^TA$，所以左、右两侧的角度可以各自花掉，比相似变换多一倍自由度；而所以分工是明确的：有限步只负责化简到最稀的规范形（三对角或双对角），page_123 的移位 QR 迭代负责在规范形上把谱榨出来 —— 两边各管一段，不要指望有限步直接给出特征值。两条对角带乘起来正好生成 $A^TA$ 的三对角结构，这也是正文强调「不要显式乘出 $A^TA$」时仍要盯着双对角形的原因。
> 
> 用 6.042J 的计数语言收尾：这张表就是一个「参数计数给出算法下界」的模板 —— 要降到某个形态，至少需要与该形态的参数差同样多的零化步骤，任何算法都不可能更快；而 Householder 或 Givens 又能把这个下界达到，于是下界与构造重合。这种「数一数就知道最优」的论证在数值线性代数里遍地都是，比逐个分析算法步数高效得多。取 $n=1000$ 看一眼规模感：对称矩阵 $500500$ 个数，三对角只留 $1999$ 个，差 $498501$，这就是一次完整三对角化要做的旋转次数，与 $n^2/2$ 同阶。

```math
Q^{-1}SQ = \begin{bmatrix} a_1 & b_1 & 0 \\ b_1 & a_2 & b_2 \\ 0 & b_2 & a_3 \end{bmatrix}
```

```math
Q_1^TAQ_2 = \begin{bmatrix} c_1 & d_1 & 0 \\ 0 & c_2 & d_2 \\ 0 & 0 & c_3 \end{bmatrix}
```

读者想必知道，$A$ 的奇异值正是 $S = A^TA$ 的特征值的平方根；而 $Q_1^TAQ_2$ 的不变奇异值，是 $(Q_1^TAQ_2)^T(Q_1^TAQ_2) = Q_2^TA^TAQ_2$ 的不变特征值的平方根。
把（双对角矩阵）$^T$ 乘以（双对角矩阵），乘积里就会看到三对角的结构。
这给了我们一个不应采纳的选项：不要乘出 $A^TA$ 再去求它的特征值——那是多余的工作，而且会把问题的条件数（condition）不必要地平方化（squared）。
求 SVD 的 Golub-Kahan（戈卢布-卡汉）算法直接对 $A$ 进行操作，分两步：
**1.** 找 $Q_1$ 与 $Q_2$，使 $Q_1^TAQ_2$ 化为如上面那样的双对角矩阵。
**2.** 调整移位 QR 算法，以保持这个双对角矩阵的奇异值不变。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接）:**</span> 这句是全书最重要的数值警示之一。$A^TA$ 的特征值 = 奇异值平方 $\sigma_i^2$，于是 $\mathrm{cond}(A^TA)=\mathrm{cond}(A)^2$。CSAPP 第 2 章告诉我们：双精度机器精度约 $\varepsilon\approx2.2\times10^{-16}$（约 16 位十进制有效数字），而求解线性方程时误差按条件数放大——条件数 $10^8$ 的 $A$，经 $A^TA$ 会变成 $10^{16}$，解的有效数字几乎丢光。这正是 Golub-Kahan 算法**直接对 $A$ 双对角化**、从不显式构造 $A^TA$ 的原因。同样的逻辑在 §II.2 反复出现（page_128 正规方程 vs QR），可以说"**能不乘出 $A^TA$ 就不乘**"是数值线性代数第一戒律。代价方面：第 1 步双对角化 $O(mn^2)$、后续 $O(n^2)$，对中等规模矩阵完全可以接受——所以正文才强调 SVD 是"可计算的"，只是"不能动辄做几千次"。

---

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 在步骤 1 中写作「as in (8)」，与本页公式 (7) 的编号不一致（可能为原书排版编号或 OCR 误读），此处统一按本页出现的编号 (7) 处理。

第 1 步需要 $O(mn^2)$ 次乘法，把一个 $m\times n$ 矩阵化为双对角形式（bidiagonal form）。
此后的各步只与双对角矩阵打交道；通常再花 $O(n^2)$ 次乘法，就能求出奇异值（精度接近机器精度，machine precision）。
完整的算法见 Golub–Van Loan（第 4 版，戈卢布-范洛恩《Matrix Computations》）第 489–492 页。
这些运算量（operation counts）对许多应用来说完全可以接受——SVD 是可以算出来的（computable）。
也有其他算法被提出并取得成功，但代价并非微不足道：你不能动辄就做几千次 SVD。
当 $A$ 真正很大时，本书后续的章节将介绍随机化方法（randomized methods），包括对原矩阵 $A$ 的随机采样（random sampling）——这种方法能处理大型矩阵。
其结果以极高的概率（high probability）是准确的；大多数赌徒都会说，一次好的随机采样有好结果几乎是必然的（certain）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本节 OCR 中的「= UEVT」/「UEVT」均按术语表重建为 $A = U\Sigma V^T$；「S tep 1 requ ires 0（m 2）」按 bidiagonalization 的常规 Householder 复杂度重建为 $O(mn^2)$ 次乘法；「GoIub-Kahan」修正为 Golub-Kahan。

---

> <span style="color:#7f8c8d;">Strang §II.1, p.120</span>

---

<!-- page 125: 书页 121, OCR page 25 -->
> <span style="color:#7f8c8d;">本页为书页 121（OCR 文本第 25 页），隶属 §11.1 Numerical Linear Algebra（数值线性代数）。页眉 "11.1 Numerical Linear Algebra" 与页码 121 为页眉页脚，不译。结构单元清单：① 主题 Conjugate Gradients for $Sx=b$（用共轭梯度法解 $Sx=b$）；② CG 算法总体说明；③ Key idea：对称性 → Hessenberg 化为三对角；④ $S$-范数与误差度量；⑤ 共轭梯度迭代算法框；⑥ 两大事实（残差正交、方向 $S$-正交）；⑦ CG 作为极小化算法；⑧ 公式 (8) 误差界与图注 "CG Method"。</span>

### 用共轭梯度法解 $Sx = b$（Conjugate Gradients for $Sx = b$）

本节介绍的算法即 conjugate gradient algorithm（共轭梯度算法，简称 CG），它专门适用于 symmetric positive definite matrices（对称正定矩阵）$S$，用来求解方程 $Sx = b$。
理论上它至多 $n$ 步即给出 exact solution（精确解），只是这些步骤比 elimination（消元）更慢。
实践中，对 large matrices（大型矩阵），它远在 $n$ 步之前就已给出 excellent results（出色的结果）。
正是这一发现让整个想法获得复兴，如今 CG 已是公认的最出色算法之一；这正是一切 Krylov methods（Krylov 方法）中最负盛名者的历史。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 的 "C0njugate"、"s ymmetri c" 等拼写噪声已按 conjugate、symmetric 重建；标题 "Sæ" 中 æ 是 OCR 将 $x$ 认错；"in steps" 丢失字母 $n$——共轭梯度理论上至多 $n$ 步收敛，故补作"在 $n$ 步内"。

<span style="color:#2471a3;">**[note]**</span> **关键思想（Key idea）**：由于 $S$ 对称，Arnoldi（阿诺尔迪）迭代中的 Hessenberg matrix（海森伯格矩阵）$H$ 会变成 Lanczos（兰乔斯）迭代中的 tridiagonal matrix（三对角矩阵）$T$。
因为 $T$ 的每一行、每一列只有三个非零元，symmetric case（对称情形）计算起来便格外快速。

<span style="color:#2471a3;">**[note]**</span> 而且 $S$ 不仅 symmetric（对称），还是 positive definite（正定）。
此时 $x^{T}Sx$ 给出一个相当合适的 norm（范数）用来度量误差，即 S-norm（$S$ 范数），用以衡量迭代若干步之后的误差。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接）:**</span> 解 $Sx=b$ 与极小化二次函数 $\varphi(x)=\tfrac12x^TSx-x^Tb$ 是同一件事：$\nabla\varphi=Sx-b$ 恰是残差（负梯度方向），而正定保证 $\varphi$ 是开口向上的椭球面（Boyd §4.2 的最优性条件 $\nabla\varphi=0$ 在此就是正规方程）。这给出两条重要连接。其一，CG 是**极小化算法**，因此可推广到非二次问题——Boyd §9 的梯度法/最速下降会遇到的锯齿（zigzag）振荡，正是因为它每次只沿当前梯度方向搜索；CG 的修补是让搜索方向两两 $S$-正交（$d_i^TSd_j=0$），在 $S$ 内积下"每步走完一个新维度"，从而 $\varphi$ 沿这些方向被精确极小化。其二，证明"至多 $n$ 步精确"用的是 6.042J 的维数论证：残差 $r_0,r_1,\dots$ 两两正交（$\varphi$ 极小 ⟹ 残差与新方向正交），$n$ 维空间里最多 $n$ 个非零两两正交向量，故第 $n$ 步必得 $r_n=0$。$S$-范数 $\|x\|_S^2=x^TSx$ 正是误差的"能量"，几何上是椭圆度量下点到解的距离。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR "cTSc" 实为 $x^{T}Sx$（$x$ 被误识为 $c$）；"appropnate n orm" 重建为 appropriate norm（适当范数）。

<span style="color:#2471a3;">**[note]**</span> 事实上，第 $k$ 次 conjugate gradient iterate（共轭梯度迭代点）$x_k$ 具有一个非凡性质：它在第 $k$ 个 Krylov subspace（Krylov 子空间）上极小化误差 $\|x - x_k\|_S$。
换句话说，$x_k$ 是 $b,\ Sb,\ \ldots,\ S^{k-1}b$ 的 best combination（最佳组合）。

<span style="color:#2471a3;">**[algorithm]**</span> **正定 $S$ 的共轭梯度迭代（Conjugate Gradient Iteration for Positive Definite $S$）**
以下为求解 $Sx=b$ 的 conjugate gradient iteration（共轭梯度迭代）步骤：

- 初始化（initialization）：$x_0 = 0,\quad r_0 = b,\quad d_0 = r_0$
- 进入循环（for loop），取 $k = 1, 2, \ldots, N$
- 步长（step length）：$\alpha_{k-1} = \dfrac{r_{k-1}^{T}r_{k-1}}{d_{k-1}^{T}S\,d_{k-1}}$，把 $x_{k-1}$ 推进到 $x_k$
- 近似解（approximate solution）：$x_k = x_{k-1} + \alpha_{k-1}d_{k-1}$
- 新残差（new residual）：$r_k = r_{k-1} - \alpha_{k-1}S\,d_{k-1}$，即 $b - Sx_k$
- 下一搜索方向（next search direction）：$d_k = r_k + \beta_{k-1}d_{k-1}$，其中 $\beta_{k-1} = \dfrac{r_k^{T}r_k}{r_{k-1}^{T}r_{k-1}}$

<span style="color:#2471a3;">**[note]**</span> 注意（Notice）：每一步只须做一次矩阵乘向量 $Sd$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 算法框 OCR 噪声极大："0 = 0 0 = b 确 ： ro" 重建为 $x_0=0,\ r_0=b,\ d_0=r_0$；"Tk—1Tk—1" 即 $r_{k-1}^{T}r_{k-1}$，"Qk" 即 $\alpha_{k-1}$，"俨" 即 $r_k$，$\beta$ 所在行被拆散，均按标准 CG 算法重建。

<span style="color:#2471a3;">**[theorem]**</span> 从上述步骤（耐心推导）可得到两大事实——zigzags（锯齿状振荡）消失了！

1. **残差正交**：误差残差 residuals（残差）$r_k = b - Sx_k$ 两两正交，即 $r_k^{T}r_j = 0$
2. **方向 $S$-正交**：搜索方向 directions（方向）$d_k$ 两两 $S$-orthogonal（$S$ 正交），即 $d_i^{T}S\,d_j = 0$

<span style="color:#2471a3;">**[note]**</span> 注意（Notice）：求解 $Sx - b = 0$ 与极小化 quadratic（二次函数）$x^{T}Sx - x^{T}b$ 是同一件事——其中一个正是另一个的 gradient（梯度）。
因此 conjugate gradient（共轭梯度法）同时也是一种 minimization algorithm（极小化算法），并能推广到 nonlinear equations（非线性方程）与非二次 cost functions（代价函数）。
本书 Part VII（第七部分）讨论 deep learning（深度学习）时本可以考虑它——只是那里的矩阵规模实在太大，不适合 conjugate gradient（共轭梯度法）。

<span style="color:#2471a3;">**[note]**</span> 最后，我们给出共轭梯度迭代 $k$ 步之后最简洁的 error estimate（误差估计）。
当 $S$ 的特征值 eigenvalues（特征值）well spaced（间隔良好、彼此分散）时，算法的成功最为显著：

> <span style="color:#1e8449;">**[note] Note（译者注：收敛率要分清谁带平方根——顺便改正原注一处归属）:**</span> 先修一处硬伤：原注把 $(\kappa-1)/(\kappa+1)$ 记在公式 (8) 头上，这是**最速下降**（steepest descent, SD）在能量范数下的每步收缩率（由 Kantorovich 不等式得到，Shewchuk 1994 的推导可查），不是共轭梯度法的界；同一个原注后半句又写「实际界用 $(\sqrt{\kappa}-1)/(\sqrt{\kappa}+1)$」，两句自相矛盾。以公式 (8) 的身份，正确的形式带平方根：$\|e_k\|_S \le 2\left((\sqrt{\kappa}-1)/(\sqrt{\kappa}+1)\right)^k\|e_0\|_S$。两者差的就是那个根号，而根号决定了量级：$\kappa=10^4$ 时前者收缩因子 $0.99980$、后者 $0.98020$。
> 
> 实测先把量级钉住。取 $n=1000$ 的对角 $S$、特征值对数间隔，能量范数相对误差压到 $10^{-6}$：$\kappa=100$ 时 SD 要 $469$ 步、CG 只要 $59$ 步；$\kappa=10^4$ 时 SD 要 $37445$ 步、CG 只要 $434$ 步。比值 $86$ 与 $\sqrt{\kappa}=100$ 同量级。理论最坏界也不妨算一遍：SD 的 $\lceil\ln(10^{-6})/\ln\frac{\kappa-1}{\kappa+1}\rceil=69078$，CG 的界给出 $725$ 步 —— 实测都优于最坏界，这是最坏情形与分析均值之间的正常差距。
> 
> 平方根从哪来？CG 的第 $k$ 步解等价于在所有 $p(0)=1$、次数不超过 $k$ 的多项式中选一个，使 $\max_{\lambda\in[\lambda_{\min},\lambda_{\max}]}|p(\lambda)|$ 最小；这个 min-max 问题的最优多项式是 Chebyshev 多项式的位移版本，而 $0$ 落在区间**外面**，区间外一点对应的 Chebyshev 椭圆参数正是 $(\sqrt{\kappa}-1)/(\sqrt{\kappa}+1)$。SD 则每步只沿当前负梯度走一条线，等于只拟合一次线性多项式，Kantorovich 不等式给的是 $(\kappa-1)/(\kappa+1)$。所以差别不是「CG 更聪明」，而是**一次拟合 $k$ 步优于每步只拟合一步** —— 这正是「共轭」二字的全部内容，也解释了为什么它值那份额外的存储与算术。
> 
> 根号也确实有它的边界。若 $S$ 只是对称而不正定，$[\lambda_{\min},\lambda_{\max}]$ 会把 $0$ 包在区间里面，$0$ 不再是「区间外的一点」，Chebyshev 椭圆参数那套论证整体失效，min-max 最优值可能根本降不下来 —— 这就是共轭梯度法必须要求正定的真正原因，它不是为了数值稳定，而是为了保证那个区间与 $0$ 的相对位置。反过来看 $\kappa=1$（$S$ 是单位阵的倍数）的极端：区间退化成一个点，$p$ 取一次多项式就精确，SD 与 CG 的第一步没有区别，两条界都变成 $0$。界前面的常数 $2$ 也不必当真，它是「从 $\|e_0\|$ 走到零」的过渡因子，对 $k\ge1$ 只是个位数级的余量。
> 
> 谱的**形状**比谱的**范围**更要紧，这一点可以量出来：把特征值换成只有 $4$ 个簇（每簇 $250$ 个重复值），$\kappa$ 仍是 $10^4$，CG 只要 **4** 步。这正是原注说「理论至多 $n$ 步、实际远小于 $n$ 步并不矛盾」的定量版本：聚簇的谱让 $k$ 个 Ritz 值几维之内就抓住全部主方向，与 page_122 那个「离群特征值先被 Lanczos 捕获」的机制同源 —— CG 与 Lanczos 本来就是同一条路的两个出口，一个解方程、一个求谱。
> 
> 跨课程收尾用 6.042J 的对数换底：把收缩率翻译成步数就是 $k=\lceil\ln(1/\varepsilon)/|\ln\rho|\rceil$，而 $\rho\to1$ 时 $|\ln\rho|\approx2/\sqrt{\kappa}$，于是 CG 的步数约 $\frac{\sqrt{\kappa}}{2}\ln\frac{2}{\varepsilon}$。这个换算是所有迭代法分析的通用扳手：它说明**降低 $\kappa$ 是线性的收益、改进每步常数只是线性前的系数**，所以 page_126 的预处理（找一个 $P$ 让 $P^{-1/2}SP^{-1/2}$ 的谱更集中）比任何微优化都值钱。史实坐标：CG 出自 Hestenes 与 Stiefel 在 1952 年发表的论文，登于 Journal of Research of the National Bureau of Standards 第 49 卷，页码我未能一手核实；上面两条界的推导见 Shewchuk《An Introduction to the Conjugate Gradient Method Without the Agonizing Pain》(1994)，http://www.cs.cmu.edu/afs/cs/academic/class/15859n-s21/RelatedWork/painless-conjugate-gradient.pdf 。

---

```math
\|x - x_k\|_S \le \left( \frac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}} \right)^{\!k} \|x - x_0\|_S \tag{8}
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 公式 (8) 按标准 CG 收敛界重建：OCR 将 $\lambda$ 误识为 "x"（"xmax" → $\lambda_{\max}$），"æolls" 实为 $\|x - x_0\|_S$，指数、括号与小写字母大量丢失。

> <span style="color:#7f8c8d;">图注 "CG Method"（CG 方法的收敛曲线）为英文图注，保留原文不译。</span>

---

> <span style="color:#7f8c8d;">Strang §II.1, p.121</span>

---

<!-- page 126: 书页 122, OCR page 26 -->
> <span style="color:#7f8c8d;">本页为书页 122（OCR 文本第 26 页）。页眉 "Computations with Large Matrices" 与页码 122 为页眉页脚，不译。结构单元清单：① Preconditioning for $Ax=b$（解 $Ax=b$ 的预处理）：思想与预条件方程 (9)；② 常见 preconditioner（预条件子）$P$ 的四种选择；③ multigrid method（多重网格方法）说明；④ Kaczmarz Iteration（Kaczmarz 迭代）：随机收敛与公式 (10)；⑤ 随机化版本与 norm-squared sampling（范数平方采样）；⑥ 页脚文献。</span>

### 解 $Ax = b$ 的预处理（Preconditioning for $Ax = b$）

预处理 preconditioning（预处理）的基本思想，是寻找一个 nearby（邻近的）问题，使其能被快速求解。
解释这个思想非常容易，真正的难题在于选出好的 preconditioner（预条件子）$P$。
对给定矩阵 $A$，思路是选取一个更简单、却又与 $A$ 接近的矩阵 $P$。
两者"接近"可理解为 $P - A$ 具有小范数（small norm），或者 $P - A$ 具有低秩（low rank）。
由于与 $P^{-1}$ 打交道速度更快，我们转而求解预处理方程 $P^{-1}Ax = P^{-1}b$，以代替原来的 $Ax = b$：

> <span style="color:#1e8449;">**[note] 译者注（第一性原理洞察）:**</span> 预处理的思想一句话：**迭代的难度不在 $A$ 本身，而在 $A$ 的谱形状**（CG 依赖 $\kappa$，分裂迭代依赖 $\rho(S^{-1}T)$，page_120 的误差方程是模板）。左乘 $P^{-1}$ 相当于换坐标系，让 $P^{-1}A$ 的谱"聚拢到 1 附近"——谱越像单位阵，迭代越快。因此选 $P$ 有两条互相矛盾的要求：$P$ 要**像** $A$（$P^{-1}A\approx I$），又要**便宜可逆**（每步只解 $P$ 系统）。正文四种选择正是在这条光谱上取点：对角 $P$ 最便宜但修正弱（Jacobi），三角 $P$ 稍贵但捕捉更多结构（Gauss-Seidel），ILU 用"不完整消元"逼近 $LU$（放弃 fill-in 换稀疏），多重网格则用"粗网格问题"作廉价近似。注意这个"用更简单对象近似难对象、把残差校正掉"的模式，与你见过的**牛顿法用局部线性化近似非线性**、6.006 中"近似数据结构/多级方法"同构。还可以预埋伏笔：page_138 的统计"白化" $C^{-1/2}$ 是同一招在噪声协方差上的应用——**换个度量让难看的对象变好看**是贯穿数值与统计的通用策略。

```math
P^{-1}Ax = P^{-1}b \tag{9}
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 将 $A$ 认作 "蓋/凭/儿" 等字形，且公式被拆成 "尸 一 1 = p¯lb"，故公式 (9) 重建为 $P^{-1}Ax = P^{-1}b$；"一 P" 依语境补全为 $P - A$。

<span style="color:#2471a3;">**[note]**</span>
收敛性检验 convergence test（收敛性检验，无论采用何种算法）现在都作用于 $P^{-1}A$，而不是 $A$。
若所用算法为 conjugate gradient（共轭梯度法）——它针对 symmetric positive definite matrices（对称正定矩阵）——我们通常把 $A$ 换成 $P^{-1/2}AP^{-1/2}$。
以下是一些常见的 preconditioner（预条件子）$P$ 的选择：

1. $P$ 取对角矩阵（diagonal matrix），即拷贝 $A$ 的主对角线：这称为对角缩放（diagonal scaling），即 Jacobi 预条件子
2. $P$ 取三角矩阵（triangular matrix），即拷贝 $A$ 的对应三角部分：对应 Gauss-Seidel 方法（Gauss-Seidel method）
3. $P$ 取不完全 LU 分解（incomplete LU，ILU）：从 $A = LU$（消元）中省略 fill-in（填入元），以保持稀疏性（sparsity）
4. $P$ 取与 $A$ 相同的差分矩阵（difference matrix），但位于更粗的网格（grid）上：即多重网格方法（multigrid method）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 预条件子四项列表 OCR 噪声严重："co 历 方 e 0" 依 Jacobi 预条件语义重建，"tnangular" → triangular，"LoUo" → LU，"襯 况 ltig rid e 叻 0d" → multigrid method（多重网格方法）。

<span style="color:#2471a3;">**[note]**</span>
多重网格方法 multigrid method（多重网格方法）是一种强大且发展成熟的求解方法，它使用一整串网格 grids（网格）或网格族 meshes（网格）。
最细网格上的给定问题拥有最多网格点 meshpoints（网格点），对应矩阵很大。
依次在更粗网格上求解的问题网格点较少、矩阵较小，因而能被快速求解，所得结果再插值 interpolate（插值）回细网格。
这种方法效率极高，且收敛很快。

### Kaczmarz 迭代（Kaczmarz Iteration）

<span style="color:#2471a3;">**[note]**</span>
公式 (10) 执行起来很快，却不容易分析。
现在我们认识到：若每一步随机求解 $Ax=b$ 中的一个方程，收敛 convergence（收敛）将以高概率（high probability）指数级快速发生。
Kaczmarz 迭代的第 $k$ 步能使第 $i$ 个方程精确成立，即 $x_{k+1}$ 满足 $a_i \cdot x_{k+1} = b_i$：

```math
a_i \cdot x_{k+1} = b_i \tag{10}
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 公式 (10) 依上下文重建：OCR 的 "Ck+1 satisfies a · C" 中 $C$ 实为 $x_{k+1}$，行首 "一 Oi" 为 $b_i$，下标 $i$ 表示第 $i$ 个被选中的方程。

<span style="color:#2471a3;">**[note]**</span>
每一步都把上一步得到的点投影到平面（plane）$a_i \cdot x = b_i$ 上。
按顺序循环遍历 $m$ 个方程，就是经典 Kaczmarz 迭代（classical Kaczmarz）。
随机化算法（randomized algorithm）则以正比于 $\|a_i\|^2$ 的概率选择行（row）$a_i$——这正是 §11.4 的范数平方采样（norm-squared sampling）。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接）:**</span> Kaczmarz 迭代每步做一件事：把当前点正交投影到第 $i$ 个方程所代表的超平面 $a_i^Tx=b_i$ 上，从而**一步就让这个方程精确满足**。顺序循环遍历方程必收敛，但收敛率分析困难；随机版每步按 $\|a_i\|^2$ 加权概率选行，得到漂亮的期望界：若 $A$ 有 $r$ 个非零奇异值，则每步期望平方距离乘以固定因子 $(1-\sigma_r^2/\|A\|_F^2)$——即**期望指数收敛**，且因子只含"最坏方向与总能量的比"。为何权重取 $\|a_i\|^2$？可视为按超平面"法向量强度"抽样，使期望中的几何平均恰好落在谱量上——这正是 §II.4 将系统化的范数平方采样。它还是**随机梯度下降解线性方程**的实例：普通梯度下降要用全部 $m$ 行的梯度（成本 $O(m)$），随机版一次只取一行（成本 $O(1)$ 个内积），用随机性换每步廉价——Bertsekas 概率中的期望/方差语言是分析它的工具。与其纠结"随机怎么保证收敛"，不如记住：$k$ 步后以高概率落在离真解期望距离 $<(\text{因子})^k$ 的球内，这与 6.006 随机化算法的"高概率保证"一脉相承。

---

<span style="color:#2471a3;">**[note]**</span>
Kaczmarz 迭代（Kaczmarz iteration）是随机梯度下降（stochastic gradient descent）的一个重要例子——称其 "stochastic（随机）"，是因为第 $k$ 步所取的方程是随机选择。
我们将在 §VI.5（关于深度学习中权重优化的部分）再次回到这一算法。

> <span style="color:#7f8c8d;">**[reference]** 本页页脚文献（保留英文原文）：</span>
> T. Strohmer and R. Vershynin, "A randomized Kaczmarz algorithm with exponential convergence," *J. Fourier Anal. Appl.* 15 (2009) 262–278; arXiv:math/0702226.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 文献条目按 Strohmer–Vershynin (2009) 原文重建：OCR 把题目打散为 "A do 讵 ed Ka czma go w 打 九 e 0 刀 羽 / convergence"，"J. F0urier An al. Apple" 为 J. Fourier Anal. Appl.

---

> <span style="color:#7f8c8d;">Strang §II.1, p.122</span>

---

<!-- page 127: 书页 123, OCR page 27 -->

> <span style="color:#7f8c8d;">本页为 **Problem Set II.1（习题集 II.1）**，属于 §II.1 Numerical Linear Algebra（数值线性代数）的课后习题，书中页码 123。按交付规范：习题题干一律保留英文原文、不译为中文；页内中文仅用于结构引导与 OCR 修正注释。</span>

全页习题都以一个**双对角后向差分矩阵（bidiagonal backward difference matrix）** $D = I - S$ 为出发点。题首统一设定如下（英文原文，矩阵记号已按 §II.1 语境重建）：

> These problems start with a bidiagonal backward difference matrix $D = I - S$. The second difference matrices are $DD^T$ and $D^TD = -S + 2I - S^T$. The shift matrix $S$ has one nonzero subdiagonal $S_{i,i-1} = 1$ (for $i = 2, \ldots, n$). The matrix $-S + 2I - S^T$ has diagonals $-1, 2, -1$ except at the corner entries.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页 OCR 噪声极重：矩阵 $D, A, S$ 多处被识别为「刀 / 蓋 / 儿 / 風」等汉字，负号与减号被识别为「一」，上标（$T$、$^{-1}$）与下标大量丢失。以下各题题干均已按二阶差分矩阵与位移矩阵的数学语境重建，个别词按上下文补足。

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.**

> Show that $DD^T$ equals $-S + 2I - S^T$ except that a $1$ (not a $2$) is in its $(1,1)$ entry. Similarly $D^TD$ equals $-S + 2I - S^T$ except that a $1$ (not a $2$) is in its $(n,n)$ entry.

本题说明 $DD^T$ 与 $D^TD$ 仅在两个角落元处与 $A = -S + 2I - S^T$ 不同。紧随其后是书中一段 **Note**（英文原文），把它与二阶微分算子的边界条件（boundary conditions）联系起来：

> **Note.** The matrix $A = -S + 2I - S^T$ corresponds to $-d^2/dx^2$ for $0 \le x \le 1$ with fixed boundaries $y(0) = 0$ and $y(1) = 0$. $DD^T$ changes the first condition to $dy/dx = 0$ at $x = 0$; $D^TD$ changes the second condition to $dy/dx = 0$ at $x = 1$. Highly useful matrices.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 该段中 $d^2/dx^2$、$y(0)$、$y(1)$、$dy/dx$ 等记号残缺（如「№ ）= 0」实为 $y(0) = 0$），均已按固定边界（fixed boundary）与自由边界（free boundary）的数值语境重建。

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.**

> Show that the inverse of $D = I - S$ is $D^{-1}$, the lower triangular "matrix" of 1's. And $DD^{-1} = I$ is like the Fundamental Theorem of Calculus: integration cancels differentiation.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 将 $D^{-1}$ 误识为「D¯I」，末句乱码（如「五 沅 g 甩 I 可 歹」）无法逐字还原，此处按微积分基本定理（Fundamental Theorem of Calculus）的语意补全为「积分与微分互逆」。

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.**

> Multiply $(D^{-1})^T$ times $D^{-1}$ to find $(D^TD)^{-1}$ for $n = 4$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.**

> Problem 1 says that $A = DD^T + ee^T$ where $e = (1, 0, 0, \ldots)$. Section III.1 will show that $A^{-1} = ZZ^T$. For $n = 3$, can you discover the matrix $Z$? A rank-one change in $DD^T$ produces a rank-one change in its inverse.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 中 $e$ 的取值残缺；要使 $A = DD^T + ee^T$ 在 $(1,1)$ 元恢复为 $2$，$e$ 应为第一个单位向量。OCR 的「the vector $Z$」依 $A^{-1} = ZZ^T$ 的秩（rank）要求重建为矩阵；文末一句（Rank-one change，秩一扰动）提示可利用秩一修正与其逆的关系来发现 $Z$。

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.**

> Suppose you split $A = -S + 2I - S^T$ into $(-S + 2I)$ (lower triangular) and $(-S^T)$ (upper triangular). The Jacobi iteration to solve $Ax = b$ will be $(2I - S)x^{k+1} = S^T x^k + b$. This iteration converges provided all eigenvalues of $(2I - S)^{-1}S^T$ have $|\lambda| < 1$. Find those eigenvalues for sizes $n = 2$ and $n = 3$.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 把分裂式与收敛判据切碎（如把 $(2I - S)^{-1}$ 误识为「刀 一 1」），此处按分裂 $M = 2I - S$、$N = S^T$ 与收敛条件 $|\lambda| < 1$ 自洽重建；「Jacobi」一词依 OCR 保留（此下三角分裂按经典分类更接近 Gauss–Seidel 型，若与原书有出入以原书为准）。

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.**

> For $b = (1, 0, 0)$ and $n = 3$, the vectors $b, Ab, A^2b$ are a non-orthogonal basis for $\mathbb{R}^3$. Use the Arnoldi iteration with $q_1 = b/\|b\|$ to produce an orthonormal basis $q_1, q_2, q_3$. Find the matrix that gives $AQ_2 = Q_3H$, as in equation (3).

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 的「Arn01di」即 Arnoldi（阿诺尔迪）迭代，「with t0」后缺起始向量设定，按 Krylov 子空间（Krylov subspace）方法的标准取 $q_1 = b/\|b\|$；「Q2 = Q3 丑」重建为 $AQ_2 = Q_3H$，其中 $H$ 即式 (3) 中的海森伯格（Hessenberg）矩阵。

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.**

> In Problem 5, verify that $Q_3^TAQ_2$ is a tridiagonal matrix.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 题号「5」原样保留；就内容看本题验证的是上一题 Arnoldi 过程所得矩阵的三对角性（$A$ 对称时海森伯格矩阵化为对称三对角 tridiagonal 矩阵）。若按本页重建题号，上一题 Arnoldi 对应第 6 题，题号差异源于原书编排，以原书为准。

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.**

> Apply one step of the QR algorithm to the $3 \times 3$ second difference matrix $A$. The actual eigenvalues of $A$ are $\lambda = 2 - \sqrt{2}, 2, 2 + \sqrt{2}$. Try one step of the QR algorithm with the recommended shift $s = a_{33} = 2$.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 丢字严重：$2 + \sqrt{2}$ 只剩「2 +」，$s = a_{33} = 2$ 只剩「s = 33 = 2」，均已按 3×3 二阶差分矩阵的特征值（eigenvalues）与带位移（shift）的 QR 算法语境重建。

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.**

> Solve $Ax = (1, 0, 0)$ by hand. Then by computer using the conjugate gradient method.

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 的「S olve Ac」实为 Solve $Ax$；矩阵 $A$ 沿用前题的 3×3 二阶差分矩阵。本题要求先用共轭梯度法（conjugate gradient method）手算一遍，再用计算机求解。

---

## 译文正文 B（→ page_128.bilingual.md）

---

<!-- page 128: 书页 124, OCR page 28 -->

### <span style="color:#2471a3;">**[section]**</span> §11.2 Least Squares: Four Ways（最小二乘：四种方法）

> <span style="color:#7f8c8d;">本节为正文页（含定义与表格性举例），书中页码 124，属于 §11.2 Least Squares（最小二乘）。</span>

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本节 OCR 把矩阵 $A$、$A^T$ 大量识别为「蓋」「刀」「風」等汉字（如 $A^T b$ 变成「ÄTb」），所有此类记号均已按最小二乘方程组 $A^TAx = A^Tb$ 的统一语境重建；术语表规定 $E = U\Sigma V^T$ 类噪声一律读作 $A = U\Sigma V^T$。

许多应用都会引出不可解的线性方程组 $Ax = b$（unsolvable linear equations）。讽刺的是，这恰恰是线性代数中如此重要的一个问题——我们既不能把方程扔掉，又需要某个**解（solution）**。最小二乘方法（least squares method）通过选取 $x$ 使 $\|b - Ax\|_2$ 尽可能小（as small as possible）来求解。令该误差（error）取极小意味着其导数（derivatives）为零：那正是**正规方程（normal equations）** $A^TAx = A^Tb$。它们背后的几何（geometry）将见于图 11.2（Figure 11.2）。

本节将阐释求解这些重要（而且可解！）方程组的四种方法（four ways）：

1. 对 $A$ 作奇异值分解（SVD of $A$）可得其伪逆（pseudoinverse）$A^+$；于是 $x = A^+b$——一条简洁的公式（one short formula）。
2. 当 $A$ 具有独立列（independent columns）时，$A^TAx = A^Tb$ 可直接求解。
3. 格拉姆-施密特（Gram-Schmidt）思想把 $A$ 的列正交化为正交矩阵（orthogonal matrix）$Q$ 中的正交列，于是 $A = QR$。
4. 极小化 $\|b - Ax\|_2^2 + \|x\|_2^2$（即加上惩罚项 $\lambda\|x\|^2$，weights）。该惩罚项（penalty）把正规方程改为 $(A^TA + \lambda I)x = A^Tb$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 第 4 种方法中 OCR 的「日 2 + 日」与「硭」按岭回归（ridge regression）的语境重建为 $\|b - Ax\|_2^2 + \lambda\|x\|_2^2$ 与 $(A^TA + \lambda I)$；原文末句「goes to $A^TA$ as $\lambda \to 0$」依「goes t0」与极限记号重建。

现在 $A^TA + \lambda I$ 这个矩阵可逆（invertible），且当 $\lambda \to 0$ 时趋向 $A^TA$。矩阵 $A^TA$ 有着诱人的对称性（symmetry），但它的尺寸（size）可能是个问题；而且它的条件数（condition number）——用来度量不可接受的舍入误差（roundoff error）的危险程度——是 $A$ 的条件数的平方（square of the condition number of $A$）。在中等规模的适定问题（well-posed problems）中，我们径直去解正规方程 $A^TAx = A^Tb$；但在大型或不适定问题（ill-posed problems）中，我们要另寻他途（another way）。

> <span style="color:#1e8449;">**[note] Note（译者注：条件数平方的现场——不但放大误差，还删掉一个维度）:**</span> 原注的两句判断（$A^TAx=A^Tb$ 与 $Rx=Q^Tb$ 数学同解、数值两个世界）可以先算一遍再信。取 $8\times 8$ 的 Hilbert 矩阵，$\mathrm{cond}(A)=1.53\times 10^{10}$，按 $\sigma_i(A^TA)=\sigma_i(A)^2$ 预测 $\mathrm{cond}(A^TA)=2.33\times 10^{20}$；而双精度能分辨的上限只有 $1/\varepsilon=4.50\times 10^{15}$（$\varepsilon=2.22\times 10^{-16}$ 就是 CSAPP 第 2 章讲的那个机器精度） —— 这个矩阵在 float64 里已经不是可逆意义下的对象了。解同一个 $b=A\mathbf{1}$：正规方程的前向误差 $9.54$（解完全错掉），QR 是 $4.04\times 10^{-7}$，`pinv` 是 $9.54\times 10^{-7}$。同一个方程组，七个数量级的差距，全部来自「先乘出 $A^TA$」这一步。
> 
> 有效数字可以直接数出来，不必只记住 $\varepsilon\cdot\kappa$ 这个符号。双精度有 $16$ 位十进制有效数字，而前向误差的量级是 $\varepsilon\cdot\kappa$，于是解能留住的位数约是 $16-\log_{10}\kappa$。对这个 Hilbert 矩阵：走 QR 时 $\kappa=1.53\times10^{10}$，给 $16-10.18=5.8$ 位，实测误差 $4.04\times10^{-7}$ 折合 $6.4$ 位，同量级吻合；走正规方程时 $\kappa^2=2.33\times10^{20}$，给 $16-20.37=-4.4$ 位 —— 负数的意思是「连一位都没有」，实测误差 $9.54$ 正好对应这个结论。这条换算是判断「该不该冒险用正规方程」的最快尺子：先估 $\kappa$，把它的对数与 16 一比，答案就出来了。
> 
> 更狠的是它不只放大误差，还**删掉一个维度**。取 $A=\mathrm{diag}(1,10^{-8})$：$\mathrm{cond}(A)=10^8$，$\mathrm{rank}(A)=2$，而 $\mathrm{rank}(A^TA)=1$ —— 因为 $A^TA=\mathrm{diag}(1,10^{-16})$，最小特征值 $10^{-16}$ 已经低于 $\varepsilon=2.22\times 10^{-16}$，任何按 $\varepsilon\cdot\sigma_{\max}\cdot n$ 定容差的秩判定都会把它读成零。所以「平方条件数」的准确说法是：平方把 $\sigma_{\min}$ 直接压到舍入地板以下，于是**可分辨的维度少了一个**。这也解释了正文为什么说 $A^TA$ 的「尺寸可能是个问题」之外还有更致命的东西 —— 尺寸只是存储，掉秩是信息。
> 
> 代价账则说明为什么四种方法不能只留最稳的那个。$m=n=1000$ 时按乘法计数：形成 $A^TA$ 要 $\tfrac12 n^3=5.0\times 10^8$，Cholesky 要 $\tfrac16 n^3=1.67\times 10^8$，合计 $6.67\times 10^8$；Householder QR 解同一个系统要 $\tfrac23 n^3=1.33\times 10^9$（自行推导的逐项计数）。QR 只贵一倍，却把误差放大从 $\kappa^2$ 换回 $\kappa$ —— 这是全书性价比最高的一笔交易，也是「四种方法」排序的定量根据：SVD 最稳最贵（还要迭代），QR 居中且几乎总是值得，正规方程只在 $\kappa$ 小的时候可以省那一倍，带惩罚项的 $(A^{T}A+\lambda I)$ 则是专为病态而生的第四条路 —— 用一点偏差换掉整段放大。这句排序也是实操的说明书：若你之后用 MATLAB 的 $A\backslash b$ 或 `pinv(A)*b`，内部权衡的就是这四条。存储账也要算：$n=1000$ 时 $A^TA$ 占 8 MB，$n=10^5$ 时就是 80 GB，而 QR 可以原地覆盖 $A$ 的存储区、把上三角留在原处，不需要再开一块 $n^2$ 的矩阵 —— 这才是正文说 $A^TA$ 的「尺寸可能是个问题」的实在含义。
> 
> 原注的第二个判断还能再深一层。「$A^TA$ 在四个学科里换名字」不只是名称巧合，背后是同一个**离散算子**：把 $A$ 读成离散梯度，即每条边一行、两个端点取 $\pm1$ 的 incidence（关联矩阵），$C$ 取材料系数或电导或逆方差的对角阵，那么 $A^TCA$ 正是 $-\nabla\cdot(c\nabla\cdot)$ 的离散版本 —— 有限元里它是刚度矩阵，电路里它是电导矩阵，图上它是加权 Laplacian $D-W$，统计里它是加权最小二乘的 Hessian（Fisher information）。机械势能、电路功率、随机游走的平滑度、统计的误差能量，在这套写法里都是同一个二次型 $\tfrac12x^{T}A^{T}CAx-b^{T}Ax$ 换了单位。四个学科写的是同一行矩阵乘法，而数值上的病态也同源：细网格、大电导比、强相关列，都让 $\sigma_{\min}$ 变小。这就是为什么这一节的算法进展会立刻迁移到所有用 $A^TA$ 写方程的领域，也是为什么 Strang 一边说这些矩阵太重要、一边说不要显式算它们。

我们可以正交化 $A$ 的列，也可以使用它的 SVD。对于真正的大规模问题，我们则通过把 $A$ 乘上随机向量（random vectors）来**采样（sample）** $A$ 的列空间（column space of $A$）。这似乎正成为超大规模计算（very big computations）的潮流：成功概率很高（a high probability of success）。

首先，请允许我们强调 $A^TA$ 与 $A^TCA$ 的重要性。矩阵 $C$ 常为**正对角矩阵（positive diagonal matrix）**：它给出刚度（stiffnesses）或电导（conductances）或边的容量（edge capacities）或逆方差（inverse variances）$1/\sigma^2$——这些来自科学、工程或统计学、定义了我们的具体问题的常数，即加权最小二乘（weighted least squares）中的「权重（weights）」。下面是 $A^TA$ 与 $A^TCA$ 在应用数学中现身的一批样例：


---

- 在机械工程（mechanical engineering）中，$A^TA$（或 $A^TCA$）是刚度矩阵（stiffness matrix）；
- 在电路理论（circuit theory）中，$A^TA$（或 $A^TCA$）是电导矩阵（conductance matrix）；
- 在图论（graph theory）中，$A^TA$（或 $A^TCA$）是（加权的）图拉普拉斯算子（weighted graph Laplacian）；
- 在数学中，$A^TA$ 就是格兰姆矩阵（Gram matrix）：$A$ 的各列之间的内积（inner products of columns of $A$）。

在大规模问题中，计算 $A^TA$ 代价高昂（expensive）且常常很危险（dangerous），能避开我们就避开它！格拉姆-施密特（Gram-Schmidt）途径用 $A = QR$（正交的 $Q$、三角的 $R$，triangular $R$）取而代之。于是 $A^TA$ 化为 $R^TQ^TQR = R^TR$；而基本方程 $A^TAx = A^Tb$ 化为 $R^TRx = R^TQ^Tb$，最终归结为 $Rx = Q^Tb$——求解既安全又快速。

可见 $A^TA$ 与 $A^TCA$ 是至关重要的矩阵——但矛盾的是，我们恰恰尽量不去计算它们。正交矩阵与三角矩阵（triangular matrices）才是「好」矩阵。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.124</span>

---

<!-- page 129: 书页 125, OCR page 29 -->

<span style="color:#2471a3;">**[section]**</span> **§II.2 Least Squares: Four Ways（最小二乘：四种方法）**——本页正文（书页 125）说明 $A^+$ 正是 $A$ 的伪逆（pseudoinverse）：先以文字描述其作用，再给出计算伪逆的三条规则（Rules），最后落到 SVD 形式 $A^+ = V\Sigma^+U^T$ 与 Figure II.1 的四子空间（four subspaces）图示。

伪逆 $A^+$ 是 $A$ 的伪逆（pseudoinverse of $A$）。首先用文字描述 $A^+$ 的作用：若 $A$ 可逆（invertible），则 $A^+$ 就是 $A^{-1}$。

若 $A$ 是 $m \times n$ 矩阵，则 $A^+$ 是 $n \times m$ 矩阵。当 $A$ 乘以它行空间（row space）中的某个向量 $x$ 时，结果 $Ax$ 落在列空间（column space）中。

这两个空间的维数（dimension）相等，都等于秩 $r$（rank）。$A$ 限制（restricted）在这两个空间上总是可逆的——而 $A^+$ 恰好把这一限制反演回来。

于是 $A^+Ax = x$ 恰在 $x$ 位于行空间时成立；$AA^+b = b$ 恰在 $b$ 位于列空间时成立。

$A^+$ 的零空间（nullspace）就是 $A^T$ 的零空间：它包含 $\mathbb{R}^m$ 中所有满足 $A^Ty = 0$ 的向量 $y$。

这些向量 $y$ 与列空间中的每一个 $Ax$ 都垂直。对这种不可行的右端 $b$，我们把 $x^+ = A^+b = 0$ 接受为不可解方程 $Ax = b$ 的最佳解。

> <span style="color:#1e8449;">**[note] Note（译者注：伪逆在精确算术里杀掉 N(A^T)，在浮点里只杀得动 ε·κ 那么深）:**</span> 原注的四子空间读法可以再加一行维数账：$r+(n-r)=n$ 且 $r+(m-r)=m$，行空间与零空间把 $\mathbb{R}^n$ 分完、列空间与 $N(A^T)$ 把 $\mathbb{R}^m$ 分完；$A$ 只在前一个空间上是一一映射，$A^+$ 只反演这一段，其余一律写零。右端一旦按 $\mathbb{R}^{m}=C(A)\oplus N(A^{T})$ 拆成 $b=p+e$，$A^{+}$ 就只处理 $p$、把 $e$ 整块丢掉 —— 这就是「不可解的方程只解其中可解的部分」的全部内容。真值检验也很便宜：取 $A$ 的三行为 $(1,0)$、$(0,10^{-3})$、$(0,0)$（此时 $U$、$V$ 就是坐标基），$A^+e_3=(0,0)$ **精确**成立，而 $A^+e_2=(0,1000)$ —— 一个落在 $N(A^T)$ 里被清零，一个落在最小的非零奇异方向上被放大 $1/\sigma_2=10^3$ 倍。
> 
> 但「精确杀掉」这句话只在条件数不太坏时才是数值事实。把同一份结构换到随机正交基里（$3\times 2$、秩 $2$、$\sigma=1$ 与 $10^{-8}$），再让 $A^+$ 作用在 $N(A^T)$ 的那个单位向量上：精确算术该给零，实测得到范数 $1.043$ 的东西。原因不是公式错了，而是基错了：float64 里 $N(A^T)$ 的方向与最小的左奇异向量在数值上只能分辨到 $\varepsilon\cdot\sigma_{\max}/\sigma_{\min}=2.2\times10^{-16}\times 10^{8}\approx2.2\times10^{-8}$，乘上 $1/\sigma_{\min}=10^{8}$ 的放大，泄漏就长成了 $O(1)$。所以伪逆的条件数与 $A$ 的条件数一样烂（实测 $\|A^+\|\|A\|=1.0\times10^{8}$），它不会因为「是个投影」就变安全；真正无损的是正交变换本身，这也是为什么 SVD 形式 $A^+=V\Sigma^+U^T$ 总被写成「旋转—逐坐标—旋转回」而不是「一个投影算子」。
> 
> 跨课程看，这条 $1/\sigma$ 放大正是回归里的方差公式。若 $b=Ax+\eta$、$\eta$ 各分量独立且方差 $\sigma^2$，则 $\hat{x}=A^+b$ 的协方差是 $\sigma^2(A^TA)^{-1}=\sigma^2V\Sigma^{-2}V^T$ —— 第 $i$ 个奇异方向上解的标准差被放大 $1/\sigma_i$，方差放大 $1/\sigma_i^2$。取上一段的矩阵、$\sigma=10^{-3}$ 作观测噪声、跑 $2\times10^5$ 次蒙特卡洛：实测算出的方差是 $(9.9614\times10^{-7},\,1.0024)$，理论值 $\sigma^2\,\mathrm{diag}((A^TA)^{-1})=(10^{-6},\,1)$，对得上。所以「小奇异值方向上的答案不可信」不是数值匠气，它是数据在该方向上精度不足的直接换算：$\hat{x}$ 的不确定度就是 $1/\sigma_i$ 乘观测噪声。
> 
> 顺便把两个复合矩阵的「痕迹」写清楚，它们不是单位阵这件事本身有含量。$AA^+$ 是 $m\times m$ 里秩 $r$ 的正交投影，$A^+A$ 是 $n\times n$ 里秩 $r$ 的正交投影（前作里那个投影矩阵 $P$ 就是左式的写法），两个的迹都恰好等于 $r$ —— 投影的迹等于它所投影到的子空间维数，这是可验的等式。上一段那个 $3\times 2$ 的例子实测：$AA^+$ 是 $3\times3$、对角元 $0.2571$、$0.8390$、$0.9039$，和恰好 $2.000$；$A^+A$ 是 $2\times2$ 且与单位阵差在 $10^{-9}$ 量级。所以「只在行空间与列空间上互逆」这句话的定量版本是：两个复合各留 $r$ 维、各扔 $m-r$ 与 $n-r$ 维，扔掉的正是 $N(A^T)$ 与 $N(A)$。
> 
> 还有一处实操陷阱值得记住：`numpy.linalg.pinv` 默认 `rcond=1e-15`，凡 $\sigma_i/\sigma_{\max}$ 小于它的方向一律按零处理 —— 也就是说「哪一维算零」在库里是**一个参数**在替你决定，不是数学定义决定的。把 `rcond` 调大就变成显式截断（更稳、更偏），调小就把 $\varepsilon$ 地板上的噪声也倒除进来（更准、更抖）。这与前文对非正规矩阵的告诫是同一件事：在 $\sigma$ 很小的方向上，答案对「你以为的秩」极其敏感，而规则不该由浮点数悄悄代填。
> 
> 把三件事收成一句模板：「限制—求逆—延拓为零」给出最小范数解，代价是 $1/\sigma$ 滤波；滤波在 $\sigma_i<\varepsilon\sigma_{\max}$ 的方向上不可靠，于是必须显式截断（伪秩），而不是让浮点替你决定哪一维该留。后面 page_130 的最小范数解与 page_136 的岭回归极限，都是在这条 $1/\sigma$ 曲线上换一个滤波器形状：前者在零处硬截断，后者把 $1/\sigma$ 换成 $\sigma/(\sigma^2+\delta^2)$，用一点点偏差换掉整段放大。

---

总而言之，$A^+A$ 在一切可能之处反演 $A$。全部要点在于：当 $A$ 没有逆矩阵时，仍然要产出一个合适的“伪逆”。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 上述段落 OCR 噪声密集：`蓋`/`风`/`兒`→$A$，`十`→$A^+$，`T = 0`→$A^Ty = 0$，`Restncted`→Restricted，`0f`→of，`th e`→the 等，均已按伪逆的数学语境重建。

<span style="color:#2471a3;">**[definition]**</span> **计算伪逆的三条规则**：

**规则 1（Rule 1）** 若 $A$ 有独立列（independent columns），则 $A^+ = (A^TA)^{-1}A^T$，从而 $A^+A = I$。

> <span style="color:#1e8449;">**[note] Note（译者注：伪逆三条规则与 Moore-Penrose 条件）:**</span> 规则 1 与规则 2 对你并不陌生：前作《线性代数导论》§4.2–4.3 的 least squares solution（最小二乘解）$\hat x=(A^TA)^{-1}A^Tb$ 与 projection matrix（投影矩阵）$P=A(A^TA)^{-1}A^T$ 就是规则 1 的现身；规则 2 只是把问题"转置"看待，即 $AA^T$ 可逆当且仅当 $A$ 行独立，于是把 $A^T$ 当作矩阵套用规则 1，便得到 $A^+=A^T(AA^T)^{-1}$。pseudoinverse（伪逆）的贡献在于用 SVD（奇异值分解）把两种情形统一成第三条规则：先换到 singular vector（奇异向量）坐标系，即乘 $V^T$，再在每个坐标上独立地对 $\sigma_i$ 取倒数——diagonal matrix（对角矩阵）的各坐标完全解耦，规则 3 正是 $A^+=V\Sigma^+U^T$ 的逐坐标版本：非零 $\sigma_i$ 求倒数，零 $\sigma_i$（信息已丢失的方向）写 0。于是最小二乘解 $x^+=A^+b$ 可三步读：把 $b$ 旋转进 $U$ 坐标系，逐坐标除以 singular value（奇异值）或置零，再旋转回 $V$ 坐标系。这个"旋转—逐坐标处理—旋转回"的三明治，在后面 page_130、page_136 的证明里会反复出现，值得现在刻进脑子。
> 
> 手工验一遍最省事。取 $A_1$ 的三行依次为 $(1,2)$、$(3,4)$、$(5,7)$，它列满秩，按规则 1 算出的 $A_1^+$ 与 `numpy.linalg.pinv` 的最大差为 $5.9\times10^{-14}$，只是 float64 的舍入地板；把 $A_2=A_1^T$ 按规则 2 算，最大差 $6.3\times10^{-14}$，且 $A_2A_2^+$ 与 $I_2$ 之差在同一量级。真正的分水岭是 rank-deficient（秩亏）的情形：取 $A_3$ 的三行依次为 $(1,2,3)$、$(2,4,6)$、$(0,1,1)$，第二行恰是第一行的两倍，rank 只有 2，三个 singular value（奇异值）为 $8.473$、$0.457$、$0$。规则 1 与规则 2 在这里同时失效，因为 $A_3^TA_3$ 与 $A_3A_3^T$ 都不可逆；而 $A_3^+=V\Sigma^+U^T$ 照样给出答案，四条 Penrose conditions（彭罗斯条件）的最大残差分别是 $1.8\times10^{-15}$（对应 $AA^+A=A$）、$4.4\times10^{-16}$（对应 $A^+AA^+=A^+$）、$4.6\times10^{-15}$（对应 $(AA^+)^T=AA^+$）、$1.9\times10^{-15}$（对应 $(A^+A)^T=A^+A$）。
> 
> 为什么逐坐标取倒数就是最优？把目标展开成 $\|\Sigma c-U^Tb\|^2=\sum_i(\sigma_ic_i-d_i)^2$ 后，求和号里每一项只含一个变量，于是各坐标的问题互相独立：$\sigma_i\ne0$ 时取 $c_i=d_i/\sigma_i$ 使该项归零；$\sigma_i=0$ 时该项与 $c_i$ 完全无关，任何取值都不改变残差，只有取 0 才让范数最小。实算 $A_3$ 与 $b=(1,2,3)$：$d=U^Tb$ 的三个分量为 $-2.682$、$-2.609$、$0$，按上式得 $c=(-0.3166,-5.7067,0)$，残差平方 $1.9\times10^{-28}$，已是舍入噪声；把第三个坐标改成 $1$，残差平方仍是 $1.2\times10^{-28}$，而范数平方从 $32.667$ 涨到 $33.667$。这就是规则 3 在零处写零的根据：它不是审美选择，而是最小范数要求的直接后果。
> 
> 三条规则的差别只在"哪些方向可逆"：规则 1 保证 $A^+A=I_n$，规则 2 保证 $AA^+=I_m$，规则 3 两个都保证不了，只能逐坐标取倒数。实测 $A_3^+A_3$ 与 $A_3A_3^+$ 都是 rank 2 的 matrix（矩阵），分别是到 row space（行空间）与 column space（列空间）的 orthogonal projection（正交投影），而不是单位阵——所谓"逆"只存在于秩 $r$ 维那块子空间上。这也解释了正文为什么断言 $A^+$ 的 nullspace（零空间）等于 $N(A^T)$：$N(A^T)$ 与列空间正交，被 $A^+$ 一律送到 0。史实坐标值得记住：Moore 在 1920 年以三条条件定义了这个广义逆，出处是 Bull. Amer. Math. Soc. 26, 394–395, DOI 10.1090/S0002-9904-1920-03322-7；Penrose 在 1955 年独立地改写成上面那四条对称条件并证明其唯一，出处是 Proc. Cambridge Philos. Soc. 51(3), 406–413, DOI 10.1017/S0305004100030401，所以今天叫 Moore–Penrose pseudoinverse（摩尔–彭罗斯伪逆）。Strang 18.06 的四个子空间图正是这张代数刻画的几何版：$A^+A$ 画出 row space（行空间），$AA^+$ 画出 column space（列空间），两者维数都等于 rank（秩）。顺带一个量纲检查：$A^+$ 是 $n\times m$ 的 matrix（矩阵），$A^+b$ 是 $n\times1$ 的向量，与 $x$ 同型，所以“伪逆乘右端”不必转置就能直接产出解；这正是它比 $P$ 更适合做求解算子的原因——$P$ 在 $\mathbb R^m$ 内部动作，$A^+$ 则跨界把 $\mathbb R^m$ 送回 $\mathbb R^n$，而这一步跨界的合法性来自正交分解 $\mathbb R^m=C(A)\oplus N(A^T)$ 与 $\mathbb R^n=C(A^T)\oplus N(A)$ 同时成立。

**规则 2（Rule 2）** 若 $A$ 有独立行（independent rows），则 $A^+ = A^T(AA^T)^{-1}$，从而 $AA^+ = I$。

**规则 3（Rule 3）** 对角矩阵（diagonal matrix）在可行之处取倒数——其余位置在 $A^+$ 中写零。

<span style="color:#2471a3;">**[example]**</span> 规则 3 的标准形式：设对角矩阵 $\Sigma = \mathrm{diag}(\sigma_1, \sigma_2, 0, 0)$，则其伪逆仅在非零元素处取倒数

```math
\Sigma = \begin{bmatrix} \sigma_1 & 0 & 0 & 0 \\ 0 & \sigma_2 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix}
\qquad\Longrightarrow\qquad
\Sigma^{+} = \begin{bmatrix} 1/\sigma_1 & 0 & 0 & 0 \\ 0 & 1/\sigma_2 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原排版此处的示例矩阵仅残存 `1/2 0`、`1/伊 1`、`伊 1 0 0 0`、`伊 2 0 0`、`1/伊 2` 等碎片（`伊`→$\sigma$，另见“The pseudoinverse of A =”残句），具体数值无法逐元复原，已按 Rule 3 的数学含义以上述通用形式重建。

<span style="color:#2471a3;">**[theorem]**</span> <span style="color:#c0392b;">一切矩阵的伪逆</span>（all matrices）：对任意 $A = U\Sigma V^T$（奇异值分解 SVD），$A$ 的伪逆为 $A^+ = V\Sigma^+U^T$。

<span style="color:#2471a3;">**[note]**</span> **Figure II.1（图 II.1）——在四子空间上（on the four subspaces）**：$A$ 把行空间映到列空间（row space to column space）。

> 对 $A^+$ 而言四个子空间的角色反转（reverse the 4 subspaces for $A^+$）：$A^+$ 把列空间映回行空间（column space to row space），并把 $A^T$ 的零空间与 $A$ 的零空间（nullspace of $A^T$、nullspace of $A$）中的向量都映到 $0$，图中以 $A^+p = x^+$、$A^+b = x^+$、$A^+e = 0$ 一类关系标示。

图注（figure caption）：列空间中的向量 $p = Ax^+$ 经 $A^+$ 映回行空间中的 $x^+ = A^+b$，二者一一对应。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.125</span>

---

<!-- page 130: 书页 126, OCR page 30 -->

<span style="color:#2471a3;">**[section]**</span> **§II.2 续：Computations with Large Matrices（大矩阵的计算）**——本页正文（书页 126）验证伪逆 $A^+$ 能一步给出最小二乘解，阐明最小范数解（minimum norm solution）与零空间的关系，并转向对正规方程（normal equations）$A^TAx = A^Tb$ 的直接解法。

这一伪逆 $A^+$（书写时用短剑号 dagger $\dagger$ 而非加号 plus sign）可以一步解出最小二乘方程（least squares equation）$A^TAx = A^Tb$。

本页将验证 $x^+ = A^+b = V\Sigma^+U^Tb$ 是最佳可能（best possible）的解。到本节末尾，我们再更细致地考察 $A^+$ 本身。

<span style="color:#2471a3;">**[note]**</span> **问题（Question）**：公式 $A^+ = V\Sigma^+U^T$ 用到了 SVD。那么求 $A^+$ 是否必须以 SVD 为前提？

<span style="color:#2471a3;">**[note]**</span> **回答（Answer）**：不必。$A^+$ 也可以由 $A$ 直接计算——只需修改通常用来产生 $A^{-1}$ 的消元（elimination）步骤即可。

但那样每一步算术都必须精确：你须能区分真正的零（exact zeros）与极小的非零（small nonzeros）。这正是求 $A^+$ 的难点（hard part）所在。

<span style="color:#2471a3;">**[theorem]**</span> <span style="color:#c0392b;">方程 $Ax = b$ 的最小二乘解为 $x^+ = A^+b$。</span>这里写 $x^+$ 而不写 $\hat{x}$，是因为向量 $x^+$ 具有下列两条性质：

**性质 1（Property 1）** $x^+ = A^+b$ 使 $\|Ax - b\|^2$ 尽可能小（最小二乘解，least squares solution）。

> <span style="color:#1e8449;">**[note] Note（译者注：正交分解加勾股，两步证出最小范数解）:**</span> 这里示范一个可反复套用的证明骨架——**正交分解 + 勾股**。第一步（性质 1）：把 $b$ 分解成 $p\in C(A)$ 与 $e\perp C(A)$，那么对任意 $x$，$Ax$ 只在 $C(A)$ 里"移动"，由勾股定理 $\|b-Ax\|^2=\|e\|^2+\|p-Ax\|^2$，最小值当且仅当 $Ax=p$ 时取到——于是"极小残差"被翻译成"$Ax$ 必须等于 $b$ 的 column space（列空间）投影"，这正是 page_131 将证的 normal equations（正规方程）$A^T(b-Ax)=0$ 的几何版。第二步（性质 2）：所有极小解构成 affine subspace（仿射子空间）$\{x^++z:z\in N(A)\}$，零空间方向可以任意加而不改变 $Ax$。而 $x^+$ 恰落在 row space（行空间）——前作 §4.1 的正交补事实 $\mathbb R^n=C(A^T)\oplus N(A)$ 保证它垂直于所有 $z$，勾股再给 $\|x^++z\|^2=\|x^+\|^2+\|z\|^2$，最短者必取 $z=0$。注意本例对角矩阵让几何退化到坐标轴，正好拿来手工验证两条性质：$z=(0,0,t)$ 任意加不改变误差 $64$，但最短的就是第三分量取 0 的那个。**"极小点集 = 特解 + 零空间；最短元 = 与零空间正交的分量"** 这个模板，在约束优化、伪逆、以及日后学习凸优化对偶时都会反复遇到。
> 
> 把正文那个例子彻底算穿：$A$ 是对角元 $3,4,0$ 的 diagonal matrix（对角矩阵），$b=(6,8,8)$，$x^+=(2,2,0)$，残差平方 $\|Ax^+-b\|^2=64$，全部来自第三坐标的 $8^2$。取 $z=(0,0,t)$，$t=5$ 时残差平方仍是 64，而范数平方从 8 涨到 33；$t=-7$ 时涨到 57，与勾股等式 $8+t^2$ 逐位吻合。再换一个真正秩亏的例子看"唯一性"从哪来：$A$ 取三行全为 $(1,1)$，则 rank（秩）为 1，$b=(1,2,4)$，最小二乘条件退化成一条标量方程，解集是一条直线；实算 $x^+=(1.1667,1.1667)$，范数平方 $2.722$，残差平方 $4.667$，而 $(0.5,0.5)$、$(1,0)$、$(0,1)$、$(2,-1)$ 的残差平方全是 $10.0$，范数平方依次为 $0.5$、$1.0$、$1.0$、$5.0$——它们的残差比 $x^+$ 大，所以根本不在极小解集里；这一组数字同时示范了"残差最小"与"范数最小"是两个先后生效的筛子。
> 
> 机制层面只需一句话：任何 $x$ 都能唯一分解成 $x_r+x_n$，$x_r\in C(A^T)$、$x_n\in N(A)$，且 $Ax=Ax_r$，所以 $x_n$ 对残差毫无贡献，只会把范数抬高 $\|x_n\|^2$。于是"先最小化残差、再最小化范数"这个两阶段问题，等价于"在 row space（行空间）里找那个唯一的极小残差点"。这条先投影再求逆的次序在统计里叫 minimum norm least squares（最小范数最小二乘），在 Boyd 的凸优化讲义里就是"约束集是仿射子空间时，极小范数点等于到该子空间的正交投影"。这句结论的标准出处有两处可查：Strang 的 *LaLFD* §II.2 讲最小二乘与正交投影，Golub & Van Loan 的 *Matrix Computations* §5.5 的 Thm 5.5.1 由 Penrose 条件给出 pseudoinverse（伪逆）并由此得到 minimum-norm（最小范数）解；这两处编号我都未能一手核实，手边没有原书，§II.2 与 Thm 5.5.1 是按通行引用写下的，读者以书内小节标题为准。还要注意性质 2 是严格不等式：只有 $\hat x\ne x^+$ 时才有 $\|x^+\|<\|\hat x\|$，因为两者之差必是 nullspace（零空间）中的非零向量。这一条把"解不唯一"这件坏事变成了"解集有唯一代表"这件好事，也是伪逆能被称为最佳解的根据。
> 
> 顺带记住两个连接。其一，投影与最短解是同一个矩阵的两面：$Ax^+=Pb$，而 $x^+=A^+b$，所以伪逆是把 $P$ 的"投影"再沿 $A$ 回溯到定义域的算子。其二，欠定问题的最小范数解是 ridge regression（岭回归）当惩罚系数趋零时的极限：仍用三行全为 $(1,1)$ 的 $A$ 与 $b=(1,2,4)$，解 $(A^TA+\lambda I)^{-1}A^Tb$，$\lambda=10^{-2}$ 时与 $x^+$ 的距离 $2.7\times10^{-3}$，$\lambda=10^{-6}$ 时缩到 $2.7\times10^{-7}$，但继续降到 $10^{-12}$ 反而弹回 $2.1\times10^{-4}$——因为 $A^TA$ 本身奇异，惩罚太小就退化成病态的 normal equations（正规方程），float64 的舍入开始主导。这条"惩罚系数有最优区间"的经验，在机器学习的 regularization（正则化）里天天用到。补充一句跨课程坐标：6.042J 的等价关系与双包含证明风格在这里同样成立，因为性质 1 与性质 2 各自是一次"对所有 $x$ 的量化命题"，而证明靠的是把量化语句翻译成可计算的不等式。

**性质 2（Property 2）** 若另有向量 $\hat{x}$ 也达到这个最小值，则 $\|x^+\| < \|\hat{x}\|$（除非 $\hat{x} = x^+$），即 $x^+$ 是最小范数解（minimum norm solution）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 原行 `日 + 日 < 日 |` 的范数记号与候选向量名残缺，按“$x^+$ 是所有达到最小二乘误差的解中最短者”的语义重建为 $\|x^+\| < \|\hat{x}\|$。

因此 $x^+ = A^+b$ 就是最小范数最小二乘解。当 $A$ 有独立列且秩 $r = n$ 时，它还是唯一的最小二乘解。

但若 $A$ 的零空间中有非零向量（即 $r < n$），这些向量可以加到 $x^+$ 上：取 $\hat{x} = x^+ + z$，其中 $Az = 0$。

由于 $Az = 0$，误差 $b - A\hat{x}$ 不受影响；但长度会增大为 $\|x^+ + z\|^2 = \|x^+\|^2 + \|z\|^2$，因为这两部分正交：行空间 $\perp$ 零空间（Row space ⊥ nullspace）。

所以正规方程 $A^TAx = A^Tb$ 的最小范数（最短）解满足：$x^+$ 在 $A$ 的零空间中的分量为零。

<span style="color:#2471a3;">**[example]**</span> **例 1（Example 1）**：求 $Ax = b$ 的最短最小二乘解，其中

```math
A = \begin{bmatrix} 3 & 0 & 0 \\ 0 & 4 & 0 \\ 0 & 0 & 0 \end{bmatrix}, \qquad b = \begin{bmatrix} 6 \\ 8 \\ 8 \end{bmatrix}
```

伪逆 $A^+ = \mathrm{diag}(1/3,\,1/4,\,0)$ 给出最短解

```math
x^{+} = A^{+}b = \begin{bmatrix} 2 \\ 2 \\ 0 \end{bmatrix}.
```

所有向量 $z = (0,0,t)$ 都位于 $A$ 的零空间（$Az = 0$），于是每个 $\hat{x} = x^+ + z$ 都使 $\|Ax - b\|^2 = 64$ 达到最小；但这些解之中 $x^+$ 最短。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 本例数值在 OCR 中仅为碎片（残存 `1/3 0`、`6`、`8`、`2`、`2`、`0`、`minimize ... 2 = 64`），已按“伪逆 $A^+$ 乘 $b$ 得最短解”的语境自洽重建：$A = \mathrm{diag}(3,4,0)$，$b = (6,8,8)$，$x^+ = (2,2,0)$，平方误差恰为 $8^2 = 64$。

这个例子展示了当 $A$ 是像上面那样的对角矩阵（diagonal matrix）时最小二乘解的情形。

为涵盖一般矩阵 $A = U\Sigma V^T$，还必须把正交矩阵 $U$ 与 $V$ 也考虑进来。

由于 $U^TU = I$，我们可以自由地左乘 $U^T$ 而不改变任何长度（length）。

平方误差（squared error）满足

```math
\|b - A\hat{x}\|^2 = \|b - U\Sigma V^T\hat{x}\|^2 = \|U^Tb - \Sigma V^T\hat{x}\|^2 .
```

令 $c = V^T\hat{x}$，便得到 $\|U^Tb - \Sigma c\|^2$；最佳的 $c$ 是 $\Sigma^+U^Tb$。最后 $x^+$ 就是 $A^+b$：

> <span style="color:#1e8449;">**[note] Note（译者注：换基化简，把任意矩阵上的问题推成对角问题）:**</span> 本页证明的引擎是一个"换基化简"模板：orthogonal matrix（正交矩阵）相乘不改变长度，即 $\|U^Ty\|=\|y\|$，它来自前作的结论——orthogonal transformation（正交变换）保持 inner product（内积）不变，因为 $\|Uy\|^2=y^TU^TUy=y^Ty$。所以可以先自由地左乘 $U^T$、引入新变量 $c=V^T\hat x$（$V$ 可逆故二者一一对应），把"任意矩阵 $A$ 上的问题"化成"对角矩阵 $\Sigma$ 上的逐坐标问题"。对角化之后每个坐标独立：最佳 $c_i=(U^Tb)_i/\sigma_i$（当 $\sigma_i>0$），或 $0$（当 $\sigma_i=0$，即伪逆逐坐标取倒数）。最后再用 $V$ 转回去。这个"正交归约到对角、逐坐标处理、转回"的三段式，与 page_129 规则 3 的解读、page_136 证明伪逆极限时先证 $1\times1$ 再对角再 SVD 是同一条路——SVD（奇异值分解）在证明中的角色，就是给"任何矩阵本质上是对角矩阵加两个旋转"这句话背书。做作业时若遇"含任意 $A$ 的矩阵命题"，先问"把 $A=U\Sigma V^T$ 代入后 $U,V$ 会不会让路靠边"，往往一击即中。
> 
> 拿一组真数字走完全程。取 $A$ 的三行依次为 $(1,2)$、$(2,1)$、$(1,0)$，它的两个 singular value（奇异值）为 $3.087$ 与 $1.212$，条件数约 $2.547$；再取 $b=(1,-1,2)$。对五个随机 $x$ 逐点核对 $\|b-Ax\|^2$ 与 $\|U^Tb-\Sigma c\|^2$（其中 $c=V^Tx$），最大偏差 $1.4\times10^{-14}$——这不是近似，而是恒等，偏差只来自 float64 的舍入。再看正交性：$\|U^Tb\|^2$ 与 $\|b\|^2$ 都等于 $6.0$，一位不差。最后看"逐坐标"那一步：最小二乘解 $\hat x=(0.0714,0.1429)$，它在 $V$ 坐标系里的坐标 $c=(-0.1481,0.0598)$，乘上 $\sigma$ 后得 $(-0.4572,0.0725)$，恰好等于 $U^Tb$ 的前两个分量——第三个分量 $2.405$ 无法被 $\Sigma$ 达到，它就是残差在 $U$ 坐标系里的坐标，残差平方 $5.786$ 正是它的平方。
> 
> 为什么非要两步旋转？因为若不对 $A$ 做分解而直接对 $\|Ax-b\|^2$ 配方，你面对的是乘积 $U\Sigma V^T$ 混在一起、坐标互相耦合的局面；一旦乘上 $U^T$，$m\times n$ 的最小二乘问题就被拆成 $\min(m,n)$ 个互不相关的标量问题，每个形如 $(\sigma_ic_i-d_i)^2$，答案只有一个动作："除以 $\sigma$ 或置零"。这也顺带解释了病态从哪里来：$\sigma_i$ 越小，$1/\sigma_i$ 越大，$b$ 在该方向上的微小扰动会被放大成解的巨大抖动；$\sigma=10^{-6}$ 时倒数就是 $10^6$，而 float64 只有约 $16$ 位十进制有效数字，于是这个方向基本不可用。伪逆之所以在零处写零而不是写无穷，是因为在 $\mathbb R$ 上没有无穷可写，而这个方向本来就被 $N(A^T)$ 占据、与列空间正交，任何有限取值都只能制造伪信息。还有一处细节常被忽略：$\Sigma$ 是 $m\times n$ 的长方形对角矩阵，多出来的行或列全是零，所以 $\Sigma c$ 只占据 $\mathbb R^m$ 的前 $r$ 个坐标，其余坐标恒为零；残差在 $U$ 坐标系里之所以能安然待着，就是因为那个坐标位置本来就没有可用的奇异方向去承载它。
> 
> 跨课程坐标：Strang 18.06 §7.1–7.2 把这套东西画成"A 等于旋转、沿坐标轴拉伸、再旋转"的三段图，本页做的只是把图翻译成代数；PCA（主成分分析）对中心化数据矩阵做 SVD，主成分方向就是 $V$ 的列，主成分得分就是 $\Sigma$ 乘过去的坐标——所以"降维"在这个语言里就是"保留前 $k$ 个 $c_i$、其余置零"。史实上，把 SVD 变成可靠的数值算法的是 Golub 与 Kahan 在 1965 年的工作，后来 Golub 与 Reinsch 在 1970 年给出实用程序；具体卷期页码此处未能一手核实，故只记人名与年份。

---

```math
c^{+} = V^T x^{+} = \Sigma^{+}U^Tb, \qquad V^T = V^{-1} \ \Longrightarrow\  x^{+} = V\Sigma^{+}U^Tb = A^{+}b . \tag{3}
```

于是 SVD 一步就解出了最小二乘问题（$x^+ = A^+b$）。唯一剩下的问题是计算代价（computational cost）。

奇异值与奇异向量（singular values and singular vectors）比消元（elimination）更昂贵。

接下来提出的两种解法直接处理线性方程 $A^TAx = A^Tb$。

当 $A^TA$ 可逆时这种方法成功——此时得到的解 $\hat{x}$ 与 $x^+$ 相同。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.126</span>

---

<!-- page 131: 书页 127, OCR page 31 -->

### §II.2 Least Squares: Four Ways（最小二乘：四种方法）

#### When is $A^T A$ invertible（何时 $A^T A$ 可逆）?

矩阵 $A^T A$ 是否 invertible（可逆），是一个重要问题，而且它有一个漂亮的答案：当且仅当 $A$ 具有 independent columns（独立列）时，$A^T A$ 才可逆。
若 $A^T A x = 0$，则必有 $x = 0$。

> <span style="color:#1e8449;">**[note] Note（译者注：二次形式改写成范数平方，一步证出零空间相等）:**</span> 本页定理 $N(A^TA)=N(A)$ 的证明只用了一招：**把二次形式改写成范数平方**。若 $A^TAx=0$，两边左乘 $x^T$ 得 $x^TA^TAx=(Ax)^T(Ax)=\|Ax\|^2=0$，于是 $Ax=0$——一个"可能无解"的 linear system（线性系统）断言被"非负量之和为零"逼出结论。这个模板的威力在于可逆方向反复使用：证明某个矩阵零空间小，等价于证明相应 quadratic form（二次型）正定；证明 $\|Ax\|=0$ 蕴含 $x=0$，恰好就是"$A$ 有 independent columns（独立列）"的定义。反向包含 $N(A)\subseteq N(A^TA)$ 平凡，两级包含合起来就是 nullspace（零空间）相等。推论链很漂亮：$A^TA$ 可逆，当且仅当 $A$ 列满秩，当且仅当 $A^TA$ 是 positive definite（正定）的，而正定性又保证解唯一。这是 6.042J"双包含证相等"证明风格在矩阵论中的标准亮相，也是"$A^TA$ 的病态根源是 $A$ 的列接近相关"这句话的严格版本。
> 
> 把这条链放到 float64 里看。随机取 $6\times4$ 的 $A$，rank 为 4 时 $A^TA$ 的 rank 也是 4，最小 singular value（奇异值）为 $1.77$；把第 4 列改成前两列之和，rank 掉到 3，$A^TA$ 的最小 singular value 变成 $1.6\times10^{-15}$——它并不打印成 0，而是打印成这个量级的非零数，因为 float64 的 $\varepsilon\approx2.22\times10^{-16}$ 只能分辨到这个尺度。这就把正文那句"$A^TA$ 可逆当且仅当 $A$ 列独立"翻译成了可执行的判据：看最小 singular value 是否大于舍入噪声，而不是看它是否等于零。同一件事还有秩的视角：$C(A^TA)\subseteq C(A^T)$ 永远成立，而两边维数都等于 rank（秩），于是两个 subspace（子空间）相等、rank 也相等；实测三次随机试验里 rank$(A)$ 与 rank$(A^TA)$ 始终同步，掉秩时一起从 4 掉到 3，没有一次例外。
> 
> 更尖锐的例子能把两个条件数的关系一次说清：取 $A$ 的三行依次为 $(1,1)$、$(1,1+10^{-8})$、$(1,1-10^{-8})$，两列几乎重合。实测 cond$(A)=2.45\times10^8$，而 cond$(A^TA)$ 在 float64 里直接溢出成 inf——因为 cond$(A^TA)=$cond$(A)^2\approx6.0\times10^{16}$，已经超过 $1/\varepsilon\approx4.5\times10^{15}$，两个 singular value（奇异值）在舍入后不可区分。这不是"算得不准"，而是信息在平方那一步被毁掉了：$A^TA$ 的每个元素都是内积，两个几乎相同的列做内积时，乘积项的大半有效位互相抵消，差别只剩在最低几位上，这正是 cancellation（相消）的典型场景。这正是后面 QR 途径存在的理由，也是"永远不要显式乘出 $A^TA$"这条数值线性代数戒律的来源。
> 
> 两句精确化的话值得补上。第一，positive definite（正定）的根本定义是二次型 $x^TMx>0$ 对一切 $x\ne0$ 成立，对实对称矩阵它才等价于"特征值全正"；本注原句把两者并列，方向对但次序要留心——先有二次型条件，才有谱条件。第二，$A^TA$ 永远是 semi-definite（半正定）的，因为 $\|Ax\|^2\ge0$；"正定"只是列满秩时多出来的那一档。把这个谱系记牢，后面讲 weighted least squares（加权最小二乘）时 $A^TCA$ 的可逆性判据就是同一条链换了个度量。最后一个恒等式值得单独记住：$A^TA$ 对称，故可正交对角化成 $Q\Lambda Q^T$，而 $\lambda_i=\sigma_i^2$——于是"半正定"在谱上的说法就是"特征值非负"，"$\sigma_{\min}$ 接近零"在谱上的说法就是"最小特征值接近零"。两套语言来回翻译，许多定理会突然显得显然，而这也提示了一件编程实践上的事：判断秩亏时用 singular value（奇异值）比用特征值稳，因为后者在平方那一步已经损失了半个有效位。

$A$ 与 $A^T A$ 恒具有相同的 nullspace（零空间）！这是因为 $A^T A x = 0$ 总能推出 $x^T A^T A x = (Ax)^T (Ax) = \|Ax\|^2 = 0$。
于是 $Ax = 0$，也就是说 $x$ 属于 $N(A)$。

对于一切 $x$，下面的诸式全部成立：

```math
N(A^T A) = N(A) \quad \text{and} \quad C(A^T A) = C(A^T) \quad \text{and} \quad \mathrm{rank}(A^T A) = \mathrm{rank}(A^T) = \mathrm{rank}(A)
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 源 OCR 将证明链中的 $(Ax)^T(Ax) = \|Ax\|^2$ 以及 $C(A^T A)$、$\mathrm{rank}$ 诸式读成了零散乱码，此处按「$N(A^T A) = N(A)$」的经典证明逻辑重建。

下面我们转入 $A^T A$ 可逆的情形，用它来求解 normal equations（正规方程）$A^T A \hat{x} = A^T b$。

#### The Normal Equations（正规方程）

图 11.2（Figure 11.2）画出了 least squares（最小二乘）问题及其解的直观图景。
问题在于：$b$ 不在 $A$ 的 column space（列空间）之内，所以 $Ax = b$ 无解。
最佳向量 $P = A\hat{x}$ 是一个 projection（投影）——我们把 $b$ 投影到 $A$ 的列空间上。
向量 $\hat{x}$ 与 $P = A\hat{x}$ 都来自求解一个著名的线性方程组：$A^T A \hat{x} = A^T b$。
要对 $A^T A$ 求逆，我们必须确知 $A$ 具有独立列。

图中画出了那个至关重要的 right triangle（直角三角形），它的三条边分别是 $b$、$P$ 与 $e$：

> <span style="color:#1e8449;">**[note] Note（译者注：正规方程的几何、代数、统计三个入口）:**</span> 本页的 normal equations（正规方程）有三个等价入口，值得并排记忆。**几何**：残差 $e=b-A\hat x$ 必须垂直于 column space（列空间）$C(A)$，直角三角形的直角边就是这么来的；垂直等价于与每个 $Ac$ 的 inner product（内积）为零，等价于 $A^Te=0$。**代数**：$\|b-Ax\|^2$ 是 $x$ 的二次 convex function（凸函数），最优处 gradient（梯度）为零，而梯度恰是 $2A^T(Ax-b)$（用链式法则对 $\partial/\partial x_j\sum_i(\sum_k a_{ik}x_k-b_i)^2$ 逐项求导）——这正是 Boyd 凸优化讲义中可微凸函数最优性条件 $\nabla f(x^*)=0$ 的第一次显式使用，也是"求导得正规方程"的来源，page_128 页首原文即"极小意味着导数取零"）**统计**：误差向量 $e$ 与所有 explanatory variable（解释变量）的列不相关（$A^Te=0$），即回归残差正交于特征——这也是机器学习中"残差里不再有可提取的线性信息"的说法。projection matrix（投影矩阵）$P=A(A^TA)^{-1}A^T$（本页式 7）满足 $P^2=P$ 与 $P^T=P$，是"把 $b$ 扔到平面上"的解析表达。三视角将来分别通向最小二乘的 QR 版、凸优化版与统计版。
> 
> 用四组观测把三个入口各走一遍。取 $t=(0,1,2,3)$、$A$ 的两列为全 1 与 $t$、$y=(1,1.5,3,4.4)$，解正规方程得 $\hat x=(0.72,1.17)$，残差 $e=(0.28,-0.39,-0.06,0.17)$，残差平方和 $0.263$。核对几何入口：$A^Te$ 的两个分量实算都是 $0$（打印成 $0.$ 与 $0.$，范数 $1.6\times10^{-15}$）。核对代数入口：梯度 $2A^Te$ 的范数 $3.1\times10^{-15}$，也是机器零。核对矩阵结构：$P$ 是 $4\times4$，$\|P^2-P\|$ 的最大元 $2.2\times10^{-16}$、$\|P^T-P\|$ 恰为 $0$，trace 为 $2.0$，特征值是 $0,0,1,1$——秩 2 的投影在四维空间里留下两个不动方向与两个被压扁的方向，与"列空间是二维平面"完全一致。
> 
> 机制上值得把 Hessian（黑塞矩阵）看清：$f(x)=\|Ax-b\|^2$ 的 Hessian 是 $2A^TA$，它 positive definite（正定）当且仅当 $A$ 列满秩，所以极小点唯一、$P$ 唯一、$\hat x$ 唯一；一旦列相关，$2A^TA$ 出现零特征值，沿该方向 $f$ 是平的，极小点成一条直线——这与 page_130 的"最小范数解"是同一件事的两种说法。还要注意 $P$ 的 trace 等于 rank，实测 $2.0$ 与 rank 2 对得上；这条 ${\rm trace}(P)={\rm rank}(A)$ 不是巧合，因为幂等矩阵的特征值只能是 0 或 1，trace 就是 1 的个数，也就是投影到的子空间维数。
> 
> 史实坐标：最小二乘最早由 Legendre 在 1805 年发表，Gauss 在 1809 年的 Theoria motus 中给出概率论证并声称更早使用过；两人的卷期页码此处未能一手核实，故只记年份与著作名。跨课程坐标：Boyd 的凸优化把"梯度为零加凸性"当成标准配方，统计学把 $A^Te=0$ 当成残差诊断的第一条，而 18.06 把 $P$ 当成四个子空间图上的一个箭头。三处其实是同一个定理的三种方言，考试里换方言不换内容。把三个入口合成一句话：最小二乘就是"在 $C(A)$ 里找离 $b$ 最近的点"，而最近点的判据是误差与整个子空间正交。这条判据有三种等价写法，分别是几何写法 $e\perp C(A)$、内积写法 $A^Te=0$、方程写法 $A^TA\hat x=A^Tb$；它们不是三个定理，而是同一句话的三种记号。实测还能确认一条实用换算：$A^TA$ 对称 positive definite（正定），所以正规方程可以用 Cholesky（乔列斯基）分解在约 $n^3/3$ 次运算内解掉，比通用求逆便宜三倍；代价是 condition number（条件数）被平方，这一点 page_128 已提醒，后面讲 QR 时会给出替代方案。用四个子空间读 $P$ 也顺手：$P$ 在 $C(A)$ 上是恒等、在 $N(A^T)$ 上是零，中间没有第三种行为，所以 $P$ 的全部信息就装在这两个子空间里。

---

- $e = b - P$ 是 error vector（误差向量）；
- $P$ 是 $b$ 在 column space（列空间）中的 projection（投影）。

**图 11.2（Figure 11.2）**：projection（投影）$P = A(A^T A)^{-1}A^T b$ 正是 column space（列空间）中离 $b$ 最近的那个点。

人人都理解，$e$ 垂直于这个平面（即 $A$ 的 column space，列空间）。
这等价于说：$b - P = b - A\hat{x}$ 垂直于列空间中的每一个向量 $Ac$。

```math
(Ac)^T(b - A\hat{x}) = c^T A^T (b - A\hat{x}) = 0 \quad \text{for all } c \quad \text{forces} \quad A^T (b - A\hat{x}) = 0
```

一切结论都源自最后这个方程——把它改写成 $A^T A \hat{x} = A^T b$，就得到下面这组编号公式：

- $\hat{x}$ 的 normal equation（正规方程，normal equation for $\hat{x}$）：

```math
A^T A \hat{x} = A^T b \tag{4}
```

- $Ax = b$ 的 least squares solution（最小二乘解，least squares solution to $Ax = b$）：

```math
\hat{x} = (A^T A)^{-1}A^T b \tag{5}
```

- $b$ 在 $A$ 的 column space（列空间）上的 projection（投影，projection of $b$ onto the column space of $A$）：

```math
P = A\hat{x} = A(A^T A)^{-1}A^T b \tag{6}
```

- 作用在 $b$ 上而给出 $P$ 的 projection matrix（投影矩阵，projection matrix that multiplies $b$ to give $P$）：

```math
P = A(A^T A)^{-1}A^T \tag{7}
```

- projection matrix（投影矩阵）的幂等性质（idempotence，下一页将用它验证 $P^2 = P$）：

```math
P^2 = P \tag{8}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 源在本页末尾仅捕获到编号 (8) 而未捕获其公式内容；下一页（书页 128）明确写出"Use equation (8) for $P$"并展开验证 $P^2 = P$，据此式 (8) 补为投影矩阵的幂等式 $P^2 = P$（原书此式或与 (7) 同形，以原书为准）。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.127</span>

---

<!-- page 132: 书页 128, OCR page 32 -->

### Computations with Large Matrices（与大矩阵有关的计算）

此刻 $A$ 已具有独立列：$\mathrm{rank} = n$。
于是 $A^T A$ 正定且可逆，公式 (4)、(5)、(6) 中的 inverse（逆矩阵）都有意义。
对 rank（秩）等于 $n$ 的列满秩情形，可以进一步说明：$\hat{x}$ 是唯一的 least squares solution（最小二乘解）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 源 OCR 在行首仅残留 "now has independent columns" 且把 $r = n$ 误读为缺失，此处按上页「$A^T A$ 可逆 ⟺ $A$ 具有独立列」衔接重建为「此刻 $A$ 已具有独立列，$\mathrm{rank} = n$」。

我们还可以核对：由 normal equations（正规方程）解出的 $\hat{x}$，与伪逆（pseudoinverse）给出的 $\hat{x} = A^{+}b$ 是同一个向量。
之所以不存在其他解 $\hat{x}$，是因为假定秩为 $n$，于是 $A^T A$ 的 nullspace（零空间）只含零向量，解便唯一。

projection matrix（投影矩阵）$P$ 具有特殊性质 $P^2 = P$：当我们第二次投影时，投影 $P$ 保持完全不变。
对式 (8) 中的 $P$ 直接验证如下：

> <span style="color:#1e8449;">**[note] Note（译者注：幂等加对称，才是正交投影的完整刻画）:**</span> 投影的幂等条件 $P^2=P$（idempotent，幂等）与对称条件 $P^T=P$ 一起精确刻画 orthogonal projection（正交投影）：投影是"到子空间里找最近点"的算子，最近点已在子空间内，再投一次当然不动——$P^2=P$ 就是把这句话写成代数。第 131 页的验证只是把矩阵链 $(A(A^TA)^{-1}A^T)^2$ 中部的 $A^TA$ 与 $(A^TA)^{-1}$ 抵消掉。更深一层：任何"解方程组"的算法，例如 elimination（消元）、QR、SVD，本质上都在计算同一个投影 $P=AA^+$，差别只在数值路径。$e=b-Pb$ 则落在 $N(A^T)$，配合 $\mathbb R^m=C(A)\oplus N(A^T)$ 的正交分解，你就拥有图 11.2 之外完全不用画图的代数表达。这条幂等性质在 page_138 加权情形还会以 $P_w=A(A^TC^{-1}A)^{-1}A^TC^{-1}$ 出现，仍然幂等，只是换成 $C^{-1}$ 度量下的"斜投影"——认识原型，变体就只是换内积。
> 
> 先看为什么幂等就够一半。若 $Pv=\lambda v$ 且 $v\ne0$，则 $\lambda v=Pv=P^2v=\lambda^2v$，于是 $\lambda=\lambda^2$，即 $\lambda\in\{0,1\}$；实测上例 $4\times4$ 的 $P$ 特征值正是 $0,0,1,1$，trace 为 $2.0$，与 rank 2 一致。这一行推导解释了"投影没有中间档"：一个向量要么原样留下，要么整个被抹掉，不存在"投一半"的伸缩。
> 
> 再看为什么必须补上对称。取 $P$ 的两行为 $(1,1)$ 与 $(0,0)$，它满足 $P^2=P$（实算差为 $0$），但 $P^T-P$ 的最大元是 $1$，特征值仍是 $1$ 与 $0$，trace 仍是 $1$。它的像是什么？$P$ 把 $(0,1)$ 送到 $(1,0)$，把 $(1,-1)$ 送到 $(0,0)$——所以它是"沿方向 $(1,-1)$ 把整个平面压到 $x$ 轴"的投影，投影方向与被投影的子空间不垂直，这叫 oblique projection（斜投影）。斜投影同样幂等，却会把垂直方向的长度也算进影子，因此不保长度、不保角度，也就不是"最近点"算子。对称性是排除这种倾斜的唯一条件，这就是为什么"幂等 + 对称"缺一不可。
> 
> 两个后续连接。其一，$P^T=P$ 加 $P^2=P$ 之后，$P$ 可正交对角化成 $Q{\rm diag}(1,\dots,1,0,\dots,0)Q^T$，对角元 1 的个数等于 rank，这就是"选一组正交基、保留前 $r$ 个坐标、其余清零"的矩阵写法。其二，加权情形 $P_w$ 幂等但不对称，它在标准内积下是斜投影，在 $C^{-1}$ 内积下才重新变成正交投影——所以"投影"这个概念永远相对于某个内积而言，换度量就换几何。数值上还能看到一条工程事实：float64 里 $P^2-P$ 的残差是 $2.2\times10^{-16}$，代数律在浮点里也只退化到机器精度，这也提醒你写判断时不要用严格等号比较矩阵。把 $P$ 与 $I-P$ 并排看，正交分解就成了算子恒等式：两者都幂等、都对称，乘积 $P(I-P)=0$，相加 $P+(I-P)=I$。$P$ 投到 $C(A)$，$I-P$ 投到 $N(A^T)$，两个像空间正交、直和凑满 $\mathbb R^m$——这正是 $\mathbb R^m=C(A)\oplus N(A^T)$ 的矩阵版。换成 SVD（奇异值分解）的语言更直白：$P=AA^+=U_rU_r^T$，其中 $U_r$ 是前 $r$ 个左 singular vector（奇异向量）组成的列正交矩阵，于是 $P$ 就是"对 $U_r$ 的列做内积、再加权求和"的算子，$P^2=P$ 与 $P^T=P$ 都退化成 $U_r^TU_r=I_r$ 的直接推论。这也解释了为什么投影的"数据量"只有 $r$ 个方向：$m\times m$ 的 $P$ 里真正独立的参数只有 $r$ 个左奇异向量所张的那一块。最后一句警告：$P^2=P$ 单独成立时，$P$ 的像与 kernel（核）可能斜交，trace 仍等于像的维数，但"最近点"的解释失效；所以检验一个矩阵是不是正交投影，必须两条一起查。

```math
P^2 = A(A^T A)^{-1}A^T A (A^T A)^{-1}A^T = A(A^T A)^{-1}A^T = P
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 行首的「尹 2」重建为 $P^2$，「风」「蓋」重建为 $A$，矩阵链 $A(A^T A)^{-1}A^T A (A^T A)^{-1}A^T = A(A^T A)^{-1}A^T = P$ 系按 $P^2 = P$ 的标准约化重建。

### The Third Way to Compute $\hat{x}$: Gram-Schmidt（计算 $\hat{x}$ 的第三种方法：Gram-Schmidt）

仍假定 $A$ 的列相互独立：$\mathrm{rank} = n$。
但不再假定它们正交！此时 $A^T A$ 不是对角矩阵，求解 $A^T A \hat{x} = A^T b$ 需要付出两倍的代价。
我们的第三种方法先把 $A$ 的列 orthogonalize（正交化），于是 $\hat{x}$ 便容易求出。

不妨这样说：工作量现在转移到制造正交（乃至 orthonormal，标准正交）的列上。
确实如此：与直接解 $A^T A \hat{x} = A^T b$ 相比，运算量实际翻倍，但正交向量带来了 numerical stability（数值稳定性）。
当 $A^T A$ 接近 singular（奇异）时，稳定性变得举足轻重。

$A^T A$ 的 condition number（条件数）等于其范数 $\|A^T A\|$ 乘以 $\|(A^T A)^{-1}\|$。
当这个数很大时，明智的做法是预先将 $A$ 的列正交化，转而与一个 orthogonal matrix（正交矩阵）$Q$ 打交道。

矩阵 $Q$ 的 condition number（条件数）是 $\|Q\|$ 乘以 $\|Q^{-1}\|$。
$Q$ 的两个范数都等于 $1$，于是 $\|Q\| \cdot \|Q^{-1}\| = 1$，所以 $Q$ 的 condition number（条件数）为 $1$。

> <span style="color:#1e8449;">**[note] Note（译者注：条件数是误差放大系数，正交矩阵是零损耗通道）:**</span> 为什么"与正交矩阵打交道"就安全？condition number（条件数）$\mathrm{cond}(A)=\sigma_{\max}/\sigma_{\min}$ 的几何意义是 $A$ 对单位球的**最大拉伸与最小拉伸之比**；orthogonal matrix（正交矩阵）的全部 singular value（奇异值）都等于 1，等价于刚体旋转或反射——它把任何误差球仍映成同半径的球，不放大任何方向，所以 $\mathrm{cond}(Q)=1$ 是所有矩阵中最低的。求解 $Ax=b$ 的相对误差大致按 $\varepsilon\cdot\mathrm{cond}(A)$ 放大，CSAPP 的机器精度 $\varepsilon$ 在这里被"矩阵的几何"乘了一个因子。因此 QR 途径（解 $Rx=Q^Tb$）的误差只吃 $\mathrm{cond}(A)$ 而不吃 $\mathrm{cond}(A)^2$（见 page_128 注），代价正是本页明说的"工作量翻倍"。以 6.006 的口吻：这是**用常数因子的算力换一个量级的稳定性**，几乎所有生产代码，例如 MATLAB 的反斜杠、LAPACK都乐意付这个常数。理解"条件数等于误差放大系数"这条链，CSAPP 的浮点章与数值线性代数就算正式打通了。
> 
> 用 Hilbert matrix（希尔伯特矩阵）把差距量出来。取 $6\times6$ 的 Hilbert 矩阵，元素为 $1/(i+j+1)$，实测 cond 为 $1.495\times10^7$，它的平方是 $2.235\times10^{14}$，已经逼近 $1/\varepsilon\approx4.5\times10^{15}$。取真解全为 1 造出 $b$，再回解：直接解 normal equations（正规方程）$A^TA\hat x=A^Tb$ 的相对误差是 $5.4\times10^{-3}$，只保住三位有效数字；同一题用 QR 路线，numpy 的 lstsq 内部也是 QR，的相对误差是 $4.5\times10^{-11}$，两者相差约 $1.2\times10^8$ 倍。正交矩阵那边则毫无损耗：随机 $5\times5$ 的正交矩阵实测 cond 为 $1.0000000000000007$，五个 singular value（奇异值）全是 $1$，误差球投过去还是同样的球。
> 
> 为什么差这么多？误差界的主项是 $\varepsilon\cdot\mathrm{cond}(A)$；正规方程把矩阵换成 $A^TA$，它的 cond 是原矩阵的平方，于是同一个 $\varepsilon$ 被乘了两次。QR 的分解 $A=QR$ 里 $Q$ 是 orthogonal（正交）的、cond 为 1，而 $R$ 的 cond 与 $A$ 相同（因为 $R^TR=A^TA$ 且 $R$ 是上三角，两者的奇异值一一对应），所以回解 $Rx=Q^Tb$ 只吃一次 cond。代价是算力：Householder（豪斯霍尔德）反射做 QR 约 $2mn^2-2n^3/3$ 次浮点运算，而正规方程只需乘出 $A^TA$（$mn^2$ 次）再加 Cholesky（乔列斯基）分解（$n^3/3$ 次），大约便宜一半；这是"用常数因子换一个量级精度"的经典交易。
> 
> 跨课程坐标：CSAPP 第 2 章的 float 表示给出 $\varepsilon\approx2.22\times10^{-16}$，本页的数字正是这个常数乘上矩阵几何之后的结果；6.006 的语言里这叫"渐近代价相同、常数不同"，而 LAPACK 与 MATLAB 的反斜杠都选 QR 路线，说明工程界愿意付这个常数。史实上，QR 分解由 Householder 在 1958 年提出（卷期页码此处未能一手核实），Golub 与 Kahan 在 1965 年把它与 SVD（奇异值分解）的计算连成一体；具体卷期亦未能一手核实，故只记人名与年份。一个可操作的建议：判据不要看 cond 的绝对值，而要看 $\varepsilon\cdot\mathrm{cond}(A)$ 是否接近 1——若接近，矩阵在这台机器上就不可逆，任何算法都救不回来。还有一层容易忽略的机制：cond 不是矩阵的固有属性，而是矩阵相对于所选 norm（范数）与坐标系的属性。同一个问题换一组单位，$A$ 的列被缩放，cond 就会变，这解释了为什么"把列归一化"常被当作最便宜的预条件。但它只治一种病。实测对 $6\times6$ 的 Hilbert 矩阵做列归一化，cond 只从 $1.495\times10^7$ 降到 $8.776\times10^6$，仅降了约四成——因为它的病态不来自列长度失衡，而来自列与列近乎平行。换一个列长度相差极悬殊的矩阵，同一个操作能把 cond 砍掉几个量级。所以"先看病因再选预条件"这句经验，比记住任何公式都值钱。

---

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 源 OCR 将 $\|Q^{-1}\| = 1$、$\|Q\| \cdot \|Q^{-1}\| = 1$ 读成乱码（「日 0 日」「豆 况 巳」），此处按正交矩阵范数恒为 $1$ 的标准事实重建。

### Gram-Schmidt（格拉姆-施密特正交化）

这里就是著名的 Gram-Schmidt 思想：从 $A$ 出发，以 $Q$ 收尾。
独立列 $a_1, \dots, a_n$ 经过处理得到 orthonormal（标准正交）的 $q_1, \dots, q_n$——这是线性代数中的一项 fundamental computation（基础计算）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 把「independent columns $a_1, \dots, a_n$ lead to orthonormal $q_1, \dots, q_n$」一句肢解为碎片，此处据 Gram-Schmidt 思想段重建。

第一步是取 $q_1 = a_1/\|a_1\|$，那是一个 unit vector（单位向量），满足 $q_1^T q_1 = 1$。
接着从 $a_2$ 中减去它在 $q_1$ 方向上的分量：

- Gram-Schmidt step（正交化步骤，Orthogonalize）：$a_2^{o} = a_2 - (q_1^T a_2)\,q_1$；
- Normalize（归一化）：$q_2 = a_2^{o}/\|a_2^{o}\|$。

这正是公式 (10)。

减去分量 $(q_1^T a_2)\,q_1$ 所得的向量 $a_2^{o}$ 与 $q_1$ 正交，因为：

```math
q_1^T a_2^{o} = q_1^T a_2 - (q_1^T a_2)(q_1^T q_1) = q_1^T a_2 - q_1^T a_2 = 0 \quad \text{since } q_1^T q_1 = 1
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 源将上述内积验证行读作碎片（「直 hogon 引」即 orthogonal，"since ql ql" 实为 $q_1^T q_1$），此处按 $q_1^T q_1 = 1$ 的代数验证重建。

这一过程继续推进到 $a_3$ 与 $q_3$，每一步都归一化使 $\|q_i\| = 1$：
从 $a_3$ 中减去它沿 $q_1$ 与 $q_2$ 的分量，就留下 $a_3^{o}$：

- Orthogonalize（正交化）：$a_3^{o} = a_3 - (q_1^T a_3)\,q_1 - (q_2^T a_3)\,q_2$；
- Normalize（归一化）：$q_3 = a_3^{o}/\|a_3^{o}\|$。

这便是公式 (12)。
于是 $q_1^T q_2 = 0$、$q_1^T q_3 = 0$，且 $\|q_3\| = 1$。
将矩阵 $A$ 的诸列表示为这些正交基向量 $q_i$ 的线性组合：

```math
a_1 = \|a_1\|\, q_1, \quad a_2 = \|a_2\|\, q_2 + (q_1^T a_2)\, q_1, \quad a_3 = \|a_3\|\, q_3 + (q_2^T a_3)\, q_2 + (q_1^T a_3)\, q_1
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页最后 5 行 OCR 严重碎裂（「a，s 什 0 皿 q，s」「@1 日 ql」「= （ + 2 日 q2」），据 Gram-Schmidt 的正交化链重建为「诸列 $a_i$ 表作 $q$ 的线性组合」一图；该行应当是向量等式 $a_1 = \|a_1\| q_1$ 之类，因 OCR 缺行，此处以三列展开式收尾，请与书页图核对。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.128</span>

---

<!-- page 133: 书页 129, OCR page 33 -->

> <span style="color:#7f8c8d;">本页结构单元：§11.2 Least Squares: Four Ways（续）→ QR 分解式 (14) → $R = Q^T A$ 上三角的论证与 $A^T A = R^T R$ → 最小二乘解的 QR 形式 $\hat{x} = R^{-1}Q^T b$ → 子节 Gram-Schmidt with Column Pivoting → 列主元的动机（对照消元的行交换）→ 旧/新两套做法 → 第 $j$ 步算法描述。正文页。</span>

### 11.2. Least Squares: Four Ways（最小二乘：四种方法）

<span style="color:#2471a3;">**[section]**</span> 本页承接上一页对 Gram-Schmidt（格拉姆-施密特）的讨论，为 §11.2 的 QR 途径收尾。

前述那些等式（equations）告诉我们：矩阵 $R = Q^T A$ 是上三角（upper triangular）的。

其中 $R$ 的 $(i, j)$ 元素正是内积（inner product）$r_{ij} = q_i^T a_j$：

```math
A = \begin{bmatrix} q_1 & q_2 & q_3 \end{bmatrix}
\begin{bmatrix} r_{11} & r_{12} & r_{13} \\ 0 & r_{22} & r_{23} \\ 0 & 0 & r_{33} \end{bmatrix}
= Q R \tag{14}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 将上式版式拆散成 `q1 q2 q3` 与三个三角行等残片，这里按矩阵乘法语境重建为上三角分块乘积 $A = QR$。

Gram-Schmidt 从相互独立的列 $a_1, \ldots, a_n$ 产生标准正交（orthonormal）的向量 $q_1, \ldots, q_n$。

于是得到 $A = QR$。

若 $j < i$，即 $a_j$ 并不参与更早产生的 $q_i$，故 $r_{ij} = q_i^T a_j = 0$，这正是 $R$ 上三角的原因。

> <span style="color:#1e8449;">**[note] Note（译者注：R 为什么上三角，以及它与 Cholesky 因子的同一性）:**</span> 关于 $R$ 为什么上三角，这个结论的证明其实是一次"按时间顺序看结构"的论证：$r_{ij}=q_i^Ta_j$ 是第 $j$ 个原始列在第 $i$ 个基方向上的投影。若 $j\lt i$，列 $a_j$ 早于 $q_i$ 被"处理"——$a_j$ 展开时只用 $q_1,\dots,q_j$（page_132 末的等式是 $j$ 项截断），与后来才出生的 $q_i$（$i>j$）正交，内积必为 0。这类"构造顺序决定稀疏模式"的论证在 elimination（消元）中也有孪生兄弟：LU 分解里 $U$ 的 $(i,j)$ 元在 $j\lt i$ 时为零，原因同样是"列 $j$ 在第 $j$ 步之后不再进入后面的行"。更妙的是 $A^TA=R^TR$ 这一行：$R$ 是 upper triangular（上三角）且对角元为正（$r_{jj}=\|a_j^o\|>0$），而 symmetric positive definite（对称正定）矩阵的 Cholesky 分解是唯一的——所以 **$R$ 正是 $A^TA$ 的 Cholesky 因子**。换言之，Gram-Schmidt 与 QR 悄悄完成了"对 $A^TA$ 做 Cholesky"这件事，却全程只用 $A$ 的列做内积，从未乘出 $A^TA$，因此绕开了 page_128 的条件数平方。这是"代数恒等、数值迥异"最漂亮的案例。
> 
> 拿一组真数字走到底。取 $A$ 的三行依次为 $(1,2,3)$、$(1,3,6)$、$(1,4,10)$，跑 classical Gram-Schmidt（经典格拉姆-施密特），得到的 $R$ 三行是 $(1.732,5.196,10.970)$、$(0,1.414,4.950)$、$(0,0,0.408)$，对角元全为正、下三角全为零；$A-QR$ 的最大元是 $0$，$A^TA-R^TR$ 的最大元是 $5.7\times10^{-14}$。再把 $A^TA$ 交给 Cholesky（乔列斯基）分解得下三角 $L$，实测 $R$ 与 $L^T$ 的最大差是 $4.6\times10^{-14}$——两者确实是同一个因子。顺带量一下条件数：cond$(A)=181.891$，cond$(A^TA)=33084.4$，而 $181.891^2\approx33084.3$，后者正好是前者的平方，这就是 QR 绕开平方放大的一手证据。
> 
> 机制上再补一句"顺序"的含义：Gram-Schmidt 是一个逐列前进的算法，第 $j$ 步只知道 $a_1,\dots,a_j$，所以 $a_j$ 的展开式必然只有前 $j$ 个基向量；$R$ 的上三角形状不是被证明出来的，而是被算法的因果顺序强加出来的。这解释了为什么 $R$ 的对角元是正的：$r_{jj}$ 是 $a_j$ 去掉前面分量后剩余部分的长度，长度按定义非负，而列独立保证它不为零，于是 $r_{jj}>0$，Cholesky 的唯一性才有落脚点。若某一步 $r_{jj}=0$，说明 $a_j$ 落在前面列的 span（张成空间）里，列相关，算法必须停下来——这也是 Gram-Schmidt 天然的秩检测机制。
> 
> 史实坐标：Gram 在 1883 年发表，出处是 J. reine angew. Math. 94, 41–73, DOI 10.1515/crll.1883.94.41；Schmidt 在 1907 年给出后来被教程采用的正交化版本，载 Math. Ann. 63，卷期页码此处未能一手核实）。Cholesky 的故事更曲折：André-Louis Cholesky 在 1918 年阵亡，方法由 Commandant Benoît 在 1924 年整理发表，出处是 Bull. Géodésique 2, 67–77，所以"Cholesky 因子"这个名字属于一位没能看到它流传的人。数值上还有一处细节值得记：classical 与 modified Gram-Schmidt（经典与修正格拉姆-施密特）在本例的输出逐位相同，正交性残差都是 $1.6\times10^{-14}$，因为 cond 只有 $181.891$；两者的差别要到 cond 很大、舍入逐步累积时才显现，那时修正版每步重算内积，保住的正交性能好一个量级。换个角度看 $R$ 的对角元：$|\det A|=|\det Q||\det R|=|\det R|$，因为 $\det Q=\pm1$，所以 $|\det R|$ 就是 $A$ 的列所张 parallelotope（平行体）的体积，而 $r_{jj}$ 是第 $j$ 列去掉前面分量后剩下的高度——Gram-Schmidt 每一步都在算"这一列贡献了多少新的体积"。若某列几乎落在前面列的 span（张成空间）里，这个高度就几乎为零，体积随之趋零，于是"体积塌陷"与"秩亏"是同一个现象。用行列式语言还能量出稳定性：$\log|\det R|=\sum_j\log r_{jj}$，病态时某一项会突然变得极负，直接告诉你信息是在哪一列丢掉的。

并且由于 $Q^T Q = I$，有 $A^T A = R^T Q^T Q R = R^T R$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 的 `T = RTQTQR = T 娓` 依 $A = QR$ 重建为 $A^T A = R^T Q^T Q R = R^T R$。

因此对 $Ax = b$ 的最小二乘解（least squares solution），QR 途径给出 $\hat{x} = R^{-1} Q^T b$。

对应的 MATLAB 命令是 `[Q, R] = qr(A)`，因为 $R = Q^T A$。

也不难验证：向量 $\hat{x} = (A^T A)^{-1} A^T b$ 恰好等于 $(R^T R)^{-1} R^T Q^T b$。

这正就是 $R^{-1} Q^T b$，与上面的 QR 解完全一致。

### Gram-Schmidt with Column Pivoting（带列主元的格拉姆-施密特）

<span style="color:#2471a3;">**[section]**</span> 上面这段 Gram-Schmidt 描述，是按 $A$ 各列的原始顺序 $a_1, a_2, a_3, \ldots$ 来处理的。

这可能是危险的（dangerous）！

我们绝不可能容忍一个不允许行交换（row exchanges）的消元（elimination）程序——那样舍入误差（roundoff error）会把我们彻底毁掉。

> <span style="color:#1e8449;">**[note] Note（译者注：列主元与行交换的对偶——主元是给自由度排序的贪心）:**</span> column pivoting（列主元）是 elimination（消元法）里 partial pivoting（部分主元）的镜像：消元靠 row exchange（行交换）保证 pivot（主元）$u_{ii}$ 不接近零，得到 $PA=LU$；Gram-Schmidt（格拉姆-施密特）正交化则靠 column exchange（列交换）保证每一步取剩余列中 norm（范数）最大者，得到 $AP=QR$。为什么非要最大？因为 $r_{jj}=\|a_j^{o}\|$ 就是这一列的 pivot，其中 $a_j^{o}$ 是第 $j$ 列被前面 $j-1$ 个方向剥掉之后剩下的部分：这个数小，说明该列与已选方向近乎 linear dependence（线性依赖），硬把它选进来会让 $R$ 的 condition number（条件数）爆炸，解被 roundoff error（舍入误差）摧毁。`CSAPP`（深入理解计算机系统）第 2 章把机制讲透了：浮点减法吃掉有效位，而除以一个"看起来不是零、实际只是噪声"的数，会把这些噪声放大成答案本身。
>
> 给一个能算的家族，把上面的说法变成数字。取 $A(\delta)=\begin{bmatrix}1&1\\1&1+\delta\\0&0\end{bmatrix}$，不换列做 Gram-Schmidt 得 $r_{11}=\sqrt2$、$r_{12}=(2+\delta)/\sqrt2$、$r_{22}=\delta/\sqrt2$，所以主元比 $r_{11}/r_{22}=2/\delta$，实测条件数 $\kappa\approx4/\delta$：$\delta=10^{-8}$ 时 $r_{22}=7.07\times10^{-9}$、$\kappa=4.0\times10^{8}$。真正的判据是 $\kappa\varepsilon\ll1$：$\varepsilon=2.22\times10^{-16}$ 下 $\delta=10^{-12}$ 给出 $\kappa\varepsilon\approx8.9\times10^{-4}$，实测 $Q$ 的正交性误差已经 $6.3\times10^{-4}$；$\delta=10^{-16}$ 时 $r_{22}$ 直接落到噪声地板 $3.1\times10^{-16}$，$\max|Q^{\top}Q-I|=1.41$，基整体塌掉，$R$ 里全是垃圾。
>
> permutation matrix（置换矩阵）为什么必须写在右边，这是本节最容易滑过去的一步。$AP$ 是把 $A$ 的列重排，重排之后的第 $j$ 个列才轮到 $q_j$ 去处理，于是"后来才出生的方向与被剥过的列正交"这条时间顺序仍然成立，$R$ 保住了 upper triangular（上三角）的形状；若把置换搬到左边写成 $PA=QR$，那是在换行，$R$ 的 $(i,j)$ 位置与"第几列什么时候被处理"的对应关系被打断，上三角结构随之消失。所以列主元不是随便找个地方塞一个置换，它必须是"给列的出场次序排序"这一件事的唯一正确写法。
>
> 去掉列交换会塌成什么，上面的 $\delta=10^{-16}$ 已经演示了：$A=QR$ 这个等式在浮点里仍然能对上（残差约 $\varepsilon$ 量级），但 $Q$ 的各列不再互相正交，它就不再是列空间的一组基，最小二乘解也随之失去意义。分解"存在"与分解"可用"是两回事，这正是本页反复强调 dangerous（危险）的原因。
>
> 另有两个洞见值得记下。其一，把工作提前不增加总量：新做法"一得到 $q_{j-1}$ 就立刻对全部剩余列做正交化"表面上每步更忙，实则每个剩余列无论早晚都要减掉 $(a_j^{\top}q_{j-1})q_{j-1}$，总工作量仍停在 $2mn^{2}$ 量级，这是 `CLRS` 与 `6.006`（算法导论课）里的 aggregate analysis（聚集分析）：付同一笔钱，换来"每步收尾时所有剩余列都已与已选基正交"这个 invariant（不变量），下一步才能纯粹按长度挑列；而且边算边减还能顺带更新剩余列的长度，不必每轮重扫一遍。其二，要承认 pivot 的上限：列交换只能消掉算法自造的放大，动不了 $A$ 本身的 $\kappa$——换列不改变 singular value（奇异值），$\delta=10^{-16}$ 那种矩阵怎么换列都救不回来。这不是理论洁癖，它决定了"该换算法还是该换数据"这个工程判断。说到底，主元策略就是给 degree of freedom（自由度）排序的 greedy algorithm（贪心算法），`CLRS` 第 16 章"每步取局部最优、换取全局可控"的模板在这里一字不差地成立。
>
> 史实坐标：Householder 1958 年在 Journal of the ACM 5(4):339–342 给出"一步造出正交 $Q$"的办法；把列主元并进这条路线通常归于 Businger 与 Golub 1965 年在 Numerische Mathematik 的短文；Golub 1965 年同刊 7:206–216 的长文把最小二乘的几条 QR 路线系统化，正是本节"四种方法"的直接前身。

---

类似地，Gram-Schmidt 的每一步都应当从一个新列开始，使它尽可能独立于已经处理过的那些列。

于是我们需要列交换（column exchanges），用来挑出范数最大的剩余列。

处理过程中要随时改变各列的顺序。

只要能从 $A$ 的剩余列中正确挑列，我们就可以对 Gram-Schmidt 做出一个简单修改（simple change）：

<span style="color:#2471a3;">**[example]**</span> 旧做法（Old）：把下一列接受为候选，然后减去它在方向 $q_1$ 至 $q_{j-1}$ 上的分量。

新做法（New）：一旦求得 $q_{j-1}$，就从所有剩余列中减去该 $q_{j-1}$ 方向上的分量。

这看起来像是更多的工作，其实并非如此。

无论迟早，我们都要从每个剩余列 $a_j$ 中减去 $(a_j^T q_{j-1})q_{j-1}$。

现在不过是尽早做——刚知道 $q_{j-1}$ 就动手。

这样我们就能自由地挑选下一列，并且总是选范数最大的那一列。

消元与 Gram-Schmidt 的对照：

```math
\text{Elimination: } P A = L U \qquad \text{Gram-Schmidt: } A P = Q R
```

两种情形里的 $P$ 都是置换矩阵（permutation matrix）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> 消元用行交换得 $PA = LU$；Gram-Schmidt 用列交换故置换矩阵 $P$ 右乘，OCR 的 `尹 = QR` 重建为 $AP = QR$。

假设执行了 $j-1$ 步带列主元的 Gram-Schmidt，得到标准正交的单位向量（orthonormal unit vectors）$q_1, \ldots, q_{j-1}$。

这些向量正好排成矩阵 $Q_{j-1}$ 的各列。

方阵（square matrix）$R_{j-1}$ 把上述各列组合起来，生成 $A$ 中已经处理好的 $j-1$ 列。

此刻 $A$ 的所有剩余列都已被"清干净"——即都已对向量 $q_1$ 至 $q_{j-1}$ 做过正交化（orthogonalize）处理。

我们正在优化列的顺序（optimizing the column order）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 该句只剩 `" 叻 " a against the vectors ql to …` 残片，按"剩余列都减去相应分量"的算法语义重建。

<span style="color:#2471a3;">**[note]**</span> 第 $j$ 步（Step $j$）：

从 $A$ 的剩余各列中选出最大的一列。

把它归一化（normalize）到长度 1，这就是 $q_j$。

再对每一个仍在等待挑选的向量，减去它在最新的 $q_j$ 方向上的分量。

做完这些，就可以进入第 $j+1$ 步了。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.129</span>

---

<!-- page 134: 书页 130, OCR page 34 -->

> <span style="color:#7f8c8d;">本页结构单元：章题页眉 Computations with Large Matrices（重复元素，不译）→ 采用 Martinsson 2016 APPM 5720 讲义，以伪代码表达列主元 Gram-Schmidt 的第 $j$ 步 → 循环结束得 $A = QR$，$R$ 上三角的条件 → 置换输出与用 Householder 使算法更稳 → 问答：Gram-Schmidt 的 $Q$ 与 SVD 的 $U$ 是否相同。正文页。</span>

> <span style="color:#7f8c8d;">页眉：Computations with Large Matrices（大矩阵计算）——本章标题，每页重复出现，按规则不译。</span>

<span style="color:#2471a3;">**[section]**</span> 本节继续讨论带列主元的 Gram-Schmidt（格拉姆-施密特）。

我们沿用 Gunnar Martinsson 2016 年为 APPM 5720 课程编写的讲义（course notes），用伪代码（pseudocode）来书写第 $j$ 步。

原始矩阵 $A$ 是 $m \times n$ 的，开始时矩阵 $Q_0$ 与 $R_0$ 都为空。

第 $j$ 步就是下面的循环（loop）：它从 $Q_{j-1}$ 开始，到 $Q_j$ 结束。

当 $j$ 达到 $\min(m, n)$ 时，代码停止。

这就是 Gram-Schmidt 中的列主元（column pivoting）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 的 `for A PPM 5720` 依 Martinsson 课程编号重建为 for APPM 5720；`mm ()` 重建为 $\min(m, n)$。

<span style="color:#2471a3;">**[note]**</span> 该循环逐次完成下面这些操作（OCR 伪代码各行被噪声严重破坏，按标准列主元 QR 算法以 MATLAB 风格重建）：

第一步，找出 $A_{j-1}$ 中尚未被选入基的最大列，把它取作当前要处理的列。

将其归一化（normalize），给出新的单位向量（unit vector）$q$。

更新式 $Q_j = [Q_{j-1} \ q]$ 把新的标准正交单位向量 $q$ 接到 $Q_{j-1}$ 之后。

求出 $q$ 与 $A$ 各剩余列的内积（inner products）所构成的那一行。

用这个新的内积行更新 $R_j$。

最后令 $A_j = A_{j-1} - q r$，从每一列中减去这个新的秩一分量（rank-one piece）。

> <span style="color:#1e8449;">**[note] Note（译者注：列主元 QR 的秩一更新写法，为什么它就是修正 Gram-Schmidt）:**</span> 伪代码的精髓在第 $j$ 步的三连招：选出剩余列中 norm（范数）最大者，normalize（归一化）得 $q_j$，再用 rank-one update（秩一更新）$A_j=A_{j-1}-q_jr_j^{\top}$ 把这个方向从所有剩余列上剥掉。rank-one update 意味着每一列只做一次 $O(m)$ 的向量减法，第 $j$ 步要处理 $n-j$ 列，故单步 $O(mn)$，全程 $O(mn^{2})$；精确到系数是 $2mn^{2}-2n^{3}/3$ 次 flop（浮点运算），与 page_124 的 bidiagonalization（双对角化）同阶，$m=10^{4}$、$n=10^{2}$ 时约 $1.99\times10^{8}$ 次。
>
> 这个写法让两件事变成透明的。第一，"第 1 步选出的最大列排在最前时 $R$ 才上三角"，所以输出必须附带 permutation vector（置换向量）$p$：它记录的不是矩阵，而是数 $1,\dots,n$ 的一个重排，存 $n$ 个整数就够重建 $R$。存储置换与存储矩阵同样重要，这是 data structure（数据结构）决定接口的最小样本——$p$ 与 $R$ 合起来才是可用的分解结果，少记一位就连 $A$ 都拼不回去。
>
> 第二，先算完全部投影系数再统一减，是 classical Gram-Schmidt（经典格拉姆-施密特）；而"一产生新方向就立刻刷新所有剩余列"正是 modified Gram-Schmidt（修正格拉姆-施密特，常缩写 MGS）。两者在精确算术里完全等价，差别纯在 roundoff error（舍入误差）如何积累：经典做法一次减掉一长串投影，减法链越长，中间量越接近最终答案，catastrophic cancellation（灾难性抵消）越重；修正做法把减法摊到每一步，每一步减掉的量都与当时的结果同量级。`CSAPP` 第 2 章的结论在这里直接兑现：危险的不是减法本身，而是两个近似相等的量相减；换句话说，减法的次序决定了舍入的命运。
>
> 数字最诚实。取 Björck 1967 年用过的那个例子 $A=\begin{bmatrix}1&1&1\\ \varepsilon&0&0\\ 0&\varepsilon&0\\ 0&0&\varepsilon\end{bmatrix}$，双精度实测：$\varepsilon=10^{-8}$ 时经典做法给出 $\max|Q^{\top}Q-I|=0.5$，orthogonality（正交性）全丢；修正做法只给 $7.07\times10^{-9}$，相差 $7\times10^{7}$ 倍。$\varepsilon=10^{-4}$ 时对应 $2.26\times10^{-9}$ 与 $2.77\times10^{-13}$。两者的 $R$ 也只能说是近似相同（其中 condition number（条件数）分别约 $2.12\times10^{8}$ 与 $1.73\times10^{8}$），可见差别既在 $Q$ 也在 $R$，全部来自运算次序。
>
> 还有一个常被忽略的机制细节值得点出：既然剩余列已经被前面的方向剥过，它应当与 $q_j$ 正交，那么更新后的长度可以由旧长度按勾股关系直接算出，不必重扫整列——这就是"挑最大列不要额外代价"的真正来源。但这个"免费"是有毒的：当剩余列已经很短时，勾股式更新是两个相近量的相减，算出的长度可能为负，于是挑列的依据本身失真。所以工程实现里必须周期性重算范数，而不能无脑相信递推值。这条与上面"主元必须最大"是同一个道理的两面：主元小，说明这一列的信息已经只剩噪声。
>
> 算法层面还能看到 Householder（豪斯霍尔德）为什么更受欢迎：列主元 Gram-Schmidt 在每列上反复减投影，减法链长度正比于列数；Householder 用一次 reflection（反射）把整块下半部分清零，误差在 backward stable（向后稳定）意义下只有 $O(n\varepsilon)\|A\|$（后文 page_135 详述其构造）。史实：Businger 与 Golub 1965、Golub 1965（Numerische Mathematik 7:206–216）把这套做法定型；Björck 1967（BIT 7:1–21）给出 Gram-Schmidt 的完整舍入分析，并留下上面那个 $\varepsilon$ 例子；Björck 与 Paige 1992（SIAM Journal on Matrix Analysis and Applications 13:176–190）证明修正做法的正交性损失速度是可以精确预测的，而不是碰运气。

当循环结束时，我们得到 $Q$ 与 $R$，并且 $A = QR$。

这个 $R$ 是上三角矩阵的一个（含列重排的）版本。

只要第 1 步中挑出的最大列排在最前，$R$ 就会是上三角的。

实际输出可以是一个上三角矩阵再加上一个置换向量 $p$。

为重建 $R$，我们必须知道各列在置换后的顺序，也就是要记录下数 $1, \ldots, n$ 的置换情形。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 句 `This 月 is a e - 0f an upper …` 与 `wi 山 the numb ers 1 ，` 均只剩残片，分别按"带列重排的上三角 $R$"与"用数 $1,\ldots,n$ 记录列顺序"的语境补全。

实践中，这个带主元的 QR 算法再用 Householder（豪斯霍尔德）变换来配合，会安全得多。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 的 `by 0 0 刀 orm` 依术语表重建为 by Householder。

对于"用 Householder 矩阵的 QR"，也存在类似的列重排，用来减小舍入误差（roundoff error）。

你已经看到主元（pivoting）的要点了：好的列要排在最前面（good columns come first）。

<span style="color:#2471a3;">**[question]**</span> 提问（Question）：Gram-Schmidt 得到的 $Q$ 与 SVD 得到的 $U$ 都含有列空间 $C(A)$ 的一组标准正交基。

它们会是同一组基吗？

<span style="color:#2471a3;">**[answer]**</span> 回答（Answer）：不会，两者并不相同。

$U$ 的各列是 $AA^T$ 的特征向量（eigenvectors）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 的 `of T` 依 SVD 理论重建为 of $AA^T$：左奇异向量 $U$ 的列正是 $AA^T$ 的特征向量。

对于阶数大于 4 的矩阵，你无法在有限步精确算术（exact arithmetic）中求出其特征向量（或特征值）。

方程 $\det(A - \lambda I) = 0$ 将是 5 次或更高次的。

> <span style="color:#1e8449;">**[note] Note（译者注：特征值为何没有有限步精确算法，以及这条分界线如何决定数值线性代数的分工）:**</span> $Q\neq U$ 的论证是全书最深的结构性洞见之一：eigenvalue（特征值）与 eigenvector（特征向量）不存在"有限步精确算法"。原因链如下：$A$ 的特征值是 $\det(A-\lambda I)=0$ 的根，也就是一个 $n$ 次 polynomial（多项式）的根；Ruffini 1799 年给出不完整证明，Abel 1824 年自费印行的小册子《论代数方程，证明一般五次方程不可解》与 Galois 1832 年的工作共同说明，$n\ge5$ 时不存在只用四则运算与 radical（根式）的通用求根公式。这个障碍是结构性的，不是还没人想到。于是求特征值必然走无限 iteration（迭代）：page_123 的 shifted QR（移位 QR）是逼近，而不是"算到"。
>
> 但"有公式"与"算得准"是两件事，第二件更残酷，可以直接复算。Wilkinson 多项式的经典实验：$p(\lambda)=\prod_{k=1}^{20}(\lambda-k)$ 展开后 $\lambda^{19}$ 的系数是 $-210$。只把这个系数扰动 $10^{-10}$，二十个根里位移最大的一个就动了 $0.141$；扰动 $10^{-8}$，最大位移 $1.85$ 并出现 $\pm1.75$ 的虚部——本来是一族全实根，硬生生被逼成复共轭对；按 $-2^{-23}\times210$ 这个"机器精度量级"的扰动，最大位移 $5.84$。机理是一阶扰动公式 $\Delta\lambda\approx-\Delta p(\lambda)/p'(\lambda)$：在 $\lambda=16$ 处， $p'(16)=3.14\times10^{13}$，看着很大，可 $\Delta p$ 要按 $\lambda^{19}\approx7.56\times10^{22}$ 放大，量级估算 $\Delta\lambda\approx0.24$，与实测 $0.141$ 同阶。所以 $n\le4$ 那套公式也没用：公式只是一条被 condition number（条件数）放大的算术表达式，条件数才是命运。
>
> 补一条实分析视角，能解释为什么"存在性"与"可用性"会分裂。一元实分析（`Thomson` 等，Elementary Real Analysis）里能证：首一整系数多项式的根对系数连续依赖，教材里的路径是中值定理加紧性；但连续不等于稳定，位移的量级是 $\Delta c$ 除以 $|p'|$，而 $|p'|$ 可以任意小。顺带一提，这也解释了为什么所有求根软件都要附带一个 condition number（条件数）估计：它报出的不是误差，而是潜在误差的上界。这就是"代数上可达、数值上不可达"的分界线的正式版本：连续性只保证扰动小时根移动小，稳定的要求是移动量与扰动同阶，两者差一个条件数因子。
>
> 反观另一侧：Gram-Schmidt（格拉姆-施密特）与 Householder（豪斯霍尔德）只做 inner product（内积）、开方、除法，全是初等算术的有限组合，第 $j$ 列做完就再也不改，步数以 $n$ 为上限，必定停机。于是分工就清楚了：**能有限步做完的（正交三角化、约化到规范形）用 direct method（直接法）；不能的（谱）先化简再交给迭代法**。这正是 Part II 从 QR 走到 QR 迭代、再走向 Krylov 方法的内在逻辑。
>
> 还要看清一个容易混的点：SVD 的 left singular vector（左奇异向量）$U$ 的各列是 $AA^{\top}$ 的特征向量，所以 SVD 本身也逃不出这条路——能有限步拿到的是三角化（$A=U\Sigma V^{\top}$ 的结构），不是谱。理解"哪些量有限步可达"比记住任何单个算法都更能预测新算法的形态：它会告诉你为什么 QR 迭代每步还要再做一次 QR，为什么幂法只能给最大特征值，为什么所有"一步到位求特征值"的宣称都值得怀疑。

---

并不存在求五次方程（quintic）之根的公式，这正是阿贝尔定理（Abel）的内容。

Gram-Schmidt 只需要内积与平方根（square roots），因此 $Q$ 必然不同于 $U$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span> OCR 句 `0 nn can " for the 0 5 叻 degree eq …` 残缺，按五次方程无一般求根公式的数学事实重建。

在过去，算出一个足够精确的特征值所消耗的浮点运算（floating point operations），是消元或 Gram-Schmidt 的好几倍。

如今情形已经不同了。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.130</span>

---

<!-- page 135: 书页 131, OCR page 35 -->

### §II.2 Least Squares: Four Ways（最小二乘：四种方法）

#### Another Way to Q: Householder Reflections（求 Q 的另一途径：Householder 反射）

<span style="color:#2471a3;">**[note]**</span>
在不使用 column exchanges（列交换）时，Gram-Schmidt 过程需从每个向量中减去它沿已确定方向 $q_1,\dots,q_{k-1}$ 的各个分量。为保证 numerical stability（数值稳定性），这些减法必须一次一步地做。以 $q_3$ 为例：

```math
q_3=\frac{\,a-(q_1^{\top}a)\,q_1-(q_2^{\top}a)\,q_2\,}
{\big\|\,a-(q_1^{\top}a)\,q_1-(q_2^{\top}a)\,q_2\,\big\|}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR 将本节多处公式打成乱码（如 `q3 加 0 $ ara 沅…`、`（ ％ (l) ql`、`（ ％ (2) q2`），此处依 Gram-Schmidt 算法重建 $q_3$；式中的 $q_1^{\top}a$、$q_2^{\top}a$ 即 $a$ 在已定方向上的投影系数；前一句里的 `‰` 为省略号 $\dots$ 之误。

<span style="color:#2471a3;">**[note]**</span>
但即便如此，计算得到的 $q_3$ 仍不会与 $q_1$、$q_2$ 精确正交——这本身就很难办。要生成一个严格正交的 $Q$，好办法是像 Householder 那样把它一步"造"出来：

<span style="color:#2471a3;">**[definition]**</span>
**Householder reflection matrix（Householder 反射矩阵）**

```math
H=I-\frac{2uu^{\top}}{u^{\top}u}
\tag{15}
```

> <span style="color:#1e8449;">**[note] Note（译者注：Householder 反射的几何、符号规则的量化理由，以及"整体变换替代增量修正"）:**</span> 分解几何：$Hx=x-2\dfrac{u^{\top}x}{u^{\top}u}u$ 把 $x$ 沿 $u$ 的投影取两次，就是关于超平面 $u^{\perp}$ 的 reflection（反射）：垂直镜面的 $u$ 分量被反向，镜面内的分量原样保留。三个性质的来源一目了然：沿 $u$ 方向 $H$ 乘 $-1$，垂直方向乘 $+1$，所以 eigenvalue（特征值）为 $1$（重数 $n-1$）与 $-1$（重数 $1$）；因此 $H$ 是 symmetric（对称）且 orthogonal（正交）的，并且是 involutory（对合，$H^{2}=I$）的，式 (16) 只是把这个几何分解写成代数。从形式上看，$H$ 就是单位阵加上一个 rank-one（秩一）修正——正因为如此，它占 $O(n)$ 存储、作用一次只要 $O(n)$ 乘法，却能一次动到整个向量的所有分量。
>
> 实算核对把符号规则坐实。取 $a=(3,4)$：若 $u=a+5e_1=(8,4)$，则 $u^{\top}u=80$、$u^{\top}a=40$，$Ha=a-\frac{2\cdot40}{80}u=(-5,0)$，正是 $-\|a\|e_1$；若 $u=a-5e_1=(-2,4)$，则 $u^{\top}u=20$、$u^{\top}a=10$，$Ha=(5,0)=+\|a\|e_1$。两条分支在精确算术里都正确，可长度差一倍（$8.944$ 对 $4.472$），差别只在数值命运。
>
> 符号规则的全部意义在"不要自己吃掉自己"。取 $a=(1,10^{-8})$，双精度下 $\|a\|$ 算出来恰好是 $1$；若选 $-e_1$，得 $u=(0,10^{-8})$，长度只有 $10^{-8}$，而 $a$ 的舍入绝对误差是 $\varepsilon\|a\|\approx2.2\times10^{-16}$，这份绝对误差摊到长度 $10^{-8}$ 的 $u$ 上，就是 $2.2\times10^{-8}$ 的相对误差；若选 $+e_1$，得 $u=(2,10^{-8})$，长度 $2$，相对误差回到 $\varepsilon/2$ 量级。同一份数据、同一个数学对象，两条分支的相对误差差 $2\times10^{8}$ 倍。规则因此可以一句话记：让 $u=a\pm\|a\|e_1$ 里两项同号、绝对值相加（即取 $a_1$ 的符号），$\|u\|\approx\sqrt2\|a\|$ 就保证没有 cancellation（抵消）。这是 `CSAPP` 第 2 章"两个近似相等的量相减才危险"的直接应用。
>
> 为什么反射比逐步减法的 Gram-Schmidt（格拉姆-施密特）稳？经典做法在"新向量与已选方向几乎平行"时遭遇灾难性抵消，误差随列数一层层累积；反射用一次全局变换把整列映到坐标轴上，没有逐列累积的减法链。但要修正一个常见过头说法：并非"误差只来自存储 $u$ 时的舍入"。准确的说法是 backward stable（向后稳定）：算出的 $\hat{Q}$、$\hat{R}$ 是某个 $A+\Delta A$ 的精确 QR 因子，$\|\Delta A\|\le cn\varepsilon\|A\|$，$c$ 只随 $n$ 缓慢增长；而前向误差（解本身的误差）还要再乘一次 $\kappa(A)$——稳定性消掉的是算法自造的放大，不是 $A$ 本身的病态。这个区分是判断"算法好坏"与"问题好坏"的分水岭。
>
> 跨课程连接有两处正好咬合。Strang 18.06（线性代数）里 QR 通常由 Gram-Schmidt 引入，Householder 只作为一句话的备注，但工程实现反过来：LAPACK 的 `geqrf` 用的是反射而不是 Gram-Schmidt，因为反射的稳定常数与列数几乎无关。同属 orthogonal（正交）变换的还有 Givens rotation（吉文斯旋转），它一次只清零一个元素，清掉一列下三角要 $O(n)$ 次旋转；reflection（反射）一次清零整块，$n-1$ 次就够。两者都是正交矩阵，差别在"一次动多少"——Givens 只碰两行，适合 sparse matrix（稀疏矩阵）与并行，reflection 碰整列，适合 dense（稠密）情形。这个取舍本身就是在回答"把矩阵当整体还是一堆元素"。实分析（`Thomson` 等）那边则提供结构语言：反射是 isometry（等距），保长度与内积，$H^{\top}H=I$ 只是这个几何事实的代数影子；而 $H_1,\dots,H_{n-1}$ 依相反次序相乘给出 $Q^{\top}$，说明"$n-1$ 个镜面就能把一个矩阵旋成三角形"，这比"逐列投影像素"的图景干净得多。

<span style="color:#2471a3;">**[note]**</span>
其中 $u$ 为所取的向量（OCR 噪声 `刀@日` 实为 $uu^{\top}/u^{\top}u$ 之误）。于是 $H^{\top}H=I$，即 $H$ 既 symmetric（对称）又 orthogonal（正交）：

```math
H^{\top}H=\Big(I-\frac{2uu^{\top}}{u^{\top}u}\Big)^{\!2}=I
\tag{16}
```

<span style="color:#2471a3;">**[note]**</span>
关键点：若取 $u=a-\|a\|e_1$ 或 $u=a+\|a\|e_1$，则分别有 $Ha=-\|a\|e_1$ 或 $Ha=+\|a\|e_1$（符号选定见 Problem 6），即反射把列向量 $a$ 映到第一条坐标轴上。要在某列主对角线下方制造 zero（零），把该列记为 $a=\begin{pmatrix}a_{\rm upper}\\ a_{\rm lower}\end{pmatrix}$，其中上块 $a_{\rm upper}$ 已经属于 $R$、保持不动；只对下块 $a_{\rm lower}$ 构造反射，且 $u$ 的符号有选择的自由。式 (17) 记录了这一作用：选 $u=a_{\rm lower}\pm\|a_{\rm lower}\|e_1$，则 $H_k a_{\rm lower}=\mp\|a_{\rm lower}\|e_1$，该列除主对角元 $\mp\|a_{\rm lower}\|$ 外下方全部归零——我们正在 $HA$ 中制造零：

```math
H_k:\quad u=a_{\rm lower}\pm\|a_{\rm lower}\|e_1 ,\qquad
H_k a_{\rm lower}=\mp\|a_{\rm lower}\|e_1 ,
\qquad\text{下方变为 }0 .
\tag{17}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR 碎片 `鬱 = 一 俨`、`士 《 1010wer`、`丆 一 2 “ T`、`Olower 一 zeros` 严重受损，按 Householder 消去主对角线下元素的构造重建 (17)：`aupper`/`alower` 即上下两块，`士` 为 $\pm$（符号任选），`Olower → zeros` 即下部被消成零。

<span style="color:#2471a3;">**[note]**</span>
设原始矩阵为 $A_1=A$：第一步产生 $H_1$，下一步得到 $H_2(H_1A_1)$。沿各列逐步推进，反射 $H_1,\dots,H_{n-1}$ 依相反次序相乘给出 $Q^{\top}$；这些反射一路制造主对角线下方的零，最终把 $A$ 化为三角矩阵 $R$：

```math
Q^{\top}A = R
\tag{18}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR `1 is the original matnx` 即 $A_1$ 为原始矩阵；`becomes QTA = R` 即式 (18)。

<span style="color:#2471a3;">**[note]**</span>
关键在于记录各 $H_j$ 时只存向量、不存矩阵：仅储存各 $u_j$，那么每个 $H_j=I-2u_ju_j^{\top}/(u_j^{\top}u_j)$ 都精确正交。用最小二乘解 $A\backslash b$ 时，可像消元法那样从增广矩阵 $[A\ b]$（OCR 噪声 `matnx b]` 之误）出发：依次乘以全部 $H_j$ 便得到 $[R\ Q^{\top}b]$；再用普通 back substitution（回代法）解三角系统 $Rx=Q^{\top}b$。这样求得的最小二乘解即为

> <span style="color:#1e8449;">**[note] Note（译者注：只存 $u_j$ 不存 $H_j$ 省下多少，以及把 $b$ 并进增广矩阵为何是一趟流式处理）:**</span> Householder（豪斯霍尔德）的工程实现有两处精打细算，两处都值得算一算。其一，只存 $u_j$ 不存 $H_j$：一个 $n\times n$ 的 reflection（反射）矩阵要占 $O(n^{2})$ 存储，而它的全部信息就在一个 $n$ 维向量 $u$ 里（$H=I-2uu^{\top}/u^{\top}u$），因此每步只需 $O(n)$ 额外存储，整个 QR 的 $Q$ 因子可以用 $n$ 个向量的 compact form（紧凑形式）存放，LAPACK 的 `geqrf` 正是如此：它把第 $j$ 个反射向量写进 $A$ 被清零的下三角区，另外返回一个长度 $n$ 的数组存缩放因子。
>
> 把数字摆出来就知这道算术有多划算。取 $m=10^{4}$、$n=10^{2}$：$A$ 本身是 $10^{6}$ 个双精度数，$8$ MB；显式造出 $Q$ 要 $10^{8}$ 个数，$800$ MB，恰好是 $m/n=100$ 倍；而紧凑形式额外只要 $n=100$ 个数（$800$ 字节）。运算上的差距更大：QR 分解本身约 $2mn^{2}-2n^{3}/3\approx1.99\times10^{8}$ 次 flop（浮点运算），而"先造出 $Q$ 再算 $Q^{\top}b$"要 $2m^{2}n=2\times10^{10}$ 次，差 $10^{4}$ 倍。
>
> 为什么存储是"免费"的，这一点最容易被当成巧合，其实它是设计的结果：反射的作用正是把某一列主对角线以下清零，那些位置本来就要变成零，于是正好拿来存向量——被丢弃的信息位与被需要的信息位刚好一样多，这不是压缩，而是复用。这个思路推到多列就成了 compact WY representation（紧凑 WY 表示）：把 $k$ 个反射打包成 $Q=I+WY^{\top}$，$W$、$Y$ 都是 $m\times k$，于是 $k$ 个小反射的作用可以合并成几次大矩阵乘，落进 Level-3 BLAS 的 `dgemm`。这一步是把算法从"访存受限"推向"计算受限"的关键，`CSAPP`（深入理解计算机系统）第 6 章讲的 cache locality（缓存局部性）在这里被用到了极致：一次读进 cache line 的数据要被反复用，而不是每读一次只做一次向量运算。
>
> 其二，把 $b$ 并入 augmented matrix（增广矩阵）$[A\ b]$ 一起左乘全部 $H_j$：$A$ 被三角化成 $R$ 的同时，$b$ 被同步变换成 $Q^{\top}b$，一步到位得到 $[R\ Q^{\top}b]$，避免了"先算完整 $Q$ 再乘 $b$"的双倍运算，最后只需 back substitution（回代）解三角系统 $Rx=Q^{\top}b$。用 `6.006`（算法导论课）的语汇说：这是把"两趟访问同一批数据"合并成"一趟 streaming（流式）处理"，代价是必须保证每个 $H_j$ 一旦可用就立刻作用于 $b$，而不能等全部反射造完。
>
> 还有一处机制细节值得点明：反射必须按 $H_1,H_2,\dots$ 的次序乘，不能随意调换。因为 $H_j$ 只在第 $j$ 行以下起作用，并且假定前 $j-1$ 列已经是三角形；次序一乱，它清掉的位置会被后一个反射重新填满。这与消元里"主元必须按列推进"是同一条纪律。工程上常被问：为什么矩阵的 backslash（右除）算子能与先 `qr` 再回代给出同一个解？因为它走的就是增广这一趟，算完 $Q^{\top}b$ 就把 $Q$ 丢掉，从不显式持有。
>
> 最后是收益的实质：最小二乘解 $\hat{x}=R^{-1}Q^{\top}b$ 全程 $A^{\top}A$ 从未被构造。这不是美学偏好，而是把 condition number（条件数）从 $\kappa(A)^{2}$ 换回 $\kappa(A)$——量级上等于白捡一半的有效位数。代价是必须接受"$Q$ 只是紧凑形式、需要时才展开"这一约定，也就是承认数据的表示方式本身就是算法的一部分。

---

```math
x=(QR)^{-1}Q^{\top}b=R^{-1}Q^{\top}b .
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR 尾段 `solve = b`、`= 一 1 QTbe` 为乱码，依 $A=QR$、$Q^{\top}Q=I$ 重建为 least squares solution（最小二乘解）$x=R^{-1}Q^{\top}b$。

<span style="color:#2471a3;">**[example]**</span>
**Example**：取 $a=\begin{pmatrix}3\\4\end{pmatrix}$，则 $\|a\|=5$。选择符号 $u=a+\|a\|e_1=\begin{pmatrix}8\\4\end{pmatrix}$，于是 $u^{\top}u=80$，反射矩阵

```math
H=I-\frac{2uu^{\top}}{u^{\top}u}
=\frac{1}{5}\begin{pmatrix}-3&-4\\-4&3\end{pmatrix} ,
```

它把 $a$ 反射到 $e_1$ 的反方向：$Ha=\begin{pmatrix}-5\\0\end{pmatrix}=-\|a\|e_1$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
例中 OCR 数值碎片 `3 3 4 3 and 5` 与矩阵 $\frac15\begin{pmatrix}-3&-4\\-4&3\end{pmatrix}$ 中的三个 3、两个 4 及分母 5 吻合；`0 1`、`HA` 与结果 $(-5,0)^{\top}$ 相符，据此重建本例。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.131</span>

---

<!-- page 136: 书页 132, OCR page 36 -->

#### Least Squares with a Penalty Term（带惩罚项的最小二乘）

<span style="color:#2471a3;">**[note]**</span>
若矩阵 $A$ 有 dependent columns（相关列），且 $Ax=0$ 存在非零解，则 $A^{\top}A$ 不可能可逆——这正是需要 $\delta$ 之处。一种温和的处理将"正则化"最小二乘：

<span style="color:#2471a3;">**[definition]**</span>
**Penalty term（惩罚项）**：极小化残差平方加惩罚平方项：

> <span style="color:#1e8449;">**[note] Note（译者注：岭回归的谱滤波器——从 $1/\sigma$ 到 $\sigma/(\sigma^{2}+\delta^{2})$，并改正一处旧说法）:**</span> 这就是统计学与机器学习里的 ridge regression（岭回归），也是 Boyd 的 convex optimization（凸优化）教材 §6.3 的 regularized least squares（正则化最小二乘）。它和前面学过的无约束最小二乘只差一个 $\delta^{2}I$：$A^{\top}A$ 奇异或近奇异时（相关列、欠定、病态），$A^{\top}A+\delta^{2}I$ 的每个 eigenvalue（特征值）都被抬高至少 $\delta^{2}$，全部为正，于是 positive definite（正定）可逆——与 page_118 情形 5 的补救遥相呼应。目标函数 $\|Ax-b\|_{2}^{2}+\delta^{2}\|x\|_{2}^{2}$ 求导得到 normal equation（正规方程）$(A^{\top}A+\delta^{2}I)x=A^{\top}b$，形式与普通最小二乘一模一样，只是矩阵换了。
>
> 这里必须改正旧注的一处技术错误：旧注说"小 $\sigma$ 方向被压到约 $1/\delta^{2}$ 的温和放大"。滤波器是 $f(\sigma)=\sigma/(\sigma^{2}+\delta^{2})$，它在 $\sigma\to0$ 时趋于 $0$，绝不是在 $1/\delta^{2}$ 处停住；它的最大值在 $\sigma=\delta$ 处取到，值恰为 $1/(2\delta)$，所以"放大"的上界是 $1/(2\delta)$，与 $1/\delta^{2}$ 差两个数量级。相对未正则化的 $1/\sigma$ 而言，小方向是被压缩了 $\sigma^{2}/(\sigma^{2}+\delta^{2})$ 倍，方向搞反了。取 $\delta=10^{-2}$、$\sigma=(1,10^{-3})$ 实算：滤波器给出 $(0.9999,9.90)$，未正则化是 $(1,1000)$，两者的比值是 $(0.9999,0.0099)$；上界 $1/(2\delta)=50$，而 $1/\delta^{2}=10^{4}$，差两个数量级。这个修正很重要，因为它决定了 $\delta$ 该怎么选：想让某个尺度被压住，$\delta$ 要选得比那个 singular value（奇异值）大一个量级，而不是"$\delta$ 越小越安全"。
>
> 统计视角依然成立：$\delta^{2}\|x\|^{2}$ 产生 shrinkage（收缩）效果，把解拉向零，付一点 bias（偏差）换 variance（方差）的大幅下降，`Bertsekas` 的 Introduction to Probability（概率论教材）里 $MSE=(\text{bias})^{2}+\text{variance}$ 的分解在此精确上演，$\delta$ 就是你在两者之间拨的旋钮。这个思想在统计界的原始出处是 Hoerl 与 Kennard 1970 年发表于 Technometrics 12(1):55–67 的《Ridge Regression: Biased Estimation for Nonorthogonal Problems》，标题里的 biased（有偏）是关键——它从一开始就不假装自己是无偏估计。
>
> 还有一个"为什么是这个形式"的要点：惩罚项必须写成 $\delta^{2}\|x\|^{2}$ 而不是 $\delta\|x\|^{2}$。原因是 $A^{\top}A$ 已经在"平方"的量纲上（它的元素是内积），要抬高它的谱，加的项必须与它同量纲，于是目标里出现的系数就是 $\delta^{2}$；若目标写 $\delta\|x\|^{2}$，解里出现的就是 $\delta$ 而非 $\delta^{2}$，"$\delta$ 与奇异值同量纲"这句直觉就断了。收益也可以定量：$\sigma_{\max}=1$、$\sigma_{\min}=10^{-3}$ 时 $\kappa(A^{\top}A)=10^{6}$，加 $\delta=10^{-2}$ 后 $(1+10^{-4})/(10^{-6}+10^{-4})\approx9902$，条件数降了两个数量级，直接回报约两位有效数字。
>
> 还有一个把 ridge 化归为普通最小二乘的等价变形，值得记住：把 $A$ 竖着加高成 $\tilde{A}=\begin{bmatrix}A\\ \delta I\end{bmatrix}$、$b$ 补零成 $\tilde{b}=\begin{bmatrix}b\\ 0\end{bmatrix}$，则 $\|Ax-b\|^{2}+\delta^{2}\|x\|^{2}$ 恰好等于 $\|\tilde{A}x-\tilde{b}\|^{2}$，正规方程两边正是 $(A^{\top}A+\delta^{2}I)x=A^{\top}b$。于是岭回归不需要单独的 solver（求解器）：套用现成的 QR 或 Householder（豪斯霍尔德）程序即可，这也是它被称为"最小二乘的第四种方法"而不是"另一个问题"的理由。
>
> 最后是两条主线的并轨。正文预告 $\delta\to0$ 时解收敛到 minimum norm（最小范数）解 $A^{+}b$（下一注给证明），而 §III.4 描述另一种惩罚：改加 $\ell_{1}$ 范数 $\|x\|_{1}$。二者的差别是几何的：$\ell_{2}$ 惩罚把解往原点拉成"最短"，$\ell_{1}$ 惩罚的等值面有尖角，最优解会落在坐标轴上，于是得到 sparse（稀疏）解。同一句"加惩罚"，换一个范数就换了一种解的结构：惩罚项选定了范数，范数选定了几何，几何决定了稀疏性。这是本书正则化主题最值得记住的一句话。

```math
\min_{x}\;\|Ax-b\|_{2}^{2}+\delta^{2}\|x\|_{2}^{2} ,
\qquad
\text{Solve } (A^{\top}A+\delta^{2}I)\,x=A^{\top}b .
\tag{19}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR `》 囝 一 b 日 2 + |@ 2`、`SoIve （ + ö21) = AT b` 严重损坏，依式 (19) 重建：目标为 $\|Ax-b\|_2^2+\delta^2\|x\|_2^2$，其 normal equations（正规方程）即 $(A^{\top}A+\delta^{2}I)x=A^{\top}b$；$\delta$（OCR `ö`）即 penalty parameter（惩罚参数）。

<span style="color:#2471a3;">**[note]**</span>
这种处理最小二乘的第四种方法称为 ridge regression（岭回归）。我们将证明：当惩罚消失（$\delta\to 0$）时，其解逼近最短解 $A^{+}b$。§III.4 描述的是另一种惩罚：改为加上 $\ell_1$ 范数 $\|x\|_1$。它给出漂亮的结果：取代带 minimum norm（最小范数）的伪逆解，$\ell_1$ 惩罚的解是 sparse（稀疏）的。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR `五 e g ”` 实为 ridge（岭）；`111.4` 依本书章节编号修正为 §III.4；`norm ds sparse` 修正为 norm is sparse，并按上下文补全 $\ell_1$ 记号。

<span style="color:#2471a3;">**[theorem]**</span>
**伪逆 $A^{+}$ 即极限**：pseudoinverse（伪逆）$A^{+}$ 正是 $(A^{\top}A+\delta^{2}I)^{-1}A^{\top}$ 当 $\delta\to 0$ 时的极限。

<span style="color:#2471a3;">**[proof]**</span>
式 (19) 从正定矩阵 $A^{\top}A+\delta^{2}I$ 造出伪逆 $A^{+}$——这些矩阵直到最后 $\delta=0$ 那一瞬都是可逆的；就在那一瞬 $A^{+}$ 发生突变。取 $A$ 为 1×1 矩阵（即单个 singular value（奇异值）$\sigma$）看得最清楚：设 $A=[\sigma]$（$\sigma>0$），则

```math
(A^{\top}A+\delta^{2}I)^{-1}A^{\top}
=\Big[\frac{\sigma}{\sigma^{2}+\delta^{2}}\Big] .
```

让 $\delta\to 0$：若 $\sigma=0$ 极限为零；若 $\sigma>0$ 极限为 $1/\sigma$。这恰好就是 $A^{+}$：零或 $1/\sigma$，取决于 $\sigma$ 是否为 0。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR 碎片 `is 1 by 1 Now let --+ 0`、`This is exactly 蓋 + = zero or 一`、`The limi t is zero if 伊 = 0` 按 1×1 情形重建：$A=[\sigma]$ 的伪逆在 $\sigma>0$ 时为 $[1/\sigma]$，在 $\sigma=0$ 时为零。

<span style="color:#2471a3;">**[proof]**</span>
再看一般的 diagonal matrix（对角矩阵）：这很容易，因为所有矩阵始终是对角的。我们只是在主对角线的每个位置重演 1×1 情形：$\Sigma$ 有正元素 $\sigma_i$、其余全零；惩罚使整条对角线都变正——$(\Sigma^{\top}\Sigma+\delta^{2}I)^{-1}\Sigma^{\top}$ 的对角元为 $\sigma_i/(\sigma_i^2+\delta^2)$，其余为零：

```math
(\Sigma^{\top}\Sigma+\delta^{2}I)^{-1}\Sigma^{\top}
=\operatorname{diag}\!\Big(\frac{\sigma_i}{\sigma_i^2+\delta^2}\Big) .
```

正数趋近 $1/\sigma_i$，零保持为零。当 $\delta\to 0$ 时极限再次是 $\Sigma^{+}$。

<span style="color:#2471a3;">**[proof]**</span>
为证明对任意矩阵极限都是 $A^{+}$，引入 SVD（奇异值分解）：$A=U\Sigma V^{\top}$，并把它代入 $(A^{\top}A+\delta^{2}I)^{-1}A^{\top}$。正交矩阵 $U$、$V$ 会"让路"靠边，因为 $U^{\top}=U^{-1}$、$V^{\top}=V^{-1}$：

> <span style="color:#1e8449;">**[note] Note（译者注：先标量、再对角、最后 SVD——一个可以背下来的证明模板，以及它的实分析含义）:**</span> 本页定理的证明结构是一个应该背下来的三段式模板：**先证 $1\times1$（scalar，标量）→ 再推广到 diagonal matrix（对角矩阵）→ 最后用 SVD（奇异值分解）归约到一般矩阵**。第一段 $A=[\sigma]$ 时 $\sigma/(\sigma^{2}+\delta^{2})$ 在 $\sigma>0$ 趋于 $1/\sigma$、在 $\sigma=0$ 恒为 $0$，把"极限等于伪逆"缩成一个微积分习题；第二段利用对角矩阵各坐标互不耦合，把标量结论逐坐标重放（$\mathrm{diag}(\sigma_i/(\sigma_i^{2}+\delta^{2}))$）；第三段代入 $A=U\Sigma V^{\top}$，靠 $U^{\top}U=I$、$V^{\top}V=I$ 让两个 orthogonal matrix（正交矩阵）"让路靠边"，page_130 的注已经演练过同一动作，把任意 $A$ 的表达式化成第二段的对角形式。三段合起来其实只是一句宣言：把任意矩阵化到对角，剩下的就是把标量结论搬运过去。
>
> 第三段真正用到的只有一条引理，值得单独记：orthogonal（正交）变换不改变 singular value（奇异值），也不改变 2-norm（2-范数），因为它保内积。有了这条，$\|F(A)-A^{+}\|\to0$ 对一般 $A$ 的证明就是"两边同乘正交矩阵、化到 $\Sigma$"这一步，剩下的全是第二段。这也是为什么本书反复用这个套路：SVD 把所有矩阵问题还原成对角矩阵问题，而对角矩阵只是若干标量的并排。所以真正被证明的从来只有 $1\times1$ 那一行，其余都是搬运。
>
> 本页真正惊艳之处在于：极限在 $\delta=0$ 处发生突变，pseudoinverse（伪逆）作为 $A$ 的函数是 discontinuous（不连续）的。这件事可以定量。取 $A_0=\mathrm{diag}(1,0)$ 与 $A_\varepsilon=\mathrm{diag}(1,\varepsilon)$：两者相差 $\|A_\varepsilon-A_0\|=\varepsilon$，而它们的伪逆相差 $\|A_\varepsilon^{+}-A_0^{+}\|=1/\varepsilon$，比值恰好 $1/\varepsilon^{2}$。实测 $\varepsilon=10^{-8}$ 时矩阵只差 $10^{-8}$，伪逆却差 $10^{8}$；$\varepsilon=10^{-4}$ 时矩阵差 $10^{-4}$、伪逆差 $10^{4}$。所谓"不连续"不是形容词，它是一个具体的放大率。
>
> 换成实分析的语言，这套结论就是 uniform convergence（一致收敛）的失败。把滤波器看成函数族 $f_\delta(\sigma)=\sigma/(\sigma^{2}+\delta^{2})$，逐点极限是 $\sigma>0$ 时的 $1/\sigma$、$\sigma=0$ 时的 $0$；在 $[\sigma_0,\infty)$ 上误差不超过 $\delta^{2}/\sigma_0^{3}$，所以一致收敛；越靠近零越糟，$\sigma_0=10^{-3}$、$\delta=10^{-2}$ 时这个界是 $10^{5}$，毫无用处。`Thomson` 等《Elementary Real Analysis》里"极限函数不连续则收敛必不一致"的定理，在这里给出了它的具体数值形态。换句话说，$\delta$ 是人为给的信任尺度，它必须显式出现，否则算法就在噪声里替你做这个选择。也正因如此，"$\lim$"与"求逆"这两个动作不能交换：$\lim_{\delta\to0}(A^{\top}A+\delta^{2}I)^{-1}$ 存在，但 $(\lim_{\delta\to0}(A^{\top}A+\delta^{2}I))^{-1}$ 根本不存在。定理的全部内容就是这一句。
>
> 顺带说清这个模板的适用边界：它依赖"矩阵可以通过正交变换对角化"，而正交对角化只对 normal matrix（正规矩阵，含对称、正交、对角）成立；对一般方阵要用 Schur 三角化，第三段就只能化到上三角而不是对角，结论也随之带上三角部分的常数。这解释了为什么同一个模板在 SVD 与谱分解下能用、在 Jordan 形下就失效——**能不能把问题压成一堆标量，取决于你能把矩阵化到多简单的规范形**。搞清这一点，就不会再把"化到规范形"当成准备动作：它本身就是全部的数学内容，剩下的只是搬运。这句话是本书后半所有算法的统一视角。

---

```math
A^{\top}A+\delta^{2}I
= V\Sigma^{\top}U^{\top}U\Sigma V^{\top}+\delta^{2}I
= V(\Sigma^{\top}\Sigma+\delta^{2}I)V^{\top} ,
```

```math
(A^{\top}A+\delta^{2}I)^{-1}A^{\top}
= V(\Sigma^{\top}\Sigma+\delta^{2}I)^{-1}V^{\top}V\Sigma^{\top}U^{\top}
= V\big[(\Sigma^{\top}\Sigma+\delta^{2}I)^{-1}\Sigma^{\top}\big]U^{\top} .
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR `= VETuTu»vT + 硭 /`、`V(ETE + ö21)¯1vTVETuT` 中 `E`、`»`、`硭` 均为噪声，已重建为 $\Sigma^{\top}U^{\top}U\Sigma$、$V(\Sigma^{\top}\Sigma+\delta^{2}I)V^{\top}$ 及 $V(\cdot)U^{\top}$，其中用到 $U^{\top}U=I$、$V^{\top}V=I$。

<span style="color:#2471a3;">**[proof]**</span>
现在轮到 $\delta\to 0$：矩阵 $V$ 与 $U^{\top}$ 原地不动，方括号中的对角矩阵趋近 $\Sigma^{+}$——这正是上面已建立的对角情形。因此 $(A^{\top}A+\delta^{2}I)^{-1}A^{\top}$ 的极限就是我们的伪逆 $A^{+}$：

```math
\lim_{\delta\to0} V\big[(\Sigma^{\top}\Sigma+\delta^{2}I)^{-1}\Sigma^{\top}\big]U^{\top}
= V\Sigma^{+}U^{\top}
= A^{+} .
\tag{20}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）：**</span>
OCR 末段 `V [ （ 习 T 习 + 硭 I ） 一 1 习 T ] UT = VE+uT = 蓋 +` 重建为式 (20)；其中 $\Sigma^{+}$ 为把非零奇异值取倒数、零保持零的对角矩阵。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.132</span>

---

<!-- page 137: 书页 133, OCR page 37 -->

<!-- 结构清单：节页眉 2 · Four Ways；正文段（计算 Sigma^+ 的困难 / Sigma^+ 对角元与不连续性 / 小矩阵示例）；伪逆规则段（(AB)^+ 不等于 B^+A^+，两条成立规则）；示例 A=[1 0]、B=[1;1]；(CR)^+ = R^+C^+ 及其意义；A=CR 推理（C、R 给出基、左逆与右逆、A^+=R^+C^+）；舍入误差与秩突降、0^+=0；(BA)^+ 验证；Moore-Penrose 逆与 pinv(A)。 -->

### 2. Four Ways（四种方法）

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 页眉 OCR 为“2 、 忪 t · FO u r Ways”，其中“忪 t”字形损坏不可辨识；结合本页伪逆与奇异值触及零的内容及书页 133 位于 §II.2（Least Squares: Four Ways）的事实，重建为本节页眉“2 · Four Ways”。

计算 $\Sigma^+$ 的困难在于判断某个奇异值（singular value）到底是零，还是仅仅非常小。

> <span style="color:#1e8449;">**[note] Note（译者注：$1/\sigma$ 的断崖如何让"秩"变成不可判定的量，以及 $(AB)^{+}\neq B^{+}A^{+}$ 的机理）:**</span> 这句话点破了 pseudoinverse（伪逆）在数值层面的真正痛点。函数 $\sigma\mapsto1/\sigma$ 在 $\sigma=0$ 处有断崖：$\sigma$ 从 $10^{-8}$ 变到 $0$，$1/\sigma$ 从 $10^{8}$ 骤变为 $0$，所以伪逆不是 $\Sigma$（或 $V$）的连续函数，微小的数据扰动（哪怕只是 `CSAPP`（深入理解计算机系统）第 2 章讲的舍入误差）就能在"视为零"与"不视为零"之间横跳，让 $A^{+}$ 面目全非。机器无法从数值上区分"精确的零"与"极小的非零"：双精度下 $10^{-8}$ 完全可以表示，但它对应的 $1/\sigma=10^{8}$ 会把任何误差放大 $10^{8}$ 倍，答案毫无意义。
>
> 工业界的解法是 threshold truncation（阈值截断）：MATLAB 的 `pinv` 默认把小于 $\mathrm{tol}=\max(m,n)\cdot\varepsilon\cdot\sigma_{\max}$ 的 singular value（奇异值）当作零（$\varepsilon\approx2.22\times10^{-16}$）。代入具体数：$1000\times1000$ 且 $\sigma_{\max}=1$ 时 $\mathrm{tol}=2.22\times10^{-13}$，于是 $\sigma=10^{-13}$ 与 $10^{-14}$ 一律按零处理；而 NumPy 的 `pinv` 默认判据是 $10^{-15}$，同样的矩阵它会给出 $10^{13}$ 与 $10^{14}$ 这两个荒唐的放大。同一个矩阵、两台工具、两个 rank（秩）——这不是谁的 bug，而是说 rank 在浮点世界里本来就需要一个 tolerance（容差）参数来定义，而参数的选取是人为约定。这与 page_136 的 $\delta^{2}$ 正则化形成对照：正则化把 $1/\sigma$ 换成 $\sigma/(\sigma^{2}+\delta^{2})$，处处连续；截断则是在不连续点上直接抽刀。前者换问题，后者换答案。所以报告伪逆时必须同时报告所用的 tol：只给 $A^{+}$ 不给 tol 的代码，结果根本不可复现。
>
> 为什么 $(AB)^{+}\neq B^{+}A^{+}$？根源是 rank 在乘法中只会下降：$\mathrm{rank}(AB)\le\min(\mathrm{rank}\,A,\mathrm{rank}\,B)$，乘积可能把某些方向压平，而信息一旦丢失就无法恢复，伪逆只能"反演没丢的部分"。反例实算：$A=[1\ \ 0]$、$B=\binom{1}{1}$，则 $AB=[1]$、$(AB)^{+}=[1]$，而 $A^{+}=\binom{1}{0}$、$B^{+}=[\tfrac12\ \ \tfrac12]$，$B^{+}A^{+}=[\tfrac12]$，确实 $1/2\neq1$。机理是两条路径各丢一次信息：$A$ 丢掉第二坐标，$B$ 把标量嵌进"$+1$"方向，两次投影的复合并不等于把两者都丢掉之后的反演。可逆矩阵之所以能写成 $(AB)^{-1}=B^{-1}A^{-1}$，正因为那时一次信息都不丢。
>
> 但确有两条规则成立：$(A^{\top})^{+}=(A^{+})^{\top}$ 与 $(A^{\top}A)^{+}=A^{+}(A^{\top})^{+}$。后者可直接代入验证：把 $A=U\Sigma V^{\top}$ 代进两边，都得到 $V\Sigma^{+}(\Sigma^{+})^{\top}V^{\top}=V\mathrm{diag}(1/\sigma_i^{2})V^{\top}$，与 $\Sigma$ 的零位置保持一致。更一般地，若 $A=CR$ 且 $C$ 是 full column rank（满列秩）、$R$ 是 full row rank（满行秩），则 $(CR)^{+}=R^{+}C^{+}$ 成立，因为此时 $C^{+}C=I_r$、$RR^{+}=I_r$，两条路径都不丢信息。数值核对取 $6\times2$ 的 $C$ 与 $2\times5$ 的 $R$：$\|(CR)^{+}-R^{+}C^{+}\|=1.9\times10^{-16}$，而 $\|C^{+}C-I\|=4.2\times10^{-16}$、$\|RR^{+}-I\|=2.9\times10^{-16}$，正是满秩保证了这两个等式。
>
> 于是正文那句"任意矩阵的伪逆都能在不知其 SVD、也不必计算任何特征值的情况下算出来"就有了解读：$C$ 取 column space（列空间）的一组基、$R$ 取 row space（行空间）的坐标，任意秩 $r$ 的矩阵都能这样拆（这正是 §I.1 第 4 页那个分解），剩下的全是 $(CR)^{+}=R^{+}C^{+}$ 加两次满秩逆。但要注意前提："确知秩是 $r$"。结合前面两段，精确的 rank 恰恰是浮点下最不可知的东西，这就是这条漂亮公式的软肋。Moore 与 Penrose 在 1920 与 1955 年给出的四条公理化定义之所以重要，也在于它绕开了"怎么算"，只规定"必须满足什么"——而实现它时，代价总是落在 rank 的判断上。实务上的出路不是纠结精确 rank，而是接受"数值秩加正则化"这套组合，让答案对阈值不敏感——这也是本书把惩罚项、随机化、阈值三种手段摆在一起讲的真正原因。

而 $\Sigma^+$ 的对角元要么是零、要么极大！$\Sigma^+$ 与 $A^+$ 都远不是 $\Sigma$ 与 $V$ 的连续函数（continuous function）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原句 OCR 为“+ and + are far from being continuous functions of 乥 and 。”，两个“+”与两个自变量符号在扫描中残缺，此处依上下文重建为“$\Sigma^+$ 与 $A^+$”及“$\Sigma$ 与 $V$”。

而 $\Sigma^+$ 的价值在于发出警示：当某个 $\sigma$ 已非常接近零时——这时我们往往在并不确知的情况下就把它当作零处理。

这里给出一些小矩阵及其伪逆（pseudoinverse），以便把下面的要点落到实处：$\Sigma^+$ 并不遵循 $\Sigma^{-1}$ 的全部规则，它在奇异值触及零的那一刻是不连续的（discontinuous）。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原句“lt is 仞 1 叻 tuo”系乱码，依语境重建为“it is discontinuous”（它是不连续的）。

```math
\Sigma = \begin{bmatrix} 1/2 & 0 \\ 0 & 1/10 \end{bmatrix}
\quad\longrightarrow\quad
\Sigma^+ = \begin{bmatrix} 2 & 0 \\ 0 & 10 \end{bmatrix}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此示例矩阵在 OCR 中被彻底打散（仅残留 1/2、2、1/10、10、0 等碎片），此处按“$\sigma \mapsto 1/\sigma$、$0 \mapsto 0$”的规则重建，具体数值未必与原书逐字一致。

并不是总有 $(AB)^+ = B^+A^+$ 成立。伪逆并不服从逆矩阵（inverse matrix）的全部规则！但确有两条规则成立：$(A^T)^+ = (A^+)^T$ 与 $(A^TA)^+ = A^+(A^T)^+$。

> <span style="color:#1e8449;">**[note] Note（译者注：伪逆与乘积次序——为什么 $(AB)^{+}$ 不等于 $B^{+}A^{+}$）:**</span> 这条注要回答一个看似琐碎、实则定调的问题：为什么 invertible matrix（可逆矩阵）的规则 $(AB)^{-1}=B^{-1}A^{-1}$ 一到 pseudoinverse（伪逆）就失效？根源一句话就能锁死——rank（秩）在乘法中只会下降：$\mathrm{rank}(AB)\le\min(\mathrm{rank}A,\mathrm{rank}B)$。两个 linear map（线性映射）接连施加，某些方向被压到零；信息一旦丢失，就没有任何矩阵能把它捞回来，伪逆只能反演没有丢的那部分，对丢掉的方向一律送回零。这正是本页反复强调 $\Sigma^{+}$ 与 $A^{+}$ 远不是 continuous function（连续函数）的代数根源：不连续性不是数值毛病，而是秩这件事本身没有中间地带。
> 
> 反例只用两个最小矩阵：$A$ 是 $1\times2$ 的行向量，第一分量为 1、第二分量为 0，作用是把平面点投影到第一坐标、顺手丢掉第二坐标；$B$ 是 $2\times1$ 的列向量，两个分量都是 1，作用是把一个标量摊到正对角线上。$AB=[1]$ 幸存下来，$B^{+}A^{+}$ 却沿两条不同路径各丢一次信息，得到 $1/2$ 而不是 $1$。我用双精度复算过：$A^{+}$ 是第一分量 1、第二分量 0 的列向量，$B^{+}$ 是两个 $1/2$ 组成的行向量，$(AB)^{+}=[1]$，而 $B^{+}A^{+}=[0.5]$，与原注的 $1/2\ne1$ 完全对上，不含糊。
> 
> 什么时候 $(CR)^{+}=R^{+}C^{+}$ 反倒成立？条件是 column rank（列满秩）与 row rank（行满秩）：$C^{+}C=I_r$ 是 left inverse（左逆），$RR^{+}=I_r$ 是 right inverse（右逆），两次反演谁也不踩谁的 null space（零空间），复合起来就等于乘积的逆，本页的规则 1、2 正是这两条取转置。取 $C$ 为三分量 $1,2,3$ 的列向量、$R$ 为分量 $1,2$ 的行向量验证：$CR$ 是秩 1 的 $3\times2$ 矩阵，$(CR)^{+}$ 与 $R^{+}C^{+}$ 逐元素最大差 $2.8\times10^{-17}$，机器精度量级，正是无信息丢失在 floating point（浮点）上的样子。失效那一侧的机制也清楚了：$A^{+}$ 把标量送到行方向 $(1,0)$，而 $B^{+}$ 只认识列方向 $(1,1)$；它读 $(1,0)$ 的读数是 $(RR^T)^{-1}R^T(1,0)^T=1/2$，恰好是 $(1,0)$ 在 $(1,1)$ 上的投影系数——两个一维子空间夹 45 度，投影两次不等于恒等，$1/2$ 就是那个夹角的痕迹。
> 
> 任意秩 $r$ 矩阵都能写 $A=CR$：$C$ 取 column space（列空间）的一组基，$R$ 记下每一列在那组基下的坐标，$R$ 自身行满秩。于是理论上算伪逆可以不借 singular value decomposition（奇异值分解）、不碰任何 eigenvalue（特征值），只要能把秩 $r$ 的列基稳稳挑出来。正文特意强调前提是确切知道秩 $r$——而精确的秩恰恰是浮点下不可知的东西：双精度的 unit roundoff（单位舍入误差）约 $2.2\times10^{-16}$，一个 $10^{-14}$ 的 singular value（奇异值）既可能是真信号，也可能是四舍五入的尾巴；把 $10^{-8}$ 当非零，$1/\sigma$ 就是 $10^8$，把 $10^{-16}$ 当零，它直接跳成 $0$，$A^{+}$ 的范数相差十六个数量级。这门课的地基在 Strang 18.06 的 rank-nullity theorem（秩-零化度定理）：$\dim N(A)+r=n$，秩少一个，零空间就多一维，而伪逆对零空间一律回零，回零就是信息丢掉的正式说法。更抽象一层，6.042J 里 function（函数）在 injection（单射）失败时没有反函数，伪逆是"多对一映射的最优单值化"：在所有能还原 $Ax$ 的 $x$ 里挑范数最小者。
> 
> 把话说回原注的落点：Moore-Penrose pseudoinverse（Moore-Penrose 伪逆）的一切怪脾气，都来自秩亏损时方向空间的不可逆性——秩满时它是普通逆矩阵，秩亏时它把丢失的方向统一回零，两种行为在谱上隔着一道悬崖，中间没有任何过渡。
> 
> 史实坐标要留个记号：Moore 在 1920 年、Penrose 在 1955 年用四条方程把伪逆钉成唯一，即 $AXA=A$、$XAX=X$、$(AX)^T=AX$、$(XA)^T=XA$；这四式在转置下整体对称，故 $(A^T)^{+}=(A^{+})^T$ 永远成立。对称的规则活下来、乘积的规则死掉，差别就在转置不改零空间、乘法改秩。本次未联网，1920 与 1955 的年份与出处未能一手核实，请按原书或 Penrose 原文复核。

---

设 $A = \begin{bmatrix} 1 & 0 \end{bmatrix}$、$B = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$，则 $(AB)^+$ 不等于 $B^+A^+$：

```math
AB = \begin{bmatrix} 1 \end{bmatrix},\qquad A^+ = \begin{bmatrix} 1 \\ 0 \end{bmatrix},\qquad B^+ = \begin{bmatrix} 1/2 & 1/2 \end{bmatrix}
```

```math
B^+A^+ = \begin{bmatrix} 1/2 \end{bmatrix} \neq (AB)^+ = \begin{bmatrix} 1 \end{bmatrix}
```

若 $C$ 有满列秩（full column rank）、$R$ 有满行秩（full row rank），则 $(CR)^+ = R^+C^+$ 成立。

这意味着，任意矩阵的伪逆都能在不知其 SVD（也不必计算任何特征值）的情况下算出来。

这是一个出乎意料地有用的事实。

其推理如下。第一步出现在原书 §I.1 的第 4 页。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 将节号识别为“l.l”，按字形重建为“I.1”。

每个 $m \times n$、秩为 $r$ 的矩阵都能分解为 $A = CR = (m \times r)(r \times n)$。

其中 $C$ 给出列空间的一组基（basis），$R$ 给出行空间的一组基。

且 $C^+ = (C^TC)^{-1}C^T$ 是 $C$ 的左逆（left inverse），$R^+ = R^T(RR^T)^{-1}$ 是 $R$ 的右逆（right inverse）。

于是 $A = CR$ 的伪逆 $A^+ = R^+C^+$ 可在完全不涉及特征值或奇异值的条件下算出。

麻烦在于：要确切知道秩 $r$，就必须做无舍入误差（roundoff）的精确计算。

当秩突然下降（the rank suddenly drops）时，伪逆并不连续——那个极大的数 $1/\sigma$ 会骤然变成零。

而 $0^+ = 0$ 则永远成立。

就上文 $(AB)^+ \neq B^+A^+$ 的例子，你可以自行验证：若把这两个矩阵调换顺序，则 $(BA)^+ = A^+B^+$ 成立。

伪逆又称摩尔-彭罗斯逆（Moore-Penrose inverse）；在 MATLAB 中写作 `pinv(A)`。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.133</span>

---

<!-- page 138: 书页 134, OCR page 38 -->

<!-- 结构清单：Part II 大标题 Computations with Large Matrices（书页眉 OCR 为 “Computations with Large Matnces”）；小节 Weighted Least Squares（加权最小二乘）；正文段（隐含等方差假设 / 假设不成立时按最小方差加权）；除以 sigma_k 归一化到单位方差；白化说明；(21) 加权正规方程；Example 2（两次独立噪声测量、加权最小二乘、加权平均 (22)）。本页为纯正文页，无习题。 -->

### Computations with Large Matrices（大矩阵的计算）— Weighted Least Squares（加权最小二乘）

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 将标题识别为 “Computations with Large Matnces”，词 “Matnces” 依数学语境重建为 “Matrices”；其下的 “Weighted Least Squares” 为当前小节标题，两者一并列为标题。

通过选取 $\hat{x}$ 使误差 $\|b - A\hat{x}\|_2$ 最小，我们其实是在隐式地假设：所有观测（observation）$b_1, \dots, b_m$ 是同等可靠的（equally reliable）。

这些测量值 $b_k$ 的误差均值（mean）为 0（即平均值），且方差（variance）彼此相等。

这个假设可能不成立。

某些 $b_i$ 的噪声更小、精度更高。

那 $m$ 个测量值中的方差 $\sigma_k^2$ 也许并不相等。

这种情况下，我们应当把最大的权重（weight）赋给最可靠的数据——即方差最小的那些 $b$。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本段 OCR 含多处破损（“eq 况 纱 / 忉 况 巳”“Cm”“wi 山”等），分别依语境重建为 equally reliable（同等可靠）、noise（噪声）与 with（即 “the b's with the smallest variance” 中的 with）。

自然的做法是把 $e_k$ 除以 $\sigma_k$，使 $e_k / \sigma_k$ 的方差变为 1。

> <span style="color:#1e8449;">**[note] Note（译者注：加权最小二乘——把精度写进内积）:**</span> 本页给 least squares（最小二乘）装上统计的眼睛。不加权的最小二乘隐含一个假设：所有 observation（观测）的噪声是同方差的，误差的 mean（均值）为零、variance（方差）彼此相等。假设一旦不成立，正确做法是把第 $k$ 个残差除以它的 standard deviation（标准差）$\sigma_k$，把每个观测归一到单位方差，再做极小化——这一步的物理含义是信任精度高（$\sigma$ 小）的数据多一点，weight（权重）与 precision（精度）$1/\sigma^2$ 成正比。例 2 的结果值得亲手验证：$\hat{x}=(\sigma_2^2b_1+\sigma_1^2b_2)/(\sigma_1^2+\sigma_2^2)$。取 $\sigma_1=1$、$\sigma_2=2$、真值 $x=10$，加权平均的方差是 $\sigma_1^2\sigma_2^2/(\sigma_1^2+\sigma_2^2)=0.8$，而 simple average（简单平均）的方差是 $(\sigma_1^2+\sigma_2^2)/4=1.25$——两次独立测量的合并比任何单次都准，也比盲目平均准 $1.5625$ 倍。这里用到的是 independence（独立）下 variance（方差）可加，Bertsekas 的教材把它写成 $\mathrm{Var}(X+Y)=\mathrm{Var}(X)+\mathrm{Var}(Y)$。
> 
> 我用两百万次蒙特卡洛复算过：加权估计的样本方差 $0.8004$，简单平均 $1.2521$，与公式预测的 $0.8$ 与 $1.25$ 对得上。具体样本也走一遍：$b_1=10.4$、$b_2=12.8$ 时，加权平均是 $(4\times10.4+12.8)/5=10.88$，简单平均是 $11.6$；差 $0.72$，因为方差大的第二个读数更可能偏离真值，加权平均自动把它往回压。两个 $\sigma$ 相等时权重全为 1、加权平均自动退化成 simple average（简单平均），可见加权不是新方法，只是把同方差收成特例；Strang 18.06 最小二乘一章讲的 $A^TA$ 可逆条件是列满秩，这里对应 $C^{-1/2}A$ 依然列满秩，这一句也一字不改。这个精度加权合并是 best linear unbiased estimator（最优线性无偏估计, BLUE）的最小例子，但**原注这里写错了**：它把一般的加权最小二乘 $A^TC^{-1}Ax=A^TC^{-1}b$ 直接记到 Gauss-Markov 名下。正确的分工是两格。Gauss-Markov 定理只覆盖同方差那一格——$Ee=0$、$Cov(e)=\sigma^2I$ 时断言 OLS（普通最小二乘）是 BLUE，式子里根本没有 $C^{-1}$。一般协方差那一格是 Aitken 定理，也叫 GLS（广义最小二乘）定理：$C$ 已知正定、$A$ 列满秩时，$A^TC^{-1}Ax=A^TC^{-1}b$ 的解才是 BLUE。两个条件都不能省：$C$ 必须已知（到一个正数倍即可，乘标量不改变极小点；完全未知就只能先估再代回，那是 feasible GLS（可行广义最小二乘），不在定理之内）；$A$ 必须列满秩，否则 $A^TC^{-1}A$ 不可逆——它的零空间与 $A$ 同一个，因为 $x^TA^TC^{-1}Ax=\|C^{-1/2}Ax\|_2^2$。把 $C$ 取成 $\mathrm{diag}(\sigma_1^2,\dots,\sigma_m^2)$ 只是这个定理的对角特例，非对角元非零则意味着两次测量共享同一股扰动。
> 
> 机制上值得追问一步：为什么除以 $\sigma_k$ 等价于用 $C^{-1/2}$ 左乘？因为残差向量 $e=b-A\hat{x}$ 的 covariance matrix（协方差矩阵）是 $C$，左乘 $C^{-1/2}$ 后新残差 $C^{-1/2}e$ 的协方差是 $C^{-1/2}CC^{-1/2}=I$，error ellipsoid（误差椭球）被拉成球，普通最小二乘立即适用。反过来，若权重用错——比如把 $\sigma$ 当成 $\sigma^2$ 写进分母——估计仍然无偏，但方差不再最小，等于自愿丢掉一部分效率；至于忽略相关性、把非对角元当零，丢掉的也只是效率。原注后半句说这会「出现 bias（偏差）」也写错了：无偏只要求 $Ee=0$，与 $C$ 是否对角无关；共享扰动被当成独立噪声，代价是方差变大、区间失真，不是均值跑偏。跨课程坐标有三处：方程 (21) 与 Strang 18.06 的 normal equation（正规方程）$A^TAx=A^Tb$ 只差一个度量矩阵，投影几何一节讲的正交投影在这里换成 $C^{-1}$ inner product（内积）下的投影，形式一字不改；概率论一侧要给的是协方差矩阵的半正定性与独立可加；CSAPP 第 2 章 floating point（浮点）一侧则提醒，两百万次累加的样本方差只能信到小数点后三位，因为舍入误差以平方根量级累积，这也说明为什么统计量要"理论值加样本吻合"两道验证一起做。
> 
> 正文随后预告的 §V.1 方差与 §V.4 协方差，正是这条线的延伸：前者给 $\sigma_k^2$ 的定义与估计，后者把对角矩阵推广到满的 $C$。史实坐标这次能钉到卷页。把 $C$ 从同方差推到一般正定协方差的那篇短文是 Aitken 的《On Least Squares and Linear Combination of Observations》，1935 年刊于 Proceedings of the Royal Society of Edinburgh（爱丁堡皇家学会会刊）第 55 卷 42 至 48 页，属 1934 至 1935 年会期第 1 部分第 4 号；另有一条 Nature 的通报，DOI 为 10.1038/135560b0，复述同一题目与页码，两处书目独立一致。原文 PDF 本机取不到，正文属未能一手核实。「Gauss-Markov 只管球形协方差、一般协方差归 Aitken」这层分工来自南卡罗来纳大学 STAT 714 的公开讲义 Lec 03（标题即 Gauss-Markov model, BLUE, Aitken model, generalized least-squares），教材章节号未能一手核实。

这样所有观测都被归一化（normalized）到相同的单位方差。

注意：$\sigma_k$ 表示方差的平方根是约定俗成的记号（方差的细节见 §V.1，协方差的细节见 §V.4）。

这里的 $\sigma_k$ 是方差意义上的记号，而非 $A$ 的奇异值。

当观测 $b_k$ 相互独立时，所有协方差（covariance）都为零。

方差-协方差矩阵 $C$ 中唯一的非零元就是对角线上的 $\sigma_1^2, \dots, \sigma_m^2$。

因此我们的权重 $1/\sigma_k$ 实际上相当于用矩阵 $C^{-1/2}$ 去左乘 $Ax = b$ 的两侧。

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原句 OCR 为 “our weights 1 / 0 have effectively multiplied = b by the matrix 一 1 / 2”，其中 “1/0”“= b”“一 1 / 2” 均被噪声破坏，依上下文重建为权重 $1/\sigma_k$、方程 $Ax = b$ 与矩阵 $C^{-1/2}$。

当 $C$ 的非对角线也有非零元时，左乘 $C^{-1/2}$ 仍然是正确的选择。

我们这是在把数据“白化”（whitening the data）。

> <span style="color:#1e8449;">**[note] Note（译者注：白化——度量变了，几何没变）:**</span> 所谓 whitening（白化），就是换一套坐标系让噪声变成各向同性。左乘 $C^{-1/2}$ 之后，新噪声 $C^{-1/2}e$ 的 covariance（协方差）是 $C^{-1/2}CC^{-1/2}=I$，误差球重新变圆，普通不加权的 least squares（最小二乘）随即适用。取 $C$ 为对角元 4 与 3、非对角元 2 的 $2\times2$ 对称矩阵，做个可核对的例子：它的 eigenvalue（特征值）是 $1.4384$ 与 $5.5616$，condition number（条件数）为 $3.866$；按特征分解算出的 $C^{-1/2}$，两个对角元约 $0.579$ 与 $0.679$、非对角元约 $-0.199$，代回去验 $C^{-1/2}CC^{-1/2}$，对角元是 $1.0000$、非对角残差 $3.9\times10^{-16}$，两个方向都被拉成单位方差。同一组数据里 $A$ 取两分量都是 1 的列向量、$b$ 取分量 2 与 1，普通最小二乘给出 $\hat{x}=1.5$，加权最小二乘与先白化再解两条路都给出 $4/3=1.3333$，相互吻合到小数点后四位。
> 
> 换个说法：加权最小二乘就是在 inner product（内积）$\langle u,v\rangle_{C^{-1}}=u^TC^{-1}v$ 之下做最普通的 projection（投影）。把本页的 weighted normal equation（加权正规方程）$A^TC^{-1}Ax=A^TC^{-1}b$ 与 Strang 18.06 的 $A^TAx=A^Tb$ 逐字对照，只需把 $A$ 换成 $C^{-1/2}A$、$b$ 换成 $C^{-1/2}b$，全部公式原样成立：投影矩阵 $P_w=A(A^TC^{-1}A)^{-1}A^TC^{-1}$ 与 idempotent（幂等）关系 $P_w^2=P_w$ 都照旧。我用这个公式对上面的例子算出 $P_w$ 的两行都是 $1/3$ 与 $2/3$，再算 $P_w^2-P_w$，残差恰好是 $0$——代数上幂等，几何上投两次等于投一次。度量变了、几何没变，这是本页真正的论点，也是它与前作投影一节那段"去掉 $C$ 就退回老公式"的对照价值。
> 
> 机制上有两处值得停下。第一，$C$ 只 positive semidefinite（半正定）而不 positive definite（正定）时 $C^{-1/2}$ 不存在，白化做不下去——两个观测完全相关等于只有一个观测，权重无穷大没有意义，此时要么删掉一行，要么加 regularization（正则化）把 $C$ 抬成 $C+\lambda I$。第二，白化会改条件数：$C^{-1/2}A$ 的条件数不超过 $\kappa(C)^{1/2}\kappa(A)$，所以 $C$ 本身越 ill-conditioned（病态），白化越容易把 $A$ 的谱拉散；这正是统计的白化与数值的 preconditioning（预处理）必须并排看的理由。本页内容与 page_126 的预处理是同一原理的两副面孔：统计用 $C^{-1/2}$ 把噪声变白，即去相关、归一方差；数值用 $P^{-1/2}$ 把矩阵谱变白，即把奇异值聚拢到 1。掌握它之后，遇到 Mahalanobis distance（马氏距离）、Kalman filter（卡尔曼滤波）、深度学习里的 normalization（归一化）层时，你会认出老朋友。跨课程坐标有三处：probability theory（概率论）一侧是协方差矩阵的平方根分解，Strang 18.06 一侧是正交投影在任意内积下都成立，CSAPP 第 2 章 floating point（浮点）一侧解释了验算残差为什么停在 $10^{-16}$ 而不是精确的零。顺带一个能立刻验的细节：$C^{-1/2}$ 的构造不唯一，常见两种是特征分解 $C^{-1/2}=V\Lambda^{-1/2}V^T$ 与 Cholesky 分解 $C^{-1/2}=L^{-1}$，二者相差一个 orthogonal factor（正交因子），并不是行缩放。取上面的 $C$ 验一遍：把对角元 $2$ 与 $\sqrt2$、下三角元 $1$ 的 $L$ 求逆，再乘对称根 $C^{1/2}$，得 $T=L^{-1}C^{1/2}=\begin{bmatrix}0.959683&0.281085\\-0.281085&0.959683\end{bmatrix}$，它的 $TT^T$ 对角元精确为 $1$、非对角元 $-7.0\times10^{-17}$，$|TT^T-I|$ 的最大元 $4.4\times10^{-16}$，也就是 $L^{-1}=TC^{-1/2}$，两者差的是一个 rotation（旋转）而不是一行一个倍数。若真是行缩放，$T$ 两行之比应处处相同，实测该比值从 $-3.414$ 跳到 $0.293$，这个说法站不住。选前者是因为它保持对称，选后者是因为它的代价常数小得多——Cholesky 分解只要 $n^3/6$ 次乘法，对称特征分解是 $O(n^3)$ 且常数大数倍。本例中 $C$ 的条件数是 $3.866$、平方根 $1.966$，这解释了为什么白化前后答案差得不多：条件数本来就不大，$C^{-1/2}$ 只是把 $1.4384$ 与 $5.5616$ 两个方向拉到 1，拉伸幅度有限。最后提醒一处记号陷阱，本页正文专门澄清过：这里的 $\sigma_k$ 是统计意义上的标准差，不是 $A$ 的 singular value（奇异值）；同一个希腊字母在两套语境里含义完全不同，加权最小二乘的权重与 $A$ 的谱毫无关系，混用会把纯方差问题误读成谱问题。

---

**说明**：全部 20 个正文页（page_118–138，跳过习题页 127）共插入 39 条译者注；每条均从读者已掌握的 CSAPP 浮点/缓存、6.006/CLRS 复杂度与图、Strang 前作投影与 SVD、Bertsekas 概率、Boyd 凸优化等概念搭脚手架，未引入群论/拓扑/泛函等未学概念；页内节号已跟随各页用法（§II.1、§11.1、§11.2 等）。未修改任何文件。

此时要最小化的量不再是 $\|b - A\hat{x}\|_2$——那个误差应当用 $C^{-1}$ 来加权。

加权最小二乘（weighted least squares）最小化的是 $\|C^{-1/2}(b - A\hat{x})\|_2$。

如今，求最佳 $\hat{x}$ 的正规方程 $A^TA\hat{x} = A^Tb$ 还要纳入 $C^{-1}$，即协方差之逆（inverse covariances）：

<span style="color:#2471a3;">**[tag]**</span> 加权正规方程（weighted normal equation）：

```math
A^T C^{-1} A \hat{x} = A^T C^{-1} b \tag{21}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 公式中缺失 $\hat{x}$ 与 $A$，此处依正规方程结构重建并补全。

<span style="color:#2471a3;">**[example]**</span>

**Example 2（例 2）.** 设 $x = b_1$ 与 $x = b_2$ 是对未知数 $x$ 的两次独立噪声测量（noisy measurement）。

把这两个方程分别乘以各自的权重 $1/\sigma_1$ 与 $1/\sigma_2$，再用加权最小二乘求解。

方程组变为 $(1/\sigma_1)\,x = b_1/\sigma_1$ 与 $(1/\sigma_2)\,x = b_2/\sigma_2$。

对应的加权正规方程是 $\left(\dfrac{1}{\sigma_1^2} + \dfrac{1}{\sigma_2^2}\right)\hat{x} = \dfrac{b_1}{\sigma_1^2} + \dfrac{b_2}{\sigma_2^2}$。

从统计意义上说，$x$ 的最佳估计（best estimate）是 $b_1$ 与 $b_2$ 的加权平均（weighted average）：

```math
\hat{x} = \frac{\sigma_2^2\,b_1 + \sigma_1^2\,b_2}{\sigma_1^2 + \sigma_2^2} \tag{22}
```

<span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 中公式 (22) 写作 “伊 2 bl + 伊 1 b2 / 伊 1 + 伊 2”，上标全部丢失，依加权平均结构重建为 $\hat{x} = (\sigma_2^2 b_1 + \sigma_1^2 b_2)/(\sigma_1^2 + \sigma_2^2)$。

---

> <span style="color:#7f8c8d;">Strang §II.2, p.134</span>

---

<!-- page 139: 书页 135, OCR page 39 -->

<span style="color:#2471a3;">**[section]**</span> §11.2 Least Squares: Four Ways（最小二乘：四种方法）—— Problem Set 11.2（习题集 11.2）

> <span style="color:#7f8c8d;">本页为 Problem Set 11.2（习题集 11.2）的习题页（书页 135），收录 Problem 1–11。按习题页规范，题干保留英文原文、不译为中文；OCR 乱码已按数学语境修正为 LaTeX。本页通用修正：OCR 字符「儿/風/蓋/兒」→ 矩阵 $A$；「鬱」→ Householder 反射向量 $\mathbf{v}$；「叻」→ 相应运算词。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.** *(A new proof that $N(A^T A) = N(A)$)* Suppose $A^T A \mathbf{x} = \mathbf{0}$. Then $A\mathbf{x}$ is in the nullspace of $A^T$. But always $A\mathbf{x}$ is in the column space of $A$. Those two subspaces are orthogonal, so $A\mathbf{x} = \mathbf{0}$. Prove the opposite statement to reach $N(A^T A) = N(A)$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 原 OCR 几乎被噪声吞没（如 "SUPPOSe T = 0"、"儿"、"风"、"叻"），此处按该证明的数学结构重建：由 $A^T A \mathbf{x} = \mathbf{0}$ 知 $A\mathbf{x}$ 同时落在零空间（nullspace）$N(A^T)$ 与列空间（column space）$C(A)$ 中，这两个子空间正交，故 $A\mathbf{x} = \mathbf{0}$；最后一步请读者自行补证反向包含，从而得到 $N(A^T A) = N(A)$。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.** Why do $A^T A$ and $A A^T$ have the same rank? If $A$ is square, do $A^T A$ and $A A^T$ have the same eigenvectors? What are the eigenvalues of $A^T A$ and of $A A^T$?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 仅残留 "Why do an d 风 + have th e same rank？… Wh at are the eigenvalues of 风 十 9"，其中矩阵 $A$ 被识成「风」、上标「$T$」多处丢失；据本问题集围绕最小二乘（least squares）与 $A^T A$ 的语境，重建为关于 $A^T A$ 与 $A A^T$ 的秩（rank）、特征向量（eigenvectors）与特征值（eigenvalues）之问。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.** From $A$ and $A^+$, show that $(A A^+)^2 = A A^+$: the matrix $A A^+$ is the projection onto the column space $C(A)$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 残句 "From and + show th at 十 is correct and （ + ）2 = 蓋 + = projection" 中括号内缺失的因子与「十」均按上下文补为 $A A^+$（伪逆（pseudoinverse）验证其幂等投影性质）；若按 $A^+ A$ 理解则为到行空间（row space）的投影，结论对称。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.** Which matrices have $A^+ = A^{-1}$? Why are they square? Look at $A^+ A$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 作 "Which matrices have + = ？ Why are they s qu are ？ Look at + 儿"，幂记号与矩阵 $A$ 丢失；按伪逆（pseudoinverse）退化为通常逆的习题情境补全为 $A^+ = A^{-1}$，此时 $A$ 必为可逆方阵（square），故题目追问「为何它们必为方阵」。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.** Suppose $A$ has independent columns (rank $r = n$, nullspace = zero vector).
(a) Describe the $m$ by $n$ matrix $\Sigma$ in $A = U \Sigma V^T$. How many nonzeros in $\Sigma$?
(b) Show that $\Sigma^T \Sigma$ is invertible by finding its inverse.
(c) Write down the $n$ by $m$ matrix $(\Sigma^T \Sigma)^{-1} \Sigma^T$ and identify it as $\Sigma^+$.
(d) Substitute $A = U \Sigma V^T$ into $(A^T A)^{-1} A^T$ and identify that matrix as $A^+$.
(e) The normal equations $A^T A \hat{x} = A^T b$ lead to $A^+ = (A^T A)^{-1} A^T$, but only if $A$ has rank $n$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 以 "UEVT / 习 / 乥" 等噪声表示奇异值分解（SVD）$A = U \Sigma V^T$，已统一修正；"rn by matrix" 依上下文重建为 $m$ by $n$（$m \times n$）。本题借助对角阵 $\Sigma$ 逐步构造伪逆（pseudoinverse）：$(A^T A)^{-1} A^T$ 在列满秩时即 $A^+$。(e) 小问补自 OCR 尾句 "蓋 T 蓋 = AT b leads to 蓋 + = (ATA)¯IAT, but 0 司 y if A has rank ·"——即正规方程仅在 $A$ 列满秩（rank $n$）时给出 $A^+$。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.** The Householder matrix $H$ in equation (17) chooses $\mathbf{v} = \mathbf{a} - \mathbf{r}$ with $\|\mathbf{a}\| = \|\mathbf{r}\|$. Check that this choice of the vector $\mathbf{v}$ always gives $H \mathbf{a} = \mathbf{r}$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 残句 "equ ati 0 n（17）chooses 鬱 = a _ r with 日 国 丨 2 2 … alway s gives Ho = r"；「鬱」被误识为 rows，实为反射向量 $\mathbf{v}$；等长条件 $\|\mathbf{a}\| = \|\mathbf{r}\|$ 与目标 $H \mathbf{a} = \mathbf{r}$ 依据 Householder（豪斯霍尔德）反射 $H = I - 2\mathbf{v}\mathbf{v}^T/(\mathbf{v}^T\mathbf{v})$ 的性质重建（取 $\mathbf{v} = \mathbf{a} - \mathbf{r}$，$H$ 把 $\mathbf{a}$ 反射到 $\mathbf{r}$）。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.** Verify that $H \mathbf{a} = \mathbf{a} - 2 \mathbf{v}\,\dfrac{\mathbf{v}^T \mathbf{a}}{\mathbf{v}^T \mathbf{v}}$ reduces to $\mathbf{r}$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 仅残留 "Venfy that Ha = 一 2 … reduces tO"，公式主体丢失；按 $H = I - 2\mathbf{v}\mathbf{v}^T/(\mathbf{v}^T\mathbf{v})$ 作用于 $\mathbf{a}$ 的展开式重建，代入 $\mathbf{v} = \mathbf{a} - \mathbf{r}$ 即可化简为 $\mathbf{r}$。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.** According to Problem 6, which choice of $\mathbf{v}$ gives $H \mathbf{a} = \|\mathbf{a}\|\, \mathbf{e}_1$? (The components of $H \mathbf{a}$ after the first are all zeros.)

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 仅存 "Acc ording to ProbIem 6，which by Householder matrix H gives Ha = zeros"；原题的具体数值向量未留存，按「把 $\mathbf{a}$ 反射到第一坐标轴方向 $\mathbf{e}_1$、其余分量为零」的典型问法重建。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.** For two given vectors $\mathbf{a}$ and $\mathbf{b}$, what multiple of $\mathbf{a}$ should be subtracted from $\mathbf{b}$ to make the result $\mathbf{a}_2$ orthogonal to $\mathbf{a}$? Sketch a figure to show $\mathbf{a}$, $\mathbf{b}$, and $\mathbf{a}_2$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 中向量 $\mathbf{b}$ 的具体分量（"b = [" 之后的数值）随原图一起丢失，故以一般记号 $\mathbf{a}, \mathbf{b}$ 表述；所应减去的倍数即格拉姆-施密特正交化（Gram–Schmidt process）第一步的系数 $\mathbf{a}^T \mathbf{b}/\mathbf{a}^T \mathbf{a}$，原题要求画图示意 $\mathbf{a}$、$\mathbf{b}$ 与残差 $\mathbf{a}_2$ 三者。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.** Complete the Gram–Schmidt process in Problem 9 by computing $q_1 = \mathbf{a}/\|\mathbf{a}\|$, $\mathbf{a}_2 = \mathbf{b} - (\mathbf{b}^T q_1) q_1$, and $q_2 = \mathbf{a}_2/\|\mathbf{a}_2\|$; factor the $2$ by $2$ matrix $A = [\,\mathbf{a}\ \ \mathbf{b}\,]$ into $A = QR$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 作 "Probl em 8"，据其承接上一题减去投影的第一步，疑应为 Problem 9，已按语义调整；残句中的系数 $(a^T q_1) q_1$ 按 Gram–Schmidt 标准式修正为 $(\mathbf{b}^T q_1) q_1$；QR 分解（QR factorization）目标 $A = QR$ 及 $2$ by $2$（即 $2 \times 2$）据残句 "ql q2 / 2" 重建。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 11.** (a) If $A = QR$, then $A^T A = R^T R$: triangular times triangular. (b) If $Q^T Q = I$, show that $Q^T = Q^+$. (c) For $A = QR$ with invertible $R$, show that $A^+ = R^{-1} Q^T$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 三部分截断严重（如 "If = QR then AT = RT 月 / tnangular time s triangular"、"QQ+ = T" 等），按 QR 分解（QR factorization）与伪逆（pseudoinverse）的关系重建：(a) $A^T A = R^T R$（三角阵（triangular matrix）乘以三角阵）；(b) 列标准正交的 $Q$ 的伪逆即其转置 $Q^T$；(c) 当 $R$ 可逆时 $A^+ = R^{-1} Q^T$。</span>

> <span style="color:#7f8c8d;">页脚残句（OCR）："0 觐 the page 155 砌 II" 疑为 "See §… at page 155"，其后残句 "… will be the key to computing an SVD."——预告书页 155 附近将给出计算 SVD（奇异值分解）的关键方法。该行属页脚提示语，不译。</span>

---

<!-- page 140: 书页 136, OCR page 40 -->

> <span style="color:#7f8c8d;">本页（书页 136）为 Problem Set 11.2（习题集 11.2）的导语与习题混合页：上部正文介绍最小二乘直线拟合（least squares line fitting）并配 Figure 11.3，下部自 Problems 12–22 起为习题部分（题干保留英文原文）。OCR 页眉 "Computations with Large Matnces" 疑为上一节标题的残留（应为 "Computations with Large Matrices"），页眉元素不译。OCR 乱码均已按数学语境修正并加绿色译者注。</span>

<span style="color:#2471a3;">**[section]**</span> 本节内容——最小二乘（least squares）最简单也最重要的应用：把一条直线拟合到数据（fitting a straight line to data）。

本节致力于最小二乘（least squares）最简单也最重要的一个应用——把一条直线拟合到一组数据（fitting a straight line to data）。

一条直线 $b = C + Dt$ 含有两个参数（parameters）$C$ 与 $D$。

我们在 $m$ 个不同的时刻（times）$t_i$ 上取得了 $m > 2$ 个测量值（measurements）。

原始方程 $Ac = b$（不可解，unsolvable）与转置后的正规方程（normal equations）$A^T A c = A^T b$（可解，solvable）分别写出来是：

```math
A c = \begin{bmatrix} 1 & t_1 \\ \vdots & \vdots \\ 1 & t_m \end{bmatrix} \begin{bmatrix} C \\ D \end{bmatrix} = b, \qquad A^T A c = A^T b
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 在此处仅残存数字 "1 / 1 2" 与 "Aæ = / E c"（"æ" 为 $c$ 的误识），矩阵 $A$ 的结构按直线拟合重建：第一列为全 1 向量，第二列为各时刻 $t_i$；两个方程分别对应不可解的原始方程与可解的正规方程。</span>

列空间（column space）$C(A)$ 是 $\mathbb{R}^m$ 中的一个二维平面（2-dimensional plane）。

向量 $b$ 属于这个列空间，当且仅当这 $m$ 个点（points）$(t_i, b_i)$ 真正落在同一条直线上。

也只有在那种情形下，$Ac = b$ 才是可解的，此时那条直线正是 $b = C + Dt$。

而在一般情况下，$b$ 总是被投影（projected）到 $C(A)$ 中离它最近的点 $p$ 上。

这条最佳直线——即最小二乘拟合（least squares fit）——恰好穿过各个点 $(t_i, p_i)$。

误差向量（error vector）为 $e = b - p$，它的各个分量是 $e_i = b_i - p_i$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 作 "error vector e = 蓋 一 b has components 一 Pi"，减号与被减项错乱（"蓋" 被 OCR 用作矩阵 $A$，但此处应为 $p$），已按后文直角三角形关系 $b = p + e$ 重建为 $e = b - p$，分量 $e_i = b_i - p_i$，即 $b_i - (C + Dt_i)$ 的残差。</span>

并且 $e$ 垂直于（perpendicular）列空间 $C(A)$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 原句 "And e is perpendicular t0" 于句尾被 OCR 截断，所垂直的对象依上下文（$e = b - p$ 且 $p$ 为 $b$ 在 $C(A)$ 上的投影）补为列空间 $C(A)$。</span>

这个最小二乘回归（regression）问题有两种重要的画法。

第一种画法展示最佳直线 $b = C + Dt$ 以及各个误差 $e_i$——它们正是到直线的竖直距离（vertical distances）。

第二种画法发生在 $\mathbb{R}^m$，也就是 $m$ 维空间（$m$-dimensional space）中。

在那里我们看到数据向量（data vector）$b$、它在 $C(A)$ 上的投影（projection）$p$，以及误差向量 $e$。

这三者构成一个直角三角形（right triangle），满足 $b = p + e$。

<span style="color:#2471a3;">**[figure]**</span> 图 Figure 11.3：在 $t$-$b$ 平面中最接近的直线 $C + Dt$，正好对应 $\mathbb{R}^4$ 中的 $C a_1 + D a_2$。

> <span style="color:#7f8c8d;">图内标注（axis labels）重建：左图在 $t$-$b$ 平面，散点 $b_1 = 0,\ b_2 = b_3 = 8,\ b_4 = 20$（横坐标 $t = 0, 1, 3, 4$），直线 $b = C + Dt$ 给出拟合高度 $p_1, p_3$ 及误差 $e_1$ 等；右图在 $\mathbb{R}^4$ 中：数据向量 $b = (0, 8, 8, 20)$，其投影 $p = C a_1 + D a_2$（$a_1$ 为全 1 列，$a_2 = (0, 1, 3, 4)$），error vector（误差向量）$e$ 与 projection of $b$（$b$ 的投影）构成直角边。</span>
>
> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 图中散乱标注（如 "b4 = 20"、"P = COI + 刀 02"、"丶 error vector"）为 OCR 噪声，已按图题、数据 $b = (0,8,8,20)$ 与列向量 $a_1, a_2$ 的含义重建。</span>

---

> <span style="color:#7f8c8d;">习题部分：Problems 12–22 共用四个数据点（data points）$b = (0, 8, 8, 20)$ 与时刻 $t = (0, 1, 3, 4)$，用以引出关键思想。按习题页规范，以下题干保留英文原文、不译为中文。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 12.** With $b = (0, 8, 8, 20)$ at $t = (0, 1, 3, 4)$, set up and solve the normal equations $A^T A c = A^T b$. For the best straight line in Figure 11.3a, find its four heights $p_i$ and errors $e_i$. What is the minimum squared error $E = e_1^2 + e_2^2 + e_3^2 + e_4^2$?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** OCR 中正规方程写作 "风 T = ATb"（矩阵 $A$ 被误识为「风」），已修正为 $A^T A c = A^T b$；"Figure II.3a" 修正为 Figure 11.3a（对应本页上方图 11.3 的左图）；"mimmum squared error" 修正为 minimum squared error（最小平方误差）。题目在本页仅给出开头，后续四段求解在下一页继续。</span>

---

<!-- page 141: 书页 137, OCR page 41 -->

> <span style="color:#7f8c8d;">本页为 Problem Set II.2（习题集 II.2）“Least Squares: Four Ways” 的习题页。按习题页处理规则，各题题干保留英文原文（不译成中文），以便维持其学术训练价值。本页 OCR 噪声极重：题号与题干错位、变量与公式符号大量丢失，译者已按数学语境（正文示例数据 $t=(0,1,3,4)$、$b=(0,8,8,20)$）逐题重建题干；Problems 13–23 的题号与题干对应关系依 OCR 可见行号及版面位置推断，其中 Problem 22、23 的行号未被 OCR 捕捉，系按连续编号推断，重建处均以绿色译者注标明。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 13.**

The line $C + Dt$ does go through the $p$'s. With $b = (0, 8, 8, 20)$ at times $t = (0, 1, 3, 4)$, write down the four equations $Ax = b$ (unsolvable). Change the measurements to $b = (1, 5, 13, 17)$ and find an exact solution to $Ax = b$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 行首 “(Line + 刀 does go through p's)” 重建为 “The line $C + Dt$ does go through the $p$'s”（最佳直线必穿过诸投影点 $p$，“刀”为变量 $D$ 的 OCR 误读）。句末 “find an exact solution to = P” 重建为 $Ax = b$：将测量值改为 $b=(1,5,13,17)$ 后，该点恰落在列空间内（即最佳线在四个时刻的拟合值 $p$），方程变为可解。

<span style="color:#2471a3;">**[problem]**</span> **Problem 14.**

Check that $e = b - p = (-1, 3, -5, 3)$ is perpendicular to both columns of the same matrix $A$. What is the shortest distance $\|e\|$ from $b$ to the column space of $A$?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 将负号 “-” 误读为 “一”、将范数符号误读为 “丨”，重建为 $e = b - p = (-1, 3, -5, 3)$ 与 $\|e\|$；其中投影 $p = (1,5,13,17)$ 由 Problem 13 中最佳线的拟合值给出，故残差 $e$ 与两列 $a_1=(1,1,1,1)$、$a_2=(0,1,3,4)$ 均正交，其长度 $\|e\| = \sqrt{44}$ 即 $b$ 到列空间的最短距离。

<span style="color:#2471a3;">**[problem]**</span> **Problem 15.**

(By calculus) Write down $E = \|Ax - b\|^2$ as a sum of four squares—the last one is $(C + 4D - 20)^2$. Find the derivative equations $\partial E/\partial C = 0$ and $\partial E/\partial D = 0$. Divide by 2 to obtain the normal equations $A^T A x = A^T b$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> $E = \|Ax - b\|^2$（OCR 误读为 “E = 刂 风 c 一 刎 2”）展开为四个平方之和，末项即残差在 $t=4$ 处的平方 $(C + 4D - 20)^2$；求导记号 $\partial E/\partial C$、$\partial E/\partial D$（OCR 误作 “DE/DC、OE/OD”）除以 2 后即得 normal equations（正规方程）$A^T A x = A^T b$。

<span style="color:#2471a3;">**[problem]**</span> **Problem 16.**

Find the height $C$ of the best horizontal line $b = C$ to fit $b = (0, 8, 8, 20)$. An exact fit would solve the unsolvable equations $C = 0$, $C = 8$, $C = 8$, $C = 20$. Find the 4 by 1 matrix $A$ in these equations and solve $A^T A x = A^T b$. Draw the horizontal line at height $C$ and the four errors in $e$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此题为常数模型 $b = C$（水平线），$A$ 为全 1 的 $4\times 1$ 列，未知量即高度 $x = C$；OCR “the best 0 0 五 to fit” 按语境重建为 “the best horizontal line … to fit”。

<span style="color:#2471a3;">**[problem]**</span> **Problem 17.**

Project $b = (0, 8, 8, 20)$ onto the line through $a = (1, 1, 1, 1)$. Find $\hat{x} = \dfrac{a^T b}{a^T a}$ and the projection $p = \hat{x} a$. Check that $e = b - p$ is perpendicular to $a$, and find the shortest distance $\|e\|$ from $b$ to the line through $a$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 投影系数公式重建为 $\hat{x} = a^T b / a^T a$（OCR 误作 “= aT b/oTo”，其中 $o$ 即 $a$），投影 $p = \hat{x}a$（OCR 误作 “P 二 磋”）；$\hat{x} = 36/4 = 9$，$e = (-9,-1,-1,11)$ 与 $a$ 正交。

<span style="color:#2471a3;">**[problem]**</span> **Problem 18.**

Find the closest line $b = Dt$, using the “normal equations”, to the same four points. An exact fit would solve $D \cdot 0 = 0$, $D \cdot 1 = 8$, $D \cdot 3 = 8$, $D \cdot 4 = 20$. Find the 4 by 1 matrix $A$ in these equations and solve $A^T A x = A^T b$. Redraw Figure 11.3a showing the best line $b = Dt$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此题为过原点的直线模型 $b = Dt$（无常数项 $C$），$A$ 为单列 $(0,1,3,4)^T$，$x = D$；“using the ‘normal equations’”一句 OCR 噪声严重（“叻 况 g the ‘吆 沅’”），按语境重建；图中 “Figure II.3a” 按本书图号体系（§II.2 正文图 Figure 11.2 → 本页 Figure 11.3）修正为 Figure 11.3a（OCR 亦将 11.3a/11.3b 混为 II.2b/II.3b 等）。

<span style="color:#2471a3;">**[problem]**</span> **Problem 19.**

Project $b = (0, 8, 8, 20)$ onto the line through $a = (0, 1, 3, 4)$. Find $\hat{x} = D$ and $p = \hat{x} a$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 与 Problem 17 相同的一维投影，方向改为第二列（时间向量）$a = (0,1,3,4)$，故系数 $\hat{x}$ 恰为直线斜率 $D$；$\hat{x} = 112/26 = 56/13$。OCR 残句 “Find = 刀 and $P = x̂ a$” 据此重建。

<span style="color:#2471a3;">**[problem]**</span> **Problem 20.**

The best $C$ in Problem 16 and the best $D$ in Problem 18 agree with the best $(C, D)$ in Problems 11–14. That is because the two columns $(1, 1, 1, 1)$ and $(0, 1, 3, 4)$ are perpendicular.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 句中跨题引用的题号（Problem 16、Problem 18、Problems 11–14）按 OCR 原样保留，译者无法据此页数据逐题核实其与引用问题的对应关系；另需提请读者注意：按本页数据，两列 $(1,1,1,1)$ 与 $(0,1,3,4)$ 的内积为 $1\cdot0+1\cdot1+1\cdot3+1\cdot4 = 8\neq 0$，并不正交，原句结论应结合被引用问题（可能采用中心化或其他列向量）理解。

<span style="color:#2471a3;">**[problem]**</span> **Problem 21.**

For the closest parabola $b = C + Dt + Et^2$ to the same four points, write down the unsolvable equations $Ax = b$ in three unknowns $x = (C, D, E)$. Set up the three normal equations $A^T A x = A^T b$ (solution not required). In Figure 11.3a you are now fitting a parabola to 4 points—what is happening in Figure 11.3b?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 抛物线模型中丢失的二次项重建为 $Et^2$（OCR “b = C + 刀 + …”，未知数仅显式出现 $(C, D, E)$）；图号按本书图号体系（正文 Figure 11.3 的子图）修正：Figure 11.3a / Figure 11.3b（OCR 读作 “IIe3a / II.3b”）。

<span style="color:#2471a3;">**[problem]**</span> **Problem 22.**

For the closest cubic $b = C + Dt + Et^2 + Ft^3$ to the same four points, write down the four equations $Ax = b$. Solve them by elimination. In Figure 11.3a this cubic now goes exactly through the points. What are $p$ and $e$?

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 三次多项式重建为 $b = C + Dt + Et^2 + Ft^3$（OCR “C 十 刀 纟 + Et2 + 尹3” 中 “刀 纟” 为 $Dt$、数字 “2/3” 为 $t$ 的指数、“尹” 为 $F$）。四次数据恰可由三次曲线精确插值，故 $p = b$、$e = 0$。题号 22 未被 OCR 单独捕捉，按连续编号推断。

<span style="color:#2471a3;">**[problem]**</span> **Problem 23.**

The averages of the $t$'s and $b$'s are $\bar{t} = 2$ and $\bar{b} = 9$. Show that $C + D\bar{t} = \bar{b}$. Explain! (a) Verify that the best line goes through the center point $(\bar{t}, \bar{b})$. (b) Explain why $C + D\bar{t} = \bar{b}$ comes from the first equation in $A^T A x = A^T b$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 平均值记号重建：$\bar{t} = 2$、$\bar{b} = 9$（OCR 丢上方横线读作 “= 2 and b = 9”，“b” 前符号即 $\bar{\cdot}$），等式重建为 $C + D\bar{t} = \bar{b}$（OCR 将 $\bar{t}$ 误读为竖线 “丨”）；中心点（center point）$(\bar{t}, \bar{b})$。题号 23 未被 OCR 捕捉，按连续编号推断。

---

<!-- page 142: 书页 138, OCR page 42 -->

> <span style="color:#7f8c8d;">页眉 “Computations with Large Matrices（大矩阵的计算）” 与页脚页码 138 为重复性版式元素，不译。</span>

### II.3 Three Bases for the Column Space（列空间的三种基）

本节所触及的是严肃的 computational questions（计算问题）。这些 matrices（矩阵）会变得越来越大。若存在 random noise（随机噪声），它们的 rank（秩）也会相当大。但一旦除去噪声，effective rank（有效秩）就可能远小于 $m$ 与 $n$。modern linear algebra（现代线性代数）已经发展出快速算法（fast algorithms），用于求解大型矩阵的方程 $Ax = b$、特征值问题 $Ax = \lambda x$ 与齐次方程 $Ax = 0$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 节号 “11.3” 依上下文修正为 II.3；OCR 的 “solve = b and = /\æ and 鬱 = 0” 重建为求解 $Ax = b$、$Ax = \lambda x$、$Ax = 0$（“鬱”为 $Ax$ 的噪声，“/\æ”为 $\lambda x$）；“smaller than m and n” 中的 $n$ 被 OCR 并入下一词 “Modern”。

大部分专用的 special algorithms（特殊算法），我们会留给专业人士处理。数值线性代数（Numerical Linear Algebra）发展得又快又好——有这些专家把关，我们是安全的。但你我都应当认得几条最基本的 common computational sense（常规计算常识）规则，其中包括这两条：

- 当你能直接在 $A$ 上运算时，就不要使用 $A^T$ 与 $A^T A$。
- 不要假定 rows（行）与 columns（列）的原始顺序就必然是最好的。

第一条 warning（警告）适用于 least squares（最小二乘）、SVD（奇异值分解），也适用于 computational statistics（计算统计）。构造 $A^T A$ 相当于把 condition number（条件数）$\sigma_1/\sigma_n$ 平方了，而这个量度量的正是 $A$ 的 sensitivity（敏感性）与 vulnerability（脆弱性）。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接 + 第一性原理）：**</span> "$A^{T}A$ 把条件数平方"是法方程组灾难的浓缩。回看 Strang 前作《线性代数导论》§4.3：解最小二乘曾用正规方程 $A^{T}A$ x̂ = $A^{T}b$，代数上干净、数值上却最危险。用 SVD 一句话就能看懂：$A^{T}A$ 的特征值恰是 $\sigma_{1}^{2}$,…,$\sigma_{n}^{2}$，故 cond($A^{T}A$)=$\sigma_{1}^{2}$/$\sigma_{n}^{2}$=[cond(A)]$^{2}$。后果用 CSAPP 2.4 学过的 IEEE 双精度来度量：线性求解的相对误差量级约 $\kappa$·$\epsilon$_mach（$\epsilon$_mach≈2.2×$10^{-16}$）。若 $\kappa$(A)=$10^{6}$，正规方程把它推到 $10^{12}$，误差上界≈2×$10^{-4}$——能用的有效数字只剩三四位；数据矩阵中的噪声列还会被平方进一步放大。这就是"直接作用 A"的算法被称为 square root algorithm 的缘由：QR 先把 A 拆成正交 Q（条件数恰为 1）与上三角 R，病态全部显形于 R 而不再被平方；SVD 同理。正文提到刚度矩阵、电导矩阵与图拉普拉斯形如 $A^{T}CA$ 属例外——那是物理结构天然对称半正定、正定即良态，而非算法选择。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 条件数记号由 OCR 的 “伊 1 / 0” 重建为 $\sigma_1/\sigma_n$（最大与最小奇异值之比）。

对于真正巨大的矩阵，计算并存储 $A^T A$ 的代价简直不可想象。诚然，力学的 stiffness matrix（刚度矩阵）、电子学的 conductance matrix（电导矩阵）与网络的 graph Laplacian matrix（图拉普拉斯矩阵）都具有 $A^T A$ 或 $A^T C A$ 的形式（物理常数放在 $C$ 中）。但对 data matrices（数据矩阵）来说，我们想要的是能直接作用于基本矩阵 $A$ 的 “square root algorithms（平方根算法）”。

我们究竟需要从 $A$ 得到什么？这个问题的答案往往直指 pure and applied algebra（纯数学与应用代数）的核心：我们需要的是 column space（列空间）的一组好 basis（基）。有了这个出发点，我们几乎什么都能做！对 $Ax = b$，我们能找到 basic columns（基本列）的一个组合，使它接近 $b$；对 $Ax = \lambda x$，我们能算出精确的 singular vectors（奇异向量）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> “For = b, we can find a combination of basic columns 山 at comes near b / For 鬱 = …” 中的变量重建为 $Ax = b$ 与 $Ax = \lambda x$，“山 at” 为 that 的噪声。

还要再次强调，我们不能做的，是把 $A$ 的前 $r$ 个 independent columns（独立列）自动当作在 column space（列空间）$C(A)$ 中从事计算的一组好基。

> <span style="color:#1e8449;">**[note] 译者注（第一性原理洞察）：**</span> 三种基同答一个问题——列空间的基——却构成质量/代价的三角：SVD 的 U 全局最优但最贵；Gram–Schmidt+列主元给出标准正交基、贪心而廉价；直接取自 A 的列 C 零合成代价、最可解释。要读懂这套排序，关键是本页最锋利的观点：为什么 A 的前 r 个独立列不能自动当"好基"。独立（independent）只保证 $\sigma$_min>0，良态要求 $\sigma$_min 不与 $\sigma_{1}$ 差太远——两者之比每差 10 倍，后续计算就约丢一位有效数字（见本页前注）。数据矩阵里原始前 r 列往往高度相关，张成的平行体扁到行列式落入浮点抹平区，计算机里的"独立"形同退化。这正是 Strang 前作消元必须选主元的原因：主元要大而可靠、才不把误差放大。它预告了后面两次升级：列主元 QR 每步取范数最大的列（贪心），与 §II.3 下一页"行列式最大子矩阵"（全局最优），两者是"基质量"执念的两个版本。effective rank 的思想也在伏笔处：r 应取在噪声地板之上，$\sigma$_{r+1} 以下属于噪声、不该进基。

---

### Three Good Bases（三种好基）

让我立刻揭示我们建议研究的这三种基。你也许会忍不住给它们排成 gold（金）、silver（银）、bronze（铜）的顺序。这三个奖项在一定程度上代表了三种基的 guaranteed quality（有保证的品质），但它们同时也暗示 SVD 的代价最高。在为 column space（列空间）构造基这件事上，三者都是赢家。

1. 来自 SVD（奇异值分解）的 singular vectors（奇异向量）$u_1, \ldots, u_r$，且奇异值按降序排列 $\sigma_1 \ge \sigma_2 \ge \cdots \ge \sigma_r$。
2. 来自 Gram-Schmidt（格拉姆-施密特）过程的 orthonormal vectors（标准正交向量）$q_1, \ldots, q_r$，使用 column pivoting（列主元）。
3. 在 column exchanges（列交换）之后直接从 $A$ 取出的 independent columns（独立列）$a_1, \ldots, a_r$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 此三条 OCR 噪声极重（“ur 什 0 m the SVD, with 01 02 · 一 之 产”等），按 §II.2 的 SVD 记号重建为 $u_1, \ldots, u_r$、$q_1, \ldots, q_r$、$a_1, \ldots, a_r$，并补出奇异值降序条件 $\sigma_1 \ge \sigma_2 \ge \cdots \ge \sigma_r$。

对 $C(A)$ 的每一种基选择，都会在一个 “rank-revealing factorization（秩揭示分解）” 中给出 column matrix（列矩阵）：矩阵 $A$（$m\times n$ 型）等于 column matrix（$m\times r$ 型）乘以 row matrix（$r\times n$ 型），即

```math
A = \text{(column matrix)} \cdot \text{(row matrix)} : \qquad (m \times n) = (m \times r)(r \times n)
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 该分解式由 OCR “= column matnx ti mes row matrix ： (m by ） equals (m by r)(r by ）” 重建，原式的书写顺序为 $A =$（column matrix）（row matrix）。

---

> <span style="color:#7f8c8d;">Strang §II.3, p.138</span>

---

<!-- page 143: 书页 139, OCR page 43 -->

## II.3 Bases for the Column Space（列空间的基）

> <span style="color:#7f8c8d;">OCR 页眉 "11 3" 系 "II.3" 之误读；本节正式标题按术语表为 Three Bases for the Column Space（列空间的三种基），本页为书页 139。</span>

<span style="color:#2471a3;">**[section]**</span> 三种分解把列空间（column space）的一组基分别放进 $U$、$Q$ 与 $C$ 中，它们的因子（factors）如下：

1. 在缩减 SVD（reduced SVD）$A = U\Sigma V^T$ 中，因子为 $U_{m\times r}$ 乘以 $\Sigma_{r\times r}V_{r\times n}^T$。
2. 在格拉姆-施密特（Gram-Schmidt）分解 $A = QR$ 中，因子为 $Q_{m\times r}$ 乘以 $R_{r\times n}$。
3. 在主元消元（pivoted elimination）分解 $A = CZ$ 中，因子为 $C_{m\times r}$ 乘以 $Z_{r\times n}$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 上述三条中的分解式与因子尺寸均按数学语境重建：损坏的 OCR 片段 "$UT$ times $ErV$"、"$QmXr$"、"$Zrxn$" 分别对应 $U_{m\times r}$ 与 $\Sigma_{r\times r}V_{r\times n}^T$、$Q_{m\times r}$ 与 $R_{r\times n}$、$C_{m\times r}$ 与 $Z_{r\times n}$。

<span style="color:#2471a3;">**[note]**</span> 让我立即评述这三种重要分解（factorization）的性质：

1. $U$ 中的列基（column basis）$u_1,\dots,u_r$ 是标准正交（orthonormal）的；它还有额外性质（extra property）：第二因子 $\Sigma V^T$ 的各行也是正交（orthogonal）的。
2. $Q$ 中的列基 $q_1,\dots,q_r$ 是标准正交的；第二因子 $R$ 的各行并不正交，但它们是良态（well-conditioned）的，即安全独立（safely independent）。
3. $C$ 中的列基 $c_1,\dots,c_r$ 不是标准正交的；但 $C$ 与第二因子 $Z$ 二者都可以是良态的，这通过允许列交换（column exchanges）来实现——不只是允许，而是坚持（not just allowing but insisting）！$C$ 含有取自 $A$ 的 $r$ 个"好列"（good columns）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 以上三点中的 $u_1,\dots,u_r$、$q_1,\dots,q_r$、$c_1,\dots,c_r$ 及各形容词（OCR 噪声如 "or 0 or"、"or 0 刀 orm 况"、"研 or 叻 0g0" 等）均按三种分解的标准性质重建。

<span style="color:#2471a3;">**[section]**</span> 第三种分解 $A = CZ$ 可以称为插值分解（interpolative decomposition, ID），而不是 SVD 或 QR。由于它是本节的新思想，我下面集中讨论它的性质。

<span style="color:#2471a3;">**[note]**</span> Gunnar Martinsson（冈纳·马丁森）及其杰出合著者（distinguished coauthors）的注记与论文，是这次 ID 阐述的基础。

<span style="color:#2471a3;">**[note]**</span> $C$ 的列直接取自 $A$，而 $Z$ 的行并非如此——若要求行也直接取自 $A$，那就要求过高了（asking too much）。稍后我们将会看到 $CMR$ 分解：把 $A$ 的列放进 $C$、把 $A$ 的行放进 $R$，再用一个可逆的混合矩阵 $M$（invertible mixing matrix）使乘积接近 $A$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 上句中部为重度噪声（OCR 如 "columns of in C and rows of in 月 一"、句尾 "close t0"），按"列/行分解 + 可逆混合矩阵"的语境重建；$CMR$ 记法与后文将要出现的 $CUR$ 分解（$A \approx CUR$）相衔接。

## Interpolative Decomposition = Column/Row Factorization（插值分解 = 列分解/行分解）

<span style="color:#2471a3;">**[note]**</span> 与 $A = QR$ 和 $A = U\Sigma V^T$ 相比，$A = CZ$ 有四个重要优点（advantages）。请记住：$C$ 的列是 $A$ 的真实列——经过精心挑选的列，这给 $A = CZ$ 带来实在的优势。

> <span style="color:#1e8449;">**[note] Note（译者注：插值分解的四个优点——为什么真实列值钱）:**</span> 这类分解在英文里叫 interpolative decomposition（插值分解, ID），它的四个优点全由一个源头导出：$C$ 是 $A$ 的真实列，不是合成列。SVD 的左奇异向量 $u_i$ 是 $A$ 的 $n$ 个 columns（列）带符号的加权组合（原注这里写错了，原文写「全部 $m$ 列」；$m$ 是行数不是列数）。由 $Av_i=\sigma_iu_i$ 按列展开即得 $u_i=\sum_{j=1}^{n}v_{ij}a_j/\sigma_i$：$v_i$ 是 $n$ 维的，参加组合的正是 $n$ 列，结果落在 $m$ 维空间里，$m$ 只是那个空间的维数。出处见 Trefethen 与 Bau 的《Numerical Linear Algebra》Lecture 4 与 Golub 与 Van Loan 第 2 章，两处都以 $Av_j=\sigma_ju_j$ 定义左奇异向量；本节例 1 是 3 行 4 列，$n=4$、$m=3$，与后文「第一奇异向量大致是四列的加权和」正好对上；而合成向量本身，像 PCA 的 latent factor（潜在因子），数学上完美，却 humanly hard to know（从人的角度难以认识）——两个奇异向量之差没有工程语义，因为它不对应任何一个真实记录。$C$ 的每一列自带身份：数据矩阵里它对应第 2 个时刻、第 5 个用户、第 $k$ 个传感器的原始记录。于是优点 2、3 是自动的：sparse（稀疏）与 nonnegative（非负）是 $A$ 的性质，取子列不改写任何元素，故被原样继承；对 differential equation（微分方程）离散化得到的 $A$，$C$ 中的列仍是网格上的真实未知量，而不是混合出来的模态。优点 4 直接命中智能科学日后必遇之争：interpretability（可解释性）与 latent factor（潜在因子）之争，这就是机器学习里 feature selection（特征选择）与 sparse coding（稀疏编码）可读、PCA 最优但难懂的那场争论的线性代数原版。
> 
> 用本节例 1 的 $A$ 走一遍：它 3 行 4 列、秩 2，第 3 列恰是第 2 列的两倍，第 4 列与第 2 列相同。取列 1 与列 3 组成 $C$，解出 $Z=C^{+}A$，其第一行是 $(1,0,0,0)$、第二行是 $(0,0.5,1,0.5)$，残差 $\|A-CZ\|$ 的最大元是 $8.9\times10^{-16}$，精确重建。换成带列主元的 Gram-Schmidt，第一轮挑中列 3（当时残差范数 $7.4833$），第二轮挑列 1（残差范数 $0.4629$），两轮之后残差归零。代价上也省：一次带列主元的 QR 是 $O(mnr)$，SVD 是 $O(mn\min(m,n))$；取 $m=n=3000$、$r=25$，两者相差 $120$ 倍，这就是"用 $r$ 替换 $\min(m,n)$"的复杂度红利。
> 
> 代价那笔账还可以说得更狠：原注说省掉整台正交化与迭代机器，量化下来就是 QR 要维持整列正交性、SVD 要迭代求奇异值，而 ID 一旦锁定 $r$ 个好列，只需在 $C$ 上做消元把其余列表示成组合，正交化与特征迭代两套机器都不必开机。
> 
> 机制上，$C$ 选得好不好可以量化：$Z$ 的元素是用 $C$ 的列表示 $A$ 的列时的系数，两列近乎共线，系数就爆炸；$|z_{ij}|\le1$ 是没有任何一列过分依赖别的列的安全线。所以取真实列不是免费的礼物，它把负担从算正交基转到选对列：选错了，重建仍然精确（只要 $C$ 真是基），但数值上不可用。跨课程坐标：CLRS 6.006 一侧是复杂度对比 $O(mnr)$ 对 $O(mn^2)$，以及用随机化绕开最坏输入的算法范式；Strang 18.06 一侧是 SVD 与 PCA 的谱分解；6.042J 一侧是组合计数 $C(n,r)$，候选列子集的个数决定了挑最好到底有多难。史实上，这套方法在 2010 年代由 Martinsson 及其合作者系统化，本页正文点名的 Martinsson 注记正是入口；举个能直接看出来的对比：把例 1 的 $A$ 送进 SVD，第一奇异向量大致是四列的加权和，分量符号还有正有负；工程师拿到它，没法说它对应哪一列、哪一天、哪个传感器，而 $C$ 的第 2 列明明白白是第 3 号传感器的读数。还有一处实践细节：ID 的重建误差可以精确为零（只要 $C$ 真是列空间的一组基），精度问题全部转嫁到选列上，这正是 §II.4 要用随机化选列、而不是继续改进求解器的原因。另外，ID 只要求 $C$ 是真实列、$Z$ 的行是合成系数；若进一步要求行也取自 $A$，就得到 $CMR$ 分解（也记作 $CUR$），$M$ 是可逆的混合矩阵，本页后文正是这条路。本次未联网，具体年份与文献未能一手核实。

1. $A = CZ$ 花费更少的计算时间与存储，比 $A = U\Sigma V^T$ 与 $A = QR$ 都少。
2. 当 $A$ 稀疏（sparse）、非负（nonnegative）或二者兼备时，$C$ 也同样如此——因为 $C$ 直接来自 $A$。
3. 当 $A$ 来自对微分方程或积分方程（differential or integral equation）的离散化时，$C$ 中的列比 $U$ 与 $Q$ 中的标准正交基更有意义。
4. 当 $A$ 是数据矩阵（matrix of data）时，保留在 $C$ 中的列具有简单易懂的解释（interpretations）。

<span style="color:#2471a3;">**[note]**</span> 最后这三点能在计算完成后对我们理解输出产生重大差异。这一直是对 SVD 的批评：奇异向量（singular vectors）在代数上与几何上都完美，但"从人的角度"难以认识（humanly hard to know）。

<span style="color:#2471a3;">**[note]**</span> 当 $A$ 中的数字本质上是正数时，目标可能是非负矩阵分解（Nonnegative Matrix Factorization, NMF）——两个因子都可以是非负的。这对中等规模（moderate sizes）很重要，但在大数据（big data）的世界里要求太高。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 上句"两个因子均可非负"半句（OCR 为 "bo 叻 c 忉 MN…" 乱码）按 NMF 的定义（两个非负因子逼近 $A$）重建。

<span style="color:#2471a3;">**[note]**</span> 当 $Z$ 的条目很小（small entries）时，$A = CZ$ 正适合大型矩阵。

> <span style="color:#1e8449;">**[note] 译者注（第一性原理洞察）：**</span> "Z 的条目小"值得与后面 §II.3 的定理对读：Z 的每个元素是"非基本列在基本列坐标系下的表示系数"（本页后文的 $z_{j}$ 正是解 $Bz_{j}$=某列）。条目小有两重含义。其一，数值上安全：表示系数不大意味着非基本列是基本列的温和组合，远离"病态外推"——§II.3 将证明只要选行列式最大的 r 列作基，就能保证 |z_ij|≤1。其二，压缩上有利：Z 既然是 r×n 的稠密系数表，若大部分条目接近零，就可以设阈值砍掉小项，近似仍好——这与 Strang 前作 §7 讲 SVD 图像压缩同一逻辑：SVD 靠"小奇异值可弃"，ID 靠"小系数可弃"，都是"稀疏表示"思想在矩阵层面的表现。反过来，若某列在好基下的坐标出现大数，说明该列方向被严重拉伸或近乎共线，正是页面开头警告的 bad choice。这也是 §II.4 随机 CUR 后文里"为什么列由算法精心挑选而非随意取前 r 个"的伏笔。

---

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页末句括号内的数值示例（OCR "say 爿孓2"）严重损坏、无法可靠确定，译文按"条目很小"的语义作保留处理；此为本页（书页 139）的结尾。

---

> <span style="color:#7f8c8d;">Strang §II.3, p.139</span>

---

<!-- page 144: 书页 140, OCR page 44 -->

## Factoring $A$ into $CZ$（将 $A$ 分解为 $CZ$）

> <span style="color:#7f8c8d;">页眉重复元素 Computations with Large Matrices（与大型矩阵的计算）为章题，不译；本页为书页 140。</span>

<span style="color:#2471a3;">**[section]**</span> 当 $C$ 包含 $A$ 的列空间（column space）的一组基时，因子 $Z$ 就被完全确定了。

<span style="color:#2471a3;">**[note]**</span> $A$ 的每一列都是 $C$ 中那些基本列（basic columns）的唯一组合：

```math
(\text{column } j \text{ of } A) = (\text{matrix } C)(\text{column vector } z_j) \tag{1}
```

<span style="color:#2471a3;">**[note]**</span> 这正是 $A = CZ$ 的逐列（column by column）陈述。

<span style="color:#2471a3;">**[note]**</span> 这一思想在 §I.1 已经出现（当时用 $R$ 而不用 $Z$）。

<span style="color:#2471a3;">**[note]**</span> 它给出了行秩 = 列秩（row rank = column rank）的一个简洁证明；不过当时那个 $C$ 的列可能并不很独立。

<span style="color:#2471a3;">**[note]**</span> 本节很快将认真对待"又快又好地选择 $C$"这件事（但还不是现在）。

<span style="color:#2471a3;">**[section]**</span> 首先，我们可以通过考察 $C$ 的行空间（row space），迈出超越 $A = CZ$ 的一步。

<span style="color:#2471a3;">**[note]**</span> $C$ 在某处含有 $r$ 个独立的行；把这些行 $y_1,\dots,y_r$ 放进一个 $r\times r$ 矩阵 $B$，那么 $B$ 是可逆的。

<span style="color:#2471a3;">**[note]**</span> $C$ 的每一行都是 $B$ 中那些基本行（basic rows）的唯一组合：

```math
(\text{row } i \text{ of } C) = (\text{row vector } y_i)(\text{invertible matrix } B) \tag{2}
```

<span style="color:#2471a3;">**[note]**</span> 这正是 $C = YB$ 的逐行（row by row）陈述。把它与 $A = CZ$ 结合起来：

```math
A = CZ = YBZ \tag{3}
\qquad (m\times r)(r\times r)(r\times n)
```

<span style="color:#2471a3;">**[note]**</span> 所有这些矩阵的秩（rank）都是 $r$。

<span style="color:#2471a3;">**[note]**</span> 现在利用这一事实：$C$ 的列直接来自 $A$，而 $B$ 的行直接来自 $C$。

<span style="color:#2471a3;">**[note]**</span> 对这些列与行而言，（1）中的向量 $z_j$ 与（2）中的 $y_i$ 正来自单位矩阵（identity matrix）！

<span style="color:#2471a3;">**[note]**</span> 若你允许我假定 $z_j$ 与 $y_i$ 分别是 $A$ 与 $C$ 的前 $r$ 列与前 $r$ 行，那么 $A = YBZ$ 便具有特殊形式。写成分块（block）形式：设 $M$ 为 $A$ 左下角的 $(m-r)\times r$ 块、$N$ 为 $A$ 右上角的 $r\times(n-r)$ 块，则有：

> <span style="color:#1e8449;">**[note] Note（译者注：Schur 补的零化形态——秩 r 矩阵被一个块钉死）:**</span> 你正在 Boyd 凸优化附录 §A.5.5 学的 Schur complement（舒尔补）在这里以零化的形态出现。把秩 $r$ 的 $A$ 分块成左上 $B$、右上 $N$、左下 $M$、右下 $D$ 四块；若 $B$ 可逆，则 $A=YBZ$ 逼出 $D=MB^{-1}N$——Schur complement（舒尔补）$S=D-MB^{-1}N$ 恰好等于零矩阵。
> 
> ```math
> A = \begin{bmatrix} B & N \\ M & M B^{-1}N \end{bmatrix}
>   = \begin{bmatrix} I_r \\ M B^{-1} \end{bmatrix}
>     B \begin{bmatrix} I_r & B^{-1}N \end{bmatrix}
>   = YBZ
> ```
> 
> 这段可以读作：满秩子块一旦坐镇左上角，整个矩阵就被它内插锁定，右下块不再有独立自由度。这符合维数直觉：秩 $r$ 的矩阵只含 $r^2$ 个独立参数，全在 $B$ 内部，其余一切块都只是 $B$ 经过行、列线性变换的影子。
> 
> 例 1 可以逐项验算：$A$ 是 3 行 4 列、秩 2，左上 $B$ 取对角元 1 与 1、右上元素 2 的块，$M$ 是 $(1,3)$，$N$ 的两行是 $(4,2)$ 与 $(2,1)$，右下块则是 $(6,3)$。$B^{-1}$ 是主对角 1、右上 $-2$ 的矩阵；$MB^{-1}$ 算出 $(1,1)$，再乘 $N$ 得 $(6,3)$，与右下块逐元素相等。$Y$ 的三行是 $(1,0)$、$(0,1)$、$(1,1)$，$Z$ 的两行是 $(1,0,0,0)$ 与 $(0,1,2,1)$，代回 $YBZ$ 与 $A$ 的最大偏差是 $0$——浮点里也精确相等，因为这四步只做加减与乘 1。原注引的那条等式用 $B^{-1}$ 显式写出，结果为 $(6,3)$，复算一致。再做两个能当场验的实验。其一，把 $A$ 右下角最后一个元素从 3 改成 $3.001$，秩立刻跳到 3，最小奇异值掉到 $5.3\times10^{-4}$——分块判据是可以检验的：右下块比 $MB^{-1}N$ 多出 $10^{-3}$，秩就多 1。这也说明秩 $r$ 是精确的代数条件，浮点里它退化成阈值问题，$5.3\times10^{-4}$ 算不算零取决于阈值怎么选，阈值一换，$B$ 与 $Z$ 的形状就全变。其二，算一笔存储账：这个 $3\times4$ 矩阵有 12 个元素，秩 2 的自由度只有 $r^2=4$ 个，$12-4=8$ 个约束全压在某个 $2\times2$ 子块可逆上；把 $YBZ$ 用到 $m=n=10^6$、$r=10$，存储从 $10^{12}$ 降到 $2\times10^7$，相差约 $5\times10^4$ 倍，这就是低秩分解值钱的地方。
> 
> 顺带把符号对齐：Boyd 的 Schur 补写作 $S=D-CA^{-1}B$，本页记作 $S=D-MB^{-1}N$，字母换了、公式一字不差；本页的新意只是要求 $S=0$，于是分块矩阵塌成一对因子的乘积 $YBZ$。补一句实操提醒：本页 (4) 式在 OCR 里被拆得较散，验算比读字更可靠——把例 1 的四个块代进去，$YBZ$ 与 $A$ 的差必须是 $0$；差不为零，就说明某个块的位置或符号抄错了。这也解释了一句常被跳过的话——为什么秩 $r$ 的矩阵看起来总由少数几列生成：$B$ 一旦可逆，剩下的 $M$ 与 $N$ 只是 $B$ 的行组合与列组合，自由度全在 $B$ 里。
> 
> 分块标准形同时给出一个可验证判据：$\mathrm{rank}(A)=r$ 当且仅当右下块恰等于 $MB^{-1}N$。若右下块比这个值多出一点，秩就升到 $r+1$；这也解释了为什么秩亏矩阵看起来总有规律——它的每个元素都被少数几个参数锁住。机制上，$B$ 可逆是全部推导的前提：$B$ 若奇异，消元会在主元位置撞上零，必须换一个可逆的 $r\times r$ 子矩阵，而每个秩 $r$ 矩阵必在某处有这样的子矩阵，这就是本页后一句的来源。与 Strang 18.06 的 row rank（行秩）等于 column rank（列秩）殊途同归：同一个秩同时限制独立列数与独立行数，二者通过可逆子矩阵互相锁定。日后见到的任何 rank-$r$ 证明，包括 low-rank matrix completion（低秩矩阵补全）与 Boyd 里的低秩约束建模，都以此为底层几何。史实上，Schur complement（舒尔补）的名字来自 Issai Schur 1917 年前后的工作；本次未联网，年份与出处未能一手核实。

```math
A = \begin{bmatrix} B & N \\ M & M B^{-1}N \end{bmatrix}
= \begin{bmatrix} I_r \\ M B^{-1} \end{bmatrix}
B \begin{bmatrix} I_r & B^{-1}N \end{bmatrix}
= YBZ \tag{4}
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 上式所在区为重度 OCR 噪声区（可辨片段 "$C_{m-r}B^{-1}$"、"[ $B^{-1}Z_{n-r}$ ]"、"$B$ = submatrix of $A$" 等），已按"秩 $r$ 矩阵分块标准形 $A = [B\;N;\,M\;MB^{-1}N]$、$Y = [I_r;\,MB^{-1}]$、$Z = [I_r\;B^{-1}N]$"重建，并以例 1 数据自洽验证；原书此处排版的个别符号建议对照原书 PDF 核对。

<span style="color:#2471a3;">**[note]**</span> 我们其实只是假定 $A$ 的左上 $r\times r$ 角 $B$ 可逆。

<span style="color:#2471a3;">**[note]**</span> 每个秩为 $r$ 的矩阵都会在某个位置有一个可逆的 $r\times r$ 子矩阵 $B$！（也许这样的 $B$ 还不止一个。）

<span style="color:#2471a3;">**[note]**</span> 一旦 $B$ 位于那个左上角，消元（elimination）便能求出 $Y$ 与 $Z$。

> <span style="color:#1e8449;">**[note] Note（译者注：消元的侧记就是 Z——从行阶梯到可逆子矩阵）:**</span> 本页那句消元能求出 $Y$ 与 $Z$，其实复用了 Strang 18.06 的 Gaussian elimination（高斯消元）：把 $A$ 化到 row echelon form（行阶梯形）的过程中，每一步记录的是当前列如何由已选的 pivot column（主元列）线性表示，这些记录正是 $Z$ 的行。看例 1：$Z$ 的第二行是 $(0,1,2,1)$，直言第 3 列是第 2 列的两倍、第 4 列与第 2 列相同；第一行 $(1,0,0,0)$ 则说明第 1 列自己就是主元列。把消元真的跑一遍：第三行减去第一行得到 $(0,1,2,1)$，再减去第二行得到全零行——零行出现，正好宣布前两行是行空间的一组基，$r=2$。为什么记录的正是 $Z$？因为第 $j$ 列写成 $Cz_j$ 后，$z_j$ 就是这一列要用主元列怎样凑出来的系数；消元把第 3 列化成 $2$ 倍第 2 列、把第 4 列化成 $1$ 倍第 2 列，于是 $Z$ 的两列分别是 $(0,2)$ 与 $(0,1)$，拼起来正好是前面那个 $(0,1,2,1)$ 的第二行。换句话说，$Z$ 不是额外的计算，它是你早已做过的事情的账本。
> 
> 选错列会立刻塌：若把第 3、4 列当基，这两列共线，$C$ 的秩只有 1，条件数无穷大，$C^{+}$ 退化成最小二乘解，重建残差最大元 $0.357$——而取列 (1,2) 或列 (1,3) 都精确重建。这就是本页反复强调快速且良好地选列的分量：同一个 $A=CZ$ 框架，选列一换，结论从精确变成残差 $0.357$。
> 
> 另一侧的命题是：每个秩 $r$ 矩阵必在某处有一个可逆的 $r\times r$ 子矩阵。这是 6.042J 里 linear independence（线性无关）知识的精致推论，证明分两步走完。第一步，$\mathrm{rank}(A)=r$ 意味着存在 $r$ 个线性无关的列，把它们组成 $m\times r$ 矩阵 $C$；$C$ 列满秩，故 $C^TC$ 可逆。第二步，$C$ 的 $m$ 个行向量是 $\mathbb{R}^r$ 中的向量，$C$ 的行空间维数等于列空间维数 $r$，于是这 $m$ 个行向量张成整个 $\mathbb{R}^r$；在一组张成 $\mathbb{R}^r$ 的向量里必能挑出 $r$ 个线性无关的，它们对应的 $r\times r$ 行子块就可逆。若想绕开行秩等于列秩这一步，可以走 SVD：$A=U_r\Sigma_rV_r^T$ 中 $U_r$ 是 $m\times r$ 列正交矩阵，$U_r^TU_r=I_r$，它的 $m$ 个行向量必张成 $\mathbb{R}^r$，否则存在非零 $x$ 使 $U_r^Tx=0$，与 $U_r^TU_r=I$ 矛盾，故存在 $r$ 个线性无关的行。补一句限定：这样的 $B$ 未必唯一，本页后文的 $B_{\max}$ 只是行列式最大的那个。
> 
> 这个从秩到可逆子矩阵的桥，是 §II.3 后文找一个好的 $B$ 的理论底气，也是例 2 中 $B_{\max}$ 存在性的保证。机制上它还解释了为什么带列主元的消元总能走完：每步挑剩余列中范数最大者，等价于贪心地寻找那个可逆子块，$\sigma_{\min}$ 被逐步顶大，$Z$ 的元素就不至于爆炸。跨课程坐标：Strang 18.06 的消元与 $LU$ 分解给出算法形式，rank-nullity theorem（秩-零化度定理）给出维数账本，6.042J 的线性无关与基给出存在性论证的语言；CLRS 6.006 一侧则是消元本身的 $O(mnr)$ 复杂度账目。顺带指出原注一处可收紧的表述：说这个命题是线性无关知识的推论没错，但完整证明还必须用到行秩等于列秩，或等价的 SVD，只用列的线性无关推不出行子块可逆。

---

<span style="color:#2471a3;">**[example]**</span> **Example 1（例 1）.** 这个 $3\times 4$、秩为 2 的矩阵以一个可逆的 $2\times 2$ 矩阵 $B$ 开头：

```math
A = \begin{bmatrix} 1 & 2 & 4 & 2 \\ 0 & 1 & 2 & 1 \\ 1 & 3 & 6 & 3 \end{bmatrix},
\qquad
B = \begin{bmatrix} 1 & 2 \\ 0 & 1 \end{bmatrix}
```

```math
C = \begin{bmatrix} 1 & 2 \\ 0 & 1 \\ 1 & 3 \end{bmatrix}, \quad
Y = \begin{bmatrix} 1 & 0 \\ 0 & 1 \\ 1 & 1 \end{bmatrix}, \quad
Z = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 2 & 1 \end{bmatrix} \tag{5}
```

<span style="color:#2471a3;">**[note]**</span> 各矩阵尺寸为（3×2）（2×2）（2×4），可直接验证 $A = CZ = YBZ$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 例 1 的数字区 OCR 噪声严重（断行错位、重影等），已按"第 3 行 = 第 1 行 + 第 2 行"（秩 2 条件）与 $C$、$Y$、$Z$ 的尺寸及 $A = CZ = YBZ$ 的分解关系重建；重建后的数字与分解完全自洽。

---

> <span style="color:#7f8c8d;">Strang §II.3, p.140</span>

---

<!-- page 145: 书页 141, OCR page 45 -->
> <span style="color:#7f8c8d;">*页眉（running head）：Three Bases for the Column Space*</span>

请理解（Please understand）：如果 $C_{m-r}$ 或 $Z_{n-r}$（或二者同时）恰好含有很大的数值，那么（5）中的那些因子就是糟糕的选择（bad choice）。

若 $Y$ 与 $Z$ 中的其余分量都很小，我们最为满意（We are happiest）。

最理想的情形是 $|y_{ij}|\le 1$ 且 $|z_{ij}|\le 1$。

而我们的确能够找到一个使这一性质成立的子矩阵（submatrix）$B$！

把 $B$ 取为 $A$ 中行列式（determinant）最大的 $r\times r$ 子矩阵。

> <span style="color:#1e8449;">**[note] 译者注（证明策略模板 + 跨课程连接）：**</span> 这里的证明骨架是你在 6.042 反复用过的极值论证（extremal argument）：想证明"存在良态的 B"，就别显式构造，改证"取行列式最大的那个必然良态"。两个工具你都有：Strang 前作 §5.3 的 Cramer 法则把解写成行列式之比 z_ij = det(B 的第 i 列换成该列)/det(B)；分子恰是 A 的另一个 r×r 子矩阵的行列式。于是"det B 最大"一次性压住所有分子，|z_ij|≤1 不用算任何具体数——只有有限多个候选子矩阵，极值必然取到，这是极值论证不必依赖构造的本钱。同一命题还有几何读法：det=体积（前作 §5.3），det 最大意味着所选 r 列张成的平行体"最胖"——既不短、又尽量互不倾斜，$\sigma$_min 被顶到最大。因此 det 最大子矩阵是"全局最优的列主元"；而 §II.3 后文的列主元 QR 每步只取剩余列中范数最大者，是它降维后的贪心近似。反过来 |z|≤1 防的病态也直观：若某列与基本列近乎共线，其表示系数会趋于爆炸，界 1 就是安全线。

于是 $Y$ 与 $Z$ 的所有分量都满足 $|y_{ij}|\le 1$ 与 $|z_{ij}|\le 1$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 本页 OCR 噪声较重，已依数学语境重建：「蓋/風」等残缺形符 → 矩阵 $A$；「孓/引」→ $\le$；「一」→ 负号或减号；$C_m-B^{-1}$ 与 $B^{-1}Z_{n-r}$ 的下角标恢复为 $C_{m-r}B^{-1}$、$B^{-1}Z_{n-r}$。

这些 $y_{ij}$ 与 $z_{ij}$ 正是 $C_{m-r}B^{-1}$ 与 $B^{-1}Z_{n-r}$ 中的数。

我们先从 $Z_{n-r}$ 入手。

由于 $B(B^{-1}Z_{n-r})=Z_{n-r}$，我们知道 $B^{-1}Z_{n-r}$ 的每一列 $z_j$ 都求解如下线性方程组（system of linear equations）：

```math
B\,z_j=\bigl(Z_{n-r}\text{ 的第 }j\text{ 列}\bigr)
```

根据克莱姆法则（Cramer's Rule），解中的数 $z_{ij}$ 都是如下之比（ratio）：

```math
z_{ij}=\frac{\det\bigl(B\text{ 的第 }i\text{ 列被替换成该列之后}\bigr)}{\det(B)}
```

请记住 $B$ 是 $A$ 中行列式最大的 $r\times r$ 子矩阵。

分子中的矩阵正是我们当初没有选中的众多子矩阵之一。

它的行列式小于 $\det B$，所以 $|z_{ij}|\le 1$。

类似地，$Y$ 的各行来自 $C_{m-r}B^{-1}$。

因为 $(C_{m-r}B^{-1})B=C_{m-r}$，这些行求解线性方程组 $xB=$（$C_{m-r}$ 的某一行）。

转置并运用克莱姆法则时，$Y$ 的分量 $y_{ij}$ 再一次成为行列式之比，而 $\det B$ 依然充当分母！

由于 $\det B$ 已经尽可能大，我们得到 $|y_{ij}|\le 1$。

我们必须承认一个重大问题（problem）。

我们说"能找到 $B$ 使 $|y_{ij}|\le 1$、$|z_{ij}|\le 1$"，这其实并不为真。

现实中，我们找不到行列式最大的子矩阵 $B$。

除非借助量子计算机（quantum computer）——而它尚不存在。

$B$ 就在 $A$ 的内部某处，但我们完全无从知晓它究竟是哪一个子矩阵。

令人惊奇的是，借助随机化（randomization）我们能够识别出一个好的子矩阵 $B$。

> <span style="color:#1e8449;">**[note] Note（译者注：det 最大的子矩阵与随机化——从最坏保证到高概率保证）:**</span> 原文说找不到 det 最大的子矩阵除非量子计算机存在，这是修辞，真意是组合搜索不可行。但用词要收紧一档：固定 $r$ 时候选子矩阵的个数是 $C(n,r)$，它是 $n$ 的多项式（$n^r/r!$ 量级），严格说不叫超指数；真正致命的是常数——$n=10^6$、$r=50$ 时 $\log_{10}C(n,r)\approx235.5$，即要翻 $10^{235}$ 个候选才能确认最大，比可观测宇宙的原子数还多出几十个数量级。所以"除非量子计算机"这句修辞其实不需要量子：它需要的是一台一秒内扫完 $10^{235}$ 个矩阵的机器。只有当 $r$ 随 $n$ 一起增长时，$C(n,r)$ 才真正变成指数乃至超指数级别的量。这个用法在原文里是修辞，注里值得点明，免得把二项式系数误当超指数函数。
> 
> 证明骨架是 6.042J 反复用过的 extremal argument（极值论证）：想证明存在良态的 $B$，不要显式构造，改证取 determinant（行列式）最大的那个必然良态。工具是 Strang 18.06 的 Cramer's rule（克莱姆法则）：$z_{ij}$ 等于把 $B$ 的第 $i$ 列换成待表示列之后的矩阵行列式，再除以 $\det(B)$；分子恰是 $A$ 的另一个 $r\times r$ 子矩阵的行列式，于是 det $B$ 最大这一条一次性压住所有分子，$|z_{ij}|\le1$ 不用算任何具体数——只有有限多个候选，极值必然取到，这就是极值论证不必依赖构造的本钱。我把例 1 的 18 个 $2\times2$ 子矩阵全枚举了一遍：9 个非零，行列式取值只有 $-2$、$-1$、$0$、$1$、$2$；最大绝对值是 $2$，出现在前两行、第 1 与第 3 列，对应 $B_{\max}$；按 Cramer 公式算出的比值最大绝对值恰是 $1.0$，$|z_{ij}|\le1$ 被顶到上界但不是严格小于。
> 
> 同一命题还有几何读法：行列式是体积，det 最大意味着所选 $r$ 列张成的平行体最胖——既不短、又尽量互不倾斜，$\sigma_{\min}$ 被顶到最大。因此 det 最大子矩阵是全局最优的列主元；而 §II.3 后文的列主元 QR 每步只取剩余列中范数最大者，是它降维后的贪心近似。反过来 $|z|\le1$ 防的病态也直观：若某列与基本列近乎共线，表示系数会趋于爆炸，界 1 就是安全线。作者没有放弃良态保证，而是把它降级——从必然 $|y|,|z|\le1$ 放松到以极高概率 $|y|,|z|\le2$。这是一次范式跳跃：从最坏情形保证转向高概率保证，正是 CLRS 第 5 章随机化算法的思路，随机化快排的期望分析与随机哈希对抗最坏输入都是这一招，收益是把不可行搜索换成近线性随机采样。它成立还有一个先决条件值得玩味：det 最大的 $B$ 与随机 $B$ 之间只差常数因子 2，说明良态基在矩阵里是富集的，好子矩阵很多，随机扫几发就能撞上。这正是 §II.4 的核心赌注：把 $A$ 乘上随机矩阵 $A\Omega$，以高概率一次捕获 $r$ 维子空间。2 的常数裕量意味着即便 $B$ 挑得差些，计算仍有安全余量，所以放手随机不是赌博，而是有界的概率化计算。
> 
> 史实上，随机化数值线性代数在 2000 年代中后期成形，Drineas、Kannan、Mahoney 那一系列工作把采样与 CUR 分解推到台面上，Martinsson 等人随后给出更快的算法；本次未联网，具体年份与卷期未能一手核实。

---

于是存在非常高的概率（并非必然）使 $|y_{ij}|\le 2$ 与 $|z_{ij}|\le 2$。

因此，下一节将完成对插值分解（Interpolative Decomposition, ID）的完整介绍——即列或行直接取自 $A$ 的情形。

列与行的选取将是随机的，并配以精心设计的概率（probabilities）。

<span style="color:#2471a3;">**[example]**</span> **Example 2（例 2）**：例 1 中的矩阵 $A$ 具有如下行列式最大（等于 2）的子矩阵 $B_{\max}$；于是 $|Y_{ij}|\le 1$ 与 $|Z_{ij}|\le 1$ 都成立。

将 $A$ 的列按顺序 $1,3,2,4$ 重排后，分解式（6）写为：

```math
\begin{bmatrix}1&4&2&2\\0&2&1&1\\1&6&3&3\end{bmatrix}
=\begin{bmatrix}1&0\\0&1\\1&1\end{bmatrix}
\begin{bmatrix}1&4\\0&2\end{bmatrix}
\begin{bmatrix}1&0&0&0\\0&1&\tfrac12&\tfrac12\end{bmatrix}\quad(6)
```

其中 $B_{\max}=\begin{bmatrix}1&4\\0&2\end{bmatrix}$（$\det B_{\max}=2$），$Y=\begin{bmatrix}1&1\end{bmatrix}$，$Z=\begin{bmatrix}0&0\\\tfrac12&\tfrac12\end{bmatrix}$，即 $A=YB_{\max}Z$ 的列、行重排形式。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> Example 2 的 OCR 数字矩阵损坏严重（原文仅剩 "1 2 4 2 / 1 4 1 / = 0 1 2 1 …" 等碎片），无法逐位还原。此处按正文约束重建：$A$ 为秩 2 的 $3\times4$ 矩阵（第 3 行 = 第 1、2 行之和，第 3 列 = 第 2 列的 2 倍，第 4 列 = 第 2 列），取第 1、2 行与第 1、3 列得 $\det B_{\max}=2$，且 $Y$、$Z$ 的分量均不超过 1，与文中论断吻合。矩阵具体元素请以原书为准。

---

---

> <span style="color:#7f8c8d;">Strang §II.3, p.141</span>

---

<!-- page 146: 书页 142, OCR page 46 -->
> <span style="color:#7f8c8d;">*页眉（running head）：Computations with Large Matrices*</span>

<span style="color:#2471a3;">**[section]**</span> **CMR Factorization: Selecting C and R（CMR 分解：选取 $C$ 与 $R$；亦称 CUR 型分解，decomposition）**

现在我们描述一种推荐的选取方式：把 $A$ 的列与行直接放进 $C$ 与 $R$。

要实现 CMR 分解，总需要一个混合矩阵（mixing matrix）$M$。

若 $A$ 确实具有低秩（low rank），这可以成为等式 $A=CMR$。

对于近似低秩（approximately low rank，这正是我们的假设）的大型矩阵，我们可以从奇异值分解（Singular Value Decomposition）$A=U\Sigma V^T$ 出发，取其中的近似奇异向量（approximate singular vectors）。

我们将利用 $U$ 与 $V$ 得到一个贴近 $A$ 的秩 $r$ 分解（rank $r$ factorization）$CMR$。

我们的向导是 D. C. Sorensen 与 M. Embree 的论文 *A DEIM induced CUR factorization*（arXiv:1407.5516v2，2015 年 9 月 18 日；发表于 SIAM J. Scientific Computing 38（2016）1454–1482）。

离散经验插值方法（Discrete Empirical Interpolation Method, DEIM）负责选出 $C$ 与 $R$。

我们把中间矩阵记为 $M$ 而不是 $U$。

初看有些奇怪：$CMR$ 直接使用 $A$ 的列与行，却始于 $A=U\Sigma V^T$——后者给出的是那些列与行的标准正交（orthonormal）组合。

而对 $A=U\Sigma V^T$ 的近似计算又往往始于 QR，以便快速得到一个正交矩阵（orthogonal matrix）$Q$。

于是，列空间（column space）的基 $C$、$Q$ 全部由快速算法联系在一起。

最终近似的精度受 $A=U\Sigma V^T$ 中下一个奇异值（singular value）$\sigma_{r+1}$ 以及与我们为 $C$、$R$ 所作选择相对应的 $U$、$V$ 的各 $r$ 个列控制：

```math
A=U\Sigma V^T\quad(7)
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 原 OCR 中 $A=U\Sigma V^T$ 记为 "UEVT"/"蓋 = UEVT" 且本页仅见公式编号 "（7）"，此处将编号（7）重建为奇异值分解公式本身；它对应的 $r$ 个列选入 $C$、$R$。

<span style="color:#2471a3;">**[section]**</span> **Selection of Columns from $A$ to Enter $C$（从 $A$ 中选取进入 $C$ 的列）**

从 $U_{m\times r}$ 的 $r$ 个列开始——它们是 $A$ 的近似左奇异向量（left singular vectors）。

设 $E_{m\times s}$ 的 $s$ 个列直接取自单位阵（identity matrix）$I_m$（即选中 $s$ 个行位置的选择矩阵，selection matrix）。

若 $E^TU$ 是可逆矩阵（invertible matrix），那么 $P=U(E^TU)^{-1}E^T$ 满足 $P^2=P$，即 $P$ 是投影矩阵（projection matrix）。

并且 $P$ 在这 $s$ 个被选中的位置等于单位阵 $I$，所以 $P$ 是一个插值投影（interpolatory projection）。

> <span style="color:#1e8449;">**[note] Note（译者注：DEIM 插值投影——幂等与插值如何同时成立）:**</span> 插值投影 $P=U(E^TU)^{-1}E^T$ 的两个性质可以完全用已掌握的计算验证。其一 $P^2=P$：把 $P\cdot P$ 展开，中间出现 $E^TU\cdot(E^TU)^{-1}=I$ 互相消掉，剩下的还是 $U(E^TU)^{-1}E^T=P$——projection matrix（投影矩阵）的幂等是逐项代数消去的自然产物。其二插值性：$E^TP=E^TU(E^TU)^{-1}E^T=E^T$，即 $P$ 在 $s$ 个被选坐标上等于恒等——在采样点精确插值、在别处用 $U$ 的列外推，这正是 interpolatory（插值型）一词的来源。两点我都在一个 3 行 2 列的正交 $U$ 上验过：按取最大分量的规则先选第 3 行、再选第 2 行，$E^TU$ 的行列式是 $-0.5774$、非零，算出 $P$ 之后 $P^2-P$ 的最大元是 $0$、$E^TP-E^T$ 的最大元也是 $0$，机器精度内精确成立。
> 
> 可逆条件 $E^TU$ 不是技术性假设，它就是 6.042J 的 linear independence（线性无关）检验：要求被选的 $s$ 个行位置在 $U$ 的行向量族中张成满维，即用 $s$ 个坐标把 $U$ 列空间的形状钉住。回看 §II.3 那句秩 $r$ 矩阵必含可逆 $r\times r$ 子矩阵，$E^TU$ 可逆正是该命题施加在 $U$ 上的实例——$U$ 列满秩 $s$，它的 $m$ 个行向量必张成 $\mathbb{R}^s$，于是存在 $s$ 个线性无关的行。所以 DEIM 每加一个坐标都隐含一次独立性维护，与主元消元护着 pivot 不小是同一个动作的两副面孔。DEIM 的选法还值得从算法角度重读：第 $s$ 步不取 $u_s$ 自身的最大分量，而取前一步插值没抓住的残差 $u_s-P_{s-1}u_s$ 的最大分量位置——这是典型的 residual-driven（余量驱动）贪心，已插值好的坐标不再重复投资，火力全压在最没表示好的方向。
> 
> 它与消元每次挑最大主元同构：主元是当前最危险的入口，先吃掉它可以防止后几步拿小除数放大误差，这是数值稳定性的第一性原理，也是 CSAPP 第 2 章 floating point（浮点）对消教训的必然要求。与 6.006 里多数只能当启发式的贪心不同，本页的误差界给了它可证的后验保证：$\|A-C(C^TC)^{-1}C^TA\|_2\le q_c\sigma_{r+1}$，精度只受第 $r+1$ 个奇异值控制，$q_c$ 是量级不到 100 的常数。这意味着 $r$ 是用户旋钮：谱尾衰减越快、矩阵越接近低秩，DEIM 的误差掉得越快。正文随后说理论上的快速增长在实践中从未出现，这是把数值线性代数界的经验事实复述了一遍：主元增长因子的最坏上界与平均表现之间通常差好几个数量级，这与 CSAPP 第 6 章 cache（缓存）预取的最坏情形分析一样，界只是保险，不是预测。再补一个直观的读法：$P$ 的秩等于 $s$，本例里是 2，因为 $P$ 的像就是 $U$ 的列空间、而 $P$ 在每个像点上又是恒等；这意味着 $P$ 只保留 $s$ 个自由方向，其余 $m-s$ 维全被投掉。若 $E^TU$ 奇异，$P$ 这个式子根本写不出来，DEIM 只能改用伪逆并接受更大的误差，可见可逆性是算法的前提，而不是事后的运气。史实上，DEIM 由 Chaturantabut 与 Sorensen 在 2010 年前后提出，本页所据的 Sorensen 与 Embree 论文是 2015 年的 arXiv 稿、2016 年发表在 SIAM J. Scientific Computing 第 38 卷；本次未联网，卷期与页码按本页正文转录，未能一手核实。

---

关键性质正是这第 2 条（全部证明见 Sorensen 与 Embree 的论文）。

对 $s=1$，DEIM 算法选取第一个奇异向量 $u_1$ 中的最大分量，于是得到 $P_1$。

下一个选择（导致 $P_2$）由 $u_2-P_1u_2$ 的最大分量决定。

此后每一个 $P_s$ 都由 $u_s-P_{s-1}u_s$ 的最大分量决定。

这相当于在普通消元（elimination）中让每个主元（pivot）都取到最大。

> <span style="color:#1e8449;">**[note] Note（译者注：DEIM 的余量驱动选择）:**</span> 前文说的 DEIM 展开是 discrete empirical interpolation method（离散经验插值方法），它解决的问题是：给定 $m\times r$ 的基矩阵 $U$，如何挑出 $s$ 个行位置组成 selection matrix（选择矩阵）$E$，使 interpolatory projection（插值投影）$P_s=U_s(E^TU_s)^{-1}E^T$ 同时满足幂等 $P_s^2=P_s$ 与采样等式 $E^TP_s=E^T$。第一条说它是投影，第二条说它在被选中的坐标上恰好等于恒等、在其余坐标上借 $U_s$ 的列做外推，插值一词的全部内容就在这里。设计自由度只剩一个：选哪 $s$ 个行。
> 
> 这个方法的原始动机不在矩阵分解，而在非线性模型降阶：一个非线性项要在 $m$ 个网格点上求值，代价随 $m$ 增长，DEIM 只在这 $s$ 个被选中的点求值，再乘上 $U(E^TU)^{-1}$ 把结果搬回全空间。于是 $s$ 必须远小于 $m$，而 $P_s$ 的插值性保证搬回来的近似在采样点上精确、在别处按 $U$ 的形状延拓。这也解释了判据为什么必须稳定：任何一个重复的采样点都等于白花一次求值预算，还让 $(E^TU)^{-1}$ 失去意义。
> 
> 规则若写成「第 $s$ 步取 $u_s$ 的绝对值最大分量」，直觉上最省事，但基向量彼此不正交时它会重复命中同一坐标。取四行三列、列已单位化但未正交化的基：第一步取 $u_1$ 最大分量落在行 0，第二步照同一规则取 $u_2$ 最大分量仍落在行 0，$E^TU$ 于是有两行完全相同，行列式 $8.56\times10^{-17}$、condition number（条件数）$3.46\times10^{16}$，求逆在浮点里已经不存在。改取 residual（残差）$u_s-P_{s-1}u_s$ 的最大分量，第二步落到行 1、第三步落到行 2，行列式 $0.2163$、条件数 $8.55$。两种规则差的不是精度，而是公式有没有定义：残差规则保证新坐标在已选坐标之外仍有分量，这正是 $(E^TU)^{-1}$ 存在的前提。
> 
> 这条规则与 elimination（消元）里每步挑最大 pivot（主元）是同一个动作：主元取最大，为的是后面当除数的数不缩小；残差取最大，为的是新坐标带来的信息量最大。保证方式却不同：列主元消元只有「growth factor（增长因子）的最坏情形没有好上界」这类经验说法，DEIM 有干净的误差界 $\|f-P_sf\|_2\le C\|(I-UU^T)f\|_2$，$u_i$ 正交时 $C=\|(E^TU)^{-1}\|_2$——这两行是 Chaturantabut 与 Sorensen 自己的讲义里逐字给出的（论文为 SIAM J. Sci. Comput. 32 卷 5 期 2737 至 2764 页，2010；引出它的引理编号未能一手核实）。**原注这里写错了**：它把 $q_c$ 说成「量级小于 100」的普适常数，而这样的普适上界不存在。$U$ 列正交时 $\|E^TU\|_2\le1$，故 $\|(E^TU)^{-1}\|_2\ge1$；把选中的几行挑到近乎共面，它就可以任意大。我实测过：2000 个随机 $9\times3$ 正交基、枚举全部 84 个选点（16.8 万组），该范数的最大值达到 $4.763\times10^{5}$，远远越过 100；而贪心 DEIM 选点在同一批基上只给出 1.163 到 3.848，中位数 1.900。所以「实践里 O(1) 到 O(10)」描述的是贪心规则的表现，不是定理：选点病态，放大就跟着病态，界随之退化甚至失效；先前那轮 200 个随机矩阵得到的 62.922 也只是采样没撞上坏点。后来者的工作正为此改规则——Drmač 与 Gugercin 的 Q-DEIM 专门给出更紧的先验界，本身就说明原界的常数既不普适也不小。CUR 一侧同理：Sorensen 与 Embree 证明误差被某个只依赖所选子矩阵条件数的因子放大，同样没有普适数字。
> 
> 史实坐标：DEIM 由 Chaturantabut 与 Sorensen 在 SIAM J. Sci. Comput. 32 卷 5 期（2737 至 2764 页）提出，本文引的 Sorensen–Embree 版本是 arXiv:1407.5516v2（2015 年 9 月 18 日），2016 年发表于同刊 38 卷 1454 至 1482 页，为 CUR 型分解补上了完整误差证明；这两篇的一手原文本机取不到，卷期按书目记录，属未能一手核实。跨课程上，它与 Strang 18.06 的消元主元、投影矩阵同构，界里那步代数消去用 6.042J 的归纳与正交分解，「主元不能太小」的数值后果在 CSAPP 第 2 章的浮点舍入里被重讲一遍。下一个该拿下的是 §II.4 的 randomized algorithm（随机化算法）：它把逐列贪心换成一次随机投影，选列代价从反复扫描降到一次矩阵乘法。

在 [Sorensen-Embree] 中有这段算法的简单伪代码（pseudocode）。

要进入 $R$ 的 $A$ 的各行以同样的方式选取。

与基于 $U$、$V$ 全部行范数（row norms）的范数平方采样（norm-squared sampling）相比，这种逐次处理（sequential processing）带来一大优势。

下一步是估计插值投影中的误差：

```math
\bigl\|A-C(C^TC)^{-1}C^TA\bigr\|_2\le q_c\,\sigma_{r+1}
```

```math
\bigl\|A-A R^T(RR^T)^{-1}R\bigr\|_2\le q_r\,\sigma_{r+1}\quad(8)
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 公式（8）第二式的 OCR 字形残缺（"日 风 一 毳 T T ） 一 1 月 日 + 1"），已依行插值投影 $R^T(RR^T)^{-1}R$ 的数学语境重建为对行空间（row space）的误差界；$q_c$、$q_r$ 为量级不超过 100 的小常数。

在实践中，常数 $q_c$ 与 $q_r$ 都不大（量级小于 100）。

这又与主元法（pivoting）相似：理论上的快速增长是可能的，但在实践中从未出现过。

---

> <span style="color:#7f8c8d;">Strang §II.3, p.142</span>

---

<!-- page 147: 书页 143, OCR page 47 -->

> <span style="color:#7f8c8d;">运行页眉：3. Bases for the Column Space；本页为书页 143（OCR page 47）。</span>

### 3. Bases for the Column Space（列空间的基）

#### The Mixing Matrix M（混合矩阵 $M$）

关键在于等式 $A = CMR$ 中如何选取混合矩阵（mixing matrix）$M$。

若没有这个矩阵 $M$，乘积 $CR$ 通常并不会接近 $A$。

对 $M$ 而言，一个自然的选取（natural choice）是

> <span style="color:#1e8449;">**[note] Note（译者注：混合矩阵 M 与两个最小二乘）:**</span> 矩阵的乘积 $A=CMR$ 里，$M$ 不是装饰，它是两个坐标系之间的换算表。$C$ 的列是 $A$ 的若干真实列，$R$ 的行是 $A$ 的若干真实行，两者各自带着 $A$ 的刻度，但列空间的基与行空间的基一般不是互为对偶的两组，直接把 $C$ 与 $R$ 相乘等于把两种刻度硬乘。正文给的选取是 $M=(C^TC)^{-1}C^TA\,R^T(RR^T)^{-1}$，把它读成 $C$ 的 left inverse（左逆）、$A$、$R$ 的 right inverse（右逆）三者的乘积，即 $M=C^{+}AR^{+}$，就是 least squares（最小二乘）在两个方向各做一次的产物。
> 
> 具体数字最能说明「没有 $M$ 时 $CR$ 不接近 $A$」。取 $4\times 5$ 的整数矩阵 $A=\begin{bmatrix}1&2&4&5&6\\2&1&5&4&3\\1&0&2&1&0\\3&1&7&5&3\end{bmatrix}$，它等于 $\begin{bmatrix}1&2\\2&1\\1&0\\3&1\end{bmatrix}\begin{bmatrix}1&0&2&1&0\\0&1&1&2&3\end{bmatrix}$，秩为 2、奇异值 14.912 与 3.694、$\|A\|_F=15.362$。$C$ 取第 1、5 列，即 $\begin{bmatrix}1&6\\2&3\\1&0\\3&3\end{bmatrix}$；$R$ 取第 3、4 行，即 $\begin{bmatrix}1&0&2&1&0\\3&1&7&5&3\end{bmatrix}$。于是 $\|A-CR\|_F=64.343$，是 $\|A\|_F$ 的四点二倍，比零矩阵（距离 $15.362$）还差得远。代入 $M^{*}=C^{+}AR^{+}=\begin{bmatrix}1&0\\-1&1/3\end{bmatrix}$ 后 $\|A-CM^{*}R\|_F=5.66\times10^{-15}$，正规方程残差 $\|C^T(A-CM^{*}R)R^T\|_F=4.21\times10^{-13}$；再对这个 $2\times 2$ 的 $M$ 加 2000 组标准差 $10^{-3}$ 的高斯扰动（`default_rng(7)`），残差 2000 次全部变大。
> 
> 为什么必须是 $C^{+}AR^{+}$：把 $M$ 当未知量，$\|A-CMR\|_F^2$ 对 $M$ 的每个元素求偏导并置零，得到 $C^T(A-CMR)R^T=0$，两边左乘 $(C^TC)^{-1}$、右乘 $(RR^T)^{-1}$ 即得上式。这是对 $M$ 线性的最小二乘：$C$ 与 $R$ 固定时它对 $M$ 就是最普通的线性最小二乘，所以有闭式解（把它叫 bilinear（双线性）最小二乘并不准确，双线性指两个变量各自线性，而这里 $C$ 与 $R$ 是固定的常量，只有 $M$ 在变）。解只是两个 $r\times r$ 线性系统，但代价不能只数这两步：组装 $C^TA$ 要把 $m\times n$ 乘成 $r\times n$，那一步是 $O(mnr)$，它才是主导项，总代价 $O(mnr+mr^2+nr^2)$，仍远低于直接对 $A$ 做 singular value decomposition（奇异值分解）的 $O(mn\min(m,n))$。令 $M=I$ 就塌回 $CR$，上面那组数字说明塌得多彻底；$C$ 只留第 1 列、秩不够时无论 $M$ 怎么选，最小残差停在 11.451（只留第 1 列时的最小二乘最优），缺失的那一维不在 $C$ 的列空间里，换算补不回来。
> 
> 修正原注一处过强的说法：原注称该 $M$「恰好无损于前 $r$ 个奇异值方向」，这只在 $C$ 的列空间与 $R$ 的行空间恰好张成前 $r$ 个奇异子空间时成立。按这种对齐情形复算（取 $B=\operatorname{diag}(9,4,1,0.3)$、$r=3$，$C$ 与 $R$ 分别取其前三个左、右奇异向量），$\|B-CMR\|_2$ 恰为 $0.3000$，正是 $\sigma_4$，因为此时 $CMR$ 精确等于 $B_3$。但一般选列时误差被一个只依赖所选子矩阵条件数的因子放大，它不是普适常数——那一对误差界里 $q_c$（上一条无编号的 display）与 $q_r$（式 (8)）正是这两个系数，也与同文 page_146 那条「$q_c$ 无普适上界」的 note 自洽。跨课程上，这就是 Strang 18.06 的 §4.3 最小二乘与投影矩阵套用两次，$C^{+}C=I_r$ 与 $RR^{+}=I_r$ 是满秩情形的左逆、右逆；史实上这类骨架式分解叫 pseudoskeleton approximation（伪骨架近似），Goreinov、Tyrtyshnikov、Zamarashkin 于 1997 年在 Linear Algebra Appl. 261 卷提出，一手原文未能核实。
> 
> 值得补一句为什么非要真列真行。SVD 给的是 $U$ 与 $V$ 的线性组合，系数一负，读者就说不清第 3 个列向量代表哪个样本；$C$ 与 $R$ 直接取自数据的行列，每个元素都能指回原始表格，这是 CUR 型分解在推荐系统、基因表达这类需要解释的场合被偏爱的唯一理由。代价也清楚：选列是组合问题，精确最优要枚举子集，工业实现全是贪心或随机化近似，误差界里的常数就是这份妥协的价格。
> 
> 再记一个容易被忽略的量：这组 $C$ 与 $R$ 的条件数分别是 3.288 与 11.421，属于中等偏好的情形；若换成高度相关的列，条件数会升到 $10^{6}$ 量级，$C^{+}$ 与 $R^{+}$ 自身的误差随之放大，$M$ 算得再准也追不回来。所以选列算法必须同时看两件事：被丢掉的尾部能量，与被选中子矩阵的良态性，前者决定 $\sigma_{r+1}$ 前面的那个系数里有多少是 $1$，后者决定这个系数的量级。这也是 DEIM 用残差而不是用范数挑点的另一半理由。下一个该拿下的是 §II.4 的随机化算法，它把选 $C$、$R$ 的代价再压一个量级。

```math
M = (C^TC)^{-1}C^TA\,R^T(RR^T)^{-1} = [\text{left inverse of } C]\,A\,[\text{right inverse of } R]
```

（9）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 原文公式被 OCR 读作「(CTC)-ICTART(RRT)—I…= [left of C] of …」，上标 $-1$ 全部丢失、第二行等式仅存碎片。此处按数学语境重建：$C$ 取左逆 $(C^TC)^{-1}C^T$、$R$ 取右逆 $R^T(RR^T)^{-1}$，故 $M = \text{左逆}(C)\cdot A\cdot\text{右逆}(R)$。</span>

在 <span style="color:#7f8c8d;">§I.1</span> 的最后一页，正是这一选取使得等式 $A = CMR$ 精确成立。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 此处为 `Section I.I`（大写 I 后接点再接 I），易与 §II.1 混淆；按所指内容——$A = CMR$ 的三因子分解（本节开头的骨架形式）首次出现于书首 §I.1 的矩阵乘法讨论（与本书 page_144 自引「这一思想在 §I.1 已经出现」同指）——判定为 §I.1。

在那一页上，矩阵 $A$ 的秩恰好等于 $r$——那时的我们还算天真（we were innocent then）。

而如今，$r$ 只是一个大矩阵的近似秩（approximate rank）而已。

对于 <span style="color:#7f8c8d;">§II.4</span> 的随机化算法（randomized algorithms）——那里的 $A$ 太大，DEIM 算法已无法适用——你会看到 Halko–Martinsson–Tropp 与 Mahoney–Drineas 也作出了同样的选取。

Stewart 的早期分析（Numer. Math. 83（1999）313–323）为（8）式中的误差估计（error estimate）指明了道路。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 期刊名 OCR 仅存「me Math.」碎片，依卷期 83（1999）313–323 复原为 Numerische Mathematik 的缩写 Numer. Math.；「HaIko」→ Halko。</span>

#### Starting from $A = QR$ with Column Pivoting（从带列主元的 $A = QR$ 出发）

对于含大型矩阵的数值线性代数（numerical linear algebra）而言，QR 分解（factorization）是一个备受偏爱的出发点（starting point）。

它以合理的代价，在 $Q$ 中为 $A$ 的列空间（column space）生成一组标准正交基（orthonormal basis）。

从 $Q$ 出发，我们可以快速而精确地转向另外两种基本基：

- 列 $C$ 的列——直接取自 $A$：插值分解（interpolative decomposition，ID）$A = CDR$；
- 列 $U$ 的列——标准正交向量：奇异值分解（singular value decomposition，SVD）$A = U\Sigma V^T$。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 第一项中「commg directly 什 om」→ coming directly from，「lnterpolatory Decomposition 蓋 = CDfR」按语境重建为插值分解 $A = CDR$（$D$ 为 $r\times r$ 中间矩阵）；第二项「UEVT」→ $U\Sigma V^T$。</span>

请理解，$C$ 与 $U$ 的良好选择，依赖于 $Q$ 的良好选择。

由于矩阵 $Q$ 是正交矩阵（orthogonal），从而具有理想的条件数（perfectly conditioned），因此决定 $A = QR$ 之质量的，是另一个因子 $R$。

<span style="color:#7f8c8d;">§II.2</span> 中普通的格拉姆–施密特（Gram–Schmidt）过程，保持了 $A$ 各列的原有顺序。

主元 QR（pivoted QR）则在每一步开始时，选取剩余各列中范数最大的一列——即列主元（column pivoting）。

> <span style="color:#1e8449;">**[note] Note（译者注：列主元 QR 与秩的现场显形）:**</span> 列主元 QR 做的是一件很朴素的事：把「哪几列值得当基」这个判断塞进消去过程本身，而不是等分解完了再回头看。形式是 $AP=QR$，其中 $P$ 是 column permutation（列置换），$Q$ 是 orthogonal matrix（正交矩阵），$R$ 为上三角，且第 $k$ 步在剩余列里挑范数最大的一列换到第 $k$ 位。按 $r$ 分块之后，两个近似式 $\sigma_{\min}(R_{11})\approx\sigma_r(A)$ 与 $\sigma_{\max}(R_{22})\approx\sigma_{r+1}(A)$ 合起来就叫 rank revealing（秩揭示）：秩不是事后算出来的，是分解进行到某一步时自己显形。
> 
> 差距可以量化。取一个 $5\times 3$ 矩阵，第一个列向量是第二个的 0.999 倍再加 0.001 倍的第三个，真实秩为 2（奇异值 1.999 与 1.732）。不换列的 QR 给出对角 $1.4128,\ 0.001734,\ 0$，第二个对角元比第一个小近三个量级；若停机判据只看对角元、界取相对量级 $10^{-2}$，第 2 步就会误判秩为 1，而实际第二列与第三列独立。换列后置换为 $[2,1,0]$，对角变成 $1.732051,\ 1.414214,\ 0$，两个非零元同量级，秩 2 当场显形。更大规模上，$60\times 40$、秩 3 的矩阵（奇异值 52.79、40.26、28.67）做部分 QR，对角前三个是 $-22.92,-12.91,-12.60$，第四步直接掉到机器零，停机条件一眼可读。
> 
> 去掉列主元会塌成什么：$R$ 的对角元可以任意小，而 $A$ 的秩不变。固定列序时对角元只反映「按给定顺序消去后的剩余长度」，既不单调也不可靠，任何基于 $|R_{kk}|$ 的停机判据都会漏判。代价有两项：每步要更新剩余列的范数，用降范数公式可把总代价保持在 $O(mnr)$，与 QR 本身同阶；列序被打乱，必须靠 $P$ 记回原始位置。原注说 $R_{11}$「吞下大奇异值」，这句要改：$A$ 与 $R$ 的奇异值满足交错不等式，$R_{11}$ 只是承载前 $r$ 维的近似块，说它吞下大奇异值会把「近似」说成「等于」。原文把它称作最大行列式策略的「连续版本」也不准确：max volume（最大体积）选列是组合优化，列主元 QR 是它的贪心近似，两者是近似关系而非连续化关系。
> 
> 跨课程上，列主元与 Strang 18.06 消元里的 pivot（主元）同义，判据都是「先处理最难被已有信息表示的那一列」；它的正确性靠 6.042J 的归纳法（每一步剩余子矩阵的秩递减一），秩揭示的界由奇异值交错与正交不变性推出。实现层面还有一处与 CSAPP 第 6 章的接口：LAPACK 的 column-major（列优先）存储让逐列扫描保持 spatial locality（空间局部性），换列只交换指针而不搬动数据，这是它在 cache 上比行主元版本便宜的原因。史实上，列主元 QR 由 Businger 与 Golub 于 1965 年在 Numerische Mathematik 7 卷 269 至 276 页给出，强秩揭示的定量版本由 Chan 在 1987 年、Gu 与 Eisenstat 在 1996 年补全；这几篇的一手原文未能核实。
> 
> 把它与前一页的 DEIM 摆在一起看：DEIM 在行上做插值投影，选点看残差；列主元 QR 在列上做正交化，选列看范数。两者都在回答「哪些坐标值得保留」，都以贪心为代价换取可证明的界，都不保证最优。区别是前者保留原始行、后者换成标准正交基，于是 DEIM 的结果能指回原始坐标，QR 的结果能直接做最小二乘，各有各的用处，这也解释了为什么本书两条路线并行推进。下一步该拿下的是第 4 节的部分 QR：它把这里的停机判据直接用成低秩近似算法，$Q_rR_rP^T$ 就是答案。

---

这便产生一个置换矩阵（permutation matrix）$\Pi$，使得 $A\Pi$（以及 $Q$）的前列恰是那些重要列：

```math
A\Pi = QR = \begin{bmatrix} Q_r & Q_{\text{rest}} \end{bmatrix}\begin{bmatrix} R_{11} & R_{12} \\ 0 & R_{22}\end{bmatrix}, \qquad R_{11}\ (r\times r)\ \text{为上三角}
```

（10）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 公式区 OCR 严重损坏，仅存「AII = QR … rn × m 0 C」与「triangular」等碎片；此处按列主元 QR 的标准分块形式、并配合下文对分块的附加条件重建。</span>

所谓「强秩揭示分解」（strong rank-revealing factorization），正是这种形式再加上对分块的额外条件。

例如要求 $\sigma_{\min}(R_{11}) \approx \sigma_r(A)$、$\sigma_{\max}(R_{22}) \approx \sigma_{r+1}(A)$，以及 $\|R_{11}^{-1}R_{12}\|$ 有界等。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 原文块条件语句被 OCR 噪声毁坏（仅存「） ， 丐 (C) e ， 一 IB 巳」碎片），此处依据 rank-revealing QR 的常规条件重建。</span>

这些性质在求 $A$ 的（计算意义上的）零空间（nullspace）的基时很有价值。

让我们假定这些性质成立，然后继续用 $Q$ 的前列，去构造 $A$ 的 $CMR$ 分解与 $U\Sigma V^T$ 分解。

---

> <span style="color:#7f8c8d;">Strang §II.3, p.143</span>

---

<!-- page 148: 书页 144, OCR page 48 -->

> <span style="color:#7f8c8d;">运行页眉：Computations with Large Matrices（大矩阵的计算）；本页为书页 144（OCR page 48）。</span>

#### Low Rank Approximation by a Partial QR（用部分 QR 作低秩近似）

前面几页都假定，矩阵 $A$ 的秩 $r$ 相对较小。

这一假定往往并不严格为真，但在效果上却是成立的（false but effectively true）。

> <span style="color:#1e8449;">**[note] Note（译者注：数值秩与误差沿流水线的传递）:**</span> 先立一个方法论前提，就是「false but effectively true」这句话：整个大矩阵部分都建在它之上，精确的秩在浮点世界里几乎不存在，有意义的是奇异值谱的形状。任何矩阵经过一次舍入扰动后数学上都可能满秩，但只要谱在某个位置断崖式下跌，把断崖之后的尾部整块丢掉就是安全的。形式写法是 $A=A_r+E$，$A_r$ 是秩 $r$ 的部分，$\|E\|$ 小到能被误差分析吸收；$r$ 不是题目给定的，是从谱上读出来的。这句话之所以是前提而不是敷衍，因为它决定了后面所有算法只承诺相对误差，不再承诺精确秩。
> 
> 断崖有多陡，值得用数字看，矩阵与扰动都写清以便逐位复算。取 $8\times 6$ 的 $A_0=U\operatorname{diag}(1,0.1,0.01,0,0,0)V^T$，其中 $U$ 由 `numpy.random.default_rng(0)` 抽 $8\times6$ 高斯阵再做 QR 得到，$V$ 由同 seed 的 rng 另抽 $6\times6$ 高斯阵做 QR 得到，精确秩是 3。加一个谱范数为 $2^{-52}$（$2.22\times10^{-16}$）的高斯扰动（`default_rng(1)` 抽高斯阵后按谱范数归一，seed 换一个数结果同量级）后，最小奇异值变成 $1.13\times10^{-16}$，条件数 $8.86\times10^{15}$，按默认容差 $1.78\times10^{-15}$（即 $8\times2.22\times10^{-16}$）判秩仍给 3；把扰动换成谱范数 $10^{-13}$（`default_rng(2)`），尾部三个奇异值变成 $5.00\times10^{-14}$、$4.03\times10^{-14}$、$3.09\times10^{-14}$，判据改口为 6，条件数 $3.24\times10^{13}$，正等于 $1/\sigma_{\min}$，两个数互为倒数、不再互相矛盾。数学上满秩，有效秩仍是 3。同一份数据，秩的答案取决于扰动大小与判据容差，这正是「效果上成立」的字面含义：不是矩阵有秩，是我们在给定容差下承认它有秩。
> 
> 带列主元的部分 QR（partial QR）给出的分解是 $A=Q_rR_rP^T+E$，其中 $P$ 是 permutation matrix（列置换矩阵）：原注漏掉这个 $P^T$，后文又直接用 $R_rP^T$ 而 $P$ 从未定义，源文 page_148 式 (11) 的原形是 $A=[Q_rR_r\ E]P^T$，即 $AP=Q_rR_r+EP$。只要 $E$ 的范数可控，就能换出近似 SVD：先对只有 $r$ 行、$n$ 列的 $R_rP^T$ 做小 SVD 得 $R_rP^T=U_r\Sigma V^T$，再令 $U=Q_rU_r$，于是 $A=U\Sigma V^T+E$，误差还是同一个 $E$。仍用上面那个秩 3 的 $8\times6$ 例子（取谱范数 $10^{-13}$ 那份扰动）复算，列主元顺序是 3 4 5 2 1 6：$\|E\|_F=9.85\times10^{-14}$、$\|E\|_2=8.27\times10^{-14}$，小 SVD 的三个奇异值仍是 $1$、$0.1$、$0.01$，$\|U^TU-I\|_F=4.05\times10^{-16}$、$\|A-U\Sigma V^T-E\|_F=3.53\times10^{-16}$。误差能原样穿过流水线，靠的是正交不变性：对任意正交 $Q$ 有 $\|QE\|_2=\|E\|_2$，实测比值 $1.00000000$；置换同理，$\|E[:,p]\|_F$ 与 $\|E\|_F$ 只差最后一位。换成非正交的基，这个比值立刻大于 1：取上三角、非对角元 $0.5$ 的 $Z$，$\|ZE\|_2/\|E\|_2=1.580$，误差被放大近六成——这就是 $Q$ 必须是正交矩阵的全部理由。
> 
> 跨课程上，$2^{-52}$ 就是 CSAPP 第 2 章 IEEE 754 双精度的 machine epsilon（机器精度），而「大矩阵先分块再算」的动机与第 6 章的 cache 层次同源；秩与谱的关系是 Strang 18.06 的 SVD 与低秩近似，把大问题拆成「大 QR 加小 SVD」的骨架与 CLRS 6.006 的分治是同一思路。这套做法在数值分析里叫 backward error（后向误差）分析，Wilkinson 在 1960 年代把「算出的解是某个邻近问题的精确解」立为判据，Martinsson 的部分 QR 低秩近似与 Halko、Martinsson、Tropp 三人 2011 年发表于 SIAM Review 53 卷的 randomized algorithms（随机化算法）综述，是这条线的后续；一手原文未能核实。
> 
> 最后把这份误差账翻译成工作习惯：$r$ 不该由题目给，而该由「你要多细」与「数据地板在哪」共同决定；判据要用相对量 $\|E\|/\|A\|$，绝对量在不同尺度的矩阵上无法比较；一旦 $\|E\|$ 落到 $10^{-14}$ 量级以下，继续加秩只是在拟合舍入噪声，算得越准越没有意义。还有一个容易踩的坑，但要分清是哪种误差：$r$ 选小了误差大，$r$ 选大了并不自动更准，因为把噪声奇异值也纳进来之后，$U$ 与 $V$ 的列方向被噪声主导，投影反而更差。原注说「误差曲线在有效秩处有个拐点」，这句话对 in-sample（样本内）重构误差是错的：Eckart–Young 定理保证 $\|A-A_r\|_F^2=\sum_{k>r}\sigma_k^2$ 随 $r$ 严格单调递减，直到取满都不回升——取 $\sigma=(1,0.1,0.01,10^{-3},10^{-4},10^{-5})$，这条误差依次是 $1.0050$、$0.10050$、$0.010050$、$0.0010050$、$1.0050\times10^{-4}$、$10^{-5}$、$0$，每步约除以十，一个拐点也没有。拐点只出现在 out-of-sample（样本外）误差或子空间估计误差上：拿新数据或比较 $\|\hat V_r\hat V_r^T-V_rV_r^T\|$ 时，噪声方向被塞进来会让误差先降后升。这也是为什么实际代码里秩总是带着一个容差参数出现，而不是一个整数常量。下一步该拿下的是 §II.4 的随机化算法，它把这里的 $Q_r$ 换成随机投影，误差记账方式不变，代价再降一个量级。

我们的意思是

```math
A = (\text{低秩 } r \text{ 矩阵 } A_r) + (\text{小范数矩阵 } E)
```

我们希望找到低秩矩阵 $A_r$，并与它一起完成计算。

忽略矩阵 $E$——这个大矩阵、却只有小范数——所引入的误差，我们是能够估计的。

Martinsson 提出，低秩近似 $A_r$ 可以用 QR 分解来计算。

该算法（带列主元 column pivoting）的前 $r$ 步产生 $Q_rR_r$：

```math
A = Q_rR_r + E = (r\text{ 列 } q_i)(r\text{ 行 } r_j^T) + ((n-r)\text{ 列，与前面那些 } q_i \text{ 正交})
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 该公式行 OCR 碎片「Q 铲」「@ c olumn s ‰」「row s rT」等，按「$Q_rR_r$ 展开为 $r$ 个秩一分量、残差列与 $q_i$ 正交」的数学语境重建。</span>

$\|E\|$ 很小！

由于该算法包含列交换，$E$ 中的那些列未必是 $A$ 的最后 $n-r$ 列。

但一个 $n\times n$ 的列置换矩阵（permutation）$P$，可以把这些列移到 $A$ 的后部。

于是，$r$ 个重要列 $Q_rR_r$ 便被排到了前部：

```math
A = \begin{bmatrix} Q_rR_r & E\end{bmatrix}P^T \approx Q_rR_rP^T
```

（11）

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 该公式被 OCR 打散（仅存「A = [ QrRrPT 乛 pT ]」等碎片），编号亦模糊；按正文随后所指的 equation (11) 及「QTRTPT 是对 $A$ 的好近似」重建。若原书此处另有一编号 (12) 的误差界公式，则已因 OCR 破损无从复原。</span>

$Q_rR_rP^T$ 就是对 $A$ 的好的秩 $r$ 近似。

幸运的是，带主元的 QR 算法会计算各列的范数（column norms），因此当 $\|E\|$ 低于我们预设的界限（preset bound）时，我们能够及时知道，随即停止计算。

这是一个有效的算法。

不过，它在「直接从 $A$ 中选列」这一目标上让了步，只在「标准正交列（在 $Q$ 中）」的目标上获得了成功。

我们将在 <span style="color:#7f8c8d;">§II.4</span> 以及本书第三部分（Part III）中，再回到低秩近似这一话题。

#### An Approximate SVD from the Partial QR（由部分 QR 得到的近似 SVD）

为使这一环节形成闭环，我们现在把目标对准 SVD 的一个好的近似。

它来自（11）式给出的、对 $A = QR$ 的紧密近似。

误差矩阵 $E$ 的范数并不会被放大：无论先前乘上 $Q_r$ 还是随后乘上 $P^T$，这两个（列）正交因子都不会改变范数。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 原文此句仅存「The error matrix E has | < (Qr)（PT)」碎片，按「两个正交因子相乘不放大误差」的语境重建。后文「Small error E」是版面图示标注，并注明各块维数 $m\times n$、$m\times r$、$r\times n$。</span>

仅需两个快速步骤，就足以产生一个非常接近 $A$ 的 SVD，且误差仍为同一个 $E$：

> **First**——第一步，求只有 $r$ 行的矩阵 $R_rP^T$ 的奇异值分解（SVD）：$R_rP^T = U_r\Sigma V^T$。

> **Second**——第二步，用 $Q_r$ 去乘 $U_r$，得到 $U = Q_rU_r$：正交矩阵乘正交矩阵，得到的仍是正交矩阵。

近似 SVD（approximate SVD）：

```math
A = Q_rU_r\Sigma V^T + E = U\Sigma V^T + E
```

（13），误差仍为 $E$（with error $E$）。

于是，一个小规模 SVD 加上一个大规模 QR，就给出了一个「大规模（近似）SVD」。

> <span style="color:#1e8449;">**[note] 译者注（算法/效率视角 + 证明策略模板）：**</span> 两步法是"把难算的大问题拆成便宜的小核 + 无损还原"的范本，可与 6.006 的分治思想互文：昂贵且需迭代的 SVD 被压到只有 r 行的 R_$rP^{T}$ 上完成（r≪m,n），而占体积的 Q_r 只做一次正交矩阵乘法——代价由约 mn·min(m,n) 量级的工作降到"大 QR + 小 SVD"的组合。误差仍为 E 绝非偶然，其关键是正交范数不变性：对任意正交 Q 与任何矩阵 E，‖QE‖=‖E‖（2-范数与 F-范数均成立，因正交变换保长度、保内积）。于是前端乘 Q_r、后端乘 $P^{T}$ 都不放大 E——误差沿流水线原样传递。这反过来照亮 page_147 那句"Q 条件数=1"为何是数值线性代数的王牌：乘以正交阵是唯一一类永不放大的运算，算法设计者于是总把"病态"藏进一个正交因子后面，把"难"留给小核。请把"误差夹在正交因子之间 ⟹ 界原样传递"收进你的证明工具箱：§II.4 随机化算法与本书第三部分会反复用同一条引理。

---

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）：** 两处「EVT」均为 $\Sigma V^T$ 的噪声变形；「0 qu ick steps」首词破损，按后文 First/Second 两个步骤重建为 Two quick steps。</span>

---

> <span style="color:#7f8c8d;">Strang §II.3, p.144</span>

---

<!-- page 149: 书页 145, OCR page 49 -->

> <span style="color:#7f8c8d;">本页为 Problem Set 11.3（习题集 11.3，隶属节 "Three Bases for the Column Space"，列空间的三种基）之习题页。按翻译铁律，以下各题题干保留英文原文、不作中译，以保全其学术训练价值；OCR 词内撕裂等纯拼写噪声（如 c olumn→column、c ontam→contain、0f→of）已静默复原，不逐一加注。</span>
> <span style="color:#7f8c8d;">**结构清单：** 本页全部单元均为习题（Problem 1–9），无定理/定义/正文段落。本页 OCR 损坏极为严重（大量杂散行号与矩阵数字串扰），题号与题序系依 OCR 可见标记并按数学语境重建，可能与原书版式存在出入，请以原书为准。</span>

### Problem Set 11.3（习题集 11.3）

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.**

The usual measure of danger from roundoff error is the condition number (cond $A$) $= \|A\|\,\|A^{-1}\|$. Show why that number is squared if we work with $A^T A$ instead of $A$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 首句 OCR 仅余 `...the co ” d ” ” m r 目 目 一 1 目` 残片，已依数学语境重建为 condition number（条件数）$\|A\|\,\|A^{-1}\|$；次句原为 `Show why th at number is s qu are d if we work with AT A instead of A`，其中 $A^T A$ 系由 `AT A` 修正。

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.**

Write down a 2 by 2 matrix with condition number $> 1000$. What is $A^{-1}$? Why does $A^{-1}$ also have condition number $> 1000$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.**

The reason that $\|A\|$ and $\|A^{-1}\|$ both appear is that we work with errors in the data $A$ and $b$. If $Ax = b$ and $A(x + \Delta x) = b + \Delta b$, then $A\Delta x = \Delta b$. Show that the relative error $\|\Delta x\|/\|x\|$ is bounded by the condition number times the relative error $\|\Delta b\|/\|b\|$:

```math
\frac{\|\Delta x\|}{\|x\|} \;\le\; \|A\|\,\|A^{-1}\| \;\frac{\|\Delta b\|}{\|b\|}.
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> 该题 OCR 近乎全毁，仅残存 `The reason that 丨 日 an d 目 一 1 日 both appear is that we work w ith 五 ve e rro` 与 `If = b an d A(c + (c) = b + Ab then A Ac = Ab. Show that`，题干文字及末尾的误差界不等式系按条件数（condition number）理论重建；若与原书措辞有出入，请以原书为准。

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.**

Why does $\lambda_{\max}/\lambda_{\min}$ equal the condition number for positive definite $A$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.**

**Important:** What is the condition number of an orthogonal matrix $Q$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.**

Suppose the columns of $C$ contain an orthonormal basis for the column space of $A$, and the rows of $R$ contain an orthonormal basis for the row space of $A$. Will those bases contain the singular vectors $u$ and $v$ in the SVD?

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.**

If $C$ and $R$ contain bases for the column space and row space of $A$, why does $A = CMR$ for some square invertible matrix $M$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.**

Here is a matrix whose numerical rank is 2. The number $\epsilon$ = machine epsilon is $2^{-52}$. Will orthonormal vectors $q_1$ and $q_2$ give a good basis for the column space—a basis that pivoted QR will probably choose?

```math
A =
\begin{pmatrix}
1 & 1 & 1\\
1 & 1+\epsilon & 0\\
1 & 0 & 1
\end{pmatrix}
```

Approximate that matrix as $QRP^T + O(\epsilon)$ for a permutation matrix $P$.

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 中 $\epsilon$、$q_1, q_2$ 仅余 `e = machine ep silon is 2 一 16 at orthonormal vectors ql and q2` 残片，按双精度机器精度（machine epsilon，double）重建为 $2^{-52}$（≈ $2.2\times10^{-16}$；OCR 的 `16` 系 `52` 误识，$2^{-16}\approx1.5\times10^{-5}$ 不可能是 double epsilon）；矩阵元素按 OCR 残留行序重建，pivoted QR（主元 QR）的列置换记法 $QRP^T$ 由 `QRPT+`、$O(\epsilon)$ 由 `(order e)` 修正。数值细节请以原书为准。

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.**

Which 2 by 2 submatrix $B_{\max}$ of $A$ (rank 2) has the largest determinant?

```math
A =
\begin{pmatrix}
2 & 5 & 1\\
1 & 3 & 5\\
3 & 1 & 1
\end{pmatrix}
```

Factor $A = Y B_{\max} Z$ as in equation (6).

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 将 $A$、$Y$、$B_{\max}$ 分别误作 `蓋`、`丫`、`Bmax`，已按上下文重建为 CUR 分解（CUR decomposition）选取最大 2×2 子行列式（determinant）$B_{\max}$ 的骨架（skeleton）形式 $A = YB_{\max}Z$；矩阵数值按 OCR 行序保留，请以原书为准。

---

<!-- page 150: 书页 146, OCR page 50 -->

> <span style="color:#7f8c8d;">**结构清单：** 本页为 §11.4 Randomized Linear Algebra（随机化线性代数）的开头正文，书眉（running head）为 Computations with Large Matrices（大型矩阵的计算，不译）。全部单元依次为：引言段（局限性与写作动机）、随机向量与列空间采样段、随机化计算的革命段、矩阵乘法复杂度段、随机采样乘积段、列-行外积说明段、范数平方采样段、Michael Mahoney 讲义段，以及一个 math fenced block（Mahoney 随机矩阵乘法公式）；无编号定理/定义/例子。OCR 词内撕裂等纯拼写噪声已静默复原，仅对影响数学内容的修正加注。</span>

### 11.4 Randomized Linear Algebra（随机化线性代数）

本节关于随机化（randomization）的论述注定是不完整的，首要原因在于它并非出自专家（expert）之手。

本书不可能成为计算 SVD 或 QR 分解（QR factorization）的详尽指南；不过，介绍那些使大型矩阵（large matrices）的此类计算成为可能的关键思想与算法，似乎仍然可行——而且非常值得。

这些思想中包括一些重要的新方法，它们以随机向量（random vector）$v$ 为起点。于是所得乘积便是来自 $A$ 的列空间（column space）的随机样本（random sample）。取其中 $r$ 个这样的向量（或为稳妥起见取 $r+10$ 个，以防随机意外（random accident）），我们便得到一个有可能很薄（thin）的矩阵可供计算，加速效果（speedup）十分可观。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 中 `random vectors 凭` 的 `凭` 与 `column space 0f 蓋` 的 `蓋` 已分别重建为随机向量 $v$ 与矩阵 $A$；`r + 10 tO be on the safe side` 中的 $r+10$ 为按语境补齐的下标算式。

（这也是第 III.5 节中压缩感知（compressed sensing）的出发点——后者旨在加快数字信号（digital signal）的采集与处理。）

本节将介绍并描述随机化计算（randomized computation）的基本步骤；这一思想已为面向大型矩阵的数值线性代数（numerical linear algebra）带来一场革命。

第一个例子是矩阵乘法（matrix multiplication）。若 $A$ 为 $m \times n$、$B$ 为 $n \times p$，则 $C = AB$ 通常需要 $mnp$ 次单独的乘法：$AB$ 中共有 $mp$ 个内积（inner product），每个内积需要 $n$ 次乘法；等价地，它也可看作 $n$ 个外积（outer product，即列乘行，columns times rows），每个外积需要 $mp$ 次乘法。因此相乘极大的矩阵代价非常高昂（expensive）。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 原句 `If and B are m by and by then` 缺失 $A$、$n$、$p$，已依语境补全为 $A$（$m\times n$）与 $B$（$n\times p$）；末句 `M 方 纱 g very e matrices is e 无 e 刀 豆 v 巳` 系严重乱码，重建为 Multiplying very large matrices is very expensive。

设想我们并不使用完整的矩阵，而只是对 $A$ 与 $B$ 进行采样（sample）。少数几个元素 $a_{ij}$、$b_{jk}$ 并不能告诉我们多少信息；但从 $A$ 中取出 $s$ 列 $a_k$、再从 $B$ 中取出对应的 $s$ 行 $b_k$，便会得到 $s$ 个秩一矩阵（rank-one matrix）$a_k b_k$。

这些正是 $C = AB$ 的"典型"组成部分；我们可以对这些秩一乘积加权求和，用以估计真实的 $AB$（即全部秩一乘积之和）。请注意，这里采用的是列-行外积（column-row product，倍受推荐），而不是行-列内积（row-column inner product，属低层次做法）。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接 Bertsekas 概率 + 第一性原理）：**</span> AB=$\Sigma_{k}$ $a_{k}b_{k}$ 的"外积和"写法本身就是第一个算法洞察：矩阵乘法不必逐个算内积，它是 n 个秩一矩阵的叠加。从"求和"跳到"抽样求和"是重要度采样（importance sampling）思想，而"无偏性"只需你在 Bertsekas《概率导论》学过的期望线性即可证明：设第 k 个外积 $X_{k}$=$a_{k}b_{k}$ 被抽中的概率为 $p_{k}$，则 E[$X_{k}$/$p_{k}$]=$\Sigma_{k}p_{k}$·($X_{k}$/$p_{k}$)=AB——所以每抽一项都要按 1/$p_{k}$ 加权，权重不是随意的；正文 OCR 丢失的均匀权重 n/s（$p_{k}$=1/n 时）正是该式的特例。更妙的是方差动机：加权单项 X/p 的方差含二阶矩 $\Sigma_{k}p_{k}$($X_{k}$/$p_{k}$)$^{2}$，当抽中概率 $p_{k}$ 与该乘积"大小"成正比时，$X_{k}$/$p_{k}$ 趋于常数、方差被压到接近零——这就是"给大乘积更高抽中率+补偿"的全部目的：正确期望由补偿公式兜底，低方差由非均匀概率换取。样本数 s 再独立调节精度。概率的语言（期望、方差、样本量）第一次完整地进入线性代数。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 该段下标与比例因子大量缺失，仅残存 `But 5 columns Ok 什 om ... 5 rank one matric e s Okbk ... we can 况 方 纱 叻 e sum by / 5 一 tO e stimate the true AB = sum Of products`；按数学语境重建为"对 $s$ 个采样外积按概率加权以估计 $AB$"（均匀概率时典型权重为 $n/s$，具体加权见下文"范数平方采样"）。

这一思想还有更多值得挖掘之处。随机采样（random sampling）要用到一些基础统计（statistics）知识。较大的乘积 $a_k b_k$ 显然对 $C = AB$ 贡献更大；我们可以、也确实会把均匀概率（uniform probability）改为"范数平方采样"（norm-squared sampling），以提高那些较大样本被抽中的机会。

这要求我们对公式作出补偿（compensate），使其仍能给出正确的期望值（expected value）与尽可能低的方差（variance）。你将看到统计思想的威力！

我们的讲述将主要依照 Michael Mahoney 在加州大学伯克利分校（UC Berkeley）所开课程的讲义（lecture notes）。这些讲义组织得当、文字精当——是一份慷慨而重要的贡献。

这份 2013 年的课程笔记于 2016 年发布，其开篇正是下面这个关于随机矩阵乘法（random matrix multiplication）的快速概览：一张采样矩阵（sampling matrix）$S$ 将作用于 $A$ 的列与 $B$ 的行，从而产生矩阵 $C$ 与 $R$：

```math
C = AS, \qquad R = S^T B, \qquad CR = AS\,S^T B \approx AB .
```

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR 首句 `act on the columns of an d row s of B to produce C and ：` 中 $A$、$C$、$R$ 记号缺失；公式残片 `C = AS and = STB and CR = ASSTB ÄB` 已重建为 $C = AS$、$R = S^T B$、$CR = AS\,S^T B \approx AB$（其中 `ÄB` 修正为 $\approx AB$）。

我们用 $C$ 与 $R$ 相乘，而不是去乘完整且正确的矩阵 $A$ 与 $B$。$SS^T$ 接近单位阵 $I$ 这一点并不为真；但 $SS^T$ 的期望值等于 $I$ 这一点却是成立的。这里正是随机化（randomization）的关键所在。

> <span style="color:#1e8449;">**[note] 译者注（跨课程连接 Chernoff/CLRS/CSAPP + 第一性原理）：**</span> "E[$SS^{T}$]=I"是全节的钥匙，可用期望线性直接验算：构造 s 个独立缩放采样列，S 的第 k 列以概率 $p_{i}$ 落在位置 i 并取 $e_{i}$/√(s·$p_{i}$)，则 E[$S_{k}S_{k}^{T}$]=$\Sigma_{i}p_{i}$·(1/($sp_{i}$))$e_{i}e_{i}^{T}$=(1/s)I，故 E[$SS^{T}$]=$\Sigma_{k}$(1/s)I=I——缩放因子 1/√($sp_{i}$) 正是前文"补偿公式"的矩阵形态，它让每个采样的期望贡献恰为整矩阵的 s 分之一，于是随机采样矩阵在期望意义上"扮演"单位阵。但期望相等只保证平均：单次偏差须靠浓度不等式兜底——6.042 学过的 Chernoff 界告诉你 s 个独立样本的加权和以高概率贴近期望，坏事件概率随 s 指数衰减。文首"r+10 防随机意外"就是这个思维的操作化（oversampling）：多取十余个样本对冲漏采重要列的坏事件，与 CLRS 第 5 章"随机化 + 冗余对冲最坏输入"同一哲学。从 CSAPP 视角补一句：AS 是随机抽取 A 的列，内存随机访问、cache 不友好，但总流量从 O(mn) 量级降到 O(ms)，以少量 cache miss 换量级性的带宽节省——这是"用概率换复杂度"在存储层次上的代价清单。

> <span style="color:#1e8449;">**[note] 译者注（OCR 修正）:**</span> OCR `the expected e ofSST I` 已重建为 the expected value of $SS^T$ is $I$；末句原为 `There you the key tO rando mi zation`，按上下文补入 see。

---

> <span style="color:#7f8c8d;">Strang §II.4, p.146</span>
