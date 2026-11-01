# Linear Algebra and Learning From Data（线性代数与数据学习）· V.5

## 书页 305-310 ｜ PDF 页 307-312 ｜ Multivariate Gaussian and Weighted Least Squares（多元高斯与加权最小二乘）

> <span style="color:#7f8c8d;">本节把最小二乘从"误差独立同方差"的假设推广到"误差相关且方差不齐"的一般情形：用协方差矩阵 $V$ 定义多元高斯分布，用 $V^{-1}$ 作为权重把异方差噪声"白化"，得到加权最小二乘（weighted least squares）正规方程，并引出估计量的协方差、BLUE 定理与卡尔曼滤波（Kalman filter）的递推更新。</span>

---

<!-- page 307 -->

> <span style="color:#7f8c8d;">本页为书页 305，属 V.5 开篇，讲多元高斯分布如何由协方差矩阵 $V$ 刻画变量间的相关性，并用特征分解把多维积分化为一维积分之和；页眉与印页码不译。</span>

## Non-independent $x$ and $y$（不再独立的 $x$ 与 $y$）

我们准备好放弃独立性了。即使 $V$ 不再是对角矩阵，指数中的项 (5)（连同 $\frac12$ 因子）依然正确。现在这个 Gaussian（高斯分布）同时依赖一个向量 $m$ 和一个矩阵 $V$。

当 $M=2$ 时，第一个变量可能给出关于第二个变量 $y$ 的部分信息（反之亦然）。也许 $y$ 的某一部分由 $x$ 决定，而另一部分是真正独立的。正是这个 $M\times M$ 的协方差矩阵（covariance matrix）$V$ 刻画了 $M$ 个变量 $x=(x_1,\dots,x_M)$ 之间的相互依赖。协方差矩阵的逆 $V^{-1}$ 进入 $p(x)$：

```math
p(x) = \frac{1}{(2\pi)^{M/2}\sqrt{\det V}}\,\exp\!\Big(-\tfrac12 (x-m)^{T} V^{-1} (x-m)\Big)
```

Multivariate Gaussian（多元高斯） probability distribution（概率分布）

向量 $x=(x_1,\dots,x_M)$ 与 $m=(m_1,\dots,m_M)$ 分别包含随机变量及其均值。分子里的 $2\pi$ 的 $M$ 个平方根（即 $(2\pi)^{M/2}$）与 $\det V$ 的平方根，都是为了让总概率等于 1。让我用线性代数来验证。我利用对称矩阵 $V=Q\Lambda Q^{T}$ 的特征值 $\lambda$ 与标准正交特征向量 $q$，于是 $V^{-1}=Q\Lambda^{-1}Q^{T}$：

```math
(x-m)^{T} V^{-1}(x-m) = X^{T}Q\Lambda^{-1}Q^{T}X = Y^{T}\Lambda^{-1}Y
```

注意！组合 $Y=Q^{T}X=Q^{T}(x-m)$ 是统计上独立的，它们的协方差矩阵 $\Lambda$ 是对角阵。

用 $V$ 的特征向量矩阵 $Q$ 把 $V$ 对角化这一步，等同于把随机变量"去相关"（uncorrelating）。对于新变量 $Y_1,\dots,Y_M$，协方差全部为零。这正是线性代数帮助微积分计算多维积分的切入点。

把变量 $x$ 减去 $m$ 平移到 $X$，再旋转到 $Y=Q^{T}X$，$p(x)$ 的积分不会改变。矩阵 $\Lambda$ 是对角的！于是我们要的积分拆成 $M$ 个我们已知的一维积分之积：

```math
\int e^{-Y^{T}\Lambda^{-1}Y/2}\,dY
= \int e^{-Y_1^2/2\lambda_1}\,dY_1\ \cdots\ \int e^{-Y_M^2/2\lambda_M}\,dY_M
= (2\pi\lambda_1)^{1/2}\cdots(2\pi\lambda_M)^{1/2}
```

且 $ (2\pi)^{M/2}\sqrt{\det V} = \prod_{i=1}^{M}(2\pi\lambda_i)^{1/2}$（由 (7) 得）。

$V$ 的行列式（也是 $\Lambda$ 的行列式）等于特征值之积 $\lambda_1\cdots\lambda_M$。于是 (7) 给出了正确的除数，使得 (6) 式中的 $p(x_1,\dots,x_M)$ 的积分 $=1$，如我们所愿。

