# Linear Algebra and Learning From Data（线性代数与数据学习）· VI.4

## 书页 345-357 ｜ PDF 页 347-359 ｜ Gradient Descent Toward the Minimum（梯度下降走向极小点）

> <span style="color:#7f8c8d;">本节说明：从导数的有限差分逼近（finite difference approximation）谈起，引入 gradient（梯度）向量与 steepest descent（最速下降）方向，逐步讲清梯度下降走向极小点的几何直观、收敛速率分析（m/M 比值与 condition number 条件数）、backtracking 回溯线搜索、momentum 动量（heavy ball 重球）与 Nesterov 加速，最后落到带约束的 projected/proximal gradient 方法。全节是优化算法在数据学习中的核心数学基础。</span>

---

<!-- page 347 -->
> <span style="color:#7f8c8d;">本页为书页 345，属 VI.4 引言——由单变量有限差分引入导数与 centered difference（中心差分）；页眉与印页码不译。</span>

VI.4 Gradient Descent Toward the Minimum（梯度下降走向极小点）

345

对光滑函数 $f(x)$，比值 $\Delta f/\Delta x$ 会从两侧安全地趋近导数 $df/dx$。但这种趋近可能很慢（只是一阶 first order）。

再看看点 $x=0$，此处真实导数 $df/dx=2x$ 现在为零：

```math
\text{在 }x=0\text{ 处，比值 }\frac{f(x+\Delta x)-f(x)}{\Delta x}=\frac{(\Delta x)^2}{\Delta x}
```

于是取极限得 slope（斜率）$=0$。

在这一情形以及几乎所有情形中，我们把 forward difference（前向差分，$\Delta x>0$）与 backward difference（后向差分，$\Delta x<0$）取平均，就能得到更接近极限斜率 $df/dx$ 的更好比值。这个平均值就是更精确的 centered difference（中心差分）。

```math
\text{Centered:}\quad \frac{f(x+\Delta x)-f(x-\Delta x)}{2\Delta x}
```

对例子 $f(x)=x^2$，这种 center（中心化）会产生精确的导数 $df/dx=2x$。

图中，我们把正斜率与负斜率取平均，从而在 $x=0$ 处得到正确斜率 $0$。

对所有光滑函数，中心差分把误差降到 $(\Delta x)^2$ 量级。这相比非中心差分 $f(x+\Delta x)-f(x)$ 的 $\Delta x$ 量级误差，是一大改进。

[[FIGURE: 书页 345, ReLU 函数（深度学习中的 ramp 坡道函数）图像，展示 forward、backward、centered 三种斜率逼近，$f=x^2$ 的中心斜率为精确值]]

**Figure VI.6:** 深度学习中的 ReLU function（整流线性单元）坡道。$f=x^2$ 的 centered slope（中心斜率）是精确的。

大多数有限差分逼近都采用 center（中心化）以求更高精度。但我们仍然要除以一个小数 $2\Delta x$。而且对一个 multivariable（多变量）函数 $F(x_1,x_2,\dots,x_n)$，我们需要在 $n$ 个不同方向上的比值 $\Delta F/\Delta x_i$——可能对很大的 $n$ 也如此。这些比值逼近构成 gradient vector（梯度向量）$\operatorname{grad}F=\nabla F$ 的 $n$ 个偏导数。

$F(x_1,\dots,x_n)$ 的梯度是列向量

```math
\nabla F=\begin{pmatrix}\partial F/\partial x_1\\ \vdots\\ \partial F/\partial x_n\end{pmatrix}
```

它的分量是 $F$ 的 $n$ 个偏导数。$\nabla F$ 指向最陡的方向。

例子 1–3 将展示 vector notation（向量记号）的价值（$\nabla F$ 总是列向量）。

**例 1** 对常向量 $(a_1,\dots,a_n)$，$F(x)=a^{T}x$ 有梯度 $\nabla F=a$。

$F=a_1x_1+\cdots+a_nx_n$ 的偏导数是数 $\partial F/\partial x_k=a_k$。

---

<!-- page 348 -->
> <span style="color:#7f8c8d;">本页为书页 346，属 VI.4——给出二次型、行列式、对数行列式的梯度例子，奠定梯度向量运算基础；页眉与印页码不译。</span>

**例 2** 对对称矩阵 $S$，$F(x)=x^{T}Sx$ 的梯度是 $\nabla F=2Sx$。

为看清这一点，当 $n=2$ 时把函数 $F(x_1,x_2)$ 写出来。矩阵 $S$ 是 $2\times 2$：

```math
F=\begin{pmatrix}x_1 & x_2\end{pmatrix}
\begin{pmatrix}a & b\\ b & c\end{pmatrix}
\begin{pmatrix}x_1\\ x_2\end{pmatrix}
=ax_1^2+2bx_1x_2+cx_2^2
```

```math
\nabla F=\begin{pmatrix}\partial F/\partial x_1\\ \partial F/\partial x_2\end{pmatrix}
=\begin{pmatrix}2ax_1+2bx_2\\ 2bx_1+2cx_2\end{pmatrix}=2Sx
```

**例 3** 对正定对称矩阵 $S$，二次型 $\tfrac12 x^{T}Sx-a^{T}x$ 的极小值点位于 $x^{*}=S^{-1}a$，极小值是负数 $F_{\min}=-\tfrac12 a^{T}S^{-1}a$。

这是一个重要例子！极小值出现在 $F$ 的一阶导数为零处：

```math
\nabla F=Sx-a=0\quad\text{在 }x^{*}=S^{-1}a=\arg\min F \tag{3}
```

一如既往，记号 $\arg\min F$ 表示 $F=\tfrac12 x^{T}Sx-a^{T}x$ 达到极小值的那一点 $x^{*}$。我们通常对这个极小化点 $x^{*}$ 比对那一点的极小值 $F_{\min}=F(x^{*})$ 更感兴趣：

```math
F_{\min}=\frac12 (S^{-1}a)^{T}a-a^{T}S^{-1}a=-\frac12 a^{T}S^{-1}a
```

$F$ 的图是一个 bowl（碗），在 $x=0$ 处过零点，并在 $x^{*}$ 处下探到极小值。

**例 4** 行列式 $F(X)=\det X$ 是所有 $n^2$ 个变量 $x_{ij}$ 的函数。

在 $\det X$ 的公式里，每一行的每个元素都乘以它的 "cofactor"（余子式）$C_{ij}$。这个 cofactor 是一个 $n-1$ 阶行列式，用 $X$ 中除第 $i$ 行外所有行、除第 $j$ 列外所有列，再乘以 $(-1)^{i+j}$。

```math
\frac{\partial(\det X)}{\partial x_{ij}}=C_{ij}
```

余子式矩阵 $C$ 中的 $C_{ij}$ 给出 $\nabla F$。

**例 5** 行列式的对数是极不寻常的函数：

$L(X)=\log(\det X)$ 的偏导数是

```math
\frac{\partial L}{\partial x_{ij}}=\frac{1}{\det X}C_{ij}=\left(X^{-1}\right)_{ji}
```

对 $L=\log F$ 用 chain rule（链式法则）：$(\partial L/\partial F)(\partial F/\partial x_{ij})=(1/F)(\partial F/\partial x_{ij})$。

于是这个「余子式比行列式」给出逆矩阵的 $j,i$ 位置元素。妙处在于 $X^{-1}$ 包含了 $L=\log\det X$ 的 $n^2$ 个一阶导数。$L$ 的二阶导数也同样不凡。我们有 $n^2$ 个变量与 $n^2$ 个一阶导数（都在 $\nabla L=X^{-1}$ 中）——这意味着 $n^4$ 个二阶导数！令人惊叹的是，当 $X=S$ 是对称正定时，二阶导数矩阵是负定 negative definite。

