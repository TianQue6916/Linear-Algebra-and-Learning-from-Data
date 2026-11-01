# Part VII　Learning from Data（从数据中学习）· §VII.1–§VII.5

## 书页 368-415 ｜ PDF 页 370-417

---

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

---

> <span style="color:#7f8c8d;">本节从线性代数的视角讲解卷积神经网络：如何用权值共享（weight sharing）与局部连接（locality）把全连接层换成只有少数独立权重的卷积层，进而说明 2D 卷积、滤波器、步长、填充、深度网络、Softmax 输出、AlphaGo 与 ResNet 等概念。全节的核心是「卷积 = 平移矩阵（shift matrix）的组合」，由此把梯度计算变得极其简单。</span>

---

<!-- page 389 -->
> <span style="color:#7f8c8d;">本页为书页 387，属 VII.2 的开篇，交代卷积神经网络（CNN）与之前全连接网络在结构上的根本区别，并引入一维卷积与平移矩阵的概念；页眉与印页码不译。</span>

本节讨论的是具有**不同 architecture（架构）**的网络。到目前为止，每一层都与下一层 fully connected（全连接）。若某一层有 $n$ 个神经元、下一层有 $m$ 个神经元，则连接这两层的矩阵 $A$ 是 $m \times n$ 的，$A$ 中有 $mn$ 个 independent weights（独立权重）。所有层的权重都要被选择，使最终输出与训练数据相匹配；该优化所需的 derivatives（导数）由 backpropagation（反向传播）算出。而现在，每层可能只有 3 个或 9 个独立权重。

那种全连接网络用于图像识别将极度低效。首先，权重矩阵 $A$ 会极其庞大。若一幅图像有 $200 \times 300$ 个像素，则其输入层有 $60{,}000$ 个分量，而第一个隐藏层的权重矩阵 $A_1$ 有 $60{,}000$ 列。问题在于：我们一直在寻找相距遥远的像素之间的联系，而几乎在所有情况下，图像中的重要连接都是**局部**的。

- 文本与音乐具有一维（1D）局部结构：即一个 time series（时间序列）。
- 图像具有二维（2D）局部结构：红-绿-蓝三份拷贝。
- 视频具有三维（3D）局部结构：一个时间序列中的一帧帧图像。

更重要的是，对结构的搜寻在图像的每个位置本质上都是相同的。通常没有任何理由对文本、图像或视频的某一部分与其它部分区别对待。我们可以在所有位置使用同样的权重：即 **share the weights（权值共享）**。这种像素之间局部连接的神经网络是 shift-invariant（平移不变）的：处处相同。

其结果就是独立权重的数量大幅下降。假设每个神经元只连接到下一层的 $E$ 个神经元，且这些连接对所有神经元都相同，那么这两层之间的矩阵 $A$ 只有 $E$ 个独立权重 $c$。对这些权重的优化就会变得快得多。现实中我们有时间创建若干个不同的 channel（通道），各自带有自己的 $E$ 或 $E^2$ 个权重，它们可以在不同方向（水平、垂直、对角）寻找 edge（边缘）。

在一维情形下，一个带状（banded）平移不变矩阵就是一个 Toeplitz matrix（托普利茨矩阵），也即一个 filter（滤波器）。用该矩阵 $A$ 作乘法即是一次 convolution（卷积） $c * v$。所有层之间的这种连接网络就是一个 Convolutional Neural Net（卷积神经网络，简称 CNN 或 ConvNet）。此处 $E = 3$。

[[FIGURE: 书页 387, 一维卷积示意图：$N+2$ 个输入、$N$ 个输出，每个神经元连接左右邻近神经元，$Y=Av$]]

把 $A$ 看作三个 shift matrices（平移矩阵）$L, C, R$（Left 左、Center 中、Right 右）的组合是很有价值的：

```math
A = c_1 L + c_0 C + c_{-1} R
```

每个平移矩阵都有一条由 1 构成的对角线。于是 $y = Av = c_1 L v + c_0 C v + c_{-1} R v$ 的导数变得格外简单：

```math
\frac{\partial y}{\partial c_1} = Lv,\qquad
\frac{\partial y}{\partial c_0} = Cv,\qquad
\frac{\partial y}{\partial c_{-1}} = Rv \tag{1}
```

> <span style="color:#27ae60;">**译者注（为何卷积的梯度如此简单）**：把卷积矩阵 $A$ 拆成平移矩阵的线性组合 $A = c_1 L + c_0 C + c_{-1} R$，是本节最关键的代数洞见。因为 $L, C, R$ 是只含 0/1 的固定矩阵，而权重 $c_i$ 只是这些固定矩阵前的标量系数，所以 $A$ 对每个权重 $c_i$ 的偏导 $\partial A/\partial c_i$ 就等于那个平移矩阵本身——不再有任何「对矩阵逐项求导」的麻烦。对线性映射 $y = Av$ 而言，$\partial y/\partial c_i = (\partial A/\partial c_i) v = S_i v$，其中 $S_i \in \{L,C,R\}$。这正是公式 (1) 所写。全连接网络中每个权重都单独出现一次，导数必须逐项回传；而卷积网络里权重被共享，每个 $c_i$ 同时作用于整条信号，其梯度只是「把信号平移一次」这种廉价操作。这一化简使得 SGD 中反复求梯度变得可以承受，也是 CNN 能训练得很深的结构性原因。</span>

---

<!-- page 390 -->
> <span style="color:#7f8c8d;">本页为书页 388，把卷积推广到二维（图像），说明 2D 卷积是 9 个平移的线性组合、其 9 个导数在反向传播中计算，并阐释卷积的 operational meaning（运算意义）；页眉与印页码不译。</span>

### 二维卷积（Convolutions in Two Dimensions）

当输入 $v$ 是一幅图像时，卷积 $c * v$ 变成二维的。系数 $c_{-1}, c_0, c_1$ 变成 $E^2 = 3^2 = 9$ 个独立权重。输入 $v_{ij}$ 带两个下标，$v$ 代表 $(N+2)^2$ 个像素；除非在边界做 zero-padding（零填充），否则输出只有 $N^2$ 个像素。二维卷积 $c * v$ 是 9 个平移的线性组合。

- 输入图像 $v_{ij}$，$i,j$ 从 $(0,0)$ 到 $(N+1, N+1)$
- 输出图像 $y_{ij}$，$i,j$ 从 $(1,1)$ 到 $(N,N)$
- 权重 $c_{00}, \dots, c_{-1,-1}$
- 平移 $L, C, R, U, D$ = Left 左、Center 中、Right 右、Up 上、Down 下

```math
A = c_{11}LU + c_{01}CU + c_{-1,1}RU + c_{10}LC + c_{00}CC + c_{-1,0}RC + c_{1,-1}LD + c_{0,-1}CD + c_{-1,-1}RD
```

这把卷积矩阵 $A$ 表示为 9 个平移的组合。输出 $y = Av$ 的导数同样格外简单。我们利用这 9 个导数来构造 stochastic gradient descent（随机梯度下降）所需的梯度 $\nabla F$ 与 $\nabla L$，以改进权重 $c_k$。下一次迭代的 $c_k$ 会拥有能更好地匹配训练数据正确输出的权重。

$y = Av$ 的这 9 个导数在 backpropagation（反向传播）内部计算：

```math
\frac{\partial y}{\partial c_{11}} = LU\,v,\quad \frac{\partial y}{\partial c_{01}} = CU\,v,\quad
\frac{\partial y}{\partial c_{-1,1}} = RU\,v,\quad \dots\quad
\frac{\partial y}{\partial c_{-1,-1}} = RD\,v \tag{2}
```

CNN 可以轻松承担 $B$ 个 parallel channels（并行通道），且 $B$ 可以随网络加深而变化。权重 $c$ 的数量因 weight sharing（权值共享）与 weight locality（权值局部性）而大幅减少，以至于我们既不需要、也不能指望单单一组 $E^2 = 9$ 个权重就完成卷积网络的全部工作。

让我强调卷积的**运算意义**。在一维情形下，形式上的代数定义 $y_j = \sum_k c_{j-k} v_k$ 涉及对 $v$（或 $c$）做一次「flip（翻转）」。这正是造成困惑的源头，而我们并不需要它。我们改为考察整个信号（一维中）的左右平移 $L$、$R$，以及二维中的上下平移 $U$、$D$。每个平移都是一个对角线全为 1 的矩阵，这样我们就不用再去记翻转后的下标了。

- 一个 convolution（卷积）是平移矩阵的组合（产生一个 filter 滤波器或 Toeplitz matrix 托普利茨矩阵）。
- 一个 cyclic convolution（循环卷积）是循环平移的组合（产生一个 circulant matrix 循环矩阵）。
- 一个 continuous convolution（连续卷积）是平移的连续组合（一个积分）。

在深度学习中，组合中的系数就是待学习的「权重」。

> <span style="color:#27ae60;">**译者注（卷积的「翻转」与平移视角）**：教科书里卷积常写成 $y_j = \sum_k c_{j-k} v_k$，其中 $c$ 的下标被「翻转」了（取 $j-k$），这与信号处理中的相关（correlation）容易混淆。本书作者刻意回避这个翻转约定，而把卷积重新定义为「把整条信号向左、右平移，再按权重相加」。这样做的好处是：权重 $c_i$ 直接就是「平移 $i$ 格的幅度」，物理意义一目了然；更重要的是，如上一页译者注所说，每个权重对应的导数就是一次平移，梯度不再需要处理翻转下标。三种卷积（普通、循环、连续）其实是同一个想法的三个层次：普通卷积用有限个平移（有限滤波器），循环卷积用循环平移（对应循环矩阵，可被 DFT 对角化，见 IV.2），连续卷积则把平移连续化成一个积分。理解了「卷积 = 平移的组合」，三者就统一了。</span>

---

<!-- page 391 -->
> <span style="color:#7f8c8d;">本页为书页 389，进入 CNN 真正的成功领域——图像识别，介绍块托普利茨结构、高斯平滑滤波器与梯度检测滤波器；页眉与印页码不译。</span>

### 二维卷积网络（Two-dimensional Convolutional Nets）

现在我们来到 CNN 真正成功之处：image recognition（图像识别）。ConvNets 与深度学习在计算机视觉领域引发了一场小革命，应用遍及自动驾驶汽车、无人机、医学成像、安防、机器人——看不到止境。我们关心的，是使这一切成为可能的代数、几何与直觉。

在二维（图像）情形下，矩阵 $A$ 是 block Toeplitz（块托普利茨）的，每个小块是 $E \times E$。这是计算工程中常见的一种结构。待优化的独立权重个数 $E^2$ 远小于全连接网络的情形；同样的权重被用于所有像素周围（平移不变性）。该矩阵产生一个二维卷积 $c * v$，$A$ 也常被称作一个 filter（滤波器）。

要理解一幅图像，就要看它在哪里发生变化，找到它的 edge（边缘）。我们的眼睛会寻找锐利的截断与陡峭的 gradient（梯度），计算机也可以通过构造一个滤波器来做同样的事。一个 smooth function（光滑函数）与一个移动的滤波器窗口之间的 dot product（点积）会是光滑的；但当图像中的一条边与一个「对角墙」对齐时，我们会看到一个尖峰。这些点积「（固定图像）·（移动图像）」恰好就是两幅图像的「卷积」。