$p(x)$ 的均值与方差同样是 $M$ 维积分。用 $V$ 的特征向量 $q_1$ 到 $q_M$ 把 $V$ 对角化、并引入 $Y=Q^{T}X$ 的同一思路，可以求出这些积分：

```math
\int x\,p(x)\,dx = (m_1, m_2, \dots, m_M) = m
\qquad
\text{Covariance matrix } V
```

Vector $m$ of means（均值向量） ｜ Covariance matrix $V$（协方差矩阵）

---

<!-- page 308 -->

> <span style="color:#7f8c8d;">本页为书页 306，属 V.5 第二节，引出加权最小二乘：当误差不独立或方差不齐时，正确度量是 $E=(b-Ax)^{T}V^{-1}(b-Ax)$，正规方程为 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$；页眉与印页码不译。</span>

## Probability and Statistics（概率与统计）

**结论**：概率密度 $p(x)$ 的公式 (6) 具备我们想要的全部性质。

## Weighted Least Squares（加权最小二乘）

在第 4 章，最小二乘从一个无解方程组 $Ax=b$ 出发。我们选择最小化误差 $\lVert b-Ax\rVert^2$，这引导我们得到最小二乘方程 $A^{T}A\hat x=A^{T}b$。最优的 $\hat x$ 是 $b$ 在 $A$ 的列空间上的投影。但问题在于：这个平方距离 $E=\lVert b-Ax\rVert^2$ 真的是该最小化的正确误差度量吗？

如果 $b$ 中的测量误差是独立随机变量，均值为 0、方差 $\sigma^2=1$ 且服从正态分布，Gauss（高斯）会说：是的，用最小二乘。

如果误差不独立、或它们的方差彼此不等，Gauss 会说：不，用加权最小二乘。

本节将说明，好的误差度量是 $E=(b-Ax)^{T}V^{-1}(b-Ax)$。最优 $\hat x$ 的方程用到了协方差矩阵 $V$：

```math
A^{T}V^{-1}A\hat x = A^{T}V^{-1}b .
```

Weighted least squares（加权最小二乘） (10)

最重要的例子是 $b$ 中有 $m$ 个独立误差，这些误差的方差为 $\sigma_1^2,\dots,\sigma_m^2$。由独立性，$V$ 是对角矩阵。好的权重 $1/\sigma_1^2,\dots,1/\sigma_m^2$ 来自 $V^{-1}$。我们是在给 $b$ 中的误差加权，使其方差变为 1（且协方差 $=0$）：

```math
\text{Minimize } E = \sum_{i=1}^{m} \frac{(b_i - A_i x)^2}{\sigma_i^2}
\qquad
\text{Independent errors in } b
```

Weighted least squares（加权最小二乘） (11) ｜ Independent errors in $b$（$b$ 中的独立误差）

通过给误差加权，我们在"白化"（whitening）噪声。White noise（白噪声）是对基于标准高斯 $N(0,1)$（均值零、$\sigma^2=1$）的独立误差的简洁描述。

让我写下得到最优 $\hat x$ 的方程 (10) 与 (11) 的步骤：

- 从 $Ax=b$ 出发（$m$ 个方程、$n$ 个未知数，$m>n$，无解）
- 每个右端项 $b_i$ 均值零、方差 $\sigma_i^2$，各 $b_i$ 相互独立
- 把第 $i$ 个方程除以 $\sigma_i$，使每个 $b_i/\sigma_i$ 的方差 $=1$

这一除法把 $Ax=b$ 变成 $V^{-1/2}Ax=V^{-1/2}b$，其中 $V^{-1/2}=\operatorname{diag}(1/\sigma_1,\dots,1/\sigma_m)$。

对这些加权后的方程做普通最小二乘，即 $A\to V^{-1/2}A$、$b\to V^{-1/2}b$，得到

```math
(V^{-1/2}A)^{T}(V^{-1/2}A)\,\hat x = (V^{-1/2}A)^{T} V^{-1/2}b
\quad\Longrightarrow\quad
A^{T}V^{-1}A\hat x = A^{T}V^{-1}b .
```

(12)

由于 $V^{-1}$ 中的 $1/\sigma_i^2$，更可靠的方程（$\sigma_i$ 更小）得到更重的权重。这是加权最小二乘的核心要点。