于是我们把 $L$ 变号：正定二阶导数 $\Rightarrow$ 凸函数 convex function。

```math
-\log(\det S)\text{ 是正定矩阵 }S\text{ 诸元素的凸函数。}
```

---

<!-- page 349 -->
> <span style="color:#7f8c8d;">本页为书页 347，属 VI.4——梯度向量的几何：长度即最陡斜率，最陡方向垂直于 level（等高）方向；页眉与印页码不译。</span>

### 梯度向量 $\nabla f$ 的几何

从二元函数 $f(x,y)$ 开始。它有 $n=2$ 个变量，其梯度为 $\nabla f=(\partial f/\partial x,\ \partial f/\partial y)$。

当我们移动计算导数的点 $(x,y)$ 时，这个向量的长度会变化：

```math
\text{Length}=\lVert\nabla f\rVert=\sqrt{\left(\frac{\partial f}{\partial x}\right)^2+\left(\frac{\partial f}{\partial y}\right)^2}=\text{最陡斜率}
```

长度 $\lVert\nabla f\rVert$ 告诉我们 $z=f(x,y)$ 图上的陡峭程度。这个图通常是 $xyz$ 空间里的一张曲面——像一座山或一条山谷。每一点处有 $x$ 方向的斜率 $\partial f/\partial x$ 与 $y$ 方向的斜率 $\partial f/\partial y$。最陡的斜率就在 $\nabla f=\operatorname{grad}f$ 的方向上。该最陡斜率的大小是 $\lVert\nabla f\rVert$。

**例 6** 线性函数 $f(x,y)=ax+by$ 的图是平面 $z=ax+by$。

```math
\text{梯度是向量 }\nabla f=\begin{pmatrix}a\\ b\end{pmatrix}
```

该向量的长度 $\lVert\nabla f\rVert=\sqrt{a^2+b^2}$ 是屋顶的斜率。斜率在 $\nabla f$ 方向上最陡。

这个最陡方向垂直于 level direction（等高方向）。等高方向 $z=\text{常数}$ 即 $ax+by=\text{常数}$。这是安全行走的方向，垂直于 $\nabla f$。$\nabla f$ 在这个平坦方向上的分量是零。**Figure VI.7** 展示了平面 $z=x+2y=f(x,y)$ 上的两个垂直方向（level 等高与 steepest 最陡）。

[[FIGURE: 书页 347, 平面 z=x+2y 上最陡方向与等高方向的垂直关系，负梯度 −∇f 指向最陡下降方向]]

```math
\text{plane } z=x+2y
\qquad
\text{negative gradient }-\nabla f=\begin{pmatrix}-1\\-2\end{pmatrix}
\qquad
\text{slope is }-\lVert\nabla f\rVert=-\sqrt{5}
```

```math
\text{steepest direction}=\begin{pmatrix}1\\2\end{pmatrix}\quad\text{slope is }\lVert\nabla f\rVert=\sqrt{5}
\qquad
\text{level direction}=\begin{pmatrix}2\\-1\end{pmatrix}\quad f=x+2y\text{ 在此方向为常数}
```

**Figure VI.7:** 负梯度 $-\nabla f$ 给出最陡下降的方向。

对非线性函数 $f(x,y)=ax^2+by^2$，梯度是

```math
\nabla f=\begin{pmatrix}2ax\\ 2by\end{pmatrix}
```

它告诉我们逐点变化的最陡方向。我们处在一张曲面上（一个开口朝上的 bowl 碗）。碗底在 $x=y=0$ 处，那里梯度向量为零。最陡方向的斜率是 $\lVert\nabla f\rVert$。在极小值处，

```math
\nabla f=(2ax,2by)=(0,0)\quad\text{且斜率}=0.
```

---

<!-- page 350 -->
> <span style="color:#7f8c8d;">本页为书页 348，属 VI.4——指出最速下降的核心困境：最陡方向并不指向碗底，引出 zig-zag 之字形模型问题；页眉与印页码不译。</span>

348

Optimization（最优化）

等高方向有 $z=ax^2+by^2=$ 常数高度。该平面 $z=\text{常数}$ 以一条 level curve（等高线）截穿这个碗。本例中 level curve $ax^2+by^2=c$ 是一个 ellipse（椭圆）。椭圆的方向（等高方向）垂直于梯度向量（最陡方向）。但对最速下降存在一个严重困难：

**最陡方向在你下行时不断改变！梯度并不指向碗底！**

[[FIGURE: 书页 348, 碗形 ax$^{2}$+by$^{2}$=z 上，最陡方向 ∇f 垂直于椭圆等高线却不指向极小点 (0,0)]]

```math
\text{最陡方向 }\nabla f=\begin{pmatrix}2ax\\2by\end{pmatrix}\text{ 在碗 }ax^2+by^2=z\text{ 内上下}
\qquad
\text{平坦方向 }(\nabla f)^{\perp}\text{ 沿椭圆 }ax^2+by^2=\text{常数}
```

**Figure VI.8:** 最速下降沿梯度方向 $\begin{pmatrix}2ax\\2by\end{pmatrix}$ 下移。

让我重复一遍。在点 $(x_0,y_0)$，$f=ax^2+by^2$ 的梯度方向沿 $\nabla f=(2ax_0,2by_0)$。过 $(x_0,y_0)$ 的最陡直线是

```math
2ax_0(y-y_0)=2by_0(x-x_0)
```

但最低点 $(x,y)=(0,0)$ 并不在这条直线上！我们无法用一步 "gradient descent"（梯度下降）找到这个极小点。最陡方向并不通向碗底——除非 $b=a$ 且碗是圆形。

水在下山时不断改变方向。迟早我们也必须改变方向。实践中，我们沿梯度方向继续前进，当 cost function（代价函数）$f$ 不再快速下降时就停下。此时 Step 1 结束，我们重算梯度 $\nabla f$，为 Step 2 给出新的下降方向。

### 一个 zig-zag（之字形）的重要例子

例子 $f(x,y)=\tfrac12(x^2+by^2)$ 对 $0\lt b\le 1$ 极为有用。其梯度 $\nabla f$ 有两个分量 $\partial f/\partial x=x$ 与 $\partial f/\partial y=by$。$f$ 的极小值是零，在点 $(x^{*},y^{*})=(0,0)$ 处达到。最妙的是，带精确线搜索的 steepest descent（最速下降）为缓慢下探碗底趋向 $(0,0)$ 的每个点 $(x_k,y_k)$ 产生一个简单公式。从 $(x_0,y_0)=(b,1)$ 出发，我们得到这些点：

```math
\begin{pmatrix}x_k\\ y_k\end{pmatrix}
=\begin{pmatrix}b\,r^{k}\\ (-r)^{k}\end{pmatrix}
,\qquad r=\frac{1-b}{1+b} \tag{4}
```

```math
f(x_0,y_0)=\frac12(b^2+b)=b\cdot\frac{b+1}{2}
```

---

<!-- page 351 -->
> <span style="color:#7f8c8d;">本页为书页 349，属 VI.4——用 zig-zag 例子展示 b 很小时收敛近乎停滞，并正式给出梯度下降步与 linear convergence 线性收敛概念；页眉与印页码不译。</span>

当 $b=1$ 时，你立刻看到一步成功。点 $(x_1,y_1)$ 就是 $(0,0)$。碗完美地呈圆形，$f=\tfrac12(x^2+y^2)$。负梯度方向恰好穿过 $(0,0)$。于是梯度下降的第一步就找到了 $f=0$ 处的那个正确极小点。

