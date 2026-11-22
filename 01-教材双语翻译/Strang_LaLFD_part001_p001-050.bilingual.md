# <span style="color:#c0392b;">Linear Algebra and Learning From Data（线性代数与从数据中学习）</span>

<span style="color:#2471a3;">**[section]**</span> **Part I: Highlights of Linear Algebra（线性代数精要）**

---

## Part I 引言

本书的 Part I 是对 applied linear algebra（应用线性代数）的一个 serious introduction（严肃导论）。

如果读者的 background（背景）在这个重要的数学分支上 <span style="color:#00838f;">not great（不够强）</span> 或 <span style="color:#00838f;">not recent（不够新）</span>，请务必仔细阅读。

本书完全从使用矩阵的 columns（列）进行 $Ax$ 和 $AB$ 的 multiplication（乘法）开始。

这看起来可能似乎只是 <span style="color:#00838f;">normal（常规操作）</span>，但实际上它是 <span style="color:#00838f;">fundamental（基础性的）</span>。

让我指出本章研究的五个基本问题。

它们是：$Ax=b$（求解）、$Ax=\lambda x$（特征值）、$Ax=0$（零空间）、Minimize $\|Ax-b\|^2$（最小二乘），以及 Factor（分解）矩阵 $A$。

这些问题中的每一个看起来都像是一个普通的 computational question（计算问题）：求解 $x$，求解 $x$ 和 $\lambda$，求解 $x$，minimize（最小化），以及 factor（分解）$A$ 为 columns times rows（列乘以行）。

你会看到 <span style="color:#00838f;">finding（寻找）</span>（甚至比 <span style="color:#00838f;">solving（求解）</span> 更重要）是我们的目标。

我们首先想知道 $Ax=b$ 在 first place（一开始）是否有 solution（解）。

问：向量 $b$ 是否在矩阵 $A$ 的 column space（列空间）中？

这个看似天真的单词 <span style="color:#00838f;">space（空间）</span> 会引导我们走很长一段路。

正如你将看到的，这将是一条富有成效的道路。

The eigenvalue equation（特征值方程）$Ax=\lambda x$ 非常不同。

这里没有向量 $b$——我们只关注矩阵本身。

我们想要 eigenvector directions（特征向量方向），使得 $A$ 保持与 $x$ 相同的 direction（方向）。

然后沿着那条线，$A$ 的所有复杂 interconnection（相互关联）都消失了。

向量 $Ax$ 就是 $\lambda x$。

矩阵 $e^{At}$（来自 differential equation（微分方程））就只是乘以 $e^{\lambda t}$。

当我们知道每一个 $x$ 和 $\lambda$ 时，我们可以解决任何 linear（线性）问题。

方程 $Ax=0$ 很接近但又不同。

现在我们有两个 vectors（向量）$u$ 和 $v$。

我们的矩阵很可能是 rectangular（矩形）的，并且充满了 data（数据）。

那个 data matrix（数据矩阵）的哪一部分是重要的？

Singular Value Decomposition（奇异值分解，SVD）找到了 $A$ 的最简单的 pieces（部分）。

那些 pieces（部分）是 rank-one matrices（秩一矩阵）$u\sigma v^T$（column times row（列乘以行））。

每个矩阵都是由这些 orthogonal pieces（正交部分）构建的。

Data science（数据科学）在 SVD 中与 linear algebra（线性代数）相遇。

找到那些 pieces（部分）$v$ 是 Principal Component Analysis（主成分分析，PCA）的目标。

Minimization（最小化）和 factorization（分解）表达了 fundamental applied problems（基本应用问题）。

它们引向那些 singular vectors（奇异向量）和 $U\Sigma V^T$。

在 least squares（最小二乘）中计算 best（最优）$x$，在 PCA 中计算 principal component（主成分）$v$，是拟合数据的 algebraic problem（代数问题）。

我们不会给出代码——那些属于 online（在线资源）——我们正在努力解释 ideas（想法）。

当你理解了 column spaces（列空间）、nullspaces（零空间）、eigenvectors（特征向量）和 singular vectors（奇异向量）后，你就为各种 applications（应用）做好了准备：Least squares（最小二乘）、Fourier transforms（傅里叶变换）、LASSO（在统计学中）、以及 stochastic gradient descent（随机梯度下降）（在带有 neural nets（神经网络）的 deep learning（深度学习）中）。

---

<span style="color:#2471a3;">**[section]**</span> **1.1 Multiplication $Ax$ Using Columns of $A$（使用 $A$ 的列进行乘法 $Ax$）**

我们总是使用 examples（例子）来使我们的观点 clear（清晰）。

### Inner Products（内积）

将矩阵 $A$ 与向量 $x$ 相乘有两种方式：by rows（按行）和 by columns（按列）。

对于矩阵 $A=\begin{bmatrix}2&3\\2&4\\3&7\end{bmatrix}$ 和向量 $x=\begin{bmatrix}1\\2\end{bmatrix}$，计算 $Ax$：

```math
Ax = \begin{bmatrix}2&3\\2&4\\3&7\end{bmatrix}\begin{bmatrix}1\\2\end{bmatrix}
```

**By rows（按行）方式** 产生三个 inner products（内积）：

```math
\begin{aligned}
\text{row 1}\cdot x:&\quad\begin{bmatrix}2&3\end{bmatrix}\cdot\begin{bmatrix}1\\2\end{bmatrix}=2(1)+3(2)=8 \\
\text{row 2}\cdot x:&\quad\begin{bmatrix}2&4\end{bmatrix}\cdot\begin{bmatrix}1\\2\end{bmatrix}=2(1)+4(2)=10 \\
\text{row 3}\cdot x:&\quad\begin{bmatrix}3&7\end{bmatrix}\cdot\begin{bmatrix}1\\2\end{bmatrix}=3(1)+7(2)=17
\end{aligned}
```

因此 $Ax=\begin{bmatrix}8\\10\\17\end{bmatrix}$。

这些 inner products（内积）也被称为 "dot products（点积）"，因为使用了 dot notation（点记号）：

```math
\text{row}\cdot\text{column} = (2,3)\cdot(1,2)=2(1)+3(2)=8
```

这是找到 $Ax$ 的三个 separate components（独立分量）的方式。

我们使用这种方法进行 computation（计算）——但不是为了 understanding（理解）。

它是 <span style="color:#00838f;">low-level（低层次）</span> 的。

Understanding（理解）是 <span style="color:#00838f;">higher-level（高层次）</span> 的，使用 vectors（向量）。

### Columns View（列的视角）

Vector approach（向量方法）将 $Ax$ 视为 $a_1$ 和 $a_2$ 的一个 "linear combination（线性组合）"。

这是线性代数的 <span style="color:#00838f;">fundamental operation（基本操作）</span>！

$a_1$ 和 $a_2$ 的一个 linear combination（线性组合）包括两个步骤：

(1) 将 columns（列）$a_1$ 和 $a_2$ 乘以 "scalars（标量）" $x_1$ 和 $x_2$。

(2) 将向量相加：$x_1a_1+x_2a_2=Ax$。

在我们的例子中，$x_1=1$，$x_2=2$，所以：

```math
Ax = 1\cdot a_1 + 2\cdot a_2 = \begin{bmatrix}2\\2\\3\end{bmatrix} + \begin{bmatrix}6\\8\\14\end{bmatrix} = \begin{bmatrix}8\\10\\17\end{bmatrix}
```

$Ax$ 是矩阵 $A$ 的 columns（列）的一个 linear combination（线性组合）。这是 <span style="color:#00838f;">fundamental（基础性的）</span>。

这种思维方式引导我们走向矩阵 $A$ 的 column space（列空间）。

关键思想是取 columns（列）的 all combinations（所有组合）。

所有实数 $x_1$ 和 $x_2$ 都是允许的——这个 space（空间）包含每个 $x_1a_1+x_2a_2$。

这样我们得到 infinitely many（无穷多个）output vectors（输出向量）。

而且我们可以 geometrically（几何地）看到这些 output（输出）。

在我们的例子中，每个 $Ax$ 是一个在 3-dimensional space（三维空间）中的向量。

那个 3D space（三维空间）称为 $\mathbb{R}^3$。（字母 $\mathbb{R}$ 表示 real numbers（实数）。具有三个复分量的向量在 $\mathbb{C}^3$ 中。）

我们坚持使用 real vectors（实向量），并提出这个 key question（关键问题）。

所有 combinations（组合）$x_1a_1+x_2a_2$ 产生了完整 3D space（三维空间）的哪一部分？

**答案：** 这些向量产生一个 plane（平面）。

这个 plane（平面）包含方向为 $a_1=(2,2,3)$ 的完整直线，因为每个向量 $x_1a_1$ 都包含在内。

这个 plane（平面）也包含方向为 $a_2=(3,4,7)$ 的所有向量 $x_2a_2$ 的直线。

并且它包含一条线上任意向量与另一条线上任意向量的 sum（和）。

这种 addition（加法）填充了一个包含两条直线的 infinite plane（无穷平面）。

但它并没有填满整个 3-dimensional space（三维空间）$\mathbb{R}^3$。

> <span style="color:#1e8449;">**[note] 为什么列视角是全书第一原理：**</span> 矩阵乘法有两种算法，而只有一种给出了这本书后面每一页的动机。row-dot-column（行点列）把 $Ax$ 看成 $m$ 个 inner product（内积）并排，它回答「怎么算最省事」；column combination（列的组合）把 $Ax$ 看成 $n$ 个 columns（列）按 $x$ 加权后相加，它回答「$A$ 到底是什么」。后者才是这门学科的 source（源头）：$A$ 的 columns（列）是 $\mathbb{R}^m$ 中的向量，$x$ 只是配给它们的 coefficient（系数）。
> 
> 完整形式只有一行：$Ax=\sum_{j=1}^{n}x_ja_j$，其中 $a_j$ 是 $A$ 的第 $j$ 个 column（列）。于是「$Ax=b$ 有 solution（解）」被翻译成一个 membership（归属）问题：$b\in C(A)$，即 $b$ 落在那些 columns（列）的 span（张成）里。这个翻译没有信息损失，但它把「方程组」换成了「一个点落在一个几何对象里」；后面关于 rank（秩）、dimension（维数）、projection（投影）的每一句话都从这个换位起步。顺带记下两个尺寸：$x$ 的维数是 $n$ 而 $b$ 的维数是 $m$，这两个数不必相等 —— rectangular（长方形的）矩阵在本书里是常态而非例外，所以「方程个数」与「未知数个数」从一开始就不该被期待对齐。
> 
> 两种算法的等价是逐字的。取书中 $A$ 的两个 columns（列）$a_1=(2,2,3)$、$a_2=(3,4,7)$ 与 $x=(1,2)$，实测 $Ax=\begin{bmatrix}8\\10\\17\end{bmatrix}$ 与 $1\cdot a_1+2\cdot a_2$ 完全相同，都是 $(8,10,17)$。差别在 $x$ 的角色。row view（行视角）里 $x$ 是 unknown（未知量），每行给一个 constraint（约束），$m$ 个超平面求交；column view（列视角）里 $x$ 是 recipe（配方），$A$ 是原料清单，问题变成「这些原料能不能配出 $b$」。前一种视角让你以为方程越多越难解，后一种视角告诉你反话：方程越多，$b$ 越容易被挤出那个 plane（平面）。
> 
> 用同一个 $b=(1,1,1)$ 把这件事算成数。$a_1,a_2$ 张成的 plane（平面）的 normal（法向量）是 $n=a_1\times a_2=(2,-5,2)$，实测 $n\cdot a_1=n\cdot a_2=0$、$n\cdot b=-1$，所以 $b$ 不在 plane（平面）里 —— 不可解不是一次消元事故，而是一个投影不为零。把它量化：$\|Ax-b\|$ 的最小值等于 $|n\cdot b|/\|n\|=1/\sqrt{33}=0.17408$，对应的 least squares（最小二乘）解是 $x=(28/33,-7/33)=(0.84848,-0.21212)$，residual（残差）$Ax-b=(0.06061,-0.15152,0.06061)$ 恰好平行于 $n$。缺的那一块，就是 $b$ 在 normal direction（法向）上的分量。
> 
> 反过来问：把「$x$ 跑遍整个 $\mathbb{R}^n$」这次量词删掉，会塌成什么？把 $x$ 限制在 $\mathbb{R}^n_{\ge0}$，$C(A)$ 就从 subspace（子空间）塌成 cone（锥），可解性不再由 rank（秩）决定：$a_1=(1,0)$、$a_2=(0,1)$ 配 $b=(-1,-1)$，rank（秩）仍是 $2$，但 $b$ 不在 cone（锥）里。此时判据换成 Farkas lemma（法卡斯引理）：$b$ 不在 cone（锥）中，当且仅当存在 $y$ 使每个 $y\cdot a_j\ge0$ 而 $y\cdot b<0$ —— 这正是 linear programming（线性规划）弱对偶的几何形态。一行改动，付掉的是整条免费的「$Ax=b$ 可解 $\iff b\in C(A)$」。
> 
> 跨课程：Strang 18.06 第一讲把 column picture（列图）与 row picture（行图）并排画在同一块黑板上，$Ax=b$ 的两个画法各占一半；CSAPP 第 6 章则把这件事变成性能数字：$n\times n$ 的 double（双精度浮点）矩阵按 row-major（行主序）存放时，取一列要跨 $8n$ 字节的 stride（步长），$n=1000$ 时是 $8000$ 字节，一条 $64$ 字节的 cache line 只用得上 $8$ 字节，利用率 $12.5\%$；而 row-dot-column 的顺序扫描几乎全命中。同一条公式，两种读法在 cache 上差一个数量级。
> 
> 历史坐标：把矩阵当线性映射、把 image（像）当子空间，是 20 世纪抽象代数定型之后的事 —— Halmos 的 *Finite-Dimensional Vector Spaces*（1958 年第 2 版）已经以此为主线。而把 column picture（列图）放在教材第一页、并明说「别用 dot product（点积）去理解」，是 Strang 自己的教学选择；他在 1993 年 *American Mathematical Monthly* 100(9):848--855 的短文里用同一张图讲完四个 subspace（子空间），那篇就是本节的祖先（卷期页码已核实）。
> 
> 落点：一旦承认 $Ax$ 是 columns（列）的 combination（组合），「所有 combination（组合）填满了什么」就自然升格成一个 subspace（子空间），而「填不满」的四个等级 —— 点、线、面、整个空间 —— 正是 rank（秩）的雏形。这也是为什么下一小节讨论 column space（列空间）时，第一个问题就是「它有多大」。

### The Column Space（列空间）

<span style="color:#00838f;">基本思想：</span> Columns（列）的组合填充了矩阵的 column space（列空间）。

在我们的例子中，column space（列空间）是一个 plane（平面）。

这个 plane（平面）包含 zero point（零点）$(0,0,0)$（当 $x_1=x_2=0$ 时产生）。

这个 plane（平面）包含 $(5,6,10)=a_1+a_2$ 和 $(-1,-2,-4)=a_1-a_2$。

每个 combination（组合）$x_1a_1+x_2a_2$ 都在这个 column space（列空间）中。

<span style="color:#2471a3;">**[theorem]**</span> $b=(b_1,b_2,b_3)$ 在矩阵 $A$ 的 column space（列空间）$C(A)$ 中，当且仅当 $Ax=b$ 有 solution（解）$(c_1,c_2)$。

当你看到这个 truth（事实）时，你就理解了 column space（列空间）$C(A)$。

Solution（解）显示了如何将 right side（右端项）$b$ 表达为 columns（列）$a_1$ 和 $a_2$ 的一个 combination（组合）。

对于某些 $b$，这是不可能的——它们不在 column space（列空间）中。

<span style="color:#2471a3;">**[example]**</span> **Example 2.** $b=(1,1,1)$ 不在 $C(A)$ 中。

```math
\begin{bmatrix}2&3\\2&4\\3&7\end{bmatrix}\begin{bmatrix}c_1\\c_2\end{bmatrix}=\begin{bmatrix}1\\1\\1\end{bmatrix}
```

前两个方程给出 $2c_1+3c_2=1$ 和 $2c_1+4c_2=1$。

相减得 $c_2=0$，然后 $c_1=0.5$。

但第三个方程：$3(0.5)+7(0)=1.5$，不等于 $1$。

这意味着 $b=(1,1,1)$ 不在 column space（列空间）中——即 $a_1$ 和 $a_2$ 张成的 plane（平面）中。

该系统是 unsolvable（不可解的）。

<span style="color:#2471a3;">**[example]**</span> **Example 3.** 三个矩阵的 column spaces（列空间）各是什么？

```math
A_2=\begin{bmatrix}2&3&5\\2&4&6\\3&7&10\end{bmatrix},\qquad
A_3=\begin{bmatrix}2&3&1\\2&4&1\\3&7&1\end{bmatrix}
```

**解：** $A_2$ 的 column space（列空间）与之前相同。

新列 $(5,6,10)$ 是 column 1 + column 2 的 sum（和）。

所以 column 3 已经在 plane（平面）中，没有添加新内容。

通过包含这个 "dependent（依赖的）" 列，我们并没有超越原来的 plane（平面）。

$A_3$ 的 column space（列空间）是完整的 3D space（三维空间）$\mathbb{R}^3$。

Example 2 向我们展示了新第三列 $(1,1,1)$ 不在 plane（平面）$C(A)$ 中。

column space（列空间）$C(A_3)$ 变得更大了。

但在 plane（平面）和完整 3D space（三维空间）之间没有可停的地方。

想象一下 plane（平面）和一个不在 plane（平面）中的第三向量 $(x_3,y_3,z_3)$（意味着 $z_3\neq0$）。

它们组合起来给出 $\mathbb{R}^3$ 中的每个向量。

以下是 $\mathbb{R}^3$ 内部所有可能 column spaces（列空间）的完整列表。Dimension（维数）有 0, 1, 2, 3：

- **零向量** $(0,0,0)$ 本身（dimension 0）
- **一条直线**：所有向量 $x_1a_1$（dimension 1）
- **一个平面**：所有向量 $x_1a_1+x_2a_2$（dimension 2）
- **整个 $\mathbb{R}^3$**：所有向量 $c_1a_1+c_2a_2+c_3a_3$，其中 $a_1,a_2,a_3$ 独立（dimension 3）

在这个列表中，我们需要 vectors（向量）$a_1,a_2,a_3$ 是 "independent（独立的）"。

给出零向量的唯一 combination（组合）是 $0a_1+0a_2+0a_3$。

所以 $a_1$ 本身给出一条直线，$a_1$ 和 $a_2$ 给出一个 plane（平面），$a_1,a_2,a_3$ 给出 $\mathbb{R}^3$ 中的每个向量 $b$。

零向量在每个 subspace（子空间）中！

在线性代数的语言中：

三个在 $\mathbb{R}^3$ 中的独立列产生 invertible matrix（可逆矩阵）：$AA^{-1}=I$。

$Ax=0$ 要求 $x=(0,0,0)$。

那么 $Ax=b$ 有 exactly one solution（唯一解）$x=A^{-1}b$。

你现在看到了矩阵 $A$ 的列的 picture（图像）：它们的组合填充了它的 column space（列空间）：即所有 $\mathbb{R}^n$。

我们需要那些 ideas（想法）和那种 language（语言）来走得更远。