那些对角权重（方程之间不耦合）是最常见、也最简单的。它们适用于 $b_i$ 中的独立误差。当这些测量误差不独立时，$V$ 不再对角——但 (12) 仍然是正确的加权方程。实际中，找出全部协方差可能是繁重的工作，而对角的 $V$ 要简单得多。

---

<!-- page 309 -->

> <span style="color:#7f8c8d;">本页为书页 307，属 V.5 第三节，讲估计量的方差-协方差矩阵 $W=(A^{T}V^{-1}A)^{-1}$ 及其最优性（BLUE），并给出心率测量三次数值例；页眉与印页码不译。</span>

## The Variance in the Estimated $\hat x$（估计量 $\hat x$ 的方差）

还有一点：通常重要的问题并不是针对某个特定 $b$ 的最优 $\hat x$——那只是一个样本！真正的目标是了解整个实验的可靠性。这（一如可靠性总是如此）由估计量 $\hat x$ 的方差来度量。

首先，$b$ 的零均值给出 $\hat x$ 的零均值。然后，把输入 $b$ 的方差 $V$ 与输出 $\hat x$ 的方差 $W$ 联系起来的公式，结果十分优美：

```math
\text{Variance-covariance matrix for } \hat x = (A^{T}V^{-1}A)^{-1} .
```

(13)

这一最小可能的方差来自最优的加权，也就是 $V^{-1}$。这个关键公式正是 V.4 节的完美应用。若 $b$ 的协方差矩阵为 $V$，则 $\hat x=Lb$ 的协方差矩阵为 $LVL^{T}$。矩阵 $L$ 是

```math
L = (A^{T}V^{-1}A)^{-1}A^{T}V^{-1},
```

因为 $\hat x=Lb$ 解加权方程 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$。把它代入 $LVL^{T}$，就能看到 (13) 出现：

```math
LVL^{T}
= (A^{T}V^{-1}A)^{-1}A^{T}V^{-1}\; V\; V^{-1}A\,(A^{T}V^{-1}A)^{-1}
= (A^{T}V^{-1}A)^{-1}.
```

这就是输出 $\hat x$ 的协方差 $W$。是时候看一个例子了。

**例 1** 假设一位医生三次测量你的心率 $x$（$m=3,n=1$）：即 $Ax=b$，其中

```math
A = \begin{bmatrix}1\\1\\1\end{bmatrix},
\qquad
V = \begin{bmatrix}\sigma_1^2 & 0 & 0\\ 0 & \sigma_2^2 & 0\\ 0 & 0 & \sigma_3^2\end{bmatrix}.
```

方差可能是 $\sigma_1^2=1/9$、$\sigma_2^2=1/4$、$\sigma_3^2=1$。权重于是依次是 3、2、1。随着测量进行你越来越紧张：$b_3$ 不如 $b_2$ 和 $b_1$ 可靠。三次测量都含有一些信息，所以它们都进入最优（加权）估计：

```math
V^{-1/2}A\hat x = V^{-1/2}b \quad\Longleftrightarrow\quad
\begin{cases} 3\hat x = 3b_1\\ 2\hat x = 2b_2\\ 1\hat x = 1b_3 \end{cases}
```

进而 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$：

```math
\begin{bmatrix}1&1&1\end{bmatrix}
\begin{bmatrix}9&0&0\\0&4&0\\0&0&1\end{bmatrix}
\begin{bmatrix}1\\1\\1\end{bmatrix}\hat x
=
\begin{bmatrix}1&1&1\end{bmatrix}
\begin{bmatrix}9&0&0\\0&4&0\\0&0&1\end{bmatrix}
\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix}
```

```math
14\,\hat x = 9b_1 + 4b_2 + b_3
\quad\Longrightarrow\quad
\hat x = \frac{9b_1 + 4b_2 + b_3}{14}
```

即 $b_1,b_2,b_3$ 的最优加权平均。

---

<!-- page 310 -->

> <span style="color:#7f8c8d;">本页为书页 308，属 V.5 第四节，收束加权最小二乘（BLUE 定理与 $\ell_1$ 范数的动机），并转入卡尔曼滤波：动态最小二乘与新数据到来时的递推更新思想；页眉与印页码不译。</span>

权重最大落在 $b_1$ 上，因为它的方差最小。$\hat x$ 的方差有优美的公式：

```math
W = (A^{T}V^{-1}A)^{-1} = \frac{1}{14}.
```

