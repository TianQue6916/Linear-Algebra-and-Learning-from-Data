# Linear Algebra and Learning From Data（线性代数与数据学习）· VII.3

## 书页 397-405 ｜ PDF 页 399-407 ｜ Backpropagation and the Chain Rule（反向传播与链式法则）

> <span style="color:#7f8c8d;">本节说明：深度学习本质是一个大规模优化问题，核心就是高效计算损失函数对各权重的偏导数。作者从显式导数公式讲到计算图（computational graph），对比 forward-mode（前向模式）与 backward-mode（后向模式，即反向传播）两种自动微分（automatic differentiation）方式，最终落脚于「反向模式能更省地计算导数」这一贯穿全书的线性代数思想。</span>

---

<!-- page 399 -->
> <span style="color:#7f8c8d;">本页为书页 397，属 VII.3 开篇，介绍反向传播的动机、链式法则、计算图概念，以及前向/后向模式两种自动微分的区别与选择依据。页眉与印页码不译。</span>

**VII.3 Backpropagation and the Chain Rule（反向传播与链式法则）**

Deep learning is fundamentally a giant problem in optimization.（深度学习本质上是一个庞大的优化问题。）我们在选择数值化的 "weights"（权重）来最小化一个损失函数 loss function $L$（它依赖于这些权重）。$L(c)$ 把所有的损失 $(w-\text{true})$（计算输出与真实标签之差）累加起来，这里输出 $w=F(c,v)$，而 true 是输入 $v$ 的真实分类。微积分告诉我们要解的方程组——使 $L$ 最小的权重满足：

> 损失函数 $L$ 关于各权重的偏导数应当为零。

各种变体的 gradient descent（梯度下降）都需要在权重的当前取值处计算导数（即 $F$ 的梯度分量）。由 $\partial F/\partial c$ 可以推得 $\partial L/\partial c$。基于这些信息，我们移到能给出更小损失的新权重，再在新权重处重新计算 $F$ 与 $L$ 的导数，如此反复。

Backpropagation（反向传播）是一种利用 chain rule（链式法则）快速计算导数的方法：

```math
\frac{dF_3}{dx} = \frac{dF_3}{dF_2}\,\frac{dF_2}{dF_1}\,\frac{dF_1}{dx}
```

目标之一，是找到一种方式来直观呈现函数 $F$ 是如何由权重计算出来的。一种巧妙的方法是 computational graph（计算图）。它把庞大的计算拆成一个个小步骤，我们在图上就能求出每一步（每一个计算）的导数；然后微积分中的链式法则给出最终输出 $w=F(c,v)$ 关于所有权重 $c$ 的导数。对一个标准网络而言，链式法则中的每一步恰好可以对应神经网络中的一层 layer。

相对于「对每个导数 $\partial F/\partial c_i$ 分别单独计算」，这是一种惊人的效率提升。乍看之下很难相信——仅仅重新组织计算顺序就能带来如此巨大的差别。质疑者也许会说：归根结底你还不是要对每一步求导、再用链式法则相乘？但这方法确实管用——计算 $N$ 个导数所需的代价，远小于「单个导数 $\partial F/\partial x_1$ 代价的 $N$ 倍」。

Backpropagation 已被多次独立发现，另一个名字是 automatic differentiation（AD，自动微分）。你会看到这些步骤可以按两种基本方式排布：forward-mode（前向模式）与 backward-mode（后向模式）。模式选得对不对，代价可能差出成千上万倍。这个选择取决于：你是有「很多函数 $F$ 依赖少数几个输入」，还是「少数几个函数 $F$ 依赖很多输入」。

深度学习基本上就是「一个损失函数依赖海量权重」，所以正确的选择是 backward-mode AD，也就是我们所说的 backpropagation。它是深度学习的计算核心。下面我们用一个小例子来展示计算图与反向传播。

这些计算图的灵感来自 Christopher Olah 在其博客（colah.github.io）上精彩的阐述，自 2017 年起他也在 https://distill.pub 上发表文章。此外，Catherine 与 Desmond Higham 的新论文（arXiv:1801.05894，将刊于 SIAM Review）对 backpropagation 给予了特别关注，并附有非常实用的代码。

---

<!-- page 400 -->
> <span style="color:#7f8c8d;">本页为书页 398，属 VII.3，给出学习函数 $F(c,v)$ 的结构（各层矩阵与偏置向量）、最后一层权重/偏置的显式导数公式，以及一个 $2\times 2$ 的数值例子。页眉与印页码不译。</span>

**Learning from Data（数据学习）**

学习函数 $F(c,v)$ 关于 $c$ 的导数 $\partial F/\partial c$。权重 $c$ 由所有的矩阵 $A_1,\dots,A_L$ 以及偏置向量 bias vectors $b_1,\dots,b_L$ 组成。输入 $v=v_0$ 是训练数据，输出 $w=v_L$ 出现在第 $L$ 层。在输出之前是隐藏层中的 $v_1,\dots,v_{L-1}$。

因此 $w=v_L$ 是神经网络中经过 $v_1,\dots,v_{L-1}$ 之后的最后一步。每个新层 $v_n$ 都由前一层经过 $R(b_n+A_n v_{n-1})$ 得到，这里 $R$ 是逐分量作用的非线性激活函数 nonlinear activation function（通常是 ReLU）。