二维及以上情形的难点在于：边缘可以有很多方向。对于测试图像，我们需要水平、垂直、对角的滤波器；而且滤波器用途多样，包括 smoothing（平滑）、gradient detection（梯度检测）与 edge detection（边缘检测）。

**1. 平滑（Smoothing）** 对于一个二维函数 $f$，最自然的平滑器是与一个 Gaussian（高斯函数）的卷积：

```math
G f(x,y) = \left[ \frac{1}{2\pi\sigma^2} e^{-(x^2+y^2)/2\sigma^2} \right] * f(x,y)
= \left[ \frac{1}{\sqrt{2\pi}\sigma} e^{-x^2/2\sigma^2} \right]
  \left[ \frac{1}{\sqrt{2\pi}\sigma} e^{-y^2/2\sigma^2} \right] * f(x,y)
```

这展示了 $G$ 是一维平滑器的乘积。高斯函数处处为正，所以它是做平均：$G f$ 的最大值不可能超过 $f$ 的最大值。该滤波器去除 noise（噪声）（代价是损失锐利边缘）。当方差 $\sigma^2$ 很小时，细节会变得更清晰。

对于一个二维向量（矩阵 $f_{ij}$ 而非函数 $f(x,y)$），高斯必须离散化。由于矩阵 $G$ 是方阵，完美的 radial symmetry（径向对称）会丢失。下面是一个 $5\times 5$ 的离散高斯 $G$（$E=5$）：

```math
G = \frac{1}{273}
\begin{bmatrix}
1 & 4 & 7 & 4 & 1\\
4 & 16 & 26 & 16 & 4\\
7 & 26 & 41 & 26 & 7\\
4 & 16 & 26 & 16 & 4\\
1 & 4 & 7 & 4 & 1
\end{bmatrix}
\quad\approx\quad
\frac{1}{289}
\begin{bmatrix}
1 & 4 & 7 & 4 & 1
\end{bmatrix}^{T}
\begin{bmatrix}
1 & 4 & 7 & 4 & 1
\end{bmatrix}
\tag{3}
```

我们也丢失了「一维滤波器精确乘积」这一性质。为了更接近，可用更大的矩阵 $G = c\,c^{T}$，其中 $c = (.006, .061, .242, .383, .242, .061, .006)$，并丢弃外侧的微小像素。

**2. 梯度检测（Gradient detection）** 图像处理（区别于 CNN 的学习）需要能检测梯度的滤波器，它们包含特意选定的权重。我们列举几个简单的滤波器，只为说明它们如何求梯度——即 $f$ 的一阶导数。

> <span style="color:#27ae60;">**译者注（高斯核的可分离性与离散化的代价）**：二维高斯核有一个极其省算力的性质——可分离性（separability）：$e^{-(x^2+y^2)/2\sigma^2} = e^{-x^2/2\sigma^2} \cdot e^{-y^2/2\sigma^2}$，于是二维卷积等于先对行、再对列各做一次一维卷积，计算量从 $O(E^2)$ 降到 $O(E)$。但一旦把函数离散成方阵，这个「行向量×列向量」的秩 1 分解就只是近似：正文把 $5\times 5$ 核写成 $[1,4,7,4,1]^T [1,4,7,4,1]$ 时，$41 \neq 7 \cdot 7 = 49$，即中心点对不上，这正是「丢失精确乘积」的直观体现。真正的离散高斯核可以通过反复与 $[1,2,1]$（二项式核）卷积来逼近，随阶数升高越来越接近各向同性。理解「连续核可分离、离散化后只能近似」这一落差，是读懂 (3) 式两套数字（273 与 289）为何不一致的关键。</span>

---

<!-- page 392 -->
> <span style="color:#7f8c8d;">本页为书页 390，给出梯度检测的 Sobel 算子、边缘检测的 Laplacian of Gaussian，并引入卷积滤波器的 stride（步长）概念；页眉与印页码不译。</span>

**一维情形** 卷积形式下：

```math
A v \quad\text{由}\quad \left[\, \tfrac12, 0, -\tfrac12 \,\right] \text{（中心差分核）产生}
```

此时 $Av$ 的分量是 centered differences（中心差分）：

```math
(Av)_i = \tfrac12 v_{i+1} - \tfrac12 v_{i-1}
```

当 $v$ 的分量从左到右线性增长时，滤波器的输出是 $3(i+1)$——即正确的梯度。$\tfrac12$ 处的 flip 来自卷积的定义 $y_j = \sum_k c_{j-k} v_k$。

**二维情形** 这些 $3\times 3$ 的 Sobel operators（索贝尔算子）近似 $\partial/\partial x$ 与 $\partial/\partial y$：

```math
S_x =
\begin{bmatrix}
-1 & 0 & 1\\
-2 & 0 & 2\\
-1 & 0 & 1
\end{bmatrix},\qquad
S_y =
\begin{bmatrix}
-1 & -2 & -1\\
0 & 0 & 0\\
1 & 2 & 1
\end{bmatrix}
\tag{4}
```

对于函数，梯度向量 $g = \nabla f$ 的模长为 $\sqrt{|\partial f/\partial x|^2 + |\partial f/\partial y|^2}$。这些权重是为图像处理而设计的，用于定位典型图像最重要的特征——它的 edges（边缘）。它们可以成为二维卷积矩阵 $A$ 内部 $E\times E$ 滤波器的候选。但要记住：在深度学习中，$\tfrac12$ 与 $-5$ 这类权重不是用户选择的，而是从训练数据中生成的。

本书 IV.2 与 IV.5 节研究了循环卷积与托普利茨矩阵，平移不变性引出了 discrete Fourier transform（离散傅里叶变换）的应用。但在 CNN 中，ReLU 很可能作用于每个神经元，网络还可能包含 zero-padding（零填充）以及 max-pooling（最大池化）层，所以我们不能指望运用傅里叶分析的全部威力。

**3. 边缘检测（Edge detection）** 估计出梯度方向后，我们寻找边缘——最有价值的知识特征。「Canny Edge Detection（Canny 边缘检测）」是一个高度成熟的流程。现在我们不想要会模糊边缘的平滑，好的滤波器是 Laplacians of Gaussians（高斯函数的拉普拉斯，LoG）：

```math
\nabla^2 [G_\sigma * f] = [\nabla^2 G_\sigma] * f(x,y)
```

高斯函数的拉普拉斯 $\nabla^2 G$ 为：

```math
\nabla^2 G_\sigma(x,y) = \frac{1}{\sigma^4} \left(x^2 + y^2 - 2\sigma^2\right) e^{-(x^2+y^2)/2\sigma^2}
\tag{5}
```

### 卷积滤波器的步长（The Stride of a Convolutional Filter）

**重要**：迄今描述的滤波器步长都是 $S = 1$。步长更大时，移动窗口在图像上跨过图像时每步迈得更远。下面是一个一维、3 权重、stride（步长）为 2 的滤波器的矩阵 $A$。尤其注意：输出 $y = Av$ 的长度被因子 2 缩短了（原来四个输出，现在只有两个）。

```math
A =
\begin{bmatrix}
c_{-1} & c_0 & c_1 & 0 & 0 & 0 & \cdots\\
0 & 0 & c_{-1} & c_0 & c_1 & 0 & \cdots\\
\vdots & & & & & & \ddots
\end{bmatrix}
\quad\text{(Stride } S = 2\text{)}
\tag{6}
```

现在，$L$ 中那样的非零权重相隔两列（步长为 $S$ 时相隔 $S$ 列）。在二维中，步长 $S = 2$ 使每个方向都缩小为原来的 $\tfrac12$，整个输出缩小为 $\tfrac14$。

> <span style="color:#27ae60;">**译者注（Sobel 算子与「中心差分 + 平滑」的分工）**：Sobel 算子可以拆成两个一维核的外积：$S_x = [-1,0,1]^T \cdot [1,2,1]$，$S_y = [1,2,1]^T \cdot [-1,0,1]$。其中 $[-1,0,1]$ 是上一行的中心差分核（求一阶导），$[1,2,1]$ 是二项式平滑核。也就是说 Sobel 本质是「先在一个方向做差分、在正交方向做平滑」，既抑制了噪声又保留了方向性——这正是「梯度检测」比裸差分更稳健的原因。而 LoG（Laplacian of Gaussian）则相反：先平滑后求二阶导 $\nabla^2$，它在边缘处出现「过零点」（zero crossing），所以 LoG 找边缘是靠找符号翻转，而非找极值。这条「平滑 ↔ 微分」的组合线索贯穿本页三个小节，理解了它，三者就不再是孤立的滤波器清单。</span>

---

<!-- page 393 -->
> <span style="color:#7f8c8d;">本页为书页 391，讨论如何通过零填充、环绕、反射等边界延拓保持输出尺寸，并引出 filter bank（滤波器组）与小波（wavelets）；页眉与印页码不译。</span>

### 延拓信号（Extending the Signal）

当 $A$ 不是方阵时，与其在图像边缘丢失神经元，我们可以延拓输入层——在图像边界之外「虚构」一些分量，使输出 $y = Av$ 与图像块等尺寸：输入输出维数相等。

最简单也最流行的方法是 zero-padding（零填充）：把全部新增分量取为零。$A$ 左右两侧多出来的列乘的就是这些零；中间则是一个方形的 Toeplitz matrix（托普利茨矩阵），如 IV.5 节所述。它仍然由远比 $A$ 中元素个数少得多的权重所决定。

对于 periodic signals（周期信号），零填充被 wraparound（环绕）取代：托普利茨矩阵变成 circulant（循环矩阵，见 IV.2 节），其 eigenvalues（特征值）由离散傅里叶变换给出，eigenvectors（特征向量）恒为傅里叶矩阵的列。此时乘法 $Av$ 是一次循环卷积，Convolution Rule（卷积定理）适用。

更精确的做法是用 reflection（反射）越过边界：若信号的最后一个分量是 $v_N$，而矩阵需要 $v_{N+1}$ 与 $v_{N+2}$，我们可以复用 $v_N$（否则就用 $v_{N-1}$ 与 $v_{N-2}$）。无论 $v$ 的长度和 $A$ 的尺寸如何，$A$ 的所有元素都来自同一组 $E$ 个权重（$c_{-1}$ 到 $c_1$，或 $c_{-2}$ 到 $c_2$；二维中为 $E^2$ 个）。

**另一个想法**：我们也可以接受原始维度（例中为 128），并把「缩减到 64」当作应用两个滤波器 $C_1$ 与 $C_2$ 的方式。每个滤波器输出从 128 下采样到 64，总样本数仍为 128。若两个滤波器足够独立，则没有信息丢失，原始的 128 个值可以被恢复。这一过程是线性的：两个 $64\times 128$ 矩阵合并成一个 $128\times 128$ 的方阵；若该矩阵如我们所愿可逆，则这个 filter bank（滤波器组）是 lossless（无损）的。

这正是 CNN 通常的做法：增加更多通道的权重矩阵 $A$，以捕获训练样本的更多特征。神经网络拥有 $B$ 个滤波器的 bank（库）。

### 滤波器组与小波（Filter Banks and Wavelets）