> <span style="color:#1e8449;">**[note] 列空间为什么必须与另外三个子空间一起出场：**</span> column space（列空间）$C(A)$ 是 $A$ 的所有 columns（列）的一切 combination（组合）构成的集合，它是 $\mathbb{R}^m$ 的一个 subspace（子空间）。它可以单独定义，却不能单独使用：一旦你问「$Ax=b$ 有没有解」，答案要么用 $C(A)$ 说（$b$ 在不在里面），要么用 $N(A^T)$ 说（$b$ 是否垂直于每个满足 $A^Ty=0$ 的 $y$），而这两种说法靠一条 orthogonality（正交性）粘在一起。这就是 four fundamental subspaces（四个基本子空间）必须同时出场的原因。另外三个子空间的正式定义要到 §I.3（本文件 602--808 行）才出现，这里先把整张图摆出来。
> 
> 完整形式，设 $A$ 是 $m\times n$、rank（秩）为 $r$：
> 
> - $C(A)=\{Ax:x\in\mathbb{R}^n\}\subseteq\mathbb{R}^m$，$N(A)=\{x:Ax=0\}\subseteq\mathbb{R}^n$，$C(A^T)\subseteq\mathbb{R}^n$，$N(A^T)=\{y:A^Ty=0\}\subseteq\mathbb{R}^m$；
> - $\dim C(A)=\dim C(A^T)=r$，$\dim N(A)=n-r$，$\dim N(A^T)=m-r$；
> - $C(A^T)\perp N(A)$ 且两者直和成 $\mathbb{R}^n$；$C(A)\perp N(A^T)$ 且两者直和成 $\mathbb{R}^m$（这两条直和由 §I.3 的 rank theorem 保证，不是这里的前提）；
> - $Ax=b$ 有解 $\iff b\in C(A)\iff y\cdot b=0$ 对每个 $y\in N(A^T)$ 成立。
> 
> 最后一条不能靠「$C(A)$ 与 $N(A^T)$ 直和成 $\mathbb{R}^m$」来证，那句话与结论等价；正确的前提是 §I.3 的 rank theorem（秩定理）本身：它给出 $\dim C(A)=r$、$\dim N(A^T)=m-r$ 与两者的正交性，三者合起来才把直和分解合法化。直和一旦站住，验证只要两行：若 $A^Ty=0$ 而 $b=Ax$，则 $y\cdot b=y^TAx=(A^Ty)^Tx=0$；反过来若 $b$ 垂直于 $N(A^T)$，按直和把 $b$ 拆成 $b_1+b_2$（$b_1\in C(A)$、$b_2\perp C(A)$），于是 $A^Tb_2=0$ 即 $b_2\in N(A^T)$，而差 $b-b_1$ 又垂直于 $N(A^T)$，与自己垂直的向量只能是零。出处：教材 §I.3 Facts about Ranks 第 5 条，加上我补的消元论证 —— 对 $A$ 消元到 $R=\operatorname{rref}(A)$，pivot（主元）恰好 $r$ 个，pivot columns 是 $C(A)$ 的 basis（基），$R$ 的非零行是 $C(A^T)$ 的 basis，两边数到同一个 $r$，两个 nullity 于是只是减法。这条路径不用 inner product（内积），所以能反过来支撑那张直和图。
> 
> membership（归属）判定本身只是一个是非题，但它并不缺少否证手段：否定它同样有有限 certificate（证书）。消元到某一行落成 $0=c$（$c\neq0$）是一次证书；从 $N(A^T)$ 里取一个 $y$ 使 $y\cdot b\neq0$ 是另一次，后者只要一次 inner product（内积）就能复核，可挑的方向有 $m-r$ 个维度。判据与证书的差别，是「可陈述」与「可验证」的差别。
> 
> 用书中的三个矩阵实测。$A=\begin{bmatrix}2&3\\2&4\\3&7\end{bmatrix}$ 是 $3\times2$：rank（秩）$r=2$、$\dim N(A)=0$、$\dim N(A^T)=1$，$N(A^T)$ 由 $(2,-5,2)/\sqrt{33}=(0.34816,-0.87039,0.34816)$ 张成。对 $A^T$ 做 SVD（奇异值分解），即取 $A=U\Sigma V^T$ 的第三列 $u_3$，实测 $(0.3481553119,-0.8703882798,0.3481553119)$ 与它逐位相同，因为 $A$ 只有两个非零 singular values（奇异值）$9.52029$ 与 $0.60340$，第三个只能落在零空间里。$b=(1,1,1)$ 在这个方向上的投影是 $-0.174078$（恰为 $-1/\sqrt{33}$），于是不可解，最短距离正好是 $0.174078$。$A_2$ 把第三列换成 $a_1+a_2=(5,6,10)$：$r$ 仍是 $2$，$\dim N(A_2)$ 从 $0$ 变成 $1$，$\det A_2=0$；$A_3$ 把第三列换成 $(1,1,1)$：$r=3$，两个 nullity 都归零，$\det A_3=-1$。同一张 $3\times3$ 表格，行列式是不是零，只取决于第三列有没有落进那个 dimension（维数）为 $2$ 的 plane（平面）。
> 
> 换个系数域，这张图就塌。若 $A$ 的 entry（元素）都是有理数且列在 $\mathbb{Q}$ 上 independent（如有理矩阵列满秩），$\{Ax:x\in\mathbb{Z}^n\}$ 才是 lattice（格），点与点之间有正的最小间距；一般情形它可以稠密：取 $A=(1,\sqrt2)^T$，集合 $\{m+n\sqrt2\}$ 在 $\mathbb{R}$ 里稠密，实测在 $|m|,|n|\le100$ 内相邻两点最小间隔是 $5.05\times10^{-3}$，放宽到 $|m|,|n|\le1000$ 就掉到 $3.59\times10^{-4}$，范围越大越密。可解性于是从消元的 $O(mn\min(m,n))$ 掉进 integer programming（整数规划），而后者是 Karp 在 1972 年那 21 个 NP-complete 问题里的一个。$C(A)$ 之所以能被一个数 $r$ 完全刻画，全靠 $\mathbb{R}$ 是 field（域），除法随时可用。
> 
> 历史坐标：$C(A)\perp N(A^T)$ 的内容比它的名字老得多 —— Fredholm 在 1903 年研究 integral equation（积分方程）时得到的 Fredholm alternative（二择一），把「要么可解、要么存在一个正交的障碍」变成分析学的标准工具；有限维版本则被 Strang 画成一张四个 block（区块）的图，并命名为 linear algebra 的 fundamental theorem（基本定理），见 *Amer. Math. Monthly* 100(9):848--855 (1993) 第 2 节（卷期页码已核实）。
> 
> 跨课程：Thomson 实分析里 $V/\ker T\cong\operatorname{im}T$ 是同一句话的无限维版本，作为 linear space（线性空间）它由第一同构定理恒成立、不需要任何拓扑；只有在 Banach 空间意义下要求这个同构是拓扑同构时，才需要 $\operatorname{im}T$ 闭（开映射定理），而处理不闭的情形正是 Fredholm 那一路的活儿。
> 
> CLRS 的图搜索把 $\mathbb{R}$ 换成 boolean semiring（布尔半环）：系数只能取 $0$ 或 $1$，加法是 OR。这时先要说清「span」指哪一种运算 —— 链 $1\to2\to3$ 的 adjacency matrix（邻接矩阵）$A$ 有三列，其 boolean span 只含 $\{\varnothing,\{0\},\{1\},\{0,1\}\}$，因为 OR 只会把列并起来，走不到两步之外；BFS 的 reachable set（可达集）$\{0,1,2\}$ 要的是 $C(A^*)$，$A^*$ 是 boolean 意义下的 transitive closure（传递闭包），实测它的非空列是 $\{0\}$ 与 $\{0,1\}$，读成「谁能到 $j$」。boolean 半环上的 span 与 $\mathbb{R}$ 上的 span 不是同一个运算，到达与「是某种组合」在这里也不是同一件事。
> 
> 落点：这张图的下一格是 $A=CR$。$C$ 收走 pivot columns（主元列），$R$ 记下坐标，于是 $C(A)$ 的 basis（基）从「从一堆列里挑出来的几个」变成「矩阵乘积的一侧」，rank（秩）也不再只是一个计数，而是两块矩阵的公共尺寸。

### Independent Columns and the Rank of $A$（独立列与矩阵的秩）

在写出那些话之后，我以为这一小节已经完成了。错了。

只需一个小小的 effort（努力），我们就可以为 $A$ 的 column space（列空间）找到一个 basis（基），将 $A$ factor（分解）为 $C$ 乘以 $R$，并且可以证明线性代数中的第一个 great theorem（伟大定理）。

你将看到矩阵的 rank（秩）和 subspace（子空间）的 dimension（维数）。

所有这些都源于对 independence（独立性）的理解。

目标是创建一个矩阵 $C$，其 columns（列）直接来自 $A$——但不包含任何是之前列的 combination（组合）的列。

$C$ 的 columns（列）（尽可能多地保留）将是 "independent（独立的）"。

以下是 $C$ 的一个自然构造：

- 如果 $A$ 的 column 1 不是全零，将其放入矩阵 $C$。
- 如果 $A$ 的 column 2 不是 column 1 的 multiple（倍数），将其放入 $C$。
- 如果 $A$ 的 column 3 不是 columns 1 和 2 的 combination（组合），将其放入 $C$。以此类推。

最终 $C$ 将有 $r$ 个 columns（列）（$r\le n$）。

它们将成为 $A$ 的 column space（列空间）的一个 "basis（基）"。

被排除的列是 $C$ 中那些 basic columns（基本列）的组合。

一个 subspace（子空间）的 basis（基）是一个 <span style="color:#00838f;">full set（完备集）</span> 的 independent vectors（独立向量）：该 space（空间）中的所有向量都是 basis vectors（基向量）的组合。

例子将说明这一点。

<span style="color:#2471a3;">**[example]**</span> **Example 4.** 
```math
A=\begin{bmatrix}1&3&8\\1&2&6\\0&1&2\end{bmatrix},\quad 
C=\begin{bmatrix}1&3\\1&2\\0&1\end{bmatrix},\quad r=2
```

Column 3 of $A$ 是 2(column 1) + 2(column 2)。将它排除在 $C$ 的 basis（基）之外。

<span style="color:#2471a3;">**[example]**</span> **Example 5.**
```math
A=\begin{bmatrix}1&2&3\\0&4&5\\0&0&6\end{bmatrix},\quad
C=A,\quad r=3
```

这个矩阵是 invertible（可逆）的。其 column space（列空间）是整个 $\mathbb{R}^3$。保留所有3列。

<span style="color:#2471a3;">**[example]**</span> **Example 6.**
```math
A=\begin{bmatrix}1&2&5\\1&2&5\\1&2&5\end{bmatrix},\quad
C=\begin{bmatrix}1\\1\\1\end{bmatrix},\quad r=1
```

数字 $r$ 是 $A$ 的 "rank（秩）"。它也是 $C$ 的秩。它统计 independent columns（独立列）的数量。

诚然，我们也可以从右到左处理 $A$，从它的最后 column（列）开始。

这不会改变最终的计数 $r$。

不同的 $A$ 的相同列空间 $C(A)$ 将总是给出相同的数字 $r$。

这个数字 $r$ 是 $A$ 和 $C$（相同空间）的 column space（列空间）的 "dimension（维数）"。

矩阵的 rank（秩）就是其 column space（列空间）的 dimension（维数）。

> <span style="color:#1e8449;">**[note] 线性无关、零空间、主元列是同一件事：**</span> 所谓 independent（线性无关），说的不是「这些向量看上去各走各的」，而是「同一个 $b$ 只有一种配方」。定义只有一行：$c_1a_1+\cdots+c_na_n=0$ 仅当 $c_1=\cdots=c_n=0$ 时成立。这一行的全部信息量，在于它把 existence（存在性）换成了 uniqueness（唯一性）—— 而唯一性在 6.042J 里早就有名字，叫 injection（单射）。
> 
> 定理（四个说法等价）：设 $A$ 是 $m\times n$ 的实矩阵，则 (i) $A$ 的 columns（列）independent；(ii) $N(A)=\{0\}$；(iii) $\operatorname{rank}(A)=n$；(iv) 每个 $b\in C(A)$ 的 representation（表示）唯一。证明如下，一步不缺（这套写法对照 Strang 的 *LaLFD* §I.2 与 Golub & Van Loan 的 *Matrix Computations* §2.4；两处章节号我都未能一手核实，手边没有原书，按通行引用写下）。(i)$\Leftrightarrow$(ii)：$Ax=0$ 逐字就是 columns（列）的一个 zero combination（零组合），而 $x=0$ 永远是解，independent 说的正是「除它以外一个都没有」，所以这两句是同一句话的两种标点。(ii)$\Rightarrow$(iv)：若 $Ax=b=Ay$，则 $A(x-y)=0$，由 (ii) 得 $x=y$。(iv)$\Rightarrow$(ii)：若 $x\ne0$ 而 $Ax=0$，则 $b=0$ 有两个 representation（表示），矛盾。
> 
> (ii)$\Rightarrow$(iii) 是唯一需要动手的一步。把 columns（列）按 pivot column（主元列）与 free column（自由列）分块，写成 $A=[A_P\ A_F]$，其中 $A_P$ 有 $r$ 列、列 independent，并且张成 $C(A)$ —— 它就是一个 basis（基）。于是任给 $x_F$，右端 $-A_Fx_F$ 落在 $C(A)$ 里，方程 $A_Px_P=-A_Fx_F$ 既有解又唯一：有解，因为 $A_P$ 张成整个 $C(A)$；唯一，因为 $A_Pz=0$ 只能给出 $z=0$。所以 free variable（自由变量）的每个取值恰好配一个解。只要存在 free column（自由列），取 $x_F\ne0$ 就得到一个 $x\ne0$ 而 $Ax=0$，与 $N(A)=\{0\}$ 矛盾，故 $r=n$。(iii)$\Rightarrow$(ii)：$r=n$ 时消元后没有 free variable（自由变量），back substitution（回代）从末行往上把每个分量压成 $0$。$\square$
> 
> 补一句方法论。(ii)$\Rightarrow$(iv) 这种写法是 6.042J 逻辑与证明一章里反复使用的 uniqueness template（唯一性模板）：先假设两个对象都满足同一个条件，再推出这两个对象相等。整本书里凡是形如「解唯一」「分解唯一」的结论，收尾都是同一个动作，一个字的改动都不需要。
> 
> 例子与反例一起看。书中 Example 4 的 $A$ 有三列，第三列由前两列给出：$a_3=2a_1+2a_2$。实测 $A$ 的 singular values（奇异值）是 $10.94416$、$0.47479$、$0$，那个 $0$ 就是 dependent（相关）的指纹；零空间由 $(-2/3,-2/3,1/3)\propto(-2,-2,1)$ 张成，对应 $2a_1+2a_2-a_3=0$，秩 $r=2<n=3$，所以不 independent。反例取 $2\times3$ 的 $B=\begin{bmatrix}1&2&3\\4&5&6\end{bmatrix}$，实测 $r=2$，零空间由 $(1,-2,1)$ 张成。这不是巧合：$n>m$ 时必有 $r\le m<n$，free variable（自由变量）至少一个，任何这样的矩阵都不可能 independent。
> 
> 两条边界顺手记下，其中只有第二条是真前提。第一条是 $m\ge n$：上面那个 $B$ 说明方程比未知数少时无关必然失败；需要讲清的是，$m\ge n$ 只是 (i) 可能成立的必要条件，不是四等价定理的隐含前提：定理对 $m<n$ 照常成立，只是那时四句同时为假，而「假蕴含假」的等价关系依旧成立。第二条是 field（域）：把系数限制在 $\mathbb{Z}$，单个向量 $\{2\}$ 与 $\{1\}$ 在 $\mathbb{Q}$ 上都 independent，但 $\{2\}$ 张不出 $1$，于是它有作 basis（基）的资格却没有作 basis（基）的事实 —— $\mathbb{Z}$ 上可逆的元素只有 $\pm1$，independent 这句判据还活着，span（张成）与 basis（基）已经死了。更狠的一刀是把 $\mathbb{R}$ 换成 $\mathbb{Z}/6\mathbb{Z}$：那里 $3\cdot2=0$ 而两个因子都不为零，判据却照样写得出来——拿非零的 $3$ 去乘 $[2]$ 得 $[0]$，直接判 $\{[2]\}$ 不 independent；零空间也仍是良定义的非平凡集合，$N([2])=\{[0],[3]\}$ 而不是 $\{[0]\}$。塌掉的不是判据、也不是零空间，而是 dimension（维数）那一整套：$\mathbb{Z}/6\mathbb{Z}$ 不是 field（域），「基的个数」不存在，rank（秩）作为列空间的维数无从定义，(iii) 立刻失去真假可言；若强行把 rank 定义成「无关列的个数」，它给出 $0\ne1$，(iii) 也假，四句于是同假——只是这样定义的 rank 已经不再满足 rank-nullity，(iii) 与 (ii) 的等价就靠不住了。这两条合起来说明：「无关」这个词之所以干净，全靠除法随时可用。
> 
> 跨课程：6.042J 的函数一节里，$f:X\to Y$ 是 injection（单射）的判据是 $f(x_1)=f(x_2)\Rightarrow x_1=x_2$；把 $f$ 取成 $T(x)=Ax$，这两行字与上面的 (ii)$\Rightarrow$(iv) 逐字同构，连证明都不用改（只多用一条：$T$ linear 保证 $T(x)-T(y)=T(x-y)$）。再进一步看本节那个构造：「按顺序扫列，凡不是前面 columns（列）的 combination（组合）就收下」，这是在贪心求 maximal independent set（极大无关组），而贪心在这里最优不是运气 —— independent 满足 exchange property（交换性质），构成一个 matroid（拟阵）。Whitney 在 1935 年 *American Journal of Mathematics* 57(3):509--533 把这组公理抽出来（卷期页码已核实），CLRS 里 Kruskal 的正确性证明用的正是同一条 matroid（拟阵）贪心定理，而 6.042J 的 Hall 定理就是这套「先用小的、再拿交换律把它换大」的想法在二分图匹配上的判据。所以 basis（基）不只属于线性代数，它是「能贪心」这件事的一般形状。
> 
> 落点：这一步之后，rank（秩）有了两副面孔 —— counting（计数）意义上的「independent columns（列）的个数」，与 dimension（维数）意义上的「$C(A)$ 的维数」。下一节 $A=CR$ 就是把这两副面孔缝在同一块布上的那一针：$C$ 收走 pivot columns（主元列），$R$ 记下其余各列怎样由它们表出。

### The Factorization $A=CR$（分解 $A=CR$）

矩阵 $C$ 通过一个第三个矩阵 $R$ 连接到 $A$：$A=CR$。

它们的形状是 $(m\times n)=(m\times r)(r\times n)$。

我可以在上面的 Example 4 中展示这个 "factorization（分解）"：

```math
\begin{bmatrix}1&3&8\\1&2&6\\0&1&2\end{bmatrix}
= \begin{bmatrix}1&3\\1&2\\0&1\end{bmatrix}
\begin{bmatrix}1&0&2\\0&1&2\end{bmatrix}
= CR
```

当 $C$ 乘以 $R$ 的第一列 $\begin{bmatrix}1\\0\end{bmatrix}$，我们得到 $C$ 的 column 1：即 $A$ 的 column 1。

当 $C$ 乘以 $R$ 的第二列 $\begin{bmatrix}0\\1\end{bmatrix}$，我们得到 $C$ 的 column 2：即 $A$ 的 column 2。

当 $C$ 乘以 $R$ 的第三列 $\begin{bmatrix}2\\2\end{bmatrix}$，我们得到 2(column 1) + 2(column 2)：即 $A$ 的 column 3。

这一切匹配 $A$ 的 column 3。

我们所做的只是把正确的数字放入 $R$。

$C$ 的 columns（列）的组合产生 $A$ 的 columns（列）。

那么 $A=CR$ 将所有信息存储为一次 matrix multiplication（矩阵乘法）。

实际上 $R$ 是线性代数中一个著名的矩阵：$R=\text{rref}(A)$（$A$ 的 row-reduced echelon form（行简化阶梯形），不含零行）。

Example 5 中 $C=A$，然后 $R=I$（identity matrix（单位矩阵））。

Example 6 中 $C$ 只有一列，所以 $R$ 只有一行：

```math
\begin{bmatrix}1&2&5\\1&2&5\\1&2&5\end{bmatrix}
= \begin{bmatrix}1\\1\\1\end{bmatrix}
\begin{bmatrix}1&2&5\end{bmatrix}
= CR
```

所有三个矩阵的 rank（秩）都是 $r=1$。