于是深度学习把我们由 $v_0$ 带到 $w=v_L$，再把 $w$ 代入损失函数来衡量该样本 $v$ 的误差。它可能是分类误差（该为 $0$ 却得到 $1$，或该为 $1$ 却得到 $0$）；可能是最小二乘回归误差 $\|g-w\|^2$，其中 $w$ 取代了期望输出 $g$；也常是 cross-entropy（交叉熵）。总损失 $L(c)$ 是所有输入向量 $v$ 上损失之和。

深度学习这个庞大的优化目标，是要找到使 $L$ 最小的权重 $c$。对 full gradient descent（全量梯度下降），损失是 $L(c)$；对 stochastic gradient descent（随机梯度下降），每次迭代的损失是一个输入或一个 minibatch（小批量）的输入。无论哪种情况，我们都需要输出 $w$（最后一层的分量）关于权重（把我们从一层带到下一层的那些 $A$ 与 $b$）的导数 $\partial w/\partial c$。

这正是深度学习如此昂贵、耗时如此之久的原因之一——即便在 GPU 上也是如此。对卷积网络而言，这些导数已在 VII.2 节被快速、简便地求出了。

**计算 $\partial F/\partial c$：显式公式**

我们计划用两种方法计算导数 $\partial F/\partial c$。第一种是给出显式公式——关于每一个权重的导数；第二种是描述实践中常用的反向传播算法。

先从产生最终输出 $v_L=w$ 的最后一个偏置向量 $b_L$ 与权重矩阵 $A_L$ 入手。这一层没有非线性，我们省去层下标 $L$：

```math
v_L = b_L + A_L v_{L-1} \quad\text{或简写为}\quad w = b + Av. \tag{1}
```

我们的目标是求出 $b+Av$ 所有分量的导数 $\partial w_i/\partial b_j$ 与 $\partial w_i/\partial A_{jk}$。当 $j\neq i$ 时，第 $i$ 个输出 $w_i$ 不受 $b_j$ 或 $A_{jk}$ 影响——$A$ 乘 $v$ 时，$A$ 的第 $j$ 行产生的是 $w_j$ 而非 $w_i$。我们引入符号 $\delta$（取 $1$ 或 $0$）：

```math
\delta_{ij} =
\begin{cases}
1 & \text{若 } i=j\\
0 & \text{若 } i\neq j
\end{cases}
```

单位矩阵 identity matrix $I$ 的元就是 $\delta_{ij}$，$I$ 的每一列都是 one-hot vector（独热向量）。于是这些导数取值为 $1$、$0$ 或 $v_k$（见 I.12 节）：

```math
\frac{\partial w_i}{\partial b_j} = \delta_{ij}
\quad\text{且}\quad
\frac{\partial w_i}{\partial A_{jk}} = \delta_{ij}\, v_k . \tag{2}
```

**Example（例子）**：对 $w_1$ 的导数，一共有六个 $b$ 与 $a$ ：

```math
\begin{aligned}
\frac{\partial w_1}{\partial b_1} &= 1, &
\frac{\partial w_1}{\partial b_2} &= 0, \\[1ex]
\frac{\partial w_1}{\partial a_{11}} &= v_1, &
\frac{\partial w_1}{\partial a_{12}} &= v_2, \\[1ex]
\frac{\partial w_1}{\partial a_{21}} &= 0, &
\frac{\partial w_1}{\partial a_{22}} &= 0,
\end{aligned}
\qquad
\begin{bmatrix} w_1 \\ w_2 \end{bmatrix}
=
\begin{bmatrix} a_{11} & a_{12}\\ a_{21} & a_{22} \end{bmatrix}
\begin{bmatrix} v_1 \\ v_2 \end{bmatrix}
+
\begin{bmatrix} b_1 \\ b_2 \end{bmatrix}.
```

（即：$w_1 = a_{11}v_1 + a_{12}v_2 + b_1$，故对 $a_{11}$、$a_{12}$ 求导得 $v_1$、$v_2$，对 $b_1$ 求导得 $1$；而 $w_1$ 不含 $a_{21},a_{22},b_2$，故这些导数为 $0$。）

---

<!-- page 401 -->
> <span style="color:#7f8c8d;">本页为书页 399，属 VII.3，介绍把偏置 $b$ 与矩阵 $A$ 合并成增广矩阵 $M$ 的紧凑写法，并进入含一个隐藏层的网络，用链式法则给出 $\partial w/\partial A_1$ 的三因子结构。页眉与印页码不译。</span>

**把权重 $b$ 与 $A$ 合并成 $M$**

把偏置向量 $b$ 与矩阵 $A$ 合并成一个大矩阵 $M$ 往往更方便：

```math
M = \begin{bmatrix} 1 & 0\\ b & A \end{bmatrix}, \qquad
\text{权重矩阵 } M \text{ 有 } M_{00} = 1. \tag{3}
```

对神经网络的每一层，最上面一项（第 $0$ 项）现在固定为 $1$。这一层乘上 $M$ 之后，下一层的第 $0$ 分量仍是 $1$；于是 ReLU$(1)=1$ 在每个隐藏层都保持住这个分量。本书开头（第 v 页）那幅神经网络大图里，用方块表示第 $0$ 项、用圆圈表示其余各项——现在每个方块里都是 $1$。

这个分块矩阵 $M$ 给出最后一层 $w=Mv$ 的紧凑导数公式：

```math
\frac{\partial w_i}{\partial M_{jk}} = \delta_{ij}\, v_k \quad (i>0). \tag{4}
```

$v$ 与 $w$ 都以 $1$ 开头。于是 $k=0$ 正确地给出 $\partial w_0/\partial M_{j0}=0$（对 $j>0$）。

**隐藏层的导数**

