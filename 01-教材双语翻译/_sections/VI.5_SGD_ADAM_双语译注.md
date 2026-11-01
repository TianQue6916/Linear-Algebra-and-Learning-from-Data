# Linear Algebra and Learning From Data（线性代数与数据学习）· VI.5

## 书页 359-369 ｜ PDF 页 361-371 ｜ Stochastic Gradient Descent and ADAM（随机梯度下降与 ADAM）

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