上一段的思路产生了一个 filter bank（滤波器组），它不过是一组 $B$ 个不同的滤波器（卷积）。在信号处理中，一个重要情形是把一个 lowpass filter（低通滤波器）$C_1$ 与一个 highpass filter（高通滤波器）$C_2$ 组合起来：$C_1 v$ 的输出是一个平滑信号（以低频为主），$C_2 v$ 的输出以高频为主。理想的 perfect cutoff（完美截止）不可能由有限矩阵 $C_1$、$C_2$ 实现。

两个滤波器共给出 256 个输出分量，随后两者都被 subsample（下采样），得到 128 个分量，大致分为 averages（平均）与 differences（差分）——即低频与高频。该矩阵是 $128\times 128$。

**小波（Wavelets）** 小波的思路是：对低通输出的 64 个分量重复同样的步骤，于是 $(\downarrow 2) C_1 (\downarrow 2) C_1 v$ 是「平均的平均」，其频率集中在全部频率的最低四分之一（$|\omega| \le \pi/4$）；中频输出 $(\downarrow 2) C_2 (\downarrow 2) C_1 v$ 有 32 个分量，不再细分。于是 $128 = 64 + 32 + 16 + 16$。

在无限细分的极限下，小波就登场了。这种「低-高频分离」是信号处理的重要主题，对深度学习则不那么重要；但在 CNN 的多通道结构中，频率分离可能会有效。

> <span style="color:#27ae60;">**译者注（边界延拓的三种方式与循环矩阵的特征结构）**：为了让卷积输出与输入等长，必须「补」出边界外的值，三种补法各对应一种矩阵结构：(1) 零填充（zero-padding）对应托普利茨矩阵，实现最简单，但人为引入阶跃、会产生边界伪影；(2) 环绕（wraparound）对应循环矩阵，它恰好能被 DFT 对角化，因此 $Av$ 的谱完全由卷积核的傅里叶系数决定，这正是 IV.2 节「循环卷积 + 卷积定理」的落地；(3) 反射（reflection）最贴合图像自然边界（对称延拓），是 JPEG2000 等压缩标准偏爱的方式。三者背后其实是同一个问题——「非方阵的 $A$ 如何补成方阵而不失信息」。而滤波器组/小波的思路，正是把「低通 + 高通 + 下采样」反复套在低频分支上，把信号按频段一层层拆开，这也是多分辨率分析（MRA）的核心，与 CNN 的多通道思想同源。</span>

---

<!-- page 394 -->
> <span style="color:#7f8c8d;">本页为书页 392，给出计算卷积层输入输出维数的 Karpathy 公式，并介绍 Simonyan 与 Zisserman 的深度卷积网络（VGG）；页眉与印页码不译。</span>

### 计算输入与输出的个数（Counting the Number of Inputs and Outputs）

在一维问题中，设某层有 $N$ 个神经元，我们应用一个带 $E$ 个非零权重的卷积矩阵，stride（步长）为 $S$，并在输入信号两端各 pad（填充）$P$ 个零。这个滤波器产生多少个输出（$M$ 个数）？

**Karpathy 公式：**

```math
M = \frac{N - E + 2P}{S} + 1
\tag{7}
```

在二维或三维问题中，这个一维公式在每个方向上都适用。

设 $E = 3$、步长 $S = 1$。若在每端各加一个零（$P = 1$），则：

```math
M = N - 3 + 2 + 1 = N \quad(\text{输入长度} = \text{输出长度})
```

这种 $2P = E - 1$、步长 $S = 1$ 的情形是 CNN 最常见的架构。若不在输入中填零，则 $P = 0$，$M = N - 2$（如本节开头的 $4\times 6$ 矩阵 $A$）。在二维中这变为 $M^2 = (N - 2)^2$。这样我们会损失神经元，但避免了零填充。

现在设步长 $S = 2$。此时 $N - E$ 必须是偶数，否则公式 (7) 会产生分数。下面是步长 $S = 2$ 成功的两个例子，取 $N - E = 5 - 3 = 2$，五个输入的两端分别取 $P = 0$ 或 $P = 1$：

```math
P = 0:\quad M = \frac{5 - 3 + 0}{2} + 1 = 2;\qquad
P = 1:\quad M = \frac{5 - 3 + 2}{2} + 1 = 3
```

同样，我们的计数在每个方向上都适用于二维图像或张量。

### 深度卷积网络（A Deep Convolutional Network）

识别图像是深度学习的一项主要应用（也是一大成功），成功来自 AlexNet 的诞生与卷积网络的发展。本页将描述一个用于图像识别的、由局部卷积矩阵构成的深度网络。我们遵循 Simonyan 与 Zisserman 在 ICLR 2015 上的获奖论文，该论文推荐 $L = 16\text{--}19$ 层、小（$3\times 3$）滤波器的深度架构。网络具有 $B$ 个并行通道的宽度（每层 $B$ 幅图像）。

若所有层的宽度 $B$ 保持不变，且所有滤波器都有 $E\times E$ 的局部权重，那么一个直截了当的公式可估计网络中的权重数 $W$：

```math
W \approx L B E^2 \qquad(L\ \text{层},\ B\ \text{通道},\ E\times E\ \text{局部卷积})
\tag{8}
```

注意 $W$ 不依赖每层的神经元个数，因为无论 $A$ 尺寸多大，它都只有 $E^2$ 个权重。Pooling（池化）会改变那个尺寸，却不改变 $E^2$。但通道数 $B$ 会变——而且以 fully-connected layers（全连接层）收尾 CNN 十分常见，这将彻底改变权重数 $W$！

> <span style="color:#27ae60;">**译者注（Karpathy 公式的几何意义与 $W$ 为何与神经元数无关）**：公式 $M = (N - E + 2P)/S + 1$ 可以用一个滑动窗口来理解：一个长 $E$ 的窗口在长 $N$（两端各加 $P$ 的填充后实际长 $N+2P$）的信号上滑动，每步跨 $S$，它所能占的「合法起点」个数就是输出长度 $M$。$N+2P - E$ 是窗口能滑动的总余地，除以步长 $S$ 得到步数，再加 1 得到起点数。这个式子也解释了为什么「$2P = E - 1$ 且 $S = 1$ 时输出恰好等于输入 $N$」——因为填充正好把窗口「顶到」能覆盖首尾像素。而 (8) 式的 $W \approx LBE^2$ 之所以不含每层神经元数，正是权值共享的精髓：不管这一层有多少个神经元，它们共用的都是同一个 $E\times E$ 卷积核，参数只随「层数 × 通道数 × 核大小」增长，而不随特征图尺寸增长。这正是一页之前反复强调的「平移不变 ⇒ 权值共享」带来的数量级削减。</span>

---

<!-- page 395 -->
> <span style="color:#7f8c8d;">本页为书页 393，讨论 Simonyan–Zisserman 的架构决策（偏好小 $3\times 3$ 滤波器）与多分类网络的 Softmax 输出；页眉与印页码不译。</span>

值得讨论 Simonyan 与 Zisserman 所做的决策及其它选项。他们的选择得到 $W \approx 135{,}000{,}000$ 个权重，计算在四块 NVIDIA GPU 上进行，训练一个网络要 2–3 周。读者可能算力更少（问题也更小），于是会把超参数 $L$ 与 $B$ 调小。我们相信重要的原则依然不变。

这里的一个关键点是：建议减小局部卷积的尺寸 $E$。$5\times 5$ 与 $7\times 7$ 的滤波器都被否决了。事实上，一个 $1\times 1$ 的卷积层可以作为一种引入额外一组 ReLU 的方式——正如接下来要讲的 ResNets 那样。

作者们比较了「三个各带 $3\times 3$ 滤波器的卷积层」与「单个局部性更弱的 $7\times 7$ 卷积层」：前者是 27 个权重对 49 个权重，三个非线性层对一个非线性层。两种情况下，单个数据点的影响都会在图像（或 RGB 图像，$B = 3$）中向水平和垂直方向各传播到三个邻居。他们偏爱 $3\times 3$ 滤波器以及每层更多神经元带来的额外非线性。

### 多分类网络的 Softmax 输出（Softmax Outputs for Multiclass Networks）

识别数字时我们有 10 个可能输出；识别字母及其它符号时是 26 个或更多。当有多个输出类别时，我们需要一个恰当的方法来确定最后一层（即从 $v$ 开始的神经网络中的输出层 $w$）。「Softmax」取代了 logistic regression（逻辑回归）的两输出情形，把 $n$ 个数转化为概率。

输出 $w_1, \dots, w_n$ 被转化为和为 1 的概率 $p_1, \dots, p_n$：

```math
p_j = \frac{e^{w_j}}{S},\qquad S = \sum_{k=1}^{n} e^{w_k}
\tag{9}
```

Softmax 当然会把最大的概率 $p_j$ 赋给最大的输出 $w_j$。但 $e^{w}$ 是 $w$ 的非线性函数，所以 softmax 的赋值对 scale（缩放）不不变：若把所有输出 $w_j$ 加倍，softmax 会产生不同的概率 $p_j$。对于较小的 $w$，softmax 实际上会**弱化**最大的那个数 $w_{\max}$。

在 teachyourmachine.com 识别数字的 CNN 例子中，你会看到 softmax 如何产生用 pie chart（饼图）显示的概率——一个极佳的可视化辅助。

**CNN** 我们需要大量权重来拟合数据，并且为能（借助梯度下降）算出它们而自豪；但若权重可以被复用，就没有理由让权重数量大到无用。对于一维的长信号、尤其是二维的图像，我们可能没有任何理由逐像素改变权重。

**参考文献**

1. (karpathy@cs.stanford.edu) cs231n.github.io/convolutional-networks/
2. K. Simonyan and A. Zisserman, *Very deep convolutional networks for large-scale image recognition*, ICLR (2015), arXiv:1409.1556v6, 10 Apr 2015.
3. A. Krizhevsky, I. Sutskever, and G. Hinton, *ImageNet classification with deep convolutional neural networks*, NIPS (2012) 1106–1114.
4. Y. LeCun and Y. Bengio, *Convolutional networks for images, speech, and time-series*, Handbook of Brain Theory and Neural Networks, MIT Press (1998).

> <span style="color:#27ae60;">**译者注（Softmax 为何对缩放敏感，以及「小核堆叠」的等价性）**：Softmax $p_j = e^{w_j}/\sum_k e^{w_k}$ 把无界的 logits 压成和为 1 的概率。它对平移不变（$w_j$ 同时加常数 $c$，分子分母同时乘 $e^c$，$p_j$ 不变），但对缩放不不变：因为 $e^{w}$ 是凸函数，$w$ 整体放大 $\alpha$ 倍后，较大的 $w_j$ 之间的指数差距被放大，概率分布变得更「尖锐」（更接近 one-hot）；反之 $\alpha \to 0$ 时分布趋近均匀。这就是「加倍所有输出会产生不同概率」的根本原因，也是为什么 softmax 前常加一个 temperature（温度）参数来调节置信度。另一方面，正文比较「3 层 $3\times 3$」与「1 层 $7\times 7$」：三层 $3\times 3$ 的感受野（receptive field）逐层叠加后正好也是 $7\times 7$，但只用了 $3 \times 3 \times 3 = 27$ 个权重（对 49 个），且夹了三次 ReLU 非线性——在同等感受野下，参数更少、表达力更强。这正是 VGG 坚持小核的核心论证。</span>

---