> <span style="color:#1e8449;">**[note] $A=CR$ 是「秩」的第一张身份证：**</span> 这条注不谈压缩，只谈层级：$A=CR$ 站在定义 rank（秩）的那一层，往下到 $A=LU$、往上到 $A=U\Sigma V^T$，每一层各多买了什么。
> 
> 先说它回答的问题。一个 $m\times n$ 的矩阵有 $mn$ 个 entry（元素），但独立的方向只有 $r$ 个。$A=CR$ 把矩阵拆成两半：一半装方向，即 pivot columns（主元列）排成的 $C$；一半装坐标，即每一列相对这些方向的系数排成的 $R$。rank 的定义是「column space（列空间）的 dimension（维数）」，这个定义在 $CR$ 里第一次变成可算的对象：$C$ 的列数就是那个 dimension，而 $R$ 的行数把它又数了一遍。于是 $r$ 不再是一个只能靠消元数出来的计数，而是两块矩阵的公共尺寸 $(m\times r)(r\times n)$ —— 一个形状，不是一个数字。
> 
> 精确陈述如下。设 $A$ 为 $m\times n$、$r=\text{rank}(A)$，令 $R$ 是 $\text{rref}(A)$ 删去全零行后得到的 $r\times n$ 矩阵，再取 $A$ 中与 $R$ 的 pivot 列编号相同的那 $r$ 列、按原顺序排成 $m\times r$ 的 $C$，则 $A=CR$，且 $R$ 的 pivot 列（在 $R$ 内部）恰好组成 $I_r$ 的列。pivot 列不一定排在最前面，下面的反例里它们就是第 1 列与第 3 列。
> 
> 直觉是字母表与文稿。$C$ 的 $r$ 列是字母表，$R$ 的每一列是一篇用字母表写成的稿子：$R$ 第 $j$ 列第 $k$ 个数字，是 $A$ 第 $j$ 列在基向量 $c_k$ 上的坐标 —— 是坐标，不是「含有几个 $c_k$」。书中 Example 4 的 $R$ 第 3 列是 $(2,2)^T$，于是 $2c_1+2c_2=(8,6,2)^T$ 正是 $A$ 的第 3 列；我逐项复算过，$CR$ 与 $A$ 的最大偏差是 $0$。
> 
> 为什么 $C$ 必须是 pivot 列、$R$ 必须是删零行的 rref（行简化阶梯形）？两件事各管一半。$C$ 管「rank 不塌」：随便取前 $r$ 列就会塌。取三列依次为 $(1,2,1)^T$、$(2,4,2)^T$、$(3,7,4)^T$ 的 $A$，它的 rank 是 2，但前两列成比例，拿它们当 $C$ 只张成一条直线，而第 3 列不在这条直线上：我实测这两列的 rank 是 1，加上第 3 列后变 2，所以任何 $R^{\prime}$ 都救不回来。$R$ 管「坐标唯一」：若只要求存在某个 $R$ 使 $A=CR$，那 $C$ 可以整体乘 $c$、$R$ 整体除 $c$，坐标就不可读；把 $R$ 钉死为删零行的 rref，pivot 列上的 $I_r$ 一举给出两件事 —— $C$ 的列 independent（独立），以及每列坐标的唯一数字。
> 
> 「$CR$ 不省存储」这件事，本节末尾那张价目表已经数过个数，这里只补它的判据：$C$ 与 $R$ 合起来 $(m+n)r$ 个数，只在 $r<mn/(m+n)$ 时少于 $mn$，$1000\times1000$ 时门槛是 $r<500$。所以 $CR$ 的价值不在省内存，而在把 rank 摆到台面上；真要靠低秩省存储，得做截断，那是 SVD 的事。
> 
> 把三个分解并排看，就是三层楼。$A=CR$ 在地下室：消元顺手就拿到，零额外代价，$C$ 的列不正交、$R$ 的行也不正交；要小心的是这份便宜有价格 —— $C$ 的列越接近 linear dependence（线性相关），$R$ 里的坐标就越大，而重建 $A$ 时的浮点误差会被 $\kappa(C)$（$C$ 的条件数）放大，列正交时这个因子是 $1$，列几乎相关时它可以任意大。$A=LU$ 在一楼：为求解服务，强制一侧单位下三角、一侧上三角，代价是要么假定不必行交换、要么多背一个 permutation（置换）$P$，约 $n^3/3$ 次运算。$A=U\Sigma V^T$ 在顶楼：两侧都 orthonormal（标准正交）、系数非负且降序，代价是两次正交化，换回 Eckart–Young 意义下的最优截断。三层都在写 $A=\sum_{k=1}^{r}(\text{rank one piece})$，差别只在 piece 有多干净：$CR$ 的 piece 是斜的，$LU$ 的 piece 是三角的，SVD 的 piece 是正交的。
> 
> 所以书中 §I.2 末尾列五种 factorization（分解）时没有 $CR$：那五种是 $A=LU$、$A=QR$、$S=Q\Lambda Q^T$、$A=X\Lambda X^{-1}$、$A=U\Sigma V^T$，每一种的因子里都装着 eigenvalue（特征值）或 singular value（奇异值）这类内部信息，而 $CR$ 只装着两样外部可见的东西：哪些列独立、坐标是多少。$S=Q\Lambda Q^T$ 之所以必须在这张表里，并且左边写成 $S$ 而不是 $A$，是因为它把「两侧同时正交」与「对称」一次性兑换：只有对称矩阵才有正交的 eigenvector 矩阵，$Q^{-1}=Q^T$ 才成立；写成一般的 $A$ 就不成立，写成 $X\Lambda X^{-1}$ 才是通例。
> 
> 史实坐标：行简化阶梯形来自 Gauss 的消元法，Jordan 在 1888 年给出连主元上方也清零的变体。Wilhelm Jordan（1842--1899）不是代数学家而是测地学家，那篇文章出自《Handbuch der Vermessungskunde》第 3 版，语境是测量平差 —— 观测值的最小二乘归算，不是微分方程；详细的史实考证见 Althoen 与 McLaughlin, *Amer. Math. Monthly* 94 (1987) 130--142。把 $CR$ 提为第一种 factorization、并用它一步证 rank theorem（秩定理）是 Strang 的教学选择。
> 
> 跨课程只说一句：这套东西在 Strang 18.06 里就是消元那几讲，pivot columns、special solutions、$R=\text{rref}$ 都在那里；在 6.042J 里它就是「选一组基则每个元素有唯一坐标」，即坐标映射 $x\mapsto Cx$ 是 injection（单射），所以 $R$ 的列能被唯一读出。
> 
> 下一条注证 column rank = row rank，整个证明不要新工具，只要这一条 $A=CR$ 加上「$R$ 的 pivot 列是 $I_r$」这一眼。

### Column Rank = Row Rank（列秩 = 行秩）

Independent columns（独立列）的数量等于 independent rows（独立行）的数量。

这个 rank theorem（秩定理）对每个矩阵都成立！

在线性代数中，columns（列）和 rows（行）总是协同工作的！

$m$ 行包含与 $n$ 列相同的数字 $a_{ij}$，但它们是不同的 vectors（向量）。

这个定理通过 $A=CR$ 得到证明。

从不同的角度来看——按 rows（行）而非 columns（列）。

矩阵 $R$ 有 $r$ 行。

乘以 $C$ 取那些行的 combinations（组合）。

由于 $A=CR$，我们从 $R$ 的 $r$ 行中得到 $A$ 的每一行。

而且这 $r$ 行是 independent（独立）的，所以它们是 $A$ 的 row space（行空间）的一个 basis（基）。

$A$ 的 column space（列空间）和 row space（行空间）都有 dimension（维数）$r$，各有 $r$ 个 basis vectors（基向量）——$C$ 的 columns（列）和 $R$ 的 rows（行）。

**一个注记：** 为什么 $R$ 有 independent rows（独立行）？再看 Example 4。

```math
A=\begin{bmatrix}1&3&8\\1&2&6\\0&1&2\end{bmatrix},\quad
R=\begin{bmatrix}1&0&2\\0&1&2\end{bmatrix}
```

正是 $R$ 中的那些 ones（1）和 zeros（0）告诉我：没有一行是其他行的 combination（组合）。

对于 data science（数据科学），重要的 factorization（分解）是 $A$ 的 "SVD"——当第一个因子 $C$ 有 $r$ 个 orthogonal columns（正交列），第二个因子 $R$ 有 $r$ 个 orthogonal rows（正交行）时。

> <span style="color:#1e8449;">**[note] 列秩等于行秩的两条证明路径，以及它在张量上为什么塌：**</span> 这条注把 rank theorem（秩定理）证完，两条路径各走一遍，再说明这个等号依赖「矩阵只有两个指标」这个前提，换成张量就不成立。
> 
> 定理：对任意域上的 $m\times n$ 矩阵 $A$，column rank（列秩）等于 row rank（行秩）。它不显然，因为列住在 $\mathbb{R}^m$、行住在 $\mathbb{R}^n$，两个不同空间里的维数凭什么相等。等号的含义是：$A$ 作为线性映射 $\mathbb{R}^n\to\mathbb{R}^m$，其 image（像）的维数等于它的 transpose（转置）的 image（像）的维数。也就是说，矩阵那 $mn$ 个数字把两个空间的维数焊在一起，这是有限维线性代数最硬的一条刚性。
> 
> 路径一，用 $A=CR$，四步走完。第一步，取上一条注的分解 $A=CR$，$C$ 是 $m\times r$、$R$ 是 $r\times n$，$r$ 是 pivot columns（主元列）的个数，于是 column rank（列秩）等于 $r$。第二步，记 $C_i$ 为 $C$ 的第 $i$ 行，则 $A$ 的第 $i$ 行等于 $C_iR$，即 $A$ 的每一行都是 $R$ 那 $r$ 行的线性组合，故 row space（行空间）有包含关系，$A$ 的行空间落在 $R$ 的行空间里。第三步，$R$ 的 $r$ 行 independent（独立）：设 $y^TR=0$，$R$ 的主元列组成 $I_r$，只取这些列得 $y^T=0$，故 $y=0$；于是 $R$ 的行空间维数恰为 $r$，配合第二步得 row rank（行秩）不超过 $r$。第四步，把前三步原样施加到 $A^T$ 上，$A^T=R^TC^T$ 是同形状的分解，得到 $A^T$ 的行秩不超过 $A^T$ 的列秩；而 $A^T$ 的行秩就是 $A$ 的 column rank（列秩）、$A^T$ 的列秩就是 $A$ 的 row rank（行秩），所以这一步给出的正是 column rank（列秩）不超过 row rank（行秩）。两个方向的不等式合起来，等号成立。
> 
> 路径二，用消元，同样四步。第一步，消元的每一步是左乘一个可逆的 elementary matrix（初等矩阵）$E$；$EA$ 的行是 $A$ 的行的组合，而 $A=E^{-1}(EA)$ 给出反向包含，所以行空间不变。第二步，于是 $A$ 与 $R=\text{rref}(A)$ 有同一 row space（行空间），其维数等于 $R$ 的非零行数 $r$，直接给出 row rank（行秩）等于 $r$。第三步，同一批行运算也管列：$R=EA$ 即 $A=E^{-1}R$，$R$ 的主元列是 $I_r$ 的列，而 $E^{-1}$ 可逆，把 independent（独立）的列映成 independent（独立）的列，所以 $A$ 对应的那 $r$ 列 independent（独立）。第四步，$R$ 的每一列都是 $I_r$ 的列的组合，左乘 $E^{-1}$ 之后，$A$ 的每一列都是那 $r$ 个主元列的组合，故 column rank（列秩）也等于 $r$。
> 
> 还有一条更概念的走法，可当交叉检验。rank-nullity（秩-零化度）给出 $n=\dim C(A)+\dim N(A)$ 与 $m=\dim C(A^T)+\dim N(A^T)$，而 four subspaces（四个基本子空间）那幅图给出 $N(A^T)=C(A)^{\perp}$，于是 $\dim C(A^T)=m-(m-\dim C(A))=\dim C(A)$。这条走法把等号翻译成「两个 orthogonal complement（正交补）的维数互补」，比矩阵运算干净，前提是先建好内积。
> 
> 两条证明的关系值得点一句：路径一是构造性的，顺手给出 basis（基）；路径二是计算性的，顺手给出算法。书中先走第一条，因为 $CR$ 已经在手，不必再引入「行运算不改变行空间」这条额外引理。
> 
> 数值上我特意不用 SVD（奇异值分解）算 rank（秩），因为奇异值天然对称，用它验等号等于用结论验结论。改用纯分数消元数两套独立量：书中 Example 4 的 $A$，主元列数为 2、$\text{rref}$ 的非零行数为 2；我的反例 $A$（三列依次为 $(1,2,1)^T$、$(2,4,2)^T$、$(3,7,4)^T$），主元列数为 2、非零行数也为 2，两边相等。
> 
> 等号依赖两个前提：只有两个指标，系数在域里。换掉第一个就得到张量。对三阶 array（数组）$T$，CP rank（CP 秩）定义为写成 $\sum_{k=1}^{R}a_k\otimes b_k\otimes c_k$ 的最小 $R$。三个方向看似共享同一个 $R$，等号却会塌，机制是：矩阵的证明里 $A=CR$ 只用了一次乘法、一个求和指标，行与列共用它；而把张量按某个 mode flatten（展平）成矩阵时，$b_k\otimes c_k$ 被压成一个向量，rank（秩）会掉，掉多少取决于这组压出来的向量有多相关。
> 
> 我实测两个例子。$T=e_1\otimes e_1\otimes e_1+e_2\otimes e_2\otimes e_1$ 的三个 mode（模式）展开的秩为 $(2,2,1)$；$2\times2\times2$ 的 $W$ state，即 $e_1\otimes e_1\otimes e_2+e_1\otimes e_2\otimes e_1+e_2\otimes e_1\otimes e_1$，三项写出、CP rank（CP 秩）为 3，而三个展开的 rank（秩）全是 2。矩阵没有这个现象：$A$ 与 $A^T$ 的 rank（秩）由同一批 singular value（奇异值）决定，永远相等。
> 
> 史实坐标：CP rank（CP 秩）能超过 $\max(m,n,p)$ 的经典例子就是 Strassen 的 $W$ state（CP rank 为 3，border rank（边秩）为 2），其原文我未能一手核实；矩阵情形则从 Gauss 消元起就成立，Strang 18.06 把它放在 four subspaces（四个基本子空间）那一讲，$r$ 从 rref（行简化阶梯形）一次读出；6.042J 里它是「两个有限集等势当且仅当存在 bijection（双射）」的线性版本，coordinates（坐标）与 vectors（向量）之间的双射就是 rank（秩）对称性的离散原型。
> 
> 下一条该拿下的是 $A=LU$：路径二的第一步会从「引理」升级成主题，消元本身被写成一个 factorization（分解）。

---

<span style="color:#7f8c8d">*以上为 p6-11（Part I 引言 + §I.1 完整）的极高密度逐句翻译。每句原文对应一句翻译。OCR 错误已根据数学知识全部修正。*</span>

---

<span style="color:#2471a3;">**[section]**</span> **I.2 Matrix-Matrix Multiplication AB（矩阵-矩阵乘法 AB）**

---

矩阵乘法 $AB=C$ 有两种互补的视角：inner products（内积）方式和 outer products（外积）方式。

Inner product（内积）方式按行乘列逐个计算 $C$ 中的每个数字，而 outer product（外积）方式将 $AB$ 视为 rank-one matrices（秩一矩阵）的和。

后者对于理解矩阵的 structure（结构）至关重要。

### Inner Products（内积）方式

$A$ 的行乘以 $B$ 的列，产生 $C$ 中的每个 entry（元素）。

$A$ 的 row 2（第2行）和 $B$ 的 column 3（第3列）给出 $C$ 中的 $c_{23}$：

```math
c_{23} = a_{21}b_{13} + a_{22}b_{23} + a_{23}b_{33} = \sum_{k=1}^{n} a_{2k}b_{k3}
```

这是 dot product（点积）$C_{23} =$（row 2 of $A$）$\cdot$（column 3 of $B$）。

用 summation notation（求和符号）写为：

```math
c_{ij} = \sum_{k=1}^{n} a_{ik}b_{kj}
```

这就是我们通常计算 $AB=C$ 中每个 number（数字）的方式。

但还有另一种方式。

### Columns of A Times Rows of B（$A$ 的列乘以 $B$ 的行）

另一种乘法 $AB$ 的方式是 $A$ 的 columns（列）乘以 $B$ 的 rows（行）。

我们必须看到这一点！

让我从 numbers（数字）开始，说明两个 key points（关键要点）。

一个 column（列）$u$ 乘以一个 row（行）$v^T$ 产生一个 matrix（矩阵）$uv^T$。

<span style="color:#2471a3;">**[example]**</span> **Outer product（外积）示例：**

```math
\begin{bmatrix}2\\2\\1\end{bmatrix}
\begin{bmatrix}3 & 4 & 6\end{bmatrix}
= \begin{bmatrix}
6 & 8 & 12 \\
6 & 8 & 12 \\
3 & 4 & 6
\end{bmatrix}
```

这个矩阵 $uv^T$ 被称为 "outer product（外积）"。

它是一个 <span style="color:#00838f;">rank one matrix（秩一矩阵）</span>。

一个 $m\times1$ 的 matrix（矩阵）（a column）乘以一个 $1\times p$ 的 matrix（矩阵）（a row $v^T$）给出一个 $m\times p$ 的 matrix（矩阵）。

### What is Special About a Rank One Matrix（秩一矩阵的特殊之处）

秩一矩阵 $uv^T$ 的特殊之处在于：

$uv^T$ 的所有 columns（列）都是 $u$ 的 multiples（倍数），所有 rows（行）都是 $v^T$ 的 multiples（倍数）。

$uv^T$ 的 column space（列空间）是 one-dimensional（一维）的——即通过 $u$ 的直线。

Column space（列空间）的 dimension（维数）（即 independent columns（独立列）的数量）就是矩阵的 rank（秩）——这是一个 <span style="color:#00838f;">key number（关键数字）</span>。

所有非零矩阵 $uv^T$ 的 rank（秩）都是 1。

它们是每个矩阵的完美 building blocks（构建块）。

同时注意：$uv^T$ 的 row space（行空间）是通过 $v^T$ 的直线。

根据 definition（定义），任何矩阵的 row space（行空间）就是其 transpose（转置）$A^T$ 的 column space（列空间）$C(A^T)$。

这样我们始终处理 column vectors（列向量）。

在这个例子中，我们对 $uv^T$ 取 transpose（转置）（将行与列交换），得到矩阵 $vu^T$：

```math
vu^T = \begin{bmatrix}3\\4\\6\end{bmatrix}\begin{bmatrix}2&2&1\end{bmatrix}
= \begin{bmatrix}
6 & 6 & 3 \\
8 & 8 & 4 \\
12 & 12 & 6
\end{bmatrix}
```

注意 $vu^T$ 的所有 columns（列）都是 $v$ 的 multiples（倍数），所有 rows（行）都是 $u^T$ 的 multiples（倍数）。

> <span style="color:#1e8449;">**[note] 秩一矩阵是压缩的原子：**</span> 这条注解释 $uv^T$ 为什么被叫做 building block（构建块）：它的存储、它的真实自由度、它作为 SVD（奇异值分解）原子的地位，以及「用模型假设换存储」这个和 CLRS 共享的结构。
> 
> 先从记号说起，所谓 rank one matrix（秩一矩阵）指的就是 $uv^T$：一个 $m\times1$ 的列乘一个 $1\times n$ 的行。它特殊，因为 $mn$ 个 entry（元素）被压进 $m+n$ 个参数，而且压的方式是纯乘法、没有任何求和。但参数个数不等于自由度：$m+n$ 个参数里只有 $m+n-1$ 个是自由的，剩下那一维是 scale（缩放）冗余 —— $(cu,\,v/c)$ 与 $(u,v)$ 给出同一个 $uv^T$，$c$ 非零。把 scale 钉死（例如令 $\|u\|=1$）之后，$m+n-1$ 个参数与 $uv^T$ 一一对应，这就是「冗余只有一维」的准确说法。这个位置让它同时是三个东西：SVD 的原子，因为 $A=\sum_k\sigma_ku_kv_k^T$ 的每一项都是它；压缩的原子，因为存 $m+n$ 而不是 $mn$；以及「rank（秩）是信息量」这句话的度量单位。
> 
> 三条命题合起来就是它的全部特殊性。命题一，设 $u$、$v$ 均非零，则 rank 为 1，column space（列空间）是过 $u$ 的直线，row space（行空间）是过 $v^T$ 的直线；证明只需一个等式 $(uv^T)x=u(v^Tx)$：右边永远落在过 $u$ 的直线上，且 $x=v$ 时非零，故像恰是一维。命题二，同一等式给出乘法捷径，但前提要写全：若 $uv^T$ 已经存成一个 $m\times n$ 矩阵，$(uv^T)x$ 仍要 $mn$ 次乘法；只有保留因子形式才只需 $v^{T}x$ 的 $n$ 次乘法与 $n-1$ 次加法，再由 $u$ 乘这个标量的 $m$ 次乘法，合计 $m+n$ 次乘、$n-1$ 次加，这是「低秩则快」的最小样本。命题三，映射 $(u,v)\mapsto uv^T$ 的 fiber（纤维）是 $(cu,\,v/c)$，是一维的，所以像的真实自由度是 $m+n-1$。
> 
> 数值上先对齐书中的外积例子。书中写的是 $vu^T=\begin{bmatrix}3\\4\\6\end{bmatrix}\begin{bmatrix}2&2&1\end{bmatrix}=\begin{bmatrix}6&6&3\\8&8&4\\12&12&6\end{bmatrix}$，其中 $v=(3,4,6)^T$、$u=(2,2,1)^T$ 都作列向量；若按 $uv^T$ 的顺序乘，得到 $\begin{bmatrix}6&8&12\\6&8&12\\3&4&6\end{bmatrix}$，恰好是它的 transpose（转置）。两者 rank 都是 1，每一行都是 $(3,4,6)$ 的倍数，$3+3=6$ 个数存下 9 个数。规模上去才见真章：$1000\times1000$ 的 float64 矩阵是 $8\times10^6$ 字节，秩一时只要 $2000\times8=16000$ 字节，省 500 倍；秩十时 $10\times2000\times8=160000$ 字节，省 50 倍。
> 
> 非例子是 $I_2$。若 $I_2=uv^T$，非对角元给出 $u_1v_2=0$ 与 $u_2v_1=0$，对角元给出 $u_1v_1=u_2v_2=1$，四个数被迫全非零，矛盾。定量地说，最佳秩一逼近的残差不小：$I_2$ 的两个 singular values 都是 1，截掉一个后 Frobenius 残差是 1，等于说用一个 piece 表示它，误差和信号一样大 —— 原子这个词就是这个意思，它需要两个 piece。
> 
> 两个前提一去掉就塌。若 $u$ 或 $v$ 是零向量，$uv^T$ 是零矩阵，rank 为 0，所以「秩一」这个词要求两侧都非零。若放宽成「近似秩一」，省下的存储立刻变成误差，而误差有精确下界：Eckart–Young 定理（1936）说最佳 rank 为 $k$ 的逼近就是前 $k$ 个 $\sigma_ku_kv_k^T$ 之和，Frobenius 残差等于尾部奇异值平方和开根。我实测一个 $50\times50$ 的秩三矩阵：取 `np.random.default_rng(20261122)` 生成两组随机正交因子 $U_3$、$V_3$，与谱 $(667.10,34.31,30.77)$ 拼成 $U_3\operatorname{diag}(\cdot)V_3^T$，回测的前三个 singular values 正是 $667.10$、$34.31$、$30.77$；用三项表示残差为 $0$，用一项（最佳秩一）残差是 $46.09$，正是 $\sqrt{34.31^2+30.77^2}=46.0865$。
> 
> 于是压缩有了统一语法：每一档都是拿一个结构假设换存储。sparse（稀疏）假设多数 entry 为零，CSR（压缩稀疏行）每个非零只存三个数；low rank（低秩）假设行是少数几行的组合，存 $r(m+n)$ 个数；SVD 截断把两者统一成「谱的稀疏」。阈值很干脆：$r(m+n)<mn$ 即 $r<mn/(m+n)$，$1000\times1000$ 时是 $r<500$，超过它低秩表示反而比原矩阵更大。
> 
> 与 CLRS 第 11 章（hash tables）的同构在于赌注的形状，MIT 6.006 的 hashing 讲次沿用的就是这一章：hashtable（哈希表）的期望 $O(1)$ 查找依赖 simple uniform hashing（简单均匀哈希）假设，假设破了退化成 $O(n)$；秩一的 $m+n$ 存储依赖「矩阵真的秩一」，假设破了要么退回 $mn$（精确），要么付出残差（近似）。CSAPP 第 6 章的 cache（缓存）是第三个同构：它假设 locality（局部性），假设破了 hit rate（命中率）就塌。三者结构完全一样，模型越强，省得越多，最坏情况越糟。
> 
> 史实坐标：把矩阵乘法定成行乘列的是 Cayley 1858 年的那篇 memoir（回忆录），而 $n\times1$ 乘 $1\times n$ 得 $n\times n$ 的 outer product（外积）是那个定义的极端特例，秩一的全部代数都从那里来；按 singular value 排序截断的思想来自 Schmidt 1907 与 Eckart–Young 1936，后者我按公式复算过，原文未能一手核实。
> 
> 落点：这一节之后 Strang 立刻把 $AB$ 写成「$A$ 的列乘 $B$ 的行」的求和，那只是把原子用在乘法上；真正兑现的是五种 factorization（分解）那张总表，它把「原子」摊成一张价目表，每一种都在回答「用哪种 piece 拆、拆几个」。

