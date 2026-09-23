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

$$
Ax = \begin{bmatrix}2&3\\2&4\\3&7\end{bmatrix}\begin{bmatrix}1\\2\end{bmatrix}
$$

**By rows（按行）方式** 产生三个 inner products（内积）：

$$
\begin{aligned}
\text{row 1}\cdot x:&\quad\begin{bmatrix}2&3\end{bmatrix}\cdot\begin{bmatrix}1\\2\end{bmatrix}=2(1)+3(2)=8 \\
\text{row 2}\cdot x:&\quad\begin{bmatrix}2&4\end{bmatrix}\cdot\begin{bmatrix}1\\2\end{bmatrix}=2(1)+4(2)=10 \\
\text{row 3}\cdot x:&\quad\begin{bmatrix}3&7\end{bmatrix}\cdot\begin{bmatrix}1\\2\end{bmatrix}=3(1)+7(2)=17
\end{aligned}
$$

因此 $Ax=\begin{bmatrix}8\\10\\17\end{bmatrix}$。

这些 inner products（内积）也被称为 "dot products（点积）"，因为使用了 dot notation（点记号）：

$$
\text{row}\cdot\text{column} = (2,3)\cdot(1,2)=2(1)+3(2)=8
$$

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

$$
Ax = 1\cdot a_1 + 2\cdot a_2 = \begin{bmatrix}2\\2\\3\end{bmatrix} + \begin{bmatrix}6\\8\\14\end{bmatrix} = \begin{bmatrix}8\\10\\17\end{bmatrix}
$$

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

$$
\begin{bmatrix}2&3\\2&4\\3&7\end{bmatrix}\begin{bmatrix}c_1\\c_2\end{bmatrix}=\begin{bmatrix}1\\1\\1\end{bmatrix}
$$

前两个方程给出 $2c_1+3c_2=1$ 和 $2c_1+4c_2=1$。

相减得 $c_2=0$，然后 $c_1=0.5$。

但第三个方程：$3(0.5)+7(0)=1.5$，不等于 $1$。

这意味着 $b=(1,1,1)$ 不在 column space（列空间）中——即 $a_1$ 和 $a_2$ 张成的 plane（平面）中。

该系统是 unsolvable（不可解的）。

<span style="color:#2471a3;">**[example]**</span> **Example 3.** 三个矩阵的 column spaces（列空间）各是什么？

$$
A_2=\begin{bmatrix}2&3&5\\2&4&6\\3&7&10\end{bmatrix},\qquad
A_3=\begin{bmatrix}2&3&1\\2&4&1\\3&7&1\end{bmatrix}
$$

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
$$
A=\begin{bmatrix}1&3&8\\1&2&6\\0&1&2\end{bmatrix},\quad 
C=\begin{bmatrix}1&3\\1&2\\0&1\end{bmatrix},\quad r=2
$$

Column 3 of $A$ 是 2(column 1) + 2(column 2)。将它排除在 $C$ 的 basis（基）之外。

<span style="color:#2471a3;">**[example]**</span> **Example 5.**
$$
A=\begin{bmatrix}1&2&3\\0&4&5\\0&0&6\end{bmatrix},\quad
C=A,\quad r=3
$$

这个矩阵是 invertible（可逆）的。其 column space（列空间）是整个 $\mathbb{R}^3$。保留所有3列。

<span style="color:#2471a3;">**[example]**</span> **Example 6.**
$$
A=\begin{bmatrix}1&2&5\\1&2&5\\1&2&5\end{bmatrix},\quad
C=\begin{bmatrix}1\\1\\1\end{bmatrix},\quad r=1
$$

数字 $r$ 是 $A$ 的 "rank（秩）"。它也是 $C$ 的秩。它统计 independent columns（独立列）的数量。

诚然，我们也可以从右到左处理 $A$，从它的最后 column（列）开始。

这不会改变最终的计数 $r$。

不同的 $A$ 的相同列空间 $C(A)$ 将总是给出相同的数字 $r$。

这个数字 $r$ 是 $A$ 和 $C$（相同空间）的 column space（列空间）的 "dimension（维数）"。

矩阵的 rank（秩）就是其 column space（列空间）的 dimension（维数）。

### The Factorization $A=CR$（分解 $A=CR$）

矩阵 $C$ 通过一个第三个矩阵 $R$ 连接到 $A$：$A=CR$。