<!-- page 396 -->
> <span style="color:#7f8c8d;">本页为书页 394，介绍最后一层的支持向量机（SVM）形式，并以 AlphaGo 战胜李世石为例说明深度卷积网络的自学习能力；页眉与印页码不译。</span>

### 最后一层的支持向量机（Support Vector Machine in the Last Layer）

在计算机视觉的 CNN 中，最后一层常有特殊形式。若前面的层使用 ReLU 与 max-pooling（两者都是 piecewise linear，分段线性的），最后一步可以变成一个 difference-of-convex program（凸差规划），最终成为一个 multiclass Support Vector Machine（多分类支持向量机，SVM）。于是，分段线性 CNN 中权重的优化可以逐层进行。

> L. Berrada, A. Zisserman, and P. Kumar, *Trusting SVM for piecewise linear CNNs*, arXiv:1611.02185, 6 Mar 2017.

### 围棋世界冠军之战（The World Championship at the Game of Go）

深度卷积网络的一次戏剧性成就是击败了（人类）围棋世界冠军。这是在一张 $19\times 19$ 棋盘上进行的困难游戏，两名棋手轮流落「子」，试图围住对方的棋子；当某一颜色的一个棋块四周（左、右、上、下）没有空位时，这些棋子就被从棋盘上提走。维基百科有动画演示。

AlphaGo 在 2016 年以 4 比 1 击败顶尖棋手李世石（Lee Sedol），它曾在成千上万局人类对局上训练。这是一场令人信服但并非压倒性的胜利。随后神经网络被加深、改进，Google 的新版本 AlphaGo Zero 学会了无需任何人类干预地弈棋——纯粹靠自我对弈，如今它以 100 比 0 击败了它的前身 AlphaGo。

这个更新、更好版本的关键点在于：机器是**靠自己**学会的，它只被告知规则，别无其它。第一个版本曾被喂入历史棋局，旨在发现胜者为何胜、败者为何败。新方法的成果与机器翻译语言的情形如出一辙：要掌握一门语言，语法中的特例似乎必不可少，否则如何学会那么多例外？Google 的翻译团队曾告诉系统它需要知道什么；与此同时，另一个小团队采取了不同方法——让机器自己摸索。无论在围棋还是在语言翻译上，成功都来自更深的神经网络、更多的对局、以及零人工指导。

我们在此感兴趣的是 AlphaGo Zero 的深度与架构。超参数将在 VII.4 节（fateful decisions，命运攸关的决策）中出现；Google Translate 的平行历史则须等到 VII.5 节，因为需要 Recurrent Neural Networks（循环神经网络，RNN）来捕获文本的 sequential structure（序列结构）。

有趣的是，机器常常下出人类很少甚至从未选择过的开局着法。网络的输入是棋盘位置及其历史；输出向量给出选择每一步棋的概率，同时还有一个标量，估计从该位置获胜的概率。每一步都与一个 Monte Carlo tree search（蒙特卡洛树搜索）通信，以产生 reinforcement learning（强化学习）。

> <span style="color:#27ae60;">**译者注（从监督学习到强化学习：AlphaGo 两次范式转变）**：AlphaGo 第一版是「监督学习 + 强化学习」混合体——先用人类棋谱训练策略网络（学「高手怎么下」），再用自我对弈微调。AlphaGo Zero 则彻底去掉人类棋谱，只给规则，靠「策略网络 + 价值网络 + 蒙特卡洛树搜索」三者循环自举。这里「输出向量给每步概率、标量给胜率」正对应两个网络：前者是策略（policy），后者是价值（value）。这与正文反复强调的「权重从训练数据中生成、而非人工设定」一脉相承——只不过 Zero 把「训练数据」也换成了自己生成的对局。翻译与围棋的平行之处在于：早期范式都靠人工注入「例外规则/棋谱」，而深度网络够深后，端到端地「让机器自己摸索」反而更强，这正是深度学习的范式胜利。至于 SVM 最后一层：ReLU 与 max-pooling 都是分段线性映射，所以整个网络是 $v$ 的分段线性函数，其损失可在每个线性区域内局部视作凸差规划（DC）来求解，这解释了「为何能逐层优化」。</span>

---

<!-- page 397 -->
> <span style="color:#7f8c8d;">本页为书页 395，介绍残差网络（ResNets）的 skip connection 如何对抗梯度消失，并以一个识别字母的简单 CNN 收尾本节；页眉与印页码不译。</span>

### 残差网络（Residual Networks, ResNets）

网络正变得越来深，隐藏层越来越多，其中大多是具有适中数量独立权重的卷积层。但深度会带来危险：信息可能「堵塞」而永远到不了输出端。vanishing gradients（梯度消失）问题可能很严重——传播得如此之远，做如此之多的乘法，结果是算出的梯度呈指数级地小。若设计得当，深度是件好事；但你必须为学习开辟向前流动的路径。

了不起的是，那些快速路径可以非常简单：即直接通往下一层的 skip connections（跳跃连接），绕过通常的一步

```math
x_{n+1} = \operatorname{ReLU}(A_n x_{n} - \mathbf{1} + b_n)
```

Veit、Wilber 与 Belongie 提出了一个高效方案：每一层要么走 skip、要么走普通卷积，且每次都跟一个 ReLU 步。若网络有 $L$ 层，就会有 $2^L$ 条可能路径——每层到下层的「快速」或「普通」二选一。

结果之一是：整层整层的层可以被移除而不产生显著影响。第 $n$ 层可由 $2^{n-1}$ 条可能路径到达，其中许多路径长度远小于 $n$（不计 skip）。

很难预测深度 ConvNets 是否会被 ResNets 取代。

> K. He, X. Zhang, S. Ren, and J. Sun, *Deep residual learning for image recognition*, arXiv:1512.03385, 10 Dec 2015. 该文通过添加跳过层、权重 $A = I$ 的 shortcut 来处理极深网络，否则深度会损害性能。
> K. He, X. Zhang, S. Ren, and J. Sun, *Identity mappings in deep residual networks*, arXiv:1603.05027, 25 Jul 2016.
> A. Veit, M. Wilber, and S. Belongie, *Residual networks behave like ensembles of relatively shallow networks*, arXiv:1605.06431, 27 Oct 2016.

### 一个简单的 CNN：学习读字母（A Simple CNN: Learning to Read Letters）

MIT 的一个课堂项目就是做一个卷积网络。用户先画多份（不很多）的 A 和 B，在这个训练集上，正确分类是用户输入的一部分。接下来是学习这些数据的神秘一步——创建一个 continuous piecewise linear（连续分段线性）函数 $F(v)$，它给正确答案（本意要写的那个字母）以高概率。

对于学习读数字，饼图中会出现 10 个概率。你很快会发现：训练集太小会导致频繁出错。若示例中的数字或字母是居中的、而测试图像不居中，用户就会明白那些错误为何出现。

teachyourmachine.com 的目的之一，是面向所有层次的机器学习教育（包括学校），每个读者都能使用。

以下参考文献把信号处理中极有原创性的想法应用于 CNN：

- R. Balestriero and R. Baraniuk, *Mad Max: Affine spline insights into deep learning*, arXiv:1805.06576.
- S. Mallat, *Understanding deep convolutional networks*, Phil. Trans. Roy. Soc. 374 (2016); arXiv:1601.04920.
- C.-C. J. Kuo, *The CNN as a guided multilayer RECOS transform*, IEEE Signal Proc. Mag. 34 (2017) 81–89; arXiv:1701.08481.

> <span style="color:#27ae60;">**译者注（ResNet 的指数路径与梯度消失）**：深层网络的反向传播要把 $\partial L/\partial x$ 一路乘上各层雅可比矩阵，若这些矩阵的谱半径普遍小于 1，乘积会随深度指数衰减——这就是「梯度消失」。ResNet 把每层改成 $x_{n+1} = \operatorname{ReLU}(x_n + F(x_n))$ 的残差形式，前向多了一条恒等捷径，反向时梯度就多了一条「沿恒等路径原样流回」的通道，等于给梯度装了一条高速公路，使其不再必然指数衰减。正文「$2^L$ 条路径」「第 $n$ 层由 $2^{n-1}$ 条路径到达」正是这个结构的组合学计数：每一层在「走卷积」与「走 skip」间二选一，故路径数随层数指数增长——这也解释了 Veit 等人「ResNet 像浅网络集成（ensemble）」的观点，因为总有一条捷径让信息以接近浅层的方式流动。末段「$F(v)$ 是连续分段线性函数」则把 ReLU 网络整体刻画为样条（spline），与前面「分段线性 ⇒ 可用 DC 规划/SVM」的讨论闭环。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么卷积层只有 $E$ 或 $E^2$ 个独立权重：**</span> 正文…本节一开头就把卷积层与全连接层做了一次鲜明的账目对比：若前一层有 $n$ 个神经元、后一层有 $m$ 个，全连接矩阵 $A$ 是 $m\times n$，携带 $mn$ 个独立权重；而卷积层的权重矩阵虽然形状仍是“大矩阵”，真正自由度的个数却只有 $E$（一维）或 $E^2$（二维）这么几个。这个数量级上的塌缩，来自两个彼此独立、却同时被图像特性所“逼出来”的假设。第一个是 **locality（局部性）**：一幅 $200\times300$ 的图像有 $6\times10^4$ 个输入分量，但我们根本不需要让每一个像素都和远处的每一个像素相连——图像里几乎所有的信息联系都是局部的，边缘、纹理、明暗变化都发生在邻近像素之间。第二个是 **weight sharing / shift-invariance（权值共享 / 平移不变性）**：图像里没有哪个位置比别处更“特殊”，同样的边缘检测器应当在图像的任意角落都适用，因此可以把同一组权重搬到每个位置反复使用。两条假设合起来，等于宣告“每个神经元只连接到下一层的 $E$ 个邻居，而且这套连接对所有神经元都一样”，于是整张矩阵 $A$ 只剩 $E$ 个真正可调的数。这回答的是“为什么这样定义”：不是人为地省参数，而是把图像的两种结构性先验——信息近邻、处处同质——直接翻译成了权重的约束，从而让梯度下降要优化的参数数量从数万级骤降到个位数，计算上也骤然加速。理解了这一点，后面“多通道（channels）各自带一组 $E$ 或 $E^2$ 权重去抓不同方向的边缘”的设计就是顺理成章的补充：单一组 $9$ 个权重做不了全部工作，于是用并行通道来补足表达能力。