现在假设有一个隐藏层，即 $L=2$。输出是 $w=v_2$，隐藏层含 $v_1$，输入为 $v_0=v$。非线性 $R$ 多半是 ReLU：

```math
v_1 = R(b_1 + A_1 v_0)
\quad\text{且}\quad
w = b_2 + A_2 R(b_1 + A_1 v_0) .
```

公式 (2) 仍给出 $w$ 关于最后一组权重 $b_2$、$A_2$ 的导数——输出端没有函数 $R$，且此时 $v$ 就是 $v_1$。但 $w$ 关于 $b_1$、$A_1$ 的导数确实牵涉到作用在 $b_1+A_1 v_0$ 上的非线性函数 $R$。所以 $\partial w/\partial A_1$ 中的导数需要链式法则 $\partial f/\partial x = (\partial f/\partial g)(\partial g/\partial x)$：

```math
\frac{\partial w}{\partial A_1}
= \frac{\partial [A_2 R(b_1 + A_1 v_0)]}{\partial (b_1 + A_1 v_0)}
\cdot \frac{\partial (b_1 + A_1 v_0)}{\partial A_1} . \tag{5}
```

这条链式法则有三个因子。从第 $L-2=0$ 层的 $v_0$ 出发，权重 $b_1$ 与 $A_1$ 把我们带向第 $L-1=1$ 层，这一步的导数与公式 (2) 完全一样；但这一步部分计算的输出还不是 $v_{L-1}$，要得到该隐藏层还得先作用 $R$，因此链式法则要包含 $R$ 的导数 $R'$；最后一步（到 $w$）则乘上最后一层的权重矩阵 $A_2$。

Problem Set 把这些公式推广到 $L$ 层。它们也许有用，但有了 pooling（池化）与 batch normalization（批归一化）之后，自动微分似乎胜过了硬编码求导。

**非常重要的提醒**：注意公式 (2) 与 (5) 是怎样从 $w$ 反向走回 $v$ 的。自动反向传播也是如此——reverse mode（反向模式）从输出端开始。

---

<!-- page 402 -->
> <span style="color:#7f8c8d;">本页为书页 400，属 VII.3，细看 $\partial w/\partial A_1$ 中的非线性部分：引入 ReLU 及其导数（阶跃/δ 函数）、Leaky ReLU、dying ReLU 问题与尺度不变性，并配图 VII.4。页眉与印页码不译。</span>

**导数 $\partial w/\partial A_1$ 的细节**

我们有责任更仔细地看一看公式 (5)。其中非线性部分 $R'$ 来自非线性激活函数的导数。通常的选择是斜坡函数 ramp function ReLU$(x)=x^+$，而我们可以把 ReLU 视为 S 形 sigmoid 函数的极限情形。下面是 ReLU 连同它的前两阶导数：

```math
\text{ReLU}(x) = \max(0, x), \qquad
\frac{dR}{dx} = \begin{cases} 1 & x>0\\ 0 & x<0 \end{cases},
\qquad
\frac{d^2 R}{dx^2} = \delta(x).
```

即：斜坡函数（ramp）→ 阶跃函数（step）→ $\delta$ 函数（delta）。这里的积分覆盖全域。

$\delta$ 函数 delta function 表示一个冲激 impulse，它模拟「无穷小时间内的有限变化」。它在物理上不可能，但数学上很方便。它并不是在每一点 $x$ 处定义的，而是通过它作用在从 $-\infty$ 到 $\infty$ 的连续函数 $g(x)$ 上的积分来定义的：

```math
\int_{-\infty}^{\infty} \delta(x-a)\, g(x)\, dx = g(a), \qquad
\int_{-\infty}^{\infty} \delta(x)\, g(x)\, dx = g(0).
```

使用 ReLU 时，某个神经元可能在深度学习的整个过程中一直停在 $0$。这种 dying ReLU（死亡 ReLU）可以用几种方法避免——通常它并非大问题。一种彻底避免它的办法，是改用梯度非零的 Leaky ReLU：

```math
\text{Leaky ReLU: } R_\alpha(x) = \alpha\,\text{ReLU}(x),\quad
\alpha x \ (x<0), \quad \text{通常 }\alpha\approx .01 . \tag{6}
```

Geoffrey Hinton 指出：若把每一层的偏置向量 $b_1,\dots,b_L$ 都置为零，输入 $v$ 的尺度就会原封不动地传到输出 $w=F(v)$，即 $F(\alpha v)=\alpha F(v)$（最后的 softmax 会破坏这种尺度不变性）。

```math
\text{ReLU: } R(x)=\max(0,x),\quad
\text{Leaky ReLU: } R(x)=\begin{cases} x & x\ge 0\\ 0.01x & x<0 \end{cases}.
```

[[FIGURE: 书页 400, Figure VII.4：ReLU 与 Leaky ReLU 的图像（两种非线性激活选项），ReLU 负半轴斜率为 0、正半轴斜率为 1，Leaky ReLU 负半轴斜率约为 1/100、正半轴斜率为 1。]]

回到公式 (5)，把产生最后一个隐藏层的矩阵与向量记作 $A=A_{L-1}$、$b=b_{L-1}$；随后 ReLU 与 $A_L$、$b_L$ 产生最终输出 $w=v_L$。我们关心的是 $w$ 关于倒数第二个权重矩阵的依赖 $\partial w/\partial A$：

```math
w = A_L R(Av + b) + b_L, \qquad
\frac{\partial w}{\partial A} = \dots \tag{7}
```

---

