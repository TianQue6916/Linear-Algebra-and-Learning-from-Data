# Linear Algebra and Learning From Data（线性代数与数据学习）· VII.1

## 书页 375-385 ｜ PDF 页 377-387 ｜ The Construction of Deep Neural Networks（深度神经网络的构造）

> <span style="color:#7f8c8d;">本节说明深度神经网络是怎样一步步拼装起来的：先定义单层神经元的线性部分与非线性激活，再讲权重初始化、降维与 subsampling、max-pooling，最后用超平面排列计数的方法度量这个学习函数 $F(x,v)$ 的"表达力"（flat pieces 的个数），并落到 universal approximation 定理。</span>

---

<!-- page 377 -->

> <span style="color:#7f8c8d;">本页为书页 375，属 VII.1 的开篇，给出构造学习函数 $F(x,v)$ 所需的五个关键要素；页眉与印页码不译。</span>

## VII.1 The Construction of Deep Neural Networks（深度神经网络的构造）

Deep neural networks（深度神经网络）已经演化为 machine learning（机器学习）中的一股主力。一步一步地，网络的结构变得更有弹性、更强大——也更容易适配到新的应用上。一种切入方式，是先描述结构中的几个基本组成件（essential pieces）。这些组成件汇聚成一个 learning function（学习函数）$F(x, v)$，其中的 weights（权重）$x$ 从 training data（训练数据）$v$ 中捕捉信息——以便为将来用于新的 test data（测试数据）做好准备。下面是创建这个函数 $F$ 的几个重要步骤：

| 编号 | 名称 | 内容 |
|---|---|---|
| 1 | Key operation（关键运算） | 复合 $F = (x, v)$ |
| 2 | Key rule（关键法则） | 关于 $F$ 对 $x$ 导数的 chain rule（链式法则） |
| 3 | Key algorithm（关键算法） | Stochastic gradient descent（随机梯度下降），用来找最优权重 $x$ |
| 4 | Key subroutine（关键子程序） | Backpropagation（反向传播），用来执行链式法则 |
| 5 | Key nonlinearity（关键非线性） | $\mathrm{ReLU}(y) = \max(y, 0)$，即 ramp function（斜坡函数） |

我们的第一步，是逐层（one layer of neurons at a time）描述这些组成件 $F_1, F_2, F_3, \dots$。连接各层的权重 $v$ 在构造 $F$ 的过程中被优化。向量 $v_0$ 来自训练集，而函数 $F_k$ 在第 $k$ 层产生向量 $v_k$。

整套成功的关键，在于用方程 (1) 中的那些组成件 $F_k$ 来构建 $F$ 的能力。

### $F_k$ 是 $v_{k-1}$ 的一个 Piecewise Linear Function（分段线性函数）

$F_k$ 的输入是一个长度为 $N_{k-1}$ 的向量；输出是一个长度为 $N_k$ 的向量 $v_k$，准备作为 $F_{k+1}$ 的输入。这个函数 $F_k$ 有两个部分，先是 linear（线性），后是 nonlinear（非线性）：

1. $F_k$ 的线性部分得到 $A_k v_{k-1} + b_k$（那个 bias vector（偏置向量）$b_k$ 使这一步成为 "affine"（仿射））；
2. 一个固定的非线性函数，例如 ReLU，被施加到 $A_k v_{k-1} + b_k$ 的每一个分量上：

```math
F_k(v_{k-1}) = \mathrm{ReLU}(A_k v_{k-1} + b_k) \tag{1}
```

每个样本的 training data 都在一个 feature vector（特征向量）$v_0$ 中。矩阵 $A_k$ 的形状为 $N_k \times N_{k-1}$；列向量 $b_k$ 有 $N_k$ 个分量。这些 $A_k$ 和 $b_k$ 就是由优化算法构造出来的 weights。通常，stochastic gradient descent 会在深度学习这一核心计算中算出最优权重 $x = (A_1, b_1, \dots, A_L, b_L)$。它依赖 backpropagation 来求 $F$ 对 $x$ 的导数，从而解出 $\nabla F = 0$。

### 激活函数 $\mathrm{ReLU}(y) = \max(y, 0)$ 带来灵活性与适应性

仅仅用线性步骤，其能力是有限的，最终也不成功。ReLU 被施加到每一个 internal layer（内部层）里的每一个 "neuron"（神经元）上。第 $k$ 层有 $N_k$ 个神经元，装着 $A_k v_{k-1} + b_k$ 的 $N_k$ 个输出。注意 ReLU 本身是 continuous（连续）且 piecewise linear 的，正如它的图像所示。（这个图像只是一条 ramp，斜率为 0 和 1；它的导数就是通常的 step function（阶跃函数）。）当我们选择 ReLU 时，复合函数 $F(x, v)$ 就具有一个重要且有吸引力的性质：

> **学习函数 $F$ 对 $v$ 是连续且分段线性的。**

---

<!-- page 378 -->

> <span style="color:#7f8c8d;">本页为书页 376，属 VII.1，用一个"单个内部层、4 个神经元"的具体例子走通 forward 计算，并配图 VII.1 展示 ReLU 与 sigmoid 的图形及其导数；页眉与印页码不译。</span>

## One Internal Layer (L=2)（单个内部层，$L=2$）

假设我们对训练集中一个样本点测量了 $m=3$ 个特征。这些特征就是输入向量 $v_0$ 的 3 个分量。那么链条里的第一个函数 $F_1$ 就把 $v_0$ 乘以一个矩阵 $A_1$，再加上一个偏移向量 $b_1$（bias vector）。

若 $A_1$ 是 $4\times 3$ 的、$b_1$ 是 $4\times 1$ 的，我们就得到 $A_1 v_0 + b_0$ 的 4 个分量。

这一步找到了原始特征向量 $v_0$ 中 3 个特征的 4 种组合。矩阵 $A_1$ 里的 12 个权重，是在训练集上对许多特征向量 $v_0$ 优化出来的，为的是选出一个 $4\times 3$ 矩阵（和一个 $4\times 1$ 偏置向量），去找到 4 种有洞察力的组合。

