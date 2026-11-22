# Part VI　Optimization（最优化）· §VI.1–§VI.5

## 书页 320-369 ｜ PDF 页 322-371

---

> <span style="color:#7f8c8d;">本节是全书最优化部分的开篇：先用「图像位于弦线之下」这个几何判据定义凸性，指出凸函数恰是所有低于它的切线性函数的上包络；再把二阶导数矩阵（Hessian）引入凸性检验，建立牛顿法及其二次收敛；最后以 Levenberg–Marquardt 这一「牛顿步与梯度步的插值」收尾，作为非线性最小二乘的通用求解器。</span>

---

<!-- page 327 -->
> <span style="color:#7f8c8d;">本页为书页 325，属 VI.1 开篇——给出凸函数的定义、三个例子，以及「凸函数族的最大值仍是凸函数」「凸集族之交仍是凸集」两条核心性质；页眉与印页码不译。</span>

对于函数 $F$，凸性有一种直接的几何定义。考察介于 $x$ 与 $y$ 之间的所有点 $px+(1-p)y$，函数 $F$ 的图形（graph）停留在或低于连接两点的直线（chord）之下。

$F$ 为凸（convex），当且仅当对一切 $0\lt p<1$ 成立：

```math
F(px+(1-p)y)\ \le\ pF(x)+(1-p)F(y). \tag{1}
```

对于严格凸（strictly convex）函数，上式取严格不等号（把 $\le$ 换成 $<$），此时 $F$ 的图形严格位于连接点 $(x,F(x))$ 与 $(y,F(y))$ 的弦线之下。

值得玩味的一点是：凸函数的图形**位于其切线之上、弦线之下**。

下面是三个凸函数的例子，只有 $F_2$ 是严格凸的：

```math
F_1 = |x|,\qquad F_2 = x^2\ (\text{但不含 } -x^2),\qquad F_3 = \max(x, 0).
```

第三个函数 $F_3$ 的凸性是一个重要的事实。这正是**线性失效而凸性奏效**的地方：两个或更多线性函数的最大值通常不再是线性的；但两个或更多凸函数 $F_i(x)$ 的最大值 $F(x)$ 恒为凸。

对任意 $z = px+(1-p)y$ 位于 $x$ 与 $y$ 之间，每个函数 $F_i$ 都有

```math
F_i(z)\ \le\ pF_i(x)+(1-p)F_i(y)\ \le\ pF(x)+(1-p)F(y). \tag{2}
```

这对每个 $i$ 都成立，于是 $F(z)=\max_i F_i(z)\le pF(x)+(1-p)F(y)$，正是所需。

任意一族凸函数（特别是一族线性函数）的最大值都是凸函数。设想我们取遍所有落在凸函数 $F$ 之下的线性函数，那么这些「低于 $F$ 的线性函数」的最大值恰好等于 $F$ 本身。

[[FIGURE: 书页 325, 图 VI.2：一个凸函数 F 是其全部切线函数（linear F1、linear F2、linear F3）的最大值（上包络）。]]

一个凸集（convex set）$K$ 是所有包含它的半空间（half-space）的交。而任意一族凸集的交仍是凸集；但两个凸集的并（union）却未必是凸集。

类似地，任意一族凸函数的最大值恒为凸；但两个凸函数的最小值一般而言**不是**凸的——它可能出现「双阱（double well）」的形状。

下面给出两条关于矩阵的有用事实，其依据是「正定 + 正定 = 正定」：

- $n\times n$ 正定（positive definite）矩阵之集是凸集。
- $n\times n$ 半正定（positive semidefinite）矩阵之集是凸集。

第一类是「开（open）」集，第二类是「闭（closed）」集——它包含其半正定的极限点。

> <span style="color:#27ae60;">**译者注（凸性的几何本质）**：凸性的定义式 (1) 表面上是一行不等式，其实讲的是「割线在图形之上」。把 $p$ 从 0 连续变到 1，点 $px+(1-p)y$ 扫过线段 $[x,y]$，右端 $pF(x)+(1-p)F(y)$ 扫过连接 $(x,F(x))$ 与 $(y,F(y))$ 的割线段。所以「凸」就是说：任意两点间的割线，其函数值都落在图形上方。这就是为何严格凸函数会「在切线上方、在弦线下方」——切线是从下方逼近（一阶 Taylor 是下界），弦线是从上方逼近（凸性的定义本身就是上界）。这一「上、下两个线性界夹住函数」的图像，正是下一小节把 $F$ 写成其切线函数族上包络的直觉来源。</span>

---

<!-- page 328 -->
> <span style="color:#7f8c8d;">本页为书页 326，属 VI.1——引入二阶导数矩阵（Hessian）作为凸性的判据，并说明「双重凸性」（凸函数 + 凸集）如何避免两个孤立极小值；页眉与印页码不译。</span>

**二阶导数矩阵**

普通一元函数 $f(x)$ 是凸的，当且仅当 $d^2f/dx^2\ge 0$。理由：斜率 $df/dx$ 递增，曲线向上弯（如同抛物线 $f=x^2$，其二阶导数恒为 2）。

推广到 $n$ 个变量，就要用到 $n\times n$ 的二阶导数矩阵 $H(x)$。若 $F(x)$ 是光滑函数，则有一个近乎完美的凸性检验：

> $F(x_1,\dots,x_n)$ 是凸函数，当且仅当它的二阶导数矩阵 $H(x)$ 在一切 $x$ 处半正定。

这个 Hessian 矩阵是对称的，因为 $\partial^2F/\partial x_i\partial x_j=\partial^2F/\partial x_j\partial x_i$。若 $H(x)$ 在一切 $x$ 处正定，则 $F$ 严格凸。Hessian 的元素为

```math
H_{ij}=\frac{\partial^{2}F}{\partial x_i\,\partial x_j},\qquad
H(x)=\begin{bmatrix}
\dfrac{\partial^2 F}{\partial x_1^2} & \dfrac{\partial^2 F}{\partial x_1\partial x_2}\\[2mm]
\dfrac{\partial^2 F}{\partial x_2\partial x_1} & \dfrac{\partial^2 F}{\partial x_2^2}
\end{bmatrix}.
```

线性函数 $F=x$ 是凸的（但不严格凸）：其图形之上是一个半空间，边界平坦，二阶导数矩阵 $H=0$（极度半正定）。

二次型 $F=\tfrac12 x^TSx$ 的梯度为 $Sx$，其对称的二阶导数矩阵恰为 $S$。当 $S$ 正定时，图形之上是一个「碗（bowl）」，此 $F$ 严格凸。

**凸性阻止两个局部极小值**

我们在一个凸集 $K$ 上极小化一个凸函数 $F(x)$。这种「双重凸性」带来一个有利后果：**不会出现两个孤立的解**。若 $x$ 与 $y$ 都在 $K$ 中且给出相同的最小值，则它们连线上的一切点 $z$ 也都在 $K$ 中，并给出同样的最小值。凸性避免了那种真正危险的局面——$F$ 在 $K$ 中数目未知的分散点上各自达到最小值。

凸性的这一贡献，在一元函数 $F(x)$ 上已经看得清楚。下面是一个非凸函数的图形，它在 $x$、$y$、$z$ 处各有极小值：

[[FIGURE: 书页 326, 一个非凸函数的示意图形，在 x、y、z 三处各有一个局部极小，且在拐点 i 之前有定义区间的断口。]]

$F$ 不是凸的：它在拐点（inflection point）$i$ 之后变为凹，那里 $d^2F/dx^2$ 转负。而且 $F$ 的定义域不是凸集 $K$（因为 $x$ 与 $y$ 之间有断口）。要同时修复这两个问题，可以用直线把 $x$ 接到 $y$，并把图形终止于 $i$。

一个凸问题若要有多重解 $x$ 与 $y$，则它们之间的整个区间都必须填满解——绝不会是两个孤立的极小值，通常只是一个单点：

> 凸问题的极小点之集是凸集。

CVX 系统提供了用于「disciplined convex programming（规范凸规划）」的 MATLAB 软件。用户在其中选择 least squares（最小二乘）、linear programming（线性规划）与 quadratic programming（二次规划）。参见 cvxr.com/cvx。

> <span style="color:#27ae60;">**译者注（Hessian 与凸性的关系，以及「双重凸性」为何关键）**：一元凸性判据 $f''\ge0$ 说的是「斜率单调不减」，推广到多元就是「Hessian 处处半正定」——这等价于沿任意方向 $v$ 的二阶方向导数 $v^THv\ge0$，即无论往哪个方向走，函数都向上弯。至于「双重凸性」：凸函数保证极小值点集是凸的，凸集保证可行域 $K$ 是连通的「整块」，两者合起来才堵死「两个孤立极小点」的漏洞。若定义域有断口（非凸），函数完全可以在两端各有一个极小，而它们之间根本无可比之点。这一页实际上是在为一章的方法学打地基：只有确认了「解是唯一的、凸的」，后面的牛顿法才有明确的收敛目标 $x^*$。</span>

---

<!-- page 329 -->
> <span style="color:#7f8c8d;">本页为书页 327，属 VI.1——说明范数是凸函数（单位球是凸集），并给出牛顿法的核心：用 Hessian 的一阶近似把梯度线性化，推出牛顿步公式；页眉与印页码不译。</span>

**$\ell_1$、$\ell_2$ 与 $\ell_\infty$ 范数**

范数 $F(x)=\|x\|$ 是 $x$ 的凸函数；单位球（unit ball）$\{\|x\|\le 1\}$ 是向量 $x$ 的凸集 $K$。第一句话正是三角不等式（triangle inequality）：

```math
\|px+(1-p)y\|\ \le\ p\|x\|+(1-p)\|y\|.
```

[[FIGURE: 书页 327, 图 VI.3：三种范数（l1、l2、l∞）在平面上的单位球——菱形、圆、正方形，均以 x=0 为中心，均为凸集。]]

```math
\ell_1:\ \|x\|_1=|x_1|+|x_2|;\qquad
\ell_2:\ \|x\|_2=\sqrt{x_1^2+x_2^2};\qquad
\ell_\infty:\ \|x\|_\infty=\max(|x_1|,|x_2|).
```

**牛顿法**

我们在寻找使 $F(x)$ 达到极小、且其梯度 $\nabla F(x^*)$ 为零向量的点 $x^*$。设已到达邻近点 $x_k$，目标是移动到比 $x_k$ 更接近 $x^*$ 的新点 $x_{k+1}=\argmin F(x)$。怎样的一步 $x_{k+1}-x_k$ 合适？

微积分给出了答案。在当前点 $x_k$ 附近，梯度 $\nabla F$ 常常能用它的一阶导数（也就是 $F(x)$ 的二阶导数）来很好地估计。这些二阶导数 $\partial^2F/\partial x_i\partial x_j$ 就在 Hessian 矩阵 $H$ 里：

```math
\nabla F(x_{k+1})\ \approx\ \nabla F(x_k)+H(x_k)(x_{k+1}-x_k). \tag{3}
```

我们希望左端为零，于是当右端为零时得到 $x_{k+1}$ 的自然选择——即关于步长 $\Delta x_k=x_{k+1}-x_k$ 的 $n$ 个线性方程：

```math
H(x_k)\,\Delta x_k = -\nabla F(x_k),\qquad x_{k+1}=x_k+\Delta x_k. \tag{4}
```

牛顿法同时也在极小化一个由 $F$ 及其梯度 $\nabla F$、二阶导数 $H$ 在 $x_k$ 处拼出的二次函数：

```math
x_{k+1}\ \text{极小化}\quad
F(x_k)+\nabla F(x_k)^T(x-x_k)+\tfrac12(x-x_k)^TH(x_k)(x-x_k). \tag{5}
```

> <span style="color:#27ae60;">**译者注（牛顿法 = 在局部用二次模型替代原函数）**：式 (5) 是理解牛顿法的钥匙。它把 $F$ 在当前点 $x_k$ 处做二阶 Taylor 展开，得到一个局部的二次模型；牛顿步 $x_{k+1}$ 就是**这个二次模型**的精确极小点（而梯度下降只把 $F$ 做一阶展开，得到线性模型，只能给出方向不能给出步长）。对二次模型求梯度并令其为零，立即得到式 (4) 的线性方程组 $H\Delta x=-\nabla F$。所以牛顿法本质上是在说：「用一个抛物面去贴合原函数，跳到抛物面的顶点」。这也解释了它的二次收敛（下一页）：二次模型与真函数的误差是 $\|x-x_k\|^2$ 量级，误差每步被平方。</span>

---

<!-- page 330 -->
> <span style="color:#7f8c8d;">本页为书页 328，属 VI.1——牛顿法具有二次收敛性（以 sqrt(2) 数值计算为例），并介绍回溯线搜索作为安全步长策略；页眉与印页码不译。</span>

牛顿法是**二阶**方法：它用到了（$H$ 中的）二阶导数。新的 $x_{k+1}$ 仍会有误差，但该误差与 $x_k$ 的误差的平方成正比：

```math
\|x_{k+1}-x^*\|\ \le\ C\,\|x_k-x^*\|^2. \qquad \text{二次收敛（Quadratic convergence）} \tag{6}
```