> <span style="color:#1e8449;">**[note] 式 (1) 的导数为何“异常简单”，它等价于什么：**</span> 正文…正文在把卷积矩阵 $A$ 写成移位矩阵组合 $A=c_{-1}L+c_0C+c_{1}R$（左、中、右三个 shift 各有一条对角线上全为 1）之后，直接写出 $\partial y/\partial c_{-1},\partial y/\partial c_0,\partial y/\partial c_1$ 这一组导数，并强调它们“exceptionally simple”。这背后的机制值得点透：因为 $y=Av=c_{-1}Lv+c_0Cv+c_{1}Rv$ 对每一个权重 $c$ 都是**线性**的，所以 $\partial y/\partial c_k$ 恰好就是那个权重所对应的移位结果本身——比如 $\partial y/\partial c_{-1}=Lv$，$\partial y/\partial c_0=Cv$，$\partial y/\partial c_1=Rv$，完全不需要任何反向传播的链式迭代，直接“读出”即可。这正是把 $A$ 拆成移位基底的真正用意：它把“对权重的导数”转化成了“对信号的移位”，从而让反向传播（backpropagation）里最耗时的梯度计算退化为几次平移操作。一维如此，二维也如此：$A$ 是 $9$ 个移位 $L,C,R,U,D$ 等的线性组合，输出 $y=Av$ 对九个权重 $c_{ij}$ 的九个偏导同样是九次移位，把它们拼起来就得到随机梯度下降（stochastic gradient descent）所需的 $\nabla F$ 与 $\nabla L$，用来迭代更新权重。这里其实还暗含一个等价视角：与常见的代数定义 $y_j=\sum_k c_{j-k}v_k$（它要求记忆“翻转”下标）相比，用左右、上下移位矩阵来表述卷积，等于把“翻转”这件事从公式里彻底抹掉——卷积不再是一串容易记错的翻转下标，而是“若干平移的线性组合”，这就是作者反复强调“saves us from the complication of remembering flipped subscripts”的原因。

> <span style="color:#1e8449;">**[note] 与全书 IV.2 / IV.5 的联系，以及一个具体数值例子：**</span> 正文…这一节在好几个关键处都回头指向了本书前面讲过的内容，形成一条清晰的“先有线性代数工具、后有卷积网络”的线索。正文明确写道：零填充（zero-padding）之后，中间得到的是一块 **square Toeplitz matrix（方 Toeplitz 矩阵）**，这正是 Section IV.5 讨论的对象；而对周期信号改用“环绕”（wraparound）填充时，Toeplitz 矩阵就退化成 **circulant（循环矩阵）**，这正是 Section IV.2 的内容——循环矩阵的特征向量永远是 Fourier 矩阵的列，离散傅里叶变换给出它的特征值，于是 $Av$ 成为一个循环卷积，卷积定理（Convolution Rule）随之适用。换句话说，同一个 $Av$，在“零填充—Toeplitz—IV.5”和“周期环绕—circulant—IV.2”两种边界约定下，分别落进本书早已建立的两套线性代数框架里，这一节的卷积层并不是凭空出现的新对象，而是把旧工具换了个用法。用一个具体数值例子更能看清本节的“账目”：正文以 $E=3$、$S=1$ 为例，若在两端各补一个零（$P=1$），则输出长度 $M=N-3+2+1=N$，即输入输出等长——这是 CNN 最常见的架构；若完全不补零（$P=0$），则 $M=N-2$，对应本节开头那张 $4\times6$ 的矩阵 $A$，二维情形下输出变成 $(N-2)^2$。此外，正文用 Simonyan 与 Zisserman 的 VGG 网络给出的数字也很醒目：$L=16$–$19$ 层、$3\times3$ 小卷积的深层架构，用估算式 $W\approx LBE^2$ 数出约 $1.35\times10^8$ 个权重，却强调 $W$ 与每层的神经元个数**无关**（因为 $A$ 无论多大都只有 $E^2$ 个自由权重）——这个“参数数量与网络规模解耦”的事实，正是权值共享带来的、全连接网络永远做不到的特性。

---

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

---

> <span style="color:#7f8c8d;">本节承接损失函数与网络结构的选择，集中讨论训练算法的"旋钮"——超参数（hyperparameters）：步长（学习率）的选择、交叉验证、批归一化、Dropout，以及损失函数在平方损失与交叉熵之间的比较。作者反复强调：这些决定并不"自动"，而是深刻影响算法能否快速、准确、稳健地找到权重。</span>

---

<!-- page 409 -->

> <span style="color:#7f8c8d;">本页为书页 407，属 VII.4 开头，讨论超参数的意义，并聚焦第一个、也是最重要的超参数——梯度下降的步长（stepsize / learning rate）；页眉与印页码不译。</span>

在选定了损失函数（loss function）、确定了网络架构（network architecture）之后，仍然有一些至关重要的决定要做。我们必须选择**超参数**（hyperparameters）。它们支配着算法本身——也就是权重的计算。这些权重代表着计算机从训练集（training set）中学到的东西：如何根据输入中的特征（features）预测输出。

在机器学习里，这些决定包括超参数、损失函数、dropout 以及正则化（regularization）。

目标是找到那些能把 5 与 7、与 2 区分开来的模式——靠的是观察像素。超参数决定了这些模式被发现的**速度与准确程度**。梯度下降（gradient descent）中的步长 $s_k$ 首当其冲。这个数出现在迭代式

```math
x_{k+1} = x_k - s_k \nabla L(x_k)
```

或其某个变体之中：加速型（借助动量 momentum）、自适应型（ADAM），或是每一步 $k$ 都从训练数据里随机取一个 minibatch（小批量）的随机型。

"学习率"（learning rate）这个词常被用来代替"步长"。依作者不同，两者可能完全一致，也可能相差一个归一化因子。此外，也常用 $\theta_k$ 代替 $s_k$。

首先，我们讨论当只有一个未知量时的最优步长；然后，我们指出一条一般性的途径。最终，我们想要的是一个更快的决策。

1. 取 $s_k = 1/L''(x_k)$。牛顿法（Newton）用到 $L$ 的二阶导数。这个选择顾及了 $L(x)$ 在点 $x_k$ 附近 Taylor 级数（泰勒展开）中的二次项。结果是，牛顿法是**二阶**的：$x_{k+1}$ 中的误差正比于 $x_k$ 中误差的**平方**。在极小点 $x^{*}$ 附近，收敛很快。在更高维时，二阶导数变成 Hessian 矩阵（海森矩阵）$H(x) = \nabla^2 L(x_k)$。其规模等于权重（$x$ 的分量）的个数。为求 $x_{k+1}$，牛顿法要解一个大型方程组 $H(x_k)(x_{k+1} - x_k) = -\nabla L(x_k)$。梯度下降则用单个数 $1/s_k$ 来替代 $H$。

2. 用**线搜索**（line search）来决定 $s_k$。梯度 $\nabla L(x_k)$ 规定了这条线的方向。当前点就是这条线的起点。通过在线上各点处求 $L(x)$ 的值，我们找到一个近乎极小化的点——它就成为 $x_{k+1}$。线搜索是一个实用的想法。其中一种算法是**回溯**（backtracking），如第 VI.4 节所述。它把步长 $s$ 按一个常数因子不断缩小，直到 $L$ 的下降量与梯度的陡峭程度（同样在一个选定的因子之内）相一致为止。优化一次线搜索是一个被仔细研究过的一维问题。

但没有哪种方法是完美的。接下来我们看看一个不佳的步长 $s$ 会带来什么后果。

### 太小或太大（Too Small or Too Large）

我们需要认清学习率选择不当所造成的困难：

- **$s_k$ 太小**——那么梯度下降要花太久才能最小化 $L(x)$；许多步 $x_{k+1} = x_k - s_k \nabla L(x_k)$ 只带来微小的改进。
- **$s_k$ 太大**——我们在下降方向上越过了最佳点 $x_{k+1}$。梯度下降会在极小点 $x$ 附近来回跳。

<!-- page 410 -->

> <span style="color:#7f8c8d;">本页为书页 408，属 VII.4，给出学习率调整的策略（前大后小、学习率计划），并介绍交叉验证（cross-validation）及其思想来源；页眉与印页码不译。</span>

假设最初几步 $s_0$ 与 $s_1$ 由线搜索找到，且效果良好。我们或许希望在早期迭代中保持这个学习率。通常，随着 $L(x)$ 的最小化继续进行，我们会把 $s$ 调小。

- **开始时步长大些**——接近最优权重 $x^{*}$ 的附近；
- **结束时步长小些**——力求收敛而不越过。

一个学习率计划（learning rate schedule）$s_k = s_0/\sqrt{k}$ 或 $s_k = s_0/k$ 会有系统地缩小步长。

在达到接近最小化损失函数 $L(x, v)$ 的权重 $x$ 之后，我们或许想从验证集（validation set）引入新的 $v$。这还不是生产模式（production mode）。交叉验证的目的是确认：算出的权重 $x$ 能够从新数据里产生准确的输出。

### 交叉验证（Cross-validation）

交叉验证旨在估计我们模型的有效性（validity），以及我们学习函数的强度。模型是否太弱、或太简单，以至于无法给出准确的预测与分类？我们是否在过拟合（overfitting）训练数据，从而在面对新测试数据时面临风险？可以说，交叉验证在一个相对较小的数据集上做得更细致，以便测试与生产能更快地在更大的数据集上推进。

> <span style="color:#27ae60;">**译者注**：交叉验证（cross-validation）与 bootstrap（自助法）常被并列提及，但它们解决的问题不同。交叉验证把同一份数据轮流切成"训练 + 验证"，目的是估计**模型在新数据上的泛化表现**——它换的是"哪一部分数据当裁判"；而 bootstrap 是在样本本身太小、或分布未知时，对样本做**有放回的重采样**，去估计统计量（如均值、方差、置信区间）的不确定性——它换的是"同一份数据被重复抽取多少次"。两者都"重复利用数据"，但一个面向预测误差，一个面向推断不确定性。作者在这里把 bootstrap 归功于 Brad Efron（Efron 1979），它已成为现代统计的基石之一。</span>

注意：另一种统计方法——出于另一目的——同样会重复利用数据，这就是 Brad Efron 提出的 **bootstrap**（自助法）。当样本量很小、或其分布未知时，就会（且需要）用到它。我们通过回到那个（小的）样本、并重复利用这些数据来抽取新信息，从而力求最大限度的理解。通常，小数据集并非深度学习应用的背景。

交叉验证的第一步，是把可用的数据分成 $K$ 个子集。若 $K=2$，它们本质上就是训练集和测试集——但我们通常希望在与大的测试集打交道之前，先从较小的集合中获取更多信息。**K 折交叉验证**（K-fold cross-validation）把 $K$ 个子集各自单独用作一次测试集。在每一次试验里，其余 $K-1$ 个子集组成训练集。我们在对同一份（中等规模的）数据反复加工，以求比单次优化能教给我们的更多。

交叉验证可以让学习率变得**自适应**：随下降的进行而改变。它有很多变体，例如"双重交叉验证"（double cross-validation）。在一个标准化的 $m\times n$ 最小二乘问题 $Ax=b$ 中，Wikipedia 给出了均方误差的期望值 $(m-n-1)/(m+n-1)$。更高的误差通常表明过拟合。深度学习里相应的检验会提醒我们考虑**提前停止**（early stopping）。

本节关于超参数的内容，受到 Bengio 在一部杰出著作中那一长章的启发与改进。书名是 *Neural Networks: Tricks of the Trade*（第 2 版），由 G. Montavon、G. Orr 与 K.-R. Müller 主编，Springer（2012）出版，并得到该领域领军人物的大量贡献。

<!-- page 411 -->

> <span style="color:#7f8c8d;">本页为书页 409，属 VII.4，介绍批归一化（Batch Normalization）——针对各层输入分布漂移（covariate shift）的标准化方案，并引出 Dropout；页眉与印页码不译。</span>

### 每一层的批归一化（Batch Normalization of Each Layer）

随着训练的推进，原始总体的均值与方差可能在网络的**每一层**都发生变化。这种输入分布的变化被称为 **covariate shift**（协变量偏移）。由于层统计量的这种漂移，我们常常不得不调整步长和其他超参数。一个良好的方案是：**对每一层的输入做归一化**。