到达 $v_1$ 的最后一步，是把非线性 "activation function"（激活函数）施加到 $A_1 v_0 + b_1$ 的 4 个分量上。历史上，那个非线性函数的图像常由一条光滑的 "S-curve"（S 形曲线）给出。当时和现在的一些具体选择见 Figure VII.1。

[[FIGURE: 书页 376, Figure VII.1：左列为 ReLU 及其导数（阶跃函数），右列为 sigmoid 选项 $\tanh(x/2)$ 及其导数；对比"斜坡"与"光滑 S 曲线"两种非线性。]]

Figure VII.1: The Rectified Linear Unit and a sigmoid option for nonlinearity（整流线性单元与一个 sigmoid 选项）。

以前人们认为斜率的突然变化是危险的、可能不稳定。但大规模数值实验表明并非如此！用 ramp function $\mathrm{ReLU}(y)=\max(y,0)$ 反而取得了更好的结果。我们后面都用 ReLU：

> 把 $A_1 v_0 + b_1$ 代入 ReLU 就得到 $v_1$：

```math
(v_1)_k = \mathrm{ReLU}\big((A_1 v_0 + b_1)_k\big) \tag{2}
```

现在我们在第 1 层的四个 "neuron" 处得到了 $v_1$ 的分量。输入层装着这个特定训练样本的 3 个分量。我们可能有成千上万甚至上百万个样本。优化算法求出了 $A_1$ 和 $b_1$，可能就是用 backpropagation 计算整体 loss 的梯度、再走 stochastic gradient descent。

假设我们的神经网络是 shallow（浅层）而非 deep 的，它只有这一层 4 个神经元。那么最后一步将把这个 4 分量向量 $v_1$ 乘以一个 $1\times 4$ 矩阵 $A_2$（一个行向量），再加上一个数 $b_2$ 得到 $v_2 = A_2 v_1 + b_2$。非线性函数 ReLU **不**施加到输出上。

总体上，我们对训练集里每个特征向量 $v_0$ 计算

```math
v_2 = F(x, v_0) = A_2 v_1 + b_2 = A_2\,\mathrm{ReLU}(A_1 v_0 + b_1) + b_2 \tag{3}
```

---

<!-- page 379 -->

> <span style="color:#7f8c8d;">本页为书页 377，属 VII.1，给出 feed-forward 网络结构图 VII.2，并区分 classification 与 regression、square loss 与 cross-entropy loss，点出 overfitting 的风险；页眉与印页码不译。</span>

优化 $x = (A_1, b_1, A_2, b_2)$ 的目标，是让最后一层的输出值 $v_2$ 能正确捕捉训练数据 $v_0$ 的重要特征。

[[FIGURE: 书页 377, Figure VII.2：一个带 4 个神经元内部层的前馈网络。$v_0$（3 分量）→ 乘 $A_1$、加 $b_1$ 得 $y_1$ → ReLU 得 $v_1$（4 分量）→ 乘 $1\times 4$ 矩阵 $A_2$ 得输出 $v_2 = A_2 v_1$。]]

Figure VII.2: A feed-forward neural net with 4 neurons on one internal layer（一个内部层上有 4 个神经元的前馈网络）。

输出（正或负）对输入分类（狗还是猫）。于是 $v_2$ 就是这个 3 分量特征向量 $v_0$ 的一个综合度量。这个网络在 $A_k$ 和 $b_k$ 里共有 20 个权重。

对于 classification problem（分类问题），每个训练样本被赋值为 $+1$ 或 $-1$，我们希望输出 $v_2$ 有正确的符号（大多数时候如此）。对于 regression problem（回归问题），我们使用 $v_2$ 的数值本身（而不只是符号）。

我们**不**会选足够多的权重 $A_k$ 和 $b_k$ 让每个样本都对。而且我们也未必想那样做！那很可能就是 overfitting（过拟合）训练数据。当 $F$ 被用于新的、未知的测试数据时，这会导致结果飘忽不定。

根据我们所选要最小化的 loss function（损失函数）$L(x, v_2)$，这个问题可以类似 least squares（最小二乘）或 entropy minimization（熵最小化）。我们是在选择权重矩阵 $A_k$ 和偏置向量 $b_k$ 来最小化 $L$。那两种损失函数——square loss（平方损失）和 cross-entropy loss（交叉熵损失）——将在 VII.4 节进行比较。

我们的期望是这个函数 $F$ 已经 "learned"（学到了）数据。这就是 machine learning。我们不想在 $x$ 里塞进那么多权重，以致每个输入样本都保证被正确分类——那不是 learning，那只是 fitting（拟合，即 overfitting）数据。我们要的是一种平衡：函数 $F$ 学到了识别"狗 vs 猫"（或"迎面驶来的车 vs 正在转弯的车"）时真正重要的东西。

Machine learning 并不以捕捉数字 $0,1,2,\dots$ 的每一个细节为目标，它只以捕捉到足够信息来正确判定"这是哪个数字"为目标。

---

<!-- page 380 -->

> <span style="color:#7f8c8d;">本页为书页 378，属 VII.1，讲梯度下降的初始权重选择——初始方差 $\sigma^2$ 控制权重的均值、层宽控制权重方差，并引入 fan-in 与 "He uniform" 初始化；页眉与印页码不译。</span>

## The Initial Weights in Gradient Descent（梯度下降中的初始权重）

神经网络的 architecture（架构）决定了学习函数 $F(x, v)$ 的形式，训练数据进入 $v$。然后我们初始化矩阵 $A$ 和向量 $b$ 里的权重。从这些初始权重 $x_0$ 出发，优化算法（通常是某种形式的 gradient descent）依次算出 $x_1, x_2, \dots$，目标是最小化总 loss。

问题在于：该从什么权重开始？选 $0$ 会是一场灾难。糟糕的初始化是深度学习失败的一个重要原因。对网络和初始权重的正确选择，要求初始权重是随机的（且相互独立的），并满足两个要求：