若 $x_k$ 接近 $x^*$，则 $x_{k+1}$ 会近得多。一个例子是一维下计算 $\sqrt{2}$：牛顿法在解 $x^2-4=0$，即极小化 $F(x)=\tfrac14 x^4 - x^2$（其 $\nabla F=x^3-4x$，$H=3x^2-4$）。〔原书此处 OCR 残缺，依上下文推为：以 $f(x)=x^2-4$，$f'=2x$，牛顿迭代 $x_{k+1}=x_k-\tfrac{x_k^2-4}{2x_k}$，待核。〕

牛顿法的一步：由 $2x_k(x_{k+1}-x_k)=-(x_k^2-4)$，得 $2x_k x_{k+1}=x_k^2+4$，故牛顿取

```math
x_{k+1}=\frac12\left(x_k+\frac{4}{x_k}\right).
```

猜测平方根、除以 4、再取这两个数的平均。从 $2.5$ 出发，迭代得到

```math
x_0=2.5,\quad x_1=2.05,\quad x_2=2.0006,\quad x_3=2.000000009.
```

错误的小数位每步翻倍远离正确值：误差 $x_k-2$ 被平方

```math
x_{k+1}-2=\frac{1}{2x_k}(x_k-2)^2=\frac{1}{2x_k}\|x_k-2\|^2.
```

误差被平方，解释了牛顿法的速度——前提是 $x_k$ 足够接近 $x^*$。

牛顿法在实践中表现如何？起步时 $x_0$ 可能并不接近 $x^*$，不能指望 $x_0$ 处的二阶导数有用。于是我们算出牛顿步 $\Delta x_0=-H^{-1}\nabla F(x_0)$，但随后允许**回溯（backtracking）**：选取 $0<\alpha<1$ 与 $0<\beta<1$，把步长 $\Delta x$ 按因子 $\beta$ 缩减，直到确认新点 $x_{k+1}=x_k+t\Delta x$ 使 $F(x)$ 有足够的下降：

```math
\text{缩减 } t \text{ 直到 } F(x_k+t\Delta x)\ \le\ F(x_k)+\alpha t\,\nabla F^T\Delta x. \tag{7}
```

我们在 VI.4 会再次回到回溯。它是任意搜索方向下的一步安全措施——在方向 $\Delta x$ 自 $x_k$ 确定之后，保证 $x_{k+1}$ 的取值是安全的。或者，我们也可以固定一个小的步长（stepsize）——这就是超参数（hyperparameter）——从而在训练大型神经网络时省去搜索。

**小结**　牛顿法最终是快的，因为它用到了 $F(x)$ 的二阶导数；但这些导数可能太昂贵——尤其在高维。III.1 的拟牛顿法（Quasi-Newton）允许在算法推进中逐步积累出 Hessian $H$。神经网络往往大到根本用不了 $H$，此时 gradient descent（梯度下降）成为首选算法，将在 VI.4-5 展开。下面两页描述一种在接近 $x^*$ 时表现更好的折中方案。

---

<!-- page 331 -->
> <span style="color:#7f8c8d;">本页为书页 329，属 VI.1——引入非线性最小二乘问题，给出其平方损失误差函数与（加权）正规方程，为下一页的 Levenberg–Marquardt 做铺垫；页眉与印页码不译。</span>

**非线性最小二乘的 Levenberg–Marquardt 方法**

最小二乘从一组 $m$ 个数据点 $(t_i, y_i)$ 开始。它旨在通过选取拟合函数 $Y(t,p)$ 中的参数 $p=(p_1,\dots,p_n)$，尽可能好地拟合这 $m$ 个点。设参数就是通常的 $p=(C,D)$，拟合直线 $y=C+Dt$。那么误差平方和依赖于 $C$ 与 $D$：

```math
E(C,D)=(y_1-C-Dt_1)^2+\cdots+(y_m-C-Dt_m)^2. \tag{8}
```

最小误差 $E$ 在 $\partial E/\partial C=0$ 与 $\partial E/\partial D=0$ 处的 $C,D$ 上取得。由于 $C$ 与 $D$ 在拟合函数 $C+Dt$ 中线性出现，这些方程是线性的。我们在求 $m$ 个线性方程 $Jp=y$ 的最优最小二乘解：

```math
J^TJ\,p = J^Ty \quad\text{给出最优参数}.
```

这就是线性最小二乘（linear least squares）：拟合函数关于 $C,D$ 线性，$J$ 通常记为 $A$。但对非线性最小二乘，拟合函数 $Y(t,p)$ 以非线性方式依赖 $n$ 个参数 $p=(p_1,\dots,p_n)$。当我们极小化总误差 $E$（平方和）时，预期有 $n$ 个非线性方程来确定最优参数：

```math
E(p)=\sum_i (y_i-\hat y_i)^2 = y^Ty - 2y^T\hat y(p) + \hat y(p)^T\hat y(p). \tag{9}
```

这是要通过选取最优参数 $p$ 来极小化的「square loss（平方损失）」误差函数。

应用中可引入加权矩阵（weighting matrix）或白化矩阵（whitening matrix）$W$。$W$ 常常是逆方差 $1/\sigma_1^2,\dots,1/\sigma_m^2$ 构成的对角矩阵，它们进入总误差

```math
E=(y-\hat y)^T W (y-\hat y),
```

因此进入正规方程（normal equations）

```math
J^T W J\,p = J^T W y.
```

这给方差更小（即更可靠）的数据以更大的权重。为简单起见，下面取 $W=I$（单位权重）。

我们的问题是在式 (9) 中极小化 $E(p)$，于是计算其梯度向量 $\partial E/\partial p=\nabla E$。对线性最小二乘这个梯度是常数；但对我们的非线性问题，$\nabla E$ 依赖 $p$。下一页描述一个极小化 $E$ 的算法。

---

<!-- page 332 -->
> <span style="color:#7f8c8d;">本页为书页 330，属 VI.1——写出非线性情形的梯度（含 Jacobian）、梯度下降与近似牛顿更新，并推导 Levenberg–Marquardt 更新式，辨析它与 Gauss–Newton、真牛顿的关系；页眉与印页码不译。</span>

```math
\nabla E = 2J^T(y-\hat y),\qquad
J=\frac{\partial \hat y}{\partial p}\ \text{为 } m\times n \text{ 的 Jacobian 矩阵}. \tag{10}
```

当拟合函数 $y=C+Dt$ 关于参数 $p=(C,D)$ 线性时，$J$ 是常值 $m\times 2$ 矩阵。最小误差的最小二乘方程是 $\nabla E=0$；线性情形下即为 $J^TJp=J^Ty$。在非线性情形，我们有一阶方法（梯度下降）与近似牛顿法来解 (10)：

```math
\text{梯度下降}\quad p_{n+1}-p_n=-\delta\,J^T(y-\hat y(p_n)) \tag{11}
```

```math
\text{牛顿（近似）}\quad J^TJ\,(p_{n+1}-p_n)=J^T(y-\hat y(p_n)). \tag{12}
```

对称矩阵 $J^TJ$ 是二阶导数矩阵（函数 $E$ 的 Hessian）的近似。为看清这一点，把一阶近似 $\hat y(p+\Delta p)\approx\hat y(p)+J\Delta p$ 代入 (9) 的损失函数 $E$：

```math
E(p+\Delta p)\ \approx\ (y-\hat y(p)-J\Delta p)^T(y-\hat y(p)-J\Delta p). \tag{13}
```

二阶项是 $\Delta p^T J^TJ\Delta p$，所以 $2J^TJ$ 起着 Hessian 的作用。

Levenberg 与 Marquardt 的关键想法，是把梯度下降更新 (11) 与牛顿更新 (12) 合并成一条规则。它带有一个参数 $\lambda$：$\lambda$ 取小值偏向牛顿，取大值偏向梯度下降。这就是非线性最小二乘问题中备受喜爱（且灵活）的方法：

```math
(J^TJ+\lambda I)(p_{n+1}-p_n)=J^T(y-\hat y(p_n)). \qquad \text{Levenberg–Marquardt} \tag{14}
```

你从一个相当大的 $\lambda$ 起步。初始 $p_0$ 大概并不接近最优值 $p^*$；在离极小点 $p^*$ 这么远的地方，你无法真正信任 $J^TJ$ 的精度——因为问题非线性，$E$ 的 Hessian 依赖 $p$。

随着近似值 $p_1,p_2,\dots$ 越来越接近正确值 $p^*$，矩阵 $J^TJ$ 变得可信，于是我们把 $\lambda$ 推向零。目标是享受对 $\nabla E(p^*)=0$ 的解、即 $E(p)$ 的极小值的快速收敛（近乎牛顿）。

一个有用的变体，是把 (14) 中的 $\lambda I$ 乘以对角矩阵 $\operatorname{diag}(J^TJ)$，这样 $\lambda$ 变成无量纲的。与一切梯度下降一样，代码必须检查每一步误差 $E$ 是否下降，并按需调整步长。一个良好的下降信号表明 $\lambda$ 可以减小，下一步迭代更接近牛顿。

$\lambda=0$ 时它是否恰是牛顿法？很遗憾，我认为不是。回看 (13)：二次项表明二阶导数矩阵（Hessian）是 $2J^TJ$，但 (13) 只是一阶近似。对线性最小二乘，一阶是精确的；在非线性问题里这不可能成立。这里的正式名称是 Gauss–Newton（高斯–牛顿）。

换一种说法：我们**不能通过把一个一阶导数平方来得到二阶导数**。

尽管如此，Levenberg–Marquardt 仍是一个增强的一阶方法，对非线性最小二乘极其有用。它是训练中等规模神经网络的一种途径。

> <span style="color:#27ae60;">**译者注（Levenberg–Marquardt 到底在做什么）**：式 (14) 左边是 $(J^TJ+\lambda I)$，这是对 Hessian 的一个「正则化」：$\lambda\to0$ 时退化为近似牛顿/Gauss–Newton 步（式 (12)），$\lambda\to\infty$ 时 $\lambda I$ 压过 $J^TJ$，步长方向逼近负梯度（式 (11) 的梯度下降）。所以 $\lambda$ 是一个「信任旋钮」：离最优远、$J^TJ$ 不可信时调大 $\lambda$，走稳健的梯度方向；接近最优时调小 $\lambda$，切换到快速的（准）牛顿收敛。这正对应上一页 (7) 的回溯思想——用一维参数控制步长/方向的可信度。它回答了一个普遍困境：二阶方法快但不稳，一阶方法稳但不快，二者之间需要一个连续的插值开关。</span>

---

<!-- page 333 -->
> <span style="color:#7f8c8d;">本页为书页 331，属 VI.1 的习题集 Problem Set VI.1——围绕凸集/凸函数、凸包、Hessian、minimax 与凸函数分解设计练习；页眉与印页码不译。</span>

**Problem Set VI.1（习题集 VI.1）**

1. 两个圆盘（circular disc）的并集何时是凸集？两个正方形呢？
2. 正文提出：$\mathbb{R}^2$ 中两个三角形的并集凸，只有两种情形。这个检验对吗？若三角形在 $\mathbb{R}^3$ 中又如何？
3. $\mathbb{R}^n$ 中任意集合 $S$ 的「convex hull（凸包）」是包含 $S$ 的最小凸集 $K$。如何由集合 $S$ 构造其凸包 $K$？
4. (a) 解释为何两个凸集之交 $K_1\cap K_2$ 是凸集。
   (b) 这如何证明两个凸函数 $F_1$、$F_2$ 的最大值 $F_3$ 是凸函数？用正文定义：$F$ 凸，当且仅当「位于其图形之上及其图形上的点之集」是凸集。$F_3$ 图形之上的集合是什么？
5. 设 $K$ 凸，$F(x)=1$（当 $x\in K$），$F(x)=0$（当 $x\notin K$）。$F$ 是凸函数吗？若把 0 与 1 对调又如何？
6. 由二阶导数证明下列函数凸：
   (a) 熵 $x\log x$；
   (b) $\log(e^x+e^y)$；
   (c) $\ell_p$ 范数 $\|x\|_p=\left(|x_1|^p+|x_2|^p\right)^{1/p}$，$p\ge 1$；
   (d) $\lambda_{\max}(S)$，视作对称矩阵 $S$ 的函数。
7. $x^TSx$ 未必凸——$x^2+2xy$ 既有极大也有极小，它不凸。在极大值点处，其二阶导数矩阵 $H$ 为

```math
H=\begin{bmatrix}
-1 & -1\\
-1 & -1
\end{bmatrix}
\text{（依上下文：在驻点处半负定，$\lambda_{\max}$ 与 $\lambda_{\min}$ 一正一负，待核）}.
```

8. 本章包含形如「minimax = maximin」的陈述。但 minimax = maximin 并非总成立！解释这个例子：$\min_y\max_x(x+y)$ 与 $\max_x\min_y(x+y)$ 分别是 $+\infty$ 与 $-\infty$。
9. 设 $f(x,y)$ 是光滑凸函数，且 $f(0,0)=f(1,0)=f(0,1)=0$。
   (a) 关于 $f(\tfrac12,\tfrac12)$ 你能得出什么？
   (b) 关于导数 $a=\partial^2f/\partial x^2$、$b=\partial^2f/\partial x\partial y$、$c=\partial^2f/\partial y^2$ 你能得出什么？