<!-- page 403 -->
> <span style="color:#7f8c8d;">本页为书页 401，属 VII.3，把 $R'$ 写成对角矩阵 $J$ 使公式 (7) 化成 (8)，并正式引入计算图概念，用一个具体例子 $F=x^2(x+y)$ 演示前向模式。页眉与印页码不译。</span>

我们把 $R'$ 想象成一个逐分量作用在 $Av+b$ 上的、由 ReLU 导数组成的对角矩阵 diagonal matrix。那么 $R'(Av+b)$ 就是一个对角矩阵，正分量处为 $1$、负分量处为 $0$（零处别问我）。公式 (7) 于是化为 (8)：

```math
w = A_L R(Av + b), \qquad
\frac{\partial w}{\partial A}
= A_L \, R'(Av+b) \, \frac{\partial (Av+b)}{\partial A} . \tag{8}
```

第三个因子的每个分量（$v_k$ 或 $0$）我们都已从 (2) 的导数中知道了。

当 sigmoid 函数 $R_\alpha$ 取代 ReLU 时，对角矩阵 $J=R'(Av+b)$ 就不再是 $1$ 和 $0$ 了；此时我们要在 $Av+b$ 的每个分量处求值导数 $dR_\alpha/dx$。

实践中，backpropagation 求出关于所有 $A$ 与 $b$ 的导数，它自动地（且有效地）生成这些导数。

**Computational Graphs（计算图）**

设 $F(x,y)$ 是两个变量 $x$、$y$ 的函数，这两个输入是计算图 computational graph 中最初的两个节点 node。计算中的一个典型步骤——图里的一条边 edge——是算术运算之一（加、减、乘……）。最终输出就是函数 $F(x,y)$。我们的例子取 $F=x^2(x+y)$。

下面是计算 $F$ 的图，中间节点为 $c$ 与 $s=c+y$：

```math
c = x^2, \qquad s = c + y, \qquad F = cs .
```

当我们有输入 $x$、$y$（例如 $x=2$、$y=3$）时，各边依次得到 $c=4$、$s=5$、$F=20$。这和我们平时挤在一行里的代数一致：

```math
F = x^2(x+y) = 2^2(2+3) = 4(5) = 20 .
```

现在计算每一步——图中每一条边——的导数。先从 $c$ 的导数开始。最初我们选择 forward-mode（前向模式），从输入 $x$ 出发朝输出函数 $x^2(x+y)$ 走。前几步对 $c=x^2$ 用幂法则、对 $s=x+y$ 用求和法则，最后一步对 $F=cs$ 用乘积法则：

```math
\frac{\partial c}{\partial x} = 2x, \qquad
\frac{\partial s}{\partial x} = 1, \qquad
\frac{\partial s}{\partial c} = 1 .
```

沿图走下去，就得到了链式法则！

---

<!-- page 404 -->
> <span style="color:#7f8c8d;">本页为书页 402，属 VII.3，把前向模式算完得到 $\partial F/\partial x$ 与 $\partial F/\partial y$ 的数值，并强调前向模式每算一个新输入都要一张新图；随后引出「一个输出、反向走一张图」的反向模式。页眉与印页码不译。</span>

```math
\frac{\partial F}{\partial x}
= \frac{\partial F}{\partial s}\frac{\partial s}{\partial x}
+ \frac{\partial F}{\partial c}\frac{\partial c}{\partial x}
= (s)(2x) + (c)(1) .
```

结果是求出了输出 $F$ 关于单个输入 $x$ 的导数。这些 $x$ 导数都能在计算图上看到。

**Forward mode（前向模式）**：

```math
\frac{\partial c}{\partial x} = 4,\quad
\frac{\partial s}{\partial x} = 1,\quad
\frac{\partial F}{\partial x} = (s)(2x) + (c)(1) = 5\cdot 4 + 4\cdot 1 = 24.
```

对 $y$ 的导数会有一张类似的图——前向模式导向 $\partial F/\partial y$。下面是链式法则，以及 $x=2$、$c=x^2=4$、$s=x+y=5$、$F=cs$ 时图中会出现的数字：

```math
\frac{\partial F}{\partial y}
= \frac{\partial F}{\partial c}\frac{\partial c}{\partial y}
+ \frac{\partial F}{\partial s}\frac{\partial s}{\partial y}
= (c)(0) + (s)(1) = 0 + 5 = 5 .
```

$\partial F/\partial y$ 的计算图没有画出来，但关键点在于：**forward mode 要为每一个输入 $x_i$ 画一张新图**，才能算出对应的偏导数 $\partial F/\partial x_i$。

**一个输出的 Reverse Mode（反向模式）图**

反向模式从输出 $F$ 出发，它计算关于两个输入的导数，计算沿图反向进行。

这意味着它不必走前向 $x$ 导数图中那条从 $\partial y/\partial x=0$ 出发的空线；也不必走（未画出的）$y$ 导数图中 $\partial x/\partial y=0$ 那条空线。一个更大、更现实的、有 $N$ 个输入的问题会有 $N$ 张前向图，每张图有 $N-1$ 条空线（因为 $N$ 个输入彼此独立，任意输入 $x_i$ 关于其它输入 $x_j$ 的导数 $\partial x_i/\partial x_j=0$）。

我们不用从 $N$ 个输入出发画 $N$ 张前向图，而是从一个输出出发画一张反向图。下面就是这张 reverse-mode 计算图，它求出 $F$ 关于每一个节点的导数，从 $\partial F/\partial F=1$ 开始反向推进。

计算图执行链式法则来求导数。反向模式通过从输出到输入反向追踪所有链条，求出全部导数 $\partial F/\partial x_i$。这些链条都作为路径出现在**同一张图**上——而不是指数多条可能路径各自独立的一条条链式法则。这正是 reverse mode 的成功之处。