这个方差 $W=\frac{1}{14}$，因为纳入了 $b_2$ 与 $b_3$，从单独用 $b_1$ 时的 $\frac{1}{9}$ 下降了：

```math
\frac{1}{14} < \frac{1}{9}.
```

Gauss 的 BLUE 定理（证明见网站）断言：我们的 $\hat x=Lb$ 是 $Ax=b$ 之解的最佳线性无偏估计（Best Linear Unbiased Estimate）。对任何其他无偏选择 $\hat x^{*}=L^{*}b$，其方差 $W^{*}=L^{*}V L^{*T}$ 将大于我们的 $W=LVL^{T}$。

注意："更大"意味着 $W^{*}-W$ 将是正半定矩阵（positive semidefinite）。"无偏"意味着 $L^{*}A=I$，这样精确的 $Ax=b$ 会产生正确答案 $\hat x=L^{*}b=x$。

我必须补充：也有理由从一开始就不最小化平方误差。理由之一：$\hat x$ 往往有很多小分量，小数的平方非常小，而它们会在最小化时出现。更容易理解的是稀疏向量（sparse vectors）——只有少数非零元。统计学家常常更愿意最小化非平方误差：$\sum |b_i-(Ax)_i|$ 之和。这一误差度量是 $\ell_1$ 范数而非 $\ell_2$ 范数。由于绝对值的缘故，用 $\ell_1$ 范数求 $\hat x$ 的方程变成非线性的。

新出现的快速算法正在计算稀疏的 $\hat x$，未来属于 $\ell_1$。IV.4 节的压缩感知（compressive sensing）正是 $\ell_1$ 回归的一个令人印象深刻的应用。

## The Kalman Filter（卡尔曼滤波）

"Kalman filter"（卡尔曼滤波）是动态最小二乘中的伟大算法。"动态"一词意味着新的测量值 $b_k$ 不断到来，于是最优估计不断改变（基于全部的 $b_0,\dots,b_k$）。不仅如此，矩阵 $A$ 也在改变。于是 $\hat x_k$ 将是我们对"全部历史观测方程与更新方程（状态方程）的最新解"的最佳最小二乘估计。截至时间 2，共有 3 个观测方程和 2 个状态方程：

```math
A_0x_0 = b_0,\qquad
A_1x_1 = b_1,\qquad
A_2x_2 = b_2
```

```math
x_1 = F_0x_0,\qquad
x_2 = F_1x_1
```

(14)

卡尔曼的思想是一次引入一个方程。每个方程都会有误差。每来一个新方程，我们就更新当前 $x_k$ 的最优估计。但历史不会被遗忘！这个新估计用到了所有过去的观测 $b_0$ 到 $b_{k-1}$，以及所有状态方程 $x_{new}=F_{old}\,x_{old}$。这是一个不断增大的最小二乘问题。

关于 (14) 还有更重要的一点。每个最小二乘方程都用 $b_k$ 中误差的协方差矩阵 $V_k$ 加权。更新方程 $x_{k+1}=F_kx_k$ 中的误差甚至还有一个协方差矩阵 $C_k$。于是最优 $\hat x_k$ 依赖 $b_0,b_1$ 与 $F_1$，以及 $V_0,V_1$ 与 $C_1$。把它写成对前一个 $\hat x_{k-1}$ 的更新，才是好的写法。

---

<!-- page 311 -->

> <span style="color:#7f8c8d;">本页为书页 309，属 V.5 第五节，给出卡尔曼滤波的核心——用增益矩阵 $K_1$ 与协方差更新 $W_1^{-1}=W_0^{-1}+A_1^{T}V_1^{-1}A_1$ 把旧估计递推到新估计；页眉与印页码不译。</span>

让我集中处理一个简化问题：不含矩阵 $F_k$ 与协方差 $C_k$。我们在每一步估计同一个真实的 $x$。如何从 $\hat x_0$ 得到 $\hat x_1$？

$b_0$ 引出加权方程 $A_0^{T}V_0^{-1}A_0\hat x_0=A_0^{T}V_0^{-1}b_0$：

```math
\text{OLD } A_0\hat x = b_0
```

(15)

下面的旧问题引出如下的新加权方程：

```math
\text{NEW } \begin{bmatrix}A_0\\A_1\end{bmatrix}\hat x = \begin{bmatrix}b_0\\b_1\end{bmatrix}
\quad\text{with}\quad
V = \begin{bmatrix}V_0 & 0\\0 & V_1\end{bmatrix}
```