10. 圆 $x^2+y^2<1$ 内的任何光滑函数 $f(x,y)$，是否都能写成两个凸函数之差 $g(x,y)-h(x,y)$？大概是肯定的。

> <span style="color:#27ae60;">**译者注（为何这些习题反复强调「并集不凸、交集凸、最大值凸、最小值不凸」）**：这组对偶贯穿整个凸分析：凸集的「交」与凸函数的「最大」保凸，而凸集的「并」与凸函数的「最小」一般不保凸。习题 4 把这两个事实用「图形之上集合」这一几何定义统一起来——$F_3=\max(F_1,F_2)$ 的上方区域恰是 $F_1$ 与 $F_2$ 上方区域的**交**，交集保凸故 $F_3$ 凸。这一「凸函数 ⇔ 其 epigraph（图形上方的集合）是凸集」的等价，正是习题 4(b)、第 5 题乃至第 10 题（$f=g-h$ 的凸分解）的共同线索：把函数的凸性翻译成集合的凸性，许多证明便化为一步之交。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么把「凸性」当作可优化的准绳：**</span> 这一节把「求最小值」这件本来很凶险的事，换成了一条可验证的代数判据。普通的 $F(x)$ 可能有若干个彼此孤立的局部极小，优化算法停在哪个全看初值运气；而一旦 $F$ 是凸函数、定义域 $K$ 是凸集，正文里那句「convexity avoids the truly dangerous situation」就不是一句口号，而是一条定理：若 $x$ 与 $y$ 都取到同一个最小值，则它们连线上的一切点 $z = px + (1-p)y$ 也取同一个最小值。换句话说，凸问题里**不可能出现两个被「山谷」隔开的孤立极小点**，最小值点全体构成一个凸集（通常就是单个点）。这正是 (1) 式 $F(px+(1-p)y) \le pF(x)+(1-p)F(y)$ 存在的意义：它不只是一个函数形状的描述，而是「一旦你说函数凸，我就敢保证下降法不会陷进假的坑里」的许可证。于是整个后续——Hessian 矩阵半正定的判定、Newton 迭代、Levenberg–Marquardt——全都建立在这条许可之上：先确认问题凸（或至少局部凸），再谈算法收敛。

> <span style="color:#1e8449;">**[note] 凸性判据里「半正定 Hessian」与「切平面在下」是同一件事：**</span> 一维时凸等价于 $f''(x) \ge 0$，理由很朴素：斜率 $f'$ 单调不减，曲线向上弯。推广到 $n$ 维，正文给出「almost perfect test」——$F$ 凸当且仅当其 Hessian 矩阵 $H(x) = \left[\frac{\partial^2 F}{\partial x_i \partial x_j}\right]$ 处处半正定。这里值得点破两层等价：其一，$H$ 半正定当且仅当对任意方向 $v$ 有 $v^T H v \ge 0$，这正是「沿每个方向看，曲率都不为负」的逐方向版本；其二，二次型的 Taylor 展开 $F(x+\Delta) \approx F(x) + \nabla F^T \Delta + \tfrac12 \Delta^T H \Delta$ 告诉我们，$H \succeq 0$ 恰好意味着图形**在每一条切平面之上**，即正文那句「the graph stays above its tangent lines and below its chords」。而「切平面在下」又等价于正文图 VI.2 的刻画：$F$ 是所有**位于它下方**的线性函数（切函数）的上包络。所以「半正定 Hessian」「切平面在下」「下支撑线性函数族的上包络」这三个说法是同一枚硬币的三面，理解了这一点，后面用 $J^T J$ 去近似 Hessian 时为什么要求它半正定也就顺理成章了。

> <span style="color:#1e8449;">**[note] 从 $\sqrt{4}$ 看 Newton 法的二次收敛，以及它与 §III.1、§VI.4 的衔接：**</span> 正文用一维例子 $F(x) = \tfrac12 x^2 - 2x + 2$（即最小化到 $x^* = 2$，等价于解 $x^2 - 4 = 0$ 求 $\sqrt{4}$）把 (6) 式的二次收敛讲活了：迭代 $x_{k+1} = \frac{1}{2}(x_k + \frac{4}{x_k})$，就是「猜一个平方根、拿 4 去除它、再取两者平均」的古法；从 $x_0 = 2.5$ 出发，误差按 $e_{k+1} \approx \frac{1}{2x_k} e_k^2$ 平方地收缩，$2.5 \to 2.05 \to 2.0006 \to 2.000000009$，错误的小数位数每一步翻倍。这里要看清 (4) 式 Newton 步 $H \Delta x = -\nabla F$ 其实是在 (5) 式那个用 $F$、$\nabla F$、$H$ 拼出的**二次近似**上求精确最小值——所以 Newton 的每一次更新，都是在「相信二阶信息」与「万一二阶信息不可靠」之间做赌注。这正是本节的真实张力：二阶信息让收敛飞快，但高维时 $H$ 太贵甚至不可靠，于是正文把话说全——§III.1 的 quasi-Newton 让 $H$ 逐步攒出来，§VI.4 的 backtracking（(7) 式的 $F(x_k + t\Delta x) \le F(x_k) + \alpha t \nabla F^T \Delta x$）给任意下降方向上一道安全保险，而 §VI.4–5 的梯度下降则是在神经网络大到算不动 $H$ 时退而求其次。把这三处串起来，本节「Newton 快但要靠近 $x^*$、离得远就先小心翼翼地走」的主线就完整了。

---

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

---

> <span style="color:#7f8c8d;">本节先给出线性规划的对偶问题与弱/强对偶定理，再用「最大流—最小割」与「二人零和博弈」两个经典例子说明对偶的含义，最后引入半定规划（SDP）作为约束从线性推广到矩阵不等式的自然延伸。全节核心是同一个思想：一个最小化问题的对偶是一个最大化问题，二者在最优处「相遇」。</span>

---

<!-- page 341 -->

> <span style="color:#7f8c8d;">本页为书页 339，属 VI.3 开头，回顾单纯形法并正式写出对偶问题、弱对偶与强对偶（minimax 定理）；页眉与印页码不译。</span>

在 simplex method（单纯形法）中，每一次都是从新的起点 corner（角点）、沿新的 steepest edge（最陡边）、走向成本更低的角点。实际上，迭代步数是 polynomial（多项式的），但理论上却可能是 exponential（指数的）。

我们这里的兴趣在于识别出 dual problem（对偶问题）——一个关于 $y\in\mathbb{R}^m$ 的 maximum problem（最大化问题）。通常用 $y$ 而不是 $\lambda$ 来表示对偶未知量，也就是 Lagrange multipliers（拉格朗日乘子）。

```math
\begin{aligned}
&\text{Maximize } y^{T}b \\
&\text{subject to } A^{T}y \le c .
\end{aligned}\tag{2}
```

Dual Problem（对偶问题）

这又是一个可以交给单纯形法求解的 linear program（线性规划）。它和原来一样，输入还是 $A,b,c$。当矩阵 $A$ 是 $m\times n$ 时，矩阵 $A^{T}$ 就是 $n\times m$。所以 $A^{T}y\le c$ 有 $n$ 条约束。一个漂亮的事实是：最大化问题里的 $y^{T}b$ 永远不会大于最小化问题里的 $c^{T}x$。

Weak duality（弱对偶）：$y^{T}b=(Ax)^{T}y=x^{T}(A^{T}y)\le x^{T}c=c^{T}x$，即 Maximum（2）$\le$ Minimum（1）。

最大化把 $y^{T}b$ 往上推，最小化把 $c^{T}x$ 往下压。伟大的 duality theorem（对偶定理，即 minimax theorem / 极小极大定理）说：二者在最优点 $x^{*}$ 与 $y^{*}$ 处恰好相遇。

Duality（对偶性）：$y^{T}b$ 的最大值等于 $c^{T}x$ 的最小值。

单纯形法会同时解出这两个问题。多年来该方法一直没有对手，但现在情况变了。更新的算法不再沿可行集的边绕行（从一个角点到另一个角点），而是直接穿过可行点集的内部。Interior point methods（内点法）之所以有竞争力，是因为它们能用微积分来实现 steepest descent（最速下降）。眼下的局面是：沿边走还是走内部，两种方法都可能胜出。

## Max Flow-Min Cut（最大流—最小割）

这里有一个特殊的线性规划。矩阵 $A$ 是一张图的 incidence matrix（关联矩阵），它意味着每个 node（节点）流入等于流出。图的每条 edge（边）有一个 capacity（容量）$M_i$——沿该边的 flow（流量）$y_i$ 不得超过它。

这个最大化问题，是要从 source node（源点）$s$ 向 sink node（汇点）$t$ 发送尽可能大的流量。这个流量又从 $t$ 经一条 capacity 无限的特边回流到 $s$——画在下一页。对 $y$ 的约束是 Kirchhoff's Current Law（基尔霍夫电流定律）$A^{T}y=0$，以及图上每条边的容量上界 $M_i$。这个例子的妙处在于（对一张小图）你可以凭常识把它解出来。在此过程中，你会顺带发现并解出它的对偶最小化问题——也就是 min cut（最小割）。

<!-- page 342 -->

> <span style="color:#7f8c8d;">本页为书页 340，用一张具体的图演示最大流等于最小割（这里 M=14），并引出二分图匹配（König 定理与 Hall 婚姻定理），最后过渡到二人零和博弈；页眉与印页码不译。</span>

[[FIGURE: 书页 340, 一张从 source $s$ 到 sink $t$ 的有向图，每条边标有容量（如 7、21、8、17、6、4、5、3、2、10、14、15 等），虚线示意一个 cut。图的标题为 Figure V1.5，说明最大流 M 被任意割的容量所界定，由对偶性，最小割容量等于最大流：M=14。]]

```math
\text{Max flow problem（最大流问题）: Maximize } M \quad \text{with flow } y_j \le M_j
```

每条边上标出的就是容量 $M_j$。

由对偶性，minimum cut（最小割）的容量等于 maximum flow（最大流）：$M=14$。

先从源点向外发流。$s$ 的三条出边容量之和为 $7+2+8=17$。有没有比 $M\le 17$ 更紧的界？有——切过三条中间边的割容量只有 $6+4+5=15$，所以 $17$ 到不了汇点。有没有比 $M\le 15$ 更紧的界？有——切过靠后五条边的割容量只有 $3+2+4+3+2=14$，总流量 $M$ 不能超过 $14$。这个流量 $14$ 能否实现、这又是不是最紧的割？能，这就是 min cut（它其实是个 $\ell_1$ 问题！），由对偶性，$14$ 就是 max flow。

维基百科列出了一长串越来越快的算法来求解这个重要问题。它应用极广。如果各容量 $M_j$ 都是整数，那么最优流量 $y_j$ 也是整数。通常 integer program（整数规划）会格外困难，但这里不是。

有一种特殊的最大流问题，所有容量 $M_j=1$ 或 $0$。图是 bipartite（二分图）——所有边都从 part 1（第一部分）的节点指向 part 2（第二部分）的节点。我们在把 part 1 里的人匹配给 part 2 里的工作（每人至多一份工作、每份工作至多一人）。于是 maximum matching（最大匹配）$M$ = 图中的 max flow = 最多的 assign（分配）数。

这张二分图允许一个 perfect matching（完美匹配）$M=5$。若删去从 $2$ 向下到 $1$ 的那条边，则只剩下 $M=4$ 个分配可行，因为 $2$ 和 $5$ 只会胜任同一份工作（工作 $5$）。

对二分图而言，max flow = min cut 就是 König's theorem（柯尼希定理）和 Hall's marriage theorem（霍尔婚姻定理）。

## Person Games（双人博弈）

三人或更多人的博弈极难求解。玩家之间可以结盟对抗他人，而这些 alliances（同盟）是不稳定的，新联盟经常形成。直到 John Nash（约翰·纳什）才取得重大进展，并因此获得诺贝尔奖（经济学奖！）。

但二人零和博弈已被 von Neumann（冯·诺依曼）彻底解决。我们将看到它与线性规划及对偶的密切联系。

玩家是 X 和 Y。有一个 payoff matrix（收益矩阵）$A$。每一回合，玩家 X 选 $A$ 的一行，玩家 Y 选一列。$A$ 中该行该列处的那个数就是 payoff（收益），然后双方再进入下一回合。

<!-- page 343 -->

> <span style="color:#7f8c8d;">本页为书页 341，用一个 2×3 的小收益矩阵引出 saddle point（鞍点）与 mixed strategy（混合策略），并示范如何算出 X、Y 的最优混合策略及博弈值；页眉与印页码不译。</span>

为了与线性规划对上，我规定这笔支付从玩家 X 流向 Y。于是 X 想最小化，Y 想最大化。下面是一个很小的 payoff matrix，X 有两行可选，Y 有三列可选。

[[FIGURE: 书页 341, 左侧为 payoff matrix：两行三列，第一行 0、2、4，第二行 -1、4（列 3 处为 2，即第一行的 2 是该列最小、该行最大，构成 saddle point）；下方标注「2 是它所在列的最小值，也是它所在行的最大值」。右侧为新的 payoff matrix 及混合策略的推导图。]]