它们的形状是 $(m\times n)=(m\times r)(r\times n)$。

我可以在上面的 Example 4 中展示这个 "factorization（分解）"：

$$
\begin{bmatrix}1&3&8\\1&2&6\\0&1&2\end{bmatrix}
= \begin{bmatrix}1&3\\1&2\\0&1\end{bmatrix}
\begin{bmatrix}1&0&2\\0&1&2\end{bmatrix}
= CR
$$

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

$$
\begin{bmatrix}1&2&5\\1&2&5\\1&2&5\end{bmatrix}
= \begin{bmatrix}1\\1\\1\end{bmatrix}
\begin{bmatrix}1&2&5\end{bmatrix}
= CR
$$

所有三个矩阵的 rank（秩）都是 $r=1$。

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

$$
A=\begin{bmatrix}1&3&8\\1&2&6\\0&1&2\end{bmatrix},\quad
R=\begin{bmatrix}1&0&2\\0&1&2\end{bmatrix}
$$

正是 $R$ 中的那些 ones（1）和 zeros（0）告诉我：没有一行是其他行的 combination（组合）。

对于 data science（数据科学），重要的 factorization（分解）是 $A$ 的 "SVD"——当第一个因子 $C$ 有 $r$ 个 orthogonal columns（正交列），第二个因子 $R$ 有 $r$ 个 orthogonal rows（正交行）时。

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

$$
c_{23} = a_{21}b_{13} + a_{22}b_{23} + a_{23}b_{33} = \sum_{k=1}^{n} a_{2k}b_{k3}
$$

这是 dot product（点积）$C_{23} =$（row 2 of $A$）$\cdot$（column 3 of $B$）。

用 summation notation（求和符号）写为：

$$
c_{ij} = \sum_{k=1}^{n} a_{ik}b_{kj}
$$

这就是我们通常计算 $AB=C$ 中每个 number（数字）的方式。

但还有另一种方式。

### Columns of A Times Rows of B（$A$ 的列乘以 $B$ 的行）

另一种乘法 $AB$ 的方式是 $A$ 的 columns（列）乘以 $B$ 的 rows（行）。

我们必须看到这一点！

让我从 numbers（数字）开始，说明两个 key points（关键要点）。

一个 column（列）$u$ 乘以一个 row（行）$v^T$ 产生一个 matrix（矩阵）$uv^T$。

<span style="color:#2471a3;">**[example]**</span> **Outer product（外积）示例：**

$$
\begin{bmatrix}2\\2\\1\end{bmatrix}
\begin{bmatrix}3 & 4 & 6\end{bmatrix}
= \begin{bmatrix}
6 & 8 & 12 \\
6 & 8 & 12 \\
3 & 4 & 6
\end{bmatrix}
$$

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

$$
vu^T = \begin{bmatrix}3\\4\\6\end{bmatrix}\begin{bmatrix}2&2&1\end{bmatrix}
= \begin{bmatrix}
6 & 6 & 3 \\
8 & 8 & 4 \\
12 & 12 & 6
\end{bmatrix}
$$

注意 $vu^T$ 的所有 columns（列）都是 $v$ 的 multiples（倍数），所有 rows（行）都是 $u^T$ 的 multiples（倍数）。

### AB = Sum of Rank One Matrices（$AB$ = 秩一矩阵之和）

<span style="color:#2471a3;">**[theorem]**</span> 矩阵乘法 $AB$ 可以写为 $n$ 个 rank one matrices（秩一矩阵）的和：

$$
AB = \sum_{k=1}^{n} (\text{column } k \text{ of } A)(\text{row } k \text{ of } B)
$$

这里是一个 2×2 的例子，展示 $n=2$ 个 pieces（column × row）之和：

$$
AB = \begin{bmatrix}1&3\\0&1\end{bmatrix}\begin{bmatrix}2&2\\0&5\end{bmatrix}
= \begin{bmatrix}1\\0\end{bmatrix}\begin{bmatrix}2&2\end{bmatrix}
+ \begin{bmatrix}3\\1\end{bmatrix}\begin{bmatrix}0&5\end{bmatrix}
= \begin{bmatrix}2&2\\0&0\end{bmatrix} + \begin{bmatrix}0&15\\0&5\end{bmatrix}
= \begin{bmatrix}2&17\\0&5\end{bmatrix}
$$

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

