# Linear Algebra and Learning From Data（线性代数与数据学习）· VII.5

## 书页 413-415 ｜ PDF 页 415-417 ｜ The World of Machine Learning（机器学习的世界）

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