1. 初始权重有一个精心选定的 variance（方差）$\sigma^2$；
2. 网络的 hidden layers（隐藏层）有足够多的神经元（不能太窄）。

Hanin 与 Rolnick 指出，初始方差 $\sigma^2$ 控制着所算权重的**均值**，而各层宽度控制着权重的**方差**。关键点在于：多层的 depth（深度）能降低训练集上的 loss；但如果 $\sigma^2$ 选错、或者牺牲了宽度，梯度下降就可能失去对权重的控制——它们会爆炸到无穷大，或坍缩到零。

由初始权重的方差 $\sigma^2$ 控制的危险，是指数级过大或过小的权重。好的选择是 $\sigma^2 = 2/\text{fan-in}$。fan-in 是一个神经元输入的最大数目（Figure VII.2 在输出处 fan-in 为 4）。Keras 里的 "He uniform" 初始化就做了这个 $\sigma^2$ 的选择。

窄隐藏层带来的危险，是对深层网络而言权重方差指数级变大。若第 $j$ 层有 $n_j$ 个神经元，要控制的量就是 $\sum_j 1/n_j$（各层宽度 $n_j$ 的倒数之和）。

展望未来，convolutional nets（ConvNets，卷积网络）和 residual networks（ResNets，残差网络）可以非常深。权重的 exploding（爆炸）或 vanishing（消失）是持续存在的危险。来自物理学（mean field theory，平均场理论）的思想已成为解释并规避这些危险的有力工具。

Pennington 及其合作者提出了一种方法，即便在 10,000 层时也能停留在"快速增长与衰减之间的边界"上。关键之一是使用 orthogonal transformations（正交变换）：正如矩阵乘法 $Q_1 Q_2 Q_3$ 那样，正交性保持"大小"不变。

对 ConvNets 而言，fan-in 变成"特征数 × kernel size（核大小）"（而不是矩阵 $A$ 的完整大小）。对 ResNets 而言，正确的初始化通常能同时消除这两种危险。非常深的网络可以产生非常令人印象深刻的学习效果。

> **关键点：深度学习如果起步不对，就可能出错。**

参考文献：

- K. He, X. Zhang, S. Ren, and J. Sun, *Delving deep into rectifiers*, arXiv: 1502.01852.
- B. Hanin and D. Rolnick, *How to start training: The effect of initialization and architecture*, arXiv: 1803.01719, 19 Jun 2018.
- L. Xiao, Y. Bahri, J. Sohl-Dickstein, S. Schoenholz, and J. Pennington, *Dynamical isometry and a mean field theory of CNNs: How to train 10,000 layers*, arXiv: 1806.05393, 2018.

---

<!-- page 381 -->

> <span style="color:#7f8c8d;">本页为书页 379，属 VII.1，讲 stride 与 subsampling 两种降维方式，以及非线性的 max-pooling；页眉与印页码不译。</span>

## Stride and Subsampling（步长与下采样）

这两个词代表达成同一个目标的两种方式：Reduce the dimension（降维）。

假设我们从长度为 128 的 1D signal（一维信号）开始。我们想 filter（滤波）这个信号——把那个向量乘以一个权重矩阵 $A$，同时还想把长度降到 64。下面是达成该目标的两种方式。

- **分两步**：把 128 分量向量 $v$ 乘以 $A$，然后丢弃输出中的奇数编号分量。这是 filtering 之后接 subsampling。输出是 $(1\ 2) Av$。
- **一步完成**：丢弃矩阵 $A$ 的奇数编号行。新矩阵 $A_2$ 变得又矮又宽：64 行、128 列。滤波器的 "stride" 现在是 2。再把 128 分量向量 $v$ 乘以 $A_2$。于是 $A_2 v$ 与 $(1\ 2) Av$ 相同。stride 为 3 则保留每第 3 个分量。

一步 striding 的方法显然更高效。若 stride 为 4，维数除以 4；在二维（图像）情形下则缩小 16 倍。

分两步的方法清楚地表明，一半或四分之三的信息被丢掉了。

这里有一种和前面一样把维数从 128 降到 64、但更不容易破坏重要信息的方法：Max-pooling（最大池化）。

### Max-pooling

和前面一样，把 128 分量向量 $v$ 乘以 $A$。然后对每一对相邻输出（如 $(Av)_2$ 和 $(Av)_3$）取最大值。请立刻注意：Max-pooling 简单又快速，但取最大值**不是**一个线性运算。它是一种纯粹而简单的降维途径。

对图像（二维信号），我们可以对每一个 $2\times 2$ 像素方块做 max-pooling：每个维数减半，图像维数缩小 4 倍。当隐藏层的神经元数除以 4 时，这就加快了训练。

通常，一个 max-pooling 步骤会在神经网络的整体架构里占有一个独立的位置。于是架构的某一部分可能长这样：

```math
v_{n+1} = \max\nolimits_2 (A v_n) \quad\longrightarrow\quad v_{n+2}
```

（即：先乘权重矩阵 $A$，再对相邻两项取 $\max$，输出进入下一层。）

除减少计算量之外，降维还有另一个重要优点：pooling 也降低了 overfitting 的可能性。Average pooling（平均池化）会保留每个 pool 内数值的平均值——这时池化层是线性的。

---

<!-- page 382 -->

> <span style="color:#7f8c8d;">本页为书页 380，属 VII.1，描述学习函数 $F(v)$ 的图像——一张由许多平坦超平面拼接而成的折纸状曲面，并预告 VII.2 的 CNN；页眉与印页码不译。</span>

## The Graph of the Learning Function $F(v)$（学习函数 $F(v)$ 的图像）

$F(v)$ 的图像是一张由许许多多平坦片拼接而成的曲面——这些平坦片是 plane（平面）或 hyperplane（超平面），在 ReLU 产生斜率变化的所有 fold（折痕）处拼合在一起。这很像 origami（折纸），只不过这张图像上的平坦片一直延伸到无穷远。而且图像未必在 $\mathbb{R}^m$ 里——特征向量 $v = v_0$ 有 $m$ 个分量。