Y 喜欢第 3 列里那些大数字。X 看到那一列里最小的数是 $2$（在第 1 行）。双方都没有理由偏离这个简单策略：Y 选第 3 列、X 选第 1 行。这笔 $2$ 的支付从 X 流向 Y：

> $2$ 是它所在列的最小值，也是它所在行的最大值。

这是一个 saddle point（鞍点）。Y 别指望赢到比 $2$ 更多，X 也别指望输得比 $2$ 更少。因为谁都没有改变策略的 incentive（激励），所以每一局都会一样。最优策略 $x^{*}$ 和 $y^{*}$ 很明确：X 选第 1 行，Y 选第 3 列。

但若第 3 列发生变化，双方就得重新动脑筋了。

[[FIGURE: 书页 341, 新的 payoff matrix 推导：Y 的三列分别为 y1、y2、y3，X 的两行分别为 row1、row2。原始矩阵第二行含 -1、0、4，第一行含 1、3、2（对应左侧另一矩阵）。下方给出混合行：x1(row1)+x2(row2) = [-x1+3x2, 3x1-x2, 4x1+2x2]，并标注 c1、c2 的取值。]]

X 喜欢第 2 列里那些小的、有利的数，但 Y 绝不会选那一列。对 Y 而言第 3 列最好（最大），X 应反制选第 2 行（以免付 $4$）。可这时第 1 列对 Y 反而比第 3 列更好，因为在第 1 列赢 $3$ 比在第 3 列赢 $2$ 强。

你看到的是：Y 仍想要第 3 列，但有时必须走到第 1 列。同样地，X 必须采用 mixed strategy（混合策略）：以概率 $x_1$、$x_2$ 分别选第 1、2 行。每一回合的选择必须不可预测，否则对手就会加以利用。

于是对 X 的决策是两个概率 $x_1\ge 0$ 和 $x_2\ge 0$，且 $x_1+x_2=1$。这个混合策略给 payoff matrix 添了一行新行：

```math
x_1(\text{row 1}) + x_2(\text{row 2}) = \begin{bmatrix} -x_1 + 3x_2,\; 3x_1 - x_2,\; 4x_1 + 2x_2 \end{bmatrix}.
```

X 会选这些分数，使最坏（最大）的支付尽可能小。记住 $x_2=1-x_1$，这会在两个最大的支付相等时发生：

```math
-x_1 + 3x_2 = 4x_1 + 2x_2 \quad\Longrightarrow\quad -x_1 + 3(1-x_1) = 4x_1 + 2(1-x_1).
```

这个方程给出 $x_1=\tfrac{3}{4}$，$x_2=\tfrac{1}{4}$，于是 $x^{*}=(\tfrac{3}{4},\tfrac{1}{4})$。新的混合行是 $[2.5,\;2,\;2.5]$（依 OCR 数值，其中第二分量为 $\tfrac{3}{2}$ 与 $\tfrac{1}{2}$ 合成的 $2$，第三分量 $4\cdot\tfrac{3}{4}+2\cdot\tfrac{1}{4}=3.5$，此处以原文印出的 2.5 为准，待核）。

类似地，Y 会以概率 $y_1,y_2,y_3$ 分别选第 1、2、3 列，且 $y_1+y_2+y_3=1$。这个混合策略把 $A$ 的三列合成 Y 的一列新列：

```math
y_1(\text{column 1}) + y_2(\text{column 2}) + y_3(\text{column 3}) =
\begin{bmatrix} y_1 + 4y_3 \\ 3y_1 - y_2 + 2y_3 \end{bmatrix}.
```

<!-- page 344 -->

> <span style="color:#7f8c8d;">本页为书页 342，完成 Y 的最优混合策略并求出博弈值 2.5，随后介绍半定规划（SDP）：约束从线性（flat sides）推广到矩阵半正定（curved sides），并说明内点法在 SDP 中的优势及强对偶可能失效；页眉与印页码不译。</span>

Y 会选这些分数 $y_1+y_2+y_3=1$，使最坏（最小）的支付尽可能大。这发生在 $y_2=0$ 且 $y_3=1-y_1$ 时。两个混合支付相等：

```math
y_1 + 4y_3 = 3y_1 - y_2 + 2y_3 \quad\Longrightarrow\quad y_1 + 4(1-y_1) = 3y_1 + 2(1-y_1),
```

解得 $y_1=\tfrac{1}{2}$，$y_2=0$，$y_3=\tfrac{1}{2}$。新混合列的两个分量都是 $2.5$。这些最优策略把 $2.5$ 确定为博弈的 value（值）。采用混合策略 $y^{*}=(\tfrac{1}{2},0,\tfrac{1}{2})$ 和 $x^{*}=(\tfrac{3}{4},\tfrac{1}{4})$，玩家 X 能保证支付不超过 $2.5$，玩家 Y 能保证收入不低于 $2.5$。

我们找到了这个二人博弈的 saddle point（鞍点）——最优混合策略，其 minimax payoff（X 极小极大支付）$=$ maximin payoff（Y 极大极小支付）$=2.5$。

[[FIGURE: 书页 342, 一张表：行 1、行 2 及混合行 row1+row2，列 1、列 2、列 3 及混合列。混合行各项为 2.5、2、2.5（其中列 2 为 0.75），混合列为 2.5、2.5，与博弈值 2.5 对应。]]

Von Neumann（冯·诺依曼）的 minimax theorem（极小极大定理）为每一个 payoff matrix 都给出了解。它等价于线性规划的 duality theorem：$\min c^{T}x = \max y^{T}b$。

## Semidefinite Programming (SDP)（半定规划）

要最小化的成本仍是线性的 $c^{T}x$，但现在对 $x$ 的约束涉及 symmetric matrices（对称矩阵）$S$。给定 $S_0,\dots,S_n$，要求 $S(x)=S_0+x_1S_1+\cdots+x_nS_n$ 是 positive semidefinite（半正定的，或正定的）。幸运的是，这是一个凸的 $x$ 集合——两个半正定矩阵的平均仍是半正定的（只要把两个能量 $v^{T}Sv\ge 0$ 取平均即可）。

于是可行 $x$ 集合可以有 curved sides（曲面边），而不是 flat sides（平面边）：

```math
S_0 + x_1S_1 + x_2S_2 \succeq 0
```

当 $x_1\ge 0$ 且 $x_2\ge 1$ 时（依 OCR，此处约束原文残缺，推为对两个变量/两个矩阵的某半正定条件，待核）它是半正定的。

最小化 $S(x)$ 的最大 eigenvalue（特征值）也可以通过额外变量 $t$ 一并纳入：

```math
\text{Minimize } t \quad\text{so that } tI - S(x) \text{ is positive semidefinite}.
```

SDP 还能最小化最大的 singular value（奇异值）——即 $S(x)$ 的 $\ell_2$ 范数：

```math
\text{Minimize } t \quad\text{so that } \begin{bmatrix} tI & S(x) \\ S(x) & tI \end{bmatrix} \text{ is positive semidefinite}.
```

对这些以及大多数半定问题，内点法是最优选择。我们不再沿约束集边界绕行（像单纯形法解线性规划那样从角点到角点），而是穿过集合内部。本质上每次迭代都在解一个 least squares（最小二乘）问题——通常 5 到 50 次迭代。

和线性规划一样，也有一个 dual problem（对偶问题，一个最大化问题）。这个对偶的值总在原问题 $c^{T}x$ 的值之下。当我们在对偶中最大化、在 primal（原始问题）中最小化 $c^{T}x$ 时，希望两个答案相等。但对带矩阵不等式的半定规划而言，这可能不成立。

SDP 为那些此前看似过难的矩阵问题提供了一套求解方法。

<!-- page 345 -->

> <span style="color:#7f8c8d;">本页为书页 343，是 VI.3 的习题集 Problem Set VI.3（第 1–9 题），内容涵盖弱对偶、求角点、对偶问题、博弈策略、$\ell_1/\ell_2/\ell_\infty$ 范数约束与 SDP 的联系等；页眉与印页码不译。</span>

## Problem Set VI.3

**1.** 弱对偶中是否真的需要方程（3）里的约束 $x\ge 0$？单凭 $A^{T}y\le c$ 是否已足以证明 $(A^{T}y)^{T}x\le c^{T}x$？我不这么认为。

**2.** 设约束为 $x_1+x_2+2x_3=4$ 且 $x_1\ge 0$，$x_2\ge 0$，$x_3\ge 0$（依 OCR 残缺，推为等式约束加非负约束，待核）。求 $\mathbb{R}^3$ 中这个三角形的三个角点。哪个角点最小化成本 $c^{T}x=5x_1+3x_2+8x_3$？

**3.** 第 2 题的对偶是哪个关于 $y$ 的最大化问题？原始问题中的一条约束对应对偶问题中的一个未知量 $y$。解出这个对偶问题。

**4.** 设约束为 $x\ge 0$ 以及 $x_1+x_2+x_3+x_4=4$、$x_1-x_2+x_3-x_4=2$（依 OCR 残缺，待核）。四个未知量上有两条等式约束，所以一个像 $x=(0,6,0,4)$（依 OCR 残缺，待核）这样的角点有 $4-2=2$ 个零分量。另找一个角点，使 $x_2=0$、$x_4=0$（依 OCR，待核），并说明它的成本高于第一个角点。

**5.** 求 X 选择各行时的最优（最小化）策略，以及 Y 选择各列时的最优（最大化）策略。在这个最优极小极大点 $x^{*},y^{*}$ 处，从 X 到 Y 的支付是多少？

**6.** 若 $A^{T}=-A$（反对称 payoff matrix），为什么这对 X 和 Y 是一场公平博弈，且极小极大支付为零？

**7.** 设 payoff matrix 是一个对角矩阵 $\Sigma$，对角元为 $\sigma_1>\sigma_2>\cdots>\sigma_n$。X 和 Y 的最优策略是什么？

**8.** 把 $\ell_1$ 范数下的 $\|(x_1,x_2,x_3)\|_1\le 2$（依 OCR，待核）转换成八条线性不等式 $Ax\le b$。$\ell_\infty$ 范数下的约束 $\|x\|_\infty\le 2$ 也产生八条线性不等式。在 $\ell_2$ 范数下，$\|x\|_2\le 2$ 是二次不等式 $x_1^2+x_2^2+x_3^2\le 4$。但在 SDP 中这变成一条矩阵不等式 $XX^{T}\preceq 4I$。为什么约束 $XX^{T}\preceq 4I$ 等价于 $x^{T}x\le 4$？

**9.** Note Duality（对偶性）提供了一个重要选项：解原始问题还是解对偶问题。这也适用于机器学习中的优化，如这篇论文所示：

> F. Bach, *Duality between subgradient and conditional gradient methods*, SIAM Journal of Optimization 25 (2015) 115–129; arXiv:1211.6302.

<!-- page 346 -->

> <span style="color:#7f8c8d;">本页为书页 344，本页已进入 VI.4 节「Gradient Descent Toward the Minimum」，属另一节内容，此处仅作衔接，主体（梯度下降、导数与梯度定义、ReLU 的例子）不属 VI.3 范围；页眉与印页码不译。</span>

## VI.4 Gradient Descent Toward the Minimum（梯度下降走向最小值）

（本页属 VI.4 节开头，不属 VI.3，故不作 VI.3 的译注展开。仅指出衔接关系：VI.3 讲的线性规划 / 对偶 / SDP 是「带约束」的最优化，而 VI.4 转入「无约束光滑函数」的最小化，工具从单纯形法、内点法换成 gradient descent / 梯度下降。）

---

> <span style="color:#27ae60;">**译者注 1：为什么对偶问题要取 $A^{T}y\le c$ 这个「转置」方向，而不是别的？** 这是线性规划对偶里最容易让人迷惑的一点。原始（primal）问题是对 $x\in\mathbb{R}^n$ 求 $\min c^{T}x$、$Ax=b$、$x\ge 0$；它对偶是对 $y\in\mathbb{R}^m$ 求 $\max b^{T}y$、$A^{T}y\le c$。这里 $A$ 与 $A^{T}$ 互换、$b$ 与 $c$ 互换、等号约束换成不等式约束，正是 Lagrange 乘子法的自然结果：给等式约束 $Ax=b$ 引入乘子 $y$，拉格朗日量是 $c^{T}x+y^{T}(b-Ax)=b^{T}y+(c-A^{T}y)^{T}x$。当 $x\ge 0$ 时，要让对偶目标 $b^{T}y$ 成为原目标的合法下界，就必须有 $c-A^{T}y\ge 0$，即 $A^{T}y\le c$。所以「转置」不是人为规定，而是「要让 $y^{T}b\le c^{T}x$ 对一切可行 $x$ 成立」这一要求的直接产物——这正是弱对偶的证明核心。</span>