归一化让训练更安全、更快速。对 dropout 的需求往往随之消失。更少的迭代如今就能给出更准确的权重，而代价可以非常适中——通常我们只需在每一层上额外训练**两个参数**。

当非线性函数是 sigmoid（S 形）而非 ReLU 时，这个问题最为严重。sigmoid 会"饱和"（saturate）：它趋近于一个极限（如 1），而 ReLU 则随着输入增大而无限增大。当输入变得很大时，非线性 sigmoid 实际上变得几乎线性、甚至成为常数。训练于是变慢，因为非线性几乎派不上用场。

剩下的问题是决定在哪个点上对输入做归一化。Ioffe 与 Szegedy 避免计算协方差矩阵（那太昂贵）。他们的归一化变换作用于大小为 $B$ 的 minibatch 中的每个输入 $v_1,\dots,v_B$：

```math
\mu_B = \frac{1}{B}\sum_{i=1}^{B} v_i, \qquad
\sigma_B^2 = \frac{1}{B}\sum_{i=1}^{B}(v_i - \mu_B)^2 + \epsilon \quad (\epsilon>0 \text{ 很小})
```

```math
\hat v_i = \frac{v_i - \mu_B}{\sigma_B}, \qquad
y_i = \gamma \hat v_i + \beta
```

（$\gamma$ 与 $\beta$ 是可训练参数）

关键点在于：要把每个新层的输入 $y_i$ 都归一化。对最初的向量批次（在第零层）有益的做法，对每个隐藏层的输入同样有益。

> S. Ioffe and C. Szegedy, *Batch normalization*, arXiv: 1502.03167v3, 2 Mar 2015.

### Dropout

Dropout 是移除网络中**随机选中的神经元**。这些是输入层 $v_0$ 或输出层 $v_L$ 之前的隐藏层的分量。与那些被丢弃神经元相连的所有 $A$ 与 $b$ 中的权重，都从网络中消失（见图 VII.6）。通常，隐藏层神经元被赋予存活概率 $p=0.5$，而输入分量可能有 $p=0.8$ 或更高。随机 dropout 的主要目标是**避免过拟合**。与把众多网络的预测合并起来相比，它是一种相对廉价的对平均方法。

Dropout 由深度学习算法发展中的五位领军人物提出：N. Srivastava、G. Hinton、A. Krizhevsky、I. Sutskever 与 R. Salakhutdinov。他们的论文 "Dropout" 发表于 *Journal of Machine Learning Research* 15 (2014) 1929–1958。关于 dropout 与物理学及不确定性（uncertainty）的新近关联，见 arXiv: 1506.02142 与 1809.08327。

<!-- page 412 -->

> <span style="color:#7f8c8d;">本页为书页 410，属 VII.4，说明 Dropout 的"稀疏网络"机制、测试时的权重重缩放、其生物学灵感，并转入超参数空间的探索策略；页眉与印页码不译。</span>

[[FIGURE: 书页 410, 图 VII.6：在稀疏化（thinned）网络中，画叉的神经元已被 dropout 移除。]]

Dropout 提供了一种方式，能一次性用许多不同的神经架构进行计算。在训练中，每个新的 $v_0$（一个输入样本的特征向量）都会导向一个新的稀疏化网络。从 $N$ 个神经元出发，共有 $2^N$ 种可能的稀疏网络。

在测试时，我们使用**完整**网络（不做 dropout），权重由训练权重**重缩放**而来：一个未被丢弃的神经元，其输出权重在重缩放时要乘以 $p$。这种测试时的近似平均，让五位作者减少了泛化误差——比其他正则化方法更简单。

dropout 的一个灵感来源是**有性繁殖**——父母各有一半基因被丢弃，且伴随微小的随机突变。对一个孩子而言，这种 dropout 似乎比深度学习的 dropout 更严酷、更永久——后者是在许多稀疏网络上取平均。（诚然，我们在兄弟姐妹之间也看到某种平均。但作者推测：随着时间推移，我们的基因为了存活而被迫变得稳健。）

dropout 模型使用一个零一随机变量 $r$（一个 Bernoulli 变量，伯努利变量）：以概率 $p$ 有 $r=1$，以概率 $1-p$ 有 $r=0$。通常到第 $n$ 层的前向（feed-forward）步骤是 $y_n = A_n v_{n-1} + b_n$，之后是非线性 $R(y_n)$。现在，一个随机 $r$ 乘以 $v_{n-1}$ 的每个分量，当 $r=0$ 时丢弃该神经元。逐分量地，$v_{n-1}$ 被乘以 0 或 1，得到 $v_{n-1}'$。于是 $y_n = A_n v_{n-1}' + b_n$。

要计算梯度，就对 minibatch 中的每个训练样本做反向传播（backpropagation），然后对这些梯度取平均。随机梯度下降仍可包含加速（加动量）、自适应下降以及权重衰减（weight decay）。作者强烈建议对权重做正则化，例如对所有权重矩阵 $A$ 的列施加最大范数要求 $\|A\| \le c$。

### 探索超参数空间（Exploring Hyperparameter Space）

我们常通过实验或经验来优化超参数。为决定学习率，我们可能尝试三种取值，并衡量损失函数的下降量。一个几何数列（如 $0.1, 0.01, 0.001$）比算术数列（如 $0.05, 0.03, 0.01$）更有意义。而如果最小或最大的取值给出了最佳结果，那就继续实验到数列中的下一个数。在这个步长的例子中，你会同时考虑计算代价与验证误差。

LeCun 强调：对于多参数搜索，**随机采样**才是快速覆盖众多可能性的途径。在高维下，网格搜索（grid search）太慢了。

<!-- page 413 -->

> <span style="color:#7f8c8d;">本页为书页 411，属 VII.4，回到损失函数，比较平方损失（square loss）与交叉熵损失（cross-entropy），并追溯到香农熵与 KL 散度；页眉与印页码不译。</span>

### 损失函数（Loss Functions）

损失函数度量的是每个样本的正确输出与计算输出之间的差异。正确输出——通常是一个分类 $y=0,1$ 或 $y=1,2,\dots$——是训练数据的一部分。最后一层的计算输出是 $w=F(x,v)$，来自带权重 $x$ 与输入 $v$ 的学习函数。

第 VI.5 节定义了三个熟悉的损失函数。之后本章转向了神经网络的结构与函数 $F$。这里我们回到对平方损失与交叉熵损失的比较。

1. **二次代价（平方损失，square loss）**：

```math
\ell(y,w) = \frac{1}{2}\|y - w\|^2
```

这是最小二乘（least squares）的损失函数——始终是一个可能的选项，但它并非深度学习的首选。原因之一是：当我们趋向 $w=y$ 处的零损失时，$\ell(y,w)$ 的图像呈抛物线形状，导数也趋向于零。

在极小点处导数为零，对光滑损失函数来说是正常的，但它常常导致一个不受欢迎的结果：权重 $A$ 与 $b$ 在最优点附近变化得非常缓慢。学习变慢，需要很多次迭代。

2. **交叉熵损失（cross-entropy loss）**：

```math
\ell(y,w) = -\frac{1}{N}\sum_{i=1}^{N}\big[y_i \log z_i + (1 - y_i)\log(1 - z_i)\big]
\tag{1}
```

这里我们允许并预期：训练神经网络得到的 $N$ 个输出 $w_i$ 已被归一化为 $z(w)$，满足 $0 < z_i < 1$。通常这些 $z_i$ 就是概率。于是 $1 - z_i$ 也在 0 与 1 之间。因此 (1) 中的两个对数都是负的，而负号保证了整体损失为正：$\ell > 0$。

不仅如此，对数还给出了一种不同的、可取的处理 $z\to 0$ 或 $1$ 的方式。关于这个计算，我们参考 Nielsen 的在线书 *Neural Networks and Deep Learning*，它聚焦于 sigmoid 激活函数而非 ReLU。那些光滑函数的代价在于：它们在端点附近会饱和（失去非线性）。

交叉熵有良好的性质，但对数从何而来？第一点是 Shannon 的熵（entropy）公式——它是信息的一种度量。若消息 $i$ 具有概率 $p_i$，你应为该消息预留 $-\log p_i$ 比特。于是每条消息的期望（平均）比特数是最优可能的：

```math
H = -\sum_{i} p_i \log p_i . \quad \text{对 } m=2 \text{ 即 } -p\log p - (1-p)\log(1-p).
\tag{2}
```

当我们不知道 $p_i$，而改用 $\hat p_i$ 时，交叉熵就出现了：

```math
H = -\sum_{i} p_i \log \hat p_i . \quad \text{对 } m=2 \text{ 即 } -p\log \hat p - (1-p)\log(1-\hat p).
\tag{3}
```

(3) 总是大于 (2)：真实的 $p_i$ 未知，代价更高。这个差值是一个很有用、但不**对称**的函数，称为 Kullback–Leibler（KL）散度。

> <span style="color:#27ae60;">**译者注**：为什么平方损失在深度学习里"不受欢迎"，而交叉熵更好？关键在导数。平方损失 $\tfrac12(y-w)^2$ 的导数正比于 $(w-y)\cdot \sigma'(z)$——这里 $\sigma'(z)$ 是激活函数的导数，对 sigmoid 来说在饱和区（$\sigma$ 接近 0 或 1）几乎为零，于是"错误很大，梯度却很小"，学习卡死。而交叉熵若配 sigmoid，导数里 $\sigma'(z)$ 恰好被"约掉"，梯度正比于 $(z-y)$——错得越远，梯度越大，学习信号与误差量直接挂钩。这就是交叉熵"让学习保持速度"的机制，也正是作者所说的"对数的处理方式可取"。</span>

> <span style="color:#27ae60;">**译者注**：作者在此引出一条清晰的逻辑链：熵 $H(p)=-\sum p_i\log p_i$ 是"知道真实分布 $p$ 时，编码一条消息所需的最优平均比特数"；交叉熵 $H(p,\hat p)=-\sum p_i\log \hat p_i$ 是"真实分布为 $p$、却按 $\hat p$ 来编码时，所需的平均比特数"。因为编码方案与真实分布不匹配，交叉熵一定不小于熵——这正是 (3) ≥ (2) 的数学事实。两者之差 $H(p,\hat p)-H(p)=\sum p_i\log(p_i/\hat p_i)$ 就是 KL 散度，它是非负的（吉布斯不等式），且对 $p,\hat p$ 不对称，所以不是"距离"。这一整条线索与第 VI.5 节对损失函数的讨论是同一件事，只是这里把"损失"上溯到了信息论根基。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 超参数为何被称为“the fateful decisions”：**</span> 本节标题把 hyperparameters 称作“fateful decisions”（攸关命运的决定），这个措辞值得讲透它的动机。选定 loss function 与网络架构之后，网络“学到的内容”已经由权重 $w$ 这一组数字表达出来——它们是从训练集里总结出的“如何由输入特征预测输出”的规则。但权重本身并不会自动涌现，它是由算法一步步算出来的；而算法的行为，恰恰被一小组不属于网络结构、却决定算法本身的数字所控制，这就是超参数。为什么说它们“攸关命运”？因为同样一个网络、同样的数据，learning rate 取 $s_k=0.1$ 还是 $s_k=10$，结果可能一个是干净收敛、一个是在最小值附近反复震荡甚至发散；而这个问题在训练真正跑起来之前几乎无法从理论上预先判死。换句话说，权重是“模型学到了什么”，超参数是“这个学习过程能不能走得通、走多快”。本节正是要把这一层决定算法命运的选择，从 loss function、dropout、regularization 这些同样属于机器学习决策清单里的项目里单独拎出来，逐一定义清楚。