### AB = Sum of Rank One Matrices（$AB$ = 秩一矩阵之和）

<span style="color:#2471a3;">**[theorem]**</span> 矩阵乘法 $AB$ 可以写为 $n$ 个 rank one matrices（秩一矩阵）的和：

```math
AB = \sum_{k=1}^{n} (\text{column } k \text{ of } A)(\text{row } k \text{ of } B)
```

这里是一个 2×2 的例子，展示 $n=2$ 个 pieces（column × row）之和：

```math
AB = \begin{bmatrix}1&3\\0&1\end{bmatrix}\begin{bmatrix}2&2\\0&5\end{bmatrix}
= \begin{bmatrix}1\\0\end{bmatrix}\begin{bmatrix}2&2\end{bmatrix}
+ \begin{bmatrix}3\\1\end{bmatrix}\begin{bmatrix}0&5\end{bmatrix}
= \begin{bmatrix}2&2\\0&0\end{bmatrix} + \begin{bmatrix}0&15\\0&5\end{bmatrix}
= \begin{bmatrix}2&17\\0&5\end{bmatrix}
```

两种方式（inner products vs outer products）涉及完全相同的 multiplications（乘法）$a_{ik}b_{kj}$，只是顺序不同。

内积方式需要 $mnp$ 次乘法，外积方式也需要 $mnp$ 次乘法——计算量完全相同。

但外积方式的关键 advantage（优势）在于它揭示了矩阵的 structure（结构）。

### Insight from Column Times Row（列乘行的洞察）

为什么 outer product（外积）approach（方法）在 data science（数据科学）中至关重要？

简短的回答是：它展示了矩阵的 rank（秩）——我们通常不关心矩阵中最大的数字是什么，我们更关心矩阵的 largest piece（最大组成部分）。

那些 pieces（部分）就是 rank one matrices（秩一矩阵）。

在应用线性代数中，一个 dominant theme（核心主题）是：

将 $A$ factor（分解）为 $CR$，然后观察 $A=CR$ 的 pieces（部分）$c_k r_k$。

### Five Important Factorizations（五种重要分解）

Factoring（分解）是 multiplying（乘法）$CR=A$ 的逆向过程。

分解需要更长时间，尤其是当 pieces（部分）涉及 eigenvalues（特征值）或 singular values（奇异值）时。

但这些数字包含了关于矩阵的 inside information（内部信息）——在分解之前是不可见的。

以下是五种重要的 factorizations（分解）：

<span style="color:#2471a3;">**[definition]**</span> **1. $A = LU$（消元分解）.** 来自 elimination（消元法）。行组合将 $A$ 化为 $U$，再将 $U$ 代回 $A$。$L$ 是 lower triangular（下三角矩阵），$U$ 是 upper triangular（上三角矩阵）。

<span style="color:#2471a3;">**[definition]**</span> **2. $A = QR$（正交-三角分解）.** 来自对 $A$ 的列进行 orthogonalizing（正交化），如 Gram-Schmidt 过程。$Q$ 有 orthonormal columns（标准正交列），$Q^TQ=I$，$R$ 是 upper triangular（上三角矩阵）。

<span style="color:#2471a3;">**[definition]**</span> **3. $S = Q\Lambda Q^T$（对称矩阵谱分解）.** 适用于 symmetric matrix（对称矩阵）$S=S^T$。Eigenvalues（特征值）$\lambda_i$ 在对角矩阵 $\Lambda$ 中，orthonormal eigenvectors（标准正交特征向量）在 $Q$ 的列中。

<span style="color:#2471a3;">**[definition]**</span> **4. $A = X\Lambda X^{-1}$（对角化）.** 适用于 $n\times n$ 且有 $n$ 个 independent eigenvectors

（独立特征向量）的矩阵 $A$。Eigenvalues（特征值）在 $\Lambda$ 的对角线上，eigenvectors（特征向量）在 $X$ 的列中。

<span style="color:#2471a3;">**[definition]**</span> **5. $A = U\Sigma V^T$（奇异值分解 SVD）.** 适用于任何矩阵（方阵或非方阵）。Orthogonal singular vectors（正交奇异向量）在 $U$ 和 $V$ 中，singular values（奇异值）$\sigma_i$ 在对角矩阵 $\Sigma$ 中。

让我以第3种分解（对称矩阵的谱定理 $S=Q\Lambda Q^T$）为例来说明这个 idea（想法）。

对称矩阵 $S$ 有正交的单位 eigenvectors（特征向量）$q_1,\dots,q_n$。

这些互相 perpendicular（垂直）的 eigenvectors（d0t products = 0）放入 $Q$ 的列中。

$S$ 和 $Q$ 是线性代数中的 kings 和 queens。

```math
S = Q\Lambda Q^T = \sum_{k=1}^{n} \lambda_k q_k q_k^T
```

每个 eigenvalue（特征值）$\lambda_k$ 和每个 eigenvector（特征向量）$q_k$ 贡献一个 rank one piece（秩一组成部分）$\lambda_k q_k q_k^T$ 给 $S$。

SVD $A=U\Sigma V^T$ 是类似的思想，当 singular value（奇异值）$\sigma$ 在对角矩阵 $\Sigma$ 中重复 $M$ 次时，需要额外的处理——会有 $M$ 对 singular vectors（奇异向量）$v$ 和 $u$，满足 $Av=\sigma u$。

> <span style="color:#1e8449;">**[note] 五种分解各自解决什么问题：**</span> 这里说的 factorization（分解），在人类知识里的位置不是把矩阵拆得好看，而是把一整块黑箱换成几个带名字的因子：因子的名字本身编码了可以读出的量——主元、正交性、奇异值。上面五条并列容易看成五个技巧，其实它们各自回答一个不同的问题；分解选错，问题不是变难，而是变得不可回答。
> 
> 第一问：同一个 $A$、许多个 $b$，要反复解 $Ax=b$，用 $A=LU$。一次 elimination（消元）花 $n^{3}/3$ 次乘加，之后每个 $b$ 只要两次 triangular solve（三角回代），各约 $n^{2}$ 步。取 $n=1000$，前者 $3.33\times10^{8}$，后者 $2\times10^{6}$，差两个数量级——这就是"分解一次、复用多次"的全部算术理由。直接算 $A^{-1}$ 再乘 $b$ 走的是 $n^{3}$ 量级，且 $A^{-1}$ 通常是稠密的，是教科书里最贵的坏习惯。
> 
> 第二问：least squares（最小二乘）$\min\|Ax-b\|$，用 $A=QR$。原因是 condition number（条件数）会被平方：取 $A=\begin{bmatrix}1&2&3\2&5&7\3&7&8\end{bmatrix}$（对称，$\det A=-2$），实测 $\operatorname{cond}(A)=83.41$，而 $\operatorname{cond}(A^{T}A)=6957.52$，正好是 $83.41^{2}$。走 normal equation（正规方程）$A^{T}Ax=A^{T}b$ 等于先把误差放大八十多倍再交给求解器；$Q^{T}Q=I$ 让 $R$ 承接几何信息而不放大它。
> 
> 第三问：判断正定、算矩阵幂、解 differential equation（微分方程），用 $S=Q\Lambda Q^{T}$。它只对 symmetric matrix（对称矩阵）成立：此时 eigenvalue（特征值）全实、eigenvector（特征向量）互相 orthogonal（正交），$Q^{-1}$ 就是 $Q^{T}$，一次转置代替求逆。上面那个 $A$ 恰好对称，实测 eigenvalue（特征值）为 $-0.781895$、$0.175117$、$14.606778$；把 $A$ 连乘五次，eigenvalue（特征值）精确等于各自五次方，最大那个是 $14.606778^{5}=664924.29$。这就是"幂等于对角元的幂"的机制。
> 
> 第四问：$n$ 阶方阵的迭代 $u_{k+1}=Au_{k}$，用 $A=X\Lambda X^{-1}$。它把条件放宽到"有 $n$ 个 independent eigenvector（独立特征向量）"，代价是 $X^{-1}$ 要真算。非例子：$A=\begin{bmatrix}1&1\\0&2\end{bmatrix}$ 有互异 eigenvalue（特征值）$1,2$，可以对角化，但归一化后 $V^{T}V$ 的非对角元是 $0.707107$——eigenvector（特征向量）不正交，于是写不出 $Q\Lambda Q^{T}$。再退一步，$A=\begin{bmatrix}0&-1\\1&0\end{bmatrix}$ 的 eigenvalue（特征值）是 $\pm i$，实数域里连对角化都不存在，而它的 SVD 照常给出 singular value（奇异值）$(1,1)$。
> 
> 第五问：任意形状、任意 rank（秩）的矩阵，要压缩、要伪逆、要"最好的 rank one 片"，用 $A=U\Sigma V^{T}$。它两侧都正交，按 singular value（奇异值）降序截断自动最优。用实数说话：那个 $A$ 的 singular value（奇异值）是 $14.606778$、$0.781895$、$0.175117$；只留最大一片重构，$\|A-\sigma_{1}u_{1}v_{1}^{T}\|_{F}=0.801265$，与理论值 $\sqrt{\sigma_{2}^{2}+\sigma_{3}^{2}}=0.801265$ 完全一致。顺带把两条线接上：$\sigma^{2}$ 实测 $213.357975$、$0.611360$、$0.030666$，正是 $A^{T}A$ 的三个 eigenvalue（特征值）。
> 
> 为什么不能只留 SVD 一条？因为它最贵，也最不保留结构：SVD 把列与行两套坐标同时换掉，$LU$ 里"第几列消到哪一行"的记账全部消失，重复解 $Ax=b$ 时反而更慢。分解的取舍从来是"你想保留哪一种结构"，而不是"哪条更万能"。
> 
> 代价也排一次序（$n=1000$）：$LU$ 约 $n^{3}/3=3.33\times10^{8}$，$QR$ 约 $2n^{3}=2\times10^{9}$，对称特征分解与 SVD 都在 $10n^{3}=10^{10}$ 量级。所以工程上的选择顺序是：能给对称就给对称，能一次分解多次求解就绝不每次重解。
> 
> 历史坐标。elimination（消元）作为算法早于矩阵记号：Gauss 在 1809 年的《Theoria motus》里已用今天所谓 elimination（消元）处理最小二乘的正规方程；Doolittle 在 1878 年把它写成可查表的"Coast Survey method"，Werner 在 1883 年用 Crelle 乘法表、对数表和 Thomas 四则计算器三种方式复核过他的表（这条线见 Grcar 关于 ordinary elimination 如何变成 Gaussian elimination 的综述）。SVD 的谱系更长：Beltrami 1873 与 Jordan 1874 在双线性型上得到它，Autonne 1913 推广到复矩阵，Eckart 与 Young 1936 处理矩形矩阵并给出最佳秩逼近，Golub 与 Kahan 1965 才把它变成数值算法（这条年表见 Strang 本人的 SVD 讲义幻灯片）。
> 
> 跨课程：Strang 18.06 把这五条摊在 §2.6（elimination 即 factorization）、§4.3 与 §4.4（最小二乘与 Gram–Schmidt）、§6.4（谱定理）、§7.1 与 §7.2（SVD 与 PCA）四段里；CSAPP 第 6 章的 cache（缓存）层次解释了真实 $LU$ 为什么必须分块——$n^{3}$ 次浮点运算只搬 $n^{2}$ 个数，算术强度极高，分块就是让 $U$ 的更新块留在 cache（缓存）里，这也是 LAPACK 的 dgetrf 存在的理由。下一个该拿下的是 $A=LU$ 里"乘数是免费的"那句话：它把 factorization（分解）从"再算一遍"变成"顺手记下来"，见 §I.4 的注。

---

<span style="color:#2471a3;">**[exercise]**</span> **Problem Set 1.2（习题）**

**1.** 假设 $Ax=0$ 且 $By=0$（其中 $x$、$y$ 和 $0$ 是 vectors（向量））。将这两个 statements（陈述）合并为一个矩阵方程 $AB=C$。矩阵 $B$ 和 $C$ 分别是什么？如果 $A$ 是 $m\times n$，$B$ 和 $C$ 的形状是什么？

**2.** 假设 $a$ 和 $b$ 是列向量，分量分别为 $a_i$ 和 $b_j$。你能做乘法 $ab^T$ 吗（yes 或 no）？$ab^T$ 的形状是什么？行 $i$、列 $j$ 的数是哪个？关于 $aa^T$ 你能说什么？

**3（下标练习）.**
(a) 给出 $AB$ 的 "sum of rank one matrices" formula（公式）。
(b) 给出该 matrix-matrix product（矩阵-矩阵乘积）的 $(i,j)$ entry（元素）的 sigma notation（求和公式）。

**4.** 假设 $B$ 只有一列（$p=1$），所以 $B$ 的每一行只有一个数。写出 $AB$ 的 column times row（列乘行）formula（公式）。用 words（文字）说：$AB$（$m\times1$ 列向量）是 $A$ 的 columns（列）的一个 combination（组合）。

**5（先做行操作，再做列操作；先做列操作，再做行操作）.**
从矩阵 $B$ 开始。想要取它的 rows（行）的组合，我们 pre-multiply（左乘）$A$ 得到 $AB$。想要取它的 columns（列）的组合，我们 post-multiply（右乘）$C$ 得到 $BC$。Associative law（结合律）说明两种方式得到相同结果。

**6.** 如果 $A$ 有列 $a_1,a_2,a_3$ 且 $B=I$ 是 identity matrix（单位矩阵），rank one matrices（秩一矩阵）$a_1b_1^T$、$a_2b_2^T$、$a_3b_3^T$ 分别是什么？它们的和应为 $AI=A$。

**7.** $AB$ 的 columns（列）是 $A$ 的 columns（列）的组合。因此 $AB$ 的 column space（列空间）被包含在 $A$ 的 column space（列空间）中。给出 $A$ 和 $B$ 的一个例子，使得 $AB$ 的 column space（列空间）比 $A$ 的更小。

**8.** 计算 $C=AB$（$m\times n$ 乘 $n\times p$），写出 outer products（外积）算法所需的三个循环的顺序。

---

<span style="color:#7f8c8d">*§I.2 完整翻译。逐句中文写作，英文术语以 English（中文）嵌入。无英文原句。*</span>

---

<span style="color:#2471a3;">**[section]**</span> **I.3 The Four Fundamental Subspaces（四个基本子空间）**

---

本节将解释线性代数的"big picture（大图景）"。

这个大图景展示了每个 $m\times n$ 矩阵如何引出四个 subspaces（子空间）——两个 $\mathbb{R}^m$ 的子空间，还有两个 $\mathbb{R}^n$ 的子空间。

第一个例子将是一个 rank one matrix（秩一矩阵）——其中 column space（列空间）是通过 $u$ 的直线，row space（行空间）是通过 $v^T$ 的直线。

第二个例子是 2×3 矩阵。

第三个例子（一个 5×4 矩阵）将是一个 graph（图）的 incidence matrix（关联矩阵）。

Graphs（图）已经成为离散数学中最重要的模型——这个例子值得理解。

所有四个 subspaces（子空间）在 graph（图）上都有意义。

<span style="color:#2471a3;">**[example]**</span> **Example 1.** $A = \begin{bmatrix}1&3\\2&6\end{bmatrix}$ 有 $m=2$ 和 $n=2$。我们有 $\mathbb{R}^2$ 中的 subspaces（子空间）。

1. Column space $C(A)$（列空间）是通过 $u=\begin{bmatrix}1\\2\end{bmatrix}$ 的直线。Column 2 在这条直线上。
2. Row space $C(A^T)$（行空间）是通过 $v=\begin{bmatrix}1\\3\end{bmatrix}$ 的直线。Row 2 of $A$ 在这条直线上。
3. Nullspace $N(A)$（零空间）是通过 $x=\begin{bmatrix}3\\-1\end{bmatrix}$ 的直线。那么 $Ax=0$。
4. Left nullspace $N(A^T)$（左零空间）是通过 $y=\begin{bmatrix}-3\\1\end{bmatrix}$ 的直线。那么 $A^Ty=0$。

我从它们的 definitions（定义）中收集这四个子空间，如图 I.1 所示：

- Column space $C(A)$（列空间）包含 $A$ 的列的所有 combinations（组合）。
- Row space $C(A^T)$（行空间）包含 $A^T$ 的列的所有 combinations（组合），即 $A$ 的行。
- Nullspace $N(A)$（零空间）包含 $Ax=0$ 的所有 solutions（解）。
- Left nullspace $N(A^T)$（左零空间）包含 $A^Ty=0$ 的所有 solutions（解）。

**图 I.1：** 四个子空间，rank $r=1$。Row space 和 nullspace 在 $\mathbb{R}^2$ 中互相 orthogonal（正交）。Column space 和 left nullspace 也在 $\mathbb{R}^2$ 中互相 orthogonal（正交）。

那个例子有且仅有一个 $u$ 和 $v$ 和 $x$ 和 $y$。所有四个 subspaces（子空间）都是 1-dimensional（一维的）（只是 lines（直线））。

$u$、$v$、$x$、$y$ 总是 independent vectors（独立向量）——它们给出每个子空间的一个 "basis（基）"。

更大的矩阵需要每个子空间有不止一个 basis vector（基向量）。

Basis vectors（基向量）的选择是 scientific computing（科学计算）中的关键步骤。

<span style="color:#2471a3;">**[example]**</span> **Example 2.** $B = \begin{bmatrix}1&-2&-2\\3&-6&-6\end{bmatrix}$ 有 $m=2$ 和 $n=3$。Subspaces（子空间）在 $\mathbb{R}^2$ 和 $\mathbb{R}^3$ 中。

从 $A$ 到 $B$：两个子空间变化，两个子空间不变。

$B$ 的 column space（列空间）仍在 $\mathbb{R}^2$ 中。它有相同的 basis vector（基向量）。

但现在 $B$ 的行中有 $n=3$ 个数字，图 I.2 的左半部分在 $\mathbb{R}^3$ 中。

Row space（行空间）中仍然只有一个 $v$。Rank（秩）仍然是 $r=1$，因为 $B$ 的两行方向相同。

当 $n=3$ 且只有 $r=1$ 个独立方程时，$Bx=0$ 将有 $3-1=2$ 个 independent solutions（独立解）$x_1$ 和 $x_2$。所有解都进入 nullspace（零空间）。

```math
B = \begin{bmatrix}1&-2&-2\\3&-6&-6\end{bmatrix},\quad
Bx=0 \text{ 的解：} x_1 = \begin{bmatrix}2\\1\\0\end{bmatrix},\quad x_2 = \begin{bmatrix}2\\0\\1\end{bmatrix}
```

在我之前的教科书《Introduction to Linear Algebra》中，这些向量被称为 "special solutions（特解）"。

它们来自 elimination（消元法）的步骤——你可以快速验证 $Bx_1=0$ 和 $Bx_2=0$。

但这些不是 nullspace（零空间）中的完美选择，因为 $x_1$ 和 $x_2$ 并不 perpendicular（垂直）。