> <span style="color:#27ae60;">**译者注 2：最大流—最小割为什么是同一个「对偶」故事。** 最大流问题是一个线性规划：目标 $\max M$（即让源点流出的总量最大），约束是流量守恒 $A^{T}y=0$ 与每条边容量 $y_j\le M_j$，其中 $A$ 是图的关联矩阵。它的对偶，就是把每一条边上的容量上界都「折算」成一个割的代价：任何一个 $s$–$t$ 割，都把图切成两边，任何可行流都必须整体穿过这个割一次，因此流量 $M$ 不可能超过该割的总容量 $\sum_{j\in\text{cut}}M_j$。于是「最大流 $\le$ 任一割的容量」，再取所有割的最小值，就是强对偶要证的 $\max\text{flow}=\min\text{cut}$。书页 340 上的数字链正是这个思路的三次收紧：$17\to 15\to 14$，每换一个更「窄」的割，上界就往下压一档，直到压到 $14$ 且能用一条流量为 $14$ 的流真正实现为止。注意这里割的容量线性地依赖于指示各边是否被割的 0/1 变量，所以 min cut 本质上也是一个 $\ell_1$ 范数型问题。</span>

> <span style="color:#27ae60;">**译者注 3：为什么博弈的值是「两个线性表达式的交点」，以及它和强对偶是同一件事。** 在书页 341 的 2×3 例子中，X 采用混合策略 $x=(x_1,x_2)$ 后，其新行是 $x_1\cdot(\text{row 1})+x_2\cdot(\text{row 2})$，这个新行的三个分量都是 $x_1$ 的线性函数。X 的理性选择是「让三个分量的最大值尽量小」，而最大值的下界正是让其中最大的两个分量相等的那个点——因为线性函数族的逐点最大在折点（两线交点）处取最小。于是令 $-x_1+3x_2=4x_1+2x_2$，加上 $x_1+x_2=1$，解得 $x_1=\tfrac{3}{4}$。Y 侧同理，令两个混合分量相等得 $y_1=\tfrac{1}{2}$。两边算出的值都是 $2.5$，这不是巧合：X 的极小极大与 Y 的极大极小相等，正是 von Neumann minimax 定理的结论，而它等价于线性规划强对偶 $\min c^{T}x=\max b^{T}y$。可以说，博弈的 saddle point 就是对偶理论在「两个理性对手」身上的化身——一个在压，一个在抬，最后在同一个数上停住。</span>

> <span style="color:#27ae60;">**译者注 4：SDP 的「曲面边界」从何而来，以及为什么强对偶可能失效。** 线性规划里，约束 $Ax=b$、$x\ge 0$ 定义的可行集是凸多面体，边是平的（flat sides），所以最优解总能在角点找到，单纯形法就是沿这些角点爬。而半定规划要求 $S(x)\succeq 0$，即对称矩阵半正定；「半正定」这个条件是 $v^{T}S(x)v\ge 0$ 对一切 $v$ 成立，它给出的是一个凸但通常弯曲的集合（curved sides），典型例子就是书页 342 写的 $XX^{T}\preceq 4I$ 等价于 $x^{T}x\le 4$——一个球，没有角点。因为没有角点可爬，单纯形法失效，内点法反而合适：它穿过集合内部、每步解一个最小二乘。更重要的一点是：线性规划总满足强对偶（对偶间隙为零），但 SDP 在矩阵不等式情形下，原始最优值和对偶最优值之间可能出现正的 gap，强对偶不保证成立。这是从「线性/多面体」迈向「矩阵/曲凸体」时，对偶理论付出的代价，也是 SDP 比 LP 难的核心所在。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么"弱对偶"会成立，它在拿什么换什么：**</span> 这一节的核心是一对孪生问题：原问题（primal）是约束 $Ax \ge b,\ x \ge 0$ 下最小化 $c^T x$，对偶问题（dual）是约束 $A^T y \le c$ 下最大化 $y^T b$。所谓"弱对偶" $y^T b \le c^T x$，本质上不是一条新的代数结论，而是同一组数据 $A,b,c$ 被"重新排队"的结果：把 $y^T b$ 写成 $y^T (Ax)$（对可行 $x$ 有 $Ax \ge b$，再配合 $y \ge 0$），再把它重排为 $(A^T y)^T x$，最后用约束 $A^T y \le c$ 与 $x \ge 0$ 得到 $(A^T y)^T x \le c^T x$。也就是说，$y^T b$ 是 $c^T x$ 的一个**下界**，而这个下界来自"把原问题的每个约束 $Ax \ge b$ 用一个非负乘子 $y_j$ 加权相加"——这正是 Lagrange 乘子（Lagrange multiplier）在不等式约束下的角色，所以书中强调用 $y$ 而不用 $\lambda$，把它明确指认为对偶变量。弱对偶永远成立，不需要任何额外条件；真正需要证明的是"强对偶"——最大等于最小。这一对"上推 $y^T b$、下压 $c^T x$，最后在最优解处相遇"的图像，是理解后面 max flow–min cut 与博弈论价值（value of the game）的统一钥匙。

> <span style="color:#1e8449;">**[note] von Neumann minimax 定理与对偶定理为何是"同一件事"：**</span> 书中一句"Von Neumann's minimax theorem for games ... is equivalent to the duality theorem"是全节最深的连接，值得拆开。两人零和博弈里，X 选行、Y 选列，支付（payoff）是 $a_{ij}$，X 想最小化、Y 想最大化。若存在**纯策略**鞍点（saddle point），即某个 $a_{ij}$ 同时是它所在行的最大、所在列的最小，则双方都没动力偏离——这就是正文第一个 $2$ 的例子。但一般矩阵没有鞍点，于是引入**混合策略**（mixed strategy）：X 以概率 $x$ 选行、Y 以概率 $y$ 选列，期望支付变成 $x^T A y$。minimax 定理断言 $\max_y \min_x x^T A y = \min_x \max_y x^T A y$，双方的最优混合策略给出的价值 $v$ 唯一。把这个博弈写成线性规划，X 的问题是"在 $\sum x_i = 1,\ x \ge 0$ 下最小化一个上界 $t$，且 $A^T x \le t\, \mathbf{1}$"，Y 的问题正是它的对偶。于是"最小上界 = 最大下界"的强对偶恰好等价于"minimax = maximin"，一个经济学/博弈论命题与一个凸优化命题在 $v = \min c^T x = \max y^T b$ 处合流。这正是 $2.5$ 那个数值例子的由来：X 的混合策略 $\frac34,\frac14$ 与 Y 的 $\frac12,0,\frac12$ 使新行、新列的两个分量都变成 $2.5$，即鞍点，价值 $v = 2.5$。

> <span style="color:#1e8449;">**[note] max flow = min cut：一个靠"常识"就能算出的强对偶实例：**</span> 这一节把一个高度抽象的强对偶定理，落到一张可以"心算"的图上：源点 $s$ 到汇点 $t$ 的最大流（max flow）问题，约束是 Kirchhoff 电流定律 $A^T y = 0$（每个中间节点流入等于流出）加上每条边的容量上界 $y_j \le M_j$，其中 $A$ 是图的关联矩阵（incidence matrix）。书里用"逐层收紧上界"的方式示范了 min cut：先看 $s$ 出来的三条边，容量和 $7+2+8=17$，于是 $M \le 17$；但穿过中间三条边的割（cut）只有 $6+4+5=15$，更紧；再切过后面五条边，$3+2+4+3+2=14$，于是 $M \le 14$，而且 $14$ 确实可达——这个割就是最小割（min cut），由对偶定理知最大流 $M = 14$。这里的"常识"其实是弱对偶的一个具体化身：**任何一条割的容量都是任意可行流的上界**，因为从 $s$ 到 $t$ 的每一单位流都必须穿过该割的某一条边。于是"找最小割"就是在"找最紧的上界"，与"求最大流"这一强对偶等式互为表里。这条线索还通向组合数学：当图是二分图（bipartite graph）且容量取 $0/1$ 时，max flow = min cut 退化为 König 定理与 Hall 婚姻定理（marriage theorem）——线性规划的对偶性在"人—岗位匹配"里变成了一个纯粹的组合存在性判据。

---

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

---

> <span style="color:#7f8c8d;">本节说明：梯度下降是训练深度神经网络的基础，但面对海量样本与海量权重的经典最速下降代价过高且易过拟合；本节引出随机梯度下降（SGD，只取小批量样本）及其收敛性、权重平均，最后介绍 ADAM 等自适应方法，并以"泛化为何有效"收束全章。页眉与印页码不译。</span>

---

<!-- page 361 -->

> <span style="color:#7f8c8d;">本页为书页 359，属 VI.5 开头，说明经典梯度下降的两大困难并引入随机梯度下降的基本思想；页眉与印页码不译。</span>

梯度下降（gradient descent）是训练深度神经网络（deep neural network）的基础。它基于形如下式的一步迭代：

```math
c_{k+1} = c_k - s_k\,\nabla L(c_k).
```

这一步骤应当引导我们沿下坡方向走向使损失函数（loss function）$L(c)$ 对测试数据 $v$ 达到最小的那个点。但是对于拥有大量训练样本的大网络而言，这个算法（照现在这个样子）并不成功！

重要的是要识别出经典最速下降（steepest descent）的两个不同问题：

1. 在每一步下降中都计算 $\nabla L$——即总损失 $L$ 关于网络中所有权重 $c$ 的导数——代价太高。这个总损失把训练集中每个样本 $v_i$ 的单个损失 $\ell(x, v_i)$ 加在一起——在每一次计算 $L$ 时，可能要计算并累加数百万个彼此独立的损失。
2. 权重的数目甚至更多。因此对许多不同的权重取值 $c^{*}$ 都有 $\nabla L(c)=0$。其中一些取值在未见过的测试数据上可能给出糟糕的结果。学习函数（learning function）$F$ 可能无法"泛化（generalize）"。但随机梯度下降（stochastic gradient descent，SGD）确实能找到能够泛化的权重 $c^{*}$——即在来自相似总体的未见向量 $v$ 上也能成功的权重。

随机梯度下降在每一步只使用训练数据的一个"minibatch（小批量）"。随机选取 $B$ 个样本。用一个小批量取代全部训练数据的整批（full batch），就把 $L(c)=\sum_{i}\ell_i(c)$ 变成了只含 $B$ 个损失之和。这同时化解了上述两个困难。深度学习的成功就建立在下面这两个事实上：

1. 用反向传播（backpropagation）在 $B$ 个样本上计算 $\nabla L$ 快得多。通常 $B=1$。
2. 这个随机算法产生的权重 $c^{*}$ 在未见数据上同样成功。

第一点是清楚的：每一步的计算量大大减少了。第二点则是一个"奇迹"。对新数据泛化良好是一份礼物，研究者们一直在努力解释它。

我们可以描述大网络中权重优化的大图景。权重由训练数据决定。这些数据通常包含数千个样本。我们知道每个样本的"特征（features）"——也许是它的身高和体重，或它的形状和颜色，或（对一段文本样本而言）名词、动词和逗号的数目。这些特征进入每个样本对应的向量 $v$。我们使用一个 minibatch 的样本。并且对训练集中的每个样本，我们知道它是"猫还是狗"——或者这段文本是"诗还是散文"。我们寻找一个能分配合适权重的学习函数 $F$。于是对来自相似总体的 $v$，$F$ 输出正确的分类"猫"或"诗"。

我们把这个函数 $F$ 用于未识别的测试数据。测试数据的特征就是新的输入 $v$。$F$ 的输出将是正确的（？）分类——只要这个函数以能够泛化的方式学会了训练数据。

这里是来自经验的一个显著观察。我们不想把训练数据拟合得太完美。那样往往会过拟合（overfitting）。函数 $F$ 变得过度敏感——它记住了一切，却什么也没学到。SGD 的泛化能力，就是基于从训练数据学到的权重 $c$，对未见测试数据 $v$ 给出正确分类的能力。

---

<!-- page 362 -->

> <span style="color:#7f8c8d;">本页为书页 360，属 VI.5，以 60 次多项式拟合为例说明过拟合与早停，并给出三种损失函数；页眉与印页码不译。</span>

我把过拟合比作选择一个 60 次多项式去精确拟合 61 个数据点。它的 61 个系数 $a_0$ 到 $a_{60}$ 将完美地"学会"这些数据。但这个高次多项式会在数据点之间剧烈振荡。对于邻近点的测试数据，这个"完美拟合"的多项式会给出完全错误的答案。

因此训练神经网络（其含义是找到一个能从训练数据中学习并对测试数据泛化良好的函数）的一项基本策略就是 early stopping（早停）。机器学习需要知道何时该停下！也许人类的学习也是如此。

**损失函数与学习函数**

现在我们建立网络将要求解的优化问题。我们需要定义我们的函数将（近似）最小化的"损失"$L(c)$。它是把每个训练数据向量 $v$ 分类时误差的总和。我们还需要描述对每个数据向量 $v$ 分类的学习函数 $F$ 的形式。

在机器学习之初，函数 $F$ 是线性的——这是一个严重的局限。现在 $F$ 当然是非线性的。仅仅是在每层每个神经元处引入一个特定的非线性函数，就已经带来了戏剧性的差异。事实证明，有了数千个样本，函数 $F$ 就能被正确训练。

正是计算机的处理能力带来了对数据的快速运算。尤其是我们依赖 GPU（graphical processing units，图形处理单元，最初为电脑游戏开发）的速度。它们使深度学习成为可能。

我们先选择一个要最小化的损失函数。然后描述随机梯度下降。梯度由网络架构决定——即那些我们待优化的权重的"前馈（feedforward）"步骤。本节的目标是找到适用于非常大问题的优化算法。然后第七章将描述架构与算法如何使学习函数获得成功。