深度学习数学的一部分，就是估计平坦片的数量，并可视化它们如何拼成一张 piecewise linear surface（分段线性曲面）。这个估计要在一个单内部层神经网络的例子之后给出。每个特征向量含有训练集里某个样本的 $m$ 个测量值，如 height（身高）、weight（体重）、age（年龄）。

在例子中，$F$ 在 $v_0$ 处有 3 个输入、一个输出 $v_2$。它的图像将是 4 维空间里的一张分段平坦曲面；图像的高度是 $v_2 = F(v_0)$，位于 3 维空间中点 $v_0$ 的上方。本书篇幅有限（加上作者想象力的严重局限），使我们无法在 $\mathbb{R}^4$ 里画出那张图。不过我们可以基于 3 个输入、4 个神经元和 1 个输出来试着数平坦片的个数。

- **Note 1**：只有 $m=2$ 个输入（每个训练样本 2 个特征）时，$F$ 的图像是 3D 里的一张曲面。我们可以、也将会尝试描述它。
- **Note 2**：当你在 playground.tensorflow.org 上跑例子时，其实能看到 $F$ 图像上的点。这是一个极有启发性的网站。

那个网站为训练点集 $v_0$ 提供四种选项，你可以选择层数和神经元数。请务必选择 ReLU 激活函数！然后程序会在梯度下降优化权重时计数 epochs（轮次）。（一个 epoch 平均看一遍所有样本。）如果你给出了足够多的层和神经元来正确分类蓝色与橙色的训练样本，你会看到一条把它们分开的 polygon（多边形）。那条多边形展示了 $F=0$ 的位置，它就是 $z=F(v)$ 的图像在高度 $z=0$ 处的 cross-section（截面）。

那条把蓝与橙（或者说正与负——这是 classification）分开的多边形，是 Support Vector Machine（支持向量机）中 separating hyperplane（分离超平面）的类比。如果被限制在只能用线性函数、只能在蓝色球与包围它的橙色环之间画一条直线，分离就不可能；但对深度学习函数 $F$ 来说这并不难。

我们将在 Problem Set 里讨论 playground.tensorflow 网站上的这些实验。

> **Important Note: Fully Connected versus Convolutional（全连接 vs 卷积）**

我们不想误导读者。那些 "fully connected"（全连接）网络往往不是最有效的。如果图像中某个像素周围的权重可以被重复用到所有像素上（为什么不呢？），那么只需 $A$ 的一行就够了——这一行可以给远处的像素赋零权重。局部化的 convolutional neural nets（CNN's，卷积神经网络）是 VII.2 节的主题。

你会看到，平坦片的数量随神经元数和层数**指数级**增长。这是对深度学习威力的一条有用洞见。我们极其需要这样的洞见，因为神经网络的规模和深度使它难以被完整地可视化。

---

<!-- page 383 -->

> <span style="color:#7f8c8d;">本页为书页 381，属 VII.1，进入本节核心：用超平面排列（hyperplane arrangement）计数平坦片，给出 r(N,m) 的公式与一个三维例子；页眉与印页码不译。</span>

## Counting Flat Pieces in the Graph: One Internal Layer（数图像中的平坦片：单个内部层）

数权重矩阵 $A_k$ 和偏置向量 $b_k$ 里的元素个数很容易，这些数决定了函数 $F$。但更有意思的是数 $F$ 图像中平坦片的个数——这个数度量了神经网络的 expressivity（表达力）。

$F(x, v)$ 是一个比我们目前完全理解的（至少到目前为止）更复杂的函数。系统在自行决策与行动，而不需要其 "thinking"（思考）获得明确批准。对无人驾驶汽车，我们很快就会看到其后果。

假设 $v_0$ 有 $m$ 个分量，$A_1 v_0 + b_1$ 有 $N$ 个分量。我们得到 $v_0$ 的 $N$ 个线性函数，每个都在 $\mathbb{R}^m$ 里的一条 hyperplane（维数 $m-1$）上取零。当我们对该线性函数施加 ReLU，它就变成 piecewise linear，并沿那条超平面产生一条 fold；fold 一侧的图像是倾斜的，另一侧函数从负变为零。

然后下一个矩阵 $A_2$ 把这些关于 $v_0$ 的 $N$ 个分段线性函数组合起来，于是我们现在在 $\mathbb{R}^m$ 里有了沿 $N$ 条不同超平面的 fold。在典型情形下，这描述了下一层 $A_2\,\mathrm{ReLU}(A_1 v_0 + b_1)$ 的每个分段线性分量。

你可以想象平面上的 $N$ 条直线 fold（实际上 fold 是沿 $m$ 维空间里的 $N$ 条超平面）。第一条 fold 把平面分成两块，下一条来自 ReLU 的 fold 让我们得到四块，第三条 fold 更难想象，但下图表明得到的是**七块**（不是八块）。

在组合学里，我们面对的是一个 hyperplane arrangement（超平面排列）——Tom Zaslavsky 的一个定理对这些块计数，其证明见 Richard Stanley 的名著 *Enumerative Combinatorics*（2001）。但那个定理比我们需要的更复杂，因为它允许折痕线以各种可能的方式相交。我们的任务更简单，因为我们假设折痕线处于 "general position"（一般位置）——$m+1$ 条 fold 不相交。对这种情形，我们采用 Raghu、Poole、Kleinberg、Ganguli 和 Sohl-Dickstein 给出的简洁计数论证：*On the Expressive Power of Deep Neural Networks*, arXiv: 1606.05336v6；另见 Pascanu、Montufar 与 Bengio 的 *The Number of Response Regions*, arXiv 1312.6098。

> **定理**　对 $v\in\mathbb{R}^m$，设 $F(v)$ 的图像沿 $N$ 条超平面 $H_1, \dots, H_N$ 有 fold，它们来自 $N$ 个线性方程 $a_i^{\top}v + b_i = 0$，即 $N$ 个神经元处的 ReLU。那么 $F$ 的线性块数、以及由这 $N$ 条超平面界定的 region（区域）数为 $r(N, m)$：