这个例子的真正目的在 $b$ 很小时才显现。方程 (4) 中的关键比值是 $r=(1-b)/(1+b)$。对 $b=\tfrac{1}{10}$，这个比值是 $r=-9/11$。对 $b=\tfrac{1}{100}$，比值是 $-99/101$。比值趋向 $-1$，当 $b$ 极小时，向 $(0,0)$ 的推进实际上几乎停滞。

**Figure VI.9** 展示了步进趋向 $(0,0)$ 的令人沮丧的 zig-zag 之字形模式。每一步都很短，推进极慢。这是这样一种情形：$x_{k+1}=x_k-s_k\nabla f(x_k)$ 中的 stepsize（步长）$s_k$ 被精确选取以极小化 $f$（exact line search 精确线搜索）。但 $-\nabla f$ 的方向，即便最陡，也指向远离最终答案 $(x^{*},y^{*})=(0,0)$ 的地方。

当 $b$ 很小时，这个碗已变成一条狭窄山谷，我们在徒劳地横穿山谷，而不是顺着山谷下到谷底。

[[FIGURE: 书页 349, 梯度下降在 f=½(x$^{2}$+by$^{2}$) 上的之字形路径，第一步垂直于等高集，穿过更低等高集直至与某等高集相切，然后转 90°]]

**Gradient Descent（梯度下降）**：第一个下降步从垂直于 level set（等高集）开始。当它穿过更低的等高集时，函数 $f(x,y)$ 在下降。最终其路径与某等高集 $L$ 相切。下降停止——再往前会使 $f$ 增大。第一步结束，下一步垂直于 $L$。于是之字形路径转了一个 $90^\circ$ 的弯。

**Figure VI.9:** 在 $f=\tfrac12(x^2+by^2)$ 的极小点附近沿之字形路径的缓慢收敛。

对接近 $1$ 的 $b$，这种梯度下降更快。First-order convergence（一阶收敛）意味着到 $(x^{*},y^{*})=(0,0)$ 的距离每一步被常数因子 $(1-b)/(1+b)$ 缩小。下面的分析将表明，linear convergence（线性收敛）推广到所有 strongly convex（强凸）函数 $f$——先是在每步线搜索精确时，再是（更现实地）每步搜索接近精确时。

机器学习常使用 stochastic gradient descent（随机梯度下降）。下一节将描述这种变体（当 $n$ 很大且 $x$ 有很多分量时尤其有用）。我们还记得 Newton's method（牛顿法）用二阶导数产生 quadratic convergence（二次收敛）——缩减因子 $(1-b)/(1+b)$ 掉到零，误差每步被平方。（我们的极小化二次型 $\tfrac12 x^{T}Sx$ 的模型问题一步即可解出。）

这是 approximation algorithms（近似算法）在实践中不常达到的金标准。

---

<!-- page 352 -->
> <span style="color:#7f8c8d;">本页为书页 350，属 VI.4——开始最速下降的收敛性分析，引入强凸与 m/M 比值，导出线性收敛保证；页眉与印页码不译。</span>

350

Optimization（最优化）

### 最速下降的收敛性分析

本页我们沿用 Boyd 与 Vandenberghe 在《Convex Optimization》（Cambridge University Press 出版）中的表述。从具体的 $\tfrac12(x^2+by^2)$，我们推广到 $n$ 维的任意 strongly convex（强凸）$f(x)$。

凸性由二阶导数的对称矩阵 $H=\nabla^2 f$（Hessian matrix 海森矩阵）的正定性来检验。一维时这就是数 $d^2f/dx^2$。

```math
\text{Strongly convex：}\quad m\preceq H=\nabla^2 f\preceq M
```

即 $H$ 的特征值在所有 $x$ 处都介于 $m\le\lambda\le M$。

二次型 $f=\tfrac12(x^2+by^2)$ 有二阶导数 $1$ 与 $b$。混合导数 $\partial^2 f/\partial x\partial y$ 是零。所以矩阵是对角的，它的两个特征值是 $m=b$ 与 $M=1$。我们现在将看到比值 $m/M$ 控制最速下降的速度。

梯度下降步是 $-s\nabla f_k$。我们用 Taylor series（泰勒级数）估计 $f$：

```math
f(x_{k+1})\le f(x_k)+\nabla f_k^{T}(x_{k+1}-x_k)+\frac{M}{2}\lVert x_{k+1}-x_k\rVert^2 \tag{5}
```

```math
\le f(x_k)-s\lVert\nabla f_k\rVert^2+\frac{Ms^2}{2}\lVert\nabla f_k\rVert^2 \tag{6}
```

最优的 $s$ 使左边极小化（exact line search 精确线搜索）。右边的最小值在 $s=1/M$ 处。把该数代入 $s$，下一点满足

```math
f(x_{k+1})\le f(x_k)-\frac{1}{2M}\lVert\nabla f_k\rVert^2 \tag{7}
```

一个平行论证用 $m$ 代替 $M$ 把 (5) 的不等号反号：

```math
f(x_{k+1})\ge f(x_k)-\frac{1}{2m}\lVert\nabla f_k\rVert^2 \tag{8}
```

把 (7) 乘以 $M$，(8) 乘以 $m$，相减以消去 $\lVert\nabla f(x_k)\rVert^2$。把结果改写为

```math
\text{Steady drop in }f:\qquad f(x_{k+1})-f(x^{*})\le\left(1-\frac{m}{M}\right)\left(f(x_k)-f(x^{*})\right) \tag{9}
```

这表明每一步至少把「谷底上方的高度」缩小 $1-\frac{m}{M}$。这就是 linear convergence（线性收敛）：当 $b=m/M$ 很小时极慢。

我们的 zig-zag 例子有 $m=b$、$M=1$。估计式 (9) 保证 $f(x_k)$ 高出 $f(x^{*})=0$ 的高度每一步至少缩小 $1-b$。这个完全可算的问题里的精确公式产生缩减因子 $(1-b)^2/(1+b)^2$。当 $b$ 很小时这约为 $1-4b$。所以实际改进只比 (9) 中粗略估计的 $1-b$ 好 4 倍。这给了我们相当的信心认为 (9) 是符合实际的。

---

<!-- page 353 -->
> <span style="color:#7f8c8d;">本页为书页 351，属 VI.4——引入 backtracking 回溯的非精确线搜索，并给出 momentum 动量（heavy ball 重球）思想；页眉与印页码不译。</span>

### 非精确线搜索与 Backtracking（回溯）

比值 $m/M$ 遍布 approximation theory（逼近论）与 numerical linear algebra（数值线性代数）。这正是数学分析的要义——找到像 $m/M$ 这样控制向极小值 $f(x^{*})$ 下降速率的数。

到目前为止所有线搜索都是精确的：$x_{k+1}$ 沿直线 $x=x_k-s\nabla f_k$ 精确极小化 $f(x)$。选取 $s$ 是一个单变量极小化。这条直线从 $x_k$ 沿最速下降方向移动。但我们不能指望对一般函数 $f(x)$，即便只沿一条直线，也有精确极小化的公式。所以我们需要一种快速合理的方法来找近似极小点（分析也需要对这个额外误差给出界）。

一种合理方法就是 backtracking（回溯）。从 full step（满步）$s=1$ 开始，到 $x=x_k-\nabla f_k$。检验：若 $f(x)\le f(x_k)-\alpha s\lVert\nabla f_k\rVert^2$ 且 $s=1$，就停下并接受 $x$ 作为 $x_{k+1}$。否则回溯：把 $s$ 减到 $\beta$，在 $x=x_k-\beta\nabla f_k$ 上再试该检验。若再失败，就试步长 $s=\beta^2$。因为 $\nabla f$ 是下降方向，检验最终会通过。因子 $\alpha$ 与 $\beta$ 可以是任意满足 $0<\alpha<\tfrac12$、$0<\beta<1$ 的数。