(16)

是的，我们可以直接解这个新问题、忘掉旧问题。但旧解 $\hat x_0$ 花了功夫，我们希望能在 $\hat x_1$ 中复用。我们寻找的是对 $\hat x_0$ 的一个更新：

```math
\hat x_1 = \hat x_0 + K_1(b_1 - A_1\hat x_0).
```

Kalman update gives $\hat x_1$ from $\hat x_0$（卡尔曼更新：由 $\hat x_0$ 得 $\hat x_1$） (17)

更新修正量是旧状态与新测量 $b_1$ 之间的失配 $b_1-A_1\hat x_0$，再乘以卡尔曼增益矩阵（Kalman gain matrix）$K_1$。$K_1$ 的公式来自比较 (15) 与 (16) 两式的解 $\hat x_0$ 与 $\hat x_1$。而且当我们基于新数据 $b_1$ 把 $\hat x_0$ 更新到 $\hat x_1$ 时，也要把协方差矩阵 $W_0$ 更新到 $W_1$。

记得 $W_0=(A_0^{T}V_0^{-1}A_0)^{-1}$，来自方程 (13)。把它的逆从 $W_0^{-1}$ 更新到 $W_1^{-1}$：

```math
W_1^{-1} = W_0^{-1} + A_1^{T}V_1^{-1}A_1
```

Covariance $W_1$ of errors in $\hat x_1$（$\hat x_1$ 误差的协方差） (18)

```math
K_1 = W_1 A_1^{T}V_1^{-1}
```

Kalman gain matrix $K_1$（卡尔曼增益矩阵） (19)

这就是卡尔曼滤波的核心。注意协方差矩阵 $W_k$ 的重要性：这些矩阵度量整个过程的可靠性，其中向量 $\hat x_k$ 基于特定的测量 $b_0$ 到 $b_k$ 估计当前状态。

当状态 $x_k$ 也在变化（基于矩阵 $F_k$）时，解释动态卡尔曼滤波需要整章整本书。它先有一步用 $F$ 对 $x_k$ 的预测（prediction），再有一步用新数据 $b$ 的修正（correction）。也许最好到此为止！

本页讲的是递推最小二乘（recursive least squares）：加入新数据 $b_k$，基于全部数据更新最优的当前估计，并更新它的协方差矩阵 $W_k$。

这个更新思想始于 III.1 节的 Sherman–Morrison–Woodbury 公式（关于 $(A-UV^{T})^{-1}$）。数值上，这是卡尔曼成功的钥匙——把大小为 $n$ 的逆矩阵换成大小为 $k$ 的逆矩阵。

---

<!-- page 312 -->

> <span style="color:#7f8c8d;">本页为书页 310，属 V.5 习题集（Problem Set V.5），共 6 题，练习加权估计、独立性下的积分分解、卡尔曼更新与动态最小二乘；页眉与印页码不译。</span>

## Problem Set V.5（习题集 V.5）

**1.** 对同一变量 $x$ 的两次测量给出两个方程 $x=b_1$ 和 $x=b_2$。设均值皆为零，方差为 $\sigma_1^2$ 与 $\sigma_2^2$，误差独立：$V$ 为对角阵，对角元为 $\sigma_1^2,\sigma_2^2$。把这两个方程写成 $Ax=b$（$A$ 是 $2\times1$）。如正文例 1，求基于 $b_1,b_2$ 的最优估计：

```math
\hat x = \frac{b_1/\sigma_1^2 + b_2/\sigma_2^2}{1/\sigma_1^2 + 1/\sigma_2^2}.
```

**2.** (a) 在第 1 题中，设第二次测量 $b_2$ 变得极其精确，其方差 $\sigma_2^2\to 0$。当 $\sigma_2^2$ 趋于零时，最优估计 $\hat x$ 是多少？

(b) 相反的情形是 $\sigma_2^2\to\infty$，$b_2$ 不含任何信息。此时基于 $b_1,b_2$ 的最优估计又是多少？

**3.** 若 $x$ 与 $y$ 独立，概率分别为 $p_1(x)$ 与 $p_2(y)$，则 $p(x,y)=p_1(x)\,p_2(y)$。通过把二重积分拆成一元积分之积（从 $-\infty$ 到 $\infty$），证明