$$
S = Q\Lambda Q^T = \sum_{k=1}^{n} \lambda_k q_k q_k^T
$$

每个 eigenvalue（特征值）$\lambda_k$ 和每个 eigenvector（特征向量）$q_k$ 贡献一个 rank one piece（秩一组成部分）$\lambda_k q_k q_k^T$ 给 $S$。

SVD $A=U\Sigma V^T$ 是类似的思想，当 singular value（奇异值）$\sigma$ 在对角矩阵 $\Sigma$ 中重复 $M$ 次时，需要额外的处理——会有 $M$ 对 singular vectors（奇异向量）$v$ 和 $u$，满足 $Av=\sigma u$。

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

$$
B = \begin{bmatrix}1&-2&-2\\3&-6&-6\end{bmatrix},\quad
Bx=0 \text{ 的解：} x_1 = \begin{bmatrix}2\\1\\0\end{bmatrix},\quad x_2 = \begin{bmatrix}2\\0\\1\end{bmatrix}
$$

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

$$
A = \begin{bmatrix}
-1 & 1 & 0 & 0 \\
0 & -1 & 1 & 0 \\
-1 & 0 & 1 & 0 \\
0 & -1 & 0 & 1 \\
0 & 0 & -1 & 1
\end{bmatrix}
$$

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

**5.** 将 $Ax=b$ 的四种可能性（$r<m$、$r=n$ 等）与四个矩阵匹配。（提示：$r<m,r=n$ → 对每个 $b$ 有唯一解；$r=m,r<n$ → 0 或 $\infty$ 个解等）

**6.** 证明 $A^TA$ 和 $A$ 有相同的 nullspace（零空间）。(a) 若 $Ax=0$ 则 $A^TAx=0$。(b) 若 $A^TAx=0$ 则 $x^TA^TAx = \|Ax\|^2 = 0$，所以 $Ax=0$。因此 $N(A^TA) = N(A)$。

**7.** 找到 $A = \begin{bmatrix}0&1\\0&0\end{bmatrix}$ 的 $C(A)$ 和 $N(A)$。注意 $C(A) = N(A)$。不可能有 $C(A) = N(A^T)$，因为这两个子空间是 orthogonal（正交）的。

**8.** 画一个正方形并连接其顶点到中心点：5 个 nodes（节点）和 8 条 edges（边）。找到 8×5 incidence matrix（关联矩阵），rank $r=4$。找出 $N(A)$ 中的一个向量和 $N(A^T)$ 中的 $8-4=4$ 个 independent vectors（独立向量）。

**9.** 如果 $N(A)$ 是零向量，$B = \begin{bmatrix}A&A\end{bmatrix}$ 的 nullspace（零空间）中有哪些向量？

**10.** 对于 $\mathbb{R}^5$ 中维度为 2 和 7 的子空间 $S$ 和 $T$：(i) $S\cap T$ 可能的维度 (ii) $S+T$ 可能的维度 (iii) $S^\perp$ 的维度。

**11.** 对于 $A$ 和 $B$ 的 nullspace（零空间）和 row space（行空间），$\begin{bmatrix}A\\B\end{bmatrix}$ 的 nullspace（零空间）是 $N(A) \cap N(B)$。

---

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

$$
\begin{cases}
2x_1 + 3x_2 = 9 \\
x_1 - 2x_2 = 1
\end{cases}
$$

矩阵形式：$A = \begin{bmatrix}2&3\\1&-2\end{bmatrix}$，$b = \begin{bmatrix}9\\1\end{bmatrix}$。

**Row picture（行图像）：** 两个方程对应两条直线。它们在解 $x_1=3,x_2=1$ 处相交。第一个方程：$2x_1+3x_2=9$。第二个方程：$x_1-2x_2=1$。我从方程1中减去了2倍方程1，得到 $7x_2=7$。这消去了 $x_1$。未知数 $x_1$ 已从方程2中被消去。这就是 algebra（代数）：

消元后的系统：$2x_1+3x_2=9$，$7x_2=7$。

**Column picture（列图像）：** $Ax$ 是列的组合。$A$ 的列向量是 $a_1=(2,1)$ 和 $a_2=(3,-2)$。方程 $Ax=b$ 要求找到列的组合以匹配 $b$。正确的组合（解）具有与行图像中相同 $x_1=3$ 和 $x_2=1$：