```math
r(N, m) = \sum_{i=0}^{m} \binom{N}{i} \tag{4}
```

这些 binomial coefficient（二项式系数）是 $\binom{N}{i} = \dfrac{N!}{i!(N-i)!}$，其中 $0! = 1$，且约定当 $i > N$ 时 $\binom{N}{i} = 0$。

> **例**　函数 $F(x,y,z) = \mathrm{ReLU}(x) + \mathrm{ReLU}(y) + \mathrm{ReLU}(z)$ 沿三个平面 $x=0, y=0, z=0$ 有 3 条 fold。这三个平面把 $\mathbb{R}^3$ 分成 $r(3,3) = 8$ 块，其中 $F$ 分别等于 $x+y+z$、$x+y$、$x+z$、$y+z$、$x$、$y$、$z$ 和 $0$。再加 $\mathrm{ReLU}(x+y+z-1)$ 就得到第 4 条 fold 和 $r(4,3) = 15$ 块 $\mathbb{R}^3$（不是 16），因为新 fold 平面 $x+y+z=1$ 不与第 8 个原始块（其中 $x<0, y<0, z<0$）相交。

---

<!-- page 384 -->

> <span style="color:#7f8c8d;">本页为书页 382，属 VII.1，用递归公式 (5) 证明 r(N,m) 的计数公式 (4)，并给出 Figure VII.3 说明"加一条超平面"如何新增区域；页眉与印页码不译。</span>

George Polya 那支著名的 YouTube 视频 *Let Us Teach Guessing* 用 5 个平面切蛋糕，切出 26 块。公式 (4) 允许 $m$ 维的"蛋糕"。

- $\mathbb{R}^m$ 里一条超平面产生 $r(1,m) = \binom{m}{0} + \binom{m}{1} = 1 + m = 2$ 个区域（当 $m\ge 1$ 时）。
- $N=2$ 条超平面产生 $r(2,m) = \binom{m}{0} + \binom{m}{1} + \binom{m}{2} = 1 + m + \binom{m}{2}$ 个区域，当 $m>1$ 时等于 4。
- 当 $m=1$ 时，一条直线上有两条 fold，只把直线分成 $r(2,1) = 3$ 段。

线性块数 $r$ 由递归公式得出：

```math
r(N, m) = r(N-1, m) + r(N-1, m-1) \tag{5}
```

理解这个递归：从 $\mathbb{R}^m$ 里的 $N-1$ 条超平面和 $r(N-1,m)$ 个区域开始，再加一条超平面 $H$（维数 $m-1$）。已有的 $N-1$ 条超平面把 $H$ 切成 $r(N-1,m-1)$ 个区域，$H$ 的每一块都把某个既有区域一分为二，于是给原来的 $r(N-1,m)$ 加上 $r(N-1,m-1)$ 个区域；见 Figure VII.3。所以递归成立。现在用方程 (5) 计算 $r(N,m)$。

计数从 $r(0,1) = 1$ 开始，即 $r(1,0) = 1$。然后对 $N+m$ 归纳可证 (4)：

```math
r(N, m) = r(N-1, m) + r(N-1, m-1)
= \sum_{i=0}^{m}\binom{N-1}{i} + \sum_{i=0}^{m-1}\binom{N-1}{i}
= \sum_{i=0}^{m}\left[\binom{N-1}{i} + \binom{N-1}{i-1}\right]
= \sum_{i=0}^{m}\binom{N}{i} \tag{6}
```

第二行括号里的两项合并成一项，用的是恒等式 $\binom{N-1}{i} + \binom{N-1}{i-1} = \binom{N}{i}$，归纳就此完成。

Mike Giles 使这个讲解更清晰，并建议用 Figure VII.3 来展示最后一条超平面 $H$ 的效果：当 $N \ge m$ 时有 $r \sim 2^N$ 个线性块，而当 $N \gg m$（隐藏层有很多神经元）时 $r \sim N^m / m!$ 个块。

[[FIGURE: 书页 382, Figure VII.3：从 2 条平面开始，加入新平面 H；H 上的 r(2,1)=3 块产生 3 个新区域，于是计数变成 r(3,2)=4+3=7 个平坦区域。]]

Figure VII.3: $H$ 的 $r(2,1)=3$ 块产生 3 个新区域，于是计数变成 $r(3,2) = 4 + 3 = 7$ 个平坦区域，位于连续分段线性曲面 $v_2 = F(v_0)$ 上。第四条 fold 会穿过全部 3 条已有 fold 并产生 4 个新区域，所以 $r(4,2) = 11$。

---

<!-- page 385 -->

> <span style="color:#7f8c8d;">本页为书页 383，属 VII.1，把平坦片计数推广到多个隐藏层（给出 $N_1+N_2$ 的估计），并讨论函数复合与希尔伯特第 13 问题、Kolmogorov–Arnold 表示；页眉与印页码不译。</span>

## Flat Pieces of $F(v)$ with More Hidden Layers（更多隐藏层时 $F(v)$ 的平坦片）

当网络有 2 个内部层时，数 $F(v)$ 的线性块要难得多。仍设 $v_0$ 和 $v_1$ 分别有 $m$ 和 $N_1$ 个分量，$A_1 v_1 + b_1$ 在施加 ReLU 前有 $N_2$ 个分量。每一个都像上面描述的单层函数 $F$。之后施加 ReLU 会在其图像上产生新的 fold，这些 fold 沿 $A_1 v_1 + b_1$ 某分量取零的位置分布。

记住，$A_1 v_1 + b_1$ 的每个分量是 piecewise linear 的，**不是**线性的。所以它（如果确实过零）是沿一张分段线性曲面过零，而不是沿一条超平面。Figure VII.3 中 $v_1$ 的 fold 直线，会变成 $v_2$ 中 fold 的分段直线；在 $m$ 维里它们是超平面的连通片段。于是计数变得可变，取决于 $v_0, A_1, b_1, A_2, b_2$ 的细节。