Boyd 与 Vandenberghe 表明，精确线搜索的收敛分析也推广到这个 backtracking 搜索。当然，每步向极小点保证的缩减因子 $1-(m/M)$ 现在没那么大了。但新因子 $1-\min(2m\alpha,\ 2m\alpha\beta/M)$ 仍然小于 $1$。带 backtracking 搜索的最速下降仍有 linear convergence（线性收敛）——每步一个常数因子（或更好）。

### Momentum 与重球路径

最速下降缓慢的 zig-zag 路径是个真问题，我们必须改进它。我们的模型例子 $f=\tfrac12(x^2+by^2)$ 只有两个变量 $x,y$，其二阶导数矩阵 $H$ 是对角的——常数元素 $f_{xx}=1$、$f_{yy}=b$。但当 $b=\lambda_{\min}/\lambda_{\max}=m/M$ 很小时，它把 zig-zag 问题展示得十分清楚。

**关键思想**：一个滚下坡的 heavy ball（重球）不会发生 zig-zag。它的 momentum（动量）带它穿过狭窄山谷——撞击两侧但大体朝前移动。于是我们给梯度加上系数为 $\beta$ 的动量（Polyak 的重要思想）。这给出了深度学习中最便捷也最强大的思想之一。

新步的方向 $z_k$ 记住前一步方向 $z_{k-1}$：

```math
\text{Descent with momentum：}\quad x_{k+1}=x_k-sz_k,\quad z_k=\nabla f(x_k)+\beta z_{k-1} \tag{10}
```

现在我们有两个系数要选——步长 $s$ 以及 $\beta$。最重要的是，(10) 中通向 $x_{k+1}$ 的步涉及 $z_{k-1}$。动量把一步方法（梯度下降）变成了两步方法。要回到一步，我们必须把方程 (10) 改写成两个耦合方程（一个向量方程），描述 $k+1$ 时刻的状态：

```math
\text{Descent with momentum：}\quad x_{k+1}=x_k-sz_k,\quad z_{k+1}=\nabla f(x_{k+1})+\beta z_k \tag{11}
```

---

<!-- page 354 -->
> <span style="color:#7f8c8d;">本页为书页 352，属 VI.4——把动量写成一步系统，类比二阶微分方程化一阶，给出二次模型及其收敛因子的精确解；页眉与印页码不译。</span>

```math
\text{二阶方程 }\frac{d^2y}{dt^2}+b\frac{dy}{dt}+ky=0
\quad\Rightarrow\quad
\text{一阶系统 }\frac{d}{dt}\begin{pmatrix}y\\ dy/dt\end{pmatrix}
=\begin{pmatrix}0&1\\-k&-b\end{pmatrix}\begin{pmatrix}y\\ dy/dt\end{pmatrix}
```

352

Optimization（最优化）

有了这两个方程，我们就恢复了一步方法。这正像把一个二阶微分方程化成一阶方程组。当 $dy/dt$ 与 $y$ 一起成为第二个未知量时，二阶就化为一阶。

```math
\frac{d}{dt}\begin{pmatrix}y\\v\end{pmatrix}
=\begin{pmatrix}0&1\\-k&-b\end{pmatrix}\begin{pmatrix}y\\v\end{pmatrix}
,\quad v=\frac{dy}{dt}
```

有趣的是这里的 $b$ 是 damping（阻尼）运动，而 $\beta$ 是加 momentum（动量）来促进它。

### 二次模型

当 $f=\tfrac12 x^{T}Sx$ 是二次型时，其梯度 $\nabla f=Sx$ 是线性的。这是要理解的关键模型问题：$S$ 对称正定，且 (11) 中 $\nabla f(x_{k+1})$ 变成 $Sx_{k+1}$。当矩阵 $S$ 是对角、元素为 $1$ 与 $b$ 时，我们的 $2\times2$ 超模型也包含在内。对更大的矩阵 $S$，你会看到它的最大与最小特征值决定步长 $s$ 与 $\beta$ 的最优选择——所以 $2\times2$ 情形其实包含了整个问题的本质。

为追踪 accelerated descent（加速下降）的步骤，我们跟踪 $S$ 的每个特征向量。设 $Sq=\lambda q$，且 $x_k=c_kq$、$z_k=d_kq$、$\nabla f_k=Sx_k=\lambda c_kq$。那么方程 (11) 把第 $k$ 步的数 $c_k,d_k$ 与第 $k+1$ 步的 $c_{k+1},d_{k+1}$ 连接起来。沿特征向量 $q$：

```math
\begin{pmatrix}c_{k+1}\\d_{k+1}\end{pmatrix}
=\begin{pmatrix}1&-s\\\lambda&0\end{pmatrix}
\begin{pmatrix}c_k\\d_k\end{pmatrix} \tag{12}
```

最后我们把第一个矩阵求逆（$-\lambda$ 变 $+\lambda$），看清每一步下降：

```math
\text{Descent step：}\quad
\begin{pmatrix}c_{k+1}\\d_{k+1}\end{pmatrix}
=R\begin{pmatrix}c_k\\d_k\end{pmatrix}
,\qquad
R=\begin{pmatrix}1-s\beta&-s\\s\lambda(1-\beta)&1-s\lambda\end{pmatrix} \tag{13}
```

$k$ 步之后，起始向量被乘以 $R^{k}$。

为快速收敛到零（即 $f=\tfrac12 x^{T}Sx$ 的极小值），我们想让 $R$ 的两个特征值 $e_1$ 与 $e_2$ 尽可能小。显然 $R$ 的这些特征值取决于 $S$ 的特征值 $\lambda$。该 $\lambda$ 可在 $\lambda_{\min}(S)$ 与 $\lambda_{\max}(S)$ 之间任意取值。我们的问题是：

```math
\text{选择 }s\text{ 与 }\beta\text{ 以极小化 }\max_{\lambda_{\min}(S)\le\lambda\le\lambda_{\max}(S)}|e_{\max}| \tag{14}
```

这个问题竟有一个漂亮的解，仿佛奇迹。最优的 $s$ 与 $\beta$ 是

```math
s=\left(\frac{2}{\sqrt{\lambda_{\max}}+\sqrt{\lambda_{\min}}}\right)^2
,\qquad
\beta=\left(\frac{\sqrt{\lambda_{\max}}-\sqrt{\lambda_{\min}}}{\sqrt{\lambda_{\max}}+\sqrt{\lambda_{\min}}}\right)^2 \tag{15}
```

---

<!-- page 355 -->
> <span style="color:#7f8c8d;">本页为书页 353，属 VI.4——比较普通下降与加速下降的收敛因子，突出 b→√b 的改进，并作编者注与历史类比；页眉与印页码不译。</span>

想想 $2\times2$ 超模型，当 $S$ 有特征值 $\lambda_{\max}=1$ 与 $\lambda_{\min}=b$ 时：

```math
s=\left(\frac{2}{1+\sqrt{b}}\right)^2
,\qquad
\beta=\left(\frac{1-\sqrt{b}}{1+\sqrt{b}}\right)^2 \tag{16}
```

步长与动量的这些选择给出一个看似与方程 (4) 中普通最速下降（无动量）的速率相同的收敛速率。但有一个关键区别：$b$ 被换成了 $\sqrt{b}$。

```math
\text{Ordinary descent factor：}\quad \frac{1-b}{1+b}
\qquad
\text{Accelerated descent factor：}\quad \frac{1-\sqrt{b}}{1+\sqrt{b}} \tag{17}
```