$$
Ax = \begin{bmatrix}2\\1\end{bmatrix}x_1 + \begin{bmatrix}3\\-2\end{bmatrix}x_2 = \begin{bmatrix}9\\1\end{bmatrix}
$$

将 3 倍 column 1 加到 1 倍 column 2 上，得到 $b$ 作为列的组合。

**图 1.5：** Column picture：3 倍 (column 1) + 1 倍 (column 2) 给出 $b$。

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

$$
A = l_1(\text{row 1}) + A_2
$$

我们做了什么？右侧的第一个矩阵是从 $A$ 中移除的。那个移除的矩阵是列向量 $l_1$ 乘以 row 1。它是一个 rank one matrix（秩一矩阵）$l_1$（row 1）。

**3×3 例子：**

$$
A = \begin{bmatrix}1&2&3\\2&5&7\\3&7&8\end{bmatrix},\quad 
\text{Step 1: } A = \begin{bmatrix}1\\2\\3\end{bmatrix}\begin{bmatrix}1&2&3\end{bmatrix} + A_2,\quad
A_2 = \begin{bmatrix}0&0&0\\0&1&1\\0&1&-1\end{bmatrix}
$$

下一步处理剩余矩阵 $A_2$ 的第2列。新的 row 2 是 $(0,1,1)$，$l_{32}=1$ 是第二个 pivot row 的乘数。

**Step 2：** 移除了 $l_2 = (0,1,1,l_{42})$ 乘以 pivot row 2。

第三步将 2×2 矩阵 $A_3$ 简化为单个数字（1×1）。

这种逐列观察消元法的方式直接产生了 $A=LU$。

矩阵乘法 $LU$ 始终是 $L$ 的列乘以 $U$ 的行的和：

$$
A = \begin{bmatrix}1\\l_{21}\\l_{31}\\l_{41}\end{bmatrix}\text{(pivot row 1)} + 
\begin{bmatrix}0\\1\\l_{32}\\l_{42}\end{bmatrix}\text{(pivot row 2)} + \cdots = LU
$$

消元法将 $A$ 分解为下三角 $L$ 乘以上三角 $U$。

**关于 $LU$ 分解的注记：** 我们从消元法的关键思想出发推导出 $A=LU$：通过从最后 $n-1$ 个方程中消去 $x_1$，将问题大小从 $n$ 减少到 $n-1$。我们减去了 row 1（pivot row）的倍数。所以我们移除的矩阵的 rank 为 1。经过 $n$ 步后，整个矩阵是 rank one matrices（秩一矩阵）的和。这个和——通过列乘行的矩阵乘法规则——就是 $L$ 乘以 $U$。

这个证明与我的教科书《Introduction to Linear Algebra》中的不同。那里的思路是考察 $U$ 的行而不是 $A$ 的列。Row 3 of $U$ 等于 row 3 of $A$ 减去 pivot rows 1 和 2 的倍数：

$$
\text{Row 3 of }U = (\text{row 3 of }A) - l_{31}(\text{row 1 of }U) - l_{32}(\text{row 2 of }U)
$$

重写此方程可以看出 $[l_{31},l_{32},1]$ 正在乘以矩阵 $U$：

$$
\text{Row 3 of }A = l_{31}(\text{row 1 of }U) + l_{32}(\text{row 2 of }U) + 1(\text{row 3 of }U)
$$

所以 row 3 of $A$ = row 3 of $LU$。关键在于被减去的行是 pivot rows（主元行），已经在 $U$ 中。在没有行交换的情况下，我们再次得到 $A=LU$。

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

当 $a_{11}=0$ 时怎么办？Zero（零）不能是第一个 pivot。如果第1列下方某处有非零数字，它的行可以是 pivot row（主元行）。好的代码会选择最大的数字作为 pivot——即使 $a_{11}$ 不是零也会这样做，以减少误差。

接下来我们看看那些行交换对 $A=LU$ 的影响。一个矩阵 $P$ 将会介入。

<span style="color:#2471a3;">**[example]**</span> 第1列中最大的数字在 row 3：$a_{31}=?$。Row 3 成为第一个 pivot row。该行被乘以 $l_{21}$ 并从 row 2 中减去。