> <span style="color:#1e8449;">**[note] Newton 法与 $s_k=1/L''(c_k)$ 的等价来源：**</span> 正文说 Newton 法“取 $s_k=1/L''(c_k)$，用的是 $L$ 的二阶导数”，这句话背后是一个关键的“拿什么换什么”的等价关系。梯度下降的迭代式是 $c_{k+1}=c_k-s_k\,\nabla L(c_k)$，它相当于把 Hessian 矩阵 $H(c_k)=\nabla^2 L(c_k)$ 粗暴地替换成了单个标量 $1/s_k$。而 Newton 法真正的形式是 $c_{k+1}=c_k-[H(c_k)]^{-1}\nabla L(c_k)$，它来自把 $L$ 在 $c_k$ 处按 Taylor 展开并保留到二次项，再对这个二次近似求极小点。在一维情形下，$[H]^{-1}$ 退化为 $1/L''(c_k)$，于是 Newton 法恰好可以写成“梯度下降、但把步长取成 $1/L''(c_k)$”的样子。这就是文中那句话的等价来源。它的回报是二阶收敛：设误差为 $e_k=c_k-c^*$，则 $e_{k+1}$ 正比于 $e_k^2$，即误差按平方速度收缩，越接近 $c^*$ 收敛越快。代价则是在高维时要求解大型方程组 $H(c_k)(c_{k+1}-c_k)=\nabla L(c_k)$，Hessian 的大小等于权重个数，这在深度学习中昂贵到不可接受——这正是梯度下降“用一个数 $1/s_k$ 代替整个 Hessian”之所以流行的原因。

> <span style="color:#1e8449;">**[note] cross-entropy 里 log 的来源及其与熵的联系：**</span> 本节在 loss functions 部分提了一个很自然的问题：“cross-entropy 的性质很好，可那些 log 是从哪来的？”这与全书别处（§VI.5 定义的三种 loss）是同一件事的延续：当时只给出了三种 loss 的表达式，这里才追问其信息论根源。答案分两步。第一步是 Shannon 的熵公式：若消息 $i$ 出现概率为 $p_i$，则应为它分配 $-\log p_i$ 比特，于是平均比特数 $-\sum_i p_i\log p_i$ 是信息编码的下界，当 $m=2$ 时即 $-p\log p-(1-p)\log(1-p)$。第二步是当我们不知道真实分布 $p_i$、只能用一个估计分布 $\hat p_i$ 来编码时，平均比特数变成 $-\sum_i p_i\log \hat p_i$，这就是 cross-entropy。正文由此给出一个可量化的结论：cross-entropy 恒不小于熵，二者之差正是 Kullback–Leibler (KL) divergence，即“用错分布去编码”所多付的代价。拿一个具体数值体会一下：设真实分布 $p=0.9$（样本确实属于某类），若模型也输出 $\hat p=0.9$，则 cross-entropy 为 $-0.9\log 0.9-0.1\log 0.1\approx 0.325$，正好等于熵；若模型没学好、输出 $\hat p=0.5$，则 cross-entropy 涨到 $-0.9\log 0.5-0.1\log 0.5=\log 2\approx 0.693$，多出的 $0.368$ 就是 KL divergence，度量了模型与真实分布之间的信息差距。这正解释了为什么 cross-entropy 是衡量分类损失更“讲道理”的选择，而 square loss 在深层网络里会因零点处导数为零而让学习趋缓。

---

> <span style="color:#7f8c8d;">本节把全连接网络与卷积网络放进机器学习的大视野中，介绍循环神经网络、支持向量机（含核技巧）两大经典方法，并回溯深度学习的兴起历史（谷歌翻译、AlexNet、"猫论文"等关键节点），最后以关键词清单勾勒整个领域的版图。</span>

---

<!-- page 415 -->

> <span style="color:#7f8c8d;">本页为书页 413，属 VII.5 开头——概述本节内容安排，并讲 RNN 的循环结构（上一时刻输出回流作为本时刻输入）；页眉与印页码不译。</span>

Fully connected nets（全连接网络）和 convolutional nets（卷积网络）只是整个大世界的一部分。从 training data（训练数据）出发，它们导出一个 learning function（学习函数）$F(\mathbf{x}, \mathbf{v})$。这个函数对每个输入 $\mathbf{v}$（$\mathbf{v}$ 是该样本的 feature vector，特征向量）给出正确输出 $\mathbf{w}$ 的一个近似。但机器学习在"从数据中学习"这个问题上，已经发展出了大量其他方法——其中一些由来已久。

本书无法对所有这些思想都做到面面俱到。不过，描述一下 Recurrent Neural Nets（循环神经网络）和 Support Vector Machines（支持向量机）确实是有用的。我们还收录了一些 key words（关键词）来标示机器学习的范围。（这个领域实在太需要一本 glossary〔术语表〕了！那将是对本领域的一项巨大贡献。）最后是一份关于机器学习各专题的书目清单。

## Recurrent Neural Networks（RNNs，循环神经网络）

这类网络适用于**按确定顺序**到来的数据。这包括 time series（时间序列）和 natural language（自然语言）：语音、文本或手写。在从输入 $v$ 到输出 $w$ 的连接网络中，新增的特征是来自上一时刻 $t-1$ 的输入。这个 recurrent（循环）输入由函数 $h(t-1)$ 决定。

Figure VII.7（图 VII.7）勾勒出该网络架构中这一新步骤的轮廓。

[[FIGURE: 书页 413, 循环网络的计算图：每个时刻 t 都有输入 v(t)、循环状态 h(t)、输出 w 与目标 y，权重 X_in、C_recur、C_out 用于最小化损失 L(y−w)]]

> **图 VII.7 说明**：循环网络的计算图在每个时刻 $t$ 求出使 loss（损失）最小化的输出 $w$。$h(t)$ 的输入是新数据 $v(t)$ 与来自上一时刻的循环数据 $h(t-1)$。乘以数据的权重是 $X_{in}$、$C_{recur}$ 和 $C_{out}$，它们被选来最小化损失 $L(y-w)$。这一网络架构是 **universal（通用）** 的：任何可被 Turing machine（图灵机）计算的公式，它都能计算。

## Key Words and Ideas（关键词与思想）

1. Kernel learning（核学习，见下页）
2. Support Vector Machines（支持向量机，见下页）
3. Generative Adversarial Networks（生成对抗网络）
4. Independent Component Analysis（独立成分分析）
5. Graphical models（图模型）
6. Bayesian statistics（贝叶斯统计）
7. Random forests（随机森林）
8. Reinforcement learning（强化学习）

---

<!-- page 416 -->

> <span style="color:#7f8c8d;">本页为书页 414，属 VII.5 支持向量机与核技巧——先讲超平面分隔、软硬间隔、hinge loss 与二次规划，再引入 kernel trick 把线性分隔推广到非线性；页眉与印页码不译。</span>

## Support Vector Machines（SVM，支持向量机）

从 $m$ 维空间中的 $n$ 个点 $v_1, \dots, v_n$ 出发。每个 $v_i$ 带有一个 classification（分类）标记 $y_i = +1$ 或 $y_i = -1$。Vapnik 提出的目标是：在 $m$ 维空间中找一个 plane（平面）$w\cdot v = b$（如果可能的话），把 plus points（正点，$+$）与 minus points（负点，$-$）分隔开来。那个向量 $w$ 将垂直于该平面。数 $b$ 告诉我们从 $\mathbb{R}^m$ 中的这条 line（直线）、plane（平面）或 hyperplane（超平面）到点 $(0, \dots, 0)$ 的距离是 $|b|/\|w\|$。

[[FIGURE: 书页 414, 分隔直线 w·v=b 使到正点与负点的等距间隔（margin）最大化；若 v4 落在 v1、v2、v3 构成的三角形内部，则线性分隔不可能]]

> 这条 separating line（分隔线）$w\cdot v = b$ 使得到 $+$ 点与 $-$ 点的**等距间隔（margin，边际）最大化**。若 $v_4$ 在三角形内部，分隔将是不可能的。

**问题**：求 $w$ 和 $b$，使 $w\cdot v_i - b$ 对所有点 $i$ 都具有正确符号 $y_i$。若 $v_1, v_2, v_3$ 是平面中的正点（$y = +1$），则 $v_4$ 必须落在 $v_1, v_2, v_3$ 的三角形之外。图中画出了 maximum separation（最大分隔，即最大间隔）的直线。

- **Maximum margin（最大间隔）**：在条件 $y_i (w \cdot v_i - b) \ge 1$ 下最小化 $\|w\|$。

这是一个 "hard margin"（硬间隔）。该不等式要求每个点都在分隔面的正确一侧。如果这些点无法被分隔，那么就没有任何 $w$ 和 $b$ 能成功。对于 "soft margin"（软间隔），我们直接去选可用的最好 $w$ 和 $b$，其依据是 hinge loss（合页损失）加 penalty（惩罚项）：

```math
\min_{w,b}\ \frac{1}{n}\sum_{i=1}^{n}\max\bigl(0,\; 1 - y_i(w^{T}v_i - b)\bigr) + \lambda\,\|w\|^2 .
\tag{1}
```

**Soft margin（软间隔）**：最小化上面的式子。

那个 hinge loss（即 $\max$ 项）在 $v_i$ 处于分隔面正确一侧时为 $0$。若分隔不可能，惩罚项 $\lambda\|w\|^2$ 就在 hinge losses 与 margin sizes（间隔大小）之间做权衡。若我们为那个 hinge loss 引入变量 $h_i$，那么我们就是在最小化一个关于 $w$ 的 quadratic function（二次函数），并带有连接 $w, b, y_i, h_i$ 的 linear inequalities（线性不等式）。这就是高维的 quadratic programming（二次规划）——理论上研究得很透彻，实践上却颇具挑战。

## The Kernel Trick（核技巧）

SVM 是 linear separation（线性分隔）。一个平面把 $+$ 点与 $-$ 点分开。当 feature vectors（特征向量）$\mathbf{v}$ 被变换为 $\phi(\mathbf{v})$ 时，kernel trick（核技巧）允许一个 nonlinear separator（非线性分隔面）。于是，变换后向量的 dot product（点积）给出 kernel function（核函数）$K(\mathbf{v}_i, \mathbf{v}_j) = \phi(\mathbf{v}_i)\cdot\phi(\mathbf{v}_j)$。关键在于**完全用 $K$ 工作、而完全不碰函数 $\phi$**。事实上我们从未见过、也不需要 $\phi$。在线性情形下，这相当于选一个 positive definite（正定）的 $K$、而看不到 $K = A^{T}A$ 中的矩阵 $A$。RBF kernel（径向基核）$e^{-\|\mathbf{v}_i - \mathbf{v}_j\|^{2}/2\sigma^{2}}$ 见 §III.3 节。