如此相似，又如此不同。真正的考验在 $b$ 极小时。那时普通下降因子本质上是 $1-4b$，非常接近 $1$。而加速下降因子本质上是 $1-4\sqrt{b}$，离 $1$ 远得多。

为强调动量带来的改进，设 $b=1/100$。那么 $\sqrt{b}=1/10$（比 $b$ 大十倍）。方程 (17) 中的收敛因子是

```math
\text{Steepest descent：}\quad \left(\frac{0.99}{1.01}\right)=\frac{99}{101}\approx0.98
\qquad
\text{Accelerated descent：}\quad \left(\frac{0.9}{1.1}\right)=\frac{9}{11}\approx0.82
```

普通下降的十步把起始误差乘以 $0.67$。这相当于一步动量步。带动量项的十步把误差乘以 $0.018$。

注意 $\lambda_{\max}/\lambda_{\min}=1/b$ 是 $S$ 的 condition number（条件数）。它控制一切。对接下来研究的非二次问题，条件数仍是关键。这个数 $\kappa$ 会变成 $L/\mu$，你稍后会看到。

**一段编者注**：这不属于说明性教材正文。它关乎梯度下降的收敛速率。我们知道一步方法（从 $x_k$ 算 $x_{k+1}$）能把误差乘以 $1-O(1/\kappa)$。在动量项中使用 $x_{k-1}$ 的两步方法能达到 $1-O(1/\sqrt{\kappa})$。条件数是 $\kappa=\lambda_{\max}/\lambda_{\min}$，对凸二次模型 $f=\tfrac12 x^{T}Sx$ 而言。我们的例子有 $1/\kappa=b$。

人们自然希望，通过使用 $n$ 个已知值 $x_k,x_{k-1},\dots,x_{k-n+1}$，能达到 $1-c\kappa^{-1/n}$。这也许不可能——即便它与 $dx/dt=f(x)$ 的有限差分公式完全平行。那里的稳定性需要对 $\Delta t$ 的步长界。下降中的稳定性需要对步长 $s$ 的界。MATLAB 的低阶代码 ODE15S 常用于 stiff（刚性）方程，ODE45 是较光滑解的主力。这些是 predictor-corrector（预测-校正）组合，目前在优化中尚不突出。

动量带来的加速像 1950 年代的 "overrelaxation"（超松弛）。David Young 的论文对应用于一类线性方程 $Ax=b$ 的迭代方法带来了同样的改进。在数值分析的早期，$A$ 被拆成 $S-T$，迭代是 $Sx_{k+1}=Tx_k+b$。它们慢得没边。如今 overrelaxation 几乎被遗忘，被更快的方法（multigrid 多重网格）取代。加速最速下降会让位于截然不同的极小化 $f(x)$ 的思想吗？

这是可能的，但难以想象。

---

<!-- page 356 -->
> <span style="color:#7f8c8d;">本页为书页 354，属 VI.4——介绍 Nesterov 加速：把梯度求值点前移，导出同样 b→√b 的收敛因子改进；页眉与印页码不译。</span>

354

Optimization（最优化）

### Nesterov Acceleration（Nesterov 加速）

另一种把 $x_{k-1}$ 带入 $x_{k+1}$ 公式的方式来自 Yuri Nesterov。他不是在 $x_k$ 处求梯度 $\nabla f$，而是把求值点移到 $x_k+\beta(x_k-x_{k-1})$。并取 $\beta$（动量系数）把两种思想结合起来。

| 方法 | 参数 |
|---|---|
| Gradient Descent（梯度下降） | Stepsize $s$，$\beta=0$ |
| Heavy Ball（重球） | Stepsize $s$，Momentum $\beta=0$ |
| Nesterov Acceleration | Stepsize $s$，Momentum $\beta$，shift $\nabla f$ by $\beta$ |

加速下降涉及全部三个参数 $s,\beta$ 以及 shift：

```math
x_{k+1}=x_k+\beta(x_k-x_{k-1})-s\nabla f\!\left(x_k+\beta(x_k-x_{k-1})\right) \tag{18}
```

为分析 $\beta$ 取动量系数的 Nesterov 收敛速率，把 (18) 化到一阶：

```math
x_{k+1}=y_k-s\nabla f(y_k)\quad\text{且}\quad y_{k+1}=x_{k+1}+\beta(x_{k+1}-x_k) \tag{19}
```

**Nesterov**：设 $f=\tfrac12 x^{T}Sx$、$\nabla f=Sx$、$Sq=\lambda q$ 如前。为跟踪这个特征向量，在 (19) 中设 $x_k=c_kq$、$y_k=d_kq$、$\nabla f(y_k)=\lambda d_kq$：

```math
(1+\beta)c_{k+1}-\beta c_k=(1+\beta)(1-s\lambda)d_k
\quad\text{即}\quad
c_{k+1}=(1-s\lambda)d_k+\beta(c_{k+1}-c_k)
```

且 $d_{k+1}=c_{k+1}+\beta(c_{k+1}-c_k)=(1+\beta)c_{k+1}-\beta c_k$。写成矩阵：

```math
\begin{pmatrix}c_{k+1}\\d_{k+1}\end{pmatrix}
=R\begin{pmatrix}c_k\\d_k\end{pmatrix}
,\qquad
R=\begin{pmatrix}1-s\lambda& -s\lambda\\ 1-s\lambda& 1-s\lambda-\beta\end{pmatrix} \tag{20}
```

每个 Nesterov 步都是乘以 $R$。设 $R$ 有特征值 $e_1$ 与 $e_2$，取决于 $s,\beta$ 与 $\lambda$。我们想让 $|e_1|$ 与 $|e_2|$ 中较大者，对所有介于 $\lambda_{\min}(S)$ 与 $\lambda_{\max}(S)$ 的 $\lambda$ 都尽可能小。$s$ 与 $\beta$ 的这些选择给出小的 $e$：

```math
s=\frac{1}{\lambda_{\max}}
,\qquad
\beta=\left(\frac{\sqrt{\lambda_{\max}}-\sqrt{\lambda_{\min}}}{\sqrt{\lambda_{\max}}+\sqrt{\lambda_{\min}}}\right)^2
\quad\Rightarrow\quad
\max\{|e_1|,|e_2|\}\le\frac{\sqrt{\lambda_{\max}}-\sqrt{\lambda_{\min}}}{\sqrt{\lambda_{\max}}+\sqrt{\lambda_{\min}}} \tag{21}
```

当 $S$ 是特征值 $\lambda_{\max}=1$、$\lambda_{\min}=b$ 的 $2\times2$ 矩阵时，该收敛因子（$R$ 的最大特征值）是 $1-\sqrt{b}$。

这展示了与 momentum（heavy ball）公式相同的高度重要改进（从 $b$ 到 $\sqrt{b}$）。Lessard、Recht 与 Packard 的完整分析发现 Nesterov 对 $s$ 与 $\beta$ 的选择可以略作改进。Su、Boyd 与 Candès 在某个特定 Nesterov 优化与这个方程之间建立了更深层的联系：

```math
\text{Model for descent：}\quad \frac{d^2x}{dt^2}+\frac{3}{t}\frac{dx}{dt}+\nabla f(t)=0
```

---

<!-- page 357 -->
> <span style="color:#7f8c8d;">本页为书页 355，属 VI.4——按难度递增列出待极小化函数的全景：严格凸、凸非严格凸、条件数、Lipschitz 常数、subgradient 次梯度；页眉与印页码不译。</span>

### 待极小化的函数：全景

函数 $f(x)$ 可以是 strictly convex（严格凸）、barely convex（勉强凸）或 non-convex（非凸）。其梯度可以是线性或非线性的。以下按难度递增列出函数类型。