不过我们仍能估计线性块的数量。我们在第二个隐藏层有来自 $N_2$ 个 ReLU 的 $N_2$ 条分段直线（即 $\mathbb{R}^m$ 里的分段超平面）。如果这些线真是直线，$v_3 = F(v_0)$ 的每个分量里总共就有 $N_1 + N_2$ 条 fold，那么计数公式 (4) 就把 $N$ 换成 $N_1 + N_2$。这就是我们对 $v_0$ 与 $v_3$ 之间有两层时的估计（仍有改进余地）。

### Composition（复合）$F_3(F_2(F_1(v_0)))$

如果所有函数都是线性的，即 $F_k(v) = A_k v$，"复合"就只是 "matrix multiplication"（矩阵乘法）：$F(v_0) = A_3 A_2 A_1 v_0$，就一个矩阵。对非线性 $F_k$ 含义相同：先算 $v_1 = F_1(v_0)$，再算 $v_2 = F_2(v_1)$，最后 $v_3 = F_3(v_2)$。这种复合运算在造函数方面比加法强大得多！

对神经网络，复合产生连续的 piecewise linear 函数 $F(v_0)$。

Hilbert 1900 年那 23 个未解决问题中的第 13 个，问了一个关于所有连续函数的问题。他的问题的一个著名推广是：

> 每一个三变量连续函数 $F(x,y,z)$ 是否都是两变量连续函数 $G_1, \dots, G_N$ 的复合？

答案是**肯定的**。Hilbert 似乎预期答案是否定的。但 Vladimir Arnold（时年 19 岁）在 1957 年给出了肯定的答案。他的老师 Andrey Kolmogorov 此前已经用三变量函数造出了多变量函数。

相关的问题有否定答案：如果 $F(x,y,z)$ 有连续导数，可能无法让所有两变量函数也都有连续导数（Vitushkin）。而要构造两变量连续函数 $F(x,y)$ 作为单变量连续函数的复合（终极的第 13 问题），你必须允许加法。两变量函数 $x^y$ 与 $x^{y}$ 用到了单变量函数 $\exp, \log$ 和 $\log\log$：

```math
x^y = \exp(\log x + \log y), \qquad x^{y} = \exp\big(\exp(\log y + \log\log x)\big) \tag{7}
```

从网上能学到的东西太多了。*Kolmogorov's Heritage in Mathematics*（Springer, 2007）的一章把这些问题和神经网络明确联系了起来。

> 对 $\mathbb{R}^m$ 上的连续分段线性函数，希尔伯特问题的答案仍然是"是"吗？

---

<!-- page 386 -->

> <span style="color:#7f8c8d;">本页为书页 384，属 VII.1，讲 universal approximation：定性（universality，任何连续函数可被逼近）与定量（逼近误差随权重数下降的速率 $cn^{-r/d}$）；页眉与印页码不译。</span>

## Neural Nets Give Universal Approximation（神经网络给出通用逼近）

前面几段游离到了多变量函数 $f(v)$ 的分析上。对深度学习，一个关键问题是：当权重 $x$ 被选得使 $F(x, v)$ 接近 $f(v)$ 时，神经网络对 $f$ 的逼近问题。

有一个定性问题，也有一个定量问题：

1. **定性**：对 $\mathbb{R}^m$ 中一个 cube（立方体）内的任意连续函数 $f(v)$，一个层数、神经元数和权重足够多的网络，能否在任意给定精度 $\epsilon > 0$ 内一致逼近 $f$？这个性质称为 universality（通用性）。若 $f(v)$ 连续，则存在 $x$ 使

```math
|F(x, v) - f(v)| < \epsilon \quad\text{对所有 } v \tag{8}
```

2. **定量**：若 $f(v)$ 属于光滑函数组成的 normed space（赋范空间）$S$，当网络有更多权重时，逼近误差以多快改善？

```math
\|F(x, v) - f(v)\| \le C \|f\|_S \, n^{-r/d} \tag{9}
```

（即逼近 $f$ 的精度。）

函数空间 $S$ 常使用函数 $f$ 及其直到 $r$ 阶偏导数的 $L^2$、$L^1$ 或 $L^{\infty}$ 范数。泛函分析甚至对非整数的 $r$ 赋予了这些空间含义。$C$ 通常随光滑性参数 $r$ 增大而减小。对网格间距为 $h$ 的均匀网格上的连续分段线性逼近，我们常发现 $C = O(h^2)$。

问题 1 的回答是**是**。Wikipedia 指出，一个 hidden layer（只要有足够多神经元！）就足以逼近到 $\epsilon$ 以内。George Cybenko 1989 年的证明用的是 sigmoid 函数而非 ReLU，该定理还在不断被推广。Ding-Xuan Zhou 证明了可以要求 $A_k$ 是 convolution matrices（卷积矩阵，于是结构变成一个 CNN）。卷积比任意矩阵的权重少得多——而 universality 允许许多次卷积。

问题 2 的回答，由 Mhaskar、Liao 和 Poggio 给出，从对具有 $r$ 阶连续导数的函数 $f(v_1, \dots, v_d)$ 的逼近阶开始。对 $n$ 个权重，通常的误差界是 $c n^{-r/d}$。他们的新意在于引入由两变量函数构造的 composite functions（复合函数），如 $f(v_1, v_2, v_3, v_4) = f_3(f_1(v_1, v_2), f_2(v_3, v_4))$。对复合函数，hierarchical（分层）网络的逼近要精确得多，误差界变成 $c n^{-r/2}$。证明把 $d=2$ 变量的标准结果应用到每个函数 $f_1, f_2, f_3$ 上（复合函数之差是两变量差值的复合）。

参考文献：

1. G. Cybenko, *Approximation by superpositions of a sigmoidal function*, Mathematics of Control, Signals, and Systems 7 (1989) 303-314.
2. K. Hornik, *Approximation capabilities of multilayer feedforward networks*, Neural Networks 4 (1991) 251-257.
3. H. Mhaskar, Q. Liao, and T. Poggio, *Learning functions: When is deep better than shallow*, arXiv: 01603.00988v4, 29 May 2016.