```math
\iint p(x,y)\,dx\,dy = 1
\qquad\text{且}\qquad
\iint (x+y)\,p(x,y)\,dx\,dy = m_1 + m_2 .
```

**4.** 续第 3 题对独立 $x,y$，证明 $p(x,y)=p_1(x)p_2(y)$ 满足

```math
\iint (x-m_1)^2 p(x,y)\,dx\,dy = \sigma_1^2,
\qquad
\iint (x-m_1)(y-m_2)\,p(x,y)\,dx\,dy = 0 .
```

于是 $2\times2$ 协方差矩阵 $V$ 是对角的，其对角元为 $\sigma_1^2,\sigma_2^2$。

**5.** 设 $\hat x_k$ 是 $b_1,\dots,b_k$ 的平均。一个新的测量 $b_{k+1}$ 到来。卡尔曼更新方程 (17) 给出新平均：

```math
\hat x_{k+1} = \hat x_k + \frac{1}{k+1}(b_{k+1}-\hat x_k).
```

验证 $\hat x_{k+1}$ 确实是 $b_1,\dots,b_{k+1}$ 的正确平均。

再验证平均值的方差更新方程 (18)：在假设 $W_k=\sigma^2/k$ 且 $b_{k+1}$ 的方差 $V=\sigma^2$ 下，得到

```math
W_{k+1} = \frac{\sigma^2}{k+1}.
```

**6.** （稳态模型）第 5 题是静态最小二乘，所有样本平均都是对同一个 $x$ 的估计。要让卡尔曼滤波动态化，还需加入一个带自身误差方差 $s^2$ 的状态方程 $x_{k+1}=Fx_k$。动态最小二乘问题允许 $x$ 随 $k$ 增大而"漂移"：

```math
\begin{cases}
b_0 = x_0 \\[2pt]
b_1 = x_1 \\[2pt]
b_2 = x_2
\end{cases}
\qquad
\begin{cases}
x_1 = F x_0 \\[2pt]
x_2 = F x_1
\end{cases}
```

各方程带方差 $s^2,\sigma_1^2,\sigma_2^2$。取 $F=1$，把这三个方程两边除以相应的 $s,\sigma_1,\sigma_2$，用最小二乘求 $x_0$ 与 $x_1$，这会给更近期的 $b_1$ 更大权重。卡尔曼滤波在《Algorithms for Global Positioning》（Borre 与 Strang）中展开。

---

## 译者注

<span style="color:#27ae60;">**注 1：为什么"除以 $\sigma_i$"能把方程"白化"？** 加权最小二乘的全部技巧，在于用协方差矩阵的逆 $V^{-1}$ 去"消掉"误差的异质性。设第 $i$ 个方程 $b_i$ 的方差是 $\sigma_i^2$。若把它除以 $\sigma_i$，新右端 $b_i/\sigma_i$ 的方差就是 $\operatorname{Var}(b_i/\sigma_i)=\sigma_i^2/\sigma_i^2=1$。于是所有加权后的方程都变成方差为 1、彼此（因独立）协方差为 0 的"标准噪声"，即正文说的 white noise。这一步等价于作线性变换 $b\mapsto V^{-1/2}b$，其中 $V^{-1/2}=\operatorname{diag}(1/\sigma_1,\dots,1/\sigma_m)$；对 $A$ 也做同样变换 $A\mapsto V^{-1/2}A$，再套用普通最小二乘 $A^{T}A\hat x=A^{T}b$，把 $V^{-1/2}$ 代进去、合并，正好得到 (12) 的 $A^{T}V^{-1}A\hat x=A^{T}V^{-1}b$。所以"白化→普通最小二乘"与"直接写加权正规方程"是同一件事的两种说法——这正是 V.4 节协方差在线性变换下按 $LVL^{T}$ 传播的直接推论。</span>

<span style="color:#27ae60;">**注 2：估计量方差 $W=(A^{T}V^{-1}A)^{-1}$ 为什么是"最小的"？** 一旦取定 $\hat x=Lb$（线性）且要求无偏 $LA=I$，那么 $\hat x$ 的协方差就是 $W=LVL^{T}$。关键恒等式 $LVL^{T}=(A^{T}V^{-1}A)^{-1}$ 只有在 $L=(A^{T}V^{-1}A)^{-1}A^{T}V^{-1}$（即加权正规方程的解）时才成立。任何别的无偏线性估计 $\hat x^{*}=L^{*}b$（$L^{*}A=I$）都有 $L^{*}V L^{*T}-W\succeq 0$（正半定），也就是说：无论沿哪个方向看，$W$ 都给出不更大的方差——这就是 Gauss–Markov/BLUE 定理。直观上，$V^{-1}$ 把可靠（方差小）的方程权重放大、不可靠的权重压低，从而"榨取"出最小方差。注意 (13) 里的 $W$ 与 $b$ 无关，只由 $A$ 和 $V$ 决定：它描述的是整个实验的可靠性，而非某一次样本的好坏，这正是本节"关心的不是某个 $b$ 的最优 $\hat x$，而是可靠性"那句话的落点。</span>