本书将强烈偏好 perpendicular basis vectors（垂直基向量）。Section II.2 展示了如何从 independent vectors（独立向量）产生 perpendicular vectors（垂直向量）——通过 "Gram-Schmidt" 正交化。

$B$ 的 nullspace（零空间）$N(B)$ 是 $\mathbb{R}^3$ 中的一个 plane（平面）。

我们可以在这个 plane（平面）中看到 orthonormal basis（标准正交基）$q_2$ 和 $q_3$。

$q_2$ 和 $q_3$ 轴互相成 90° 角，并且与 $q_1$ 也成 90° 角。

**图 I.2：** $B = \begin{bmatrix}1&-2&-2\\3&-6&-6\end{bmatrix}$ 的 row space 和 nullspace。Row space：通过 $q_1$ 的无穷直线。Nullspace：$q_2$ 和 $q_3$ 的无穷平面。直线垂直于平面。

<span style="color:#2471a3;">**[example]**</span> **Example 3（一个 graph（图））.**
这里有一个例子，有五个 equations（方程）（对应 graph 中的每条 edge（边））。方程有四个 unknowns（未知数）（对应 graph 中的每个 node（节点））。$Ax=b$ 中的矩阵是 graph（图）的 5×4 incidence matrix（关联矩阵）。

每行有 1 和 -1——表示每条边的结束 node（节点）和开始 node（节点）。

**图：** 4 个 nodes（节点），5 条 edges（边）。Edges 编号 1-5，nodes 编号 1-4。

Incidence matrix（关联矩阵）：

```math
A = \begin{bmatrix}
-1 & 1 & 0 & 0 \\
0 & -1 & 1 & 0 \\
-1 & 0 & 1 & 0 \\
0 & -1 & 0 & 1 \\
0 & 0 & -1 & 1
\end{bmatrix}
```

Edge 1：$-x_1 + x_2 = b_1$，Edge 2：$-x_2 + x_3 = b_2$，等等。

当你理解了这个 incidence matrix（关联矩阵）的四个 fundamental subspaces（基本子空间）——column space、nullspace、以及 $A^T$ 的相应子空间——你就掌握了线性代数的一个 central idea（核心思想）。

**Nullspace $N(A)$：** 设 $b=0$ 求解五个方程。第一个方程说 $x_1=x_2$。第二个说 $x_3=x_4$。第四个说 $x_2=x_4$。所以所有 $x$ 相等：$x=(c,c,c,c)$。这是一个 line（直线）在 $\mathbb{R}^4$ 中。$N(A)$ 的维度为 1。

Rank（秩）$r=3$（因为 $n-\dim N(A) = 4-1=3$）。

从 rank $r=3$，我们可以确定四个子空间的维度：

- Row space（行空间）的维度 = $r = 3$
- Column space（列空间）的维度 = $r = 3$
- Nullspace（零空间）的维度 = $n-r = 1$
- Left nullspace（左零空间）的维度 = $m-r = 2$

**Column space $C(A)$：** 必须有 $r=3$ 个 independent columns（独立列）。最快的方法是看前三列。前三列是独立的。Column 4 是这三列的组合：column 4 = -(column 1 + column 2 + column 3)。

**Row space $C(A^T)$：** 维度必须又是 $r=3$。但 $A$ 的前三行是 dependent（相关的）：row 3 = row 2 - row 1。第一个 $r$ 行是 rows 1,2,4。这些行是 row space（行空间）的一个 basis（基）。Edges 1,2,3 在 graph（图）中形成一个 loop（回路）：dependent rows（相关行）1,2,3。Edges 1,2,4 形成一个 tree（树）：independent rows（独立行）1,2,4。

**Left nullspace $N(A^T)$：** 现在求解 $A^Ty=0$。行的组合给出零。我们注意到 row 3 = row 2 - row 1，所以一个解是 $y=(1,-1,1,0,0)$（沿着 graph 的上 loop：沿 edge 1 和 3 向前，沿 edge 2 向后）。

另一个解来自下 loop：沿 4 向前，沿 5 和 3 向后：$y=(0,0,-1,1,-1)$。

Left nullspace（左零空间）$N(A^T)$ 的维度是 $m-r=5-3=2$。所以这两个 $y$ 是 left nullspace（左零空间）的一个 basis（基）。

方程 $A^Ty=0$ 给出 edge（边）上的 "currents（电流）"：Kirchhoff's Current Law（基尔霍夫电流定律）：流入 = 流出。

Graphs（图）是应用数学中最强大的模型。你在各处都能看到 graphs：道路、管道、血液流动、大脑、Web、一个国家的经济或世界经济。

我们可以理解 incidence matrix（关联矩阵）$A$ 和 $A^T$。

对于一个 connected graph（连通图）有 $m$ 条 edges（边）和 $n$ 个 nodes（节点）：

- $N(A)$：常数向量 $(c,c,c,c)$ 构成一维 nullspace（零空间）。
- $C(A^T)$：tree（树）的 $r=n-1$ 条 edges（边）给出 independent rows（独立行）。
- $C(A)$：Voltage differences（电压差）——其分量在所有 loops（回路）中之和为零。
- $N(A^T)$：Currents（电流）——由 loop currents（回路电流）求解。有 $m-r = m-n+1$ 个 independent loops（独立回路）。

**Big Picture（大图景）：**

- Row space（行空间）$C(A^T)$：$\dim r$
- Nullspace（零空间）$N(A)$：$\dim n-r$
- Column space（列空间）$C(A)$：$\dim r$
- Left nullspace（左零空间）$N(A^T)$：$\dim m-r$

### The Ranks of $AB$ and $A+B$（矩阵乘积与和的秩）

这一页建立了关于 ranks（秩）的关键事实。

当我们 multiply（乘）矩阵时，rank（秩）不能增加。

有一个特殊情况 rank（秩）不能减少。

Statement 4 在 data science 将矩阵 factor（分解）为 $UV$ 或 $CR$ 时很重要。

以下是五个关键 facts（事实）：

<span style="color:#2471a3;">**[theorem]**</span> **Facts about Ranks（秩的事实）**

1. $\text{rank}(AB) \le \text{rank}(A)$，$\text{rank}(AB) \le \text{rank}(B)$
2. $\text{rank}(A+B) \le \text{rank}(A) + \text{rank}(B)$
3. $\text{rank}(A^TA) = \text{rank}(AA^T) = \text{rank}(A) = \text{rank}(A^T)$
4. 如果 $A$ 是 $m\times r$ 且 $B$ 是 $r\times n$（两者 rank 均为 $r$），则 $AB$ 的 rank 也是 $r$
5. Column rank = Row rank（列秩 = 行秩）

Statement 1 涉及 $AB$ 的 column space（列空间）和 row space（行空间）：$C(AB)$ 包含在 $C(A)$ 中。$C((AB)^T)$ 包含在 $C(B^T)$ 中。$AB$ 的每一列是 $A$ 的列的组合。$AB$ 的每一行是 $B$ 的行的组合。

Statement 2：$A+B$ 的每一列是（$A$ 的列）+（$B$ 的列）的和。$\text{rank}(A+B) \le \text{rank}(A) + \text{rank}(B)$ 总是成立。等号不总是成立（例如 $A=B=I$ 时）。

Statement 3：$A^TA$ 和 $A$ 有相同的 nullspace（零空间），所以 $n-r$ 对于两者相同，因此 rank $r$ 也相同。

Statement 4：$A$ 和 $B$ 有 rank $r$。$A^TA$ 和 $BB^T$ 有 rank $r$（由 Statement 3）。它们是 $r\times r$ 矩阵，所以可逆。它们的乘积 $A^TABB^T$ 也可逆。那么 $r = \text{rank}(A^TABB^T) \le \text{rank}(AB)$ 由 Statement 1 给出。同时 $\text{rank}(AB) \le \text{rank}(A) = r$。所以 $AB$ 的 rank 恰好为 $r$。

注意：这并不意味着每个秩为 $r$ 的矩阵的乘积都有 rank $r$。Statement 4 假设 $A$ 恰好有 $r$ 列，$B$ 恰好有 $r$ 行。$BA$ 很容易失败：$A=\begin{bmatrix}1\\1\end{bmatrix}$，$B=\begin{bmatrix}1&-1\end{bmatrix}$ 时 $AB$ 有 rank 1，但 $BA=0$！

<span style="color:#2471a3;">**[exercise]**</span> **Problem Set 1.3（习题）**

**1.** 证明 $A$ 的 nullspace（零空间）包含 $B$ 的 nullspace（零空间）。如果 $Bx=0$ 则 $ABx=0$。

**2.** 找到矩阵 $A$ 使得 $\text{rank}(A^2) < \text{rank}(A)$。验证 $\text{rank}(A^TA) = \text{rank}(A)$。

**3.** 如果 $C = \begin{bmatrix}A\\B\end{bmatrix}$，$C$ 的 nullspace（零空间）与 $A$ 和 $B$ 的 nullspace（零空间）有什么关系？

**4.** 如果 $\text{row space of } A = \text{column space of } A$ 且 $N(A) = N(A^T)$，$A$ 是对称的吗？

**5.** 将 $Ax=b$ 的四种可能性（$r\lt m$、$r=n$ 等）与四个矩阵匹配。（提示：$r\lt m,r=n$ → 对每个 $b$ 有唯一解；$r=m,r\lt n$ → 0 或 $\infty$ 个解等）

**6.** 证明 $A^TA$ 和 $A$ 有相同的 nullspace（零空间）。(a) 若 $Ax=0$ 则 $A^TAx=0$。(b) 若 $A^TAx=0$ 则 $x^TA^TAx = \|Ax\|^2 = 0$，所以 $Ax=0$。因此 $N(A^TA) = N(A)$。

**7.** 找到 $A = \begin{bmatrix}0&1\\0&0\end{bmatrix}$ 的 $C(A)$ 和 $N(A)$。注意 $C(A) = N(A)$。不可能有 $C(A) = N(A^T)$，因为这两个子空间是 orthogonal（正交）的。

**8.** 画一个正方形并连接其顶点到中心点：5 个 nodes（节点）和 8 条 edges（边）。找到 8×5 incidence matrix（关联矩阵），rank $r=4$。找出 $N(A)$ 中的一个向量和 $N(A^T)$ 中的 $8-4=4$ 个 independent vectors（独立向量）。

**9.** 如果 $N(A)$ 是零向量，$B = \begin{bmatrix}A&A\end{bmatrix}$ 的 nullspace（零空间）中有哪些向量？

**10.** 对于 $\mathbb{R}^5$ 中维度为 2 和 7 的子空间 $S$ 和 $T$：(i) $S\cap T$ 可能的维度 (ii) $S+T$ 可能的维度 (iii) $S^\perp$ 的维度。

**11.** 对于 $A$ 和 $B$ 的 nullspace（零空间）和 row space（行空间），$\begin{bmatrix}A\\B\end{bmatrix}$ 的 nullspace（零空间）是 $N(A) \cap N(B)$。

> <span style="color:#1e8449;">**[note] rank(AB) 与 rank(A+B) 的界、以及等号条件：**</span> 这里说的 rank（秩），在人类知识里是"一个线性映射能保留多少维信息"的度量：$A:\mathbb{R}^{n}\to\mathbb{R}^{m}$ 把 $n$ 维的 source（源）压成 $r$ 维的像，$r$ 就是 rank（秩），$n-r$ 是被压掉的 nullity（零化度）。下面两条不等式不是两个孤立事实，而是"复合映射的像不会变大"与"子空间的和不会膨胀"两句话的代数写法。
> 
> 先把 $\operatorname{rank}(AB)\le\min(\operatorname{rank}A,\operatorname{rank}B)$ 证完。第一步是一个 inclusion（包含）：$C(AB)\subseteq C(A)$。理由是 $AB$ 的第 $j$ 列等于 $A$ 乘以 $B$ 的第 $j$ 列，即 $A$ 的 columns（列）的一个 combination（组合），而 $C(A)$ 对组合封闭，故这列落在 $C(A)$ 里。于是在 dimension（维数）上有 $\dim C(AB)\le\dim C(A)$，即 $\operatorname{rank}(AB)\le\operatorname{rank}(A)$。另一半不必重证：对转置用同一句话，$C((AB)^{T})=C(B^{T}A^{T})\subseteq C(B^{T})$，而取转置不改列秩，得 $\operatorname{rank}(AB)\le\operatorname{rank}(B)$。两半合起来就是 min（最小值）。注意这条证明只用到了"像"这一侧，没有用到 $A$ 或 $B$ 的任何数值性质——它是结构性的，所以对任何域上的矩阵都成立。
> 
> 只知道上界会让人误以为乘积可以随便降秩，所以必须补一条下界，即 Sylvester 不等式 $\operatorname{rank}(AB)\ge\operatorname{rank}(A)+\operatorname{rank}(B)-n$。证明走 nullspace（零空间），三步。设 $Z=N(AB)$，先看它与 $N(B)$ 的关系：若 $Bx=0$ 则 $ABx=0$，所以 $N(B)\subseteq Z$。第二步把 $B$ 限制到 $Z$ 上，$B|_{Z}:Z\to\mathbb{R}^{m}$；对 $z\in Z$ 有 $ABz=0$，即 $Bz\in N(A)$，所以 $B|_{Z}$ 的像落在 $N(A)$ 里。第三步对 $B|_{Z}$ 用 rank-nullity（秩-零化度定理）：$\dim Z=\dim\ker(B|_{Z})+\dim\operatorname{Im}(B|_{Z})$，其中 $\ker(B|_{Z})=Z\cap N(B)=N(B)$，第二项不超过 $\dim N(A)=n-r_{A}$。把 $A$ 是 $m\times n$、$B$ 是 $n\times p$ 代进去：
> 
> ```math
> p-r_{AB}=\dim Z=(p-r_{B})+\dim\operatorname{Im}(B|_{Z})\le (p-r_{B})+(n-r_{A})
> ```
> 
> 整理即得 $r_{AB}\ge r_{A}+r_{B}-n$。换成 nullity（零化度）来读更清楚：$\nu(AB)\le\nu(A)+\nu(B)$，即乘积丢掉的维数不超过两边各自丢掉的维数之和。原注写成「两个映射各自丢掉的维数加起来不能超过中间站的大小」，方向与对象都错了：取 $A=0_{3\times5}$、$B=0_{5\times4}$，$\nu(A)=5$、$\nu(B)=4$，和是 $9>n=5$，而 $\nu(AB)=4\le9$ 照样成立。中间站 $n$ 的作用是让下界 $r_A+r_B-n$ 可能为正，不是给 nullity 之和设天花板。
> 
> 再看 $\operatorname{rank}(A+B)\le\operatorname{rank}(A)+\operatorname{rank}(B)$。它也不是新东西：$C(A+B)\subseteq C(A)+C(B)$，因为 $(A+B)x=Ax+Bx$ 是两个列空间元素的和。然后只用一条维数恒等式 $\dim(S+T)=\dim S+\dim T-\dim(S\cap T)\le\dim S+\dim T$。这条恒等式本身也要写清：考虑映射 $S\times T\to S+T$，$(s,t)\mapsto s+t$，它的 kernel（核）恰好是 $\{(v,-v):v\in S\cap T\}$，维数是 $\dim(S\cap T)$，对定义域用 rank-nullity（秩-零化度定理）即得。
> 
> 等号条件才是这两条不等式的用处。$\operatorname{rank}(AB)=\operatorname{rank}(B)$ 当且仅当 $\ker(A)\cap\operatorname{Range}(B)=\{0\}$：因为 $\operatorname{Range}(AB)=A(\operatorname{Range}B)$，对限制映射 $A|_{\operatorname{Range}B}$ 用 rank-nullity（秩-零化度定理）得 $\operatorname{rank}(AB)=\operatorname{rank}(B)-\dim(\ker A\cap\operatorname{Range}B)$。数值上看得见：$A=\begin{bmatrix}1&2&3\\4&5&6\end{bmatrix}$ 满足 $A\nu=0$，其中 $\nu=(1,-2,1)$；取 $B=[\nu,e_{1}]$（其 rank（秩）为 2），乘积的 rank（秩）掉到 1，因为 $\nu$ 躺在 $B$ 的 Range（值域）里；换成 $B=\begin{bmatrix}1&0\\0&1\\1&1\end{bmatrix}$，交集只剩零向量，rank（秩）回到 2。$\operatorname{rank}(A+B)$ 的等号同理：$\operatorname{rank}(A+B)=\operatorname{rank}(A)+\operatorname{rank}(B)$ 当且仅当 $C(A)\cap C(B)=\{0\}$。三个实测：$\operatorname{diag}(1,0)$ 加 $\operatorname{diag}(0,1)$ 得 rank（秩）2，等于 $1+1$，交集维数 0；$I+I$ 得 rank（秩）2，小于 $2+2$，交集是 $\mathbb{R}^{2}$；$I$ 加 $\operatorname{diag}(1,0)$ 得 rank（秩）2，等于 $3-1$，交集维数 1。
> 
> 去掉"同形状"这个条件，$A+B$ 根本不存在——这就是为什么 rank（秩）对乘积有 min（最小值）这种干净的上界，对和只有子空间和的界。原文 Fact 4 用 $A^{T}ABB^{T}$ 可逆推出 $r\le\operatorname{rank}(AB)$，其实是本注那条下界在内维取 $r$ 时的特例：$A$ 是 $m\times r$ 满列秩、$B$ 是 $r\times n$ 满行秩，下界 $r_{A}+r_{B}-r$ 恰好等于 $r$。
> 
> 历史坐标。Sylvester 在十九世纪八十年代造了 nullity（零化度）这个词，把这几条不等式打包成 law of nullity（零化度定律），比喻是两团可以互相渗透的气体；那句话讲的是乘积的 nullity（零化度）不超过两个因子 nullity（零化度）之和——原注写成「nullity 之积」，把对象换成了 $\nu(A)\nu(B)$，那是笔误。后半句「不小于两者中较大者」也对不上对象：$\nu(A)$ 住在 $\mathbb{R}^n$ 而 $\nu(AB)$ 住在 $\mathbb{R}^p$，能比的是 $\nu(AB)\ge\nu(B)$，等价于 $\operatorname{rank}(AB)\le\operatorname{rank}(B)$。原刊卷期页码我核不到：Sylvester 文集第四卷的 archive.org 扫描文本里只见比喻、未见页码，故改引 Horn 与 Johnson 的 *Matrix Analysis* 第 2 版 Thm 0.4.5(c)，它给的正是 $\operatorname{rank}(AB)\ge\operatorname{rank}(A)+\operatorname{rank}(B)-n$；这个定理号同样是通行引用，未能一手核实。这条不等式的真正价值要等到二十世纪才显现：它把"乘积的秩"从不可控变成双侧夹逼——上界说不会变大，下界说不会无故变小。
> 
> 跨课程：这条定理在 Strang 18.06 的 §3.5（rank 与四个子空间）里是主线推论；在 6.042J 里对应一句更朴素的话——函数复合的像集只会变小，$\operatorname{Im}(f\circ g)\subseteq\operatorname{Im}(f)$，这里的 $\operatorname{rank}(AB)\le\operatorname{rank}(A)$ 就是它在 vector space（向量空间）上的同构版；Thomson 实分析里同一件事以第一同构定理出现，$\dim V=\dim\ker T+\dim\operatorname{Im}T$ 正是本注反复用的 rank-nullity（秩-零化度定理）。CLRS 6.006 里没有直接对应，最接近的是矩阵链乘法的动态规划，那里用到的是同一套"维数决定代价"的记账法。下一个该拿下的是 $\operatorname{rank}(A^{T}A)=\operatorname{rank}(A)$，因为最小二乘、正规方程、PCA 的协方差矩阵都从它出发。