---

<!-- page 387 -->

> <span style="color:#7f8c8d;">本页为书页 385，属 VII.1，续列参考文献 4–5 并给出 VII.1 节的习题集（Problem Set）；页眉与印页码不译。</span>

4. D.-X. Zhou, *Universality of deep convolutional neural networks*, arXiv: 1805.10769, 20 Jul 2018.
5. D. Rolnick and M. Tegmark, *The power of deeper networks for expressing natural functions*, arXiv: 1705.05502, 27 Apr 2018.

## Problem Set VII.1（习题集 VII.1）

1. 在公式 (4) 之后那个 $r(N,m)$ 的例子里，$F = \mathrm{ReLU}(x) + \mathrm{ReLU}(y) + \mathrm{ReLU}(z)$。设第 4 条 fold 来自 $\mathrm{ReLU}(x+y+z)$，它的 fold 平面 $x+y+z=0$ 现在与原来的 3 条 fold 平面 $x=0, y=0, z=0$ 交于单点 $(0,0,0)$——一个例外情形。请描述这四个 ReLU 之和 $F$ 的 16 块（不是 15 块）线性块。

2. 设 $m=2$ 个输入、隐藏层上有 $N$ 个神经元，于是 $F(x,y)$ 是 $N$ 个 ReLU 的线性组合。写出 $r(N,2)$ 的公式，说明 $F$ 的线性块数的主项（leading term）是 $\tfrac12 N^2$。

3. 设平面上有 $N=18$ 条直线：9 条竖直、9 条水平，平面被分成多少块？与直线处于一般位置（无三条共点）时的 $r(18,2)$ 比较。

4. 什么权重矩阵 $A_1$ 和偏置向量 $b_1$ 会得到 $\mathrm{ReLU}(x+2y-4)$、$\mathrm{ReLU}(3x-y+1)$ 和 $\mathrm{ReLU}(2x+5y-6)$ 作为第一隐藏层的 $N=3$ 个分量？（输入层有 2 个分量 $x$ 和 $y$。）若输出 $w$ 是这三个 ReLU 之和，$w(x,y)$ 有多少块？

5. 把一条线折 4 次得到 $r(4,1)=5$ 段，把一张平面折 4 次得到 11 块。按公式 (4)，把 $\mathbb{R}^3$ 折 4 次得到多少个平坦子集？（$\mathbb{R}^3$ 的平坦子集在 2D 平面处相交，像门框一样。）

6. 二项式定理给出 $(a+b)^N = \sum_k \binom{N}{k} a^k b^{N-k}$ 中的系数。对 $a=1$（即 $b=1$ 时），这揭示了这些系数以及 $m\ge N$ 时 $r(N,m)$ 的什么？

7. 在 Figure VII.3 中，再多折一次会在 $z=F(x,y)$ 的图像上产生 11 个平坦块。验证公式 (4) 给出 $r(4,2)=11$。折 5 次之后有多少块？

8. 用文字解释或用图像说明，下面关于 Continuous Piecewise Linear functions（CPL 函数，连续分段线性函数）的每一条命题为什么成立：
   - **(M)** 两个 CPL 函数 $F_1(x,y)$ 与 $F_2(x,y)$ 的**最大值** $M(x,y)$ 是 CPL。
   - **(S)** 两个 CPL 函数 $F_1(x,y)$ 与 $F_2(x,y)$ 的**和** $S(x,y)$ 是 CPL。
   - **(C)** 若单变量函数 $y=F_1(x)$ 与 $z=F_2(y)$ 都是 CPL，则复合 $C(x) = F_2(F_1(x))$ 也是 CPL。

---

## 译者注

> <span style="color:#27ae60;">【译者注 1 · 为什么 $\sigma^2 = 2/\text{fan-in}$】这一条讲的其实是"信号在网络里传播时方差不放大也不缩小"的物理直觉。把一层的前向传播写成 $y = W x$（省略偏置），若输入 $x$ 的各分量独立、均值为 0、方差为 $\operatorname{Var}(x)$，$W$ 的元素独立、均值 0、方差 $\sigma^2$，则输出的单分量方差为 $\operatorname{Var}(y_j) = \sum_i \operatorname{Var}(W_{ji} x_i) = \operatorname{fan-in}\cdot \sigma^2 \cdot \operatorname{Var}(x)$（独立零均值乘积的方差等于方差之积）。要让方差逐层保持为常数，就须 $\sigma^2 = 1/\text{fan-in}$。作者写 $2/\text{fan-in}$，是因为下一节的 ReLU 会把约一半的负值置零，输出方差因此减半，故需把方差翻倍来补偿——这正是 He 初始化（He et al., 2015, arXiv:1502.01852）与早先 Xavier/Glorot 初始化（用 $1/\text{fan-in}$，针对 tanh 等对称激活）的关键区别。用错这一条，方差就会随层数呈几何增长或衰减，即正文所说权重的"爆炸或坍缩"，梯度也就随之 vanishing/exploding。</span>

> <span style="color:#27ae60;">【译者注 2 · 递归 $r(N,m)=r(N-1,m)+r(N-1,m-1)$ 与二项式系数】这条递归是"一条新超平面多切出多少区域"的直接翻译：$r(N-1,m)$ 是原来 $N-1$ 条超平面的区域数，而新加的第 $N$ 条超平面 $H$ 是一个 $(m-1)$ 维空间，旧超平面在 $H$ 上切出的区域数是 $r(N-1,m-1)$；$H$ 每穿过一个这样的子区域，就把那个 $m$ 维区域一分为二，故新增区域数恰好是 $r(N-1,m-1)$。它和 Pascal 三角的递推 $\binom{N}{i}=\binom{N-1}{i}+\binom{N-1}{i-1}$ 是同构的，所以闭式解正是 $\sum_{i=0}^{m}\binom{N}{i}$——也就是"在 $N$ 条超平面中任选至多 $m$ 条的组合数"。这个计数与 VII.4 里讲到的、以及本节末尾 universal approximation 里"用更多神经元逼近函数"是同一件事的两种度量：flat pieces 越多，$F$ 越能折出复杂的曲面去贴合数据。</span>