<span style="color:#27ae60;">**注 3：卡尔曼更新 (17)–(19) 与 III.1 节的关系。** 递推最小二乘想避免每来一个新数据就重解一个大方程组，而希望"在旧解上做一次小修正"。以两个数据块为例，新问题的正规方程是 $(A_0^{T}V_0^{-1}A_0+A_1^{T}V_1^{-1}A_1)\hat x_1=A_0^{T}V_0^{-1}b_0+A_1^{T}V_1^{-1}b_1$。记 $W_0^{-1}=A_0^{T}V_0^{-1}A_0$，则新协方差的逆是 $W_1^{-1}=W_0^{-1}+A_1^{T}V_1^{-1}A_1$（这就是 (18)）。要由 $\hat x_0$ 得到 $\hat x_1$，需要用 $W_1=(W_0^{-1}+A_1^{T}V_1^{-1}A_1)^{-1}$ 去求逆。而 III.1 节的 Sherman–Morrison–Woodbury 公式正是给出"秩一（或低秩）修正下的逆更新"：它把对一个 $n\times n$ 矩阵求逆，换成对一个小得多的修正子块求逆。这里 $A_1^{T}V_1^{-1}A_1$ 的秩不超过新数据数 $k$，于是每步只需对 $k\times k$ 的矩阵求逆，而非重解 $n\times n$ 系统——这是卡尔曼滤波在数值上高效、能在线实时运行的根本原因。正文末句"把大小为 $n$ 的逆矩阵换成大小为 $k$ 的逆矩阵"说的正是这个交换。</span>

---

## 本节译者注

> <span style="color:#1e8449;">**[note] 为什么要用协方差矩阵的逆 $V^{-1}$ 来刻画「依赖」：**</span> 一元高斯 $p(x)\propto e^{-(x-m)^2/(2\sigma^2)}$ 里，方差 $\sigma^2$ 出现在分母，控制着钟形曲线「有多宽」；推广到多个变量时，自然的猜测是把指数里的平方写成二次型 $(\mathbf{x}-\mathbf{m})^{\mathsf T}W(\mathbf{x}-\mathbf{m})$，而问题就变成了：那个对称正定矩阵 $W$ 该是什么？如果只是想让各分量独立（diagonal 情形），$W$ 应取对角元 $1/\sigma_i^2$；一旦变量之间相关，就必须让 $W$ 承担「同时度量每个方向的离散程度与彼此之间的耦合」的任务。答案是 $W=V^{-1}$，其中 $V$ 是协方差矩阵（covariance matrix），其元 $V_{ij}=\mathbb{E}[(x_i-m_i)(x_j-m_j)]$ 直接度量 $x_i$ 与 $x_j$ 的同涨同落。取逆的原因在归一化里看得最清楚：常数因子里出现的是 $\det V$（的平方根），而只有 $W=V^{-1}$ 才能让 $\int e^{-(\mathbf{x}-\mathbf{m})^{\mathsf T}V^{-1}(\mathbf{x}-\mathbf{m})/2}\,d\mathbf{x}$ 这个 $M$ 维积分恰好等于 $\sqrt{(2\pi)^M\det V}$，使总概率归一为 $1$。也就是说，$V$ 描述「协方差」，$V^{-1}$（常被称为精度矩阵，precision matrix）才进入概率密度的指数——这正是为什么后文加权最小二乘里权重取的也是 $V^{-1}$ 而非 $V$：可靠的信息（方差小的分量）在 $V^{-1}$ 中权重反而大。