> M. Belkin, S. Ma, and S. Mandal, *To understand deep learning we need to understand kernel learning*, arXiv:1802.01396. "Non-smooth Laplacian kernels defeat smooth Gaussians"（非光滑拉普拉斯核击败光滑高斯核）
>
> T. Hofmann, B. Schölkopf, and A. J. Smola, *Kernel methods in machine learning*, Annals of Statistics 36 (2008) 1171-1220（附大量参考文献）。

---

<!-- page 417 -->

> <span style="color:#7f8c8d;">本页为书页 415，属 VII.5 深度学习简史——从谷歌翻译的转向讲起，串起 Minsky/Papert、Hinton 与 AlexNet、"猫论文"、GNMT 论文等关键事件，点明"让机器自己找规则"这一范式转变；页眉与印页码不译。</span>

## Google Translate（谷歌翻译）

一篇关于深度学习与谷歌翻译发展历程的非凡文章，发表于 2016 年 12 月 14 日（星期日）的《纽约时报杂志》。它讲述了谷歌如何突然从 conventional translation（传统翻译）跳转到 recurrent neural network（循环神经网络）。作者 Gideon Lewis-Kraus 把这一事件描述为"三个故事合而为一"：开发团队的工作，谷歌内部那些看出可能性所在的团队，以及逐渐改变我们对"如何学习"之理解的全球科学家群体：
https://www.nytimes.com/2016/12/14/magazine/the-great-ai-awakening.html

这次开发花了不到一年时间。Google Brain 及其竞争者用五年时间孕育出这一想法。机器学习的全球故事在时间与空间上要比这长一个数量级。关于近期历史，关键在于它对"学习一门语言"这一方法所产生的**地震式**改变：

> 与其把两种语言中的每个单词、每条语法规则、每个例外都编程进去，不如让计算机自己去发现规则——只要给它足够多正确的翻译即可。

如果我们在做 image recognition（图像识别），输入就是许多带正确 label（标签）的样本（即 training set，训练集）。机器据此构造出函数 $F(\mathbf{x}, \mathbf{v})$。

这更接近儿童的学习方式，也更接近我们人类自己的学习方式。如果你想教人下 checkers（跳棋）或 chess（国际象棋），最好的办法是拿来一块棋盘、走出每一步。去**下棋**。

从这一愿景走向 neural nets（神经网络）与 deep learning（深度学习），这些步骤来得很不容易。Marvin Minsky 无疑是最重要的先驱之一。但他与 Seymour Papert 合著的书，有一部分恰恰是讲 "Perceptrons"（感知机）**做不了什么**。只用一层网络，XOR 函数（"$A$ 或 $B$、但非二者同时"）是无法实现的。缺少的正是 depth（深度）——而它又是必需的。

Geoffrey Hinton 毕生的工作对这个学科产生了巨大影响。就机器翻译而言，他恰好在正确的时间身在谷歌。就图像识别而言，他和他的学生们在 2012 年（凭借 AlexNet）赢得了 visual recognition challenge（视觉识别挑战赛）。它的深度改变了神经网络的设计。同样令人印象深刻的是 1986 年《Nature》上的一篇文章，Rumelhart、Hinton 与 Williams 在其中预见到 backpropagation（反向传播）将在权重优化中变得至关重要：*Learning representations by back-propagating errors*（通过误差反向传播学习表征）。

这些思想在世界范围内引出了出色的工作。2011–2012 年的 "cat paper"（"猫论文"）描述了如何在**没有标注图像**的情况下训练一个 face detector（人脸检测器）。第一作者是 Quoc Le：*Building high-level features using large scale unsupervised learning*（用大规模无监督学习构建高层特征）：arxiv.org/abs/1112.6209。

一个由 $200\times200$ 图像组成的大数据集从 YouTube 中采样而来。其规模是通过 localizing（局部化）receptive fields（感受野）来控制的。该网络有十亿个权重需要训练——这仍比我们视觉皮层中的神经元数量小一百万倍。读了这篇论文，你就会看到深度学习的到来。

一个小团队悄悄超越了那个使用规则的大团队。最终，那篇有 31 位作者的论文出现在 arxiv.org/abs/1609.08144。于是谷歌不得不切换到那个"不以规则开头"的深层网络。

---

## 译者注

> <span style="color:#27ae60;">**① 循环输入为什么让 RNN "通用"？** 全连接网络与卷积网络默认每个样本独立处理，输入到输出的映射是"一次性的"。而序列数据（语音、文本）的要点在于：当前输出依赖此前已经"见过"的信息。RNN 的机制是把上一时刻的隐藏状态 $h(t-1)$ 与当前输入 $v(t)$ 一起喂给函数 $h$，从而让信息沿时间轴流动——这正是"记忆"的数学表达：$h(t)$ 同时承载了"此刻数据"与"历史摘要"。图 VII.7 里 $C_{recur}$ 乘以 $h(t-1)$、$X_{in}$ 乘以 $v(t)$，两者相加再通过非线性激活，就形成了一台能"记住过去"的机器。说它 universal，是引用了图灵机的可计算性结论：只要隐藏层够宽、时间步足够，这样的循环结构可以逼近任意可计算函数——与"感知机一层做不到 XOR"形成对照，凸现出"时间/深度"这一维度的本质力量。</span>

> <span style="color:#27ae60;">**② hinge loss 到底在"换什么"？** 硬间隔要求每个点都严格满足 $y_i(w\cdot v_i - b)\ge 1$，一旦数据线性不可分，问题无解。软间隔的思路是"允许犯错、但为犯错付费"：把每个点的违反量换成 $\max(0, 1 - y_i(w\cdot v_i - b))$ 这一项——当点落在正确一侧且离分隔面够远时，括号内为负，$\max$ 取 $0$（不罚）；当点越界或离分隔面太近时，括号为正，$\max$ 就把这个"欠的账"记下来。于是原本"必须全对"的约束被替换成"总代价最小"的目标函数，代价由 hinge 项之和与 $\lambda\|w\|^2$ 两项合成。$\lambda$ 是二者的调节旋钮：$\lambda$ 大 → 更看重间隔大（$\|w\|$ 小）、容忍更多误分；$\lambda$ 小 → 更看重少犯错。这正是把"线性不可分"这一硬约束软化（relax）的标准手法，与 111.3 节核方法的"换空间"思路互为表里：核技巧换的是**特征空间**，软间隔换的是**约束松紧**。</span>

> <span style="color:#27ae60;">**③ 为什么"只用 $K$、永不碰 $N$"是核技巧的核心？** 若真把每个 $v_i$ 显式映射到高维 $N(v_i)$，再算 $N(v_i)\cdot N(v_j)$，维数可能爆炸（甚至无穷维），存储与计算都承受不起。但 SVM 的训练与预测只用向量点积，而点积 $N(v_i)\cdot N(v_j)$ 常能写成一个关于原向量的封闭函数 $K(v_i, v_j)$。于是整条流水线只需算 $K$，映射 $N$ 从未被显式构造——这就是"kernel trick"。它和本书一贯的主题同源：$K=A^{T}A$ 意味着"先乘 $A$ 再取转置点积"，你完全可以不把矩阵 $A$ 显式写出来，只认它的 Gram 形式。RBF 核 $e^{-\|v_i-v_j\|^2/2\sigma^2}$ 对应的是一个无穷维映射，靠显式计算不可能，靠 $K$ 却唾手可得。这解释了为何核方法能如此轻易地获得非线性分隔能力。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] RNN 的循环输入为什么是 $h(t-1)$：在"时间"维度上展开一个共享权重的网络**</span> 全连接网络和卷积网络处理的是"一次性、无顺序"的输入，而循环神经网络（Recurrent Neural Networks）专门处理有确定顺序的数据——时间序列、语音、文本、手写。核心动机是：顺序数据里，当前时刻的正确输出 $w$ 往往不仅取决于当前输入 $v(t)$，还取决于"之前发生了什么"。所以 RNN 的架构里多了一条"来自上一时刻"的输入 $h(t-1)$。关键机制是：处理 $t-1$ 时刻的隐藏状态 $h(t-1)$ 被原封不动地送回来，作为 $t$ 时刻的输入之一，于是网络形成了"自己输出的一部分又被自己吃掉"的闭环。注意这里的权重 $W_{\mathrm{in}}$、$W_{\mathrm{recur}}$、$W_{\mathrm{out}}$ 是**跨所有时间步共享的**——同一套参数在每个时刻重复使用，这正是"循环"二字的经济学含义：它不随序列变长而增加参数量。文中那句"这种网络架构是通用的，凡是图灵机可计算的公式它都能算"点破了动机——把时间当作可迭代的维度，就等价于用有限深度的展开去逼近任意可计算函数，只是"深度"换成了"序列长度"。

> <span style="color:#1e8449;">**[note] 软间隔的 hinge loss：为什么是 $\max(0,1-y_i(w^T v_i-b))$ 而不是"错误个数"**</span> 硬间隔（hard margin）要求每个点都满足 $y_i(w^T v_i-b)\ge 1$，一旦点不可分就无解。软间隔要的是"能分尽量分、分不开就罚"。直接数"错分了多少个点"会得到一个不可微、不平滑的目标，无法用梯度类方法优化；于是引入 hinge loss $\max(0,\,1-y_i(w^T v_i-b))$ 作为每个点的"惩罚替身"。它的机制在于：当 $y_i(w^T v_i-b)\ge 1$（点在正确一侧且离平面足够远）时该项恒为 $0$，不产生惩罚；一旦越界或落错侧，惩罚就随"越界距离"线性增长。这样把"是否分对"这个离散判定，转化成了"离界多少"这个连续、分段线性的量，从而能和 $\lambda\|w\|^2$ 这个正则项合并成一个**二次规划**问题——目标关于 $w$ 是二次的，约束关于 $w,b,y_i,h_i$ 是线性的。这正是为什么要在前面引入变量 $h_i$：把不可微的 $\max$ 拆成线性不等式，让整个问题落回"高维二次规划"这个理论上已充分研究的框架。

> <span style="color:#1e8449;">**[note] Kernel Trick 与全书的"不看见 $A$"是同一件事：一个具体数字例子**</span> 核技巧（Kernel Trick）的表述"只和 $K$ 打交道、完全不碰映射 $\phi$"，与本书前文（§III.1、§III.3）"选一个正定的 $K$ 而看不见 $K=A^TA$ 里的 $A$"是同一个数学事实：算法只需要点积 $\phi(v_i)^T\phi(v_j)$ 的值，而它恰等于核函数 $K(v_i,v_j)$。用一个具体例子最直观：设 $\phi(v)=(v_1^2,\ \sqrt{2}\,v_1v_2,\ v_2^2)$，则 $\phi(u)^T\phi(v)=u_1^2v_1^2+2u_1u_2v_1v_2+u_2^2v_2^2=(u_1v_1+u_2v_2)^2=(u^Tv)^2$。于是二次多项式核 $K(u,v)=(u^Tv)^2$ 在原始二维空间里的计算代价是两次乘法，却等价于在三维特征空间里做内积——**非线性分隔在低维空间里被"免费"实现**，$\phi$ 甚至不必显式写出。RBF 核 $K(u,v)=e^{-\|u-v\|^2/2\sigma^2}$ 则更进一步，它对应的 $\phi$ 落在无穷维空间，$K$ 的简单形式掩盖了这一点。文末引 Belkin 等人的论文"理解深度学习要先理解核学习"，正是把这一章和下一章神经网络连起来的伏笔。