> <span style="color:#27ae60;">【译者注 3 · "一般位置"与 $r(4,3)=15$ 而非 16】公式 (4) 成立的前提是超平面处于 general position（一般位置）：任意 $m+1$ 条 fold 超平面不相交于同一点。若违反，某些区域就会"退化"消失，计数变小。正文的三维例子正是反例：第 4 个 ReLU 的 fold 平面 $x+y+z=1$ 不穿过"三坐标皆负"的第 8 块区域，因为要 $x<0,y<0,z<0$ 同时又 $x+y+z=1>0$ 不可能，所以只新增 7 块得 $r=15$。习题 1 更极端：若第 4 个平面取 $x+y+z=0$，它恰好穿过三个坐标平面唯一的公共点 $(0,0,0)$，把那个"退化"的交点重新打开，反而得到满的 16 块。这就是为什么"一般位置"是超平面排列计数里不可省的前提——它保证每一条新折痕都"完整地"切开它该切开的东西，不多也不少。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么「连续分段线性」是整节的核心承诺：**</span> 本节一开篇就反复强调：在选取 ReLU（`ReLU(y) = max(y, 0)`，整流线性单元）之后，学习函数 $F(c, v)$ 具有「连续且分段线性」这一性质。这句话不是顺便一提，而是后面所有计数的起点。道理在于：若 $F$ 只用线性层 $A_k v_{k-1} + b_k$ 堆叠，那么无论叠多少层，$A_L \cdots A_2 A_1$ 相乘后仍是一个矩阵，$F$ 最终仍是一个线性函数——所以书中明确说「仅有线性步骤威力有限，最终不成功」。真正让深度网络有表达力的，正是每层线性变换之后那一步「非线性的折痕」。ReLU 的巧妙之处在于，它制造的非线性是「最温和」的一种：函数在每个折痕（fold）两侧仍是斜率为 $0$ 或 $1$ 的直线段，只在折痕处改变斜率。于是整个 $F$ 的图象不是一张光滑曲面，而是一张由许多「平面片（flat pieces / hyperplanes）」沿折痕拼合而成的分段线性曲面。这带来两个巨大好处：一是数值上稳定、好优化（不像 sigmoid 那样两端饱和、梯度消失）；二是它把「神经网络有多强」这个看似玄学的问题，转化成了一个可以精确计数的组合问题——数一数这些平面片到底有多少块。下文公式 (4) 的 $r(N, m)$ 正是在回答这个「有多少块」的问题，它衡量的是网络的表达能力（expressivity）。

> <span style="color:#1e8449;">**[note] 平面片计数公式 $r(N,m)$ 的来历与递归：**</span> 公式 (4) 给出的 $r(N,m)=\sum_{i=0}^{m}\binom{N}{i}$ 是这一节数学味最浓的一处，它回答的是：$m$ 维空间 $\mathbb{R}^m$ 被 $N$ 个「一般位置（general position，即任意 $m+1$ 个折痕不共点）」的超平面切成多少块区域。这个数为什么是这个形式，不必死记，可以从递归式 (5) $r(N,m)=r(N-1,m)+r(N-1,m-1)$ 一次看懂：先放下 $N-1$ 个超平面，得到 $r(N-1,m)$ 块区域；再加入第 $N$ 个超平面 $H$（它本身是 $m-1$ 维的），前面那 $N-1$ 个超平面会把 $H$ 切出 $r(N-1,m-1)$ 块小片，每一小片恰好把一个旧区域一分为二，于是新增 $r(N-1,m-1)$ 块。这个递归的边界是 $r(0,m)=r(1,0)=1$，解出来就是二项式系数之和。一个直观的数值例子是波利亚（Polya）切蛋糕的经典题：用 $5$ 个平面切 $\mathbb{R}^3$，得 $r(5,3)=\binom{5}{0}+\binom{5}{1}+\binom{5}{2}+\binom{5}{3}=1+5+10+10=26$ 块。注意这和「直觉上每多一刀翻倍」不同——$4$ 个超平面若互相平行或交于一点会少于 $15$ 块，正是书中「第四个折痕平面 $x+y+z=1$ 没有穿过 $x<0,y<0,z<0$ 那一块，所以是 $15$ 而非 $16$」的例子，说明了「一般位置」假设的作用。

> <span style="color:#1e8449;">**[note] 与全书别处的联系：从「分段数」到「通用逼近」：**</span> 本节关于平面片计数的讨论，表面上在数「折痕」，实质上是在给深度学习的表达能力（expressive power）定标尺，而这一主题会直接通向本节末尾「神经网络给出通用逼近（universal approximation）」的结论。逻辑链条是这样的：$r(N,m)$ 随神经元数 $N$ 与层数增长而增长——书中指出，$N \gg m$ 时 $r(N,m)$ 的数量级约为 $N^m/m!$，即多项式级；而当网络加深、折痕相互叠加时，平面片的数量会随层数呈指数增长。这解释了为什么「深」比「宽」更划算：一层网络的表达能力受限于超平面排列的计数，而把非线性分层复合（composition）能指数级地放大可实现的平面片数。这一思想正是后来一批文献的出发点，例如 Raghu、Poole 等人《On the Expressive Power of Deep Neural Networks》以及 Pascanu、Montufar、Bengio 的《The Number of Response Regions》。它与后文「通用逼近」的呼应在于：分段数只是「能表示多复杂的函数」的一个粗度量，而通用逼近定理进一步断言——只要神经元足够多，$F(c,v)$ 就能在紧集上以任意精度 $\epsilon$ 一致逼近任意连续函数 $f(v)$。换句话说，计数平面片回答的是「网络能造出多少种形状」，而通用逼近回答的是「这些形状加起来能不能逼近任意目标」，两者是同一枚硬币的两面。