---
> <span style="color:#1e8449;">**[note] Note（译者注：五张分解是一张用正交性换适用范围的价目表）:**</span> 这五种 factorizations 不是五个彼此无关的小技巧，而是同一句 $A=\sum_k u_kv_k^T$（写成外积和）在不同程度上强制「两侧的向量正交」所得到的五个出口。价目表只有一列：在哪一侧让步，换回什么。
> - $A=CR$：**零正交**。$C$ 就是 $A$ 的 pivot columns（主元列）原样搬过去，$R$ 是 rref（简化行阶梯形）的非零行，两者都不正交。它换回的不是数值精度，而是 rank 的证书：取一个 $4\times3$、rank $r=2$ 的矩阵实测，$C$ 是 $4\times2$、$R$ 是 $2\times3$，一共 $14$ 个数，比 $A$ 自己的 $12$ 个数还多 —— 所以 $CR$ 从来不是 compression（压缩存储），它证明的是「这 $12$ 个数只由 $2$ 条独立信息生成」。§I.1 的 Column Rank = Row Rank 正是用 $C$ 的列独立加 $R$ 的行独立拼出来的。那个例子等会儿还要用：四行是 $(1,0,-6)$、$(1,1,-3)$、$(0,1,3)$、$(2,1,-9)$，rref 的非零行是 $(1,0,-6)$ 与 $(0,1,3)$，第三列确实是前两列的坐标 $-6$ 与 $3$ 的组合。看清楚了：$R$ 存的是坐标而不是数据，所以它压不动体积，$14$ 比 $12$ 多出来的那两个数就是坐标的代价。
> - $A=LU$：**无正交**，只要 $L$ 是 unit lower triangular（单位下三角）。代价是所有 leading principal minors（顺序主子式）非零，否则必须先乘一个 $P$（见下一节 note）。
> - $A=QR$：**一侧正交**。$Q^TQ=I$ 的代价是 $R$ 的对角元等于 Gram-Schmidt 每一步 residual（残差）的 norm（范数）——秩满的 $4\times3$ 例子实测为 $\sqrt3$、$\sqrt{15}/3$、$\sqrt{35}/5$，即 $1.7321$、$1.2910$、$1.1832$；$A$ 的列越接近 linear dependence（线性相关），这些数越小，除以它们的放大就越凶。这个例子取列 $(1,1,1,0)$、$(0,1,1,1)$、$(1,1,0,-2)$，三个 residual 的平方分别是 $3$、$5/3$、$7/5$，开方后正是那三个数；而 $A$ 的 condition number（条件数）只有 $5.79$，说明正交化把这些列的耦合压进了三个分母，$Q$ 本身与列的强弱无关。
> - $S=Q\Lambda Q^T$：**两侧同时正交**，所以 $Q^{-1}=Q^T$，根本不用求逆。代价是必须 $S=S^T$。
> - $A=X\Lambda X^{-1}$：条件最弱，只要 $n$ 个 independent eigenvectors（独立特征向量）；代价是 $X^{-1}$ 要真算，而 $X$ 在特征值接近时可以极度 ill-conditioned（病态）。$3\times3$ 的 Jordan 块（对角线上三个 $3$、上对角线上两个 $1$、其余为 $0$）满足 $\operatorname{rank}(J-3I)=2$，几何重数 $1$ 小于代数重数 $3$，这条分解对它**不存在**（实测 sympy 抛 MatrixError）。
> - SVD $A=U\Sigma V^T$ 是唯一对任意矩阵两侧都正交的一条，代价是要同时求 $A^TA$ 与 $AA^T$ 的 eigenpairs（特征对），工作量翻倍。
> 
> 这张价目表的形状很有信息量：**正交性越强，适用面越窄**。而「片数」是同一把尺子：上面那个 rank $2$ 的矩阵，$CR$ 要 $2$ 片才精确，SVD 用 $2$ 片重构误差 $4.5\times10^{-15}$，只用最大的 $1$ 片误差就到 $1.7131$，正好等于被丢掉的 $\sigma_2$。于是 §I.9 的 best low rank approximation（最佳低秩逼近，PCA 的内核）不过在「$CR$ 挑哪两列」和「SVD 挑哪两片」之间选了后者 —— 因为后者按 $\sigma$ 降序排列，截断自动最优。这一步有确切的一手出处：Eckart 与 Young 1936 年发表在 Psychometrika 第 1 卷第 3 期 $211$ 至 $218$ 页的论文证明，在 Frobenius norm（弗罗贝尼乌斯范数）下最优的 rank $k$ 逼近就是截断 SVD，误差平方精确等于被丢掉的 $\sigma^2$ 之和 —— 所以 $1$ 片的误差是 $\sigma_2$ 本身，不是「约等于」。要说明的是，原注记的 $5.3\times10^{-15}$ 与 $0.2332$ 出自一个未留存的矩阵，此处换成上面可复算的同一构造，结论与数量级不变。
> 
> 存储账要单独记，否则容易把 SVD 当成更省的写法：rank $2$ 用 SVD 写下来是 $2\times(4+3)+2=16$ 个数，比 $CR$ 的 $14$ 还多出两个，它是多存两个数去换「随时可以再截一片」的资格。这也是 §I.9 在数据里选 SVD 的隐含前提：省的不是存储，是排序。
> 
> 往后翻，这五条各自有落点：$QR$ 在 §I.5 展开成 orthogonalization（正交化）与 projection（投影），SVD 在 §I.8，PCA 在 §I.9；§IV.8 Completing Rank One Matrices 直接用 $uv^T$ 填补缺失项；§V.4 的 covariance matrix（协方差矩阵）就是「rank one 片之和」的概率版；§VII.1 度量深度网络的表达力时数的 flat pieces（平坦片）个数，仍是复合线性映射能折出多少张平面 —— 根子还是这里的外积。
> 
> 跨课程看同一件事会更清楚：MIT 18.06 的路线是先把 rank 定义成 pivot 的个数，再用 $C$ 的列独立与 $R$ 的行独立去证明 column rank 等于 row rank，于是 $A=CR$ 在那门课里是 rank-nullity（秩-零化度）的证明工具；本课（18.065）从数据出发，入口直接是 SVD，把同一句式子读成特征提取。同一条分解在两门课里的身份不同，这正是「价目表」要解决的问题：先知道要付什么代价，再挑出口。

<span style="color:#7f8c8d">*§I.3 逐句翻译完成。逐句对照OCR原文，无概括无遗漏。覆盖：四个子空间定义（Example 1）、Example 2（不同尺寸矩阵）、Incidence Matrix（图论解释、KVL/KCL）、Big Picture、秩的五条事实及证明、Problem Set 1.3（11道习题）。*</span>

---

<span style="color:#2471a3;">**[section]**</span> **I.4 Elimination and $A=LU$（消元与 $A=LU$ 分解）**

---

### Row Picture and Column Picture（行图像与列图像）

线性代数中最古老、最基础的问题是求解 $Ax=b$。

我们得到 $n\times n$ 矩阵 $A$ 和 $n\times1$ 列向量 $b$。我们寻找解向量 $x$。

其分量 $x_1,\dots,x_n$ 是未知数，我们有 $n$ 个方程。

通常一个方阵意味着 $Ax=b$ 只有一个解（但并非总是如此）。

我们可以通过 geometry（几何）或 algebra（代数）找到它。

本节从 $Ax=b$ 的 row picture（行图像）和 column picture（列图像）开始。

然后我们通过简化方程来求解——从 $n-1$ 个方程中消去 $x_1$，得到大小为 $n-1$ 的更小系统。

最终我们到达 $1\times1$ 系统 $a_{nn}x_n = b_n$，于是我们得到 $b_n/a_{nn}$。

反向代入产生 $x_{n-1}$，最终我们得到 $x_2$ 和 $x_1$。

本节的重点是以 rank one matrices（秩一矩阵）的视角来看待消元步骤。

每一步（从 $A$ 到 $A_2$ 最终到 $U$）移除一个 rank one matrix（秩一矩阵）。

那么原来的 $A$ 就是那些 rank one matrices（秩一矩阵）的和。

这个和正是伟大的 factorization（分解）$A=LU$——下三角矩阵 $L$ 乘以上三角矩阵 $U$。

$A=LU$ 是没有行交换的消元法的矩阵描述。

那是 algebra（代数）。让我们从一个 2×2 例子的 geometry（几何）开始。

<span style="color:#2471a3;">**[example]**</span> **2×2 例子：**

```math
\begin{cases}
2x_1 + 3x_2 = 9 \\
x_1 - 2x_2 = 1
\end{cases}
```

矩阵形式：$A = \begin{bmatrix}2&3\\1&-2\end{bmatrix}$，$b = \begin{bmatrix}9\\1\end{bmatrix}$。

**Row picture（行图像）：** 两个方程对应两条直线。它们在解 $x_1=3,x_2=1$ 处相交。第一个方程：$2x_1+3x_2=9$。第二个方程：$x_1-2x_2=1$。我从方程1中减去了2倍方程1，得到 $7x_2=7$。这消去了 $x_1$。未知数 $x_1$ 已从方程2中被消去。这就是 algebra（代数）：

消元后的系统：$2x_1+3x_2=9$，$7x_2=7$。

**Column picture（列图像）：** $Ax$ 是列的组合。$A$ 的列向量是 $a_1=(2,1)$ 和 $a_2=(3,-2)$。方程 $Ax=b$ 要求找到列的组合以匹配 $b$。正确的组合（解）具有与行图像中相同 $x_1=3$ 和 $x_2=1$：

```math
Ax = \begin{bmatrix}2\\1\end{bmatrix}x_1 + \begin{bmatrix}3\\-2\end{bmatrix}x_2 = \begin{bmatrix}9\\1\end{bmatrix}
```

将 3 倍 column 1 加到 1 倍 column 2 上，得到 $b$ 作为列的组合。

**图 I.5：** Column picture：3 倍 (column 1) + 1 倍 (column 2) 给出 $b$。

对于 $n=2$，row picture（行图像）看起来很容易。但对于 $n=3$，column picture（列图像）胜出。画三个列向量比画三个平面更好！

**Row picture in 3D（三维行图像）：** 三个平面交于一点。每个方程对应一个平面。

**Column picture in 3D（三维列图像）：** 三个列向量组合起来给出向量 $b$。

### Solving $Ax=b$ by Elimination（消元法求解 $Ax=b$）

在 $\mathbb{R}^3$ 中可视化三个平面相交并不容易。在 $\mathbb{R}^n$ 中，"hyperplanes（超平面）" 在一点相交更是 mind-bending（令人费解）。

列向量的组合更简单：矩阵必须有 $n$ 个 independent columns（独立列）。这些列都必须位于同一 $\mathbb{R}^n$ 中（或位于 $\mathbb{R}^n$ 中的同一 hyperplane（超平面）中）是不可能的。这转化为一个代数陈述：

**Independent columns（独立列）：** $Ax=0$ 的唯一解是零向量 $x=0$。

换句话说，independence（独立性）意味着加到零向量的唯一组合是每个列乘以零。

那么 $Ax=0$ 的唯一解是 $x=0$。当这是真的时，elimination（消元法）将求解 $Ax=b$，找到产生 $b$ 的唯一列组合。

### How Elimination Works（消元法的工作原理）

以下是整个思路，逐列进行，当消元法按通常顺序成功时：

- **Column 1（第1列）：** 使用方程1在第1列下方创建 zeros（零）。
- **Column 2（第2列）：** 使用新方程2在第2列下方创建 zeros（零）。
- **Columns 3 to $n$：** 继续到最后一列，得到 $U$：上三角。

**Step 1：** Row 1 是第一个 pivot row（主元行）——它不变。我将该行乘以数字 $l_{21},l_{31},l_{41}$ 并从 $A$ 的行2,3,4中减去。

**Step 2：** 使用新的 row 2（第二个 pivot row）。将该行乘以 $l_{32},l_{42}$ 并从行3,4中减去。

继续直到 $U$。

到目前为止，我们处理的是矩阵 $A$（而不是 $b$）。对 $A$ 进行消元需要 $\frac{1}{3}n^3$ 次乘法和加法——远多于对每个右端项 $b$ 所需的 $n^2$ 步。

我们需要记录那些工作，完美的格式是矩阵的乘积 $A=LU$：lower triangular（下三角）乘以上 triangular（上三角）$U$。

### The Factorization $A=LU$（$A=LU$ 分解）

原来的 $A$ 与最终的矩阵 $U$ 有何关系？乘数 $l_{ij}$ 在三个步骤中到达那里。第一步将 4×4 问题简化为 3×3 问题，移除了 "row 1 的倍数"：

**关键思想：** Step 1 移除了 $l_1$（row 1），其中 $l_1 = (1,l_{21},l_{31},l_{41})$。

```math
A = l_1(\text{row 1}) + A_2
```

我们做了什么？右侧的第一个矩阵是从 $A$ 中移除的。那个移除的矩阵是列向量 $l_1$ 乘以 row 1。它是一个 rank one matrix（秩一矩阵）$l_1$（row 1）。

**3×3 例子：**

```math
A = \begin{bmatrix}1&2&3\\2&5&7\\3&7&8\end{bmatrix},\quad 
\text{Step 1: } A = \begin{bmatrix}1\\2\\3\end{bmatrix}\begin{bmatrix}1&2&3\end{bmatrix} + A_2,\quad
A_2 = \begin{bmatrix}0&0&0\\0&1&1\\0&1&-1\end{bmatrix}
```

下一步处理剩余矩阵 $A_2$ 的第2列。新的 row 2 是 $(0,1,1)$，$l_{32}=1$ 是第二个 pivot row 的乘数。

**Step 2：** 移除了 $l_2 = (0,1,1,l_{42})$ 乘以 pivot row 2。

第三步将 2×2 矩阵 $A_3$ 简化为单个数字（1×1）。

这种逐列观察消元法的方式直接产生了 $A=LU$。

矩阵乘法 $LU$ 始终是 $L$ 的列乘以 $U$ 的行的和：

```math
A = \begin{bmatrix}1\\l_{21}\\l_{31}\\l_{41}\end{bmatrix}\text{(pivot row 1)} + 
\begin{bmatrix}0\\1\\l_{32}\\l_{42}\end{bmatrix}\text{(pivot row 2)} + \cdots = LU
```

消元法将 $A$ 分解为下三角 $L$ 乘以上三角 $U$。

**关于 $LU$ 分解的注记：** 我们从消元法的关键思想出发推导出 $A=LU$：通过从最后 $n-1$ 个方程中消去 $x_1$，将问题大小从 $n$ 减少到 $n-1$。我们减去了 row 1（pivot row）的倍数。所以我们移除的矩阵的 rank 为 1。经过 $n$ 步后，整个矩阵是 rank one matrices（秩一矩阵）的和。这个和——通过列乘行的矩阵乘法规则——就是 $L$ 乘以 $U$。

这个证明与我的教科书《Introduction to Linear Algebra》中的不同。那里的思路是考察 $U$ 的行而不是 $A$ 的列。Row 3 of $U$ 等于 row 3 of $A$ 减去 pivot rows 1 和 2 的倍数：

```math
\text{Row 3 of }U = (\text{row 3 of }A) - l_{31}(\text{row 1 of }U) - l_{32}(\text{row 2 of }U)
```

重写此方程可以看出 $[l_{31},l_{32},1]$ 正在乘以矩阵 $U$：

```math
\text{Row 3 of }A = l_{31}(\text{row 1 of }U) + l_{32}(\text{row 2 of }U) + 1(\text{row 3 of }U)
```

所以 row 3 of $A$ = row 3 of $LU$。关键在于被减去的行是 pivot rows（主元行），已经在 $U$ 中。在没有行交换的情况下，我们再次得到 $A=LU$。

> <span style="color:#1e8449;">**[note] $A=LU$ 里的 $L$ 为什么是免费的：**</span> 这一节真正的定理只有一句：elimination（消元）的每一步都是左乘一个 unit lower triangular（单位下三角）矩阵 $E_k=I-\ell_ke_k^T$ 本身，而它的逆 $E_k^{-1}=I+\ell_ke_k^T$ 只把非对角元的符号翻过来 —— 于是乘数在消元过程中被算过一次，之后只是摆放，不是重算。这句话解释了为什么 $A=LU$ 比「已知 $A$ 与 $U$ 反推 $L$」便宜整整一个数量级。
> 
> 把每步写成矩阵。第 $k$ 步做的是「第 $i$ 行减去 $l_{ik}$ 倍的第 $k$ 行」，对应的初等矩阵是 $E_{k}=I-\ell_{k}e_{k}^{T}$，其中 $\ell_{k}$ 的前 $k$ 个分量是 $0$（第 $k$ 步不碰前 $k$ 行）。这里有个容易漏的细节：$e_{k}^{T}\ell_{k}=0$，于是
> 
> ```math
> (I-\ell e^{T})(I+\ell e^{T})=I-\ell e^{T}\ell e^{T}=I-\ell(e^{T}\ell)e^{T}=I
> ```
> 
> 即 $E_{k}^{-1}=I+\ell_{k}e_{k}^{T}$ —— 逆矩阵确实只是符号翻转，一次乘法都不用。例如下文那个例子里 $\ell_{1}=(0,3,2)$（即 $l_{21}=3$、$l_{31}=2$），于是 $E_{1}^{-1}$ 就是 $\begin{bmatrix}1&0&0\\3&1&0\\2&0&1\end{bmatrix}$（实测 $E_1E_1^{-1}-I$ 的最大元为 $0$）。
> 
> 消元跑完得到 $U=E_{n-1}\cdots E_{1}A$，所以 $A=E_{1}^{-1}E_{2}^{-1}\cdots E_{n-1}^{-1}U$，$L$ 就定义为这串逆的乘积。关键在乘的顺序：先做的 $E_{1}^{-1}$ 在最左边。两个因子相乘会出现交叉项 $\ell_{1}(e_{1}^{T}\ell_{2})e_{2}^{T}$，而 $e_{1}^{T}\ell_{2}=0$，因为 $\ell_{2}$ 的第一个分量是 $0$（第 2 步不动第 1 行）。把 $n$ 步拼起来，只要 $i<j$ 就有 $e_{i}^{T}\ell_{j}=0$，全部交叉项消失，$L=I+\sum_{k}\ell_{k}e_{k}^{T}$。这个矩阵的第 $k$ 列**正是** $\ell_{k}$：实测三列是 $(1,3,2)^{T}$、$(0,1,-3)^{T}$、$(0,0,1)^{T}$，与消元时记下的乘数 $3,2,-3$ 逐个对得上。所以 $L$ 的存储是免费的：$n(n-1)/2$ 个乘数，消元时顺手写下来即可。
> 
> 为什么必须把对角固定成 $1$？因为不然 $LU$ 不唯一：任意对角阵 $D$ 给出 $A=(LD)(D^{-1}U)$，$L$ 可以偷走一部分对角。固定 $\operatorname{diag}L=1$ 之后唯一，而且账正好平：$L$ 只管 $n(n-1)/2$ 个乘数，对角上那 $n$ 个 $1$ 是约定、不占存储；$U$ 存 $n(n+1)/2$ 个，两笔合计 $n^{2}$，与 $A$ 一样多。用小整数例子核对：$\operatorname{nnz}(A)=9$，$L$ 里只需存 $3$ 个乘数，$U$ 存 $6$ 个，$3+6=9$ 刚好相等 —— 把对角那 $3$ 个 $1$ 也数进去才会得到 $6+6=12$，而它们本来不必存。
> 
> 完整的数值例子：$A=\begin{bmatrix}1&2&3\\3&5&7\\2&7&9\end{bmatrix}$，$l_{21}=3$、$l_{31}=2$，消元后第二行变成 $(0,-1,-2)$，$l_{32}=-3$，最终 $U=\begin{bmatrix}1&2&3\\0&-1&-2\\0&0&-3\end{bmatrix}$、$L=\begin{bmatrix}1&0&0\\3&1&0\\2&-3&1\end{bmatrix}$，实测 $\max|LU-A|=0$，$U$ 的对角是 $1,-1,-3$，其乘积就是 $\det A=3$（逐块归因见本节「行交换」那段的 note，这里不再重述）。
> 
> 非例子：$A=\begin{bmatrix}0&2\\3&4\end{bmatrix}$ 的第一列主元是 $0$，$l_{21}=3/0$ 无定义，$A=LU$ 不存在；换行后取 $P=\begin{bmatrix}0&1\\1&0\end{bmatrix}$，$PA=\begin{bmatrix}3&4\\0&2\end{bmatrix}$ 可以直接分解。所以严格的定理是 $PA=LU$，而 $A=LU$ 只是不用换行时的简写。
> 
> 换行还有第二个、更要紧的理由：稳定性。取 $A=\begin{bmatrix}\epsilon&1\\1&1\end{bmatrix}$，$b=(1,2)^{T}$，精确解是 $(1/(1-\epsilon),\,(1-2\epsilon)/(1-\epsilon))$。不换行时乘数 $l_{21}=1/\epsilon$，$u_{22}$ 与 $b_{2}^{\prime}$ 都变成某个大数里减去 $1$ 或 $2$，小量在 $10^{8}$ 面前被吞掉。float32 的 $\epsilon_{\mathrm{mach}}=1.19\times10^{-7}$，$\epsilon=10^{-8}$ 时实测解给 $(0,1)$，第一个分量误差就是 $1$；float64 要 $\epsilon$ 小得多才塌：$10^{-8}$ 时第一个分量的绝对误差 $4.975\times10^{-9}$，$10^{-10}$ 时 $8.264\times10^{-8}$，$10^{-12}$ 时 $2.212\times10^{-5}$，$10^{-14}$ 时 $7.993\times10^{-4}$，到 $10^{-16}$ 才崩成 $1.220$。理论口径是误差上界约 $\epsilon_{\mathrm{mach}}\cdot10^{8}=2.22\times10^{-8}$，实测 $10^{-8}$ 那档只有 $4.975\times10^{-9}$，上界没被顶到。partial pivoting（部分选主元）每步选绝对值最大的主元，实测 float32 与 float64 都精确到机器精度。这就是为什么所有实用代码默认带 partial pivoting。
> 
> growth factor（增长因子）是量化的说法：$\max|u_{ij}|/\max|a_{ij}|$。Wilkinson 的 $\pm1$ 矩阵（对角为 $1$、下方全 $-1$、最后一列全 $1$）在 partial pivoting（部分选主元）下，$n=6$ 实测增长因子恰为 $32=2^{5}$，$U$ 的最后一列是 $1,2,4,8,16,32$；一般 $n$ 时上界是 $2^{n-1}$，且这是最坏情形。
> 
> 历史坐标。Gauss 在 1809 年的《Theoria motus》里已经用今天的 elimination（消元）解正规方程；Doolittle 在 1878 年把它写成可查表的 Coast Survey method，Werner 在 1883 年用三种方式复核过他的表；把 schoolbook elimination 解释成矩阵分解发生在 1947 年，von Neumann 与 Goldstine 用它分析电子计算机的舍入误差，这一条线的史料见 Grcar, *Notices AMS* 58(6):782--792 (2011)。Wilkinson 在 *Rounding Errors in Algebraic Processes*（Prentice-Hall, 1961）里系统化了 $PA=LU$ 与增长因子的分析，$2^{n-1}$ 这个上界出自这条线。
> 
> 跨课程：Strang 18.06 的 §2.6 标题就是 elimination 即 factorization，§2.5 讲逆矩阵时已埋下 $E_{k}^{-1}$ 的伏笔；CSAPP 第 2 章的 IEEE 754 浮点给出了本注所有 $\epsilon_{\mathrm{mach}}$ 的来源，即 float32 的 23 位尾数与 float64 的 52 位尾数，第 6 章的 cache（缓存）层次也解释了分块 $LU$ 为什么能让数据留在 cache 里。CLRS 第 4 章讲 Strassen 对矩阵乘法复杂度的改写，MIT 6.006 没有直接对应的分解内容。下一个该拿下的是 Cholesky（$A=LL^{T}$）：$A$ 对称正定时不必换行、乘数减半、存储减半，它是 $A=LU$ 在对称性上的红利，见 §I.7 末尾（本文件 1320 行）。