下面是三种损失函数——cross-entropy（交叉熵）是神经网络的最爱。第 VII.4 节将描述交叉熵损失相对平方损失（如最小二乘法中那样）的优势。

1. 平方损失（square loss）：

```math
L(c)=\frac12 \sum_{i}\bigl\|F(c,v_i)-\text{true}_i\bigr\|^2
```

（对训练样本 $v_i$ 求和）

2. 合页损失（hinge loss）：

```math
L(c)=\sum_{i}\max\bigl(0,\,1-t_i\,F(c,v_i)\bigr)
```

（用于分类，$t_i$ 为 $1$ 或 $-1$）

3. 交叉熵损失（cross-entropy loss）：

```math
L(c)=-\sum_{i}\bigl[Y_i\log \hat{y}_i+(1-Y_i)\log(1-\hat{y}_i)\bigr]
```

（$Y_i$ 为 $0$ 或 $1$）

Cross-entropy loss（交叉熵损失）或"logistic loss（逻辑损失）"是逻辑回归（logistic regression，只有两个选项）的首选。真实标签 $Y_i=0$ 或 $1$（也可能取 $-1$ 或 $1$），而 $\hat{y}_i$ 是计算出的标签。

对于大小为 $B$ 的 minibatch，把 $N$ 换成 $B$，并随机选取这 $B$ 个样本。

> <span style="color:#27ae60;">**译者注 1（损失函数与"总损失=逐样本损失之和"的机制）**：这三条公式的公共骨架是"把每个样本的误差加起来再平均/求和"。平方损失把预测 $F(c,v_i)$ 与真实标签 $\text{true}_i$ 的欧氏距离平方累加，等价于最小二乘（least squares）里的 $\|Ac-b\|^2$；hinge loss 只有当 $t_i F(c,v_i)\ge 1$（分类正确且留有间隔）时取 0，否则按越界程度惩罚，它在支持向量机里迫使分类边界留下最大间隔；cross-entropy 则是从信息论来的——若真实标签为 1，$-Y_i\log\hat y_i$ 惩罚 $\hat y_i$ 偏低，若真实标签为 0，$-(1-Y_i)\log(1-\hat y_i)$ 惩罚 $\hat y_i$ 偏高，它把"预测概率偏离真实分布"的 KL 散度当作损失。这三者共享同一个梯度下降框架，区别只在单个样本损失 $\ell_i$ 的表达式不同，从而 $\nabla L=\sum_i\nabla\ell_i$ 的每一项不同。这就是为什么后面讲 SGD 时只需说"只取 $B$ 个样本的 $\nabla\ell_i$ 求和"，而与具体用哪种损失无关。</span>

---

<!-- page 363 -->

> <span style="color:#7f8c8d;">本页为书页 361，属 VI.5，讨论每步一个样本的随机下降、epoch 与 semi-convergence（半收敛）；页眉与印页码不译。</span>

**每步一个样本的随机下降**

为简化起见，假设每个 minibatch 只含一个样本 $v_k$（于是 $B=1$）。该样本被随机选取。随机下降的理论通常假设样本用后放回（replacement）——原则上该样本在第 $k+1$ 步仍可能被再次选中。但与"先把样本随机排序"相比，放回的开销更大。实践中我们常省略放回，而是按随机顺序遍历样本。

对训练数据的一次完整遍历就是下降算法的一个 epoch（轮次）。普通梯度下降每步计算一个 epoch（即批处理模式，batch mode）。随机梯度下降则需要许多步（针对各 minibatch）。实践中的建议是取 $B<32$。

随机下降始于 Herbert Robbins 与 Sutton Monro 的开创性论文，载于 *Annals of Mathematical Statistics* **22** (1951) 400–407：*A Stochastic Approximation Method*（随机逼近方法）。他们的目标是一种以概率收敛到 $c^{*}$ 的快速方法：

要证明当 $k\to\infty$ 时，$\operatorname{Prob}(\|c_k-c^{*}\|>\varepsilon)$ 趋于零。

随机下降比全梯度下降对步长 $s_k$ 更敏感。若在第 $k$ 步随机选择样本，则第 $k$ 个下降步骤是我们熟悉的：

```math
c_{k+1}=c_k-s_k\,\nabla_c \ell(c_k, v_k),\qquad \nabla_c\ell=\text{样本 }v_k\text{ 的损失项的导数}.
```

每步的工作量少得多（$B$ 个输入而非训练集的全部输入）。但我们未必收敛得更慢。随机梯度下降的一个典型特征是"semi-convergence（半收敛）"：一开始收敛很快。

SGD 的早期步骤往往比 GD 更快地收敛到解 $c^{*}$。这对深度学习非常有利。第 VI.4 节展示了全批处理模式的 zig-zag（之字形）现象，通过加上来自上一步的 momentum（动量）得到了改善（对 SGD 也可这样做）。另一种改进常来自使用诸如某种 ADAM 变体之类的 adaptive（自适应）方法。自适应方法比动量回看得更远——现在之前所有下降方向都被记住并使用。这些在本节后面再讲。

这里我们暂停一下，来看 semi-convergence：随机梯度下降的快启动。我们立即承认，SGD 后期的迭代常常是飘忽不定的。开始时的收敛会在接近解时变成大幅振荡。图 VI.10 将展示这一点。一种应对办法是早停，从而避免对数据过拟合。

在下面的例子中，解 $c^{*}$ 落在某个特定的区间 $I$ 内。若当前近似 $c_k$ 在 $I$ 之外，则下一个近似更接近 $I$（或落入 $I$ 内）。这给出 semi-convergence——一个良好的开端。但最终 $c_k$ 会在 $I$ 内来回跳动。

---

<!-- page 364 -->

> <span style="color:#7f8c8d;">本页为书页 362，属 VI.5，以 $n=1$ 的最小二乘为例严格推导"快启动"区间，并配图 VI.10；页眉与印页码不译。</span>

**起点的快速收敛：$n=1$ 的最小二乘**

我们从 Suvrit Sra 那里学到：最简单的例子就是最好的例子。向量 $c$ 只有一个分量 $c$。第 $i$ 个损失是 $\ell_i(c)=\tfrac12(a_i c-b_i)^2$，其中 $a_i>0$。$\ell_i$ 的梯度就是它的导数 $a_i(a_i c-b_i)$。它在 $c=b_i/a_i$ 处为零，$\ell_i$ 在该处最小。全部 $N$ 个样本的总损失为

```math
L(c)=\sum_{i}(a_i c-b_i)^2
```

——即 $N$ 个方程、$1$ 个未知量的最小二乘。

要求解的方程是 $\nabla L=\sum_{i} a_i(a_i c-b_i)=0$。其解为

```math
c^{*}=\frac{\sum_{i} a_i b_i}{\sum_{i} a_i^2}. \tag{1}
```

**重要**：若 $B/A$ 是比值 $b_i/a_i$ 中的最大者，则真解 $c^{*}$ 低于 $B/A$。这由下面一行四个不等式推出：

```math
\frac{\sum_i a_i b_i}{\sum_i a_i^2}\ \le\ \frac{B}{A}\cdot\frac{\sum_i a_i b_i}{\sum_i a_i^2}\ \ ?\ \ \frac{B}{A}. \tag{2}
```

（$\sum_i a_i b_i\le (B/A)\sum_i a_i^2$，因为逐项 $a_i b_i\le (B/A)a_i^2$ 等价于 $b_i/a_i\le B/A$）

同理，$c^{*}$ 高于最小的比值 $\beta/\alpha$。**结论**：若 $c_k$ 在从 $\beta/\alpha$ 到 $B/A$ 的区间 $I$ 之外，则第 $k$ 个梯度下降步骤将朝着包含 $c^{*}$ 的那个区间 $I$ 移动。下面是我们对随机梯度下降可以期待的：

- 若 $c_k$ 在 $I$ 之外，则 $c_{k+1}$ 向区间 $\beta/\alpha\le c\le B/A$ 移动。
- 若 $c_k$ 在 $I$ 之内，则 $c_{k+1}$ 也在其中。迭代会在 $I$ 内来回弹跳。

用随机梯度下降最小化 $\|Ac-b\|^2$ 所得到的一个典型序列 $c_0,c_1,c_2,\dots$ 画在图 VI.10 中。你看到快启动和振荡收尾。这种行为正是"在振荡开始时考虑早停或平均（第 365 页）"的完美信号。

[[FIGURE: 书页 362, 图 VI.10 随机梯度下降的轨迹与代价函数。左图展示两个未知量时 SGD 的轨迹：早期迭代成功、后期振荡（如插图中所示）；右图为二次代价函数先迅速下降、继而波动而非收敛。四条路径从同一 $c_0$ 出发，对式 (3) 中的 $i$ 做随机选取。40×2 矩阵 $A$ 的条件数仅为 8.6。]]

---

<!-- page 365 -->

> <span style="color:#7f8c8d;">本页为书页 363，属 VI.5，说明随机 Kaczmarz 就是 $Ac=b$ 的 SGD，并列出相关文献；页眉与印页码不译。</span>

**随机 Kaczmarz 就是 $Ac=b$ 的随机梯度下降**

带随机指标 $i(k)$ 的 Kaczmarz：

```math
c_{k+1}=c_k-\frac{a_i^{\mathsf T}c_k-b_i}{\|a_i\|^2}\,a_i. \tag{3}
```

我们在第 $k$ 步随机选取 $A$ 的第 $i$ 行。我们在调整 $c$ 以解出 $Ac=b$ 中的第 $i$ 个方程。（把式 (3) 左乘 $a_i^{\mathsf T}$ 即可验证 $a_i^{\mathsf T}c_{k+1}=b_i$，这正是 $Ac=b$ 中的第 $i$ 个方程。）从几何上看，$c_{k+1}$ 是 $c_k$ 向在 $c^{*}$ 处相交的诸超平面 $a_i^{\mathsf T}c=b_i$ 之一的投影。

这个算法多年来一直难以被严密分析。方程 $a_1^{\mathsf T}c=b_1,\ a_2^{\mathsf T}c=b_2,\dots$ 以循环顺序取用，步长为 $1$。后来 Strohmer 与 Vershynin 证明了随机 Kaczmarz 的快速收敛。他们使用了带 norm-squared sampling（范数平方抽样，即重要性抽样）的 SGD，如第 II.4 节所述：以与 $\|a_i\|^2$ 成比例的概率选取 $A$ 的第 $i$ 行。

上一页描述了当 $A$ 为 $N\times 1$ 时 $Ac=b$ 的 Kaczmarz 迭代。序列 $c_0,c_1,c_2,\dots$ 移向区间 $I$，最小二乘解就在该区间内。对于 $N\times K$ 的矩阵 $A$，我们期望这些 $K\times 1$ 向量移入围绕 $c^{*}$ 的一个 $K$ 维盒内。图 VI.10 对 $K=2$ 展示了这一点。

下一页将给出随机梯度下降的数值实验：Gower 与 Richtarik 发展了随机 Kaczmarz 的一种变体，给出了不下六种等价的随机化解释。下面这些参考文献把诸多变体与 Kaczmarz 在 1937 年 *Bulletin de l'Académie Polonaise* 上的原始工作联系起来：

1. T. Strohmer and R. Vershynin, *A randomized Kaczmarz algorithm with exponential convergence*, Journal of Fourier Analysis and Applications **15** (2009) 262–278.
2. A. Ma, D. Needell, and A. Ramdas, *Convergence properties of the randomized extended Gauss-Seidel and Kaczmarz methods*, arXiv:1503.08235v3, 1 Feb 2018.
3. D. Needell, N. Srebro, and R. Ward, *Stochastic gradient descent, weighted sampling, and the randomized Kaczmarz algorithm*, Math. Progr. **155** (2015) 549–573.
4. R. M. Gower and P. Richtarik, *Randomized iterative methods for linear systems*, SIAM J. Matrix Analysis **36** (2015) 1660–1690; arXiv:1506.03296v5, 6 Jan 2016.
5. L. Bottou et al., in *Advances in Neural Information Processing Systems*, NIPS 16 (2004) and NIPS 20 (2008), MIT Press.
6. S. Ma, R. Bassily, and M. Belkin, *The power of interpolation: Understanding the effectiveness of SGD in modern over-parametrized learning*, arXiv:1712.06559.
7. S. Reddi, S. Sra, B. Poczos, and A. Smola, *Fast stochastic methods for nonsmooth nonconvex optimization*, arXiv:1605.06900, 23 May 2016.

---

<!-- page 366 -->

> <span style="color:#7f8c8d;">本页为书页 364，属 VI.5，推导随机 Kaczmarz 的投影误差公式与 Strohmer–Vershynin 期望误差界，并配图 VI.11；页眉与印页码不译。</span>

**随机 Kaczmarz 与迭代投影**

设 $Ac^{*}=b$。随机 Kaczmarz 的典型一步是把当前误差 $c_k-c^{*}$ 投影到超平面 $a_i^{\mathsf T}c=b_i$ 上。这里 $i$ 在第 $k$ 步被随机选取（常以与 $\|a_i\|^2$ 成比例的概率做重要性抽样）。为看出那个投影矩阵为 $a_i a_i^{\mathsf T}/\|a_i\|^2$，把 $b_i=a_i^{\mathsf T}c^{*}$ 代入更新步骤 (3)：

