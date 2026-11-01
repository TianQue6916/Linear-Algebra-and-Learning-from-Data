# Linear Algebra and Learning From Data（线性代数与数据学习）· VII.2

## 书页 387-395 ｜ PDF 页 389-397 ｜ Convolutional Neural Nets（卷积神经网络）

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