**1.** $f(x,y)=\tfrac12(x^2+by^2)$。这只有 2 个变量。其梯度 $\nabla f=(x,by)$ 是线性的。其 Hessian $H$ 是元素为 $1$ 与 $b$ 的对角 $2\times2$ 矩阵。它们是 $H$ 的特征值。条件数是 $\kappa=1/b$（当 $0\lt b<1$）。严格凸。

**2.** $f(x_1,\dots,x_n)=\tfrac12 x^{T}Sx-c^{T}x$。这里 $S$ 是对称正定矩阵。梯度 $\nabla f=Sx-c$ 是线性的。Hessian 是 $H=S$。其特征值为 $\lambda_1$ 到 $\lambda_n$。条件数是 $\kappa=\lambda_{\max}/\lambda_{\min}$。严格凸。

**3.** $f(x)$ = 光滑严格凸函数。其 Hessian $H(x)$ 在所有 $x$ 处正定（$H$ 随 $x$ 变化）。$H$ 的特征值 $\lambda_1(x)$ 到 $\lambda_n(x)$ 恒正。条件数是 $\max_x(\lambda_{\max}/\lambda_{\min})$。

一个本质上等价的条件数是比值 $L/\lambda_{\min}(x)$：

```math
L=\text{“Lipschitz constant（利普希茨常数）”}\quad\text{满足}\quad
\lVert\nabla f(x)-\nabla f(y)\rVert\le L\lVert x-y\rVert \tag{22}
```

这允许梯度 $\nabla f$ 出现 corner（拐角）、二阶导数矩阵 $H$ 出现 jump（跳变）。

**4.** $f(x)$ = 凸但非严格凸。Hessian 可以只是 semi-definite（半定），$\lambda_{\min}=0$。一个小例子是 ramp function（坡道函数）$f=\text{ReLU}(x)=\max(0,x)$。梯度 $\nabla f$ 在拐角点变成一个 "subgradient"（次梯度），具有多个取值。ReLU 在 $x=0$ 的次梯度取遍从 $0$ 到 $1$ 的所有值。以这些斜率过 $(0,0)$ 的直线都待在坡道函数 $\text{ReLU}(x)$ 之下。

```math
\text{正定 }H\text{ 允许，但 }\lambda_{\min}=0\text{ 也允许。条件数可以是无穷大。}
```

$\lambda_{\min}=0$ 的最简例子沿整条线 $x+y=0$ 有极小值：

```math
f=\frac12(x+y)^2=\frac12\begin{pmatrix}x&y\end{pmatrix}
\begin{pmatrix}1&1\\1&1\end{pmatrix}
\begin{pmatrix}x\\y\end{pmatrix}
\quad(\text{半定矩阵 }S)
```

这种退化在深度学习中极为典型。网络使用的 weight（权重）数目常常远超决定这些权重的 training sample（训练样本）数目。（"MNIST" 数据集可有 $60{,}000$ 个训练样本与 $300{,}000$ 个权重。）这些权重是 underdetermined（欠定）的，但梯度下降仍能成功。为什么它的权重能 generalize（泛化）良好——对未见过的测试数据给出好答案？

当严格凸性丧失（情形 4）时，收敛证明仍可能。但条件数是无穷大。且收敛速率会变得 sublinear（次线性）。

---

<!-- page 358 -->
> <span style="color:#7f8c8d;">本页为书页 356，属 VI.4——给出线性收敛的精确定义，指出非自适应方法收敛到最小范数解，并附参考文献；页眉与印页码不译。</span>

**注**：当误差 $x_k-x^{*}$（到极小点的距离）每步被一个近似常数因子 $C<1$ 缩小时，我们说 linear convergence（线性收敛）：

```math
\text{Linear convergence：}\quad \lVert x_{k+1}-x^{*}\rVert\le C\,\lVert x_k-x^{*}\rVert \tag{23}
```

这意味着误差指数式衰减（像 $C^{k}$ 或 $e^{k\log C}$，其中 $\log C<0$）。

指数听起来很快，但当 $C$ 接近 $1$ 时可能极慢。

在极小化二次型时，non-adaptive（非自适应）方法一般收敛到 minimum norm（最小范数）解。那些解（像来自 pseudoinverse（伪逆）$A^{+}$ 的 $x=A^{+}b$）在 $A$ 的行空间中有零分量。它们有最大的 margin（间隔）。

以下是关于 gradient descent（含 VI.5 中即将到来的随机版本）的优质教材参考文献：

1. D. Bertsekas, *Convex Analysis and Optimization*, Athena Scientific (2003).
2. S. Boyd 与 L. Vandenberghe, *Convex Optimization*, Cambridge Univ. Press (2004).
3. Yu. Nesterov, *Introductory Lectures on Convex Optimization*, Springer (2004).
4. J. Nocedal 与 S. Wright, *Numerical Optimization*, Springer (1999).

四篇由 Ben Recht 参与合著的文章给梯度方法分析带来了关键新思想。文 1 与文 2 研究 accelerated descent（加速下降，即本节）；文 3 与文 4 研究 stochastic descent（随机下降）与 adaptive descent（自适应下降）。视频 5 极佳。

1. L. Lessard, B. Recht, 与 A. Packard. *Analysis and design of optimization algorithms via integral quadratic constraints*, arXiv:1408.3595v7, 2015 年 10 月 28 日。
2. A. C. Wilson, B. Recht, 与 M. Jordan, *A Lyapunov analysis of momentum methods in optimization*, arXiv:1611.02635v3, 2016 年 12 月 31 日。
3. A. C. Wilson, R. Roelofs, M. Stern, N. Srebro, 与 B. Recht, *The marginal value of adaptive gradient methods in machine learning*, arXiv:1705.08292v1, 2017 年 5 月 23 日。
4. C. Zhang, S. Bengio, M. Hardt, B. Recht, 与 O. Vinyals, *Understanding deep learning requires rethinking generalization*, arXiv:1611.03530v2, 2017 年 2 月 26 日，International Conference on Learning Representations (2017)。
5. https://simons.berkeley.edu/talks/ben-recht-2013-09-04

VI.5 节关于 stochastic gradient descent（随机梯度下降）会回到这些论文，传达这样的信息：

> 自适应方法在深度学习中可能收敛到不理想的权重。

从 $x_0=0$ 出发的梯度下降（以及 SGD）找到最小二乘的 minimum norm（最小范数）解。那些自适应方法（Adam 的变体）很流行。止步于 $x_{k-1}$ 的 $x_{k+1}$ 公式会回溯得更远——纳入自 $x_0$ 起的所有早先点。在许多问题中这带来更快训练。与 momentum 一样，memory（记忆）能帮忙。

当要确定的权重比可用的样本多时（underdetermined 欠定问题），$f(x)$ 可以有多个极小点，$\nabla f=0$ 有多个解。VI.5 的一个关键问题是，改进的自适应方法能否找到好解。

---

<!-- page 359 -->
> <span style="color:#7f8c8d;">本页为书页 357，属 VI.4——约束与 proximal 近端点方法：投影、proximal 映射、投影/近端梯度下降，落到 LASSO 软阈值；页眉与印页码不译。</span>

### Constraints 与 Proximal Points（约束与近端点）

最速下降如何处理把 $x$ 限制在凸集 $K$ 上的 constraint（约束）？

projected gradient（投影梯度）与 proximal gradient（近端梯度）方法用到四个基本思想。