```math
c_{k+1}-c^{*}=\Bigl(I-\frac{a_i a_i^{\mathsf T}}{\|a_i\|^2}\Bigr)(c_k-c^{*}). \tag{4}
```

正交投影从不增加长度。误差只会减小。误差范数 $\|c_k-c^{*}\|$ 稳步下降，即使代价函数 $\|Ac_k-b\|$ 并不下降。但收敛通常很慢！Strohmer–Vershynin 估计期望误差：

```math
\mathbb{E}\bigl[\|c_{k+1}-c^{*}\|^2\bigr]\ \le\ \Bigl(1-\frac{1}{\kappa^2}\Bigr)\,\|c_k-c^{*}\|^2,\qquad \kappa=\text{矩阵 }A\text{ 的条件数}. \tag{5}
```

与梯度下降相比这很慢（那里 $\kappa^2$ 被替换为 $\kappa$，再配合 VI.4 的动量则更佳）。但 (5) 与 $A$ 的规模无关——这对大规模问题很有吸引力。

交替投影（alternating projections）理论由 von Neumann（在 Hilbert 空间中）开创。参见 Bauschke–Borwein、Escalante–Raydan、Diaconis、Xu 的著作与论文。

我们的实验收敛得很慢！$100\times 10$ 的矩阵 $A$ 是随机的，$\kappa\approx 400$。图中展示了随机 Kaczmarz 的 $600{,}000$ 步。我们用第 $k$ 步被选中的行与 $c_k-c^{*}$ 之间的夹角 $\theta_k$ 来度量收敛。误差方程 (4) 变为：

```math
\|c_{k+1}-c^{*}\|^2=\bigl(1-\cos^2\theta_k\bigr)\,\|c_k-c^{*}\|^2. \tag{6}
```

图中显示那些数值 $1-\cos^2\theta_k$ 非常接近 $1$：收敛缓慢。但第二张图确认收敛确实发生。Strohmer–Vershynin 界 (5) 变成 $\mathbb{E}[\cos^2\theta_k]\ge 1/\kappa^2$。我们的例子矩阵有 $1/\kappa^2\approx 10^{-5}$，常常 $\cos^2\theta_k\approx 10^{-5}$，这印证了该界。

[[FIGURE: 书页 364, 图 VI.11 随机 Kaczmarz 的平方误差收敛。式 (6) 中 $1-\cos^2\theta_k$ 接近 $1-10^{-5}$，造成下图中 $600{,}000$ 次迭代的缓慢收敛；上图为 $1-\cos^2\theta_k$ 随迭代的取值。]]

---

<!-- page 367 -->

> <span style="color:#7f8c8d;">本页为书页 365，属 VI.5，给出 SGD 的期望收敛证明（Sra 定理）与随机权重平均 SWA；页眉与印页码不译。</span>

**期望意义下的收敛**

对于像 SGD 这样的随机算法，我们需要一个把随机性考虑在内的收敛证明——既在假设中，也在结论中。Suvrit Sra 为我们提供了这样一个证明，这里把它复述出来。函数 $f(c)$ 是 $n$ 项之和 $\sum_i f_i(c)$。抽样在第 $k$ 步从 $1$ 到 $n$ 中均匀地选取 $i(k)$（**有放回**！），步长取 $s_k=c/\sqrt{T}$（常数 $c$ 除以 $\sqrt{T}$）。先给出关于 $f(c)$ 与 $\nabla f(c)$ 的假设，然后是随机抽样的一条标准要求（无偏，no bias）：

1. $\nabla f$ 的 Lipschitz smoothness（Lipschitz 光滑性）：$\|\nabla f(c)-\nabla f(y)\|\le L\|c-y\|$。
2. 梯度有界：$\|\nabla f_i(c)\|\le G$。
3. 随机梯度无偏（unbiased）：$\mathbb{E}\bigl[\nabla f_{i(k)}(c)\bigr]=\nabla f(c)$。

由假设 1 可得：

```math
f(c_{k+1})\le f(c_k)+\langle\nabla f(c_k),\,c_{k+1}-c_k\rangle+\tfrac{L}{2}\|c_{k+1}-c_k\|^2,
```

进而

```math
f(c_{k+1})\le f(c_k)+\langle\nabla f(c_k),\,-s_k\nabla f_{i(k)}(c_k)\rangle+\tfrac12 Ls_k^2\|\nabla f_{i(k)}(c_k)\|^2.
```

现在对两边取期望并用假设 2、3：

```math
\mathbb{E}[f(c_{k+1})]\le \mathbb{E}[f(c_k)]-s_k\|\nabla f(c_k)\|^2+\tfrac12 Ls_k^2 G^2.
```

整理得：

```math
s_k\|\nabla f(c_k)\|^2 \le \mathbb{E}[f(c_k)]-\mathbb{E}[f(c_{k+1})]+\tfrac12 Ls_k^2 G^2. \tag{7}
```

取步长 $s_k=c/\sqrt{T}$，并把 (7) 从 $k=1$ 加到 $T$。求和得到 telescoping（望远镜式消去）：

```math
\frac{1}{T}\sum_{k=1}^{T}\|\nabla f(c_k)\|^2 \le \frac{f(c_1)-f(c^{*})}{c\sqrt{T}}+\frac{Lc\,G^2}{2\sqrt{T}}. \tag{8}
```

这里 $f(c^{*})$ 是全局最小值。(8) 中的最小项低于平均值：

```math
\min_{1\le k\le T}\|\nabla f(c_k)\|^2 \le \frac{f(c_1)-f(c^{*})}{c\sqrt{T}}+\frac{Lc\,G^2}{2\sqrt{T}} = O\Bigl(\frac{1}{\sqrt{T}}\Bigr). \tag{9}
```

Sra 定理的结论是：以次线性速率（sublinear rate）按期望收敛。

**SGD 内部的权重平均**

把随机梯度下降若干步的输出取平均，这个想法看起来很诱人。学习率（learning rate，即步长）可以恒定，也可以在每一组输出上循环变化。Gordon Wilson 等人把这一方法命名为 Stochastic Weight Averaging（SWA，随机权重平均）。他们强调，这对训练深度网络给出了很有希望的结果，泛化更好、几乎无额外开销。这看起来自然且有效。

P. Izmailov, D. Podoprikhin, T. Garipov, D. Vetrov, A. Gordon Wilson, *Averaging weights leads to wider optima and better generalization*, arXiv:1803.05407.

> <span style="color:#27ae60;">**译者注 2（期望收敛证明里"拿什么换什么"）**：这段证明的精髓是一次"确定性下降 + 无偏噪声"的账目平衡。光滑性假设 1 给出的是二阶项 $\tfrac12 Ls^2\|\nabla f_{i(k)}\|^2$——这是随机性引入的"代价"，因为 $i(k)$ 是随机的，下降方向 $\nabla f_{i(k)}$ 与真实梯度 $\nabla f$ 不一致。真正的一阶收益是 $-s_k\|\nabla f(c_k)\|^2$，它靠的是无偏假设 3：$\mathbb{E}[\langle\nabla f,\nabla f_{i(k)}\rangle]=\|\nabla f\|^2$，于是随机方向的期望内积"换回"了真实梯度的范数平方。两边取期望后，噪声项变成确定性的 $+\tfrac12 Ls_k^2G^2$（有界假设 2 把随机范数压成常数 $G^2$）。取 $s_k\propto 1/\sqrt{T}$ 是让"一阶收益与噪声"在求和后达到平衡的最优选择：收益按 $\sum s_k\sim c\sqrt{T}$ 累积，噪声按 $\sum s_k^2\sim c^2$ 累积，两者相除得 $1/\sqrt{T}$ 的次线性速率。这正是 (9) 里 $O(1/\sqrt{T})$ 的来源——它比 GD 的线性收敛慢，但换来的是每步只算一个（或 $B$ 个）样本的梯度，这正是 SGD 用"单步廉价"换"总步数略多"的核心权衡。</span>

---

<!-- page 368 -->

> <span style="color:#7f8c8d;">本页为书页 366，属 VI.5，介绍利用历史梯度的自适应方法 ADAGRAD 与 ADAM 的递推式；页眉与印页码不译。</span>

**利用历史梯度的自适应方法**

为了更快地收敛梯度下降与随机梯度下降，自适应方法（adaptive methods）一直是一个重要方向。其思想是利用来自较早步骤的梯度。这个"记忆"指导搜索方向 $D$ 的选择以及至关重要的步长 $s$。

我们要找的是使指定损失函数 $L(c)$ 最小的向量 $c^{*}$。在从 $c_k$ 到 $c_{k+1}$ 的一步中，我们可以自由选择 $D_k$ 与 $s_k$：

```math
D_k=D(\nabla L_k,\,\nabla L_{k-1},\dots),\qquad c_{k+1}=c_k-s_k D_k,\qquad s_k=s(\nabla L_k,\dots). \tag{10}
```

对于标准的 SGD 迭代，$D_k$ 只依赖当前梯度 $\nabla L_k$（而 $s_k$ 可能取 $s/\sqrt{k}$）。那个梯度 $\nabla L_k(c_k,B)$ 只在测试数据的一个随机 minibatch $B$ 上求值。现在，深度网络常可选择使用部分或全部较早的梯度（在较早的随机 minibatch 上算出）：

```math
c_{k+1}=c_k-s_k D_k. \tag{11}
```

**自适应随机梯度下降**

成败取决于 $D_k$ 与 $s_k$。第一个自适应方法（称为 ADAGRAD）选择通常的搜索方向 $D_k=\nabla L(c_k)$，但从所有先前梯度计算步长 [Duchi–Hazan–Singer]：

```math
\text{ADAGRAD 步长：}\quad s_k=\alpha\Bigl[\sum_{j=1}^{k}\operatorname{diag}\bigl(\nabla L_j\nabla L_j^{\mathsf T}\bigr)\Bigr]^{-1/2}. \tag{12}
```

$\alpha/\sqrt{k}$ 是在证明随机下降收敛时典型的递减步长。它在实践中常因拖慢收敛而被略去。(12) 中的"memory factor（记忆因子）"带来了收敛速度上的真实提升。这些提升使自适应方法成为进一步开发的重点。

ADAM [Kingma–Ba] 中的指数滑动平均（exponential moving average）已经成为主流。与 (12) 不同，近期的梯度 $\nabla L$ 在 $s_k$ 与步骤方向 $D_k$ 中的权重都大于较早的梯度。$D$ 与 $s$ 中的指数权重来自 $\delta<1$ 与 $\beta<1$：

```math
m_k=(1-\delta)\sum_{j}\delta^{\,k-j}\,\nabla L(c_j),\qquad s_k=\alpha\,\Bigl[\sum_{j}\beta^{\,k-j}\operatorname{diag}\bigl(\nabla L_j\nabla L_j^{\mathsf T}\bigr)\Bigr]^{-1/2}. \tag{13}
```

典型取值是 $\delta=0.9$ 与 $\beta=0.999$。$\delta$、$\beta$ 取值过小会有效地扼杀滑动记忆，丧失自适应方法在收敛速度上的优势。这个速度在梯度下降的总代价中很重要！方向 $D_k$ 的回看（look-back）公式，就如同在 VI.4 节的 heavy ball method（重球法）中加入动量。

$D_k$ 与 $s_k$ 的实际计算将是旧值与新值的递推组合：

```math
s_k=\beta s_{k-1}+(1-\beta)\|\nabla L(c_k)\|^2,\qquad D_k=\delta D_{k-1}+(1-\delta)\nabla L(c_k). \tag{14}
```

在若干课程项目中，这个自适应方法明显产生了更快的收敛。

---

<!-- page 369 -->

> <span style="color:#7f8c8d;">本页为书页 367，属 VI.5，讨论 ADAM 的缺陷与 YOGI，并列出参考文献、收束全章；页眉与印页码不译。</span>

ADAM 在实践中非常流行（本文写于 2018 年）。但若干作者指出了它的缺陷。Hardt、Recht 与 Singer 构造了例子，表明深度学习中权重的极限 $c_{\infty}$ 可能是成问题的：收敛可能失败，或者（更糟）极限权重在应用到未见测试数据时可能泛化得很差。

式 (13)–(14) 依循了 Reddi、Kale 与 Kumar 近期的会议论文。这些作者证明了 ADAM 的非收敛性，给出简单例子，其中步长 $s_k$ 随时间增大——一个不受欢迎的结果。在他们的例子中，ADAM 每三步中有两步走错方向、只有一步走对。指数衰减把那个"好"步骤缩得太小，总体上步长 $s_k$ 并不下降。需要一个较大的 $\beta$（接近 1）并被采用，但总存在 ADAM 会失败的凸优化问题。这个思想仍然是好的。

一种做法是使用递增的 minibatch 大小 $B$。NIPS 2018 论文提出了一个新的自适应算法 YOGI，它能更好地控制学习率（步长）。与 ADAM 相比，关键改动在于改用 additive update（加性更新）；其他步骤不变。此刻，实验显示 YOGI 的结果有所改善。

而在快速收敛到近似满足 $\nabla L(c)=0$ 的权重之后，仍有那个关键问题：为什么这些权重对未见测试数据泛化良好？