---

<!-- page 405 -->
> <span style="color:#7f8c8d;">本页为书页 403，属 VII.3，配图 VII.5 展示反向模式在 $x=2,y=3$ 处的梯度计算，并用「三矩阵乘积 $ABC$ 的乘法顺序」这一纯线性代数问题，说明前向/反向选择的本质是运算量的差异。页眉与印页码不译。</span>

```math
\frac{\partial F}{\partial x} = 24, \qquad
\frac{\partial F}{\partial y} = 5, \qquad
\frac{\partial c}{\partial x} = 4, \quad
\frac{\partial s}{\partial x} = 1, \quad
\frac{\partial s}{\partial y} = 1 .
```

[[FIGURE: 书页 403, Figure VII.5：在 $x=2,\,y=3$ 处反向模式对梯度 $\partial F/\partial x$、$\partial F/\partial y$ 的计算图，各边标注导数数值。]]

**矩阵乘积 $ABC$：按什么顺序乘？**

前向与反向之间的抉择，在矩阵乘法里也出现了！若要求 $A$ 乘 $B$ 乘 $C$，结合律给出两种乘法顺序：

```math
\text{先算 } (AB)C \ \text{ 还是 } \ A(BC) \ ?
\quad \text{先 } AB \ \text{ 还是先 } BC \ ?
```

结果相同，但标量乘法的次数可能天差地别。设矩阵 $A$ 是 $m\times n$，$B$ 是 $n\times p$，$C$ 是 $p\times q$。

- 第一种方式：$AB=(m\times n)(n\times p)$ 有 $mnp$ 次乘法；$(AB)C=(m\times p)(p\times q)$ 有 $mpq$ 次乘法。
- 第二种方式：$BC=(n\times p)(p\times q)$ 有 $npq$ 次乘法；$A(BC)=(m\times n)(n\times q)$ 有 $mnq$ 次乘法。

于是比较的就是 $mp(n+q)$ 与 $nq(m+p)$。把两个数同除以 $mnpq$：

```math
\frac{1}{q} + \frac{1}{n}
\qquad\text{对比}\qquad
\frac{1}{m} + \frac{1}{p}.
```

当 $\dfrac1q+\dfrac1n$ 小于 $\dfrac1m+\dfrac1p$ 时，第一种方式更快。

这里有一个极端（且极重要）的情形。设 $C$ 是列向量，即 $p\times 1$，于是 $q=1$。你该先乘 $BC$ 得到一个列向量（$n\times 1$）、再乘 $A(BC)$ 得到输出（$m\times 1$）吗？还是先乘 $AB$？

问题几乎不言自明。正确的 $A(BC)$ 每一步都产生向量：矩阵-向量乘法 $BC$ 有 $np$ 步，下一个矩阵-向量乘法 $A(BC)$ 有 $mn$ 步；把这些 $np+mn$ 步，与从矩阵-矩阵 $AB$ 起步的代价（$mnp$ 步！）相比——任何神志清醒的人都不会去算那个。

---

<!-- page 406 -->
> <span style="color:#7f8c8d;">本页为书页 404，属 VII.3，给出 $A$ 为行向量时 $(AB)C$ 更优的对称情形，点明这正是深度网络前向传播的链式结构；随后转入 Adjoint Methods（伴随法），把「矩阵乘法顺序」问题映射到含设计变量的优化问题。页眉与印页码不译。</span>

但如果 $A$ 是行向量，则 $(AB)C$ 更优——每次都做「行向量乘矩阵」。

这恰好对应深度学习的核心计算：训练网络、优化权重。深度网络的输出 $F(v)$ 是一条以 $v$ 开头的链：

```math
F(v) = A_L\, R\big(A_{L-1}\big(\cdots R(A_2\, R(A_1 v))\big)\big)
= A_L v_{L-1} ,
```

这是穿过网络的前向过程。

$F$ 关于矩阵 $A$（及偏置向量 $b$）的导数，对链中最后一个矩阵 $A_L$ 最易求：$A_L v_{L-1}$ 中 $Av$ 关于 $A$ 的导数含有 $v$，即 $\partial w_i/\partial A_{jk}=\delta_{ij}v_k$。下一步是 $A_L\,\text{ReLU}$ 关于 $A_{L-1}$ 的导数。

我们可以说明：同一种反向模式也出现在优化（选择好的权重）中 direct methods（直接法）与 adjoint methods（伴随法）的比较里。

**Adjoint Methods（伴随法）**

矩阵乘法 $ABC$ 的最佳顺序问题，在一大类优化问题中同样出现。我们在解一个 $N$ 阶线性方程组 $Ev=b$。右端向量 $b$ 依赖于设计变量 design variables $p=(p_1,\dots,p_M)$，因而解向量 $v=E^{-1}b$ 也依赖于 $p$。含导数 $\partial v_i/\partial p_j$ 的矩阵 $\partial v/\partial p$ 将是 $N\times M$ 的。

重申：我们在最小化 $F(v)$，向量 $v$ 依赖于设计变量 $p$，于是需要一条链式法则把导数 $\partial F/\partial v_i$ 与 $\partial v_i/\partial p_j$ 相乘。

让我说明这如何变成一个三矩阵乘积——而乘法顺序是决定性的。三组导数控制着 $F$ 对输入变量的依赖：