### Solving $Ax=b$（求解 $Ax=b$）

我们必须对方程右端项应用与左端相同的操作。

直接的方法是将 $b$ 作为额外的一列——我们处理增广矩阵 $[A\;b]$。

现在我们在 $A$ 上的消元步骤（它们通过 $L^{-1}$ 相乘得到 $U$）同样作用于 $b$。

从 $A$ 到 $U$（上三角）的步骤将右端项 $b$ 改为 $c$。对 $Ax=b$ 进行消元产生方程 $Ux=c$，准备好进行 back substitution（回代）。

<span style="color:#2471a3;">**[example]**</span> **2×2 回代：**

消元后的系统：$2x_1+3x_2=8$，$1x_2=2$。

从底部向上求解——回代——从下到上：$x_2=2$，然后 $2x_1+6=8$ 给出 $x_1=1$。

仔细观察，方阵系统 $Ax=b$ 变成了两个 triangular systems（三角系统）：$Ax=b$ 分解为 $Lc=b$ 和 $Ux=c$。消元得到 $c$，回代得到 $x$。

最终结果是 $x = U^{-1}c = U^{-1}L^{-1}b = A^{-1}b$。正确的解已找到。

请注意这些步骤要求非零 pivots（主元）。我们用那些 $n$ 个 pivots 做除法。

第一个 pivot 是 $a_{11}$。第二个 pivot 是 $A_2$ 的角落。第三个 pivot 在 1×1 矩阵 $A_3$ 中。这些数字最终位于 $U$ 的主对角线上。

### Row Exchanges (Permutations)（行交换 / 置换）
> <span style="color:#1e8449;">**[note] Note（译者注：pivot 为什么既是行列式的因子、又是主子式的比值）:**</span> 式子 $\det A=\prod u_{kk}$ 不是就此背下来的一条行列式性质，而是消元只用了两种对 $\det$ 极友好的行运算的结果：行 $i$ 减去 $l$ 倍行 $k$ 是 $\det=1$ 的变换，行交换是 $\det=\pm1$ 的变换。于是除了 $L$ 的单位对角与 $P$ 的符号，整个 $\det$ 只能落在 $U$ 的对角线上。书中例子实测：$L$ 的三行取 $(1,0,0)$、$(2,1,0)$、$(3,1,1)$，$U$ 的三行取 $(1,2,3)$、$(0,1,1)$、$(0,0,-2)$，乘出来 $A$ 的三行是 $(1,2,3)$、$(2,5,7)$、$(3,7,8)$；对角元 $1,1,-2$ 的乘积 $-2$ 正是 $\det A$，sympy 有理数精确算出同一个 $-2$。
> 
> 更强的一句是逐个成立：$u_{kk}=\det A_k/\det A_{k-1}$，其中 $A_k$ 是左上 $k\times k$ 子矩阵。同一例子实测 $1/1$、$1/1$、$-2/1$ 与 $U$ 的对角元一一对上，三个主子式分别是 $1$、$1$、$-2$。机制在于消元是**按列从左到右**推进的：处理前 $k$ 列只动前 $k$ 行，所以 $A_k$ 的分解恰好就是 $L$、$U$ 的左上 $k\times k$ 块，于是 $\det A_k=\prod_{j\le k}u_{jj}$，相邻两式相除就把前面的因子约掉。这条式子顺手交出了 $A=LU$（无行交换）的存在判据：所有 $A_k$ 非奇异。反例是两行 $(0,1)$、$(1,1)$ 的矩阵 $B$，它的 $\det=-1$ 明明可逆，但 $\det A_1=0$，乘数 $l_{21}=a_{21}/a_{11}=1/0$ 无定义 —— 这就是 §I.4 习题 10 的答案，也标出了「只要 $\det A\neq0$ 就有 $LU$」这句话错在哪：缺的不是可逆性，是**顺序**主子式的非零。反过来也成立得干脆：若某个 $A_k$ 奇异，那 $k$ 行必然线性相关，整张 $A$ 也就退化，于是该步 pivot 恰为 $0$ —— 消元第一次撞上零 pivot 的位置，就是 $A$ 丢 rank 的位置。
> 
> 有行交换时结论改成符号版：实测 $D$ 的三行 $(0,0,2)$、$(1,2,3)$、$(2,1,1)$ 配上交换第 $1$、$3$ 行的 $P$，得 $\prod u_{kk}=2\cdot\tfrac32\cdot2=6$，而 $\det P=-1$、$\det A=-6$，正确的写法是 $\det A=\det P\prod u_{kk}$。而 $L$ 里「乘数原样落座」也带着顺序前提：实测 $E_{32}E_{31}E_{21}A=U$，所以 $L=(E_{32}E_{31}E_{21})^{-1}=E_{21}^{-1}E_{31}^{-1}E_{32}^{-1}$；若误按 $E_{21}E_{31}E_{32}$ 求逆，$L$ 的 $(3,1)$ 元会变成 $5$ 而不是 $3$。为什么必须这么排：第 $k$ 步的 $E$ 只碰第 $k$ 列以下的条目，后面步子的乘数落座时不会再被更早的 $E$ 拉动，所以按发生顺序相乘、取逆时反向书写，两件事缺一条 $A=LU$ 就一次成型不了。
> 
> 成本账也要记：实测 $n=32$ 时 LU 需要 $21328$ 次乘加除（$0.6509n^3$，极限 $\tfrac23n^3$），Cholesky 在同一口径（乘、加、除各记一次，开方不计）下只要 $11408$（$0.3481n^3$，极限 $\tfrac13n^3$），比值 $1.87$。原注记的 Cholesky 数 $11968$ 不是错，而是更宽的口径：把 $32$ 次开方各记两次（$+64$）、再补上列缩放时那 $n(n-1)/2=496$ 次减法，恰好 $11408+560=11968$，比值随之变成 $1.78$。两套口径讲的是同一件事：一次 $n^3$ 量级的固定投入，换来每个新右端项 $b$ 只花 $n^2$ 的回代 —— 所以解多个 $b$ 时从不重复消元。顺带一个常被忽略的推论：$|\det A|$ 是 $A$ 的列张成的平行体体积，$U$ 的对角元正是消元每一步的伸缩倍率，体积逐段累积成 $\prod u_{kk}$，符号记在 $P$ 头上。更狠的量级对照：用 Leibniz 公式展开 $20\times20$ 的 $\det$ 要 $20!=2.43\times10^{18}$ 项，消元只要约 $5333$ 次，差 $4.6\times10^{14}$ 倍。
> 
> 跨章：pivot 的**符号**在 §I.7 就是 positive definite（正定）的 Sylvester 判据，这条判据的一手出处是 Sylvester 1852 年载于 Philosophical Magazine 第 $4$ 系列第 $4$ 卷 $138$ 至 $142$ 页的惯性律论文，本书随即用它证明正定 $\Rightarrow$ Cholesky 存在；§VI.2 对 KKT 矩阵 $M$ 做块消元（$M$ 由四块拼成：左上 $S$、右上 $A$、左下 $A^T$、右下 $0$），右下的 Schur complement $-A^TS^{-1}A$ 会算出 $n$ 个正 pivot 与 $m$ 个负 pivot，这组正负号正是 Lagrangian 有 saddle point（鞍点）的代数印记；§VI.4 讨论 gradient descent 的 zig-zag（之字形）收敛速率时，控制它的条件数 $\lambda_1/\lambda_n$ 也不过是 pivot 极端比值换了个名字。跨课程再补一条：MIT 18.06 把消元讲成 $A=LU$、把 $\det$ 讲成体积的放大率，于是 $\prod u_{kk}$ 就是各行伸缩倍率之积；同一句话搬到本课 §I.4，变成「乘数按什么顺序落座」。

当 $a_{11}=0$ 时怎么办？Zero（零）不能是第一个 pivot。如果第1列下方某处有非零数字，它的行可以是 pivot row（主元行）。好的代码会选择最大的数字作为 pivot——即使 $a_{11}$ 不是零也会这样做，以减少误差。

接下来我们看看那些行交换对 $A=LU$ 的影响。一个矩阵 $P$ 将会介入。

<span style="color:#2471a3;">**[example]**</span> 第1列中最大的数字在 row 3：$a_{31}=?$。Row 3 成为第一个 pivot row。该行被乘以 $l_{21}$ 并从 row 2 中减去。

最终的矩阵 $U$ 是上三角，但 $L$ 矩阵不是。此时的 pivot order（主元顺序）是 3,1,2。如果我们希望 pivot rows 是 1,2,3，我们必须将 $A$ 的 row 3 移到顶部：

```math
PA = \begin{bmatrix}0&0&1\\1&0&0\\0&1&0\end{bmatrix}A
```

当 $Ax=b$ 的两边都乘以 $P$ 时，顺序恢复，且 $PA=LU$。

每个 $m\times n$ 矩阵 $A$ 都能得到 $PA=LU$：$P$ 是 permutation matrix（置换矩阵）。

有六个 3×3 置换矩阵：对单位矩阵的行排序的六种方式。

每个 permutation matrix（置换矩阵）$P$ 的逆就是其转置 $P^T$。行交换同样应用于 $Ax=b$ 的右端项 $b$。计算机仅仅记住交换而不实际移动行。

大小为 $n$ 的 permutation matrices（置换矩阵）有 $n!$（阶乘）个。

当 $A$ 有 dependent rows（相关行）（无逆矩阵）时，消元法会导致零行并提前停止。

<span style="color:#2471a3;">**[exercise]**</span> **Problem Set 1.4（习题）**

**1.** 将这些矩阵分解为 $A=LU$。

**2.** 如果 $a_{11}$ 是 rank one matrix（秩一矩阵）的第一行，$a_{21},\dots,a_{m1}$ 是第一列，$a_{mn}$ 是 $a_{ij}$ 的公式。当你的公式何时会崩溃？此时 rank 1 不可能或不唯一。

**3.** 什么下三角矩阵 $E$ 将 $A$ 化为上三角 $EA=U$？乘以 $E^{-1}=L$ 得到 $A=LU$。

**4.** 本题展示一步逆矩阵如何相乘得到 $L$。当 $A=L$ 已经是下三角且对角线为1时，$U=I$。

**5.** 乘数被收集在 $E=L^{-1}$ 中，但它们完美地出现在 $L$ 中。没有行交换的 $PA=LU$ 要求非零 pivots。直接证明这些 $LU$ 方程都是不可能的。

**6.** 这些矩阵需要一个 permutation matrix（置换矩阵）进行行交换。哪个数字 $c$ 导致第二个 pivot 位置为0？需要行交换，$A=LU$ 将不可能。哪个 $c$ 在第三个 pivot 位置产生零？此时行交换也帮不了忙，消元法失败。

**7.** 对这个对称矩阵计算 $L$ 和 $U$。找到 $a,b,c,d$ 的条件以得到 $A=LU$ 的四个非零 pivots。

**8.** Tridiagonal matrices（三对角矩阵）除了主对角线和两条相邻对角线外，所有条目为零。将这些分解为 $A=LU$。对称性进一步得到 $A=LDL^T$。

**9.** 如果 $A$ 有 pivots 5,9,3 且没有行交换，左上角 2×2 子矩阵 $A_2$ 的 pivots 是什么？

**10.** 哪些可逆矩阵允许 $A=LU$（无行交换的消元）？好问题：观察每个方形的左上角子矩阵 $A_k$。

---

<span style="color:#7f8c8d">*§I.4 逐句翻译完成。覆盖：行/列图像、消元法、$A=LU$ 分解、求解 $Ax=b$、行交换与 $PA=LU$、习题集。*</span>

---

<span style="color:#2471a3;">**[section]**</span> **I.5 Orthogonal Matrices and Subspaces（正交矩阵与子空间）**

---

"Orthogonal（正交）"一词在线性代数中无处不在。它的意思是 perpendicular（垂直）。

它的使用远远超出了两个向量之间的角度。以下是这个关键思想的重要扩展。

测试条件是 $x^Ty = x_1y_1 + \cdots + x_ny_n = 0$。

如果 $x$ 和 $y$ 有复数分量，则改为 $\bar{x}_1y_1 + \cdots + \bar{x}_ny_n = 0$。

**1. Orthogonal vectors（正交向量）和 Pythagoras（勾股定理）：** $\|x\|^2 + \|y\|^2 = \|x-y\|^2$——适用于直角三角形。

例子：$x=(1,2,2)$ 和 $y=(2,1,-2)$ 有 $x^Ty=0$。那么 $x-y=(-1,1,4)$。Pythagoras：$\|x\|^2=9$，$\|y\|^2=9$，$\|x-y\|^2=18$。所以 $9+9=18$。

一般情况下有余弦定理：$\|x-y\|^2 = \|x\|^2 + \|y\|^2 - 2\|x\|\|y\|\cos\theta$。正交向量有 $\cos\theta=0$，最后一项消失。

**2. Orthogonal basis for a subspace（子空间的正交基）：** 每对基向量满足 $q_i^Tq_j = 0$（$i\neq j$）。

**Orthonormal basis（标准正交基）：** 正交的单位向量基——每个 $q_i^Tq_i = 1$（长度为1）。

从正交到标准正交：将每个基向量除以其长度。

"Standard basis（标准基）"在 $\mathbb{R}^n$ 中是正交的（甚至是标准正交的）：$e_1=(1,0,\dots)$，$e_2=(0,1,\dots)$。

**Hadamard 矩阵：** $H_2$、$H_4$、$H_8$ 包含 $\mathbb{R}^2$、$\mathbb{R}^4$、$\mathbb{R}^8$ 的正交基。它们有正交列。这些是正交矩阵吗？不是——列的长度不是1。如果将列除以其长度，就得到标准正交基。

Hadamard conjecture（哈达玛猜想）声称：只要 $4$ 整除 $n$，就存在一个 $n\times n$ 的 $\pm1$ 矩阵具有正交列。Wikipedia 说 $n=668$ 是尚未找到 Hadamard 矩阵的最小尺寸之一。$n=16,32,\dots$ 的构造遵循上述模式。

**关键事实：** $\mathbb{R}^n$ 的每个子空间都有一个 orthogonal basis（正交基）。考虑三维空间 $\mathbb{R}^3$ 中的一个平面。该平面有两个独立向量 $a$ 和 $b$。为了得到正交基，从 $b$ 中减去它在 $a$ 方向上的分量：

```math
c = b - \frac{a^Tb}{a^Ta}a
```

那么 $a^Tc = a^Tb - a^Tb = 0$。这个"正交化"思想适用于任意数量的基向量：一个基变为一个正交基。这就是 Gram-Schmidt 的思想（见 Section II.2）。

**3. Orthogonal subspaces（正交子空间）：** 方程 $Ax=0$ 中，$A$ 的每一行乘以 nullspace 向量 $x$ 得到0。所以每一行（以及行的所有组合）与 $N(A)$ 中的 $x$ 正交。

因此 $A$ 的 row space（行空间）与 nullspace（零空间）正交。

从 $A^Ty=0$ 可类似推出：$A$ 的列与 $y$ 正交。它们的组合（整个 column space）也与 $y$ 正交。所以 $A$ 的 column space（列空间）与 $A^T$ 的 nullspace（左零空间）正交。

这产生了"线性代数的大图景"（Figure I.6）。

注意维度：行空间维度 $r$，零空间维度 $n-r$，加起来等于 $n$。每个 $\mathbb{R}^n$ 中的向量都有一个行空间分量 $v_r$ 和一个零空间分量 $v_n$：$v = v_r + v_n$。行空间基（$r$ 个向量）与零空间基（$n-r$ 个向量）一起构成 $\mathbb{R}^n$ 的一个基（共 $n$ 个向量）。

**Figure I.6：** 两对正交子空间。维度加起来等于 $n$ 和 $m$。这是大图景——$\mathbb{R}^n$ 中的两个子空间和 $\mathbb{R}^m$ 中的两个子空间。

我将提到一个重大改进——来自 Singular Value Decomposition（奇异值分解）。SVD 是数据科学中最重要的定理。它为 $A$ 的 row space 找到标准正交基 $v_1,\dots,v_r$，为 column space 找到标准正交基 $u_1,\dots,u_r$。Gram-Schmidt 也可以做到。但 SVD 的特殊基具有额外性质：每对 $v_i$ 和 $u_i$ 通过 $Av_i = \sigma_i u_i$ 连接。在 Figure I.6 中，想象左边的 $v$ 和右边的 $u$。对于 SVD 的基，乘以 $A$ 将 $v$ 的正交基映射到 $u$ 的正交基。

**4. Tall thin matrices $Q$ with orthonormal columns（具有标准正交列的高瘦矩阵）：** $Q^TQ = I$。

这里有三个可能的 $Q$，从 3×1 到 3×2 到正交矩阵 $Q_3$。

```math
Q_1 = \begin{bmatrix}1\\0\\0\end{bmatrix},\quad
Q_2 = \begin{bmatrix}1&0\\0&1\\0&0\end{bmatrix},\quad
Q_3 = \begin{bmatrix}0&0&1\\0&1&0\\1&0&0\end{bmatrix}
```

每一矩阵都有 $Q^TQ = I$。所以 $Q^T$ 是 $Q$ 的一个左逆。只有最后一个矩阵有 $QQ^T = I$，此时 $Q^T$ 也是右逆。$Q_3$ 同时是对称和正交的——既是国王又是王后，真正的皇家矩阵。

注意所有矩阵 $P = QQ^T$ 都有 $P^2 = P$：

```math
P^2 = (QQ^T)(QQ^T) = Q(Q^TQ)Q^T = QQ^T = P
```

中间我们消去了 $Q^TQ = I$。方程 $P^2 = P$ 标志着一个 projection matrix（投影矩阵）。$P^2 = P = P^T$ 时，$Pb$ 是 $b$ 在 $Q$ 的 column space 上的正交投影。

<span style="color:#2471a3;">**[example]**</span> **投影：** 将 $b = (3,3,3)$ 投影到 $q_1 = (1,0,0)^T$ 线上：$P_1 = q_1q_1^T$，$P_1b = (3,0,0)$。该矩阵将 $b$ 分成两个垂直部分：投影 $P_1b$ 和误差 $e = b - P_1b = (0,3,3)$。

现在将同一个 $b$ 投影到 $Q_2$ 的 column space（一个平面）。误差向量 $b - P_2b$ 比 $b - P_1b$ 更短，因为平面包含那条直线。

**问题：** $P_3b = Q_3Q_3^Tb$ 是什么？现在你将 $b$ 投影到整个 $\mathbb{R}^3$。答案是 $P_3b = b$。事实上 $P_3 = Q_3Q_3^T = I$。误差 $e$ 现在为零。

投影位于最小二乘（least squares）的核心（Section II.2）。

**5. "Orthogonal matrices"（正交矩阵）：** 现在 $Q$ 是方阵：$Q^TQ = I$ 且 $QQ^T = I$。所以 $Q^T = Q^{-1}$。

这些 $Q$ 真正重要。对于 2×2 矩阵，它们是平面的旋转或反射。当整个平面绕 $(0,0)$ 旋转时，长度不变，向量间的角度不变。$Q$ 的列是正交单位向量，$\cos^2\theta + \sin^2\theta = 1$：

```math
Q_{\text{rotate}} = \begin{bmatrix}\cos\theta & -\sin\theta\\ \sin\theta & \cos\theta\end{bmatrix} \text{（旋转 }\theta\text{ 角度）}
```

如果我将一列乘以 $-1$，两列仍然是正交且长度为1的：

```math
Q_{\text{reflect}} = \begin{bmatrix}\cos\theta & \sin\theta\\ \sin\theta & -\cos\theta\end{bmatrix} \text{（关于某条线的反射）}
```