**参考文献**

1. S. Ruder, *An overview of gradient descent optimization algorithms*, arXiv:1609.04747.
2. J. Duchi, E. Hazan, and Y. Singer, *Adaptive subgradient methods for online learning and stochastic optimization*, J. of Machine Learning Research **12** (2011) 2121–2159.
3. P. Kingma and J. Ba, *ADAM: A method for stochastic optimization*, ICLR, 2015.
4. M. Hardt, B. Recht, and Y. Singer, *Train faster, generalize better: Stability of stochastic gradient descent*, arXiv:1509.01240, 7 Feb 2017, Proc. ICML (2016).
5. A. Wilson, R. Roelofs, M. Stern, N. Srebro, and B. Recht, *The marginal value of adaptive gradient methods in machine learning*, arXiv:1705.08292, 23 May 2017.
6. S. Reddi, S. Kale, and S. Kumar, *On the convergence of ADAM and beyond*, ICLR 2018: Proc. Intl. Conference on Learning Representations.
7. S. Reddi, M. Zaheer, D. Sachan, S. Kale, and S. Kumar, *Adaptive methods for nonconvex optimization*, NIPS (2018).

我们以强调作结：随机梯度下降如今是寻找使损失 $L(c)$ 最小、即求解 $\nabla L(c^{*})=0$ 的权重 $c$ 的首要方法。由 SGD 得到的这些权重通常在未见测试数据上也能成功。

> <span style="color:#27ae60;">**译者注 3（ADAM 指数滑动平均与 VI.4 动量是同一件事的两个版本）**：ADAM 的式 (14) 拆开看，$D_k=\delta D_{k-1}+(1-\delta)\nabla L(c_k)$ 就是第 VI.4 节 heavy ball 方法的动量项——方向沿历史梯度做指数加权平均，$\delta$（0.9 附近）是"记住多少历史"的折现率；$s_k=\beta s_{k-1}+(1-\beta)\|\nabla L(c_k)\|^2$ 则对梯度**平方**做同样的指数滑动平均，用来按"每个坐标历史上变化多大"来缩放步长——变化大的坐标步长自动缩小、变化小的坐标步长放大。二者的差别只是把动量里的"一阶量 $\nabla L$"换成"二阶量 $\nabla L\nabla L^{\mathsf T}$"。这解释了为什么 $\beta$ 要取 0.999 这样接近 1 的值：它对应数千步的有效记忆窗口（$1/(1-\beta)\approx 1000$ 步），而 $\delta=0.9$ 只约 10 步。也正因这个长记忆，Reddi–Kale–Kumar 才能构造出 ADAM 步长反而增大的反例——当最近几步都是小梯度时，长记忆里的历史小平方让 $s_k$ 的分母持续偏小，于是步长不降反升，最终导致在光滑凸问题上也不收敛。</span>

---

<!-- page 370 -->

> <span style="color:#7f8c8d;">本页为书页 368，属 VI.5，讨论泛化为何有效及随机打乱输入实验，并联系到 CT 成像中的 Kaczmarz；页眉与印页码不译。</span>

**泛化：深度学习为何如此有效？**

我们以对一个深度学习核心问题的简短讨论结束第六章——并衔接第七章。这里的问题是泛化（generalization）。它指的是神经网络在未见的测试数据上的行为。如果我们构造出一个能成功分类已知训练数据 $v$ 的函数 $F(c,v)$，那么当 $v$ 在训练集之外时，$F$ 还能继续给出正确结果吗？

答案必然在于选择权重的那个随机梯度下降算法。这些权重 $c$ 在训练数据上最小化损失函数 $L(c,v)$。问题是：为什么算出来的权重在测试数据上表现得这么好？

通常 $c$ 中的自由参数比 $v$ 中的数据更多。此时我们可以预期有许多组权重（许多向量 $c$）在训练集上同样精确。这些权重可能好也可能坏，可能泛化良好也可能泛化很差。我们的算法选出一个特定的 $c$，并把这些权重应用到新数据 $v_{\text{test}}$ 上。

一个不寻常的实验产生了出乎意料的正面结果。每个输入向量 $v$ 的各分量被随机打乱，于是 $v$ 所表示的各个特征突然失去了意义。然而深度神经网络仍学会了这些随机化样本，学习函数 $F(c,v)$ 仍正确分类了测试数据。当然，当 $v$ 的分量被重新排序时，$F$ 无法在未见数据上成功。

优化问题的一个常见特征是：光滑函数比不规则函数更容易近似。但这里，对于完全随机化的输入向量，随机梯度下降只需要三倍的 epoch（三倍的迭代次数）就学会了训练数据。这种对训练样本的随机标注（该实验已广为人知）描述于 arXiv:1611.03530。

**层析成像（CT）中的 Kaczmarz 方法**

Kaczmarz 的一个关键性质是它在早期迭代中的快速成功。这在层析成像（tomography）中被称为 semi-convergence（半收敛）——其中求解 $Ac=b$ 构造出一幅 CT 图像，且该方法在数据有噪声时产生一个正则化解（regularized solution）。对含噪数据而言，快速的 semi-convergence 对这样一个简单方法来说是极好的性质。最初几步都逼近从 $\alpha/\rho$ 到 $A/B$ 的正确区间（针对一个标量未知量）。但进入该区间之后，Kaczmarz 就不起眼地跳来跳去。

我们在这里进入了不适定反问题（ill-conditioned inverse problems）这个庞大的主题（参见 P. C. Hansen 的著作）。在本书中，我们只能打开这扇门。

---

<!-- page 371 -->

> <span style="color:#7f8c8d;">本页为书页 369，属 VI.5，为全章习题集 VI.5（共 7 题）；页眉与印页码不译。</span>

**习题集 VI.5**

1. 秩一矩阵 $P=aa^{\mathsf T}/a^{\mathsf T}a$ 是到过 $a$ 的直线上的正交投影。验证 $P^2=P$（投影性）、$Pc$ 在该直线上、且 $c-Pc$ 总垂直于 $a$（为什么 $a^{\mathsf T}c=a^{\mathsf T}Pc$？）。

2. 验证式 (4)，它表明 $c_{k+1}-c^{*}$ 恰好是 $P(c_k-c^{*})$。

3. 若 $A$ 只有两行 $a_1$ 与 $a_2$，则 Kaczmarz 会产生下图中的交替投影。从任一误差向量 $e_0=c_0-c^{*}$ 出发，为什么 $e_k$ 趋于零？多快？

[[FIGURE: 书页 369, 习题 3 图：两条超平面 $a_1^{\mathsf T}c=b_1$ 与 $a_2^{\mathsf T}c=b_2$ 之间的交替投影，误差向量 $e_0,e_1,e_4$ 逐步缩短并逼近交点 $c^{*}$。]]

4. 设我们要最小化 $F(x,y)=x^2+(y-c)^2$。实际最小值在 $(x^{*},y^{*})=(0,0)$ 处为 $F=0$。求在起点 $(x_0,y_0)=(1,1)$ 处的梯度向量 $\nabla F$。对于步长 $s=1$ 的全梯度下降（非随机），$(x_1,y_1)$ 是多少？

5. 在最小化 $F(c)=\|Ac-b\|^2$ 时，minibatch 大小 $B=1$ 的随机梯度下降每步求解一个方程 $a_i^{\mathsf T}c=b_i$。解释 minibatch 大小 $B=2$ 时的典型步骤。

6. （实验）对随机的 $A$ 与 $b$（$20\times 4$ 与 $20\times 1$），试做 minibatch 大小 $B=1$ 与 $B=2$ 的随机梯度下降。比较收敛速率——比值 $r_k=\|c_{k+1}-c^{*}\|/\|c_k-c^{*}\|$。

7. （实验）试用第 365 页提出的权重平均（arXiv:1803.05407）。把它应用到最小化 $\|Ac-b\|^2$，其中 $A$（$20\times 10$）与 $b$（$20\times 1$）随机选取，minibatch $B=1$。随机下降中的平均值是否比通常的迭代收敛得更快？

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么「不完美拟合」反而更好：SGD 的泛化机制：**</span> 本节开头作者把最速下降法在深度网络上的失败拆成两个独立困难：一是每一步都要对全部样本求和算梯度 $\nabla L$，太贵；二是权重个数远大于数据，存在大量满足 $\nabla L(c)=0$ 的解 $c^*$，其中不少在未见数据上表现很差。这两点其实是同一件事的两面——前者是「算不动」，后者是「算出来也没用」。SGD 用大小为 $B$ 的 minibatch 同时化解二者：每步只算 $B$ 个样本的梯度，把计算量压下来；而随机抽样的「噪声」恰好又起到正则化的作用，让算法避开那些把训练集背得滚瓜烂熟、却毫无推广能力的锐利极小值。作者用「次数为 60 的多项式精确穿过 61 个点」这个比喻点题：系数 $a_0$ 到 $a_{60}$ 完美拟合了数据，却在数据点之间疯狂振荡，对邻近测试点给出完全错误的答案。这正是 overfitting（过拟合）的本质——函数记住了所有样本，却没学到任何规律。因此本节的真正主题不是「让损失降到最低」，而是「在降到最低之前及时收手」，即 early stopping（早停）：既然后期迭代只是围着解 $c^*$ 来回弹跳，那么趁振荡开始前停下来，反而能在测试集上取得最好结果。这一动机为后文把「半收敛」当作优点、把「权重平均」当作补救手段埋下了伏笔。

> <span style="color:#1e8449;">**[note] Kaczmarz 步等价于 SGD、也等价于一次正交投影：**</span> 公式 (3) 定义的 randomized Kaczmarz（随机化卡茨马兹）迭代 $c_{k+1}=c_k+\frac{b_i-a_i^{\mathsf T}c_k}{\lVert a_i\rVert^2}a_i$，表面上是「每次随机挑一行 $i$、把 $c$ 调整到满足第 $i$ 个方程 $a_i^{\mathsf T}c=b_i$」，但把它乘上 $a_i^{\mathsf T}$ 验证即得 $a_i^{\mathsf T}c_{k+1}=b_i$——这一步其实正是对单个样本 $v_i$ 做一次随机梯度下降：损失取 $\ell_i(c)=\frac12(a_i^{\mathsf T}c-b_i)^2$，其梯度为 $a_i(a_i^{\mathsf T}c-b_i)$，取步长 $s=\lVert a_i\rVert^{-2}$ 时两者逐字一致。更关键的几何等价在公式 (4)：把 $b_i=a_i^{\mathsf T}c^*$ 代入后，$c_{k+1}-c^*=(I-P)(c_k-c^*)$，其中 $P=\frac{a_ia_i^{\mathsf T}}{a_i^{\mathsf T}a_i}$ 是秩一正交投影。这说明每次迭代就是把当前误差向量 $c_k-c^*$ 投影到超平面 $a_i^{\mathsf T}c=b_i$ 上，而正交投影不增加长度，故 $\lVert c_k-c^*\rVert$ 单调不增——即便代价 $\lVert Ac_k-b\rVert$ 并不下降。这一「误差范数必减、但收敛通常很慢」的组合，正是公式 (5) 中 Strohmer–Vershynin 期望误差界 $\mathbb E\lVert c_{k+1}-c^*\rVert^2\le(1-1/\kappa^2)\lVert c_k-c^*\rVert^2$ 的来源：每次只削掉与所选行夹角 $\theta_k$ 对应的一个分量（公式 (6) 中的因子 $1-\cos^2\theta_k$），当该因子逼近 $1$ 时收敛就慢到令人绝望。

> <span style="color:#1e8449;">**[note] ADAM 的「记忆」机制及其与前面章节的联系：**</span> 本节后半转向 adaptive method（自适应方法），核心是用「更早的梯度」来同时决定搜索方向 $D_k$ 和步长 $s_k$，见公式 (10)。对照全书的线索：§VI.4 的重球法（heavy ball）只在方向里加入了「上一步的动量」，即 $D_k$ 依赖 $\nabla L_k$ 与 $\nabla L_{k-1}$；而 ADAGRAD（公式 (12)）把步长取成 $\alpha/\operatorname{diag}(\sum_i\lVert\nabla L_i\rVert^2)^{1/2}$，等于让历史所有梯度的平方和去「缩放」当前步长——坐标里过去梯度大的方向被压小、小的方向被放大。ADAM（公式 (13)–(14)）则把这两种思想合并成两个指数滑动平均 $m$（一阶矩，方向）与 $v$（二阶矩，步长），指数权重 $\delta=0.9$、$\beta=0.999$ 使近期的梯度比早期梯度贡献大得多，于是既保留动量式的加速，又获得自适应的逐坐标步长。一个具体数值直觉：若某坐标的梯度始终很大，$v$ 的该项持续增大，$\alpha/\sqrt v$ 就把该方向步长压小，防止在陡峭方向上来回震荡；反之梯度一直小的坐标获得更大步长，从而加速逃离平坦区。文中还点出 ADAM 的隐患——Hardt–Recht–Singer 与 Reddi–Kale–Kumar 均构造了 ADAM 不收敛或步长 $s_k$ 反而增大的反例，这正是「指数衰减会稀释那一次正确方向」的后果：每隔三步才走对一次时，指数记忆把这次好步缩得太小，导致总步长不下降。