**1. 投影到 $K$**：$x$ 到 $K$ 的 projection（投影）$\Pi x$ 是 $K$ 中离 $x$ 最近的点。若 $K$ 是弯曲的，则 $\Pi$ 不是线性的。想想投影到单位球 $\lVert x\rVert\le1$。此时 $\Pi x=\operatorname{proj}_K(x)=x/\lVert x\rVert$（对球外的点）。一个关键性质是 $\Pi$ 是一个 contraction（压缩映射）。把两点投影到 $K$ 会缩小它们的距离：

```math
\lVert\Pi x-\Pi y\rVert\le\lVert x-y\rVert
```

**2. Proximal mapping（近端映射）**：$\operatorname{Prox}_f(x)$ 是极小化 $\tfrac12\lVert x-z\rVert^2+f(z)$ 的向量 $z$。

```math
\operatorname{Prox}_f(x)=\arg\min_z\left\{\frac12\lVert x-z\rVert^2+f(z)\right\} \tag{24}
```

在 $f=0$（在 $K$ 内）且 $f=\infty$（在 $K$ 外）的情形，$\operatorname{Prox}_f(x)$ 恰好是投影 $\Pi x$。

**重要例子**：若 $f(x)=\lVert x\rVert_1$，则 $\operatorname{Prox}_f$ 是统计学中的 shrinkage function（收缩函数）。$x$ 的第 $i$ 个分量导出 $\operatorname{Prox}_f(x)$ 的第 $i$ 个分量。这就是 soft thresholding（软阈值）$S(x)$：

```math
S(x_i)=\operatorname{sign}(x_i)\cdot\max(|x_i|-c,\ 0)
```

[[FIGURE: 书页 357, 软阈值函数 S(x) 的图像，展示小分量被置零]]

我们在 denoising（去噪）与 regularizing（正则化），正如 III.4 节的 $\ell_1$ LASSO 构造。图展示小分量如何被置零——产生零正是 $\ell_1$ 范数相比 $\ell_2$ 已经达成的效果。

**3. Projected gradient descent（投影梯度下降）** 走一个正常下降步（可能越出约束集 $K$）。然后它把结果投影回 $K$：一个基本思想。

```math
\text{Projected descent：}\quad x_{k+1}=\operatorname{proj}_K\big(x_k-s_k\nabla f(x_k)\big) \tag{25}
```

**4. Proximal gradient descent（近端梯度下降）** 也从正常步开始。现在投影到 $K$ 被 proximal map（近端映射）取代，以确定 $s=s_k$：一个微妙的思想。

```math
\text{Proximal descent：}\quad x_{k+1}=\operatorname{prox}_{s_k f}\big(x_k-s_k\nabla f(x_k)\big) \tag{26}
```

要极小化的 LASSO 函数是 $f(x)=\tfrac12\lVert b-Ax\rVert^2+\lambda\lVert x\rVert_1$。proximal mapping 决定 $x$ 处的软阈值与步长 $s$：

```math
\operatorname{prox}_{sf}(x)=\arg\min_z\left\{\frac12\lVert x-z\rVert^2+s\lambda\lVert z\rVert_1\right\}
=S_{s\lambda}(x) \tag{27}
```

```math
\arg\min_z\left\{\frac12\lVert x-z\rVert^2+\lambda\lVert x\rVert_1\right\}
=\frac{1}{2}\lVert x-S_{s\lambda}(x)\rVert^2
```

这产生上图所示的软阈值函数 $S$ 作为更新 $x_{k+1}$。LASSO 的 proximal gradients（近端梯度，快速下降）：

```math
x_{k+1}=S_{s\lambda}\big(x_k-sA^{T}(Ax_k-b)\big)
```

---

## 译者注

> <span style="color:#27ae60;">**注一（为什么「最陡方向」反而到不了极小点——这是理解梯度下降真正困难的钥匙）。** 直觉上，「沿最陡方向下山」似乎一定能最快到谷底，但 VI.4 用 $f=\tfrac12(x^2+by^2)$ 这个碗形例子把直觉打破了。关键在几何：梯度 $\nabla f=(x,by)$ 在点 $(x_0,y_0)$ 的方向向量是 $(x_0,by_0)$，过该点的「最陡直线」由 $2ax_0(y-y_0)=2by_0(x-x_0)$ 确定，而极小点 $(0,0)$ 一般不在其上——除非 $b=a$。原因在于：最速方向是**局部的**、逐点变化的；只要等高线是椭圆（$a\ne b$，即两个主轴曲率不同），梯度方向就始终「斜着」穿过狭窄的椭圆谷，而真正的谷底方向（椭圆的短轴方向）与梯度并不重合。这就是 zig-zag 的根源：每次精确线搜索沿当前梯度方向走到与某条等高线相切（下降停止），再垂直转向，路径反复横穿山谷。$b$ 越小，山谷越窄、越扁长，横穿的幅度越接近 $90^\circ$、步长越短，收敛因子 $r=(1-b)/(1+b)$ 越逼近 $-1$，于是「几乎停滞」。这一困境是所有一阶优化方法（不只梯度下降）都要面对的核心命题，也是后面引入 momentum 与 Nesterov 加速的直接动机——它们正是靠「记住上一步方向」来避免在狭窄谷里来回横穿。</span>

> <span style="color:#27ae60;">**注二（收敛因子 $(1-b)/(1+b)$ 与「$m/M$ 控制一切」是怎么回事——一处把几何量换成谱量）。** 页 352 的收敛分析表面上换了「尺子」：从例子的具体比值 $b$，换成任意强凸函数的 $m/M$（海森 $H$ 的最小/最大特征值之比）。这并非两件事，而是同一件事的推广——对 $f=\tfrac12(x^2+by^2)$，$H$ 的特征值正是 $1$ 与 $b$，所以 $m/M=b$，$(1-b)/(1+b)$ 就是一般估计 $1-m/M$ 在这个「完全可算」的特例上的精确版。为什么要引入 $m/M$？因为对一般强凸函数，$(mI\preceq H\preceq MI)$ 把函数夹在两个「同心圆」二次型之间：$m$ 决定谷底的锐度（曲率下界，谷底越尖收敛越慢），$M$ 决定整个函数的曲率上界（限制步长 $s\le1/M$ 以免一步越过头）。二者之比 $m/M$ 就是椭圆等高线「扁平度」的谱表示——正是它控制 zig-zag 的严重程度。所以第 352 页的 $1-m/M$ 与第 349 页的 $(1-b)/(1+b)$、以及后面页 355 反复出现的 condition number $\kappa=\lambda_{\max}/\lambda_{\min}$ 是**同一条主线的三种写法**：$b=m/M=1/\kappa$。理解了这一点，整节的收敛结论就串成了一条线。</span>

> <span style="color:#27ae60;">**注三（momentum 为什么能把 $b$ 变成 $\sqrt{b}$——「记住历史」如何战胜「扁平谷」）。** 页 354-355 的结果初看像魔术：给梯度加一个动量项 $\beta z_{k-1}$，收敛因子就从 $(1-b)/(1+b)$ 变成 $(1-\sqrt{b})/(1+\sqrt{b})$，$b$ 换成了 $\sqrt{b}$。当 $b=1/100$，普通下降十步才做到的（误差乘 $0.67$），动量一步就做到，十步后误差只剩 $0.018$。机制在两点。其一，重球有惯性，会「冲」过狭窄谷的横穿方向而不被每次精确线搜索拦停——zig-zag 恰恰是「每一步都重新贴向最陡方向」造成的，动量通过保留上一步的速度分量，把一次横穿变成长距离的沿谷前行。其二，从代数看（页 353 的一阶系统与页 354 的 $R$ 矩阵），动量把一步迭代变成两步，$R$ 的最大特征值从 $(1-b)/(1+b)$ 变为 $(1-\sqrt{b})/(1+\sqrt{b})$——谱上恰好是把条件数 $\kappa=1/b$ 的「有效值」从 $1/b$ 降到 $1/\sqrt{b}$，即误差缩减因子从 $1-O(1/\kappa)$ 改善为 $1-O(1/\sqrt{\kappa})$。这与 1950 年代解线性方程组的 overrelaxation（超松弛）是同一思想：用一个可调的「记忆参数」压低迭代矩阵的谱半径。Nesterov 加速（页 356）只是把「在哪一点算梯度」这个细节换了个位置——在 $x_k+\beta(x_k-x_{k-1})$ 处求梯度——却得到完全相同的 $\sqrt{b}$ 改进，说明「看前一步」比「在哪算梯度」更本质。这条 $\sqrt{\kappa}$ 的提升至今仍是凸优化的一阶最优界，也是深度学习优化器（动量、Adam 等）的理论源头。</span>