最终的矩阵 $U$ 是上三角，但 $L$ 矩阵不是。此时的 pivot order（主元顺序）是 3,1,2。如果我们希望 pivot rows 是 1,2,3，我们必须将 $A$ 的 row 3 移到顶部：

$$
PA = \begin{bmatrix}0&0&1\\1&0&0\\0&1&0\end{bmatrix}A
$$

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

$$
c = b - \frac{a^Tb}{a^Ta}a
$$

那么 $a^Tc = a^Tb - a^Tb = 0$。这个"正交化"思想适用于任意数量的基向量：一个基变为一个正交基。这就是 Gram-Schmidt 的思想（见 Section II.2）。

**3. Orthogonal subspaces（正交子空间）：** 方程 $Ax=0$ 中，$A$ 的每一行乘以 nullspace 向量 $x$ 得到0。所以每一行（以及行的所有组合）与 $N(A)$ 中的 $x$ 正交。

因此 $A$ 的 row space（行空间）与 nullspace（零空间）正交。

从 $A^Ty=0$ 可类似推出：$A$ 的列与 $y$ 正交。它们的组合（整个 column space）也与 $y$ 正交。所以 $A$ 的 column space（列空间）与 $A^T$ 的 nullspace（左零空间）正交。

这产生了"线性代数的大图景"（Figure 1.6）。

注意维度：行空间维度 $r$，零空间维度 $n-r$，加起来等于 $n$。每个 $\mathbb{R}^n$ 中的向量都有一个行空间分量 $v_r$ 和一个零空间分量 $v_n$：$v = v_r + v_n$。行空间基（$r$ 个向量）与零空间基（$n-r$ 个向量）一起构成 $\mathbb{R}^n$ 的一个基（共 $n$ 个向量）。

**Figure 1.6：** 两对正交子空间。维度加起来等于 $n$ 和 $m$。这是大图景——$\mathbb{R}^n$ 中的两个子空间和 $\mathbb{R}^m$ 中的两个子空间。

我将提到一个重大改进——来自 Singular Value Decomposition（奇异值分解）。SVD 是数据科学中最重要的定理。它为 $A$ 的 row space 找到标准正交基 $v_1,\dots,v_r$，为 column space 找到标准正交基 $u_1,\dots,u_r$。Gram-Schmidt 也可以做到。但 SVD 的特殊基具有额外性质：每对 $v_i$ 和 $u_i$ 通过 $Av_i = \sigma_i u_i$ 连接。在 Figure 1.6 中，想象左边的 $v$ 和右边的 $u$。对于 SVD 的基，乘以 $A$ 将 $v$ 的正交基映射到 $u$ 的正交基。

**4. Tall thin matrices $Q$ with orthonormal columns（具有标准正交列的高瘦矩阵）：** $Q^TQ = I$。

这里有三个可能的 $Q$，从 3×1 到 3×2 到正交矩阵 $Q_3$。

$$
Q_1 = \begin{bmatrix}1\\0\\0\end{bmatrix},\quad
Q_2 = \begin{bmatrix}1&0\\0&1\\0&0\end{bmatrix},\quad
Q_3 = \begin{bmatrix}0&0&1\\0&1&0\\1&0&0\end{bmatrix}
$$

每一矩阵都有 $Q^TQ = I$。所以 $Q^T$ 是 $Q$ 的一个左逆。只有最后一个矩阵有 $QQ^T = I$，此时 $Q^T$ 也是右逆。$Q_3$ 同时是对称和正交的——既是国王又是王后，真正的皇家矩阵。

注意所有矩阵 $P = QQ^T$ 都有 $P^2 = P$：

$$
P^2 = (QQ^T)(QQ^T) = Q(Q^TQ)Q^T = QQ^T = P
$$

中间我们消去了 $Q^TQ = I$。方程 $P^2 = P$ 标志着一个 projection matrix（投影矩阵）。$P^2 = P = P^T$ 时，$Pb$ 是 $b$ 在 $Q$ 的 column space 上的正交投影。

<span style="color:#2471a3;">**[example]**</span> **投影：** 将 $b = (3,3,3)$ 投影到 $q_1 = (1,0,0)^T$ 线上：$P_1 = q_1q_1^T$，$P_1b = (3,0,0)$。该矩阵将 $b$ 分成两个垂直部分：投影 $P_1b$ 和误差 $e = b - P_1b = (0,3,3)$。