> <span style="color:#1e8449;">**[note] 对角化 $V=Q\Lambda Q^{\mathsf T}$ 为什么能把 $M$ 维积分「拆成 $M$ 个一维积分」：**</span> 这是全书「线性代数帮微积分算积分」这一主题在概率上的又一次现身。指数里的二次型 $(\mathbf{x}-\mathbf{m})^{\mathsf T}V^{-1}(\mathbf{x}-\mathbf{m})$ 一般不是平方和的形式，因为 $V^{-1}$ 非对角；但 $V$ 是对称正定矩阵，可写成 $V=Q\Lambda Q^{\mathsf T}$，其中 $Q$ 的列是标准正交特征向量，$\Lambda=\operatorname{diag}(\lambda_1,\dots,\lambda_M)$。于是 $V^{-1}=Q\Lambda^{-1}Q^{\mathsf T}$，代入并令 $\mathbf{Y}=Q^{\mathsf T}\mathbf{X}=Q^{\mathsf T}(\mathbf{x}-\mathbf{m})$，二次型就变成 $\mathbf{Y}^{\mathsf T}\Lambda^{-1}\mathbf{Y}=\sum_i y_i^2/\lambda_i$——交叉项全部消失。这一步的统计含义是：新变量 $Y_1,\dots,Y_M$ 的协方差矩阵恰是 $\Lambda$，对角线外全为零，即它们是**相互独立**的，作者说的「去相关（uncorrelating）」正是这个意思。由于 $\mathbf{Y}=Q^{\mathsf T}\mathbf{X}$ 是正交变换，其 Jacobi 行列式的绝对值为 $1$，体积元不变，于是 $M$ 重积分 $\int e^{-\sum_i y_i^2/(2\lambda_i)}\,d\mathbf{y}$ 按 Fubini 定理拆成 $\prod_i \int e^{-y_i^2/(2\lambda_i)}\,dy_i$ 这 $M$ 个已知的一维高斯积分，各自等于 $\sqrt{2\pi\lambda_i}$，乘起来就是 $\sqrt{(2\pi)^M\det\Lambda}=\sqrt{(2\pi)^M\det V}$，与式 (7) 吻合。式 (7) 的归一化常数之所以是 $\det V$，根子就在这里：$\det V=\det\Lambda=\lambda_1\cdots\lambda_M$ 恰是各独立方向方差的乘积。

> <span style="color:#1e8449;">**[note] 加权最小二乘与 §IV、§III.1 及卡尔曼滤波的呼应：**</span> 本节式 (10) 的加权正规方程 $A^{\mathsf T}V^{-1}A\hat{x}=A^{\mathsf T}V^{-1}b$，就是 §IV 中普通最小二乘 $A^{\mathsf T}A\hat{x}=A^{\mathsf T}b$ 在「噪声不独立、方差不等」时的推广：先把 $A\mathbf{x}=b$ 左乘 $V^{-1/2}=\operatorname{diag}(1/\sigma_1,\dots,1/\sigma_m)$ 得到 $V^{-1/2}A\mathbf{x}=V^{-1/2}b$，让每个方程 $b_i/\sigma_i$ 都具有方差 $1$——这就是作者说的「白化（whitening）」噪声，使标准高斯 $N(0,1)$ 的假设重新成立，再套普通最小二乘即得式 (12)。举 §例 1 的数值：医生三次测心率，方差为 $1/9,1/4,1$，对应权重 $3,2,1$，最佳加权平均 $\hat{x}=(9b_1+4b_2+b_3)/14$，方差 $W=(1/9+1/4+1)^{-1}=1/14$——比只信 $b_1$ 时的 $1/9$ 更小，说明「多一次测量即使不可靠也仍降低总方差」。而末节卡尔曼滤波式 (17)–(19) 的更新 $\hat{x}_1=\hat{x}_0+K_1(b_1-A_1\hat{x}_0)$，其增益 $K_1$ 与协方差更新 $W_1^{-1}=W_0^{-1}+A_1^{\mathsf T}V_1^{-1}A_1$ 正是式 (13) $W=(A^{\mathsf T}V^{-1}A)^{-1}$ 的递归版本：每来一个新观测，就把它的精度 $A_1^{\mathsf T}V_1^{-1}A_1$ 累加到旧的逆协方差上，而不用重解整个增长中的最小二乘问题。作者点明这背后的数值关键是 §III.1 的 Sherman–Morrison–Woodbury 公式——用低维求逆替换高维求逆，这与 §IV.4 压缩感知（compressive sensing）改用 $\ell_1$ 范数求稀疏解一样，都是本书「同一条思想在不同章节反复现身」的例子。