```math
A = \frac{\partial F}{\partial v_i}\ \text{（}F\text{ 关于 }v_1,\dots,v_N\text{ 的导数）},\qquad
B = \frac{\partial v_i}{\partial b_k},\qquad
C = \frac{\partial b_k}{\partial p_j}.
```

为求 $\partial v_i/\partial p_j$，对方程 $Ev=b$ 关于 $p_j$ 求导：

```math
E\frac{\partial v}{\partial p_j} = \frac{\partial b}{\partial p_j}. \tag{9}
```

看起来我们有 $M$ 个规模为 $N$ 的线性方程组。在我们不断搜索使 $F(v)$ 最小的 $p$ 时，一遍遍求解它们会很昂贵。矩阵 $\partial v/\partial p$ 包含 $v_1,\dots,v_N$ 关于设计变量 $p_1,\dots,p_M$ 的导数。

先假设代价函数 $F(v)=c^{T}v$ 是线性的（于是 $\partial F/\partial v=c^{T}$）。那么优化真正需要的是 $F(v)$ 关于各 $p$ 的梯度。第一组导数 $\partial F/\partial v$ 就是向量 $c^{T}$：

```math
\frac{\partial F}{\partial p}
= \frac{\partial F}{\partial v}\,\frac{\partial v}{\partial p}
= c^{T}\,\frac{\partial v}{\partial p}. \tag{10}
```

这里有三个因子要相乘。

---

<!-- page 407 -->
> <span style="color:#7f8c8d;">本页为书页 405，属 VII.3 结尾，给出伴随方程 $E^{T}\lambda=c$，说明「最优顺序是 $(AB)C$，因为 $A$ 实为行向量 $\lambda^{T}$」，并将伴随思想推广到微分方程，最后回到深度网络各层的递推关系与链式法则。页眉与印页码不译。</span>

这是关键方程。它以「行向量 $c$ 乘 $N\times N$ 矩阵、再乘 $N\times M$ 矩阵 $\partial b/\partial p$」的乘积收尾。该如何计算这个乘积？

问题同样几乎不言自明：我们不想乘两个矩阵，所以最终并不去算 $\partial v/\partial p$。相反，好的第一步是求 $c^{T}E^{-1}$，这产生一个行向量 $\lambda^{T}$。换言之，我们解伴随方程 adjoint equation $E^{T}\lambda=c$：

```math
\text{伴随方程 } E^{T}\lambda = c \ \text{ 给出 }\ \lambda = E^{-T}c,\ \text{ 即 }\ \lambda^{T} = c^{T}E^{-1}. \tag{11}
```

把 $\lambda^{T}$ 代入方程 (10) 中的 $c^{T}E^{-1}$，最后一步就把这个行向量乘上向量 $b$ 的导数（它的梯度）：

```math
\text{代价 }F\text{ 的梯度：}\quad
\frac{\partial F}{\partial p} = \lambda^{T}\,\frac{\partial b}{\partial p}
\qquad (1\times N \ \text{乘}\ N\times M). \tag{12}
```

最优顺序是 $(AB)C$，因为第一个因子 $A$ 实为行向量 $\lambda^{T}$。

这个伴随法例子始于 $Ev=b$。右端 $b$ 依赖于设计参数 $p$，于是解 $v=E^{-1}b$ 依赖于 $p$；代价函数 $F(v)=c^{T}v$ 也依赖于 $p$。伴随方程 $E^{T}\lambda=c$ 求出了那个向量，从而高效地把后两步合并起来。「Adjoint（伴随）」与「transpose（转置）」有平行的含义，我们也可以把它用于微分方程。设计变量 $p_1,\dots,p_M$ 可能出现在矩阵 $E$ 里，也可能出现在特征值问题或微分方程里。

我们此处的重点是强调并强化反向传播的核心思想：**反向模式能以更快的方式排列导数的计算**。

**深层网络的伴随与灵敏度（Adjoints and Sensitivity）**

更接近深度学习的问题：在参数为 $x_n$ 的第 $L$ 层，输出 $w=v_L$ 关于这些参数 $x_n$ 的导数 $\partial w/\partial x_n$ 是什么？

输出 $w=v_L$ 是从输入 $v_0$ 出发经 $L$ 步后看到的。我们把第 $n$ 步写成：

```math
v_n = F_n(v_{n-1}, x_n) , \tag{13}
```

其中 $F_n$ 依赖于权重（参数）$x_n$。(13) 是一个递推关系 recurrence relation。而同一组参数 $c$ 可能每一步都用。深度学习为每一层安排新的参数——这赋予了它普通递推关系无法企及的「学习能力」。事实上，一个典型递推 (13) 只是微分方程 $dv/dt=\dots$ 的有限差分近似。

这个类比不算差：这里我们同样可能瞄准一个期望输出 $v(T)$，并通过选择参数 $c$ 去逼近它。问题在于求导数矩阵 $J=\partial v_N/\partial x_M$。我们必须对方程 (13) 一路从 $N$ 反向套用链式法则到 $0$。链上的一步是：

```math
v_N = F_N(v_{N-1}, x_N) = F_N\big(F_{N-1}(v_{N-2}, x_{N-1}), x_N\big). \tag{14}
```

---

## 译者注

