# Linear Algebra and Learning From Data（线性代数与数据学习）· IV.9

## 书页 257-258 ｜ PDF 页 259-260 ｜ The Orthogonal Procrustes Problem（正交 Procrustes 问题）

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