> <span style="color:#27ae60;">**注四（proximal mapping 与软阈值——为什么 $\ell_1$ 项会把分量「抹成零」，而 $\ell_2$ 不会）。** 页 359 的 soft thresholding $S(x_i)=\operatorname{sign}(x_i)\max(|x_i|-c,0)$ 是理解稀疏性的一把钥匙。它来自 $\operatorname{Prox}_f$ 这个极小化问题：$\operatorname{Prox}_f(x)=\arg\min_z\{\tfrac12\lVert x-z\rVert^2+f(z)\}$。当 $f(z)=\lambda\lVert z\rVert_1$ 时，目标函数是 $\tfrac12(z-x_i)^2+\lambda|z_i|$（各分量独立）。它的最优解有一个硬门槛：若 $|x_i|\le\lambda$，则 $z_i=0$；若 $|x_i|>\lambda$，则 $z_i=x_i-\lambda\cdot\operatorname{sign}(x_i)$——即把 $x_i$ 朝零方向「削掉」$\lambda$。这就是「软阈值」：小分量被**恰好**归零，大分量被**均匀**收缩，中间没有过渡。与之对照，若 $f(z)=\lambda\lVert z\rVert_2^2$（$\ell_2$ 正则），最优解是 $z_i=x_i/(1+2\lambda)$，只是把所有分量按比例缩小，永不产生精确的零。正因为 $\ell_1$ 的 proximal 是「削到零」，LASSO 才能选出稀疏解（把大量权重压成 0），这是它相比 $\ell_2$（岭回归）的本质优势，也是第 359 页把它与 III.4 节的 $\ell_1$ 构造并提的原因。投影到凸集 $K$ 可看成 $f=$ 指标函数（$K$ 内 $0$、$K$ 外 $\infty$）时的特例，于是 projected descent 是 proximal descent 的特殊情形——这四点（投影、proximal、投影下降、近端下降）就这样统一在同一个极小化框架下。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么盯住条件数 $\kappa=m/M$：梯度与最速下降的动机：**</span> 这一节的核心不是"会求梯度"，而是回答一个动机问题：沿着 $\nabla f$ 方向走，凭什么就是最快的下坡？答案藏在 Taylor 展开里。把 $f(c_{k+1})$ 在 $c_k$ 处展开，取步长 $c_{k+1}-c_k=-s\nabla f_k$，一阶项 $-\nabla f^T(s\nabla f)=-s\|\nabla f\|^2$ 是负的，下降量与 $\|\nabla f\|$ 的平方成正比；而二阶项（Hessian $H$ 的特征值在 $[m,M]$ 之间）给出一个"二次惩罚" $\frac{Ms^2}{2}\|\nabla f\|^2$。于是每步下降量就是 $s\|\nabla f\|^2-\frac{Ms^2}{2}\|\nabla f\|^2$ 这对"线性收益对二次代价"的权衡——它的顶点在 $s=1/M$，这正是精确线搜索最优步长的由来。问题随之而来：Hessian 最大的特征值 $M$ 决定你能迈多大步，最小的 $m$ 决定"谷底有多窄"。二者之比 $\kappa=m/M$ 就是 condition number（条件数），它度量了等高线椭圆的扁长程度——$\kappa$ 越小碗越圆、一条直线直通谷底；$\kappa$ 越小碗越窄长，最速方向反复横穿窄谷而几乎不下行。这就是图 VI.8、VI.9 里 zig-zag 锯齿路径的根源，也是全书反复回访的同一把尺子。

> <span style="color:#1e8449;">**[note] 收敛因子 $(1-b)^2/(1+b)^2$ 从哪来：它与 $1-m/M$ 的等价关系：**</span> 正文 (4) 给出 $f=\frac12(x^2+by^2)$ 从 $(b,1)$ 出发精确线搜索的闭式迭代，步点落在 $x_k=b\,r^{2k},\ y_k=(-r)^k$，其中 $r=(b-1)/(b+1)$，于是 $f$ 每步乘上 $(1-b)^2/(1+b)^2$。这个干净公式不是巧合，而是"最速下降方向垂直于等高线"这个几何事实的直接推论：精确线搜索意味着下一步方向与当前梯度正交，于是 $x,y$ 两个坐标以 $\pm r$ 交替缩放，$f$ 的下降因子就成了 $r^2$。它要和 (9) 的一般估计 $1-m/M=1-b$ 放在一起读：一般估计保证"至少下降 $1-b$"，而精确公式给出 $(1-b)^2/(1+b)^2\approx 1-4b$（当 $b$ 小时），正好是 $1-b$ 的约四倍。也就是说，$1-m/M$ 是"任何最速下降都躲不掉的保守下界"，而 $(1-b)^2/(1+b)^2$ 是这个可完全算出的特例的"真实速度"——二者只差一个常数因子，正是这个吻合让作者"有相当信心"认为 (9) 是现实的。读者应抓住的一点：控制速度的从来不是绝对量，而是比值 $b=m/M$，这个数越小越慢。

> <span style="color:#1e8449;">**[note] momentum 把 $b$ 换成 $\sqrt b$：与牛顿法、SGD 及一个数值例子：**</span> 锯齿的根源是"每一步都忘掉上一步"，于是 heavy ball 在梯度上叠加一个动量项 $Z_k=\nabla f(c_k)+\beta Z_{k-1}$，把单步法变成两步法；这等价于把二阶方程 $y''+by'+ky=0$ 降为一阶系统，其中 $\beta$ 项像"鼓励前进"的惯性、$b$ 项像阻尼——同一套符号在力学与优化里扮演相反角色。追踪 Hessian $S$ 的特征方向后，每步化为乘以 $R$，其谱半径给出收敛因子。惊人之处在 (17)：普通下降因子 $1-4b$，而加速后是 $1-4\sqrt b$——把 $b$ 换成了 $\sqrt b$。数值对照最有说服力：取 $b=1/100$，普通下降因子约 $0.99$（走十步误差才乘 $0.67$），而加速下降因子约 $0.67$（一步就顶十步，十步误差乘 $0.018$）。这个 $\sqrt b$ 的改善正是条件数 $\kappa=1/b$ 从"一次"降为"开根号"的体现，也是 Nesterov 加速（把梯度求值点平移到 $c_k+\beta(c_k-c_{k-1})$）得到同一结论的原因。把这条线放回全书：牛顿法用二阶导把 $1-\kappa^{-1}$ 直接压到"误差平方"的二次收敛（二次模型一步到位），是加速算法达不到的黄金标准；而下一节 VI.5 的 stochastic gradient descent 在 $n$ 很大时用随机梯度代替全梯度，则是用"牺牲单步确定性"换取"每步可负担"的另一条路，condition number 与最小范数解（minimum norm solution）的话题会在那里接续。