> <span style="color:#2e7d32;">**注 1 · 为什么「反向模式一张图」能胜过「前向模式 $N$ 张图」？** 设网络有 $N$ 个权重、$M$ 个输出，前向模式是从每个输入出发沿图向前传播一个「切线方向」，要得到关于全部 $N$ 个输入的导数，就得重复 $N$ 遍，代价约为 $N$ 倍单次前向。而反向模式从**唯一**的输出（深度学习里损失 $L$ 是标量，输出数 $M=1$）出发，沿图反向一次，就能顺路把所有节点的导数都算出来，代价仅约为一次反向的常数倍。这就是书里反复强调的「一个损失函数依赖海量权重 → 选 backward-mode」。它的数学本质是：链式法则中反向模式把「多条路径共享的中间量」只算一次并复用，避免了前向模式下每条路径各自重复求导。这与下一页「三矩阵乘积 $ABC$」的次序选择是同一件事——反向 = 先算 $A(BC)$（每一步都保持向量），前向 = 先算 $(AB)C$（中途膨胀成矩阵）。理解这一点，比记住任何代码都重要。</span>

> <span style="color:#2e7d32;">**注 2 · 公式 (2) 的 $\delta_{ij}v_k$ 是怎么来的，等号在何时成立？** 因为 $w_i = b_i + \sum_k A_{ik}v_k$，对 $A_{jk}$ 求导时，只有当 $i=j$ 时求和项 $\sum_k A_{ik}v_k$ 里才出现 $A_{jk}$，贡献 $v_k$；$i\neq j$ 时 $A_{jk}$ 根本不在 $w_i$ 的表达式中，导数为 $0$。这正是 $\delta_{ij}$ 的含义。更进一步，把 $b$ 与 $A$ 合成增广矩阵 $M=\begin{bmatrix}1&0\\b&A\end{bmatrix}$ 后，公式 (4) 用一个式子 $\partial w_i/\partial M_{jk}=\delta_{ij}v_k$ 同时覆盖了 $b$ 与 $A$ 两类权重——这正体现了本书「用矩阵把看似分开的量统一起来」的一贯手法，与 I.12 节把 one-hot 向量、$\delta_{ij}$、单位矩阵串起来的讲法呼应。等号成立条件方面，(2) 是精确的线性层恒等式，无近似；真正出现「等号成立条件」的是代价比较 $mp(n+q)$ vs $nq(m+p)$，两边相等（即 $\frac1q+\frac1n=\frac1m+\frac1p$）时两种顺序代价相同。</span>

> <span style="color:#2e7d32;">**注 3 · 为什么把「矩阵乘法顺序」与「前向/反向模式」并列讲？** 这是本节最高明的一步。伴随法里 $\partial F/\partial p = c^{T}\cdot(\partial v/\partial p)$ 若直接算，等于先算 $\partial v/\partial p=E^{-1}\partial b/\partial p$，即解 $M$ 个 $N$ 阶方程组（相当于「先乘 $AB$」），代价 $O(MN^3)$ 或更高；而先解一次伴随方程 $E^{T}\lambda=c$（相当于「先算 $BC$」，保持右端是向量）再乘 $\lambda^{T}\partial b/\partial p$，代价仅 $O(N^3+MN)$。两者之比在 $M\ll N$ 时是数量级之差。这告诉我们：**「先算哪个乘积」不是实现细节，而是算法复杂度本身**。反向传播在深度网络里正是同一件事——沿着网络反向传一个「伴随量」（梯度），每层只做一次矩阵-向量乘，而不是对每个权重都从头展开一次完整前向。理解了 $ABC$ 的次序，就理解了反向传播为什么「便宜」。</span>