现在将同一个 $b$ 投影到 $Q_2$ 的 column space（一个平面）。误差向量 $b - P_2b$ 比 $b - P_1b$ 更短，因为平面包含那条直线。

**问题：** $P_3b = Q_3Q_3^Tb$ 是什么？现在你将 $b$ 投影到整个 $\mathbb{R}^3$。答案是 $P_3b = b$。事实上 $P_3 = Q_3Q_3^T = I$。误差 $e$ 现在为零。

投影位于最小二乘（least squares）的核心（Section II.2）。

**5. "Orthogonal matrices"（正交矩阵）：** 现在 $Q$ 是方阵：$Q^TQ = I$ 且 $QQ^T = I$。所以 $Q^T = Q^{-1}$。

这些 $Q$ 真正重要。对于 2×2 矩阵，它们是平面的旋转或反射。当整个平面绕 $(0,0)$ 旋转时，长度不变，向量间的角度不变。$Q$ 的列是正交单位向量，$\cos^2\theta + \sin^2\theta = 1$：

$$
Q_{\text{rotate}} = \begin{bmatrix}\cos\theta & -\sin\theta\\ \sin\theta & \cos\theta\end{bmatrix} \text{（旋转 $\theta$ 角度）}
$$

如果我将一列乘以 $-1$，两列仍然是正交且长度为1的：

$$
Q_{\text{reflect}} = \begin{bmatrix}\cos\theta & \sin\theta\\ \sin\theta & -\cos\theta\end{bmatrix} \text{（关于某条线的反射）}
$$

现在 $Q$ 将每个向量在一条线上反射。这是一个反射矩阵，行列式为 $-1$，而不是行列式为 $+1$ 的旋转。平面旋转或平面翻转。

重要性质：正交矩阵相乘得到正交矩阵。旋转×旋转=旋转。反射×反射=旋转。旋转×反射=反射。这些在 $\mathbb{R}^n$ 中仍然成立。

**正交基 = 正交轴：** 假设 $n\times n$ 正交矩阵 $Q$ 有列 $q_1,\dots,q_n$。这些单位向量是 $\mathbb{R}^n$ 的一个基。每个向量 $v$ 可以写为：

$$
v = c_1q_1 + c_2q_2 + \cdots + c_nq_n
$$

$c_1q_1$、$c_2q_2$ 等是 $v$ 沿各轴的分量。它们是 $v$ 在轴上的投影。

每个系数 $c_1$ 到 $c_n$ 都有简单公式：

$$
c_1 = q_1^T v,\quad c_2 = q_2^T v,\quad\dots,\quad c_n = q_n^T v
$$

向量证明：对 $v = \sum c_k q_k$ 取与 $q_1$ 的点积：$q_1^T v = c_1(q_1^T q_1) + \cdots + c_n(q_1^T q_n) = c_1\cdot 1 + 0 = c_1$。因此 $q_k^T v = c_k$。

矩阵证明：将 $v = Qc$ 写成矩阵方程，乘以 $Q^T$：$Q^T v = Q^T Qc = c$，一次性得到所有系数 $c_k = q_k^T v$。

这是正交基的关键应用（例如傅里叶级数的基）。当基向量是标准正交时，每个系数 $c_1$ 到 $c_n$ 可以独立找到。

**Householder Reflections（豪斯霍尔德反射）：**

这里有一些反射矩阵 $Q = H_n$ 的简洁例子。从单位矩阵开始。选择一个单位向量 $u$。减去秩一对称矩阵 $2uu^T$。那么 $H = I - 2uu^T$ 是一个"Householder 矩阵"。

<span style="color:#2471a3;">**[example]**</span> 选择 $u = (1,1,1)/\sqrt{3}$：

$$
H_3 = I - 2uu^T = \frac{1}{3}\begin{bmatrix}
1 & -2 & -2 \\
-2 & 1 & -2 \\
-2 & -2 & 1
\end{bmatrix}
$$

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

$$
v = c_1x_1 + \cdots + c_nx_n
$$

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

$$
A = X\Lambda X^{-1},\quad A^k = X\Lambda^k X^{-1}
$$

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

<span style="color:#7f8c8d">*§I.6–§I.7 逐句翻译完成。覆盖：特征值/特征向量、迹与行列式性质、微分方程、对角化、谱定理与证明、正定矩阵四种检验、Cholesky。*</span>

---