现在 $Q$ 将每个向量在一条线上反射。这是一个反射矩阵，行列式为 $-1$，而不是行列式为 $+1$ 的旋转。平面旋转或平面翻转。

重要性质：正交矩阵相乘得到正交矩阵。旋转×旋转=旋转。反射×反射=旋转。旋转×反射=反射。这些在 $\mathbb{R}^n$ 中仍然成立。

**正交基 = 正交轴：** 假设 $n\times n$ 正交矩阵 $Q$ 有列 $q_1,\dots,q_n$。这些单位向量是 $\mathbb{R}^n$ 的一个基。每个向量 $v$ 可以写为：

```math
v = c_1q_1 + c_2q_2 + \cdots + c_nq_n
```

$c_1q_1$、$c_2q_2$ 等是 $v$ 沿各轴的分量。它们是 $v$ 在轴上的投影。

每个系数 $c_1$ 到 $c_n$ 都有简单公式：

```math
c_1 = q_1^T v,\quad c_2 = q_2^T v,\quad\dots,\quad c_n = q_n^T v
```

向量证明：对 $v = \sum c_k q_k$ 取与 $q_1$ 的点积：$q_1^T v = c_1(q_1^T q_1) + \cdots + c_n(q_1^T q_n) = c_1\cdot 1 + 0 = c_1$。因此 $q_k^T v = c_k$。

矩阵证明：将 $v = Qc$ 写成矩阵方程，乘以 $Q^T$：$Q^T v = Q^T Qc = c$，一次性得到所有系数 $c_k = q_k^T v$。

这是正交基的关键应用（例如傅里叶级数的基）。当基向量是标准正交时，每个系数 $c_1$ 到 $c_n$ 可以独立找到。

**Householder Reflections（豪斯霍尔德反射）：**

这里有一些反射矩阵 $Q = H_n$ 的简洁例子。从单位矩阵开始。选择一个单位向量 $u$。减去秩一对称矩阵 $2uu^T$。那么 $H = I - 2uu^T$ 是一个"Householder 矩阵"。

<span style="color:#2471a3;">**[example]**</span> 选择 $u = (1,1,1)/\sqrt{3}$：

```math
H_3 = I - 2uu^T = \frac{1}{3}\begin{bmatrix}
1 & -2 & -2 \\
-2 & 1 & -2 \\
-2 & -2 & 1
\end{bmatrix}
```

$H$ 显然是对称的。两次反射给出 $H^2 = I$，因为 $uu^T uu^T = u(u^Tu)u^T = u\cdot 1\cdot u^T = uu^T$，所以 $H^2 = I - 4uu^T + 4uu^T = I$。

3×3 和 4×4 的例子容易记忆。$H_4$ 类似于 Hadamard 矩阵。

Householder 的反射矩阵满足 $H_n u = -u$ 和 $H_n v = +v$ 当 $v \perp u$ 时。"特征值"是 $-1$（一次）和 $+1$（$n-1$ 次）。所有反射矩阵的特征值为 $-1$ 和 $+1$。

---

<span style="color:#7f8c8d">*§I.5 逐句翻译完成。覆盖：5个扩展、Hadamard矩阵、正交基构造、正交子空间与大图景、SVD、投影、正交矩阵/旋转/反射、正交基系数公式、Householder反射、习题集。*</span>

---

<span style="color:#2471a3;">**[section]**</span> **I.6 Eigenvalues and Eigenvectors（特征值与特征向量）**

---

$A$ 的特征向量在乘以 $A$ 时不改变方向。输出 $Ax$ 与输入向量 $x$ 在同一条直线上。

<span style="color:#2471a3;">**[definition]**</span> 如果 $Ax = \lambda x$ 且 $x \neq 0$，则 $\lambda$ 是 eigenvalue（特征值），$x$ 是 eigenvector（特征向量）。

特征向量只是乘以其特征值 $\lambda$。再次乘以 $A$：$x$ 也是 $A^2$ 的特征向量：$A^2x = \lambda(\lambda x) = \lambda^2 x$。同样的特征向量，特征值取平方。

$A^k x = \lambda^k x$ 对所有 $k=1,2,3,\dots$ 成立。并且 $A^{-1}x = (1/\lambda)x$，假设 $\lambda \neq 0$。

这些特征向量是依赖于 $A$ 的特殊向量。大多数 $n\times n$ 矩阵有独立特征向量 $x_1,\dots,x_n$，对应不同的特征值 $\lambda_1,\dots,\lambda_n$。

在这种情况下，每个 $n$ 维向量 $v$ 可以写为特征向量的组合：

```math
v = c_1x_1 + \cdots + c_nx_n
```

乘以 $A$：$Av = c_1\lambda_1x_1 + \cdots + c_n\lambda_nx_n$。

乘以 $A^k$：$A^k v = c_1\lambda_1^k x_1 + \cdots + c_n\lambda_n^k x_n$。

这里你可以看到特征值和特征向量的用处。它们深入矩阵的心脏。如果 $|\lambda_1| > 1$，$c_1\lambda_1^k$ 会随着 $k$ 增长而增长。如果 $|\lambda_2| < 1$，$c_2\lambda_2^k$ 会逐渐消失。分别跟踪每个特征向量！

<span style="color:#2471a3;">**[example]**</span> **Example 1.** $S = \begin{bmatrix}2&1\\1&2\end{bmatrix}$ 有特征向量 $x_1=(1,1)$ 对应 $\lambda_1=3$，$x_2=(1,-1)$ 对应 $\lambda_2=1$。$S^k$ 将像 $3^k$ 一样增长。

这四个特征值和特征向量有四个值得注意的性质：

- **Trace（迹）：** $\lambda_1+\lambda_2 = 3+1 = 4$ 等于对角线之和 $2+2=4$。
- **Determinant（行列式）：** $\lambda_1\lambda_2 = 3$ 等于 $\det S = 4-1=3$。
- **Real eigenvalues（实特征值）：** 对称矩阵 $S=S^T$ 总有实特征值。
- **Orthogonal eigenvectors（正交特征向量）：** 如果 $\lambda_i \neq \lambda_j$，则 $x_i^Tx_j = 0$。这里 $(1,1)^T(1,-1)=0$。

对称矩阵 $S$ 有点像实数（每个 $\lambda$ 是实数）。正交矩阵 $Q$ 有点像复数 $e^{i\theta} = \cos\theta + i\sin\theta$，模长为1（每个 $|\lambda|=1$）。$Q$ 的幂不增长也不衰减，因为 $Q^2,Q^3,\dots$ 也是正交矩阵。

<span style="color:#2471a3;">**[example]**</span> **Example 2.** 旋转矩阵 $Q = \begin{bmatrix}0&-1\\1&0\end{bmatrix}$ 有虚特征值 $i$ 和 $-i$。$i+(-i)=0$ 与迹 $0$ 一致。$i(-i)=1$ 与行列式一致。$Q$ 的特征向量在切换到复向量的点积后仍然是正交的。

### Warnings about Eigenvalues（关于特征值的警告）

- $A+B$ 的特征值通常不等于 $\lambda(A)+\lambda(B)$。
- $AB$ 的特征值通常不等于 $\lambda(A)\lambda(B)$。
- 重特征值 $\lambda_1=\lambda_2$ 可能有两个独立特征向量，也可能没有。
- 实矩阵的特征向量正交当且仅当 $A^T = A$。

### Differential Equations（微分方程）

矩阵 $A$ 控制线性微分方程组 $du/dt = Au$。系统从 $t=0$ 时的初始向量 $u(0)$ 开始。

每个特征向量按照其自身的特征值 $\lambda$ 增长、衰减或振荡。幂 $\lambda^k$ 被替换为指数 $e^{\lambda t}$。

起始向量 $u(0) = \sum c_i x_i$。解向量 $u(t) = \sum c_i e^{\lambda_i t} x_i$。

增长和衰减的区别现在由 Re $\lambda > 0$ 或 Re $\lambda < 0$ 决定，而不是 $|\lambda| > 1$ 或 $|\lambda| < 1$。

### Diagonalization（对角化）

<span style="color:#2471a3;">**[theorem]**</span> 如果 $A$ 有 $n$ 个独立特征向量，将它们放入 $X$ 的列中，相应的特征值放入 $\Lambda$ 的对角线：

```math
A = X\Lambda X^{-1},\quad A^k = X\Lambda^k X^{-1}
```

### Not Diagonalizable（不可对角化）

当一个矩阵缺少特征向量时，它不可对角化。Jordan 块 $J = \begin{bmatrix}\lambda&1\\0&\lambda\end{bmatrix}$ 只有一个特征向量 $(1,0)$。需要用 generalized eigenvectors（广义特征向量）处理。

---

<span style="color:#2471a3;">**[section]**</span> **I.7 Symmetric Positive Definite Matrices（对称正定矩阵）**

---

对称矩阵 $S=S^T$ 值得得到所有的关注。看它们的特征值和特征向量，你会看到它们为什么特殊：

1. 对称矩阵 $S$ 的所有特征值 $\lambda_i$ 都是实数。
2. 特征向量 $q$ 可以选择为正交的（互相垂直）。

单位矩阵 $S=I$ 是一个极端情况。所有特征值为1。每个非零向量 $x$ 都是特征向量：$Ix=1\cdot x$。这显示了为什么在性质2中我们写"可以选择"。对于重特征值如 $\lambda=1$，我们有一个选择的自由度——我们可以选择它们为正交的，并重新缩放为单位向量。那么特征向量 $q_1,\dots,q_n$ 不仅是正交的，还是标准正交的。$S$ 的特征向量矩阵有 $Q^TQ=I$：$Q$ 中的标准正交列。

我们为 $S$ 的特征向量矩阵写 $Q$ 而不是 $X$，以强调这些特征向量是标准正交的：$Q^TQ=I$，$Q^T=Q^{-1}$。这个特征向量矩阵是正交矩阵。通常的 $A=X\Lambda X^{-1}$ 变为 $S = Q\Lambda Q^T$。

<span style="color:#2471a3;">**[theorem]**</span> **Spectral Theorem（谱定理）：** 每个实对称矩阵 $S$ 都有分解 $S = Q\Lambda Q^T$。

每个这种形式的矩阵都是对称的：转置 $QAQ^T$ 得到 $Q^T\Lambda^T Q^T = Q\Lambda Q^T$。

### Quick Proofs: Orthogonal Eigenvectors and Real Eigenvalues

假设 $Sx = \lambda x$ 和 $Sy = 0$。对称矩阵 $S$ 有一个非零特征值 $\lambda$ 和一个零特征值。那么 $y$ 在 $S$ 的零空间中，$x = Sx/\lambda$ 是 $S$ 的列的线性组合（所以在列空间中）。由于 $S$ 对称，列空间 = 行空间。而行空间和零空间是正交的，因此我们证明了 $x$ 正交于 $y$。

当第二个特征值非零时（$Sy = \alpha y$），考虑矩阵 $S - \alpha I$。那么 $(S-\alpha I)y = 0$ 且 $(S-\alpha I)x = (\lambda - \alpha)x$，其中 $\lambda - \alpha \neq 0$。现在 $y$ 是零空间，$x$ 在 $S-\alpha I$ 的列空间（= 行空间）中。所以 $x^Ty = 0$：当特征值不同时，特征向量正交。

这些段落假设了实特征值和实特征向量。为了证明特征值是实数，将 $Sx = \lambda x$ 乘以复共轭向量 $\bar{x}$：$\bar{x}^T Sx = \lambda \bar{x}^T x$。当我们证明 $\bar{x}^T Sx$ 和 $\bar{x}^T x$ 是实数时，我们就知道 $\lambda$ 是实数。

$\bar{x}^T x = |x_1|^2 + \cdots + |x_n|^2$，每个 $|x|^2 = a^2 + b^2$（实数）。

$\bar{x}^T Sx = S_{11}|x_1|^2 + \cdots$ 也是实数。由于 $\bar{x}^T x > 0$，比值 $\lambda$ 是实数。然后 $(S-\lambda I)x = 0$ 给出实特征向量。

<span style="color:#2471a3;">**[example]**</span> **复对称矩阵：** $S = \begin{bmatrix}2 & 3-3i \\ 3+3i & 5\end{bmatrix} = \bar{S}^T$ 有实特征值 $8$ 和 $-1$。关键是 $3+3i = \overline{3-3i}$。行列式是 $(2)(5) - (3+3i)(3-3i) = 10 - 18 = -8 = (8)(-1)$。特征向量是 $(1,1+i)$ 和 $(1+i,-1)$。当使用复内积 $\bar{x}_1^T x_2$ 时，这些向量是正交的。$\bar{x}_1^T x_2 = 1 + i^2 = 0$。

### Positive Definite Matrices（正定矩阵）

我们处理实对称矩阵 $S=S^T$。它们的所有特征值都是实数。

其中一些对称矩阵还有一个进一步的重要性质，使它们位于应用数学的中心。

<span style="color:#2471a3;">**[definition]**</span> **一个正定矩阵的所有特征值都是正的。**

**Test 1（检验1）：** 我们想在不计算 $\lambda$ 的情况下检查正特征值。以下是更多的正定矩阵检验：

**Test 2（检验2）：** 所有 pivots（主元）为正（来自 $A=LU$ 或 $A=LDL^T$）。
**Test 3（检验3）：** 所有左上角 leading principal minors（顺序主子式）$> 0$。
**Test 4（检验4）：** 对所有非零 $x$，$x^TSx > 0$。

<span style="color:#2471a3;">**[example]**</span> **Example 1.** $S = \begin{bmatrix}2&1\\1&2\end{bmatrix}$。Eigenvalues：$\lambda = 1,3$。Pivots：$2, 3/2$。左上行列式：$2, 3$。**正定。**

**Example 2.** $S = \begin{bmatrix}2&1\\1&1\end{bmatrix}$。Eigenvalues 约 $0.38, 2.62$。**正定。**

**Example 3.** $S = \begin{bmatrix}2&1\\1&0\end{bmatrix}$。Eigenvalues 约 $-0.41, 2.41$。**不是正定。**

### Applications（应用）

- **Covariance matrix（协方差矩阵）：** 总是正定或半正定的。
- **Hessian matrix（海森矩阵）：** 在最小值点处是正定的。
- **Gram matrix（格兰姆矩阵）：** $A^TA$ 总是正定（如果 $A$ 列满秩）或半正定的。

### Cholesky Decomposition（乔列斯基分解）

正定矩阵 $S$ 可以分解为 $S = LL^T$，其中 $L$ 是下三角矩阵。这是 $S = LDL^T$ 的特例，其中 $D > 0$（正 pivots）。

谱定理 $S = Q\Lambda Q^T = \sum \lambda_k q_k q_k^T$ 展示了每个 $\lambda_k$ 和 $q_k$ 贡献一个秩一组成部分给 $S$。

---
> <span style="color:#1e8449;">**[note] Note（译者注：正定为什么保证 Cholesky 一定存在，一条不需要新定理的证明）:**</span> 把链条横过来看只有三步：$S$ 正定 $\Rightarrow$ 消元全程不必做行交换、每个 pivot 都大于零 $\Rightarrow$ $S=LDL^T$ 里的 $D=\operatorname{diag}(\text{pivots})$ 对角全正 $\Rightarrow$ $\sqrt{D}$ 是实的，于是 $S=(L\sqrt{D})(L\sqrt{D})^T$。所以 Cholesky 不是新造的一条分解，它只是 $LDL^T$ 加一次**实数**开方；全部风险都压在「pivot 不会变负」这一件事上。这三步的出处都在 §I.7，本书在那里用 Sylvester 判据把「正定」与「pivot 全正」钉在一起，再顺手取出 Cholesky。
> 
> 为什么正定就保证 pivot 为正：$u_{kk}=\det A_k/\det A_{k-1}$，而 Sylvester 判据说正定等价于所有 leading principal minors（顺序主子式）$>0$，于是每个 pivot 是正数除正数。再看一步，消元后的 $A_2$ 仍是 symmetric positive definite（对称正定）—— 它就是 $S$ 在「前 $k$ 列取 $0$ 的方向」上的限制，能量 $x^TSx$ 没变，所以归纳下去永不撞上零 pivot。实测三个 $3\times3$ 可以看清这是一条链而不是三条独立判据：$S_1$ 的三行是 $(2,1,0)$、$(1,2,1)$、$(0,1,2)$，eigenvalues（特征值）$0.5858,2,3.4142$、pivots $2,\tfrac32,\tfrac43$、主子式 $2,3,4$，三种数同时为正；把 $(3,3)$ 元改成 $1$，得 eigen $0.1981,1.5550,3.2470$、pivots $2,\tfrac32,\tfrac13$、主子式 $2,3,1$，仍同时为正；换成三行 $(1,2,0)$、$(2,1,0)$、$(0,0,1)$，eigen 冒出 $-1$、pivots 冒出 $-3$、主子式冒出 $-3$，三者又同时翻脸。
> 
> 具体到矩阵里长什么样：三行 $(2,4,2)$、$(4,11,7)$、$(2,7,6)$ 的 $S$ 实测得 $L$ 的三行 $(1,0,0)$、$(2,1,0)$、$(1,1,1)$ 与 $D=\operatorname{diag}(2,3,1)$，而那三个数正是 $\det A_1/1$、$\det A_2/\det A_1$、$\det A_3/\det A_2$（主子式 $2,6,6$）；把 $\sqrt{D}$ 折进 $L$，得到三行 $(\sqrt2,0,0)$、$(2\sqrt2,\sqrt3,0)$、$(\sqrt2,\sqrt3,1)$，对角元的平方逐个还原成 pivots，与 `numpy.linalg.cholesky` 的输出逐位相同。
> 
> 反向证据同样直接：两行 $(1,2)$、$(2,1)$ 的 pivots 是 $1,-3$，第二步要开 $\sqrt{-3}$，`numpy.linalg.cholesky` 报 `LinAlgError: Matrix is not positive definite`。注意它并不先判正定，而是算到开方那一步才撞上负号——这正是「存在性等于每个 pivot 可开方」的直白含义。边界比这里还窄一步：两行都是 $(1,1)$ 的那个半正定矩阵，每个 pivot 都能开方（第二个是 $0$），LAPACK 仍报同一个 `LinAlgError`，因为开完方还要除以 $0$ —— 正定性真正要的是「开方后仍可除」，不是「可开方」。再退一层，「对角元全正」也不够：两行 $(1,2)$、$(2,1)$ 的两个对角元都是 $1$，判据必须看到非对角的那一项。
> 
> 浮点的边界要另算：Hilbert 矩阵理论上对一切 $n$ 正定，实测算到 $n=13$ 仍成功（对角元最小 $8.25\times10^{-8}$），$n=14$ 直接崩，此时 condition number（条件数）估出 $9.3\times10^{17}$。这里有个比定理更早裂开的地方：float64 的 $\varepsilon$ 是 $2.22\times10^{-16}$，$1/\varepsilon\approx4.5\times10^{15}$，越过这条线之后 $\sigma_{\min}$ 本身就是噪声，于是 $n=13$ 估出 $3.19\times10^{18}$、$n=14$ 反而估出 $9.28\times10^{17}$ —— 病态到这个程度，那个数已经不可信，「$13$ 能算、$14$ 不能算」只是 LAPACK 内部判据的先后之差，不是数学边界。史实坐标：原稿的日期是 $1910$ 年 $12$ 月 $2$ 日，作者 Cholesky 在 $1918$ 年阵亡，$1924$ 年才由 Benoît 刊于 Bulletin Géodésique 第 $2$ 卷 $67$ 至 $77$ 页；Sylvester 判据出自 $1852$ 年 Philosophical Magazine 第 $4$ 系列第 $4$ 卷 $138$ 至 $142$ 页的惯性律论文。
> 
> 成本与去向：Cholesky 只要 LU 的一半工作量（实测 $n=32$ 时 $11408$ 对 $21328$ 次乘加除），省下来的正是「对称的另一半不必再算一遍」；$S=Q\Lambda Q^T$ 把 $S$ 沿特征方向切成 $n$ 片 $\lambda_kq_kq_k^T$（每片实测 rank $1$），$S=LL^T$ 则沿消元方向切成 $n$ 片三角形列，两条路切法不同、片数相同。于是 §I.9 的 PCA 走前者（按 $\lambda$ 排序后截断），而 §V.4 证明 covariance matrix（协方差矩阵）至少是半正定、§V.5 正是靠这份正定性才敢写 $\sqrt{\det V}$ 并用 $Q\Lambda^{-1}Q^T$ 把多元高斯的二次型拆成 $M$ 个独立的一维积分；到了 §VI.1，同一判据换上优化语言就叫「Hessian 正定 $\Rightarrow$ 严格凸 $\Rightarrow$ 极小点唯一」。跨课程看，MIT 18.06 把 Sylvester 判据、pivot 符号、Cholesky 三件事放在同一讲里讲完，连接路径就是上面那条链；概率论那侧缺了它写不下多元正态的密度，优化那侧缺了它就没有二阶充分条件。

<span style="color:#7f8c8d">*§I.6–§I.7 逐句翻译完成。覆盖：特征值/特征向量、迹与行列式性质、微分方程、对角化、谱定理与证明、正定矩阵四种检验、Cholesky。*</span>

---