> <span style="color:#2e7d32;">**注 4 · 关于公式还原的说明与两处存疑。** 原文多处 OCR 把转置与下标压平，已按「连写大写 = 上标转置、连写小写 = 下标」等规则还原：如 $\partial w_i/\partial b_j=\delta_{ij}$、$\partial w_i/\partial A_{jk}=\delta_{ij}v_k$、$E^{T}\lambda=c$、$c^{T}v$ 等。有两处需提请注意：(i) 书页 404 中「$A=\partial F/\partial v_i$、$B=\partial v_i/\partial b_k$、$C=\partial b_k/\partial p_j$」的三矩阵记号，其实是把上一页 $ABC$ 乘法顺序的抽象符号，借用来标注三个导数量纲（$1\times N$、$N\times N$、$N\times M$），并非说 $\partial F/\partial p$ 直接等于这三个字母相乘，具体顺序由 (11)(12) 的伴随方程决定。〔原书此处 OCR 残缺，依上下文推为上述对应关系，待核。〕(ii) 图 VII.4、VII.5 的坐标与边标注中，个别数值（如 Leaky ReLU 负半轴斜率是否恰为 $1/100$、图 VII.5 各边标注）已按正文语境复原，建议对照原图核对。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么把「求导」变成「计算图」就能快一个数量级：**</span> 正文…本节的核心动机是一句乍看违反直觉的话：对 $N$ 个权重各自单独求导，代价是「一次导数成本的 $N$ 倍」，但把求导重新组织成反向传播（backpropagation）之后，$N$ 个导数竟能在**远小于** $N$ 倍单次成本的代价内全部算出来。这里的机制不在于「少算了什么」，而在于**把公共的中间量只算一次、然后反复复用**。设想前向计算 $w=F(c,v)$ 由 $L$ 步复合而成，$F=F_L\circ F_{L-1}\circ\cdots\circ F_1$；若对每个权重 $c_i$ 都从头算一遍 $\partial F/\partial c_i$，链式法则会沿同一条「输出→输入」的路径反复穿越，大量中间导数 $\partial F_k/\partial F_{k-1}$ 被重复计算了 $N$ 次。反向模式（reverse-mode）的聪明之处在于方向相反：它从输出端 $\partial F/\partial F=1$ 出发，沿图**逆序**只走一遍，把每个节点的梯度 $\partial F/\partial (\text{node})$ 存下来，遇到分叉就累加（对应微积分里「一个量影响多个量时要把各条路径求和」），于是每个中间导数恰好被算一次。这一「记忆化 + 反向遍历」的结构，正是 automatic differentiation（自动微分）的本质。正文点出的选择标准也源于此：当「很多个输出函数依赖很少输入」时，前向模式一次能带出所有输出、更划算；而深度学习是**一个**损失函数依赖**海量**权重，方向反过来，所以 backward-mode 成为唯一正确选择——这也正是本节标题把 backpropagation 与 chain rule 并列的原因：反向传播不是新的求导法则，而是链式法则的一种高效调度。
>
> <span style="color:#1e8449;">**[note] 式 (8) 中那个对角矩阵 $J$ 从哪来，它与「ReLU 求导成开关」的等价关系：**</span> 正文…正文从式 (7) 推进到式 (8) 的关键一步，是把非线性激活函数 $R$ 看作一个「按分量独立作用」的对角矩阵。要理解这个 $J=R'(Av+b)$，只需回到标量情形：层间关系 $w=A_L R(Av+b)+b_L$ 中，$R$ 对向量 $Av+b$ 的每个分量分别取函数值，于是对向量求导得到的 Jacobian（雅可比矩阵）$R'(Av+b)$ 必然是对角阵——第 $k$ 个对角元是 $\partial R/\partial x$ 在第 $k$ 个分量处的取值，因为第 $k$ 个输出只由第 $k$ 个输入决定。当 $R$ 取 ReLU（即 $R(x)=\max(0,x)$）时，这个对角元立即退化成二元开关：分量 $>0$ 处取 $1$，分量 $<0$ 处取 $0$（正文戏称「别问零点」），所以 $J$ 成为一个由 $1$ 与 $0$ 排成的对角阵——这等价于说「ReLU 的导数是 step function（阶跃函数），二阶导是 $\delta$（delta function）」，正文用图 VII.4 画出的正是这条链条：ramp → step → delta。这也顺手解释了本节对「dying ReLU（死亡 ReLU）」的讨论：若某分量在训练全过程中始终 $<0$，其梯度恒为 $0$，该神经元就永远不再更新；把 ReLU 换成 Leaky ReLU，即负半轴给一个小斜率 $0.01$（正文写 $R(x)=x\ (x\ge0)$、$R(x)=0.01x\ (x<0)$），$J$ 的对角元在负区就变成 $0.01$ 而非 $0$，梯度不再彻底消失，从而规避死亡问题。一言以蔽之：式 (8) 不是新公式，而是「逐分量求导」用矩阵语言写的紧凑形式，$J$ 的非零元来源，正是式 (2) 里 $\partial w_i/\partial b_j=\delta_{ij}$、$\partial w_i/\partial A_{jk}=\delta_{ij}v_k$ 那两个「$1$ 或 $0$」的推广。
>
> <span style="color:#1e8449;">**[note] 与 §VI.1–VI.3 的 Krylov / 幂迭代及「矩阵乘顺序」的联系，附一个数值例子：**</span> 正文…本节后半段用「$ABC$ 三个矩阵该按什么顺序相乘」的问题来类比反向传播，这其实和本书更早讲 Krylov 方法、幂迭代（power iteration）时的「矩阵—向量乘总是比矩阵—矩阵乘便宜」是同一件事。正文给出的账目最直白：设 $A$ 是 $m\times n$、$B$ 是 $n\times p$、$C$ 是 $p\times q$，则先算 $AB$ 再乘 $C$ 需要 $mnp+mpq=mp(n+q)$ 次乘法，而先算 $BC$ 再乘 $A$ 需要 $npq+mnq=nq(m+p)$ 次；两种顺序的比值可用 $\frac{1}{n}+\frac{1}{q}$ 与 $\frac{1}{p}+\frac{1}{m}$ 来比较。最极端也最重要的情形是 $C$ 为一列向量（$q=1$）：正确做法是先算 $BC$（成本 $np$）再做 $A(BC)$（成本 $mn$），总共 $np+mn$；而若愚蠢地先算 $AB$，光这一步就要 $mnp$ 次，白白多出一个量级。这正是反向传播的精髓在矩阵语言里的复现：前向传播 $F(v)=A_L\,R\,(A_{L-1}\,R(\cdots(A_1 v)))$ 本就是「矩阵乘向量」的链，梯度也该用「行向量依次左乘」而非「先乘出大矩阵」来求。用一个具体数字更能说明差别：取 $m=1000,\ n=1000,\ p=1$（一个 $1000$ 维输出、$1000$ 个权重、一维输入），先算 $BC$ 得 $n\times p$ 的向量需 $1000$ 次乘法，再算 $A(BC)$ 需 $1000$ 次，总计 $2000$；而先算 $AB$ 的矩阵—矩阵乘需 $mnp=10^6$ 次，慢了 $500$ 倍。正文把这一思想再推广到 adjoint method（伴随方法）：求解 $Ev=b$ 且 $b$ 依赖设计变量 $p$ 时，不要去算昂贵的 $\partial v/\partial p$（一个 $N\times M$ 矩阵），而应解伴随方程 $E^T\lambda=c$ 得到行向量 $\lambda^T=c^TE^{-1}$，再做一次「行向量乘矩阵」，即式 (12)——顺序永远是 $(AB)C$ 而非 $A(BC)$，这回答的正是「这个算法为什么收敛、为什么快」：因为矩阵乘法的结合律给了我们重排计算的自由，而反向模式永远选择「先与向量相乘」的那条最便宜的路。
