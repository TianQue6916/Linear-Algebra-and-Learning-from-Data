<!-- page 051: 书页 46, §I.7 Symmetric Positive Definite Matrices（对称正定矩阵） -->
# Strang LaLFD Part I（线性代数与从数据中学习）

### <span style="color:#2471a3;">**[section]**</span> **Highlights of Linear Algebra（线性代数精要）**

下面是 §I.7 关于 positive definite matrices（正定矩阵）的要点回顾，该列表自上一页开始。

- 该矩阵 $S$ 是 positive definite（正定）的：它的 eigenvalues（特征值）2 和 6 都是正的。
- 若 $Q^T = Q^{-1}$，则 $Q^T S Q$ 也是 positive definite（正定）的：得到同样的 eigenvalues（特征值）2 和 6。
- $A^T A$ 是 positive definite（正定）的，若 $A$ 是 invertible（可逆）的（这一点并不明显）。
- $S$ 是 positive definite（正定）的，当且仅当 $a > 0$ 且 $ac > b^2$。
- $S$ 只是 positive semidefinite（半正定）的：它有 $\lambda \ge 0$，但没有 $\lambda > 0$。

> <span style="color:#1e8449;">**译者注：** 本页顶部 "Highlights（要点回顾）" 列表的开头几项连同其示例矩阵 $S$ 位于上一页，本页 OCR 仅保留了以上可辨读的各项。</span>

---

### <span style="color:#2471a3;">**[section]**</span> **The Energy-based Definition（基于能量的定义）**

这里提出关于 positive definite matrices（正定矩阵）最重要的一个 idea（思想）。
这个新 approach（方法）并不直接涉及 eigenvalues（特征值），但它被证明是对 $\lambda > 0$ 的一个 perfect test（完美检验）。
这是 positive definite matrices（正定矩阵）的一个好 definition（定义）：energy test（能量检验）。

<span style="color:#2471a3;">**[definition]**</span> <span style="color:#00838f;">$S$ 是 positive definite（正定）的，如果对所有非零向量 $c$，energy（能量）$c^T S c$ 都是正的。</span>

```math
c^T S c > 0 \quad \text{对每个向量 } c \neq 0 \tag{1}
```

当然 $S = I$ 是 positive definite（正定）的：所有 $\lambda_i = 1$。
该 energy（能量）$c^T I c = c_1^2 + \cdots + c_n^2$ 在 $c \neq 0$ 时为正。
让我在一个 $2 \times 2$ 矩阵中演示这个 energy（能量），它依赖于 $c_1$ 和 $c_2$：

```math
\text{Energy } c^T S c = 2c_1^2 + 8c_1c_2 + 9c_2^2
```

这个 energy（能量）对每一对 $(c_1, c_2) \neq (0, 0)$ 都是正的吗？是的，因为它是 squares（平方）之和：

```math
c^T S c = 2c_1^2 + 8c_1c_2 + 9c_2^2 = 2(c_1 + 2c_2)^2 + c_2^2 > 0
```

我们必须把 positive energy（正能量）$c^T S c > 0$ 与 positive eigenvalues（正特征值）$\lambda > 0$ 联系起来。
若 $Sc = \lambda c$，则 $c^T S c = \lambda c^T c$，所以 $\lambda > 0$ 蕴含 $c^T S c > 0$。
上式只在每个单独的 eigenvector（特征向量）上检验了 energy（能量）。
但定理（theorem）说的是：如果每个 eigenvector（特征向量）都有 positive energy（正能量），那么所有非零向量都有 positive energy（正能量）。
若对 $S$ 的 eigenvectors（特征向量）成立 $c^T S c > 0$，则对每个非零向量 $c$ 都成立 $c^T S c > 0$。
理由如下：每个向量 $c$ 都是 eigenvectors（特征向量）的一个 combination（组合）$c = c_1x_1 + \cdots + c_nx_n$。
由于 $S$ 是 symmetric（对称）的，eigenvectors（特征向量）可以选择为 orthogonal（正交）的。
我们现在要证明：$c^T S c$ 是各 eigenvector（特征向量）中 energies（能量）$\lambda_i > 0$ 的一个 positive combination（正组合）。
> <span style="color:#7f8c8d;">Strang §I.7, p.46</span>



## 注 1 — 能量定义为何是「最好的」定义

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 作者称 energy test $c^T S c > 0$ 是正定矩阵「最好的定义」，这句话值得从设计角度追问：为什么是 $c^T S c$，而不是别的二次型？答案的第一层是，这个量在物理系统中天然出现——弹簧系统的弹性势能 $\frac{1}{2}x^T K x$、电路中的功率耗散 $I^T R I$、统计中的 Mahalanobis 距离平方 $(x-\mu)^T \Sigma^{-1}(x-\mu)$，都是同一个形式。它不是为了考试而发明的判定式，而是系统自身携带的能量量纲的量。第二层更关键：这个定义不需要对称性之外的任何假设。不必先求特征值，不必算行列式，不必做消元；对任意向量 $c$ 做一次矩阵乘法、再做一次内积即可检验。一个定义越少依赖中间工具，就越适合充当根定义。
> 从第一性原理看，energy test 的可靠性可以拆成两步。第一步：任何形如 $A^T A$（$A$ 列独立）的矩阵自动满足 $c^T S c = c^T A^T A c = \|Ac\|^2 \ge 0$，且等号只在 $Ac = 0$ 即 $c = 0$ 时成立；这里只用到了内积与范数，没有引入任何新机器。第二步：正定矩阵总能写成 $A^T A$（Cholesky 分解），所以这个检验不是碰巧成立的抽样，而是等价刻画。于是 §I.7 的五种检验中，energy test 扮演根定义的角色：当 $Sc = \lambda c$ 时 $c^T S c = \lambda c^T c$，能量的符号直接翻译成特征值的符号；其余四种检验则可以看作由这个能量判断派生出的计算接口，分别服务手算、消元、最小二乘等不同场景。
> 思想实验：想象一组由弹簧连接的质点，$K$ 是刚度矩阵。正定问题等价于问：是否存在非零位移模式 $c$，使系统总势能 $\frac{1}{2}c^T K c$ 为零或为负？若存在，说明系统在某个位移模式下不储存能量甚至释放能量，平衡态就不稳定。energy test 的物理含义因此是：任何非零位移都必须给系统注入正能量。这个实验也解释了为什么只检查特征向量不够——特征向量只是少数特殊位移模式，而稳定性要求所有可能的位移模式能量都为正；对称矩阵的正交特征基恰好保证了「特殊方向上的正性」能扩张成「所有方向上的正性」。
> 一个费曼式画面可以帮助记忆：把 $S$ 想成给空间施加的变换，$c^T S c$ 是「沿 $c$ 方向迈一步，再看这一步在 $S$ 作用后的影子是否还朝前」。若每个方向都朝前，投影为正，矩阵就是正定；若存在一个方向被推到反向，投影为负，正定就被击穿。定义因此可以被复述为一句话：$S$ 和单位矩阵共享同一种「方向感」。
> 跨课程连接：与 CSAPP 第 2 章浮点表示对照，$c^T S c$ 在机器上是有限精度求和。当 $S$ 条件数大时，两个大数相减可能因舍入产生虚假负值，让数学上正定的矩阵在数值上被误判为不定；这是 §I.9 条件数讨论的伏笔——「最好的定义」在数学上是根，在浮点硬件上却需要数值警惕。另外，当 $S = A^T A$ 时 $c^T S c = \|Ac\|^2$，正定性等价于 $A$ 的零空间只含零向量，这与你熟悉的范数非负性同源。
> 一句话收束：energy test 把「正定」还原成最原始的问题——在所有非零方向上，系统是否都在抗拒偏离零点。
---

---

<!-- page 052: 书页 47, §I.7 Symmetric Positive Definite Matrices（对称正定矩阵） -->

把 $c = c_1x_1 + \cdots + c_nx_n$ 代入 energy（能量），并利用 $Sx_i = \lambda_ix_i$，就完成了上一页的证明：

```math
\begin{aligned}
c^T S c &= (c_1x_1 + \cdots + c_nx_n)^T S(c_1x_1 + \cdots + c_nx_n) \\
&= (c_1x_1 + \cdots + c_nx_n)^T (c_1\lambda_1x_1 + \cdots + c_n\lambda_nx_n) \\
&= \lambda_1c_1^2 + \cdots + \lambda_nc_n^2 > 0 \qquad \text{如果每个 } \lambda_i > 0
\end{aligned}
```

从第 2 行到第 3 行，我们使用了 $S$ 的 eigenvectors（特征向量）的 orthogonality（正交性）：$x_i^T x_j = 0$。

这里给出 energy test（能量检验）的一个典型应用，不需要知道任何 eigenvalues（特征值）或 eigenvectors（特征向量）。
如果 $S_1$ 和 $S_2$ 都是 symmetric positive definite（对称正定）的，那么 $S_1 + S_2$ 也是。

```math
c^T(S_1 + S_2)c = c^TS_1c + c^TS_2c > 0 + 0
```

> <span style="color:#7f8c8d;">把两个 energy（能量）相加（adding energies）。</span>

而 $S_1 + S_2$ 的 eigenvalues（特征值）和 eigenvectors（特征向量）并不容易求出，energies（能量）只是相加。

---

### <span style="color:#2471a3;">**[section]**</span> **Three More Equivalent Tests（另外三种等价检验）**

到目前为止我们有 tests 1 和 2（检验 1 和 2）：positive eigenvalues（正特征值）与 positive energy（正能量）。
那个 energy test（能量检验）迅速衍生出另外三个有用的 tests（检验）（可能还有别的，但我们只列出这三个）：

- **检验 3（Test 3）**：$S = A^T A$，其中 $A$ 是具有 independent columns（独立列）的矩阵。
- **检验 4（Test 4）**：$S$ 的所有 leading determinants（前导行列式）$D_1, D_2, \dots, D_n$ 都是正的。
- **检验 5（Test 5）**：$S$ 的所有 pivots（主元）都是正的（在 elimination（消元）中）。

检验 3（Test 3）适用于 $S = A^T A$。为什么在这个 test（检验）中 $A$ 的 columns 必须 independent（独立）？请看这些 parentheses（括号）：

```math
c^T S c = c^T A^T A c = (Ac)^T(Ac) = \|Ac\|^2 \tag{2}
```

这些 parentheses（括号）就是关键：energy（能量）是向量 $Ac$ 的 length squared（长度平方）。
只要 $Ac$ 不是 zero vector（零向量），这个 energy（能量）就是正的。
要保证 $c \neq 0$ 时 $Ac \neq 0$，$A$ 的 columns（列）必须 independent（独立）。
在这个 $2 \times 3$ 例子中，$A$ 有 dependent columns（相关列）：

```math
A = \begin{bmatrix}1&1&1\\1&2&3\end{bmatrix}, \qquad
S = A^T A = \begin{bmatrix}2&3&4\\3&5&7\\4&7&10\end{bmatrix}
```

这个 $S$ 不是 positive definite（正定）的：这里 column 1 + column 3 = 2(column 2)。
于是 $c = (1, -2, 1)$ 有 zero energy（零能量）：它是 $A^T A$ 的对应 $\lambda = 0$ 的 eigenvector（特征向量）。
所以 $S = A^T A$ 只是 positive semidefinite（半正定）的。
方程 (2)（Equation (2)）说明 $A^T A$ 至少是 positive semidefinite（半正定）的，因为 $c^T S c = \|Ac\|^2$ 永远不会为负。
那个 energy（能量）$\|Ac\|^2$ 有可能为零吗？可以，恰好当 $Ac = 0$ 时。

---

### <span style="color:#2471a3;">**[section]**</span> **Determinant Test and Pivot Test（行列式检验与主元检验）**

对于小型矩阵，determinant test（行列式检验）是最快的。
我将在下面这个 $4 \times 4$ 的 symmetric second difference matrix（对称二阶差分矩阵）中标出四个 leading determinants（前导行列式）$D_1, D_2, D_3, D_4$。

> <span style="color:#1e8449;">**译者注：** 这个 $4 \times 4$ 二阶差分矩阵及其 leading determinants（前导行列式）的具体数值将在下一页（第 48 页）继续展开。</span>

---

<!-- page 053: 书页 48, §I.7 Symmetric Positive Definite Matrices -->

# Strang LaLFD Part I（线性代数与从数据中学习）

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.7 对称正定矩阵（Symmetric Positive Definite Matrices）（续）</span>

### 行列式检验与主元检验（Determinant Test and Pivot Test）

这个 $4\times4$ 对称二阶差分矩阵的四个 leading determinants（前导行列式）分别是：

```math
D_1 = 2, \qquad D_2 = 3, \qquad D_3 = 4, \qquad D_4 = 5
```

行列式检验（determinant test）在这里通过了！

能量（energy）$c^TSc$ 也必须是正的。

前导行列式与 pivots（主元）密切相关——主元就是消元（elimination）后留在主对角线上的那些数。

这里第一个主元是 2。

第二个主元出现在把 row 1（行 1）加到 row 2（行 2）上之后。

第三个主元出现在把 new row 2（新行 2）加到 row 3（行 3）上之后。

那些分数 $2,\ \tfrac{3}{2},\ \tfrac{4}{3}$ 都是行列式之比！

最后一个主元是 $\Delta_4/\Delta_3 = 5/4$。

第 $k$ 个主元等于比值 $\Delta_k/\Delta_{k-1}$。

因此当所有前导行列式都为正时，所有主元也都为正。

我可以很快地把这两个检验（4 和 5）与第三个检验 $S = A^TA$ 联系起来。

事实上，对 $S$ 做消元就会产生一个重要的 $A$ 的选择。

回想一下，早先的消元产生的是 $S = LU$（$L$ 的对角线上是 1，$U$ 中装着主元）。

但对于 symmetric matrices（对称矩阵），我们可以把 $S$ 均衡地写成 $S = LDL^T$：把主元抽出来放进 $D$，再把这些平方根（square roots）在 $L$ 与 $L^T$ 之间平分。

```math
\begin{aligned}
S &= LU \tag{3} \\
  &= LDL^T \tag{4} \\
  &= A^TA \tag{5}
\end{aligned}
```

我对那些平方根有点不放心——但 $S = A^TA$ 这个模式是漂亮的：取 $A = \sqrt{D}\,L^T$。

消元把每一个 positive definite（正定）的 $S$ 分解成 $A^TA$（其中 $A$ 是上三角矩阵）。

这就是 Cholesky factorization（乔列斯基分解）$S = A^TA$，主元位于 $A$ 的主对角线上。

> <span style="color:#1e8449;">译者注：更精确地说，$A = \sqrt{D}\,L^T$ 的主对角线上的元素是主元的平方根 $\sqrt{d_1}, \dots, \sqrt{d_n}$；这正对应标准 Cholesky 形式 $S = LL^T$ 中 $L$ 的对角线元素。</span>



## 注 2 — Cholesky 分解：对称版的 LU

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 第 053 页 的三行等式 $S = LU = LDL^T = A^T A$ 值得逐行品味。第一行是标准 LU 消元（Strang Part I 前半已详述）；第二行关键：当 $S$ 对称时，$U$ 的对角线恰好是 pivots $d_1, \dots, d_n$，把每个 pivot 抽出来放进对角矩阵 $D$，剩下的因子自然变成 $L^T$——因为对称性保证 $U = D L^T$。这正是 Gauss 消元对对称矩阵的「免费午餐」：存储量减半，计算量减半。第三行 $S = A^T A$ 更进一步：取 $A = \sqrt{D} L^T$（上三角），pivot 的平方根出现在 $A$ 的对角线上。这与标准 Cholesky 形式 $S = L L^T$（$L$ 下三角，对角元为 $\sqrt{d_i}$）是转置关系。
> 为什么对称性会自动给出 $U = D L^T$？这里的证明模板可以命名为「唯一分解夹逼法」。把对称矩阵写成 $S = L D U$，其中 $L$ 是单位下三角、$U$ 是单位上三角、$D$ 是对角；两边取转置得 $S = S^T = U^T D L^T$。由于「单位下三角、对角、单位上三角」这种分解在非零主元时是唯一的，比较两式就得到 $U^T = L$，即 $U = L^T$，于是 $S = L D L^T$。核心工具只有两个：转置不改变 $S$，以及分解的唯一性；没有任何一个新概念。对称性在这里做的事情是：把本需要单独存储的 $U$ 变成 $L^T$，也就是把上三角因子的信息全部编码进下三角因子。
> 具体例子：$S = \begin{bmatrix} 2 & 4 \\ 4 & 9 \end{bmatrix}$。消元一步得到乘数 $2$、主元 $d_1 = 2$、$d_2 = 9 - 2 \cdot 4 = 1$，于是 $L = \begin{bmatrix} 1 & 0 \\ 2 & 1 \end{bmatrix}$、$U = \begin{bmatrix} 2 & 4 \\ 0 & 1 \end{bmatrix}$，而 $L^T = \begin{bmatrix} 1 & 2 \\ 0 & 1 \end{bmatrix}$ 恰好与 $U$ 只差一个对角因子 $D = \operatorname{diag}(2, 1)$。取平方根得 $A = \sqrt{D} L^T$，能量变成 $c^T S c = \|A^T c\|^2$。关于作者「对平方根不放心」的直觉，数值上确实有对应：若某个主元 $d_k$ 非常小，$\sqrt{d_k}$ 作为除数会把绝对舍入误差放大；这直接回到条件数问题。
> 把这个例子乘回去验证：$D L^T = \begin{bmatrix}2&0\\0&1\end{bmatrix}\begin{bmatrix}1&2\\0&1\end{bmatrix} = \begin{bmatrix}2&4\\0&1\end{bmatrix} = U$，再左乘 $L$ 即恢复 $S$。唯一性也可以从第一列直接读出：$S$ 的第一列必须等于 $L$ 的第一列乘以 $d_1$，故 $d_1 = a_{11}$、$L$ 的第一列就是 $S$ 第一列除以 $d_1$；剥掉第一行第一列后对余下的 $(n-1)\times(n-1)$ 矩阵递归，这正是 6.042J 结构归纳的线性代数版——分解的存在性与唯一性由同一次递归一并证明。
> 一个可迁移的分治视角：消元求解 $S x = b$ 的流程是，先分解一次 $S$，再用前代与回代解两个三角方程组。对称性让分解阶段只需处理一个三角因子，前代与回代变成彼此转置的同一份代码；从 CSAPP 第 6 章缓存的角度看，一个三角因子占用的缓存行约为两个三角因子的一半，局部性更好，这正是「存储量减半」在硬件上的实际收益。
> 一个边界情形把适用范围钉死：若某个 pivot 为负，$LDL^T$ 仍然成立（$D$ 允许负对角元），但 $\sqrt{D}$ 会变成复数，实 Cholesky 不再存在。例如 $S = \operatorname{diag}(1,-1)$ 满足对称，却没有任何实矩阵 $A$ 使 $S = A^T A$。所以 Cholesky 的适用范围从「对称」收窄到「对称正定」，收窄换来的正是每个 pivot 都可安全开方；这也把注 3 的检验 (5)（正 pivots）与这里的第三行 $S = A^T A$ 接成一个回路。
> 跨课程连接：Cholesky 是「对称正定版的 LU」，是数值线性代数中求解 $S x = b$ 的首选算法，因为主元恒为正、不需要选主元（行交换会破坏对称性，且正定性保证不会出现零主元），计算量约为普通 LU 的一半。在凸优化与 18.065 的 Newton 法中，每次迭代要解 $H \Delta x = -g$，$H$ 的 Cholesky 因子是核心计算步骤；在 CSAPP 第 2 章浮点视角下，这一步涉及有限精度下的 $\sqrt{d_k}$ 与除法，病态 Hessian 会让 Newton 步长不可靠，正好接上后文条件数的讨论。
> 一句话收束：Cholesky 不是新算法，而是对称性帮你把 LU 里的 $U$ 免费换成了 $L^T$。
---

---

<!-- page 054: 书页 49, §I.7 Symmetric Positive Definite Matrices -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.7 对称正定矩阵（Symmetric Positive Definite Matrices）（续）</span>

### 检验 $S = A^TA$：$A$ 的特殊选择（The Test $S = A^TA$: Special Choices for $A$）

要在 $S$ 正定时应用检验 $S = A^TA$，我们必须至少找出一种可行的 $A$。

关于 $A$，选择有很多，其中包括（1）symmetric（对称）的和（2）triangular（三角）的。

**选择 1：** 如果 $S = Q\Lambda Q^T$，就对这些特征值取平方根，那么 $A = Q\sqrt{\Lambda}\,Q^T = \sqrt{S}$，即 $S$ 的平方根。

**选择 2：** 如果 $S = LU = LDL^T$，且 $D$ 中的主元为正，那么 $S = (L\sqrt{D})(\sqrt{D}\,L^T)$。

关于 $S$，正定性的五个检验（five tests）涉及线性代数的不同部分——来自消元的主元、行列式、特征值，以及 $S = A^TA$。

每一个检验都能独立给出完整的答案：positive definite（正定）、semidefinite（半正定），或者两者都不是。

正的能量 $c^TSc > 0$ 是最好的定义：它把所有这些检验都联系在了一起。

### 正定矩阵与最小值问题（Positive Definite Matrices and Minimum Problems）

假设 $S$ 是一个对称正定的 $2\times2$ 矩阵，对它应用四个检验：

- 行列式（determinants）：$a > 0$，$ac - b^2 > 0$
- 主元（pivots）：$a > 0$，$(ac - b^2)/a > 0$
- 特征值（eigenvalues）：$\lambda_1 > 0$，$\lambda_2 > 0$
- 能量（energy）：$ax^2 + 2bxy + cy^2 > 0$

我选一个 $a = c = 5$、$b = 4$ 的例子。

这个矩阵 $S$ 有特征值 $\lambda = 9$ 和 $\lambda = 1$。

它的能量为 $E = 5x^2 + 8xy + 5y^2 > 0$。

这个能量函数 $E$ 的图像是一个向上开口的碗（bowl）。

碗的底点在 $x = y = 0$ 处，那里的能量为 $E = 0$。

这把微积分（calculus）中的最小值问题（minimum problems）与线性代数中的正定矩阵联系在了一起。

本书的 Part VI 将描述数值极小化（numerical minimization）。

对于最好的问题，函数是 strictly convex（严格凸）的——就像一条向上开口的抛物线。

这里有一个完美的检验：二阶导数在所有的点处都是正定的。

我们身处高维之中，但线性代数能够识别出二阶导数矩阵（second derivative matrix）的关键性质。

对于单变量函数 $f(x)$，极小值的检验是著名的：

若在 $x = x_0$ 处一阶导数 $df/dx = 0$ 且二阶导数 $d^2f/dx^2 > 0$，则达到极小值（minimum）。

对于双变量函数 $f(x, y)$，二阶导数进入一个 Hessian matrix（海森矩阵），它必须是正定的：

若在 $(x_0, y_0)$ 处 $\partial f/\partial x = 0$、$\partial f/\partial y = 0$，并且海森矩阵

```math
\begin{bmatrix}
\partial^2 f/\partial x^2 & \partial^2 f/\partial x \partial y \\
\partial^2 f/\partial y \partial x & \partial^2 f/\partial y^2
\end{bmatrix}
```

是 positive definite（正定）的，则达到极小值。

曲面 $z = f(x, y)$ 在该点是水平的（flat），因为 $\partial f/\partial x = \partial f/\partial y = 0$。

只要二阶导数矩阵是正定的，曲面就向上弯。

于是我们就得到了函数的一个最小值点（minimum point）。



## 注 3 — 五个等价检验作为证明策略模板

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 第 054 页 总结的五种等价检验是线性代数中一个经典证明策略模板的展演：多重表征法。核心思想是，对一个数学对象给出若干看似不同但逻辑等价的刻画，然后按任务选用最便利的那一个。正定矩阵的五种刻画——(1) 正特征值、(2) $c^T S c > 0$、(3) $S = A^T A$（$A$ 列独立）、(4) 正 leading determinants、(5) 正 pivots——各自擅长不同场景：检验 (2) 最适合理论推导（证明 $S_1 + S_2$ 正定时不需要算特征值）；检验 (4) 最适合手算 $3 \times 3$ 以下矩阵；检验 (5) 连通消元法的计算流程；检验 (3) 连通最小二乘（$A^T A$ 的法方程矩阵）。
> 为什么「同一个对象有多个等价定义」是好的证明工具？可以把它想成接口抽象：每个检验暴露不同的计算接口，但背后是同一个数据类型。证明 $A \Rightarrow B$ 时，你不需要从 (1) 硬推到 (2)，而是沿着循环路径走：$c^T S c = x^T (Q \Lambda Q^T) x$ 把能量写成特征值的加权平方和，于是 (1) 直接给出 (2)；$S = A^T A$ 给出 $c^T S c = \|Ac\|^2$，于是 (3) 给出 (2)；Gauss 消元给出 $S = L D L^T$，能量的配方形式出现正主元平方，于是 (5) 给出 (2)。这些路径的终点都是 energy test，说明它确实是根定义。这也解释了为什么等价性证明通常组织成循环蕴含：不必逐一证明两两等价，只要把五个结点串成一个环，环上任两点都能顺箭头和逆箭头到达，这在 6.042J 的关系与证明里是同一个套路。
> 具体验证：$S = \begin{bmatrix} 2 & 4 \\ 4 & 9 \end{bmatrix}$ 用五种接口各查一遍。特征值 $\lambda = \frac{11 \pm \sqrt{73}}{2}$ 近似 $10.77$ 与 $0.23$，为正；$c^T S c = 2c_1^2 + 8c_1 c_2 + 9c_2^2 = 2(c_1 + 2c_2)^2 + c_2^2 > 0$；$S = A^T A$ 取 $A = \sqrt{D} L^T$；leading determinants 为 $2$ 与 $2$；pivots 为 $2$ 与 $1$。同一句话，五种说法。而接口选择的经济性可以当场演示：若要证明 $S_1 + S_2$ 正定，直接写 $c^T(S_1+S_2)c = c^T S_1 c + c^T S_2 c > 0$，一行结束；若改用特征值检验，两个矩阵的特征向量未必相同，$S_1 + S_2$ 的特征值无法由 $S_1$ 与 $S_2$ 的特征值直接读出，证明会立刻卡住。
> 三维版本：$S = \begin{bmatrix}2&4&0\\4&9&1\\0&1&2\end{bmatrix}$，消元 pivot 依次为 $2,1,1$，leading determinants 依次为 $2,2,2$——两者数值不同但符号一致，正性只要求符号，不要求数值相同。用检验 (5) 最顺：三个正 pivot 直接判定，副产品就是 $LDL^T$ 分解。
> 接口选择的复杂度差异也可以量化：检验 (2) 只花一次二次型展开；检验 (4) 递推算 $n$ 个 leading determinants，朴素实现 $O(n^3)$，但可复用消元；检验 (1) 对 $n\ge5$ 没有根式通解，只能数值迭代；检验 (5) 就是消元本身，$O(n^3/3)$ 且顺带给出 Cholesky 因子。五种接口结论相同，副产品却各有用处——这正是实际计算偏爱 pivot 检验的原因。再补两个结构性质：正定矩阵对加法与正标量乘法封闭（energy test 一行即证），但对矩阵乘法不封闭；6.042J 的视角下，五个谓词切出同一个集合，循环蕴含是传递性的最优利用——$n$ 个命题两两互推要 $n(n-1)$ 个蕴含，串成环只需 $n$ 个。
> 跨课程连接：这种多重表征策略在离散数学 6.042J 中反复出现，例如「树」的多个等价定义（连通无环、$n-1$ 条边、连通且删任一边不连通等），本质是同一概念的多个接口，选对接口比硬算快一个量级。CLRS 第 15 章动态规划也给出同构现象：同一个子问题递推既可以用自顶向下的备忘递归实现，也可以用自底向上的填表实现，两种实现等价，只是缓存命中顺序不同。今后做 Problem Set 1.7 时，建议把五种检验整理成一张对照表，每次解题前先问自己：「这个题目用哪种检验最快？」
> 一句话收束：多重表征的价值不在于知道得更多，而在于知道每个时刻该调用哪个接口。
---



## 注 4 — 正定矩阵与最小值的桥梁：Hessian

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 第 054 页 末尾建立了微积分与线性代数最直接的桥梁：多元函数 $f(x, y)$ 在某点取极小值的二阶条件，等价于 Hessian 矩阵在该点正定。直觉链条是：一阶导数为零保证该点水平（切平面是平的）；二阶导数矩阵的正定性保证该点朝所有方向向上弯曲——即「碗的底部」。单变量情形 $f''(x_0) > 0$ 是熟悉的抛物线开口向上；多元情形则是二次型 $(dx)^T H (dx) > 0$ 对所有微扰 $dx \neq 0$ 成立，这正是 energy test 的微积分版本。
> 这个桥梁的论证可以拆成三块，构成一个可复用的证明模板。第一块是一阶条件：一阶偏导全为零意味着梯度 $\nabla f = 0$，函数在切平面上静止。第二块是二阶展开：在驻点附近写出带 Lagrange 余项的二阶 Taylor 展开，沿方向 $v$ 的变化为 $f(x_0 + v) - f(x_0) = \frac{1}{2} v^T H(\xi) v$，其中 $\xi$ 在 $x_0$ 与 $x_0 + v$ 之间。第三块是关键：对二次型应用「特征分解加范数下界」。当 $H(x_0)$ 正定且二阶偏导连续时，$H(\xi)$ 在充分小的邻域内仍正定；把 $H(\xi) = Q \Lambda Q^T$ 对角化，令 $y = Q^T v$ 得 $v^T H(\xi) v = \sum_i \lambda_i y_i^2 \ge \lambda_{\min} \|v\|^2 > 0$。这个下界一旦成立，正曲率就覆盖了所有方向，极小值从「看起来像」变成「证明是」。这一串用到的全部工具——对称性、正交对角化、范数非负性、连续性——都来自你已经掌握的 Strang 与 TBB 内容。
> 具体例子：$f(x, y) = x^2 + 3y^2$ 在原点一阶导数为零，$H = \begin{bmatrix} 2 & 0 \\ 0 & 6 \end{bmatrix}$ 正定，原点确实是极小值。更有趣的是「只有一阶信息会骗人」的例子：$g(x, y) = x^2 - y^2$ 在原点一阶导数为零，但 $H = \begin{bmatrix} 2 & 0 \\ 0 & -2 \end{bmatrix}$ 有负特征值，沿 $y$ 轴方向曲面向下弯，原点不是极小值。这就是为什么必须检验所有方向，而二次型恰好提供全方向的统一检验。
> 正定与半正定的边界同样值得亲手做一遍。$h(x, y) = x^2 + y^4$ 在原点一阶导数为零，$H = \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix}$ 只是半正定，二阶检验无法下结论；但沿任何方向，$y^4$ 的非负性都压过了 $y^2$ 的缺失，原点实际上是极小值。这个例子说明：正定给出的是充分条件，不是必要条件；半正定时不判定的真空地带只能靠更高阶项或直接放缩来填补，这也正是 TBB 中极限与不等式工具派上用场的时刻。
> 更高阶退化的两个例子值得并排：$f(x,y)=x^4+y^4$ 在原点 $H=0$（零矩阵），二阶检验完全失明，但原点仍是极小值；$f(x,y)=-x^4-y^4$ 的 Hessian 同样是零矩阵，原点却是极大值。这组对照说明二阶检验的盲区由四阶项决定，此时只能回到 TBB 的不等式放缩，直接证明 $f(x,y)\ge0$ 或 $f(x,y)\le0$。
> 跨课程连接：Hessian 的对称性来自混合偏导数的可交换性，这正是 Thomson-Bruckner-Bruckner《Elementary Real Analysis》中 Clairaut 定理的内容；它使 Hessian 天然落入谱定理的管辖范围，可以被正交对角化。正定 Hessian 的条件数 $\kappa(H) = \lambda_{\max}/\lambda_{\min}$ 决定梯度下降在该点附近的收敛速度——$\kappa$ 越大，碗越「扁长」，梯度下降越慢，这直接通向 Part VI 的数值优化和机器学习中 loss landscape 的几何分析。建议在心里锚定：Hessian 的正定性等于碗的局部曲率处处向上。
> 优化视角再补一处：在局部二次模型 $f(x)\approx\frac12 x^T H x$ 上，最速下降的最优步长与 $1/\lambda_{\max}$ 同阶，收敛速率由 $\kappa(H)=\lambda_{\max}/\lambda_{\min}$ 控制；$\kappa$ 越大，等高线越像细长山谷，梯度方向与指向谷底的方向夹角越大，只能走之字形。正定性回答「是不是极小值」，条件数回答「找到它有多难」——两个问题共用同一个 Hessian。
> 一句话收束：正定性是把「导数等于零」升级为「极小值」的那一枚印章。
---

---

<!-- page 055: 书页 50, §I.7 结尾 — Optimization and Machine Learning / The Ellipse x^TAx = 1 -->

### Highlights of Linear Algebra（线性代数要点）

<span style="color:#2471a3;">**[note]**</span> 本页插图展示的是二次函数 $f = ax^2 + 2bxy + cy^2$ 的图形：当矩阵 $S$ 正定（positive definite）时，它是一个碗（bowl）。图中的标注给出了 2×2 情形的正定条件——二阶导数（second derivatives）满足 $a > 0$ 且 $ac > b^2$，并且能量处处满足 $x^TSx > 0$。

> <span style="color:#7f8c8d;">图注：插图中的碗形是二次函数 $f = ax^2 + 2bxy + cy^2$ 的图形。标注的 $a > 0$ 与 $ac > b^2$ 是行列式检验（determinant test）的两个条件，$x^TSx > 0$ 是能量检验（energy test）——它们都是 $2\times2$ 矩阵 $S$ 正定性的等价刻画。</span>

当 $S$ 正定时，$f = ax^2 + 2bxy + cy^2$ 的图形是一个碗。若 $S$ 有某个负特征值（eigenvalue）$\lambda < 0$，图形就会降到零以下。当 $S$ 负定（negative definite，所有 $\lambda < 0$）时，图形是倒扣的碗（upside down bowl），此时存在最大值。当 $S$ 同时具有正、负特征值时，出现一个鞍点（saddle point）。这样的鞍点矩阵称为不定（indefinite）矩阵。

---

### Optimization and Machine Learning（优化与机器学习）

下面我们把这些代数检验与优化（optimization）联系起来。

本书的第六部分（Part VI）将讲述梯度下降（gradient descent）。每一步都沿最陡方向（steepest direction）前进，直奔碗的底部点 $x^*$。但最陡方向会随着我们不断下降而改变。这正是微积分与线性代数交汇之处——在最小值点（minimum point）$x^*$ 处。

**微积分（Calculus）**：$f$ 的所有偏导数（partial derivatives）在 $x^*$ 处都为零：

```math
\frac{\partial f}{\partial x_i} = 0, \qquad i = 1, \dots, n
```

**线性代数（Linear algebra）**：二阶导数组成的矩阵 $S$（Hessian matrix，即海森矩阵）在 $x^*$ 处是正定的。

若 $S$ 在所有点都正定（或半正定 semidefinite），则函数 $f(x)$ 是凸的（convex）。若 $S$ 的特征值始终高于某个正数，则函数 $f(x)$ 是严格凸的（strictly convex）。这些是最值得优化的函数。它们只有一个最小值，梯度下降必定能找到它。严格凸性保证函数只有一个碗底，这正是梯度下降不会陷入多个局部最小值的原因。

机器学习（machine learning）产生的损失函数（loss functions）中含有成千上万个变量。它们度量误差（error）——正是我们要最小化的量。但要计算二阶导数完全不可能。我们利用一阶导数来告诉我们移动的方向——误差在最陡方向上下降最快。然后我们沿新的方向再迈出一步下降。这是最小二乘（least squares）、神经网络（neural nets）和深度学习（deep learning）中的核心计算。在这些情形下，只有一阶导数可用，梯度下降便成为训练这些模型的基本算法。

---

### The Ellipse $x^TAx = 1$（椭圆）

仍取正定矩阵 $S$。其能量（energy）$E = x^TSx$ 的图形是一个向上开口的碗。在高度 $x^TSx = 1$ 处横截这个碗，沿截口绕行的曲线就是一个椭圆（ellipse）。这条曲线上的每个点都满足能量 $E = 1$，因而它正是方程 $x^TSx = 1$ 的图形。

本例的特征值为 $\lambda = 9$ 和 $1$。能量椭圆（energy ellipse）$5x^2 + 8xy + 5y^2 = 1$ 见图 1.9。图 1.9 展示了这个椭圆：它来自 $x^TAx = 1$ 的高度截面，形状由 $S$ 的两个特征值决定。

---

<!-- page 056: 书页 51, §I.7 结尾 — The Ellipse x^TAx = 1 与主轴定理 -->
<!-- 页眉: 1.7 Symmetric Positive Definite Matrices（对称正定矩阵） -->

**Figure 1.9（图 1.9）**：倾斜的椭圆（tilted ellipse）$5x^2 + 8xy + 5y^2 = 1$。摆正（lined up）之后它是 $9X^2 + Y^2 = 1$。

特征向量（eigenvectors）为 $q_1 = (1, 1)$ 与 $q_2 = (1, -1)$。除以 $\sqrt{2}$ 就得到单位向量（unit vectors）。于是 $S = Q\Lambda Q^T$。现在左乘 $x^T$、右乘 $x$，得到能量 $x^TSx = (x^TQ)\Lambda(Q^Tx)$。$S$ 的特征值是 $9$ 和 $1$。

> <span style="color:#7f8c8d;">图 1.9 中的标注：原坐标下的能量方程 $x^TSx = 1$；摆正后 $X^T\Lambda X = \lambda_1 X^2 + \lambda_2 Y^2 = 9X^2 + Y^2 = 1$；平方和（sum of squares）$5x^2 + 8xy + 5y^2$；端点 $(0, 1)$。</span>

数字 $9$ 和 $1$ 来自平方项的内部。你可以看到，$q_1$ 与 $q_2$ 的方向正是倾斜椭圆所指的方向——即 $S$ 的特征向量方向。这解释了为什么 $S = Q\Lambda Q^T$ 被称为主轴定理（principal axis theorem）：它把轴（axes）展示了出来。不仅有方向（来自特征向量），还有轴长（来自特征值）：长度 $= 1/\sqrt{\lambda}$。

要看清楚这一切，用大写字母表示摆正椭圆所用的新坐标（coordinates）$X, Y$：

```math
\mathbf{x} = Q\mathbf{X}, \qquad \text{即 } \mathbf{x} = X q_1 + Y q_2, \qquad 9X^2 + Y^2 = 1
```

$X^2$ 的最大值是 $1/9$。较短轴（shorter axis）的端点处有 $X = 1/3$、$Y = 0$。

注意：较大的特征值 $\lambda = 9$ 给出较短的轴，其半长（half-length）为 $1/\sqrt{9} = 1/3$。较小的特征值 $\lambda = 1$ 给出较大的长度 $1/\sqrt{1} = 1$：即图 1.9 中的 $Y$ 轴。

在 $xy$ 坐标系中，轴沿着 $S$ 的特征向量方向。在 $XY$ 坐标系中，轴沿着 $\Lambda$（对角矩阵）的特征向量方向——也就是坐标轴本身。这些全部都来自 $S = Q\Lambda Q^T$。

当所有 $\lambda_i > 0$ 时，$S = Q\Lambda Q^T$ 是正定的。能量 $x^TSx = X^T\Lambda X = \lambda_1 X^2 + \lambda_2 Y^2 = 1$ 的图形是一个椭圆，其轴指向 $S$ 的特征向量方向。



## 注 5 — 椭圆与主轴定理：从 $xy$ 项到几何直觉

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 第 055–056 页 的椭圆 $5x^2 + 8xy + 5y^2 = 1$ 是主轴定理的绝佳可视化：$xy$ 交叉项使椭圆倾斜，但通过 $S = Q\Lambda Q^T$ 做变量替换 $\mathbf{x} = Q\mathbf{X}$，交叉项消失，方程变为 $9X^2 + Y^2 = 1$。本质是：$S$ 的特征向量给出椭圆自然对齐的方向（主轴），特征值的倒数平方根给出半轴长度 $1/\sqrt{\lambda}$。注意一个反直觉的现象：较大的特征值对应较短的轴——$\lambda = 9$ 给出半轴 $1/3$，$\lambda = 1$ 给出半轴 $1$。这是因为方程是 $x^T S x = 1$ 而非 $x^T S^{-1} x = 1$：在主轴方向上，$S$ 的「刚度」越大（$\lambda$ 越大），为保持能量为 1，在该方向的位移必须越小。这可以类比力学：硬弹簧在相同能量下振幅小。
> 第一性原理展开：为什么变量替换 $x = QX$ 能消掉交叉项？把二次型写成 $x^T S x = (QX)^T S (QX) = X^T (Q^T S Q) X$。因为 $S = Q \Lambda Q^T$ 且 $Q$ 正交，$Q^T Q = I$，中间括号恰好是 $\Lambda$。这里没有配方的巧劲，只有矩阵乘法的结合律与 $Q^T Q = I$ 这两个已知工具。交叉项 $8xy$ 来自 $S$ 的非对角元；对角化把非对角元清零，等价于把坐标轴旋转到特征向量方向。这正是「主轴定理」名字的来历：主成分方向加轴长。
> 配方法与对角化的差别值得单独看。配方 $5x^2 + 8xy + 5y^2 = 5(x + \frac{4}{5}y)^2 + \frac{9}{5}y^2$ 同样消去了交叉项，得到平方和，但留下的两个方向不是正交的：新坐标轴一个沿 $(1, 0)$、一个沿 $(-4/5, 1)$，椭圆依然「斜着」看。而特征分解给出的 $9X^2 + Y^2$ 是新坐标轴恰为 $q_1$ 与 $q_2$ 的正交系，椭圆被真正摆正。可见消交叉项只是门槛要求，主轴定理额外要求「用正交变换消」，这正是 $Q^T Q = I$ 的几何含义——不改变长度与夹角，只做旋转。
> 把 $q_1 = (1, 1)/\sqrt{2}$、$q_2 = (1, -1)/\sqrt{2}$ 代入验证：$S q_1 = (9, 9)/\sqrt{2} = 9 q_1$，$S q_2 = (1, -1)/\sqrt{2} = q_2$，所以换到新坐标后 $X$ 方向对应特征值 $9$、$Y$ 方向对应特征值 $1$。这里藏着一个可迁移的观察：任何 $2 \times 2$ 对称矩阵 $\begin{bmatrix} a & b \\ b & a \end{bmatrix}$ 在 $b \neq 0$ 时的特征方向都是 $(1, 1)$ 与 $(1, -1)$，即 $\pm 45^\circ$ 方向；本题 $S = \begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix}$ 正是 $a = 5$、$b = 4$ 的特例，对角元相等决定了主轴不偏不倚，而非对角元 $b = 4$（对应交叉项 $8 = 2b$）决定倾斜程度与特征值的分裂 $a \pm b$。
> 具体例子：沿 $q_1$ 方向，能量为 $\lambda_1 X^2 = 9X^2$；把 $X$ 取成 $1/3$ 时能量恰为 1，这就是短轴端点。反向验证：若把方程错写成 $x^T S^{-1} x = 1$，主轴方向不变，但半轴变成 $\sqrt{\lambda}$，$\lambda = 9$ 会给出长轴 $3$，与上图完全相反。这个对比说明半轴长度的来源是 $1/\sqrt{\lambda}$ 中的倒数，而不是特征值本身。
> 求特征值有一条捷径：形如 $\begin{bmatrix}a&b\\b&a\end{bmatrix}$ 的矩阵，特征值就是 $a+b$ 与 $a-b$——从迹 $2a$ 与行列式 $a^2-b^2$ 两行内读出；本题 $a=5,b=4$ 给出 $9$ 与 $1$。更一般的 $2\times2$ 对称矩阵 $\begin{bmatrix}a&b\\b&c\end{bmatrix}$，主轴旋转角满足 $\tan 2\theta = 2b/(a-c)$：对角元差得越多，主轴越贴近坐标轴；本题 $a=c$ 使分母为零，$\theta=45^\circ$，主轴不偏不倚。
> 从瑞利商的角度看轴长：在单位圆上最大化 $x^T S x$ 得 $\lambda_{\max}=9$、方向 $q_1$，最小化得 $\lambda_{\min}=1$、方向 $q_2$；水平集 $x^T S x=1$ 的轴长与这两个极值互为倒数。这正是拉格朗日乘数法里约束优化与特征值问题共用同一条纽带的实例。
> 跨课程连接：主轴定理与 SVD 的关系值得点破。以后在 18.065 中学到 SVD 时，$A = U \Sigma V^T$ 把单位球映成椭球，主半轴长度是 $\sigma_i$；而这里的水平集 $x^T S x = 1$ 的轴长是 $1/\sqrt{\lambda}$，互为倒数镜像。若你已见过二维正态分布的等概率线，形如 $x^T \Sigma^{-1} x = c$ 的水平集画出的正是协方差椭球，其主轴是协方差矩阵的特征方向、半轴为 $\sqrt{\lambda}$——它用 $\Sigma^{-1}$，与这里的 $x^T S x = 1$ 用 $S$ 相差一个取逆，这正是期望与方差框架下「数据散布方向」与「能量等值面方向」的同一套主轴语言。
> 推广到 $n$ 维：$x^T S x=1$ 是 $\mathbb{R}^n$ 中的椭球，主轴仍是 $S$ 的特征向量，半轴长 $1/\sqrt{\lambda_i}$；若某个 $\lambda_i<0$，水平集变成双曲面，这与注 3 的正定性检验共享同一张几何底图。
> 一句话收束：主轴定理把「倾斜的椭圆」翻译成「对角矩阵」，几何直觉与代数计算在这里合流。
---

---

<!-- page 057: 书页 52, Problem Set 1.7（习题 1-7，保留英文原文） -->
# Strang LaLFD Part I（线性代数与从数据中学习）

> 本页为 **Problem Set 1.7（习题集 1.7）**（1.7 Symmetric Positive Definite Matrices，对称正定矩阵）前半部分（习题 1-7），按习题页规范保留英文原文，仅补结构标签与题号；OCR 乱码已按数学上下文修正。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.** Suppose $S^T = S$ and $Sx = \lambda x$ and $Sy = \alpha y$ are all real. Show that $Sx \cdot y = \lambda x \cdot y$ and $x \cdot Sy = \alpha x \cdot y$. Show that $x \cdot y$ must be zero if $\lambda \neq \alpha$: orthogonal eigenvectors.

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.** Which of $S_1, S_2, S_3, S_4$ has two positive eigenvalues? Use a test, don't compute the $\lambda$'s. Also find an $S_0$ so that $x^T S_0 x < 0$, so $S_0$ is not positive definite.

```math
S_1 = \begin{bmatrix} 10 & 1 \\ 1 & 10 \end{bmatrix}, \qquad
S_2 = \begin{bmatrix} 1 & 10 \\ 10 & 100 \end{bmatrix}
```

> 译者注（OCR 修正）：矩阵碎片残作 `10 / 1 / 10 100`，$S_3, S_4$ 与 $S_0$ 在 OCR 中残缺；题干 "find an $S_0$ so that $x^T S_0 x < 0$" 按上下文补全（原稿残作 "find an SO that < 0"）。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.** For which numbers $b$ and $c$ are these matrices positive definite?

```math
S_1 = \begin{bmatrix} 1 & b \\ b & c \end{bmatrix}, \qquad
S_2 = \begin{bmatrix} 10 & b \\ b & 101 \end{bmatrix}
```

> 译者注（OCR 修正）：矩阵对角元素残作 `1 / 10 / 10 101`，此处按含变量 $b, c$ 的形式重建；本题的解答（两矩阵正定的测试条件）请读者自行推导，此处不再给出（答案略）。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.** With the pivots in $D$ and multiplier in $L$, factor each into $LDL^T$.

> 译者注（OCR 修正）：本题的矩阵未能在 OCR 中辨认出（疑与习题 3 的矩阵相关）。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.** Here is a quick "proof" that the eigenvalues of every real matrix are real:

> False proof: $Ax = \lambda x$ gives $x^T A x = \lambda x^T x$, so $\lambda = \dfrac{x^T A x}{x^T x}$ is real.

Find the flaw in this reasoning—a hidden assumption that is not justified. You could test those steps on the $90^\circ$ rotation matrix

```math
\begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}
```

with $x = \begin{bmatrix} 1 \\ i \end{bmatrix}$ and $\lambda = -i$.

> 译者注（OCR 修正）：句尾 "with $x = [1, i]$ and $\lambda = -i$" 在 OCR 中残缺（残作 "with = and ="），按反例需要补全。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.** Write $S$ and $B$ in the form $\lambda_1 u_1 u_1^T + \lambda_2 u_2 u_2^T$ of the spectral theorem $Q\Lambda Q^T$:

```math
S = \begin{bmatrix} 9 & 12 \\ 12 & 16 \end{bmatrix}
```

> 译者注（OCR 修正）：矩阵碎片残作 `9 12 / ()e ep 1 丨 / 12 16`，矩阵 $B$ 未能辨认，此处仅给出 $S$。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 7 (Recommended).** This matrix $M$ is antisymmetric and also orthogonal. Then all its eigenvalues are pure imaginary and they also have $|\lambda| = 1$. ($\|Mc\| = \|c\|$ for every $c$, so $|\lambda|\,\|c\| = \|c\|$ for eigenvectors.) Find all four eigenvalues from the trace of $M$:

```math
M = \frac{1}{\sqrt{3}}\begin{bmatrix} 0 & 1 & 1 & 1 \\ -1 & 0 & 1 & -1 \\ -1 & -1 & 0 & 1 \\ -1 & 1 & -1 & 0 \end{bmatrix}
```

An antisymmetric matrix can only have eigenvalues $0$ or pure imaginary. Show that $S$ (symmetric but complex) has only one line of eigenvectors:

```math
S = \begin{bmatrix} 1 & i \\ i & -1 \end{bmatrix}
```

It is not even diagonalizable: eigenvalues = $0$ and $0$. $A^T = A$ is not such a special property for complex matrices. The good property is $A^H = A$ (conjugate transpose): then all eigenvalues are real and it has orthogonal eigenvectors.

> 译者注（OCR 修正）：$M$ 的负号与归一化因子 $1/\sqrt{3}$ 在 OCR 中丢失（矩阵碎片残作一串 `1`），此处按"反对称且正交、$|\lambda| = 1$、迹 $= 0$"重建；具体特征值请读者自行计算（答案略）。复对称矩阵 $S$ 中的 $i$ 残作 `1/2`。本页末尾的复矩阵部分在原文中也可能构成独立习题（题号随次页延续）。

---

<!-- page 058: 书页 53, Problem Set 1.7 续（习题 8-14，保留英文原文） -->

> 本页为 **Problem Set 1.7（习题集 1.7）** 的延续（习题 8-14），按习题页规范保留英文原文，仅补结构标签与题号；OCR 乱码已按数学上下文修正。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.** This matrix is nearly symmetric. But its eigenvectors are far from orthogonal:

```math
S = \begin{bmatrix} 10 & -15 \\ 1 & 0 \end{bmatrix}
```

has eigenvectors $\begin{bmatrix} 1 \\ ? \end{bmatrix}$ and $\begin{bmatrix} -15 \\ ? \end{bmatrix}$. What is the angle between the eigenvectors?

> 译者注（OCR 修正）：矩阵按碎片 `10 -15 / 1` 重建为 $\begin{bmatrix} 10 & -15 \\ 1 & 0 \end{bmatrix}$；特征值、特征向量与两特征向量的夹角请读者自行计算（答案略）。原稿中特征向量的具体书写在 OCR 中残缺，未完整还原。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.** If $S$ is symmetric and also orthogonal, then $S^T = S$ and $S^T S = I$.

(a) Show how symmetry and orthogonality lead to $S^2 = I$.

(b) What are the possible eigenvalues of $S$? Describe all possible $\Lambda$.

Then $S = Q\Lambda Q^T$ for one of those eigenvalue matrices $\Lambda$ and an orthogonal $Q$.

> 译者注（OCR 修正）：题干首句在 OCR 中残缺（残作 "symmetric 口 c S are og ? Then ST = S and S"），按 (a)(b) 内容重建为对称且正交的情形。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.** If $S$ is symmetric, show that $A^T S A$ is also symmetric (take the transpose). Here $A$ is $n$ by $m$ and $S$ is $m$ by $m$. Are eigenvalues of $S$ = eigenvalues of $A^T S A$? In case $A$ is square and invertible, $A^T S A$ is called congruent to $S$. They have the same number of positive, negative, and zero eigenvalues: Law of Inertia.

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 11.** Here is a way to show that $a$ is between the eigenvalues $\lambda_1$ and $\lambda_2$ of $S$:

```math
\det(S - \lambda I) = (a - \lambda)(c - \lambda) - b^2
```

is a parabola opening upwards (because of $\lambda^2$). Show that $\det(S - \lambda I)$ is negative at $\lambda = a$. So the parabola crosses the axis left and right of $\lambda = a$; it crosses at the two eigenvalues of $S$, so they must enclose $a$.

The eigenvalues of $S^{-1}$ always lie between the eigenvalues of $S$. Section III.2 will explain this interlacing of eigenvalues.

> 译者注（OCR 修正）：末句残作 "The 一1 eigenvalues of alway s1 between the eigenvalues of S =" 与 "Section 111.2"，此处按 interlacing（特征值交错性质）主题补全，并将 "Section 111.2" 修正为 "Section III.2"。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 12.** The energy $x^2 - y^2$ certainly has a saddle point at $(0, 0)$. What symmetric matrix $S$ produces this energy? What are its eigenvalues?

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 13.** Test to see if $S = A^T A$ is positive definite in each case: $A^T A$ needs independent columns.

```math
A_1 = \begin{bmatrix} 1 & 1 & 2 \\ 1 & 2 & 1 \end{bmatrix}, \qquad
A_2 = \begin{bmatrix} 1 & 2 \\ 2 & 1 \end{bmatrix}
```

> 译者注（OCR 修正）：矩阵碎片残作 `1 1 2 / and = / and = 1 2 / 1 2 1`，此处按两个矩阵重建：$A_1$ 为 $2 \times 3$（列不独立），$A_2$ 为 $2 \times 2$。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 14.** Find the 3 by 3 matrix $S$ and its pivots, rank, eigenvalues, and determinant:

```math
S = 4x_1^2 + 2x_2^2 + x_3^2 + 2x_1x_2
```

> 译者注（OCR 修正）：能量表达式残作 `= 401 一 + 2）` 与 `1 2 3`，此处按二次型形式重建（系数以残存的 4、2、1、2 为准）。

---

<!-- page 059: 书页 54, Problem Set 1.7 续（习题 15-23，保留英文原文） -->

> 本页为 Problem Set 1.7 的延续（习题 15-23），按习题页规范保留英文原文，仅补结构标签与题号；OCR 乱码已按数学上下文修正。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 15.** Compute the three upper left determinants of $S$ to establish positive definiteness. Verify that their ratios give the second and third pivots.

*(Pivot = ratio of determinants)*

```math
S = \begin{bmatrix} 2 & 2 & 0 \\ 2 & 5 & 3 \\ 0 & 3 & 8 \end{bmatrix}
```

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 16.** For what numbers $c$ and $d$ are $S$ and $A$ positive definite? Test their 3 determinants:

```math
S = \begin{bmatrix} c & 1 & 1 \\ 1 & c & 1 \\ 1 & 1 & c \end{bmatrix}
\qquad\text{and}\qquad
A = \begin{bmatrix} 1 & 2 & 3 \\ 2 & d & 4 \\ 3 & 4 & 5 \end{bmatrix}
```

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 17.** Find a matrix with $a > 0$ and $c > 0$ and $a + c > 2b$ that has a negative eigenvalue. A positive definite matrix cannot have a zero (or even worse, a negative number) on its main diagonal. Show that this matrix fails to have $c^T S c > 0$:

```math
S = \begin{bmatrix} 4 & 1 & 1 & 1 \\ 1 & 0 & 2 & 2 \\ 1 & 2 & 3 & 5 \\ 1 & 2 & 5 & 3 \end{bmatrix}
```

$c^T S c$ is not positive when $c = (1, -1, 1, -1)$.

> 译者注（OCR 修正）：矩阵第三行末元素按对称性补为 $5$；检验向量原稿残作 $(1, 2, 3)$，此处取使 $c^T S c = -2 < 0$ 的 $c = (1, -1, 1, -1)$。

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 18.** A diagonal entry $s_{jj}$ of a symmetric matrix cannot be smaller than all the $\lambda$'s. If it were, then $S - s_{jj}I$ would have positive eigenvalues and would be positive definite. But $S - s_{jj}I$ has a zero on the main diagonal, impossible by Problem 17.

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 19.** From $S = Q\Lambda Q^T$ compute the positive definite symmetric square root $Q\sqrt{\Lambda}\,Q^T$ of each matrix. Check that this square root gives $A^T A = S$.

```math
S = \begin{bmatrix} 10 & 6 \\ 6 & 10 \end{bmatrix}
```

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 20.**

```math
S = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}
```

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 21.** Draw the tilted ellipse $x^2 + xy + y^2 = 1$ and find the half-lengths of its axes from the eigenvalues of the corresponding matrix $S$.

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 22.** In the Cholesky factorization $S = A^T A$, with $A = \sqrt{D}\,L^T$, the square roots of the pivots are on the diagonal of $A$. Find (upper triangular) $A$ for

```math
S = \begin{bmatrix} 9 & 0 & 0 \\ 0 & 1 & 2 \\ 0 & 2 & 8 \end{bmatrix}
\qquad\text{and}\qquad
S = \begin{bmatrix} 1 & 1 & 1 \\ 1 & 2 & 2 \\ 1 & 2 & 7 \end{bmatrix}
```

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 23.** Suppose $C$ is positive definite (so $y^T C y > 0$ whenever $y \ne 0$) and $A$ has independent columns (so $Ax \ne 0$ whenever $x \ne 0$). Apply the energy test to $A^T C A$ to show that $S = A^T C A$ has the crucial energy property.

---

<!-- page 060: 书页 55, §I.7 结尾 The Minimum of Function F(c1,c2)（正文，完整翻译）+ Problem Set 1.7 续（习题 24-28，保留英文） -->

### The Minimum of Function $F(c_1, c_2)$（函数 $F(c_1, c_2)$ 的最小值）

<span style="color:#2471a3;">**[section]**</span> 在最小值点（minimum point）处，一阶导数（first derivatives）$F_{c_1}$ 与 $F_{c_2}$ 均为零。

接下来就是通常的微积分检验（calculus test）$f'' > 0$ 的线性代数（linear algebra）版本。

二阶导数矩阵（second derivative matrix）$H$ 为：

```math
H = \begin{bmatrix} \dfrac{\partial^2 F}{\partial c_1^2} & \dfrac{\partial^2 F}{\partial c_1 \partial c_2} \\[2pt] \dfrac{\partial^2 F}{\partial c_2 \partial c_1} & \dfrac{\partial^2 F}{\partial c_2^2} \end{bmatrix}
```

其中 $F_{c_1 c_2} = \partial^2 F/\partial c_1 \partial c_2$ 是一个"混合"（mixed）二阶导数（second derivative）。

最小值的检验（test for minimum）：$H$ 是正定的（positive definite）。

---

### Problem Set 1.7（续，习题 24-28，保留英文原文）

<span style="color:#2471a3;">**[problem]**</span> **Problem 24.** For $F = x^2 + 2xy + 2y^2$ and $G = x^2 + 2xy - y^2$, find the second derivative matrices $H_1$ and $H_2$ (the Hessian matrices):

```math
H = \begin{bmatrix} \partial^2 F/\partial x^2 & \partial^2 F/\partial x \partial y \\ \partial^2 F/\partial y \partial x & \partial^2 F/\partial y^2 \end{bmatrix}
```

Test for minimum: $H$ is positive definite. $H_1$ is positive definite so $F_1$ is concave up (= convex). Find the minimum point of $F_1$. Find the saddle point of $F_2$ (look only where first derivatives are zero).

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 25.** Which values of $c$ give a bowl and which $c$ give a saddle point for the graph of $z = 4x^2 + 12xy + cy^2$? Describe this graph at the borderline value of $c$.

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 26.** Without multiplying

```math
S = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 5 \end{bmatrix}
```

find

(a) the determinant of $S$

(b) the eigenvalues of $S$

(c) the eigenvectors of $S$

(d) a reason why $S$ is symmetric positive definite

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 27.** For which $a$ and $c$ is this matrix positive definite? For which $a$ and $c$ is it positive semidefinite (this includes definite)?

```math
S = \begin{bmatrix} a & a & a \\ a & a + c & a - c \\ a & a - c & a + c \end{bmatrix}
```

All 5 tests are possible. The energy equals ...

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 28.** Important! Suppose $S$ is positive definite with eigenvalues $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_n \ge 0$.

(a) What are the eigenvalues of the matrix $\lambda_1 I - S$? Is it positive semidefinite?

(b) How does it follow that $\lambda_1 c^T c \ge c^T S c$ for every $c$?

(c) Draw this conclusion: The maximum value of $c^T S c / c^T c$ is $\lambda_1$.

Another way to 28(c): Maximize $c^T S c$ subject to the condition $c^T c = 1$. This leads to $S c = \lambda c$.

---

<!-- page 061: 书页 56, §I.8 The Singular Value Decomposition（奇异值分解）—— 为什么需要 SVD、data matrix、AV=UΣ -->

# Strang LaLFD Part I（线性代数与从数据中学习）

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">Highlights of Linear Algebra（线性代数要点）</span>

<span style="color:#2471a3;">**[section]**</span> **1.8 Singular Values and Singular Vectors in the SVD（SVD 中的奇异值与奇异向量）**

最好的矩阵——real symmetric matrices（实对称矩阵）$S$——拥有 real eigenvalues（实特征值）和 orthogonal eigenvectors（正交特征向量）。
但对于其他矩阵，eigenvalues（特征值）可能是复的，或者 eigenvectors（特征向量）并不 orthogonal（正交）。
如果 $A$ 不是 square（方阵），那么 $Ax = \lambda x$ 就不可能成立，eigenvectors（特征向量）随之失效——等号左侧在 $\mathbb{R}^m$ 中，右侧却在 $\mathbb{R}^n$ 中。
我们需要一个对每个矩阵都能奏效的 idea（思想）。

奇异值分解（The Singular Value Decomposition, SVD）以一种完美的方式填补了这个空缺。
在我们的应用中，$A$ 往往是一个 data matrix（数据矩阵）。
这些 rows（行）可以告诉我们 1000 个儿童的 age（年龄）与 height（身高）。
于是 $A$ 就是 $2 \times 1000$ 的：它毫无疑问是 rectangular（长方形）的矩阵。
除非 height（身高）恰好与 age（年龄）成正比，否则 rank（秩）为 $r = 2$，而那个矩阵有两个正的 singular values（奇异值）$\sigma_1$ 与 $\sigma_2$。

关键的一点在于，我们需要两组 singular vectors（奇异向量）——u's 与 v's。

对于一个实的 $m \times n$ 矩阵，right singular vectors（右奇异向量）$v_1, \dots, v_n$ 在 $\mathbb{R}^n$ 中相互 orthogonal（正交）。
而那 $m$ 个 left singular vectors（左奇异向量）$u_1, \dots, u_m$ 在 $\mathbb{R}^m$ 中两两 perpendicular（垂直）。

在 $A, u, v$ 与 $\sigma$ 之间，联系并不是 $Av = \lambda v$——那是 eigenvectors（特征向量）的情形。
对于 singular vectors（奇异向量），每个 $Av$ 都等于 $u\sigma$：

```math
Av_i = \sigma_i u_i \quad (i = 1, \dots, n) \tag{1}
```

我已经把前 $r$ 个 v's 与 u's 从其余部分中分离出来。
这个数 $r$ 就是 rank（秩），即 independent columns（独立列）的个数（也是 independent rows（独立行）的个数）。
于是 $r$ 就是 column space（列空间）与 row space（行空间）的 dimension（维数）。
我们会有 $r$ 个降序排列的正 singular values（奇异值）：$\sigma_1 \ge \sigma_2 \ge \cdots \ge \sigma_r > 0$。
最后 $n - r$ 个 v's 位于 $A$ 的 nullspace（零空间）中，最后 $m - r$ 个 u's 位于 $A^T$ 的 nullspace（零空间）中。

我们的第一步，是把方程 (1) 写成 matrix form（矩阵形式）。
全部 right singular vectors（右奇异向量）$v_1$ 到 $v_n$ 作为 columns（列）进入 $V$。
左奇异向量（left singular vectors）$u_1$ 到 $u_m$ 作为 columns（列）进入 $U$。
它们是 square orthogonal matrices（方阵正交矩阵），满足 $V^T = V^{-1}$ 与 $U^T = U^{-1}$，因为它们的列都是 orthogonal unit vectors（正交单位向量）。
于是方程 (1) 就变成完整的 SVD（奇异值分解），其中 $V$ 与 $U$ 都是方阵：

```math
AV = U\Sigma \tag{2}
```

你可以看到，$\Sigma$ 的非零部分集中在前 $r$ 列。
这就是 SVD（奇异值分解）的重要部分。
它展示了为 $A$ 的 row space（行空间）准备的一组 v's 基（basis），接着是为 column space（列空间）准备的一组 u's 基。

在 $\Sigma$ 主对角线上的正数 $\sigma_1, \dots, \sigma_r$ 之后，这条对角线的其余部分全是零——它们来自 $A$ 与 $A^T$ 的 nullspaces（零空间）。

特征向量给出 $AX = X\Lambda$。
但 $AV = U\Sigma$ 需要两组 singular vectors（奇异向量）。



## 注 6 — SVD 为什么需要两组基：列空间与行空间的分离

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 第 061 页开篇是整本教材最重要的「为什么」之一。实对称矩阵的特征分解之所以优雅，是因为 $S$ 的列空间和行空间是同一个空间（对称性使然），所以一组正交基 $Q$ 足以同时对角化。但对于一般的 $m \times n$ 矩形矩阵 $A$，输入空间是 $\mathbb{R}^n$，输出空间是 $\mathbb{R}^m$——这是两个不同的向量空间。$Av = \lambda v$ 对于非方阵根本没有意义：左侧 $Av \in \mathbb{R}^m$，右侧 $\lambda v \in \mathbb{R}^n$，维度不匹配。SVD 用 $Av_i = \sigma_i u_i$ 解决了这个问题：$v_i$ 活在输入空间 $\mathbb{R}^n$（右奇异向量，构成行空间的正交基），$u_i$ 活在输出空间 $\mathbb{R}^m$（左奇异向量，构成列空间的正交基），$\sigma_i$ 作为标量桥梁连接两个空间。这正是线性映射的本质：$A: \mathbb{R}^n \to \mathbb{R}^m$ 在两个不同的空间操作，自然需要两组坐标基。建议将此处的 $V$（$n \times n$）和 $U$（$m \times m$）分别与四个基本子空间做映射：$V$ 的前 $r$ 列张成行空间，后 $n-r$ 列张成零空间；$U$ 的前 $r$ 列张成列空间，后 $m-r$ 列张成左零空间。
> 从第一性原理重新推导一遍，就能看清两组基为什么不可避免。给定线性映射 $A: \mathbb{R}^n \to \mathbb{R}^m$，我们的目标是把 $A$ 表示成「最干净」的形式——即每个基向量只被拉伸一个倍数，不旋转到别的方向。在同一个空间里做这件事（方阵情形），只选一组基即可；但在两个不同空间里，输入端和输出端各需要一组坐标轴，因为输入端某个方向在输出端长什么样，必须用输出端的坐标系来描述。$Av_i = \sigma_i u_i$ 正是这种「输入坐标 $v_i$ 加输出坐标 $u_i$ 加标量拉伸 $\sigma_i$」的逐方向记账。四个基本子空间恰好由这两组基自然切开：行空间是 $A$ 真正能「看到」的输入维度，零空间是被 $A$ 压成零向量的输入冗余；列空间是 $A$ 真正能达到的输出维度，左零空间是输出端够不着的维度。SVD 的 $V$ 和 $U$ 分别把输入端和输出端的这四个子空间一次性配齐。
> 一个具体例子能把维度错配看得更清楚。取 $A = \begin{bmatrix} 3 & 0 & 0 \\ 0 & 2 & 0 \end{bmatrix}$，它把 $\mathbb{R}^3$ 映到 $\mathbb{R}^2$。三个输入标准基向量 $e_1, e_2, e_3$ 分别被映成 $3u_1$、$2u_2$ 和零向量：前两个方向各得到一个正奇异值 $\sigma_1 = 3$、$\sigma_2 = 2$，第三个方向落进零空间，$\sigma_3 = 0$。这里的细节正是「两组基」的要义：输入端有 3 个坐标，但输出端只有 2 个方向可以承接拉伸后的像，多出来的那一维只能被消灭。反过来想，若硬套 $Av = \lambda v$，方程左侧是 2 维向量、右侧是 3 维向量，就像把「2 元返回值」和「3 元参数列表」放在等号两边比较，类型系统直接拒绝——这不是数值问题，而是结构性不允许。$e_3$ 被压成零这件事，在特征值语言里勉强对应 $\lambda = 0$，但矩形矩阵根本写不出这个方程，SVD 用 $\sigma_3 = 0$ 把它接住了。
> 跨课程连接：这个「函数签名」的视角可以用 6.042J 中函数类型 $A \to B$ 的记法来锚定：定义域与值域是两个独立的集合，各有各的坐标描述，输入用什么坐标、输出用什么坐标不必也不应混为一谈。CSAPP 的视角则更具体：一个函数把 $n$ 个参数映射为 $m$ 个返回值，参数列表与返回值列表本来就是两套不同的存储布局；SVD 的两组基正是为这两套布局各准备了一套规范的正交坐标系。以后在最小二乘问题 $Ax \approx b$ 中还会再次遇见这种分离——残差 $b - Ax$ 落在左零空间方向，而解 $x$ 的行空间分量才是唯一有确定意义的部分。
> 一句话收束：特征分解是「一个空间里的一件工具」，SVD 是「两个空间之间的一座桥」，桥的两端各需要一套独立的坐标系。
---

---

<!-- page 062: 书页 57, §I.8 SVD（续）—— Example 1、A=UΣV^T、Pieces of the SVD、Reduced Form -->

# Strang LaLFD Part I（线性代数与从数据中学习）

<span style="color:#2471a3;">**[example]**</span> **Example 1（例 1）**

本例子展示 $AV = U\Sigma$，其中的矩阵 $A$ 为：

```math
A = \begin{bmatrix}3 & 0\\ 4 & 5\end{bmatrix}
```

矩阵 $A$ 不是 symmetric（对称的），所以 $V$ 与 $U$ 不同。
矩阵的 rank（秩）为 2，所以有两个 singular values（奇异值）：$\sigma_1 = 3\sqrt{5}$ 与 $\sigma_2 = \sqrt{5}$。
它们的乘积 $3\sqrt{5} \cdot \sqrt{5} = 15$ 正是 $A$ 的 determinant（行列式）（在这方面，singular values（奇异值）很像 eigenvalues（特征值））。
矩阵 $V$ 的列相互 orthogonal（正交），矩阵 $U$ 的列也相互 orthogonal（正交）。
在除以 $\sigma_1$ 和 $\sigma_2$ 之后，这些列都成为 unit vectors（单位向量），于是 $V$ 与 $U$ 都是 orthogonal matrices（正交矩阵）：$V^T = V^{-1}$ 且 $U^T = U^{-1}$。

正是这种 orthogonality（正交性）让我们能够从 $AV = U\Sigma$ 走到 SVD（奇异值分解）那个常见而著名的表达式。
把 $AV = U\Sigma$ 两边同乘以 $V^{-1} = V^T$：

```math
A = U\Sigma V^T \tag{3}
```

这就是 $A$ 的 Singular Value Decomposition（奇异值分解）。

于是 $U\Sigma$ 与 $V^T$ 的 column-row multiplication（列乘行乘法）把乘积分解成 $r$ 个 rank-one pieces（秩一分量）：

<span style="color:#2471a3;">**[note]**</span> **SVD 的分量（Pieces of the SVD）**

```math
A = \sigma_1 u_1 v_1^T + \cdots + \sigma_r u_r v_r^T \tag{4}
```

在这个 $2 \times 2$ 的例子中，第一个 piece（分量）比第二个 piece（分量）更重要，因为 $\sigma_1 = 3\sqrt{5}$ 大于 $\sigma_2 = \sqrt{5}$。
把这两个 piece（分量）$\sigma_1 u_1 v_1^T + \sigma_2 u_2 v_2^T$ 相加，我们就能恢复出 $A$：

```math
A = \frac{3}{2}\begin{bmatrix}1 & 1\\ 3 & 3\end{bmatrix}
  + \frac{1}{2}\begin{bmatrix}3 & -3\\ -1 & 1\end{bmatrix}
  = \begin{bmatrix}3 & 0\\ 4 & 5\end{bmatrix}
```

这一步之所以能简化，是因为 $\dfrac{\sqrt{5}}{\sqrt{20}}$ 等于 $\dfrac{1}{2}$。
注意，$V$ 中的 right singular vectors（右奇异向量）$(1,1)$ 与 $(1,-1)$ 被转置成了 $V^T$ 的行 $v_1^T, v_2^T$。
我们还没有解释 $V$、$U$ 与 $\Sigma$ 究竟是怎样算出来的！

> <span style="color:#1e8449;">**译者注：** 本页的 Example 1 只给出分解框架与奇异值 $\sigma_1 = 3\sqrt{5}$、$\sigma_2 = \sqrt{5}$；$U$、$\Sigma$、$V$ 的具体计算要到书页 60 的 "Example 1 (completed)" 才完成（即 §I.8 后续页面的内容）。</span>

---

### <span style="color:#2471a3;">**[section]**</span> The Reduced Form of the SVD（SVD 的简化形式）

方程 (2) 中的完整形式 $AV = U\Sigma$ 在 $A$ 的 rank（秩）很小、nullspace（零空间）很大时，$\Sigma$ 中会有大量的零。
这些零对 matrix multiplication（矩阵乘法）毫无贡献。
奇异值分解（SVD）的核心就在前 $r$ 个 v's、u's 与 $\sigma$'s 之中。
我们可以通过去掉那些注定产生零的部分，把 $AV = U\Sigma$ 缩减为 $A = U_r \Sigma_r V_r^T$。
这样就得到 reduced SVD（简化奇异值分解），其中 $\Sigma_r$ 现在是方阵：

```math
A = U_r \Sigma_r V_r^T \tag{5}
```

> <span style="color:#7f8c8d;">图中的标注：$U_r$ 一侧对应 column space（列空间），$V_r^T$ 一侧对应 row space（行空间）。</span>
> <span style="color:#7f8c8d;">Strang §I.8, p.57</span>

---

# Strang LaLFD Part I（线性代数与从数据中学习）

<!-- page 063: 书页 58, §1.8 奇异值与奇异向量（SVD 续） -->

### <span style="color:#c0392b;">Highlights of Linear Algebra（线性代数要点）</span>

我们仍然有 $V^T V = I$ 和 $U^T U = I$，它们来自那些正交单位向量（orthogonal unit vectors）$v$ 与 $u$。但当 $U$ 和 $V$ 不是方阵（square）时，我们就无法得到双侧逆（two-sided inverses）：$V^T V = I$，但 $V V^T \neq I$；同样 $U^T U = I$，但 $U U^T \neq I$。

<span style="color:#2471a3;">**[example]**</span> **Example（例）：** 对矩阵 $A = \begin{bmatrix} 1 & 2 \\ 2 & 4 \\ 2 & 4 \end{bmatrix}$（这是一个 $3 \times 2$、秩为 1（rank 1）的矩阵），有 $V^T V = [1]$，但 $V V^T \neq I$。

习题（Problem）21 表明我们仍然有 $A = U_r \Sigma_r V_r^T$（约化 SVD）。$U \Sigma V^T$ 的其余部分对 $A$ 没有任何贡献，因为 $\Sigma$ 中有那些零块（blocks of zeros）。关键公式（key formula）仍然是

```math
A = \sigma_1 u_1 v_1^T + \cdots + \sigma_r u_r v_r^T
```

这个 SVD 只看到对角矩阵（diagonal matrix）$\Sigma$ 中的 $r$ 个非零元。

---

### <span style="color:#c0392b;">The Important Fact for Data Science（数据科学的关键事实）</span>

为什么 SVD 对这个主题和这本书如此重要？与其他分解（factorizations）$A = LU$、$A = QR$ 和 $S = Q\Lambda Q^T$ 一样，它把矩阵分解为秩一分量（rank one pieces）。SVD 的一个特殊性质是：这些分量按重要性顺序（in order of importance）排列。第一项 $\sigma_1 u_1 v_1^T$ 是离 $A$ 最近的秩一矩阵。而且事实还不止于此：前 $k$ 项之和 $\sigma_1 u_1 v_1^T + \cdots + \sigma_k u_k v_k^T$ 是 $A$ 的最佳秩 $k$ 近似（best rank $k$ approximation）：

```math
A_k = \sigma_1 u_1 v_1^T + \cdots + \sigma_k u_k v_k^T \qquad \text{Eckart-Young} \qquad (6)
```

要理解这句话，你需要知道符号 $\|A - B\|$ 的含义：这就是矩阵 $A - B$ 的范数（norm），一个衡量其大小的度量（就像数的绝对值（absolute value）一样）。Eckart-Young 定理将在 Section 1.9（第 1.9 节）中证明。

> <span style="color:#1e8449;">*译者注：*这里 $\|A - B\|$ 可取谱范数（spectral norm）或弗罗贝尼乌斯范数（Frobenius norm），Eckart-Young 定理说的是：截断 SVD 得到的 $A_k$ 在两种范数下都是最优的秩 $k$ 近似，这正是 PCA 的理论基础。</span>

---

### <span style="color:#c0392b;">First Proof of the SVD（SVD 的第一个证明）</span>

我们的首要任务是找出方程 (1) 中的 $v$ 与 $u$，从而得到 SVD。我们的目标是 $A = U\Sigma V^T$：要确定两组奇异向量（singular vectors），即 $v$ 组与 $u$ 组。找出这些向量的一个方法，是利用对称矩阵（symmetric matrices）$A^T A$ 与 $A A^T$：

```math
A^T A = (V\Sigma^T U^T)(U\Sigma V^T) = V\Sigma^T \Sigma V^T \tag{7}
```

```math
A A^T = (U\Sigma V^T)(V\Sigma^T U^T) = U\Sigma \Sigma^T U^T \tag{8}
```

(7) 与 (8) 两个式子都产生了对称矩阵。通常 $A^T A$ 与 $A A^T$ 是不同的。两式右端都具有特殊形式 $Q\Lambda Q^T$：特征值（eigenvalues）在 $\Lambda = \Sigma^T \Sigma$ 或 $\Lambda = \Sigma \Sigma^T$ 中，特征向量（eigenvectors）在 $Q = V$ 或 $Q = U$ 中。于是从 (7) 和 (8) 我们知道了 $V$、$U$ 与 $\Sigma$ 是如何与对称矩阵 $A^T A$ 和 $A A^T$ 联系起来的。
> <span style="color:#7f8c8d;">Strang §I.8, p.58</span>



## 注 7 — $A^T A$ 与 $AA^T$ 的对称性：SVD 证明的心脏

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：主文本要分解的 $A$ 一般不对称、甚至不是方阵，而手头成熟的谱定理只对对称矩阵生效。设计问题因而是：如何把 $A$ 的信息无损搬进一个对称矩阵？答案是把 $A$ 与 $A^T$ 相乘，得到 $A^T A$（$n \times n$）与 $AA^T$（$m \times m$）。对称性可直接验证：$(A^T A)^T = A^T A$；更关键的是它们自动半正定——对任意 $x$，$x^T A^T A x = (Ax)^T(Ax) = \|Ax\|^2 \ge 0$，即长度平方非负。于是谱定理保证 $A^T A$ 拥有完整的标准正交特征向量组，这正是 $V$ 的来源；$AA^T$ 同理给出 $U$。半正定性还自动保证所有特征值非负，开方得到 $\sigma_i$ 才有意义。
> 第一性原理：这个策略可命名为**对称化归约法（Symmetrization Reduction）**——非对称问题先对称化，用已知工具解决，再映射回原问题。映射回去不丢信息的根据是：若 $A^T A v = \lambda v$ 且 $\lambda \ne 0$，则 $u = Av/\sqrt{\lambda}$ 满足 $AA^T u = \lambda u$；反过来同理。这把两个矩阵的非零特征向量一一配对，非零特征值 $\sigma_i^2$ 因此完全相同。这是 6.042J 里「构造双射证明两集合等大」的思想，只是用在谱上而非元素个数上。二者只差在零特征值：$A^T A$ 有 $n-r$ 个零，$AA^T$ 有 $m-r$ 个零，其中 $r$ 是 $A$ 的秩，多出的零来自输入与输出空间的维数差。另一个信息保真的事实：$A^T A x = 0$ 推出 $\|Ax\|^2 = x^T A^T A x = 0$，进而 $Ax = 0$，所以 $A^T A$ 与 $A$ 的零空间相同——平方没有把任何非零向量压成零，只是把缩放因子平方了。这正是「借力」的代价与收益：奇异值变成 $\sigma_i^2$，开方后丢失符号，所以主文本必须再用方程 (9) 逐对恢复 $u_k$ 与 $v_k$ 的符号；若某个 $\sigma^2$ 是二重特征值，还要在特征平面里用 $Av = \sigma u$ 选出一致的方向。
> 思想实验：取 $3 \times 2$ 矩阵 $A = \begin{bmatrix}1&0\\0&2\\0&0\end{bmatrix}$。手算得 $A^T A = \begin{bmatrix}1&0\\0&4\end{bmatrix}$，$AA^T = \begin{bmatrix}1&0&0\\0&4&0\\0&0&0\end{bmatrix}$。两者共享非零特征值 $1$ 与 $4$（即 $\sigma_1^2 = 4$、$\sigma_2^2 = 1$），而 $3 \times 3$ 的 $AA^T$ 多出一个零特征值：输出空间多了一维，而 $A$ 的像只有二维。这个具体例子里，「共同非零谱」与「多余的零来自维数差」同时落地。再从 $A^T A$ 出发按方程 (9) 恢复：$v_1 = e_2$ 给出 $u_1 = A e_2/2 = e_2'$，$v_2 = e_1$ 给出 $u_2 = A e_1/1 = e_1'$，其中 $e_1', e_2'$ 是输出空间的前两个坐标向量，$A$ 的 SVD 由此拼出，符号没有任何歧义。工程上还有一个自由选择：当 $m \gg n$ 时，$A^T A$ 只有 $n \times n$，在 $A^T A$ 上做特征分解通常比在 $m \times m$ 的 $AA^T$ 上做更省——优先选择尺寸小的那个对称化对象。
> 一个可核验的视角：$A^T A$ 的 $(i,j)$ 元恰好是 $A$ 的第 $i$ 列与第 $j$ 列的内积。若记 $A$ 的列为 $a_1, \ldots, a_n$，则 $A^T A = [a_i^T a_j]$。于是「$A^T A$ 可对角化」翻译成几何语言就是：存在一组标准正交向量 $v_1, \ldots, v_n$，使列向量重新组合后两两正交。当列与列之间出现近似线性依赖时，$A^T A$ 就接近奇异，特征值出现近零项——这与你熟悉的 CSAPP 浮点视角相接：$A^T A$ 的条件数约等于 $A$ 的条件数平方，把 $A$ 的信息压进内积表的同时也把数值敏感性放大了。这个观察解释了为什么数值上人们常常不显式构造 $A^T A$ 而是直接对 $A$ 做二对角化——但那是 §II.1 的数值话题。回到对称化归约本身：内积表保留了列之间的全部长度与夹角信息，唯一丢掉的是「每一列在输入基下的绝对朝向」，而这部分信息恰好由 $V$ 恢复。
> 再把「共同非零特征值」的事实拆成一次双射：$v \mapsto Av/\sigma$ 把 $A^T A$ 的每个非零特征方向送到 $AA^T$ 的对应方向，逆映射由 $u \mapsto A^T u/\sigma$ 给出，二者复合后回到原向量。这个双向对应不依赖任何坐标选取，正是 6.042J 双射法的线性版本。
> 跨课程连接：方程 (9) 的正交性验证 $u_j^T u_k = v_j^T A^T A v_k/(\sigma_j \sigma_k)$ 的核心只是结合律 $(AB)C = A(BC)$——先算 $A^T A$ 再与 $v_k$ 相乘，和先算 $A v_k$ 再做内积，结果相同。这与 CSAPP §3.7 过程调用中栈帧嵌套是同一逻辑结构：括号只标记计算顺序，不改变合成后的语义；调用栈的进出与矩阵乘法的结合顺序一样可以重排。$A^T A$ 的构造还预演了随后 K-L 变换里的协方差矩阵 $X^T X$：同一个「左乘转置再对角化」的动作，在这里制造奇异值，在统计里制造主成分。一句话收束：左乘 $A^T$ 就是把「$A$ 作用在向量上」的信息折叠成「作用在自身上的二次型」，谱定理由此获得入口。
---



## 注 8 — Eckart-Young：为什么截断 SVD 是最佳低秩近似

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：Eckart-Young 回答的是一个带约束的优化问题：在所有秩不超过 $k$ 的矩阵 $B$ 中，谁离 $A$ 最近？度量是 Frobenius 范数 $\|A-B\|_F$，即把 $m \times n$ 矩阵当作 $mn$ 维向量求欧氏长度。设计上的难点是秩约束：$B$ 的列只能张成不超过 $k$ 维的子空间，问题因此等价于「用 $k$ 个方向最多能保留 $A$ 的多少能量」。所谓能量是严格可算的：$\|A\|_F^2 = \sum_i \sum_j a_{ij}^2 = \operatorname{tr}(A^T A)$，而且等于奇异值平方和 $\sum_i \sigma_i^2$。这个恒等式把「矩阵的整体大小」与「每个方向上的放大倍率」接了起来，是 SVD 能作为压缩工具的第一块基石。
> 第一性原理：证明模板可命名为**对角化后排序（Diagonalize-then-Sort）**。第一步用 Frobenius 范数的正交不变性：当 $Q, Z$ 为正交矩阵时 $\|QAZ\|_F = \|A\|_F$，因为 $\|A\|_F^2$ 是各列长度平方和，而正交变换保持每列长度。取 $Q = U^T$、$Z = V$，问题就化成最干净的形式：找秩不超过 $k$ 的矩阵 $B'$，使 $\|\Sigma - B'\|_F$ 最小，其中 $\Sigma$ 是对角矩阵。对角元之间互不干扰，误差按平方累加，于是直觉上只剩下「从 $r$ 个非负数 $\sigma_i$ 中保留 $k$ 个，使被丢弃者的平方和最小」——排序后保留最大的 $k$ 个。严格证明留给 §I.9，但这里已经把「矩阵问题」化成了「排序问题」。贪心能取到全局最优的深层原因是正交性：各秩一片之间在 Frobenius 内积 $\operatorname{tr}(B_i^T B_j)$ 意义下两两正交，能量可以逐片相加，互不拖累，前一步的选择不会让后一步付出额外代价。
> 思想实验：取 $\Sigma = \begin{bmatrix}10&0&0\\0&3&0\\0&0&0.1\end{bmatrix}$。定理保证任何秩 $2$ 矩阵与它的 Frobenius 距离至少为 $0.1$，而截断 SVD 取 $\Sigma_2 = \operatorname{diag}(10,3,0)$ 恰好达到 $0.1$。第三个奇异值 $0.1$ 就是「几乎可由前两个方向解释」的冗余：它在总能量 $109.01$ 中只占约万分之零点九，丢弃它几乎无损。反过来说，若强行保留 $\sigma_1$ 与 $\sigma_3$ 而丢掉 $\sigma_2$，误差就是 $3$，远非最优——这正面说明「前 $k$ 个」里的排序不是仪式，而是最优性的实质。
> 一个可核验的视角：把 $A$ 的列看作 $m$ 维空间里的 $n$ 个点，秩 $k$ 约束就是要求这 $n$ 个点落在某个 $k$ 维子空间里。寻找最佳低秩近似因此等价于寻找「离这些列点总体最近」的 $k$ 维子空间；SVD 告诉我们，这个子空间由前 $k$ 个左奇异向量张成。把这句话与 6.042J 的最小二乘思想并列很有启发性：最小二乘是把单个点投影到给定子空间，Eckart-Young 则是把整个列集合投影到待选的子空间，投影残差的平方和就是截断误差。二者都是「欧氏距离最小化」，只是决策变量从坐标变成了子空间本身。若把列点换成行点，结论对称地落在前 $k$ 个右奇异向量上——这也是 PCA 中「主成分方向」与「样本得分方向」互为表里的几何根源。
> 用二维图像压缩复述：一张灰度图按 $m \times n$ 像素存成矩阵，若它确实由十几个强方向构成，则截断 SVD 的视觉损失与 $\sum_{i>k}\sigma_i^2$ 直接挂钩，前 $k$ 片重建的图像已经能保留大部分视觉结构；而原图存储量从 $mn$ 降到 $k(m+n)$ 的压缩比，正是奇异值衰减速度的忠实反映。
> 跨课程连接：对中心化数据矩阵 $X$，截断 SVD 的误差平方 $\sum_{i>k}\sigma_i^2$ 除以样本量就是被丢弃的方差，与 6.042J 的期望/方差脚手架直接衔接：总方差等于各主成分方差之和，截断就是「按方差贡献保留最大的 $k$ 项」。算法侧，$A_k$ 只需存 $k(m+n)$ 个数而非 $mn$ 个，联系 CSAPP 第 6 章的存储器层次：当 $k$ 很小时三块因子更容易整体留在缓存，矩阵-向量乘法的访存更紧凑；CLRS 第 9 章的选取问题则提示：只保留最大的 $k$ 个奇异值相当于部分排序，不必付出完整 SVD 的全排序代价。一句话收束：截断 SVD 把「找最佳低秩近似」这个矩阵问题，约化成「选最大的 $k$ 个奇异值」这个排序问题。
---

---

<!-- page 064: 书页 59, §1.8 奇异值与奇异向量（SVD 续） -->

### <span style="color:#c0392b;">Singular Values and Singular Vectors（奇异值与奇异向量）</span>

由 (7) 与 (8) 得到的三个核心结论如下：$V$ 包含 $A^T A$ 的标准正交特征向量（orthonormal eigenvectors），$U$ 包含 $A A^T$ 的标准正交特征向量，而 $\sigma_1^2, \ldots, \sigma_r^2$ 是 $A^T A$ 与 $A A^T$ 两者的非零特征值（nonzero eigenvalues）。

---

出于这个原因，我们还没有完全结束：SVD 要求 $Av = \sigma u$。它把每个右奇异向量（right singular vector）$v_i$ 连接到左奇异向量（left singular vector）$u_i$（$i = 1, \ldots, r$）。当我选定 $v$ 时，这一选择将决定 $u$ 的符号（signs）：如果 $Av = \sigma u$，那么 $A(-v) = \sigma(-u)$，因此我必须知道正确的符号。不仅如此，当 $\sigma^2$ 是二重特征值（double eigenvalue）时，会存在一整个特征向量平面（plane of eigenvectors）；当我在这个平面内选取两个 $v$ 时，$Av = \sigma u$ 会告诉我对应的两个 $u$。这一点正是方程 (9) 的内容。

计划是从 $v$ 入手：选取 $A^T A$ 的标准正交特征向量 $v_1, \ldots, v_r$，然后选取 $u_1, \ldots, u_r$。为了确定这些 $u$，我们要求 $Av = \sigma u$：

```math
u_k = \frac{A v_k}{\sigma_k} \qquad \text{for } k = 1, \ldots, r \tag{9}
```

于是 $A^T A v_k = \sigma_k^2 v_k$，进而

```math
A A^T u_k = \sigma_k^2 u_k \tag{10}
```

这就是 SVD 的证明！让我核实一下：那些 $u$ 确实是 $A A^T$ 的特征向量。

$v$ 已经被选成标准正交的了，我还必须检查 $u$ 也是标准正交的：

```math
u_j^T u_k = \frac{(A v_j)^T (A v_k)}{\sigma_j \sigma_k} = \frac{v_j^T (A^T A) v_k}{\sigma_j \sigma_k} = \begin{cases} 1 & \text{若 } j = k \\ 0 & \text{若 } j \neq k \end{cases}
```

注意，$(A^T A)^T = A^T A$ 是方程 (10) 的关键；而结合律（associative law）$(AB)C = A(BC)$ 是线性代数中大量证明的关键。移动括号是一个强有力的思想，这就是结合律。

---

最后我们还得选取剩下的 $n - r$ 个向量 $v_{r+1}$ 到 $v_n$，以及剩下的 $m - r$ 个向量 $u_{r+1}$ 到 $u_m$。这很容易：这些 $v$ 与 $u$ 位于 $A$ 与 $A^T$ 的零空间（nullspaces）中。我们可以为这些零空间选取任意标准正交基（orthonormal bases），它们会自动与 $A$ 的行空间（row space）中的前几个 $v$、以及 $A$ 的列空间（column space）中的前几个 $u$ 正交。这正是全部要点：$N(A) \perp C(A^T)$，且 $N(A^T) \perp C(A)$。

至此，SVD 的证明已完成。现在我们在方程 (1) 的全尺寸（full size）SVD 中有了 $U$、$V$ 与 $\Sigma$。你可能已经注意到，$A^T A$ 的特征值在 $\Sigma^T \Sigma$ 中，而同样的数 $\sigma_i^2$ 也出现在 $\Sigma \Sigma^T$ 中。一个惊人的事实：$BA$ 与 $AB$ 总是具有相同的非零特征值——这一点 5 页之后会讲到。

---

<!-- page 065: 书页 60, §I.8 SVD（续）—— Highlights of Linear Algebra 与 Example 1 详解 -->

# Strang LaLFD Part I（线性代数与从数据中学习）

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">Highlights of Linear Algebra（线性代数要点）——§I.8 SVD 的 Example 1 完整计算</span>

<span style="color:#2471a3;">**[example]**</span> **Example 1（例 1）**（完整求解 completed）求矩阵 $U, \Sigma, V$，使得 $A = U\Sigma V^T$，其中矩阵 $A$ 为

```math
A = \begin{bmatrix}3 & 0\\ 4 & 5\end{bmatrix}
```

矩阵 $A$ 的 rank（秩）为 2，因此它有两个正的 singular values（奇异值）$\sigma_1$ 与 $\sigma_2$。我们将会看到 $\sigma_1 = 3\sqrt{5}$ 大于 $\sigma_2 = \sqrt{5}$（即 $\sigma_2$ 较小）。先从 $A^TA$ 与 $AA^T$ 入手：

```math
A^TA = \begin{bmatrix}25 & 20\\ 20 & 25\end{bmatrix}, \qquad
AA^T = \begin{bmatrix}9 & 12\\ 12 & 41\end{bmatrix}
```

这两个矩阵有相同的 trace（迹）50，以及相同的 eigenvalues（特征值）$\lambda_1 = 45$ 与 $\lambda_2 = 5$。开平方根得到 $\sigma_1 = 3\sqrt{5}$ 与 $\sigma_2 = \sqrt{5}$。于是 $\sigma_1\sigma_2 = 15$，而这正是矩阵 $A$ 的 determinant（行列式）。

一个关键的步骤是求出 $A^TA$ 的 eigenvectors（特征向量）（对应特征值 45 与 5）：

```math
\begin{bmatrix}25 & 20\\ 20 & 25\end{bmatrix}\begin{bmatrix}1\\ 1\end{bmatrix} = 45\begin{bmatrix}1\\ 1\end{bmatrix}, \qquad
\begin{bmatrix}25 & 20\\ 20 & 25\end{bmatrix}\begin{bmatrix}1\\ -1\end{bmatrix} = 5\begin{bmatrix}1\\ -1\end{bmatrix}
```

于是 $v_1$ 与 $v_2$ 就是这两个相互正交（orthogonal）的特征向量重缩放（rescaled）到长度 1 后的结果——除以 $\sqrt{2}$ 即可：

**右奇异向量（Right singular vectors）**

```math
v_1 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\ 1\end{bmatrix}, \qquad
v_2 = \frac{1}{\sqrt{2}}\begin{bmatrix}1\\ -1\end{bmatrix}
```

**左奇异向量（Left singular vectors）** 现在计算 $u_1$ 与 $u_2$，它们将是 $Av_1/\sigma_1$ 与 $Av_2/\sigma_2$：

```math
u_1 = \frac{Av_1}{\sigma_1} = \frac{1}{\sqrt{10}}\begin{bmatrix}1\\ 3\end{bmatrix}, \qquad
u_2 = \frac{Av_2}{\sigma_2} = \frac{1}{\sqrt{10}}\begin{bmatrix}3\\ -1\end{bmatrix}
```

除以 $\sigma_1$ 与 $\sigma_2$ 使得 $u_1$ 与 $u_2$ 成为标准正交（orthonormal）向量。于是 $A = U\Sigma V^T$，正如所料。矩阵 $A$ 的奇异值分解（Singular Value Decomposition, SVD）就是 $U$ 乘以 $\Sigma$ 再乘以 $V^T$：

```math
A = \begin{bmatrix}3 & 0\\ 4 & 5\end{bmatrix}
  = U\Sigma V^T
  = \frac{1}{\sqrt{10}}\begin{bmatrix}1 & 3\\ 3 & -1\end{bmatrix}
    \begin{bmatrix}3\sqrt{5} & 0\\ 0 & \sqrt{5}\end{bmatrix}
    \frac{1}{\sqrt{2}}\begin{bmatrix}1 & 1\\ 1 & -1\end{bmatrix}
\tag{12}
```

$U$ 与 $V$ 分别包含 $A$ 的 column space（列空间）与 row space（行空间）的标准正交基（这两个空间都只是 $\mathbb{R}^2$）。真正的成就在于这两个基实现了 diagonalize（对角化）：$AV = U\Sigma$。矩阵 $U\Sigma V^T$ 分裂成两个 rank-one matrices（秩一矩阵）——column（列）乘以 row（行）——其中

```math
A = \sigma_1 u_1 v_1^T + \sigma_2 u_2 v_2^T
  = \frac{3}{2}\begin{bmatrix}1 & 1\\ 3 & 3\end{bmatrix}
  + \frac{1}{2}\begin{bmatrix}3 & -3\\ -1 & 1\end{bmatrix}
```

任何矩阵都是一系列秩一矩阵之和，其中的 $u$ 向量们相互正交，$v$ 向量们也相互正交。
> <span style="color:#7f8c8d;">Strang §I.8, p.60</span>

---

<!-- page 066: 书页 61, §I.8（续）奇异值与奇异向量在 SVD 中——Highlights 问题与回答 -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.8（续）奇异值与奇异向量在 SVD 中（Singular Values and Singular Vectors in the SVD）</span>

本页继续上一页 Highlights of Linear Algebra（线性代数要点）中的问题与回答（Questions and Answers）。

**问题 1（Question 1）** 如果 $S = Q\Lambda Q^T$ 是对称正定（symmetric positive definite）矩阵，它的 SVD 是什么？

它的 SVD 恰好就是 $U\Sigma V^T = Q\Lambda Q^T$。其中矩阵 $U = V = Q$ 是正交（orthogonal）矩阵，而特征值矩阵（eigenvalue matrix）$\Lambda$ 变成了奇异值矩阵（singular value matrix）$\Sigma$。

**问题 2（Question 2）** 如果 $S = Q\Lambda Q^T$ 含有一个负特征值（negative eigenvalue）（例如某个 $\lambda = -a$），那么奇异值是什么？向量 $u$ 与 $v$ 又是什么？

奇异值将是 $\sigma = +a$（正值）。其中一个奇异向量（$u$ 或 $v$ 中任选其一）必须反号（reverse the sign），即取 $-v$。于是含负特征值 $-a$ 的项 $-a\, vv^T$ 与 $\sigma(-v)v^T = +a\,(-v)v^T$ 完全相同——两处符号变化相互抵消（the two sign changes cancel）。

**问题 3（Question 3）** 如果 $U = Q$ 是一个正交矩阵，为什么它的每一个奇异值都等于 1？

因为 $A^TA = Q^TQ = I$，于是 $\Sigma = I$。所以所有奇异值都等于 1。但是 $U = Q$、$V = I$ 只是奇异向量 $u$ 与 $v$ 的一种选择：$U\Sigma V^T$ 可以是 $Q\cdot I \cdot I^T$，也可以是任意的 $(QQ_1)\cdot I \cdot Q_1^T$（其中 $Q_1$ 为任意正交矩阵）。

**问题 4（Question 4）** 为什么方阵 $A$ 的所有特征值都小于或等于谱范数 $\|A\| = \sigma_1$？

因为用正交矩阵 $U$ 与 $V^T$ 去乘不会改变向量的长度（vector lengths）：

```math
\|Av\| = \|U\Sigma V^T v\| = \|\Sigma (V^T v)\| \le \sigma_1 \|V^T v\| = \sigma_1 \|v\| \tag{13}
```

上式对所有 $v$ 成立。而由特征方程 $Av = \lambda v$ 可得 $\|Av\| = |\lambda| \, \|v\|$。于是 (13) 给出 $|\lambda| \, \|v\| \le \sigma_1 \|v\|$，从而 $|\lambda| \le \sigma_1$。

**问题 5（Question 5）** 如果 $A = uv^T$ 的秩（rank）为 1，那么 $u_1$、$v_1$ 与 $\sigma_1$ 各是什么？验证 $\sigma_1 u_1 v_1^T = A$。

奇异向量 $u_1 = u/\|u\|$ 与 $v_1 = v/\|v\|$ 的长度均为 1。于是 $\sigma_1 = \|u\| \, \|v\|$ 是奇异值矩阵 $\Sigma$ 中唯一的非零元素。这里的 SVD 是：

<span style="color:#2471a3;">**[note]**</span> **秩一矩阵（Rank 1 matrix）**

```math
A = uv^T = \sigma_1 u_1 v_1^T
```

观察（Obs.）：$A^TA = vu^T uv^T = \|u\|^2 vv^T$ 唯一的非零特征值是 $\lambda = \|u\|^2 \|v\|^2 = \sigma_1^2$，其对应的特征向量是 $v_1 = v/\|v\|$。

于是 $\sigma_1 u_1 v_1^T = \|u\| \|v\| \cdot \frac{u}{\|u\|} \cdot \frac{v^T}{\|v\|} = uv^T = A$（因为范数相互抵消（cancel））。

关键的不等式（inequality）$|u_1^T v_1| \le 1$ 恰好就是 Schwarz inequality（施瓦茨不等式）——即 $|u^T v| \le \|u\| \, \|v\|$。

**问题 6（Question 6）** Karhunen-Loève 变换（Karhunen-Loève transform）是什么？它与 SVD 有什么联系？

我们从某个零均值（zero-mean）随机过程的协方差矩阵（covariance matrix）$K$ 开始。$K$ 是对称且正定（positive definite）或半正定（positive semidefinite）的。一般地，$K$ 可以是无穷矩阵（infinite matrix）或协方差函数（covariance function），于是 K-L 展开（expansion）将是无穷级数。

$K$ 的特征向量按特征值降序 $\lambda_1 \ge \lambda_2 \ge \cdots$ 排列，它们就是 K-L 变换的基函数（basis functions）。任意向量 $x$ 在标准正交基（orthonormal basis）$x_1, x_2, \ldots$ 下的展开为

```math
x = c_1 x_1 + c_2 x_2 + \cdots
```

在这个随机（stochastic）情形下，该变换使随机过程去相关（decorrelate）：这些系数是相互独立的（independent）。不仅如此，特征值的排序意味着：只保留前 $k$ 项（在 $x_k$ 处停止）时，期望平方误差（expected square error）最小。这一事实对应于下一节 1.9 的 Eckart-Young 定理（Eckart-Young Theorem）。

这个变换是主成分分析（Principal Component Analysis, PCA）的一种随机（stochastic）形式。



## 注 11 — K-L 变换与 PCA：SVD 的随机版本

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：K-L 变换要解决的设计问题是去相关。给定零均值随机向量 $x$，协方差矩阵 $K$ 的对角元是各分量的方差，非对角元是两两协方差；非对角元非零意味着分量线性相关，一个分量的取值携带另一个分量的信息。变换的思路是换到 $K$ 的特征基：设 $K = Q\Lambda Q^T$，令 $y = Q^T x$，则 $y$ 的协方差矩阵变成 $Q^T K Q = \Lambda$，对角矩阵意味着新坐标两两不相关。这里每一步都只用你已经掌握的工具：对称矩阵正交对角化，加上「线性变换后的协方差 = $Q^T K Q$」这一条矩阵乘法规则。
> 第一性原理：这一操作的证明模板可命名为**对角化去相关（Decorrelation by Diagonalization）**。先把坐标变换与协方差变换写成同一个矩阵方程，再去读它的两个含义：$K$ 的特征向量给出方向，$K$ 的特征值给出沿该方向的方差。方向与方差被一次对角化同时解耦，而不是分开估计。特征值降序 $\lambda_1 \ge \lambda_2 \ge \cdots$ 因此自动产生「重要性排序」：第一个坐标方差最大，第二个坐标在正交于第一个方向的前提下方差最大，依此类推——这正是注 8 中 $\sigma_1 u_1 v_1^T$、$\sigma_2 u_2 v_2^T$ 的逐层剥离结构，只是这里写在协方差语言里。一个边界要分清：对角协方差消灭的是线性相关，并不自动消灭一切统计依赖，主文本里的 independent 是随机过程情形的简化表述；对只做方差解释的 PCA 而言，不相关已经足够。
> 思想实验：取二维零均值分布，协方差 $K = \begin{bmatrix}5&2\\2&2\end{bmatrix}$。$K$ 的特征值为 $6$ 与 $1$，最大特征值对应方向 $v_1 = (2,1)^T/\sqrt{5}$。把数据投影到 $v_1$ 上，投影系数的方差恰好是 $6$；沿正交方向 $v_2$ 的方差恰好是 $1$。两个分量的原始方差分别是 $5$ 与 $2$，任何单方向投影的方差都不会超过 $6$——第一主成分不是「挑分量」，而是找到方差最大的线性组合；若数据沿直线 $x_2 = x_1/2$ 高度相关，这条直线正是 $v_1$ 的方向，投影后各点的散布重新变得各向无关。用算子范数的语言，$6$ 就是 $K$ 在单位球面上的最大二次型值，与 TBB 范数、上确界语言完全对齐。
> 一个可核验的视角：$K$ 的第 $(i,j)$ 元 $k_{ij}$ 就是第 $i$ 与第 $j$ 个坐标的协方差，因此对角化 $K$ 等价于「找到一个内积坐标系，使坐标之间正交」。若把「信息」理解为方差，那么主成分排序就是把信息按大小排队，$k$ 个主成分保留的方差占总量 $\operatorname{tr}(K)$ 的比例可以精确算出——这也解释了为何协方差矩阵的迹在 PCA 中反复出现。回到矩阵与统计的交界处：$K$ 的每个特征值都是某个一维投影的方差，特征值之和等于各坐标方差之和，这个守恒关系是 6.042J 期望线性性质在协方差矩阵上的体现。再与 Question 4 的不等式对齐：$K$ 的任一特征值都非负且被最大特征值 $\lambda_1$ 压住，投影方向无论怎么选，方差都落在 $[0, \lambda_1]$ 里。
> 若数据严格落在 $x_2 = x_1/2$ 这条直线上，则 $K$ 只有一个非零特征值 $6$，另一个特征值为 $0$：方差集中在一条线上，去相关后第二坐标恒为零。这个极端情形把「近似相关产生近零特征值」说得最直白，也把 $K$ 半正定（而非正定）的可能性摆到台面上。
> 跨课程连接：对 $m$ 个样本、$n$ 个特征的数据矩阵 $X$（已中心化），$X^T X/(m-1)$ 就是样本协方差矩阵；对 $X$ 做 SVD 得到 $X = U\Sigma V^T$，代入即得 $X^T X = V\Sigma^2 V^T$，所以 $V$ 是主成分方向，$\sigma_i^2/(m-1)$ 是第 $i$ 个主成分的方差。由此可建立一条贯穿课程链：主文本在 §I.8 用 $A^T A$ 求奇异值，在 §I.9 用 Eckart-Young 证明截断最优，这里再用同一个 $X^T X$ 给出统计解释——三条路在同一点汇合。期望平方误差最小的那半句证明属于 §I.9，但其方差解释你已经可以在 6.042J 的期望/方差脚手架里完整消化。一句话收束：K-L 变换就是「在特征基上看方差」，主成分就是从大到小排列的方差。
---



## 注 12 — 谱范数与特征值不等式：矩阵「大小」的两种度量

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：要比较两种「矩阵大小」的度量：特征值模与奇异值。特征值衡量的是 $A$ 在自身特征方向上的缩放，若特征方向缺失或退化，特征值就看不见 $A$ 的某些行为；奇异值则来自单位球面上 $\|Ac\|$ 的全局最大值，扫描所有方向。设计问题在于：为什么全局扫描得到的 $\sigma_1$ 会压过任何特征值？答案藏在定义里：$\sigma_1$ 是所有方向放大倍数的最大值，而任何特征方向的放大倍数只是其中一个候选，最大者自然不小于任何候选。
> 第一性原理：证明模板是**正交不变性论证（Orthogonal Invariance Argument）**。设 $A = U\Sigma V^T$，单位向量 $v$ 满足 $Av = \lambda v$。取范数得 $|\lambda| = \|Av\| = \|U\Sigma V^T v\|$。$U$ 正交保长度，所以 $= \|\Sigma (V^T v)\|$；$V^T v$ 仍是单位向量，而 $\Sigma$ 是各奇异值为对角元的对角矩阵，它在单位向量上的最大作用就是最大的对角元 $\sigma_1$，于是 $|\lambda| \le \sigma_1$。整个论证只用了「正交矩阵保长度」与「对角矩阵的最大放大 = 最大对角元」两条最小事实，没有引入任何新名词。由此还能凑成一条链：$|\lambda| \le \sigma_1 \le \|A\|_F$，因为 $\|A\|_F^2 = \sum_i \sigma_i^2 \ge \sigma_1^2$——谱范数是「最坏方向的放大」，Frobenius 范数是「所有方向放大的平方和的根」，前者被后者包住。
> 回到不等式本身：设 $c_0$ 是单位球上使 $\|Ac\|$ 最大的向量，即 $\sigma_1 = \|Ac_0\|$；对任何单位向量 $v$ 都有 $\|Av\| \le \sigma_1$。现在让 $v$ 是一个单位特征向量，代入即得 $|\lambda| = \|Av\| \le \sigma_1$——这条捷径连 SVD 都不必引用，只用了「最大值不小于任何候选」。真正把候选提升为定理的是下一步：正交对角化保证了 $\sigma_1$ 确实被某个方向取到，而方程 (15) 保证这个方向就是 $v_1$。
> 思想实验：$A = \begin{bmatrix}0&1\\0&0\end{bmatrix}$ 把 $e_2$ 搬到 $e_1$，把 $e_1$ 压成零。$A$ 是幂零的：作用两次变为零，特征方程 $\lambda^2 = 0$ 只有一个零特征值。特征值全程只看到一个不变子空间（$e_1$ 张成的直线）上的缩放 $0$；而 $\|A e_2\| = 1$ 这个明摆着的「把长度翻倍的动作」被完全遗漏。奇异值则不然：$A^T A = \begin{bmatrix}0&0\\0&1\end{bmatrix}$，$\sigma_1 = 1$，正确捕捉到 $A$ 在 $e_2$ 上的放大；此时恰好 $\|A\|_F = 1$，整条链退化为 $|\lambda| = 0 \le \sigma_1 = 1 = \|A\|_F$。这个例子说明：特征值测的是「$A$ 在哪些方向上保持方向不变并缩放多少」，而奇异值测的是「$A$ 在所有方向上最多能把长度放大多少」。
> 一个可核验的视角：把 $A$ 看作把单位球映射为椭球，$\sigma_1$ 是椭球最长半轴。若椭球的最长半轴 $a$ 与最短半轴 $b$ 相差悬殊，那么从球到椭球的映射就是「条件很坏」的——这就是条件数 $\kappa = a/b$ 的几何来源。特征值模小于等于 $\sigma_1$ 的实质是：任何特征方向上的拉伸都只是椭球某一截面的半轴，而最长半轴天然不小于任何截面半轴。这个「截面半轴不超过最长半轴」的画面，比任何代数推演都更接近 TBB 里范数与上确界的定义方式。再用 $2 \times 2$ 矩阵复述一遍：若 $A$ 的奇异值为 $2$ 与 $0.5$，则单位圆像的椭圆半轴为 $2$ 与 $0.5$，无论 $A$ 的分量多么复杂，$\sigma_1 = 2$ 就是硬上限；此时 $\kappa = 4$，矩阵可逆但接近退化。
> 跨课程连接：这条不等式正是 TBB 实分析里算子范数公理的一个实例：$\|Av\| \le \|A\|\,\|v\|$，且 $\sigma_1$ 作为单位球面上 $\|Av\|$ 的上确界，与 TBB 的范数、上确界语言完全对齐。零奇异值的个数则连到线性代数的秩-零化度：$\min(m,n) - r$ 个零奇异值恰好记录 $A$ 把输入空间压扁的维数，这与你已经掌握的 Strang 秩定理一致。数值侧，$\sigma_1$ 是 $A$ 对向量绝对误差的最坏放大倍数，CSAPP 第 2 章的浮点舍入一旦经过 $A$ 传递，误差上界就要用这个量来估——这就是数值线性代数稳定性的入口，也为条件数 $\kappa = \sigma_1/\sigma_n$ 埋下伏笔。一句话收束：特征值忠实于 $A$ 的不变方向，奇异值忠实于 $A$ 的全部动作，度量「整体大小」时应相信奇异值。
---

# Strang LaLFD Part I（线性代数与从数据中学习）

<!-- page 067: 书页 62, §1.8 The Geometry of the SVD（SVD 的几何） -->

### SVD 的几何（The Geometry of the SVD）

奇异值分解（SVD）把一个 matrix（矩阵）分解为 $A = U\Sigma V^T$，即 (orthogonal（正交）) × (diagonal（对角）) × (orthogonal)。在二维情形下，我们可以把这些步骤画出来。正交矩阵 $U$ 和 $V$ 旋转平面，对角矩阵 $\Sigma$ 沿坐标轴把它拉伸。如 Figure 1.11（图 1.11）所示：rotation（旋转）乘以 stretching（拉伸）再乘以 rotation。单位圆上的向量 $c$ 被映到椭圆上的 $Ac$。

<span style="color:#7f8c8d;">*图 Figure 1.10：$U$ 和 $V$ 是旋转以及可能的反射；$\Sigma$ 把圆拉伸成椭圆。*</span>

这张图适用于 2×2 的可逆矩阵（因为 $\sigma_1 > 0$ 且 $\sigma_2 > 0$）。首先是 $V^T$ 把任意 $c$ 旋转为 $V^Tc$；接着 $\Sigma$ 把该向量拉伸成 $\Sigma V^Tc$；然后 $U$ 把它旋转到 $U\Sigma V^Tc = Ac$。我们保持行列式为正，以避免反射。矩阵中的四个数 $a, b, c, d$，对应两个角度 $\theta$ 和 $\varphi$，以及两个数 $\sigma_1$ 和 $\sigma_2$。

```math
A = U\Sigma V^T =
\begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}
\begin{bmatrix} \sigma_1 & 0 \\ 0 & \sigma_2 \end{bmatrix}
\begin{bmatrix} \cos\varphi & \sin\varphi \\ -\sin\varphi & \cos\varphi \end{bmatrix}
```
（14）

<span style="color:#2471a3;">**[note]**</span> 如果矩阵是 symmetric（对称）的，则 $b = c$，此时它只有 3 个（而非 4 个）参数。那么对对称矩阵 $S$，四个数 $\theta, \varphi, \sigma_1, \sigma_2$ 是如何缩减为 3 个的？

### 第一个奇异向量（The First Singular Vector）

下一页将为 $\sigma_1$ 建立一种新的看待方式。前面几页是把奇异值 $\sigma$ 选作 $A^TA$ 的 eigenvectors（特征向量），这当然依然成立。但还有一种有价值的方式：逐个地理解这些 singular vectors（奇异向量），而不是一次性全部理解。我们从 $v_1$ 和奇异值 $\sigma_1$ 开始。

最大化（Maximize）如下比值（15）：

```math
\max_c \frac{\|Ac\|}{\|c\|}
```
（15）

其最大值是 $\sigma_1$，在向量 $c = v_1$ 处取得。

椭圆（见 Figure 1.10，图 1.10）说明了为什么取到最大值的 $c$ 是 $v_1$。当你顺着页面追踪 $Ac$ 时，它终止于 $Av_1 = \sigma_1 u_1$，即椭圆的最长轴。它的长度从 $\|c\| = 1$ 开始，结束于 $\|u_1\| = \sigma_1$。



## 注 9 — SVD 的几何：旋转-拉伸-旋转与极坐标类比

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：给定 $2 \times 2$ 可逆矩阵 $A$，四个分量 $a,b,c,d$ 与四个几何参数——两个旋转角 $\theta,\varphi$ 与两个伸缩因子 $\sigma_1,\sigma_2$——之间的替换，是 SVD 作为「正交 × 对角 × 正交」的几何再编码。设计动机：$A$ 的原始分量把旋转与伸缩搅在一起，我们希望在输入侧和输出侧分别选择两个正交基，让 $A$ 的作用在基之间变成纯对角缩放。参数守恒（四个换四个）不是巧合：可逆 $2 \times 2$ 矩阵构成一个四维空间，而 $U$ 的角度、$V$ 的角度与两个奇异值正好是一组四参数坐标。
> 第一性原理：可以把它看作「把复数极形式推广为矩阵」。非零复数 $z = re^{i\theta}$ 作用于 $\mathbb{R}^2$ 是「缩放 $r$ 倍再旋转 $\theta$」；复数的乘法满足交换律，所以缩放与旋转谁先谁后无所谓。对矩阵，输入与输出的旋转不再相同，SVD 的 $A = U\Sigma V^T$ 就是把一个旋转拆成输入侧旋转 $V^T$ 与输出侧旋转 $U$，中间夹一个缩放 $\Sigma$。极分解的来历可以直接算：$A = U\Sigma V^T = (UV^T)(V\Sigma V^T)$，令 $Q = UV^T$、$P = V\Sigma V^T$，则 $Q$ 正交、$P$ 对称半正定，这就是 $A = QP$；SVD 比极分解多出的正是把 $V$ 从 $P$ 中分离出来，从而能同时看到输入与输出两个坐标系。主文本括号里的问题也由此可答：对称矩阵 $S$ 满足 $S = Q\Lambda Q^T$，输入与输出旋转合并成一个，参数从四个减为三个——一个角度加两个奇异值。
> 思想实验：取 $A = \begin{bmatrix}2&0\\0&1\end{bmatrix}$ 这样的对角矩阵，SVD 平凡：$U = V = I$，$\Sigma = A$。但把 $A$ 旋转 $45^\circ$ 后变为 $B = Q A Q^T$（$Q$ 是旋转矩阵），$B$ 的四个分量全非零，而它的 SVD 不过是 $\sigma_1 = 2$、$\sigma_2 = 1$，$U = V = Q$——椭圆只是整体转了个方向，长短半轴没变。这解释了一个重要事实：单位圆在 $A$ 下像的椭圆，其长短半轴与奇异值有关，而与坐标系选择无关；坐标旋转只改 $U$ 与 $V$，不改 $\Sigma$。反方向的退化情形同样直观：若 $\sigma_2 \to 0$，椭圆压成线段，像空间只剩一维，$A$ 不可逆——秩亏缺在几何上就是椭圆塌缩。
> 一个可核验的视角：在 Figure 1.10 的几何图景里，$\sigma_1$ 是像椭圆的长半轴，$\sigma_2$ 是短半轴；椭圆面积等于 $\pi \sigma_1 \sigma_2 = \pi |\det A|$。这与 Strang 的行列式视角接榫：正交矩阵只旋转不改变面积，所以 $|\det A| = \sigma_1 \sigma_2$，把代数中的行列式与几何中的面积缩放率统一起来。若 $\det A = 0$ 则 $\sigma_2 = 0$，椭圆塌缩为线段，面积为零——行列式为零与秩亏缺在几何上正是同一件事。方程 (14) 中四个参数守恒的原因也可由此验证：两个角度负责旋转、两个奇异值负责拉伸，任何 $2 \times 2$ 可逆变换都恰好需要这四个自由度。
> 一个推广性的观察：对 $n \times n$ 矩阵，$|\det A| = \sigma_1 \sigma_2 \cdots \sigma_n$，这是「体积缩放率」的 SVD 版本；若任一 $\sigma_i = 0$，则 $A$ 不可逆，行列式为零与奇异值出现零项完全等价。这个等式把几何体积、代数行列式与奇异值三者串成同一条链。
> 跨课程连接：若 $A$ 可逆，$A^{-1}$ 的 SVD 是 $V\Sigma^{-1}U^T$，因此 $A^{-1}$ 的奇异值是 $1/\sigma_2, 1/\sigma_1$，而 $\kappa = \sigma_1/\sigma_2$ 就是数值线性代数中的条件数，度量「可逆但接近退化」的程度，也是解方程组 $Ax = b$ 时把 $b$ 的相对误差放大到 $x$ 的倍数的上界——这是后续数值稳定性讨论中反复出现的量，与 CSAPP 第 2 章浮点相对误差的语言无缝衔接。椭圆的几何画面还给出一个 6.006 可验证的效率事实：若 $\sigma_2$ 相对 $\sigma_1$ 很小，椭圆极扁，$A$ 的信息几乎都在一个方向，低秩近似 $A_1 = \sigma_1 u_1 v_1^T$ 就够用。一句话收束：SVD 的几何图景把抽象的矩阵乘法拆成「两次旋转夹一次拉伸」，奇异值因此成为不随坐标系改变的固有尺寸。
---



## 注 10 — Rayleigh 商与奇异值的变分刻画

> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：问题在于不先构造 $A^T A$，直接用比值 $\|Ac\|/\|c\|$ 刻画最大奇异值 $\sigma_1$。这是变分（variational）思想：把对象定义为一个优化问题的解，而不是先解一个辅助方程。设计动机是「测量」与「构造」分离：要回答「$A$ 最多能把向量放大多少」，只需在单位球面上取上确界，不必先算出 $V$ 与 $\Sigma$。
> 第一性原理：与瑞利商的对偶可以写成一条恒等式：$\|Ac\|^2/\|c\|^2 = (c^T A^T A c)/(c^T c)$。左边是「$A$ 对向量 $c$ 的拉伸比的平方」，右边是「对称矩阵 $A^T A$ 的瑞利商」；平方是单调的，两个最大化问题因此完全等价。于是特征值语言与奇异值语言之间的翻译只有一步：$S$ 的特征值最大化 $c^T S c/c^T c$，而 $A$ 的奇异值平方正是 $S = A^T A$ 的特征值。若把一阶条件写出来，用商法则对 $R(c) = (c^T S c)/(c^T c)$ 求导，令分子 $\nabla(c^T S c) - R\,\nabla(c^T c) = 0$，即得 $2S c - 2R c = 0$，也就是 $S c = R c$——最大点 $c$ 是 $S$ 的特征向量。求导在这里只是确认，不是发明：瑞利商的加权平均结构已经预先决定了答案。
> 更值得记住的是这个变分刻画可迭代：剥掉 $v_1$ 方向后，在正交补空间上再最大化同一比值，就得到 $\sigma_2$，依此类推。这个「逐层剥离」模板与注 8 的排序结构严格对齐：$A_k$ 的每一片都是在「与前几片正交」的约束下使剩余能量最大化，因此贪心选出的一层层恰好拼成全局最优——这也是 §I.9 证明的核心直觉。
> 思想实验：设 $A$ 的奇异值为 $\sigma_1 = 5$、$\sigma_2 = 2$，取 $c = (v_1+v_2)/\sqrt{2}$，则 $\|Ac\|^2 = (25+4)/2 = 14.5$，比值平方 $R = 14.5$ 落在 $[4,25]$ 内；只要 $c$ 偏离 $v_1$，比值就严格下降。这个例子表明：最大值唯一地由第一奇异向量给出，这就是椭圆图景中「最长轴」的解析版本。把 $c$ 挪离 $v_1$，就是把一部分长度预算从最大放大方向搬到较小放大方向，输出自然缩水。
> 一个可核验的视角：这个最大比值问题可以按 6.042J 的优化思维拆解：目标函数 $R(c)$ 连续，约束集单位球面是紧集，连续函数在紧集上取到最大值——这是 TBB 实分析中 Weierstrass 极值定理的二维实例。最大值点满足一阶条件，恰好落在 $A^T A$ 的主特征方向上；而瑞利商作为加权平均的结构，又把「极值点在哪」这个几何问题翻译成「权重如何分配」这个离散问题。两者一结合，变分刻画就既有了存在性，又有了可计算的方向。用数值验证这层对应：$A = \operatorname{diag}(3,1)$ 时 $\sigma_1 = 3$ 且 $v_1 = e_1$，任何偏离 $e_1$ 的单位向量 $c = (\cos t, \sin t)$ 都有 $\|Ac\|^2 = 9\cos^2 t + \sin^2 t \le 9$，等号当且仅当 $\sin t = 0$。
> 再把加权平均的直觉具象化：若 $c = \sum_i c_i v_i$ 且 $\sum_i c_i^2 = 1$，则 $\|Ac\|^2 = \sum_i c_i^2 \sigma_i^2$。这是把 $\sigma_i^2$ 按权重 $c_i^2$ 做的加权平均，所以永远落在最小与最大的 $\sigma_i^2$ 之间；要逼近上界 $\sigma_1^2$，唯一办法是让 $c_1^2 \to 1$、其余权重归零。这一句已经等价于整个最大化的结论，剩下的求导只是把它写成 $A^T A c = \sigma_1^2 c$ 的固定形式。
> 跨课程连接：$\sigma_1 = \max_c \|Ac\|/\|c\|$ 正是 TBB 实分析里算子范数（单位球面上 $\|Ac\|$ 的上确界）的定义式，也是 $\|Av\| \le \|A\|\,\|v\|$ 这条范数公理的来源——矩阵方法由此接入你正在学的范数语言。算法侧，CLRS 第 4 章的分治矩阵乘法处理稠密 $A$，而低秩截断 $A_k$ 给出近似乘法，代价从 $O(mn)$ 降到 $O(k(m+n))$；$k$ 的选取依据正是奇异值的衰减速度。再往前一步，幂迭代（power iteration）从随机 $c$ 出发反复乘 $A^T A$，第 $i$ 个特征方向的系数每轮按 $\sigma_i^2$ 放大，最大的方向最终指数级胜出——这正是「最大值由加权平均锁定」这一原理的迭代版，也通向 Strang §II.1 的数值方法。一句话收束：变分刻画把「最大放大」从几何图景翻译成优化问题，再把优化问题翻译成范数上确界。
---

---

<!-- page 068: 书页 63, §1.8 奇异值与奇异向量（Singular Values and Singular Vectors in the SVD） -->

## 1.8 奇异值与奇异向量（Singular Values and Singular Vectors in the SVD）

这个 "Rayleigh quotient"（瑞利商）依赖于 $c_1, \ldots, c_n$。微积分要用 quotient rule（商法则），所以我们求它的导数。

但我们的目标是独立地推导 SVD！我们并不假设自己已经知道 $U$、$\Sigma$ 或 $V$。我们如何识别比值 $\|Ac\|/\|c\|$ 在 $c = v_1$ 时取得最大值？微积分告诉我们，一阶导数必须为零。如果先把函数平方，求导会更容易。问题（Problem）：求 $c^TS c / c^T c$ 的最大值 $\lambda$，其中 $S = A^TA$：

```math
\lambda = \max_c \frac{c^T S c}{c^T c}
```
（16）

商法则求出 $\partial/\partial c\,(c^T S c / c^T c)$。令（16）的这些 partial derivatives（偏导数）为零：

```math
\frac{\partial}{\partial c}\left(\frac{c^T S c}{c^T c}\right)
= \frac{2Sc\,(c^Tc) - 2c\,(c^TSc)}{(c^Tc)^2}
```
（17）

```math
2Sc - 2\lambda c = 0
```
（18）

```math
Sc = \lambda c
```
（19）

方程（19）说明，最好的 $c$ 是 $S = A^TA$ 的一个 eigenvector（特征向量）！

于是 $2Sc = 2\lambda c$，且 $c^TS c / c^T c$ 的最大值是 $S$ 的一个 eigenvalue（特征值）。

搜索范围被缩小到 $S = A^TA$ 的特征向量。使比值取到最大的特征向量是 $v_1$，相应的特征值是 $\sigma_1^2$。微积分证实了（15）中最大化问题的解——这正是 SVD 的第一块拼图。

为了得到完整的 SVD，我们需要全部的奇异向量和奇异值。为了求出 $v_2$ 和 $\sigma_2$，我们调整最大化问题，使它只看与 $v_1$ 正交的向量：

```math
\max_c \frac{c^T S c}{c^T c} \quad \text{subject to} \quad v_1^T c = 0
```

在条件 $v_1^T c = 0$ 下，其最大值是 $\sigma_2^2$，在 $c = v_2$ 处取得。

拉格朗日乘子（Lagrange multipliers）正是为处理像 $v_1^T c = 0$ 这样的 constraints（约束）而发明的。而习题 Problem 3（第 3 题）给出了一种处理条件 $v_1^T c = 0$ 的简单直接的方法。

同理，每一个奇异向量 $v_{k+1}$ 都是在与前面 $v_1, \ldots, v_k$ 垂直的所有向量中使比值取到最大的那个。左奇异向量则来自最大化 $\|A^Tu\|/\|u\|$——这总是在寻找一个 ellipsoid（椭球）的轴，以及对称矩阵 $A^TA$ 或 $AA^T$ 的特征向量。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 瑞利商 $R(c)=c^T S c/c^T c$ 的设计问题不是“怎么求导”，而是“为什么最大化它恰好给出最大特征方向”。答案藏在平均值结构里。把 $c$ 在 $S$ 的正交特征向量基 $x_1,\ldots,x_n$ 上展开为 $c=\sum c_i x_i$，利用 $x_i^T x_j=0$（$i\ne j$）与 $S x_i=\lambda_i x_i$，立即得到 $R(c)=\sum c_i^2\lambda_i/\sum c_i^2$（完整计算见 Problem 1, page_073）。系数 $c_i^2$ 非负且总和等于分母，因此 $R(c)$ 是特征值的加权平均，权重归一化后就是凸组合——$p_i=c_i^2/\sum c_j^2$ 满足 $p_i\ge0$、$\sum p_i=1$，这正是 6.042J 里概率质量的定义——比值被锁在 $[\lambda_n,\lambda_1]$ 内。又因 $R(\alpha c)=R(c)$（$\alpha\ne0$），比值只看方向、不看长度，把定义域限制到单位球不损失任何信息；这就是“$\|c\|=1$”不是额外假设而是归一化自由度的原因。从 6.042J 等价关系看，$c\sim\alpha c$ 把非零向量分成方向类，瑞利商是这些等价类上的良定义函数，单位球不过是给每个类取一个代表元。
> 为什么这个代数式子正是正文（15）的几何问题？因为 $\|Ac\|^2=c^T(A^TA)c=c^T S c$，而单位球约束让分母恒为 $1$。所以“单位球上找最大拉伸方向”逐字等于“最大化瑞利商”；$A$ 本身不必对称，对称性由 $S=A^TA$ 承担。最大值的取得不需要微积分，只需要一次“全押”：有界随机变量的期望永远夹在最大值与最小值之间，且取到最大值当且仅当分布退化——全部质量落在最大特征值 $\lambda_1$ 上，即 $c$ 落在 $\lambda_1$ 的特征子空间；若 $\lambda_1$ 单重，就是与 $x_1$ 共线。这就是 SVD 第一块拼图的全部内容。
> 用 $2\times2$ 对角阵 $S=\operatorname{diag}(3,1)$ 做思想实验。单位向量写成 $c=(\cos\theta,\sin\theta)$，则 $R(c)=3\cos^2\theta+\sin^2\theta=1+2\cos^2\theta$，在 $\cos^2\theta=1$（$\theta=0$ 或 $\pi$，即 $x_1$ 轴）取最大 $3$，在 $\cos^2\theta=0$（$x_2$ 轴）取最小 $1$。这与你从微积分得到的驻点一致，但完全不需要求导：目标值只依赖方向与各特征轴的夹角。费曼式直觉：瑞利商是一张按“方向与各特征轴的夹角”给自己发的期望奖金，想拿最多就把概率全押在最大奖 $\lambda_1$ 上。
> 求 $v_2$ 的约束 $v_1^T c=0$ 在概率语言里就是强制 $p_1=0$，再在剩余权重上重新最大化。这给出可命名模板“贪婪剥离”（greedy deflation）：每轮先证明存在一个最优解包含当前最大方向（贪心选择），再把问题收缩到它的正交补，逐层剥出全部奇异向量——这与 CLRS §16.1 活动选择问题“贪心选择性质加子问题收缩”的模板同构，只是可行域从时间区间换成了子空间。
> 梯度 $\partial R/\partial c=2(Sc-R(c)c)/(c^T c)$ 指向支配方向：把 $c$ 反复用 $S$ 乘（幂迭代，参见 Strang §II.1），第 $k$ 个特征方向的分量每步相对第一大方向乘以 $\lambda_k/\lambda_1<1$，按几何级数衰减——这正是 TBB 中 $|q|<1$ 时 $q^m\to0$ 的速率论证，也是数值上幂迭代收敛到 $v_1$ 的原因。
> 同一论证反向运行就得到最小值 $\lambda_n$，当 $c$ 与最小特征向量对齐。于是瑞利商把整个方向球面压成区间 $[\lambda_n,\lambda_1]$；这个双侧观被后文反复使用——page_076 的三种范数注正是在奇异值上做同样的最大/总和读数。若 $\lambda_1$ 有重数，$v_1$ 不唯一，但最大值仍是 $\lambda_1$，正文任选一个，其余方向由正交约束逐层剥离。
> 一句话收束：瑞利商把几何问题（找最大拉伸方向）翻译成概率问题（把质量全押在最大特征值上），SVD 的每一层奇异向量只是这个翻译的逐层重复。
---


---

<!-- page 069: 书页 64, §I.8 SVD 续：A Different Symmetric Matrix Also Produces the SVD -->
# Strang LaLFD Part I（线性代数与从数据中学习）

### A^T 的奇异向量（The Singular Vectors of A^T）

<span style="color:#2471a3;">**[section]**</span> 一个 SVD（奇异值分解）把 row space（行空间）中的 $v$ 与 column space（列空间）中的 $u$ 连接起来。当我们转置 $A = U\Sigma V^T$ 时，看到 $A^T = V\Sigma^T U^T$ 沿相反方向走，从 $u$ 到 $v$：

```math
Av_k = \sigma_k u_k \quad (k = 1, \ldots, r)
\qquad\text{和}\qquad
A^T u_k = \sigma_k v_k \quad (k = 1, \ldots, r)
\qquad (20)
```

将 $Av_k = \sigma_k u_k$ 两边乘以 $A^T$。回忆方程 (9) 中的 $A^T A v_k = \sigma_k^2 v_k$，再除以 $\sigma_k$ 就得到 $A^T u_k = \sigma_k v_k$。

---

### 另一种产生 SVD 的对称矩阵（A Different Symmetric Matrix Also Produces the SVD）

<span style="color:#2471a3;">**[section]**</span> 我们是用两个对称矩阵 $A^T A$ 与 $AA^T$ 构造出 SVD 的。另一个好办法是使用一个对称分块矩阵 S（symmetric block matrix）。这个矩阵 S 把 $u$ 与 $v$ 成对地配成特征向量，对应特征值 $\pm \sigma_k$。矩阵 S 的非零特征值是 $\sigma_k$ 与 $-\sigma_k$，它的规模（size）是 $m + n$：

```math
S = \begin{bmatrix} 0 & A \\ A^T & 0 \end{bmatrix}
\qquad\text{具有特征向量}\qquad
\begin{bmatrix} u_k \\ v_k \end{bmatrix} \ \text{与} \ \begin{bmatrix} u_k \\ -v_k \end{bmatrix}
```

我们可以直接验证这些特征向量，记住 $Av_k = \sigma_k u_k$ 与 $A^T u_k = \sigma_k v_k$：

```math
\begin{bmatrix} 0 & A \\ A^T & 0 \end{bmatrix}\begin{bmatrix} u_k \\ v_k \end{bmatrix}
= \begin{bmatrix} Av_k \\ A^T u_k \end{bmatrix}
= \begin{bmatrix} \sigma_k u_k \\ \sigma_k v_k \end{bmatrix}
= \sigma_k \begin{bmatrix} u_k \\ v_k \end{bmatrix}
```

以及

```math
\begin{bmatrix} 0 & A \\ A^T & 0 \end{bmatrix}\begin{bmatrix} u_k \\ -v_k \end{bmatrix}
= \begin{bmatrix} -Av_k \\ A^T u_k \end{bmatrix}
= -\sigma_k \begin{bmatrix} u_k \\ -v_k \end{bmatrix}
\qquad (21)
```

这样就得到 $2r$ 个特征值。这些特征向量是正交的：对 $k \neq j$ 有 $[u_k; v_k]^T [u_j; v_j] = u_k^T u_j + v_k^T v_j = 0$，且 $[u_k; v_k]^T [u_k; -v_k] = 1 - 1 = 0$。你能看出这个分块矩阵还有 $(m - r) + (n - r)$ 个特征值 $\lambda = 0$ 的特征向量吗？它们必然涉及 $A^T$ 与 A 的 nullspaces（零空间）中剩余的那些 $u$ 与 $v$。

---

### AB 与 BA：相等的非零特征值（AB and BA: Equal Nonzero Eigenvalues）

<span style="color:#2471a3;">**[section]**</span> 如果 A 是 $m \times n$ 而 B 是 $n \times m$，那么 AB 与 BA 有相同的非零特征值。从 $ABc = \lambda c$（$\lambda \neq 0$）开始，两边同乘以 B，得到 $BABc = \lambda Bc$。这表示 Bc 是 BA 的一个 eigenvector（特征向量），对应同一个特征值 $\lambda$——正是我们想要的。我们需要 $\lambda \neq 0$ 来确保这个特征向量 Bc 不是零向量。

注意，如果 B 是方阵且可逆，那么 $B^{-1}(BA)B = AB$。这说明 BA 与 AB 相似（similar）：有相同的特征值。但我们的第一个证明允许 A 与 B 分别是 $m \times n$ 与 $n \times m$。这就覆盖了 SVD 中 $B = A^T$ 的重要例子。在这种情况下，$A^T A$ 与 $AA^T$ 都引出 A 的 singular values（奇异值）。如果 $m > n$，那么与 BA 相比，AB 多出 $m - n$ 个额外的零特征值。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制是“加倍嵌入”：把 $m\times n$ 的矩形矩阵 $A$ 焊进 $(m+n)\times(m+n)$ 的对称矩阵 $S=\begin{bmatrix} 0 & A \\ A^T & 0 \end{bmatrix}$，让本没有特征值的 $A$ 借 $S$ 获得特征值。分块规则直白：$A$ 与 $A^T$ 只占据副对角线，主对角线留零。这个形状自带一个符号翻转相似：取 $P=\operatorname{diag}(I_m,-I_n)$，左乘把下块变号，右乘把右块变号，于是 $PSP^{-1}=-S$。相似变换不改变谱，而 $\lambda$ 是 $-S$ 的特征值当且仅当 $-\lambda$ 是 $S$ 的特征值，所以非零特征值只能成对出现为 $\pm\sigma_k$。更有用的是：若 $Sx=\lambda x$，则 $S(Px)=-\lambda(Px)$，即 $P$ 把每个正特征向量自动送到负特征向量，配对不是巧合，而是结构强制的。
> 展开单个特征向量：设 $Av=\sigma u$、$A^T u=\sigma v$，则 $S\begin{bmatrix} u \\ v \end{bmatrix}=\begin{bmatrix} Av \\ A^T u \end{bmatrix}=\sigma\begin{bmatrix} u \\ v \end{bmatrix}$；换成 $[u;-v]$ 得 $-\sigma$。同一个 $\sigma$ 的两个符号各管一半：正号向量把 $u$ 与 $v$ 同向并置，负号向量把它们反向并置。再平方就退耦：$S^2=\operatorname{diag}(AA^T,A^TA)$，特征值统一为 $\sigma_k^2$，每个重数加倍。平方在这里的作用是“去符号、验证配对”：它把 $\pm\sigma$ 折叠成 $\sigma^2$，同时把 $u$ 子问题与 $v$ 子问题分块存放，便于与 $A^TA$、$AA^T$ 的谱核对一致。反过来这也说明为何 SVD 不直接算 $A^TA$：平方丢失了 $\sigma$ 的符号信息，还把条件数平方为 $\kappa(A)^2$，对小奇异值而言等于在浮点表示中把下溢与舍入误差放大；直接对 $A$ 或 $S$ 工作才数值稳定。
> 具体例子：取 $A=\begin{bmatrix} 2 & 0 \\ 0 & 1 \\ 0 & 0 \end{bmatrix}$（$3\times2$，秩 $2$）。$S$ 是 $5\times5$，非零特征值为 $\pm2,\pm1$，外加一个零特征值；特征向量分别是 $[e_1;e_1]$、$[e_1;-e_1]$、$[e_2;e_2]$、$[e_2;-e_2]$ 与 $[0,0,1,0,0]^T$。逐块验证 $[e_1;e_1]$：上块 $Ae_1$ 是第一列 $[2,0,0]^T$，下块 $A^T e_1=[2,0]^T$，整体恰为 $2$ 倍自身。零特征向量则来自左零空间：$A^T u_3=0$，$v$ 侧没有贡献。一般地，零特征值个数是 $(m-r)+(n-r)=m+n-2r$，即左、右零空间维数之和——这正是 Strang 线性代数四个基本子空间维数公式的直接应用，也解释了为何加倍后“多出来”的谱空间全由零特征值填满。
> 跨课程路径：AB/BA 非零谱相等这条定理的证明是 6.042J 式的双射论证——若 $ABx=\lambda x$ 且 $\lambda\neq0$，则 $Bx\neq0$ 且 $BA(Bx)=\lambda(Bx)$，映射 $x\mapsto Bx$ 把 $AB$ 的 $\lambda$ 特征空间单射进 $BA$ 的 $\lambda$ 特征空间，反向同理，故非零谱一一对应；关键在 $\lambda\neq0$，否则 $Bx=0$ 会让映射失效。$S$ 做的只是把这个代数事实几何化。算法侧，CLRS §30.2 的 FFT 靠“重组出对称结构”：按奇偶下标（二分）排列输入后，$n$ 点 DFT 矩阵被置换成四个 $n/2$ 块，其中两块正是 $F_{n/2}$，另两块乘旋转因子，规模减半的递归才成立；这是用置换换结构，此处则是用加倍换对称。CSAPP 第 6 章的矩阵乘法分块同理：把大矩阵切成能装进缓存的小块，付出重排代价、换取局部性收益，属于同一设计模式。100B 实分析里的偶延拓（把 $[0,a]$ 上的函数对称延拓到 $[-a,a]$）也是这种对称化直觉：把只有“半段”的问题补成有对称性的整体，再在整体上做谱分解，奇偶与正负一一对应。
> 收束与可复用模板：记“副对角加倍嵌入”四步法——第一步，把对偶对象 $X$ 与 $Y$ 放副对角；第二步，用 $P=\operatorname{diag}(I,-I)$ 证谱关于 $0$ 对称；第三步，平方得 $\operatorname{diag}(XY,YX)$ 解耦验证；第四步，零特征值个数由两个零空间维数补齐。直觉是：当一个矩形问题被拆成“左”与“右”两半时，先把它偶延拓成一个整体，符号翻转给出配对，平方给出验证，零空间负责补齐维数。
---


---

<!-- page 070: 书页 65, §I.8 Singular Values and Singular Vectors in the SVD -->

### §I.8 SVD 中的奇异值与奇异向量（Singular Values and Singular Vectors in the SVD）

### 子矩阵有更小的奇异值（Submatrices Have Smaller Singular Values）

<span style="color:#2471a3;">**[section]**</span> 最大的奇异值 $\sigma_1$ 是通过在单位向量上最大化 $\|Ax\|$ 求得的。这使证明下面这个有用的事实变得容易：一个 submatrix（子矩阵）的 norm（范数）不可能大于整个矩阵的范数：

```math
\sigma_1(B) \le \sigma_1(A)
```

如果 B 保留 A 的 M 行和 N 列，那么 $\|B\| \le \|A\|$。（22）

<span style="color:#2471a3;">**[proof]**</span> 只看那些在对应 B 的 N 列的位置上有非零元的向量。显然 $\max \|Bx\| \le \max \|Ax\|$。再进一步，只查看对应 B 的 M 行的那些分量，可以进一步缩小 $\|Bx\|$。所以删去列和行不可能增大范数，因而 $\|B\| \le \|A\|$。

---

### 导数与积分的 SVD（The SVD for Derivatives and Integrals）

<span style="color:#2471a3;">**[section]**</span> 这可能是 SVD 最清晰的例子。它不是从矩阵开始的（但我们随后会讲到矩阵）。历史上，第一个 SVD 不是针对向量，而是针对函数（functions）。此时 A 不是矩阵而是算子（operator）。一个例子是对每个函数求积分的算子；另一个例子是取导数的（无界）算子 D（unbounded operator D）：

```math
(Ac)(t) = \int_0^t c(s)\,ds \qquad \text{和} \qquad (Dc)(t) = \frac{dc}{dt}
\qquad (23)
```

这些算子都是线性的（否则微积分会比现在困难得多）。依据微积分基本定理（Fundamental Theorem of Calculus），在某种意义上 D 是 A 的逆。更准确地说，DA 是一个左逆（left inverse）：$DA = I$，即积分的导数等于原来的函数。但 $AD \neq I$，因为常数函数的导数是零。于是 A 有一个 nullspace（零空间），就像一个列相关的矩阵。D 是 A 的 pseudoinverse（伪逆）！对 $A$ = 积分、$D$ = 导数而言，正弦和余弦就是 v 与 u：

```math
A(\cos kt) = \frac{1}{k}\sin kt \qquad \text{然后} \qquad D(\sin kt) = k\cos kt
\qquad (24)
```

这些方程的简洁性正是我们把它们写进书里的原因。我们处理的是周期函数（periodic functions）：$f(t + 2\pi) = f(t)$。矩阵 A 的输入空间包含偶函数（even functions），如 $\cos t = \cos(-t)$。矩阵 A 的输出（也就是 D 的输入）是奇函数（odd functions），如 $\sin t = -\sin(-t)$。这些输入空间与输出空间，就像一个 $m \times n$ 矩阵的 $\mathbb{R}^n$ 与 $\mathbb{R}^m$。

奇异值分解的特殊性质是：v 相互正交，u 也相互正交。在这里，那些奇异向量变成了非常漂亮的函数——余弦彼此正交，也与正弦正交。它们的内积（inner products）全都等于零：

```math
\int_0^{2\pi} (\cos kt)(\cos jt)\,dt = 0 \qquad \text{和} \qquad \int_0^{2\pi} (\sin kt)(\sin jt)\,dt = 0 \qquad (k \neq j)
```




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 不等式 $\sigma_1(B)\le\sigma_1(A)$（方程 22）的设计问题：为什么删掉行和列之后，最大拉伸能力不可能变大？答案可以压缩成一句话——可行域缩小、范数投影只会缩短。可命名模板为“限制—投影单调法”：要比较两个最大化问题，先把小问题的每个可行解嵌入大问题的可行域，再证明嵌入后目标值不大于原目标值，两边同时取最大即得不等式。
> 第一性原理展开。出发点是 $\sigma_1(A)=\max_{\|x\|=1}\|Ax\|$。设 $B$ 保留 $A$ 的 $M$ 行、$N$ 列。第一步限制定义域：只考虑在 $N$ 列之外分量为零的单位向量，这些向量构成单位球的子集，子集上的最大值不超过全集上的最大值。第二步投影值域：对这样的 $x$，$Ax$ 是长向量，$Bx_N$ 恰好是 $Ax$ 中 $M$ 个坐标组成的子向量，模长平方少加若干非负项，故 $\|Bx_N\|\le\|Ax\|$。两步合起来就是 $\sigma_1(B)\le\sigma_1(A)$。矩阵语言更干净：$B=PAQ$，$P$ 是行选取（$\|Pz\|\le\|z\|$），$Q$ 是列选取且 $Q^TQ=I$（$\|Qy\|=\|y\|$），于是任意 $y$ 满足 $\|By\|=\|PAQy\|\le\|AQy\|\le\sigma_1(A)\|Qy\|=\sigma_1(A)\|y\|$。
> 用具体数字验证：$A=\begin{bmatrix}1&2\\3&4\end{bmatrix}$，删成 $B=[1]$。显然 $\sigma_1(B)=|1|=1$；而取 $e_1$ 得 $\sigma_1(A)\ge\|Ae_1\|=\sqrt{1^2+3^2}=\sqrt{10}>1$。这条链正是证明的微缩版：$e_1$ 是列限制后的单位向量，$Ae_1=(1,3)^T$ 删去第二行得到 $B$ 的输入输出。取等条件同样可读：当被删的部分对最大拉伸毫无贡献时等式成立，例如 $A$ 的谱范数由被保留的块单独达到。
> 思想实验：把 $A$ 看成把单位球映成椭球的映射，$\sigma_1$ 是椭球最长半轴。限制输入为某个坐标子空间、再删掉若干输出坐标，等于先截椭球的一个截面，再把截面投影到更低维坐标平面；投影只会缩短长度，所以最长半轴不可能变长——影子的长度不会超过棍子。
> 跨课程连接。TBB 中上确界的序性质：若 $F\subseteq G$ 则 $\sup F\le\sup G$，本注就是在定义域与值域上连用两次这个性质。CLRS §15.1 钢条切割里出现同一个模板：长度 $i$ 的每个可行切割都可以嵌入长度 $n$ 的可行切割（补上一段长为 $n-i$ 的不切段），在价格非负的标准假设下补段不减少收益，故最优收益 $r_i\le r_n$——嵌入后可行域变大，最优值单调。本页习题集 Problem 5（第 5 题）给出另一种拆法：先删列得 $C$，转置不改变谱范数（$\|C^T\|=\|C\|$），再删列得 $B^T$，最后 $\|B\|=\|B^T\|$；顺序不同，但每一步都是同一种单调步骤。从数据矩阵的角度看，删掉一列（去掉一个特征）或删掉一行（去掉一个样本），新矩阵的谱范数都不会变大，这为“用特征子集做近似”提供了单调性保证。若删到极限 $B=0$，则 $\sigma_1(B)=0$，不等式退化为 $\sigma_1(A)\ge0$，平凡但一致。另一个边界：这套变分论证专属于谱范数，Frobenius 范数的相应不等式同样成立，但证据不是变分法，而是逐项平方和的平凡单调性——$\|B\|_F^2$ 比 $\|A\|_F^2$ 少掉的正是被删行列元素的平方；同一结论、两种工具，正是几何证法与代数证法的典型分工。
> 一句话收束：谱范数的子矩阵不等式不是新魔法，而是“子集的上确界不超过全集的上确界”在定义域与值域上各用一次。
---


---

<!-- page 071: 书页 66, §I.8 结尾 Highlights of Linear Algebra：Finite Differences 与 DST/DCT -->

# Strang LaLFD Part I（线性代数与从数据中学习）

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">Highlights of Linear Algebra（线性代数要点）</span>

<span style="color:#2471a3;">**[section]**</span> 注意，函数 $f$ 与 $g$ 的 inner product（内积）就是 $f(x)g(x)$ 的 integral（积分）：

```math
(f, g) = \int f(x)g(x)\,dx
```

这就在 function space（函数空间，即 Hilbert space（希尔伯特空间））中复制了那个把对应分量乘积相加的 dot product（点积）$\sum x_i z_i$。事实上，积分符号 $\int$ 正是由字母 $S$ 演变而来——积分就是和的极限（integrals are the limits of sums）。

---

### Finite Differences（有限差分）

<span style="color:#2471a3;">**[section]**</span> 导数的离散形式（discrete form）是一个 finite difference（有限差分）；积分的离散形式是一个 sum（和）。这里我们选取一个 4 by 3 的矩阵 $D$，它对应带 $D^T$ 的 backward difference（向后差分）：

```math
D = \begin{bmatrix} 1 & 0 & 0 \\ -1 & 1 & 0 \\ 0 & -1 & 1 \\ 0 & 0 & -1 \end{bmatrix}
\qquad (25)
```

为了求 singular values（奇异值）与 singular vectors（奇异向量），我们计算 $D^T D$（3 by 3）与 $D D^T$（4 by 4）：

```math
D^T D = \begin{bmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{bmatrix}
\qquad \text{以及} \qquad
D D^T = \begin{bmatrix} 1 & -1 & 0 & 0 \\ -1 & 2 & -1 & 0 \\ 0 & -1 & 2 & -1 \\ 0 & 0 & -1 & 1 \end{bmatrix}
\qquad (26)
```

nonzero eigenvalues（非零特征值）总是相同的！$D D^T$ 还有一个零特征值，对应的 eigenvector（特征向量）是 $(1, 1, 1, 1)/2$。这就是常函数 $1$（其导数为 $0$）的离散对应物（discrete equivalent）。

两个对称矩阵 $D^T D$ 与 $D D^T$ 的非零特征值为

```math
\lambda = 2 - \sqrt{2}, \qquad 2, \qquad 2 + \sqrt{2}
```

$D^T D$ 的特征向量 $V$ 是 $D$ 的 right singular vectors（右奇异向量），它们是 discrete sines（离散正弦）。$D D^T$ 的特征向量 $U$ 是 $D$ 的 left singular vectors（左奇异向量），它们是 discrete cosines（离散余弦）：

```math
V = \begin{bmatrix}
1/2 & \sqrt{2}/2 & 1/2 \\
\sqrt{2}/2 & 0 & -\sqrt{2}/2 \\
1/2 & -\sqrt{2}/2 & 1/2
\end{bmatrix}
```

```math
U = \begin{bmatrix}
1/2 & \cos(\pi/8)/\sqrt{2} & 1/2 & \cos(3\pi/8)/\sqrt{2} \\
1/2 & \cos(3\pi/8)/\sqrt{2} & -1/2 & -\cos(\pi/8)/\sqrt{2} \\
1/2 & -\cos(3\pi/8)/\sqrt{2} & -1/2 & \cos(\pi/8)/\sqrt{2} \\
1/2 & -\cos(\pi/8)/\sqrt{2} & 1/2 & -\cos(3\pi/8)/\sqrt{2}
\end{bmatrix}
```

<span style="color:#2471a3;">**[note]**</span> 这些就是著名的 DST 与 DCT 矩阵——Discrete Sine Transform（离散正弦变换）与 Discrete Cosine Transform（离散余弦变换）。DCT 矩阵一直是 JPEG image compression（JPEG 图像压缩）的骨干（backbone）。实际上 JPEG 把矩阵增大到 8 by 8，从而减少了图像的 "blockiness"（块状感）。8 by 8 的像素块（blocks of pixels）先经 two-dimensional DCT（二维 DCT）变换，再被压缩与传输。这些矩阵的正交性（orthogonality）正是 Section IV.4（§IV.4）的关键。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 有限差分矩阵 $D$（方程 25，$4\times3$ 向后差分）为什么天然带出 DST 与 DCT？核心机制是边界条件决定特征函数。计算 $D^TD=\begin{bmatrix}2&-1&0\\-1&2&-1\\0&-1&2\end{bmatrix}$ 与 $DD^T=\begin{bmatrix}1&-1&0&0\\-1&2&-1&0\\0&-1&2&-1\\0&0&-1&1\end{bmatrix}$（方程 26）。$D^TD$ 对应两端取零的离散二阶差分（Dirichlet 条件），特征向量是离散正弦——$\sin$ 在两端取零；$DD^T$ 对应两端自由的离散二阶差分（Neumann 条件），特征向量是离散余弦——$\cos$ 在两端导数为零。书上列出的非零特征值 $\lambda=2-\sqrt2,2,2+\sqrt2$ 就是 $\sigma_k^2$；于是 $Dv_k=\sigma_k u_k$ 成为 $D(\sin kt)=k\cos kt$ 的离散版，与 page_070 的积分/导数算子 SVD 完全同构。也可以反向看：$D^T$ 是逐分量累计求和，是积分的离散近似，所以 $D^TD$ 是“先积分再求导”的离散二阶差分。联系 page_070：连续情形中积分算子的输入是偶函数 $\cos$、输出是奇函数 $\sin$；离散情形中 $D^TD$ 生成离散正弦、$DD^T$ 生成离散余弦，偶/奇对应被有限差分完整保留下来。
> JPEG 选 DCT 而非 DFT，关键在块边界。$8\times8$ 块独立变换、独立量化；若直接对块做 DFT，隐式假设块周期重复，周期延拓在左右边界会出现灰度跳跃，人为制造高频，量化重建后块缝处出现 discontinuity，即 blocking artifacts。DCT-II 的等价实现是先把 8 点块对称反射成 16 点偶信号再做 DFT：偶对称使正弦分量两两抵消只剩余弦，更重要的是反射后的周期延拓在边界处连续，能量集中在低频，量化误差不再集中在块缝。这就是“隐含 Neumann 反射边界条件”的含义。为什么不选 DST？DST 隐含奇反射，两端强制为零，等于强迫块边缘像素变黑；DCT 的偶反射允许边界取任意灰度值，对自然图像块边缘更可接受。
> 能量集中是压缩真正的来源。自然图像块内灰度变化平缓，DCT 后大部分能量集中在左上角低频系数；量化把高频系数大多归零。量化后的系数按 zigzag 顺序从低频到高频扫描，配合游程编码把连续零段压缩成计数——这是 JPEG 基线流程的标准做法。若用 DFT，周期延拓在块边界制造的跳跃本身就是高频，量化丢弃后误差恰好落在块缝，正是视觉最敏感处。所以 DCT 不是比 DFT“更正确”的变换，而是对有限块做延拓时边界假设更正确的变换：它把块边缘的不连续性折叠成光滑的偶延拓。
> 这个设计同时讨好硬件与算法。CSAPP §6.1 的局部性原理：8 位灰度的 $8\times8$ 块恰好是 $64$ 字节，与 CSAPP §6.4 中典型的 64 字节 cache block 对齐，整块可驻留 L1 就地变换；若用 $16\times16$ 块就要跨多条 cache line。算法上 2D DCT 可分离：$C=UXU^T$，先对每行做 1D DCT，再对每列做一次；1D DCT 与 CLRS §30.2 的 FFT 同属分治模板——把长度 $N$ 拆成两个 $N/2$ 再合并，$O(N\log N)$，二维合计 $O(N^2\log N)$，而朴素矩阵乘法是 $\Theta(N^3)$。
> SVD 压缩（KLT，即数据协方差矩阵的特征向量基/PCA）在 Frobenius 意义下最优，但基向量依赖数据本身：要么额外传输基，要么每图重做 SVD；DCT 是固定基、与数据无关、有快速算法，成本极低。工程中最优性让位于可计算性。
> 一句话收束：DST/DCT 是差分算子在不同边界条件下的固有模态，JPEG 选 DCT 本质是选了一个让块边界“看不见”的坐标系。
---


---

<!-- page 072: 书页 67, §I.8：Fourier 与 LTI；The Polar Decomposition A = QS 与 Example -->

### <span style="color:#2471a3;">**[section]**</span> 我们的目标是展示美丽的 Singular Value Decomposition（奇异值分解）$D(\sin) = \sigma(\cos)$ 的离散形式。你完全可以说这只是一个例子。但对于常系数（constant coefficients）线性方程，Fourier（傅里叶）总是会出现——而且总是重要的。

在 signal processing（信号处理）中，关键的字母是 LTI：Linear Time Invariance（线性时不变）。

---

### The Polar Decomposition A = QS（极分解 A = QS）

<span style="color:#2471a3;">**[section]**</span> 每个复数 $z$ 都有极形式（polar form）$z = re^{i\theta}$。一个数 $r \ge 0$ 乘以单位圆（unit circle）上的一个数。我们有

```math
z = r\cos\theta + ir\sin\theta
```

把这些数看作 1 by 1 的矩阵。于是"一个 orthogonal matrix（正交矩阵）$Q$ 乘以 $r \ge 0$"正是一个 positive semidefinite matrix（半正定矩阵）（称之为 $S$）。极分解（polar decomposition）把同样的思想推广到 n by n 矩阵：orthogonal times positive semidefinite（正交乘半正定），即 $A = QS$。

<span style="color:#2471a3;">**[theorem]**</span> <span style="color:#c0392b;">每一个实的 square matrix（方阵）都能分解为 $A = QS$，其中 $Q$ 是正交矩阵，$S$ 是半正定矩阵。若 $A$ 可逆，则 $S$ 是 positive definite（正定）的。</span>

```math
A = U\Sigma V^T = (UV^T)(V\Sigma V^T) = (Q)(S)
\qquad (28)
```

第一个因子 $UV^T = Q$ 是正交矩阵——正交矩阵的乘积仍正交。第二个因子 $V\Sigma V^T = S$ 是半正定的，因为它的特征值都取自 $\Sigma$（即奇异值 $\sigma \ge 0$）。若 $A$ 可逆，则 $\Sigma$ 与 $S$ 也都可逆。$S$ 是 $A^T A$ 的 symmetric square root（对称平方根），因为 $S^2 = V\Sigma^2 V^T = A^T A$。于是 $S$ 的特征值就是 $A$ 的奇异值；$S$ 的特征向量就是 $A$ 的奇异向量 $v$。

还存在反向顺序的极分解 $A = KQ$。此时 $Q$ 相同，但现在 $K = U\Sigma U^T$。于是 $K$ 是 $AA^T$ 的 symmetric positive definite square root（对称正定平方根）。

---

<span style="color:#2471a3;">**[example]**</span> **Example（例）** 求 $A = \begin{bmatrix}3 & 0\\ 4 & 5\end{bmatrix}$ 的极分解中的 $Q$ 与 $S$（rotation（旋转）与 stretch（拉伸））。

<span style="color:#2471a3;">**[proof]**</span> **Solution（解）** 矩阵 $U$ 与 $V$ 已在上面方程 (3) 处求得：

```math
Q = UV^T = \frac{1}{\sqrt{5}}\begin{bmatrix}2 & -1\\ 1 & 2\end{bmatrix}
\qquad \text{以及} \qquad
S = V\Sigma V^T = \sqrt{5}\begin{bmatrix}2 & 1\\ 1 & 2\end{bmatrix}
```

于是 $A = QS$。

在力学（mechanics）中，极分解把 rotation（旋转，位于 $Q$ 中）与 stretching（拉伸）分离开来。$S$ 的特征值给出 Figure I.10（图 I.10）中的 stretching factors（拉伸因子）。$S$ 的特征向量给出拉伸方向（stretching directions）——即椭圆（ellipse）的 principal axes（主轴）。Section IV.9（§IV.9）关于 orthogonal Procrustes problem（正交 Procrustes 问题）的论述指出：$Q$ 是离 $A$ 最近的 orthogonal matrix（正交矩阵）。
> <span style="color:#7f8c8d;">Strang §I.8, p.67</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 极分解 $A=QS$ 的设计问题：如何把任意方阵的作用拆成“旋转/反射”与“拉伸”两个可独立理解的部分？第一性原理来自 SVD：$A=U\Sigma V^T$，在中间插入 $V^TV=I$，得 $A=(UV^T)(V\Sigma V^T)$。$Q=UV^T$ 是正交矩阵之积，仍正交；$S=V\Sigma V^T$ 与 $A^TA$ 同对角化，特征值为奇异值 $\sigma_i\ge0$，故半正定，且 $S^2=A^TA$。逐列看更清楚：$Av_i=\sigma_i u_i$ 拆成两步——$Sv_i=\sigma_i v_i$ 沿 $v_i$ 拉伸 $\sigma_i$ 倍，随后 $Qv_i=u_i$ 把拉伸后的轴转到 $u_i$。注意极分解只对方阵成立；矩形矩阵只有 SVD，没有极分解，因为 $m\ne n$ 时 $UV^T$ 不再是方阵上的正交变换。当 $A$ 可逆时，$S$ 正定且 $Q=AS^{-1}$ 唯一；$\det(A)=\det(Q)\det(S)=\pm\prod\sigma_i$ 说明拉伸因子的乘积是体积缩放率，反射只贡献符号。
> 反向顺序 $A=KQ$ 只是换一种括号结合：$A=U\Sigma V^T=(U\Sigma U^T)(UV^T)=KQ$，其中 $K=U\Sigma U^T$ 是 $AA^T$ 的对称平方根。$A=QS$ 是“先在 $v$ 坐标拉伸、再转到输出坐标”；$A=KQ$ 是“先转到输出坐标、再在 $u$ 坐标拉伸”；两者共享同一个 $Q$，因为旋转夹在中间并不改变两端的坐标选择。这个 $S$ 还是唯一的：若 $T$ 半正定且 $T^2=A^TA$，把 $A^TA$ 在 $v$ 基下对角化后，$T$ 的特征值只能是 $\sigma_i$（非负平方根的唯一选择）。从 Strang 的矩阵分解视角，$A=QS$ 与 LU、QR 的分工不同：LU/QR 服务消元与正交化，极分解服务几何解释，三者在各自舞台上把“形状”与“动作”分离。
> 与复数极形式 $z=re^{i\theta}$ 的类比不是比喻而是同构：$r=|z|=\sqrt{\bar z z}$ 对应 $S=(A^TA)^{1/2}$，$e^{i\theta}=z/|z|$ 对应 $Q=AS^{-1}$（可逆时）。$1\times1$ 情形下正交矩阵只能是 $\pm1$ 或 $e^{i\theta}$，半正定矩阵只能是 $r\ge0$，极分解逐字退化为 $z=re^{i\theta}$。
> 用本页例题验证：$A=\begin{bmatrix}3&0\\4&5\end{bmatrix}$，$A^TA=\begin{bmatrix}25&20\\20&25\end{bmatrix}$，奇异值为 $3\sqrt5$ 与 $\sqrt5$，主轴 $v_1=(1,1)/\sqrt2$。$S=\sqrt5\begin{bmatrix}2&1\\1&2\end{bmatrix}$ 把单位圆沿 $v_1$ 拉长到 $3\sqrt5$、沿 $v_2$ 拉长到 $\sqrt5$，得长短轴比 $3$ 的椭圆；$Q=\frac1{\sqrt5}\begin{bmatrix}2&-1\\1&2\end{bmatrix}$ 是 $\cos\theta=2/\sqrt5$ 的纯旋转（$\theta\approx26.6^\circ$），把椭圆整体转过去。把数值代回验证：$S^2=5\begin{bmatrix}2&1\\1&2\end{bmatrix}^2=5\begin{bmatrix}5&4\\4&5\end{bmatrix}=\begin{bmatrix}25&20\\20&25\end{bmatrix}=A^TA$，且 $Q^TQ=I$。验证顺序：$(QS)v_1=Q(\sigma_1 v_1)=\sigma_1 u_1=Av_1$；若先施 $Q$ 再施 $S$，$S(Qv_1)$ 一般不等于 $Av_1$，拉伸与旋转不可交换。形状信息全在 $\Sigma$，$Q$ 只负责摆放。从椭球几何看，$S$ 决定半轴长度与主轴方向，$Q$ 决定椭球在空间中的摆放姿态；两者各司其职，互不替代，这正是极分解作为几何工具的价值。
> 这也解释 $Q$ 是离 $A$ 最近的正交矩阵（§IV.9 Procrustes）：用酉不变性把 $\min_Z\|A-Z\|_F$ 化为 $\min_W\|\Sigma-W\|_F$（$W=U^TZV$）。展开 $\|\Sigma-W\|_F^2=\sum\sigma_i^2+n-2\sum\sigma_i w_{ii}$；正交矩阵每列模长为 $1$，故 $|w_{ii}|\le1$，这是 Cauchy-Schwarz 的坐标版（分量不超过列长）。因 $\sigma_i\ge0$，最大化交叉项要求每个 $w_{ii}=1$，再由列模长为 $1$ 迫使该列其余分量为零，$W=I$，故 $Z=UV^T=Q$。这里用到的酉不变性正是后文 page_077 三种范数注的同一个性质，它把几何优化化简为对角优化。
> 跨课程连接：这个最近正交矩阵正是计算机视觉中刚性运动估计的解。给定两片已配准的点集，令 $H=\sum x_i y_i^T$ 为交叉协方差矩阵，对 $H$ 做 SVD 得 $H=U\Sigma V^T$，使 $\sum\|Qx_i-y_i\|^2$ 最小的旋转是 $Q=UV^T$；若 $\det(UV^T)$ 为负还需做一步反射修正。这不是新算法，而是把 Procrustes 优化从矩阵套用到点集：SVD 从带噪声的测量中剥离纯旋转。力学同理，变形梯度的极分解把局部旋转与局部拉伸分开，材料本构只依赖拉伸部分。
> 一句话收束：SVD 把矩阵拆成“换坐标—缩放—换回坐标”，极分解把前后两个坐标变换粘成一个正交变换，于是任何线性变换都是先拉伸、后旋转。
---


---

<!-- page 073: 书页 68, Problem Set 1.8 (题 1-9) -->

# Strang LaLFD Part I（线性代数与从数据中学习）

---

<span style="color:#2471a3;">**[exercise]**</span> **Problem Set 1.8（习题集 1.8）**——奇异值与奇异向量（Singular Values and Singular Vectors in the SVD）· 本页保留英文原文，不翻译。

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.**
A symmetric $S = S^T$ has $n$ orthonormal eigenvectors $x_1$ to $x_n$. Then any vector $c$ can be written as a combination $c = c_1 x_1 + \cdots + c_n x_n$. Explain these two formulas:

```math
c^Tc = c_1^2 + \cdots + c_n^2
\qquad \text{and} \qquad
c^TSc = c_1^2\lambda_1 + \cdots + c_n^2\lambda_n
```

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.**
Problem 1 gives a neat formula for the Rayleigh quotient $c^TSc/c^Tc$. Why is the maximum value of that ratio equal to the largest eigenvalue $\lambda_1$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.**
This may be the simplest way to understand the "second construction" of the SVD in equation (15). You can see why the ratio $R(c)$ is a maximum when $c_1 = 1$ and $c_2 = c_3 = \cdots = 0$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.**
Next comes $\lambda = \lambda_2$. We maximize $R(c)$ subject to the condition that $c_1 = 0$. Does $c_2 = 1$ and $c_1 = c_3 = \cdots = 0$ do it? Why is the ratio in Problem 2 now maximized when $c_2 = 1$ and $c_1 = c_3 = \cdots = 0$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.**
Following Problem 3, what is solved by $\lambda = \lambda_3$? The best $c$'s are $c_1 = c_2 = 0$ and $c_3 = 1$ and $c_4 = \cdots = 0$.

> <span style="color:#1e8449;">译者注：本题 "best c's" 的具体写法（$c_1 = c_2 = 0,\ c_3 = 1,\ c_4 = \cdots = 0$）依据题解与上下文重建；原书 OCR 在该处有乱码（"一 1 and CI C2 = C4"）。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.**
The maximum of $R(c) = c^TSc/c^Tc$ is $\lambda_3$ subject to what two conditions on $c$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.**
Show that $A^T$ has the same (nonzero) singular values as $A$. Then $\|A^T\| = \|A\|$ for all matrices. But it's not true that $\|Ax\| = \|A^Tx\|$ for all vectors. That needs $A^TA = AA^T$.

> <span style="color:#1e8449;">译者注：句末 "That needs $A^TA = AA^T$" 依据数学上下文重建（对 normal matrix（正规矩阵）$A$，$\|Ax\| = \|A^Tx\|$ 才对一切 $x$ 成立）；原书 OCR 在此处截断。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.**
Find the $\sigma$'s and $v$'s and $u$'s in the SVD for $A = \begin{bmatrix}3 & 4\\ 0 & 5\end{bmatrix}$. Use equation (12). What is the norm $\|A\|$ when that largest rank one piece of $A$ is removed? What are the singular values of this reduced matrix, and its rank?

> <span style="color:#1e8449;">译者注：题中矩阵为 Example 1 中 $A = \begin{bmatrix}3 & 0\\ 4 & 5\end{bmatrix}$ 的 transpose（转置）$\begin{bmatrix}3 & 4\\ 0 & 5\end{bmatrix}$（奇异值仍为 $\sqrt{45}$ 与 $\sqrt{5}$，但 $u$'s 与 $v$'s 互换）；原书 OCR 中矩阵本身缺失，依据题解重建。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.**
Find the $\sigma$'s and $v$'s and $u$'s, and verify that

```math
A = \begin{bmatrix}0 & 2 & 0\\ 0 & 0 & 3\\ 0 & 0 & 0\end{bmatrix} = U\Sigma V^T
```

For this $A$, the orthogonal matrices $U$ and $V$ are permutation matrices.

---

<!-- page 074: 书页 69, Problem Set 1.8 (题 9 续 + 题 10-13) -->

<span style="color:#2471a3;">**[exercise]**</span> **Problem Set 1.8（续）**——奇异值与奇异向量（Singular Values and Singular Vectors in the SVD）· 保留英文原文，不翻译。

<span style="color:#2471a3;">**[problem]**</span> **Problem 9（续，上一页）**
Once again max $R(c) = \lambda_1$. The maximum is exactly $\lambda_1$ when $Sc = \lambda_1 c$.

> <span style="color:#1e8449;">译者注：本句为 Problem 9 的收尾部分（续上一页矩阵 $A = \begin{bmatrix}0 & 2 & 0\\ 0 & 0 & 3\\ 0 & 0 & 0\end{bmatrix}$ 的 SVD 验证），重申 Rayleigh quotient（瑞利商）的最大值恰在 $Sc = \lambda_1 c$（即 $c$ 取 $S$ 的特征向量 $x_1$）时达到。</span>

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.**
Prove $\|B\| \le \|A\|$ in (22). Remove $N - n$ columns of $A$ to produce $C$: $C$ has $\|C\| \le \|A\|$. (Why?) Transpose $C$, no change in norm. Finally remove $M - m$ columns of $C^T$ to produce $B^T$. Altogether

```math
\|B\| = \|B^T\| \le \|C^T\| = \|C\| \le \|A\|
```

> <span style="color:#1e8449;">译者注：本题的证明步骤在 OCR 中残缺（"C has $\|C\| \le \|A\|$. (Why?)"、"…columns of $C^T$ to produce $B^T$" 等为可辨片段），中间句按题解与 equation (22) 的论证重建：先删 $A$ 的 $N-n$ 列得 $C$，转置范数不变，再删 $C^T$ 的 $M-m$ 列得 $B^T$，最终 $\|B\| = \|B^T\| \le \|C^T\| = \|C\| \le \|A\|$。</span>

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 11.**
Check that the trace of

```math
S = \begin{bmatrix}0 & A\\ A^T & 0\end{bmatrix}
```

from adding up its diagonal entries agrees with the sum of its eigenvalues in equation (21). If $A$ is a square diagonal matrix, what are the $2n$ eigenvalues and eigenvectors of $S$?

> <span style="color:#1e8449;">译者注：题 11 的 $S$ 即 equation (21) 中的 block matrix（block matrix，对角块全零，特征值成对 $\pm\sigma_k$，故迹为零、特征值之和为零）；"the $2n$ eigenvalues" 中的 $n$ 在 OCR 中缺失，据上下文补全。</span>

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 12.**
Find the SVD of the rank 1 matrix $A = \begin{bmatrix}1 & 2\\ 2 & 4\end{bmatrix}$. Factor $A^TA$ into $Q\Lambda Q^T$.

> <span style="color:#1e8449;">译者注：题 12 的 rank-1 矩阵在 OCR 中缺失，据题解中 $A^TA = \begin{bmatrix}5 & 10\\ 10 & 20\end{bmatrix}$ 反推为 $A = \begin{bmatrix}1 & 2\\ 2 & 4\end{bmatrix}$。</span>

---

<span style="color:#2471a3;">**[problem]**</span> **Problem 13.**
Here is my homemade proof of the SVD. Step 2 uses the factorizations $A^TA = V\Lambda V^T$ and $AA^T = U\Lambda U^T$ (same eigenvalues in $\Lambda$).

```math
1.\quad A^TA = V\Lambda V^T
```

```math
2.\quad AA^T = U\Lambda U^T
```

```math
3.\quad A = U\Sigma V^T
```

```math
4.\quad U^TAV \ \text{must be diagonal}
```

Step 3 multiplied Step 2 on the left by $U^T$ and on the right by $V$. Then the matrix $U^TAV$ commutes with the diagonal matrix $\Lambda$ in Step 3. How does this force the matrix $U^TAV = \Sigma$ to be also a diagonal matrix? Try 3 by 3:

```math
D\Lambda =
\begin{bmatrix}d_{11} & d_{12} & d_{13}\\ d_{21} & d_{22} & d_{23}\\ d_{31} & d_{32} & d_{33}\end{bmatrix}
\begin{bmatrix}\lambda_1 & 0 & 0\\ 0 & \lambda_2 & 0\\ 0 & 0 & \lambda_3\end{bmatrix}
=
\begin{bmatrix}\lambda_1 & 0 & 0\\ 0 & \lambda_2 & 0\\ 0 & 0 & \lambda_3\end{bmatrix}
\begin{bmatrix}d_{11} & d_{12} & d_{13}\\ d_{21} & d_{22} & d_{23}\\ d_{31} & d_{32} & d_{33}\end{bmatrix}
= \Lambda D
```

Compare the first rows. When can you conclude that $d_{12} = 0$ and $d_{13} = 0$? This shows the limitation on my proof: [it needs] the eigenvalues [of $A^TA$] to be distinct.

The same bug appears in simple proofs of the spectral theorem $S = Q\Lambda Q^T$. This is easy when $S$ has no repeated $\lambda$'s. The SVD is easy when $A$ has no repeated $\sigma$'s. Both $S = Q\Lambda Q^T$ and $A = U\Sigma V^T$ remain [true] when $\lambda$'s or $\sigma$'s happen to be repeated. The problem is that this produces a whole plane of eigenvectors or singular vectors. You have to choose the singular vectors specifically as $u_k = Av_k/\sigma_k$, which is the real proof in equation (9).

> <span style="color:#1e8449;">译者注：题 13 的四步结构在 OCR 中严重乱码（"1 似 T 啕 / 2 A T = UA UT / 3 A ： A / 4 UT 风 must be diagonal"），公式按题解与 equation (9)（$u_k = Av_k/\sigma_k$）重建；"the eigenvalues [of $A^TA$] to be distinct" 即题解所说的非重复（non repeated）特征值条件。</span>

---

<!-- page 075: 书页 70, Problem Set 1.8 (续) -->

<span style="color:#2471a3;">**[section]**</span> **Problem Set 1.8**（续）——本页习题围绕 SVD 的自由参数计数、SVD 与 eigenvalue（特征值）/eigenvector（特征向量）的联系、以及 reduced SVD（约化 SVD）的验证。

<span style="color:#2471a3;">**[problem]**</span> **Problem 14.**
Figure I.10 showed how a 2 by 2 matrix with four entries $a, b, c, d$ produces an SVD with 4 parameters $\sigma_1, \sigma_2, \theta, \phi$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 15.**
Move to $A = U\Sigma V^T =$ 2 by 3 with six entries. How many $\sigma$'s for a 2 by 3 matrix? Then $U$ (2 by 2) only needs one angle. After recovering that, that leaves how many angles for the 3 by 3 orthogonal matrix $V$? The row space of $A$ is a plane in $\mathbb{R}^3$. It takes two angles for the position of that plane. Then one angle in the plane to find $v_1$ and $v_2$. A total of three angles for $V$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 16.**
Every 3 by 3 matrix has 9 entries. So $U\Sigma V^T$ must have 9 parameters. How many parameters in $U$ and $\Sigma$ and $V$? Answer: 3 for $U$, 3 for $\Sigma$, and 3 for $V$. How many parameters describe a rotation in 4-dimensional space?

<span style="color:#2471a3;">**[problem]**</span> **Problem 17.**
$n$ numbers will give the direction of a unit vector $v_1$ in $\mathbb{R}^n$. Then the direction of an orthogonal unit vector $v_2$ takes $n - 1$ numbers. How many for $v_3, v_4, \ldots, v_n$? Total: $n(n-1)/2$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 18.**
If $A = U\Sigma V^T$ is square and invertible, then $A^{-1} = V\Sigma^{-1}U^T$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 19.**
If $v$ is an eigenvector of $A^T A$ with eigenvalue $\sigma^2$, then $u = Av/\sigma$ is an eigenvector of $AA^T$ (not of $A$).

<span style="color:#2471a3;">**[problem]**</span> **Problem 20.**
Find all singular values of ...

> <span style="color:#1e8449;">译者注：此题的矩阵部分在原 OCR 文本中缺失，无法恢复原题给出的具体矩阵。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 21.**
If $S = S^T$ has orthogonal columns $q_1, q_2, q_3$ in $\mathbb{R}^3$ of lengths $2, 3, 4$, find its SVD.

<span style="color:#2471a3;">**[problem]**</span> **Problem 22.**
The reasons for the success of eigenvalues and eigenvectors are in $A^k = X\Lambda^k X^{-1}$. (a) The eigenvalues of $A^k$ are $\lambda_i^k$. (b) An eigenvector of $A$ is also an eigenvector of $A^k$. Show that (a) and (b) are false for singular values and singular vectors of $A^k$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 23.**
Show that the singular values of $A^T$ are the same as the singular values of $A$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 24.**
Equation (5) is $A = U\Sigma V^T$. Multiply by $V$ to get $AV = U\Sigma$ (reduced SVD). For that step we cannot use $V^T V = I$ (which is false when $m > r$). Show instead that this matrix $A = U_r \Sigma_r V_r^T$ satisfies equation (1).

<span style="color:#2471a3;">**[problem]**</span> **Problem 25.**
Show that an $m$ by $n$ matrix of rank $r$ has $r(m + n - r)$ free parameters in its SVD. $A = U\Sigma V^T = (m \times r)(r \times r)(r \times n)$. Why do orthonormal vectors in $\mathbb{R}^m$ have $(m - 1) + (m - 2) + \cdots + (m - r)$ parameters? Another approach uses $A = CR = (m \times r)(r \times n)$ in Section 1.1. The matrix $C$ contains an $r$ by $r$ identity matrix, removing parameters from $rm + rn$. That count is repeated in an appendix of this book.

---

<!-- page 076: 书页 71, §I.9 Principal Components and the Best Low Rank Matrix -->

### I.9 Principal Components and the Best Low Rank Matrix（§I.9 主成分与最佳低秩矩阵）

<span style="color:#2471a3;">**[section]**</span> 矩阵 $A$ 的 principal components（主成分）就是它的 singular vectors（奇异向量），即正交矩阵 $U$ 与 $V$ 的列 $u_j$ 和 $v_j$。主成分分析（Principal Component Analysis, PCA）利用与最前面几个 $u$、$v$ 相连的最大奇异值 $\sigma$，来理解一个数据矩阵（matrix of data）中的信息。

给定了矩阵 $A$，我们提取它最重要的部分（最大的那些 $\sigma$）：

```math
A_k = \sigma_1 u_1 v_1^T + \cdots + \sigma_k u_k v_k^T
\qquad \text{且} \qquad \text{rank}(A_k) = k
```

$A_k$ 求解的是一个矩阵优化问题——我们就从这里开始。最接近 $A$ 的 rank $k$ matrix（秩 $k$ 矩阵）就是 $A_k$。在统计学中，我们是在识别 $A$ 中具有最大 variance（方差）的那些分量。这把 SVD 放到了 data science（数据科学）的中心。

在那个世界里，PCA 是 unsupervised learning（无监督学习）。我们唯一的指导者是 linear algebra（线性代数）——SVD 告诉我们要选择 $A_k$。当学习是 supervised（有监督的）时，我们有一大组 training data（训练数据）。深度学习（Deep Learning，见 Section VII.I）构造一个（非线性的！）函数 $F$，它能正确分类大部分训练数据。然后我们把 $F$ 应用到新数据上，这一点你稍后就会看到。

---

主成分分析（Principal Component Analysis）建立在用 $A_k$ 对矩阵作近似的基础上。$A_k$ 是最佳选择这一结论的证明始于 Schmidt（1907）。他的 theorem（定理）原本是为函数空间中的 operators（算子）写的，并且直接推广到向量空间中的矩阵。Eckart 与 Young 在 1936 年给出了一个新的证明（对矩阵使用 Frobenius norm（弗罗贝尼乌斯范数））。随后 Mirsky 在 1955 年找到了一个更一般的证明，它允许任何只依赖于奇异值的范数 $\|\cdot\|$——正如下面的定义 (2)、(3) 和 (4) 那样。

下面是这个特殊的 rank $k$ matrix（秩 $k$ 矩阵）$A_k = \sigma_1 u_1 v_1^T + \cdots + \sigma_k u_k v_k^T$ 的关键性质：

<span style="color:#c0392b;">**Eckart-Young（Eckart-Young 定理）**</span>
如果 $B$ 的秩为 $k$，那么 $\|A - B\| \ge \|A - A_k\|$。（1）

---

矩阵 norm（范数）$\|\cdot\|$ 有三种选择具有特别的重要性，并且各有自己的名称：

- **Spectral norm（谱范数）**：$\|A\|_2 = \max_{\|x\|=1}\|Ax\| = \sigma_1$（常称为 operator norm（算子范数））（2）
- **Frobenius norm（弗罗贝尼乌斯范数）**：$\|A\|_F = \sqrt{\sigma_1^2 + \cdots + \sigma_n^2}$（前文 (12) 与 (13) 也定义了 $\|A\|_F$）（3）
- **Nuclear norm（核范数）**：$\|A\|_* = \sigma_1 + \sigma_2 + \cdots + \sigma_n$（即 trace norm（迹范数））（4）

这些范数对 $2 \times 2$ 的单位矩阵（identity matrix）就已经有不同的值：$\|I\|_2 = 1$、$\|I\|_F = \sqrt{2}$、$\|I\|_* = 2$。（5）

把 $I$ 换成任意 orthogonal matrix（正交矩阵）$Q$，这些范数保持不变（因为所有 $\sigma$ 都等于 1）：$\|Q\|_F = \|I\|_F$，$\|Q\|_2 = 1$。

不仅如此，任何矩阵 $A$ 的 spectral norm（谱范数）、Frobenius norm（弗罗贝尼乌斯范数）和 nuclear norm（核范数），在 $A$ 与一个正交矩阵相乘（无论在哪一侧）后都保持不变。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 三种范数共享的深层性质是酉不变性：$\|Q_1AQ_2\|=\|A\|$。第一性原理：$Q_1AQ_2=(Q_1U)\Sigma(V^TQ_2)$，而 $Q_1U$ 与 $Q_2^TV$ 仍是正交矩阵，所以左右乘正交矩阵只是换一组奇异向量，$\Sigma$ 不动。奇异值向量 $(\sigma_1,\ldots,\sigma_n)$ 是矩阵在正交等价下的形状指纹，任何只依赖它的对称函数都自动酉不变。谱范数读最大分量，Frobenius 读平方和的平方根，核范数读总和——三种读法从同一指纹提取不同信息。
> 三者构成链 $\sigma_1\le\sqrt{\sum\sigma_i^2}\le\sum\sigma_i$，即把 $\ell_\infty$、$\ell_2$、$\ell_1$ 依次作用于奇异值向量。两个不等号都可用脚手架验证：第一个平方后是 $\sigma_1^2\le\sum\sigma_i^2$；第二个平方后化为 $\sum\sigma_i^2\le(\sum\sigma_i)^2=\sum\sigma_i^2+2\sum_{i<j}\sigma_i\sigma_j$，交叉项非负。反向界也可以用 Cauchy-Schwarz 直接得到：$\|A\|_*=\langle\sigma,\mathbf1\rangle\le\|\sigma\|_2\|\mathbf1\|_2=\sqrt n\,\|A\|_F$，其中 $\mathbf1$ 是全 1 向量；等号当且仅当 $\sigma$ 与 $\mathbf1$ 平行，即所有奇异值相等，与下面的方差论证一致。
> 用均值—方差把三者读清楚：设 $\mu=\|A\|_*/n$ 为奇异值均值，则 $\|A\|_F^2=n(\mu^2+\operatorname{Var}(\sigma))$。核范数只读总数（均值），Frobenius 额外读出奇异值的离散程度，谱范数读最大值。于是链 $\sigma_1\le\|A\|_F\le\|A\|_*$ 读作“最大半轴不超过能量平方根，能量平方根不超过总拉伸量”。6.042J 的方差非负 $E[\sigma^2]\ge(E[\sigma])^2$ 给出 $(\sum\sigma_i)^2\le n\sum\sigma_i^2$，与 Cauchy-Schwarz 是同一个事实的两种写法。若 $A$ 秩为 1，则只有一个非零奇异值，三种范数重合为该值；这验证了链在退化情形的紧性。与上页极分解相扣：对方阵 $A=QS$，$S$ 的特征值恰是奇异值，所以 $\operatorname{tr}(S)=\|A\|_*$、$\operatorname{tr}(S^2)=\|A\|_F^2$——核范数与 Frobenius 范数正是在读拉伸因子的一次幂和与二次幂和。
> 核范数的特殊地位在于它是秩的凸替代。秩 = 非零奇异值的个数（对 $\sigma$ 向量做 $\ell_0$ 计数），核范数 = $\sum\sigma_i$（$\ell_1$）。秩是离散阶梯：每删掉一个奇异值目标函数跳变一格，既不凸也不连续，直接优化不可行；而核范数在每个方向上线性增长。一维直觉：阶梯 $f(x)=1$（$x\ne0$）、$f(0)=0$ 在 $[-1,1]$ 上的最大凸下界是 $|x|$——任何低于它的凸函数都被端点弦压在 $|x|$ 之下，而 $|x|$ 本身凸且不超过 $f$。于是矩阵补全（§IV.3）中直接最小化秩不可行时，用核范数做凸松弛：保持可优化性，又鼓励奇异值稀疏；这正是压缩感知用 $\ell_1$ 替代 $\ell_0$ 的矩阵版。高维情形：核范数是秩函数在单位球上的凸包络（所有不超过 $\operatorname{rank}$ 的凸函数中的最大者）；证明不能靠一维图，但思想一致——沿每个奇异值方向，秩的跳变被 $\ell_1$ 的线性增长从下方贴住。
> 这些范数正是 Eckart-Young 定理（page_076 上方）在三种度量下的目标函数：用 $A_k$ 近似时，误差的三种范数分别是截尾奇异值向量 $(\sigma_{k+1},\ldots,\sigma_n)$ 的对应读数。所以 Mirsky 的统一证明不是三种巧合，而是同一个“截尾后读数”机制在三种范数下的自然结果。
> 这一节也接上 TBB 的范数论：先对奇异值向量取向量范数，再定义为矩阵范数，酉不变性保证定义不依赖基；链与反向界就是 $\mathbb{R}^n$ 上三种范数等价性的显式常数。验算两个具体对象：$I_2$ 给出 $\|I\|_2=1$、$\|I\|_F=\sqrt2$、$\|I\|_*=2$；$\operatorname{diag}(3,4)$ 给出 $\|A\|_2=4$、$\|A\|_F=5$、$\|A\|_*=7$，链 $4\le5\le7$ 成立。
> 一句话收束：谱范数看最强方向，Frobenius 看整体能量，核范数看总拉伸量；三者都是奇异值指纹的忠实读数，而核范数是唯一能凸地“替代”秩的读数。
---


---

<!-- page 077: 书页 72, §I.9 Principal Components and the Best Low Rank Matrix -->
# Strang LaLFD Part I（线性代数与从数据中学习）

> <span style="color:#7f8c8d;">**Highlights of Linear Algebra**</span>

奇异值在 $U$ 与 $V$ 分别变为 $Q_1U$ 和 $Q_2V$ 时保持不变。对复矩阵，orthogonal（正交）一词由 unitary（酉）取代，于是 $Q^TQ = I$。

这三种范数——spectral norm（谱范数）、Frobenius norm（弗罗贝尼乌斯范数）与 nuclear norm（核范数）——都是 unitarily invariant（酉不变）的：$\|Q_1 A Q_2\| = \|A\|$。Mirsky 对公式 (1) 中 Eckart-Young 定理的证明适用于一切酉不变范数：$\|A\|$ 可以由奇异值 $\sigma_i$ 计算出来。

三种范数对任意正交的 $Q_1$、$Q_2$ 都有 $\|Q_1 A Q_2^T\| = \|A\|$（7）。我们现在为 L2 范数和 Frobenius 范数给出公式 (1) 的更简单证明。

---

### <span style="color:#c0392b;">Eckart-Young Theorem: Best Approximation by $A_k$（Eckart-Young 定理：用 $A_k$ 的最佳逼近）</span>

<span style="color:#2471a3;">**[theorem]**</span> 在着手证明之前，先看看这个定理告诉我们什么是很有帮助的。在这个例子中，$A$ 是对角矩阵且 $k = 2$：

```math
A = \begin{pmatrix} 4&0&0&0\\ 0&3&0&0\\ 0&0&2&0\\ 0&0&0&1 \end{pmatrix}
```

最接近 $A$ 的秩 2 矩阵为

```math
A_2 = \begin{pmatrix} 4&0&0&0\\ 0&3&0&0\\ 0&0&0&0\\ 0&0&0&0 \end{pmatrix}
```

这必然成立！你可能会说这个对角矩阵太简单了，不具有典型性。

但矩阵变成 $Q_1 A Q_2^T$（对任意正交的 $Q_1$、$Q_2$）时，L2 范数和 Frobenius 范数都不会改变。所以这个例子涵盖了任何奇异值为 4、3、2、1 的 4×4 矩阵。

根据 Eckart-Young 定理，我们要保留 4 和 3，因为它们最大。L2 范数下的误差是 $\|A - A_2\| = 2$，而 Frobenius 范数给出 $\|A - A_2\|_F = \sqrt{5}$。

---

这个问题的棘手之处在于"秩 2 矩阵"。秩 2 矩阵的集合不是 convex（凸）的。

两个秩 2 矩阵 $B_1$、$B_2$ 的平均可以很容易地具有秩 4。这个 $B_2$ 有没有可能比 $A_2$ 更接近 $A$？这个 $B_2$ 会不会是 $A$ 的更好的秩 2 逼近？

```math
B_2 = \begin{pmatrix} 3.5&3.5&0&0\\ 3.5&3.5&0&0\\ 0&0&1.5&1.5\\ 0&0&1.5&1.5 \end{pmatrix}
```

在 $A - A_2$ 有误差 2 和 1 的地方，$A - B_2$ 在主对角线上的误差只有 0.5。当然，非对角线上的误差 3.5 和 1.5 会太大。

但也许还存在另一个比 $A_2$ 更好的选择？不，$A_2$ 是最佳的。

我们为 L2 范数证明这一点，然后再为 Frobenius 范数证明。

---

### <span style="color:#2471a3;">Eckart-Young（L2 范数）</span>

<span style="color:#2471a3;">**[theorem]**</span> 如果矩阵 $B$ 的 rank（秩）不超过 $k$，那么 L2 范数下的误差至少是 $\sigma_{k+1}$：

```math
\mathrm{rank}(B) \le k \quad \Longrightarrow \quad \|A - B\|_2 \ge \sigma_{k+1} \qquad (8)
```
> <span style="color:#7f8c8d;">Strang §I.9, p.72</span>

---

<!-- page 078: 书页 73, §I.9 Principal Components and the Best Low Rank Matrix -->

> <span style="color:#7f8c8d;">**§I.9 Principal Components and the Best Low Rank Matrix**（书页 73）</span>

我们知道 $\|A - A_k\| = \sigma_{k+1}$。$\|A - B\| \ge \sigma_{k+1}$ 的整个证明依赖于在计算范数 $\|A - B\|$ 时对向量 $c$ 的巧妙选择：

```math
\text{选取 } c \text{ 使得 } Bc = 0，\text{ 且 } c = c_1 v_1 + c_2 v_2 + \cdots + c_{k+1} v_{k+1} \qquad (9)
```

首先，$B$ 的 nullspace（零空间）的维数是 $n - k$，因为 $B$ 的秩为 $k$。其次，$v_1$ 到 $v_{k+1}$ 的所有组合产生一个维数为 $k + 1$ 的子空间。

这两个子空间必然相交！当维数相加得到 $(n - k) + (k + 1) = n + 1$ 时，两个子空间必然（至少）共有一条直线。想一想 $\mathbb{R}^3$ 中过 $(0, 0, 0)$ 的两个平面——它们共有一条直线，因为 $2 + 2 > 3$。在这条直线上选取一个非零向量 $c$。

用这个 $c$ 来估计公式 (8) 中的范数 $\|A - B\|$。记住 $Bc = 0$，而 $Ac = \sigma_1 c_1 u_1 + \cdots + \sigma_{k+1} c_{k+1} u_{k+1}$，所以下列式子正是 $\|(A - B)c\|^2 = \|Ac\|^2$：

```math
\|(A - B)c\|^2 = \sigma_1^2 c_1^2 + \sigma_2^2 c_2^2 + \cdots + \sigma_{k+1}^2 c_{k+1}^2 \qquad (10)
```

由于 $\sigma_1 \ge \cdots \ge \sigma_{k+1}$，这个和至少与 $(\sigma_{k+1} c_1)^2 + \cdots + (\sigma_{k+1} c_{k+1})^2 = \sigma_{k+1}^2(c_1^2 + \cdots + c_{k+1}^2) = \sigma_{k+1}^2\|c\|^2$ 一样大。这就证明了 $\|(A - B)c\| \ge \sigma_{k+1}\|c\|$。

这就给出了我们想要的 $\|A - B\|$：

```math
\|A - B\|_2 \ge \frac{\|(A - B)c\|}{\|c\|} \ge \sigma_{k+1} \qquad (11)
```

证毕！公式 (11) 表明对任何秩不超过 $k$ 的 $B$ 都有 $\|A - A_k\| = \sigma_{k+1} \le \|A - B\|$，也就是说 $A_k$ 是最佳逼近。

> <span style="color:#1e8449;">译者注：此句在 OCR 中残缺不清，此处按数学上下文补全为"公式 (11) 表明 $A_k$ 是最佳逼近"。</span>

---

### The Frobenius Norm（弗罗贝尼乌斯范数）

<span style="color:#2471a3;">**[section]**</span> 现在我们转向 Frobenius 范数，以证明 $A_k$ 在那里也是最佳逼近。

看看这个范数的三种不同公式是有用的。第一个公式把 $A$ 的元素排成一个长向量，并取该向量的通常范数。第二个公式注意到 $A^TA$ 的主对角线包含 $A$ 每一列的范数（的平方）。例如，$A^TA$ 的 1,1 元是来自第 1 列的 $|a_{11}|^2 + \cdots + |a_{n1}|^2$。

```math
\|A\|_F^2 = |a_{11}|^2 + |a_{12}|^2 + \cdots + |a_{1n}|^2 + |a_{21}|^2 + \cdots \qquad (12)
```

所以公式 (12) 与公式 (13) 是一样的，我们只是逐列累加数字 $|a_{ij}|$。

```math
\|A\|_F^2 = \text{trace of } A^TA = (A^TA)_{11} + (A^TA)_{22} + \cdots + (A^TA)_{nn} \qquad (13)
```

然后公式 (14) 给出的 Frobenius 范数使用 $A^TA$ 的特征值 $\lambda_i$（trace（迹）总是等于特征值之和）。公式 (14) 也直接来自 SVD——$A = U\Sigma V^T$ 的 Frobenius 范数不受 $U$ 和 $V$ 的影响，所以 $\|A\|_F = \|\Sigma\|_F$。

这就是 $\sigma_1^2 + \sigma_2^2 + \cdots + \sigma_n^2$：

```math
\|A\|_F^2 = \sigma_1^2 + \sigma_2^2 + \cdots + \sigma_n^2 \qquad (14)
```




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 先把这个证明的引擎拆开看：目标是给任意秩不超过 $k$ 的竞争者 $B$ 一个无法逃避的下界 $\|A-B\|_2 \ge \sigma_{k+1}$。策略模板可以命名为**维数对撞法**——构造两个子空间，让它们的维数之和超过外围空间的维数，从而迫使交集非平凡。第一个子空间是 $\ker(B)$。由秩-零化度定理，$B$ 有 $n$ 列且秩 $\le k$，所以 $\dim \ker(B) = n - \operatorname{rank}(B) \ge n-k$。第二个子空间是前 $k+1$ 个右奇异向量张成的 $V_{k+1} = \operatorname{span}\{v_1,\ldots,v_{k+1}\}$，维数为 $k+1$。两者相加 $(n-k)+(k+1) = n+1 > n$，于是交集中存在非零向量 $c$。这是 6.042J 鸽巢原理的线性代数版：把 $n$ 维空间想象成 $n$ 个房间，两个子空间分别占了至少 $n-k$ 个和 $k+1$ 个自由度，自由度总数超过房间数，必然有重叠。
> 维数对撞的算术可以一般化：对任意两个子空间 $U,W$，有 $\dim(U\cap W)\ge\dim U+\dim W-n$，这来自 $\dim(U+W)\le n$ 与 $\dim(U+W)=\dim U+\dim W-\dim(U\cap W)$ 两式相消，与容斥原理同形。Eckart-Young 的构造正是让两项维数之和等于 $n+1$，逼出至少一维的交集。
> 关键在第二步：这个 $c$ 同时满足两个性质，恰好构成对 $B$ 的双重打击。一方面 $c \in \ker(B)$，所以 $(A-B)c = Ac$——误差矩阵在这个方向上完全暴露为 $A$ 本身的作用。另一方面 $c \in V_{k+1}$，而 $A$ 在 $V_{k+1}$ 上的最小增益就是 $\sigma_{k+1}$：把 $c = \sum_{i=1}^{k+1} \alpha_i v_i$ 代入，得 $\|Ac\|^2 = \sum_{i=1}^{k+1} \sigma_i^2 \alpha_i^2 \ge \sigma_{k+1}^2 \sum_{i=1}^{k+1} \alpha_i^2 = \sigma_{k+1}^2 \|c\|^2$。合起来就是 $\|(A-B)c\| = \|Ac\| \ge \sigma_{k+1}\|c\|$，再由算子范数定义 $\|A-B\|_2 = \max_{\|x\|=1}\|(A-B)x\|$ 推出下界。注意论证的优美之处：$B$ 的列空间怎么选、零空间长什么样，我们一概不知道，也不需要知道——无论 $B$ 怎么躲，$V_{k+1}$ 与 $\ker(B)$ 的交都逼出一个见证方向。
> 一个二维思想实验可以让它落地。取 $A = \operatorname{diag}(10, 1)$，则 $\sigma_1 = 10$，$\sigma_2 = 1$，目标是秩 $1$ 逼近，定理断言任何秩 $1$ 矩阵 $B$ 都有 $\|A-B\|_2 \ge 1$。任何秩 $1$ 矩阵的零空间维数至少是 $2-1=1$，即一条过原点的直线。而 $V_2 = \operatorname{span}\{v_1,v_2\} = \mathbb{R}^2$，交就是 $\ker(B)$ 本身。若 $B$ 的零空间恰好是 $v_2$ 轴，则取 $c = v_2$，$\|(A-B)c\| = \|Av_2\| = 1$；若 $B$ 的零空间是别的直线，与 $V_2$ 的交仍非零，取其上单位向量 $c$，它在 $v_1$ 方向必有非零分量，于是 $\|Ac\| \ge 1$。B 无法同时杀掉$v_1$ 和 $v_2$ 两个方向，这就是维数对撞的实质。
> 三维版本把直觉放得更大：$A=\operatorname{diag}(10,5,1)$，$k=1$，断言任何秩 $1$ 的 $B$ 都有 $\|A-B\|_2\ge5$。此时 $\ker(B)$ 是至少二维的平面，$V_2=\operatorname{span}\{v_1,v_2\}$ 是 $v_1v_2$ 平面；三维空间中两个平面必交于至少一条直线，任取交线上的单位向量 $c$，则 $Bc=0$ 且 $\|Ac\|\ge5\|c\|$，下界成立。
> 为什么 $V_{k+1}$ 上 $A$ 的最小增益恰是 $\sigma_{k+1}$？因为 $Av_i=\sigma_i u_i$ 且 $u_i$ 相互正交，$A$ 把 $V_{k+1}$ 映到 $U_{k+1}$ 上是一个对角线性映射，限制在这个子空间上的最小奇异值就是 $\sigma_{k+1}$。当 $k=\min(m,n)$ 时 $\sigma_{k+1}$ 不存在，定理退化为平凡结论：可取 $B=A$，误差为零。
> 与 CLRS 的连接值得精确化。原注把 §8.1 的比较排序下界称为对手论证，严格说 §8.1 用的是**决策树计数**（$n!$ 个叶子迫使深度 $\ge \log_2(n!)$），它是计数型下界；更地道的对手论证在 CLRS §9.1——同时求最小与最大元素的 $\lceil 3n/2 \rceil - 2$ 比较下界：对手不事先选定输入，而是根据算法的每次比较临时维护一个与所有已回答结果兼容的输入状态，最终证明任何算法都必须做足次数。两种模板的共同点是**非构造性**：维数对撞不构造 $c$，对手论证不构造具体最坏输入，它们只证明存在。这恰好是你熟悉的 6.042J 存在性证明策略在算法下界中的两次现身：一次在向量空间里数维数，一次在输入状态里数可能性。
> 一句话收束：所谓漂亮不是修辞，而是同一个鸽巢原理——自由度的和超过总自由度——在矩阵零空间与算法信息状态上的两次成功投注。
---


---

<!-- page 079: 书页 74, §I.9：Eckart-Young in the Frobenius Norm -->

### Eckart-Young in the Frobenius Norm（Frobenius 范数下的 Eckart-Young）

<span style="color:#2471a3;">**[proof]**</span> 对于 norm（范数）$\|A\|_F$，Pete Stewart（皮特·斯图尔特）发现并慷慨地分享了下面这个简洁的证明。

假设 rank（秩）为 $r$ 的矩阵 $B$ 是最接近 $A$ 的矩阵。我们想要证明 $B = A_r$。

出人意料的是，我们要从 $B$ 的 singular value decomposition（奇异值分解）入手：

```math
B = U\begin{bmatrix} D & 0 \\ 0 & 0 \end{bmatrix}V^T
\qquad (15)
```

其中 diagonal matrix（对角矩阵）$D$ 是 $r \times r$ 的。

来自 $B$ 的这两个 orthogonal matrices（正交矩阵）$U$ 与 $V^T$ 不一定能把 $A$ diagonalize（对角化）：

```math
U^TAV = \begin{bmatrix} L + E + R & G \\ H & K \end{bmatrix}
\qquad (16)
```

这里 $L$ 在前 $r$ 行内是 strictly lower triangular（严格下三角）的，$E$ 是对角的，而 $R$ 是 strictly upper triangular（严格上三角）的。

步骤 1（Step 1）将证明 $L$、$R$、$H$ 全部为零，做法是把 $A$、$B$ 与下面这个显然秩为 $r$ 的矩阵 $C$ 进行比较：

```math
C = U\begin{bmatrix} L + D + R & 0 \\ H & 0 \end{bmatrix}V^T
\qquad (17)
```

这是 Stewart 的关键想法：构造一个带零列、从而其秩一眼可见的 $C$。正交矩阵 $U$ 与 $V^T$ 保持 Frobenius norm（弗罗贝尼乌斯范数）不变。把所有矩阵元素平方后相加，注意到 $A - C$ 在 $A - B$ 含有矩阵 $L$、$R$、$H$ 的位置上为零：

```math
\|A - B\|_F^2 = \|A - C\|_F^2 + \|L\|_F^2 + \|R\|_F^2 + \|H\|_F^2
\qquad (18)
```

由于 $\|A - B\|_F^2$ 已经尽可能小，我们得知 $L$、$R$、$H$ 为零！类似地，我们还得到 $G = 0$。

此时我们知道 $U^TAV$ 含有两个分块（block），并且 $E$ 是对角的（像 $D$ 一样）：

```math
U^TAV = \begin{bmatrix} E & 0 \\ 0 & K \end{bmatrix}
\qquad\text{以及}\qquad
U^TBV = \begin{bmatrix} D & 0 \\ 0 & 0 \end{bmatrix}
```

如果 $B$ 最接近 $A$，那么 $U^TBV$ 最接近 $U^TAV$。现在我们就看到了结局。矩阵 $D$ 必须与 $E = \text{diag}(\sigma_1, \ldots, \sigma_r)$ 相同。

残差块 $K$ 的奇异值（singular values）必须是 $A$ 的最小的 $m - r$ 个奇异值。最小误差 $\|A - B\|_F$ 必须是：

```math
\|K\|_F = \sqrt{\sigma_{r+1}^2 + \cdots + \sigma_m^2} = \text{Eckart-Young}
```

在本节开头的 4 by 4（$4 \times 4$）例子中，$A_2$ 是最优的：$\|A - A_2\|_F = \sqrt{5}$。

对 non-convex optimization（非凸优化）问题来说，拥有这种 explicit solution（显式解）是极为罕见的。

---

> <span style="color:#1e8449;">**译者注**</span>：方程 (17) 中的 $C$ 保留了左下分块 $H$，使得 $A - C$ 在左下块处为零；$C$ 的后 $n - r$ 列全为零，故其秩显然为 $r$（OCR 此处误作 "zero rows"，按数学应为 "zero columns"）。证明末尾的右下残差块记为 $K$（OCR 显示为 $H$），它与步骤 1 中已被证明为零的左下块 $H$ 是不同位置的两个块；$K$ 承载 $A$ 的最小的 $m - r$ 个奇异值（此处假设 $m \le n$，故奇异值依次为 $\sigma_1 \ge \cdots \ge \sigma_m$）。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 这条注的任务是把 Stewart 证明里的两个零件位置讲清楚，因为它们正是新手读证明时最容易卡住的地方。先建立坐标：在 $B$ 的 SVD 基底 $U, V$ 下，把 $U^T A V$ 切成四块——左上 $E$、右上 $L$、左下 $H$、右下 $K$；而最优的 $B$ 在同一个基底下只有左上块 $D$ 非零，其余三块全为零。竞争者 $C$ 的定义是：左上块取 $D+L$，右上块取零，左下块**保留** $H$，右下块取零。这里有个反直觉的细节：$C$ 与 $A$ 在左下块完全一致，所以 $A-C$ 的左下块恰好为零；而右上块 $L$ 与右下块 $K$ 仍留在 $A-C$ 里。
> 为什么 $C$ 的秩显然不超过 $r$？注意 $C$ 的后 $n-r$ 列全为零：它的列空间被前 $r$ 列张成，秩至多 $r$。这就是表示的力量——把矩阵写成零列块形式，秩约束从列之间是否线性相关这种需要计算的问题，降级为数一数非零列块这种一眼可见的问题。这也正是原注指出的 OCR 勘误的价值：若误读成后 $n-r$ 行全为零（zero rows），秩不超过 $r$ 的结论根本不成立，因为列空间的维数由列决定；数学上必须是零**列**。这类文字方向性错误在矩阵证明里危害极大，因为行与列的不对称正是秩概念的核心。
> 支撑这套块论证的计算事实值得单独点破：Frobenius 范数的平方等于四个块范数平方之和，因为 $\|M\|_F^2=\sum_{ij}m_{ij}^2$ 对任何分块求和都没有交叉项；于是 $\|A-C\|_F^2$ 与 $\|A-B\|_F^2$ 可以逐块比较。谱范数没有这种逐块可加性，所以同一结论对谱范数要走注 19 的维数对撞路线——两条路线互为补充。
> 再看证明末尾的命名冲突。步骤 1 中已经被证明为零的左下块叫 $H$；而残差比较之后留在右下、承载 $A$ 的最小奇异值的块，在书页（或 OCR 输出）中有时也显示为 $H$，数学上它是另一个位置。为避免混淆，本条注把它记为 $K$。两个块的功能也不同：左下块 $H$ 是必须为零的块（否则 $C$ 会比最优的 $B$ 更好，矛盾），右下块 $K$ 是必须保留、且其奇异值被最优性锁死为 $A$ 的最小 $m-r$ 个奇异值的块。这里假设 $m \le n$：此时 $A$ 有 $m$ 个奇异值，秩 $r$ 截断后恰好剩下 $m-r$ 个给 $K$；若 $m > n$，则剩余个数应改为 $n-r$。原注的 $m \le n$ 假设正是为了固定这个计数。
> 若 $m>n$，把 $A$ 换成 $A^T$ 讨论即可：$A$ 与 $A^T$ 的奇异值相同、Frobenius 范数相同，最优逼近的转置就是转置的最优逼近，计数从 $m-r$ 自动换成 $n-r$。
> 用正文开头的 4 by 4 例子验证：若 $A$ 的奇异值为 $4, 3, 2, 1$，则秩 $2$ 最优逼近 $A_2$ 保留 $\sigma_1 = 4$ 与 $\sigma_2 = 3$，残差块 $K = \operatorname{diag}(2, 1)$ 承载最小的 $m-r = 2$ 个奇异值，误差 $\|A-A_2\|_F = \sqrt{2^2 + 1^2} = \sqrt{5}$，与正文一致。跨课程连接：这种通过换基把对象写成块状、让目标性质浮出表面的策略，与你学过的两处做法同构——Strang 的 SVD 用 $U, V$ 把任意矩阵对角化为 $\Sigma$，让秩与奇异值可见；CSAPP 第 6 章的记忆体层级里，缓存分块（blocking）重排循环与数据布局，让时间局部性可见。三者的共同模板是：**先选对的表示，再让困难性质变成表示下的平凡观察**。
> 方向性错误的排查可以固化成一道自检题：看到「后 $n-r$ 列/行为零」时，先问自己「秩由列数还是行数决定」。列空间维数由列张成，行空间维数由行张成，矩阵的秩同时等于两者；但「后 $n-r$ 列全为零」与「后 $n-r$ 行全为零」对列空间的约束完全不同，前者立即给出秩上界，后者什么也不给。
> 一句话收束：读矩阵证明时，先问这个块在哪个位置、被谁清零、被谁保留——位置就是论证，方向就是结论。
---


---

<!-- page 080: 书页 75, §I.9 续：Minimizing the Frobenius Distance；Principal Component Analysis 开始 -->

### Minimizing the Frobenius Distance（最小化 Frobenius 距离）$\|A - B\|_F$

<span style="color:#2471a3;">**[proof]**</span> 这里有一个证明 Eckart-Young 的不同且更直接的方法：令 $\|A - B\|_F$ 的 derivatives（导数）为零。

每个 rank（秩）为 $r$ 的矩阵都可以分解为 $B = CR = (m \times r)(r \times n)$。

借助 SVD，我们可以要求 $C$ 有 $r$ 个 orthogonal（正交）列（$C^TC = $ 对角矩阵 $D$），并要求 $R$ 有 $r$ 个 orthonormal（标准正交）行（$RR^T = $ 对角矩阵）。我们的目标正是 $C = U_k\Sigma_k^{1/2}$ 与 $R = \Sigma_k^{1/2}V_k^T$。

对 $E = \|A - CR\|_F^2$ 求导，以找出使 $E$ 最小的矩阵 $C$ 与 $R$：

```math
\frac{\partial E}{\partial C} = 2(CR - A)R^T = 0
\qquad
\frac{\partial E}{\partial R} = 2(R^TC^T - A^T)C = 0
\qquad (19)
```

第一个等式给出 $AR^T = CRR^T = C$（因为 $RR^T = I$）。第二个等式给出 $R^TD = A^TC = A^T A R^T$。由于 $D$ 是对角的，这意味着 $R^T$ 的每一列 $r_j$ 都满足 $A^TA\, r_j = d_j r_j$：

```math
A^T A R^T = R^T D \qquad \text{（逐列：} A^T A\, r_j = d_j\, r_j \text{，} j = 1, \ldots, r \text{）}
```

于是，矩阵 $R^T$ 的列是 $A^TA$ 的 eigenvectors（特征向量）。它们就是 right singular vectors（右奇异向量）。

类似地，$C$ 的列是 $AA^T$ 的特征向量：$AA^TC = CD^2$。于是 $C$ 包含 left singular vectors（左奇异向量）。

究竟是哪些 singular vectors（奇异向量）真正使误差 $E$ 最小呢？误差 $E$ 是当 $D$ 取代 $C$ 与 $R$ 中的 $\Sigma$ 时被丢弃的所有 $\sigma^2$ 之和。为了最小化 $E$，被丢弃的应当是 $A$ 的最小的奇异值。这就把最大的奇异值留给了最优矩阵 $B = CR = A_k$，其误差为：

```math
\|A - CR\|_F = \sqrt{\sigma_{k+1}^2 + \cdots + \sigma_m^2}
```

这个简洁的证明见于 Nathan Srebro 的 MIT 博士论文（*Learning with Matrix Factorizations*, MIT, 2004，链接可能已失效，可通过 MIT DSpace 检索）：

`ttic.uchicago.edu/~nati/publications/thesis.pdf`

---

### Principal Component Analysis（主成分分析）

<span style="color:#2471a3;">**[section]**</span> 现在我们使用 SVD。矩阵 $A$ 就是数据。我们有 $n$ 个 samples（样本）。对每个样本（sample），我们测量 $m$ 个 variables（变量）（如 height（身高）与 weight（体重））。数据矩阵 $A$ 有 $n$ 列和 $m$ 行。在许多应用中它是一个非常大的矩阵。

第一步是沿 $A$ 的每一行求出 average（平均值，即 sample mean（样本均值））。把该均值从该行的全部 $n$ 个 entries（条目）中减去。现在 centered matrix（中心化矩阵）的每一行均值都为零。

矩阵 $A$ 的列是 $\mathbb{R}^m$ 中的点。由于中心化，column vectors（列向量）之和为零，所以平均列就是 zero vector（零向量）。

这些点往往聚集在 $\mathbb{R}^m$ 中的一条直线、一个平面或其他 low-dimensional subspace（低维子空间）附近。Figure I.11（图 I.11）展示了一组典型的数据点，它们聚集在 $\mathbb{R}^2$ 中的一条直线附近（在把 $A$ 中心化、使点左移右移、上移下移、让均值落在 $(0, 0)$ 之后）。

线性代数（linear algebra）如何找到过原点的最接近的直线呢？它就在 $A$ 的第一个奇异向量 $u_1$ 的方向上。这正是 PCA 的关键点！

**图 I.11（Figure I.11）：** 数据点（$A$ 的列）通常靠近 $\mathbb{R}^2$ 中的一条直线或 $\mathbb{R}^m$ 中的一个子空间。

> 图中并列注明的 SVD 结构：
> - 矩阵 $A$ 是 $2 \times n$ 的（large nullspace，大零空间）
> - 矩阵 $AA^T$ 是 $2 \times 2$ 的（small matrix，小矩阵）
> - 矩阵 $A^TA$ 是 $n \times n$ 的（large matrix，大矩阵）
> - 奇异值（singular values）$\sigma_1 > \sigma_2 > 0$

---

> <span style="color:#1e8449;">**译者注**</span>：本节（§I.9）的图 I.11 即 PCA 的核心示意图：数据矩阵 $A$（$m$ 行变量、$n$ 列样本）中心化后，样本点聚集在过原点的某条直线附近；该直线方向由 $A$ 的第一个左奇异向量 $u_1$ 给出（下一页将说明 $u_1$ 也是 sample covariance matrix（样本协方差矩阵）$S$ 的特征向量）。奇异值下标按 $\sigma_1 \ge \cdots \ge \sigma_m$ 排列，此处假设 $m \le n$。

---

<!-- page 081: 书页 76, §I.9 The Statistics Behind PCA（PCA 背后的统计学） -->
# Strang LaLFD Part I（线性代数与从数据中学习）

### <span style="color:#c0392b;">The Statistics Behind PCA（PCA 背后的统计学）</span>

概率论与统计学（probability and statistics）中的关键数字是 mean（均值）与 variance（方差）。

mean（均值）就是数据在矩阵 $A$ 每一行上的平均值（average）。

从 $A$ 的每一行中减去这些均值，就得到了中心化的 $A_c$（centered $A_c$）。

至关重要的量是 variances（方差）与 covariances（协方差）。

---

variances（方差）是沿 $A_c$ 每一行、从均值出发的平方距离（sums of squares of distances from the mean）之和。

variances（方差）正是矩阵 $A_c A_c^T$ 的对角元（diagonal entries）。

---

假设 $A$ 的列对应某个儿童的 age（年龄，画在 x 轴）与 height（身高，画在 y 轴）。

（这些年龄与身高都以平均年龄与平均身高为起点来度量。）

我们要寻找的，是图中保持与数据点最接近的那条直线（straight line）。

而且我们必须把数据的 joint spread（联合散布）纳入考量。

---

covariances（协方差）是矩阵 $A_c A_c^T$ 的非对角元（off-diagonal entries）。

它们就是点积（dot products）：$A_c$ 的第 $i$ 行与第 $j$ 行的点积。

协方差高意味着身高增长伴随年龄增长。

（协方差为负则意味着一个变量增大时另一个变量减小。）

我们的例子只有年龄与身高两行，因此对称矩阵 $A_c A_c^T$ 是 $2 \times 2$ 的。

随着样本儿童数 $n$ 增大，我们除以 $n-1$，使 $A_c A_c^T$ 获得统计学上正确的尺度（scale）。

---

<span style="color:#2471a3;">**[definition]**</span> <span style="color:#00838f;">样本协方差矩阵（sample covariance matrix）定义为</span>

```math
S = \frac{A_c A_c^T}{n-1}
```

因子是 $n-1$，因为一个自由度（degree of freedom）已经被用于令均值为零。

下面是一个包含六个年龄与身高、且已中心化（每一行相加为零）的例子：

```math
A_c = \begin{bmatrix} -5 & -5 & 0 & 0 & 5 & 5 \\ -7 & -5 & -5 & 4 & 6 & 7 \end{bmatrix}
```

> <span style="color:#1e8449;">**[note]**</span> OCR 损坏，矩阵按 $S$ 重建：原书此处给出一个 $2\times 6$ 的已中心化数据矩阵，每一列是一个儿童的（年龄，身高）数据对。本页 OCR 中该矩阵的数字严重损坏（残存数字 3、7、1、7、8、7 与下文 $S$ 的数值不相容），此处按 $A_cA_c^T/(n-1) = S$ 重建为上方矩阵（每行相加为零，$n=6$）；下文 $S=\begin{bmatrix}20&25\\25&40\end{bmatrix}$ 及其特征值 57 与 3 均为原书确证的数值。

对这组数据，样本协方差矩阵 $S$ 很容易计算，它是正定的（positive definite）：

```math
S = \begin{bmatrix} 20 & 25 \\ 25 & 40 \end{bmatrix}
```

> <span style="color:#7f8c8d;">图注：Variances and covariances（方差与协方差）——对角元是方差，非对角元是协方差。</span>

$S$ 的两个正交（orthogonal）特征向量是 $v_1$ 与 $v_2$，它们正是 $A_c$ 的前导奇异向量（leading singular vectors）。

埃克特-扬（Eckart-Young）定理断言：向量 $v_1$ 指向图 I.11 中那条最接近的直线。

$S$ 的特征向量就是 $A_c$ 的奇异向量（singular vectors）。

第二个奇异向量 $v_2$ 将垂直于（perpendicular）那条最接近的直线。

---

<span style="color:#2471a3;">**[note]**</span> PCA（主成分分析，Principal Component Analysis）既可以用对称矩阵 $S = A_c A_c^T/(n-1)$ 来描述，也可以用长方形矩阵 $A_c$ 来描述。

毫无疑问 $S$ 是更漂亮的矩阵。

但是，当数据以 $A_c$ 的形式给出时，再去计算 $S$ 反而是一个计算上的失误（computational mistake）。

对大型矩阵而言，直接对 $A_c$ 做奇异值分解（SVD）更快也更精确。
> <span style="color:#7f8c8d;">Strang §I.9, p.76</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 先从第一性原理把 $S = A_c A_c^T/(n-1)$ 与方差/协方差之间的等号焊死。设 $A_c$ 的第 $i$ 行是变量 $i$ 的 $n$ 个中心化观测值，记为 $x_i = (x_{i1},\ldots,x_{in})$，其均值为零。回忆 6.042J：随机变量 $X$ 的方差是 $\operatorname{Var}(X) = E[(X-\mu)^2]$，协方差是 $\operatorname{Cov}(X,Y) = E[(X-\mu_X)(Y-\mu_Y)]$。把期望换成对 $n$ 个样本的平均，$(A_c A_c^T)_{ij} = x_i \cdot x_j = \sum_t x_{it} x_{jt}$。当 $i = j$ 时这是平方距离之和，除以 $n-1$ 得到样本方差；当 $i \ne j$ 时这是点积之和，除以 $n-1$ 得到样本协方差。所以 $S$ 不是某种代数巧合，它就是把方差定义逐条填进矩阵的产物。
> 用一个三样本的小例子把等号焊到数字上：变量一取 $1,3,5$（均值 3，中心化后 $-2,0,2$），变量二取 $2,4,6$（均值 4，中心化后 $-2,0,2$）。于是 $A_c=\begin{bmatrix}-2&0&2\\-2&0&2\end{bmatrix}$，$A_cA_c^T=\begin{bmatrix}8&8\\8&8\end{bmatrix}$，除以 $n-1=2$ 得 $S=\begin{bmatrix}4&4\\4&4\end{bmatrix}$；变量一方差 $4$、协方差 $4$，与矩阵逐元一致。
> 分母为何是 $n-1$？中心化条件 $\sum_t x_{it} = 0$ 意味着这 $n$ 个数只有 $n-1$ 个是自由的——给定前 $n-1$ 个，最后一个被强制确定。这就是自由度（degrees of freedom）的直观含义：均值本身是从数据里估计出来的，消耗掉一个自由度。除以 $n$ 会系统性低估总体方差，除以 $n-1$ 恰好把偏差补回来（Bessel 校正）。对 PCA 而言，$n-1$ 还是 $n$ 只整体缩放 $S$ 的特征值，不改变特征向量，因此不改变主成分方向；但理解 $n-1$ 的来历，才能理解为什么总方差公式 (21) 的分母是 $n-1$ 而不是 $n$。
> 为什么除以 $n-1$ 恰好无偏？令 $s^2=\frac{1}{n-1}\sum_t(x_t-\bar x)^2$，由期望线性性 $E[\sum_t(x_t-\bar x)^2]=\sum_t E[x_t^2]-nE[\bar x^2]=n(\sigma^2+\mu^2)-n(\sigma^2/n+\mu^2)=(n-1)\sigma^2$。工具只有 6.042J 的期望线性性与 $\operatorname{Var}(\bar x)=\sigma^2/n$；Bessel 校正不是黑箱，而是这两条性质的自然输出。
> 现在把 PCA 接到 SVD 上。第一个主成分 $v_1$ 被定义为最大化投影方差的方向：$v^T S v = \|A_c^T v\|^2/(n-1)$，即在单位向量上最大化 $\|A_c^T v\|$——这是 page_068 瑞利商的统计翻译。而 Eckart-Young（正文方程 8–14）告诉我们：$\|A_c^T v\|$ 的最大化方向正是 $A_c$ 的第一个右奇异向量，最大值是 $\sigma_1$。于是方差最大的方向与最佳秩 $1$ 逼近的方向在数学上被钉死为同一个 $v_1$：图 I.11 里那条最接近的直线既是投影方差最大的直线，也是垂直距离平方和最小的直线。$S$ 的特征值 $\lambda_i = \sigma_i^2/(n-1)$ 沿各主成分方向分配总方差，迹 $\operatorname{trace}(S) = \sum_i \lambda_i$ 等于总方差——这里又用上了迹在正交变换下的不变性，因为特征值之和就是对角元之和。
> 中心化本身也是一个投影：$A_c=A(I-\frac1n\mathbf{1}\mathbf{1}^T)$，其中 $I-\frac1n\mathbf{1}\mathbf{1}^T$ 是到全 1 向量正交补上的正交投影，秩 $n-1$——从投影角度再次解释自由度。总方差等于迹在上例可复核：$\operatorname{trace}(S)=8$ 恰等于两变量样本方差之和；$\lambda_1=8,\lambda_2=0$，全部方差沿 $(1,1)/\sqrt2$ 方向，与三点共线相符。
> 正文那句直接对 $A_c$ 做 SVD 更快也更精确可以从你熟悉的 CSAPP 数值视角加固：显式形成 $S = A_c A_c^T$ 会把条件数平方——$\kappa(A_c A_c^T) = \kappa(A_c)^2$。若 $A_c$ 的条件数是 $10^8$，$S$ 的就是 $10^{16}$，双精度下小奇异值已经掉进舍入误差的噪声地板。CSAPP §2.4 的灾难性抵消教你相近的大数相减会丢光有效位；矩阵版的同一现象是先平方再开方会丢光小奇异值。所以对 $A_c$ 直接做 SVD 不是风格偏好，而是把计算 $S$这一步的数值风险从流水线上拆掉。
> 一句话收束：$S$ 负责理解（方差、协方差、总方差都在它身上），$A_c$ 负责计算（SVD 又快又稳）——两者通过 $S = A_c A_c^T/(n-1)$ 共享同一组特征信息，这正是数学表示与数值实现的经典分工。
---


---

<!-- page 082: 书页 77, §I.9 Principal Components and the Best Low Rank Matrix（主成分与最佳低秩矩阵） -->

在本例中，$S$ 的特征值（eigenvalues）接近 57 与 3。

它们的和是 $20 + 40 = 60$，正好等于 $S$ 的迹（trace）。

第一个秩一分量（rank one piece）$\sigma_1^2 v_1 v_1^T$ 比第二个分量 $\sigma_2^2 v_2 v_2^T$ 大得多。

前导特征向量 $v_1 = (0.6,\, 0.8)$ 告诉我们，散点图（scatter plot）中那条最接近的直线斜率约为 $8/6$。

图中这个方向几乎构成了一个 $6$-$8$-$10$ 直角三角形（right triangle）。

现在我将从 PCA 的代数转向几何：沿 $v_1$ 方向的直线，在何种意义下是对中心化数据的最接近拟合（closest fit）？

### <span style="color:#c0392b;">The Geometry Behind PCA（PCA 背后的几何）</span>

图 I.11 中的最佳直线求解的是一个垂直最小二乘（perpendicular least squares）问题。

它也叫做 orthogonal regression（正交回归），或 total least squares（总体最小二乘）。

它与对数据点的标准最小二乘拟合不同，也与线性方程组 $Ax = b$ 的最小二乘解不同。

第 II.2 节中那个经典问题最小化的是 $\|Ax - b\|^2$，它度量的是到最佳直线的上下竖直距离。

我们的问题则最小化垂直距离。

较早的那个问题导出一个线性方程组 $A^T A x = A^T b$；我们的问题则导出 $A_c$ 的奇异向量（即 $S$ 的特征向量）。

它们代表线性代数的两个侧面——并不是同一个侧面。

---

数据点到 $v_1$ 直线的平方距离之和取到最小值：

```math
\sum_i \|a_i\|^2 = \sum_i (v_1^T a_i)^2 + \sum_i \|a_i - (v_1^T a_i)\, v_1\|^2
```

要理解这一点，把 $A_c$ 的每一列 $a_i$ 分解为沿 $v_1$ 与沿 $v_2$ 的两个分量：

```math
a_i = (v_1^T a_i)\, v_1 + (v_2^T a_i)\, v_2 \tag{20}
```

左端的和由数据完全确定。

右端第一个和的各项是 $(v_1^T a_i)^2$，它加起来等于 $v_1^T (A_c A_c^T)\, v_1$。

因此在 PCA 中，当我们选取 $A_c A_c^T$ 的最大特征向量 $v_1$ 来最大化那个和时，就同时最小化了第二个和。

这第二个和——数据点到最佳直线（或最佳子空间）的平方距离之和——达到了尽可能小。

### <span style="color:#c0392b;">The Linear Algebra Behind PCA（PCA 背后的线性代数）</span>

主成分分析（Principal Component Analysis, PCA）是理解 $m$ 维空间中样本点 $a_1, \ldots, a_n$——也就是数据——的一种方式。

这个数据图是中心化的：$A_c$ 的所有行相加为零（$A_c \mathbf{1} = 0$）。

它与线性代数的关键联系在于 $A_c$ 的奇异值 $\sigma_i$ 与奇异向量。

这些来自样本协方差矩阵 $S = A_c A_c^T/(n-1)$ 的特征值 $\lambda_i = \sigma_i^2$ 与特征向量。

数据中的总方差（total variance）来自 $A_c$ 的弗罗贝尼乌斯范数（Frobenius norm）的平方：

```math
\text{total variance} = \frac{\|A_c\|_F^2}{n-1} = \text{trace}(S) = \sum_i \frac{\sigma_i^2}{n-1} \tag{21}
```

这就是 $S$ 的迹——沿对角线的和。

线性代数告诉我们，这个迹等于样本协方差矩阵 $S$ 的特征值 $\sigma_i^2/(n-1)$ 之和。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 标准最小二乘与 PCA 的区别，根子不在几何而在**模型假设**。标准 LS（Strang §II.2）的设定是：设计矩阵 $A$ 精确已知，只有观测向量 $b$ 带噪声，误差只发生在竖直方向；于是残差 $b - Ax$ 的每一维都垂直于 $A$ 的列空间，最优解由正规方程 $A^T A x = A^T b$ 给出。PCA 的正交回归设定是：**所有坐标都可能含测量误差**，竖直方向没有任何特权。此时再去最小化竖直距离，就等于单方面相信横坐标、把横坐标的噪声也算到纵坐标头上，拟合结果会系统性偏向水平方向。垂直距离是唯一对坐标旋转不偏心的选择。
> 为什么最小化垂直距离会自动变成最大化投影方差？只需要勾股定理。把每个数据点 $a_i$ 对直线方向 $v$ 做正交分解 $a_i = P a_i + (a_i - P a_i)$，其中 $P a_i = (v^T a_i) v$ 是投影，残差垂直于 $v$。于是 $\|a_i\|^2 = \|P a_i\|^2 + \|a_i - P a_i\|^2$。对所有点求和：$\sum_i \|a_i\|^2 = \sum_i (v^T a_i)^2 + \sum_i \|a_i - P a_i\|^2$。左边是数据的固定总能量，不随 $v$ 变化；因此**最小化残差平方和（右边第二项）与最大化投影平方和（右边第一项）是同一个问题**。而 $\sum_i (v^T a_i)^2 = v^T (A_c A_c^T) v$，这正是瑞利商。这就是原注所说的对偶性：不是两条独立的优化路径，而是勾股定理把剩下多少误差与抓住多少方差绑定成互补关系。
> 正交回归的闭式解也值得写下来：最优方向 $v$ 是 $S=A_cA_c^T$ 的最大特征向量，因为最大化 $\sum_i(v\cdot a_i)^2=v^T S v$ 正是瑞利商；若直线不要求过原点，先对数据中心化（减均值），PCA 直线自动过均值点——这与最小二乘中带截距项等价于先中心化再回归是同一个道理。
> 一个思想实验可以检验两条线的差异。取五个点 $(1,1),(2,2.1),(3,2.9),(4,4.2),(5,5.0)$，真方向接近 $45^\circ$ 但两个坐标都有小幅噪声。标准 LS（$y$ 对 $x$ 回归）最小化竖直残差，当 $x$ 也含噪声时斜率会被拉向水平，估计值系统性地小于真斜率；PCA 第一主成分最小化垂直残差，两个坐标被对称对待，方向估计更接近 $45^\circ$。反过来，若你确知 $x$ 是实验设定值（如施加的电压、配好的浓度）而只有 $y$ 是测量值，则竖直距离才是对的。模型决定度量，度量决定解——这条原则在 6.006 的算法设计中同样成立：目标函数的选择就是你对问题假设的编码。
> 衰减偏误可以更精确：若真实关系 $y=\beta x+\varepsilon$，而 $x$ 被方差 $\sigma_w^2$ 的独立噪声污染，则 LS 斜率依概率收敛到 $\beta\sigma_x^2/(\sigma_x^2+\sigma_w^2)$，永远比真值更靠近零。PCA 对两个坐标对称处理，不产生这种系统性偏斜。
> 跨课程连接可以更具体。Strang §II.2 的正规方程来自残差正交于列空间这个几何事实，其投影矩阵 $A(A^T A)^{-1} A^T$ 正是竖直投影的代数化身；而 PCA 的 $v_1 v_1^T$ 是垂直投影到最佳直线的代数化身。两者都是投影，但投影方向不同，因为各自假设的误差方向不同。从 CSAPP 的数值视角再补一刀：当两个坐标量纲相同、误差量级相当时，竖直距离还会把量纲的不对称固化进结果——厘米与英寸的换算会改变 LS 的斜率，却不改变 PCA 的方向（对正交回归，各向同性缩放下解不变）。因此更诚实的度量不是修辞，而是对称性要求：对坐标轴的任意正交变换，度量应当协变而非偏心。
> 各向同性缩放下 PCA 不变的证明只需一步：把每个点换成 $c a_i$，则 $\sum_i(v\cdot c a_i)^2=c^2\sum_i(v\cdot a_i)^2$，最大化方向不变；而 LS 最小化 $\sum_i(y_i-kx_i-b)^2$，当 $x$ 与 $y$ 用不同单位缩放时目标函数改变，解也随之改变。厘米改英寸会改 LS 斜率，却不动 PCA 方向——这是量纲分析在统计建模里的现身。
> 一句话收束：LS 与 PCA 的差别可以压缩成一句——你相信哪个坐标没有误差，就沿哪个坐标量残差；都不信，就沿垂线量。
---


---

<!-- page 083: 书页 78, §I.9 Principal Components and the Best Low Rank Matrix（主成分与最佳低秩矩阵）续 -->

$S$ 的迹（trace）把总方差（total variance）与各主成分（principal component）的方差之和联系了起来：

```math
\text{Total variance} = \frac{\sigma_1^2 + \cdots + \sigma_n^2}{n-1} \tag{22}
```

与方程 (20) 完全一样，第一个主成分 $\sigma_1 v_1$ 解释了总方差 $T$ 的 $\sigma_1^2 / T$ 这一部分。

$S$ 的下一个奇异向量（singular vector）$v_2$ 解释下一个最大的部分。

每一个奇异向量都在尽自己最大的努力去捕捉矩阵中的含义——它们共同配合便成功了。

---

埃克特-扬（Eckart-Young）定理的要点在于：奇异向量（协同作用时）能尽可能好地解释数据的方差（variance）。

因此我们有理由选择 $v_1, \ldots, v_k$ 作为最接近数据点（data points）的 $k$ 维子空间（subspace）的一组基。

读者明白，我们的 Figure 1.11（图 I.11）展示的是 $m = 2$ 维空间中一簇围绕一条直线分布的数据点。

真实问题往往有 $n > 1$ 且 $m > 2$。

---

$A$ 与 $S$ 的“有效秩”（effective rank）是位于噪声（noise）淹没数据中真实信号（true signal）那一点之上的奇异值的个数。

这一点常常在碎石图（scree plot）上清晰可见，它展示奇异值（或其平方 $\sigma^2$）的骤降。

图 1.12（Figure 1.12）展示了碎石图中的“肘点”（elbow），在肘点处信号（signal）结束而噪声（noise）接管。

在本例中，噪声来自计算病态（badly conditioned）的希尔伯特矩阵（Hilbert matrix）奇异值时的舍入误差（roundoff error）。

真实奇异值的骤降依然十分陡峭。

在实际问题中，噪声位于数据矩阵（data matrix）本身之中——即对 $A$ 的测量值（measurements）中的误差。

本书的 Section III.3 将研究像 $H$ 这样奇异值快速衰减的矩阵。

---

### 图 1.12：hilb(40) 的奇异值

> <span style="color:#7f8c8d;">**Figure 1.12**：难缠的希尔伯特矩阵的 $\sigma_1, \ldots, \sigma_{39}$（$\sigma_{40} = 0$）的碎石图，肘点位于有效秩 $r = 17$ 处，且 $\sigma \approx 10^{-16}$。</span>

---

<span style="color:#2471a3;">**[section]**</span> **One-Zero Matrices and Their Properties（零一矩阵及其性质）**

本书作者与 Alex Townsend 开始研究这样一类矩阵：圆（circle）内为 $1$、圆外为 $0$。

随着这些矩阵不断变大，它们的秩（rank）也随之上升。

奇异值的图像趋近于某个极限——这一点我们还无法预测。

但对于秩，我们却是理解的。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 碎石图的"肘点"是一个数值秩的判据，先把它的第一性原理摆出来。SVD 把 $A$ 的能量按方向分解：$\|A\|_F^2 = \sigma_1^2 + \cdots + \sigma_m^2$（正文方程 14），奇异值按降序排列。如果前 $k$ 个奇异值大且下降陡峭，说明数据能量集中在少数方向，这 $k$ 个方向承载结构；如果第 $k$ 个之后奇异值小且几乎平坦，说明剩余能量在各个方向上均匀摊薄——这正是随机噪声的特征：噪声没有偏好方向，所以对应的奇异值曲线是平的。肘点就是"陡降"与"平台"的接缝，它的索引 $k$ 称为有效秩：数值上，$A$ 表现得像一个秩 $k$ 矩阵。
> 希尔伯特矩阵的例子值得把数值算清楚。$\operatorname{hilb}(40)$ 的条件数约 $10^{19}$，而双精度的机器精度 $\epsilon_{\text{mach}} \approx 2.2 \times 10^{-16}$。二者的乘积逻辑是：一个矩阵在浮点运算中能可靠分辨的最小相对尺度约为 $\sigma_1 \times \epsilon_{\text{mach}}$。$\sigma_1 \approx 1.6$，所以噪声地板约为 $10^{-16}$ 量级；$\sigma_{17}$ 恰好落在这个地板上，而 $\sigma_{18}$ 到 $\sigma_{40}$ 更小，已与舍入噪声无法区分。这就是为什么 Figure I.12 在 $\sigma_{17} \approx 10^{-16}$ 处出现平台——不是希尔伯特矩阵真的只有 17 个非零奇异值，而是**双精度浮点只能保证看到前 17 个**。CSAPP §2.4 里灾难性抵消让减法结果的有效位消失，这里是同一现象的矩阵级放大：条件数 $10^{19}$ 意味着求解或分解过程中，输入的最小相对扰动会被放大 $10^{19}$ 倍，小奇异值的信息在放大途中就被舍入误差吞掉了。
> 一个思想实验可以帮你记住"平台即噪声"：生成一个秩 $2$ 的 $100 \times 100$ 矩阵 $A = 100\,u_1 v_1^T + 10\,u_2 v_2^T$，再加一个各项独立同分布的小噪声矩阵，奇异值谱会呈现 $100, 10$ 两个大值，随后是一段缓慢下降的平坦尾巴。你不可能从尾巴里读出任何"方向"，因为它本质上是各向同性的；把秩 $2$ 截断 $A_2 = 100\,u_1 v_1^T + 10\,u_2 v_2^T$ 拿来重构，噪声几乎被完整剥离。这正是 Eckart-Young 定理的去噪用法：$A_k$ 是"保留信号、丢弃噪声"的最佳秩 $k$ 逼近，而碎石图告诉你该把 $k$ 放在肘点。
> 跨课程连接：寻找肘点的过程在算法上就是二分搜索的连续版——奇异值序列按降序单调排列，"平台开始的位置"可以用"比较相邻奇异值的下降幅度是否跌破阈值"来探测，本质上是在单调序列上找边界点（6.006 的二分查找范式）。而 CSAPP 第 6 章的记忆体层级给了一个绝佳类比：奇异值谱就像缓存访问模式，前面的大奇异值是"热点数据"（被反复访问的结构），后面的平台是"冷数据"（噪声）；保留前 $k$ 个主成分等价于把热点数据留在缓存、把冷数据刷出——数据科学的去噪与体系结构的分层存储共享同一个"集中资源于高能量分量"的经济学。
> 一句话收束：肘点不是数学定理，而是"信号各向异性、噪声各向同性"这一物理直觉在奇异值谱上的读图规则。
---

---

<!-- page 084: 书页 79, §I.9 Principal Components and the Best Low Rank Matrix（主成分与最佳低秩矩阵）续 -->

图 1.13（Figure 1.13）画出了三种形状：方形（square）、三角形（triangle）与四分之一圆（quarter circle）。

任何全为 $1$ 的方形，其秩（rank）都是 $1$。

三角形的所有特征值（eigenvalue）都是 $\lambda = 1$，而它的奇异值（singular value）更有意思。

四分之一圆矩阵的秩是我们的第一个谜题（puzzle），其解答见下文。

### 图 1.13：$N = 6$ 的矩阵中由 1 构成的三种形状

```text
方形（全 1）          三角形（下三角 1）      四分之一圆（1 在 1/4 圆内）
1 1 1 1 1 1        1                    1 1 1 1 1 1
1 1 1 1 1 1        1 1                  1 1 1 1 1
1 1 1 1 1 1        1 1 1                1 1 1 1 1
1 1 1 1 1 1        1 1 1 1              1 1 1 1 1
1 1 1 1 1 1        1 1 1 1 1            1 1 1 1
1 1 1 1 1 1        1 1 1 1 1 1          1 1 1
标注：Rank 1        Rank N                Rank ≈ CN?
```

> <span style="color:#7f8c8d;">**Figure 1.13**：$N = 6$ 的矩阵中由 $1$ 构成的方形、三角形与四分之一圆。</span>

若把这些图形关于 $x$ 轴作反射（reflection），会得到矩形、更大的三角形和边长为 $2N$ 的半圆。

秩不会改变，因为新的行（row）只是旧行的副本（copy）。

再关于 $y$ 轴作反射，则得到方形、菱形（diamond）和整圆。

这一次新的列（column）是旧列的副本：秩依旧相同。

---

从方形和三角形我们可以学到：低秩与水平-竖直方向的对齐（horizontal-vertical alignment）相伴。

对角线（diagonal）带来高秩，而 $45^\circ$ 的对角线带来的秩最高。

当半径 $R = N$ 增大时，四分之一圆的“面积”（area）是多少？

我们寻找的是秩的首项（leading term）$CN$。

第四个图形给出了计算 $C$ 的办法：在四分之一圆内画一个尽可能大的正方形。

那个方形子矩阵（submatrix）（全部为 $1$）的秩是 $1$。

正方形上方的形状有 $(1 - 1/\sqrt{2})N$ 行（约 $0.3N$），它旁边的形状有同样多的列。

那些行与那些列是相互独立的。

把这两个数相加，就得到秩的首项——并且已在数值上得到证实：

```math
\operatorname{Rank}(\text{quarter circle matrix}) = (2-\sqrt{2})\,N \qquad \text{as } N \to \infty \tag{23}
```

---

我们转而考察这些矩阵的（非零）奇异值——对方形是平凡的（trivial），对三角形是已知的，对四分之一圆是可以计算的。

对这些形状以及其他形状，我们总能看到一个“奇异值间隙”（singular gap）。

奇异值不会趋近于零。

所有的 $\sigma$ 都保持在某个极限 $L$ 之上——而我们并不知道其中的原因。

这些图形展示了四分之一圆（计算值）与三角形（精确值）的 $\sigma$。

对于全为 $1$ 的三角形，其逆矩阵（inverse matrix）只是在 $-1$ 对角线之上多了一条 $1$ 的对角线。

于是（逆矩阵的）奇异值为 $\sigma = 2\sin\theta$，其中角度 $\theta = (2k-1)\pi/(4n+2)$ 等间隔分布。

因此，不含奇异值的那个间隙一直延伸到 $\sigma_{\min} \approx 1/2$ 处。

四分之一圆同样有 $\sigma_{\min} \approx 2$。

参见 math.mit.edu/learningfromdata 网站上的学生项目（student project）。

> <span style="color:#1e8449;">**[译者注]**</span> 三角形矩阵本身的最小奇异值在 $n \to \infty$ 时趋于 $1/2$（其逆矩阵的奇异值为 $2\sin\theta$，最大者趋于 $2$）；四分之一圆的最小奇异值约为 $2$。这两处数值在 OCR 中难以完全辨认，译文依上下文与数值结果重建。

---

<!-- page 085: 书页 80, Figure I.14 图注 + Problem Set 1.9 -->

---

<span style="color:#2471a3;">**[figure]**</span> **Figure I.14（图注）**

> <span style="color:#7f8c8d;">Figure I.14: The (nonzero) singular values for the triangle and quarter circle matrices.（三角形与四分之一圆矩阵的（非零）奇异值）</span>

> <span style="color:#1e8449;">**[note]**</span> 本图描绘 triangle（三角形）与 quarter circle（四分之一圆）这两类全 1 矩阵（ones matrix）的 singular values（奇异值）随阶数变化的曲线（图注注明仅示非零奇异值）。三角形矩阵的奇异值来自精确公式，四分之一圆矩阵的奇异值来自数值计算——两者之间始终存在 "singular gap"（奇异值间隙）。

---

<span style="color:#2471a3;">**[exercise]**</span> **Problem Set 1.9（习题集，保留英文原文）**

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.** What are the singular values (in descending order) of $A - A_k$? Omit any zeros.

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.** Find a closest rank-1 approximation to these matrices (2-norm or Frobenius norm):

```math
\begin{pmatrix} 3 & 0 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & 1 \end{pmatrix}
```

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.** Find a closest rank-1 approximation in the L2 norm to $A = \ldots$

> <span style="color:#1e8449;">译者注：原书此处的矩阵 $A$ 在 OCR 扫描文本中缺失，暂以省略号标注，请以原书为准。</span>

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.** The Eckart-Young theorem is false in the matrix norm $\|\cdot\|_\infty = \max$ row sum.

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.** Find a rank-1 matrix closer to

```math
A = \begin{pmatrix} 3 & 1 & 1 \\ 2 & 3 & 3 \end{pmatrix}
```

than $\sigma_1 u_1 v_1^T$ in that norm.

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.** Show that this norm $\|A\| = \max(|a|+|c|,\ |b|+|d|)$ is not orthogonally invariant: find an orthogonal matrix $Q$ such that $\|AQ\| \neq \|A\|$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.** Find the singular values $\sigma(Q)$ for $Q = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.** If $S = Q\Lambda Q^T$ is a symmetric positive definite matrix, explain from Eckart-Young why $q_1 \lambda_1 q_1^T$ is the closest rank-1 approximation in the L2 matrix norm $\|\cdot\|_2$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.** Explain the derivatives $\partial E/\partial C$ and $\partial E/\partial R$ in equation (19) for size = 2.

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.** Which rank-3 matrices have $\|A_1\|_2 = \|A_2\|_2$? $A$ is $\sigma_1 u_1 v_1^T + \sigma_2 u_2 v_2^T$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 11.** Replace the quarter circle in Figure I.13 by the parabola $y = 1 - x^2$. Estimate the rank $cN$ of $A$ with all 1's under the parabola (1's along the axes). First remove a rectangle of 1's, touching the parabola where slope = $-2x$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 12.** If $A$ is a 2 by 2 matrix with $\sigma_1 \sigma_2 > 0$, find $\|A^{-1}\|_2$ and $\|A^{-1}\|_F$.

---

> <span style="color:#1e8449;">译者注（OCR 修正说明）：本页为扫描 OCR 文本，英文已按数学上下文重建——Problem 1 中 $A_k$ 指 $A$ 的秩 $k$ 近似（SVD 截断），故 $A - A_k$ 的非零奇异值为 $\sigma_{k+1}, \dots, \sigma_r$；Problem 4 的矩阵范数是谱范数的反例对象 $\|\cdot\|_\infty$（最大行和）；Problem 6 的范数公式取自 OCR（对 $2\times2$ 矩阵按列取两项绝对值和的最大值），具体加和项请以原书为准；Problem 7 的 $Q$ 为旋转矩阵；Problem 11 的斜率按 $y = 1 - x^2$ 的导数 $dy/dx = -2x$ 重建，原书 OCR 在该处截断。Problem 3 的矩阵在原书 OCR 中缺失。</span>

---

<!-- page 086: 书页 81, §I.10 Rayleigh Quotients and Generalized Eigenvalues -->

# Strang LaLFD Part I（线性代数与从数据中学习）

---

<span style="color:#2471a3;">**[section]**</span>

### <span style="color:#c0392b;">§I.10 Rayleigh Quotients and Generalized Eigenvalues（瑞利商与广义特征值）</span>

本节承接（picks up）并延伸（extends）§I.8 的一个主题。在那里，我们已把 symmetric matrix（对称矩阵）$S$ 的 eigenvalues（特征值）与 eigenvectors（特征向量）联系到 Rayleigh quotient（瑞利商）：

```math
R(c) = \frac{c^T S c}{c^T c} \tag{1}
```

瑞利商 $R(c)$ 的最大值正是 $S$ 的最大 eigenvalue（特征值）$\lambda_1$。该最大值在 eigenvector（特征向量）$c = q_1$ 处达到，其中 $S q_1 = \lambda_1 q_1$：

### <span style="color:#c0392b;">Maximum（最大值）</span>

```math
R(q_1) = \frac{q_1^T S q_1}{q_1^T q_1} = \frac{q_1^T \lambda_1 q_1}{q_1^T q_1} = \lambda_1 \tag{2}
```

类似地，$R(c)$ 的最小值等于 $S$ 的最小 eigenvalue（特征值）$\lambda_n$。该最小值在 "bottom eigenvector"（底部特征向量）$q_n$ 处达到。不仅如此，$S$ 对应介于 $\lambda_n$ 与 $\lambda_1$ 之间的特征值的一切 eigenvectors（特征向量）$c = q_k$，都是 $R(c)$ 的 saddle points（鞍点）。

### <span style="color:#c0392b;">Saddle point（鞍点）</span>

鞍点的 first derivatives（一阶导数）为零，但它们既不是 maxima（极大值）也不是 minima（极小值）：

```math
\frac{\partial R}{\partial c} = 0 \ \text{at} \ c = q_k, \quad \text{then} \ R(q_k) = \frac{q_k^T S q_k}{q_k^T q_k} = \lambda_k \tag{3}
```

这些事实与 $A$ 的 Singular Value Decomposition（奇异值分解）相连。其联系（connection）经由 $S = A^T A$。对于这个 positive definite（正定）（或 semidefinite 半正定）矩阵 $S$，Rayleigh quotient（瑞利商）导出了 $Ac$ 的 norm（范数）的平方（squared）；而 $S$ 的最大 eigenvalue（特征值）正是 $\sigma_1^2$：

```math
\max_c \frac{c^T S c}{c^T c} = \max_c \frac{c^T A^T A c}{c^T c} = \sigma_1^2 \tag{4}
```

这样，一个 symmetric eigenvalue problem（对称特征值问题）同时也是一个 optimization（优化问题）：maximize（最大化）$R(c)$。

---

<span style="color:#2471a3;">**[section]**</span>

### <span style="color:#c0392b;">Generalized Eigenvalues and Eigenvectors（广义特征值与广义特征向量）</span>

统计学（statistics）与数据科学（data science）中的应用把我们带到下一步。工程（engineering）与力学（mechanics）中的应用也指向同一方向。第二个矩阵 $M$ 进入了 $R(c)$ 的分母：

<span style="color:#2471a3;">**[definition]**</span> <span style="color:#00838f;">Generalized Rayleigh quotient（广义瑞利商）</span>

```math
R(c) = \frac{c^T S c}{c^T M c} \tag{5}
```

在 dynamical problems（动力学问题）中，$M$ 常常是 "mass matrix"（质量矩阵）或 "inertia matrix"（惯性矩阵）。在统计学中，$M$ 一般是 covariance matrix（协方差矩阵）。covariance matrices（协方差矩阵）的构造，以及它们在 classifying（分类）数据中的应用，将在关于 probability and statistics（概率与统计）的那一章中给出。

---

> <span style="color:#1e8449;">译者注：公式编号 (1)–(5) 与原书一致；(3) 中原文以 $\partial R/\partial c$ 表示 $R(c)$ 对向量 $c$ 的梯度，在 $c = q_k$ 处为零；(4) 中 $S = A^T A$，故 $c^T S c = c^T A^T A c = \|Ac\|^2$，最大瑞利商即最大奇异值的平方 $\sigma_1^2$。广义特征值问题 $Sx = \lambda Mx$ 将在本节约下一页展开。</span>
> <span style="color:#7f8c8d;">Strang §I.10, p.81</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 先把瑞利商从一个代数恒等式读成一个完整的约束优化问题，因为这才是它真正的工作方式。目标函数 $R(c) = c^T S c / c^T c$；可行域可以取单位球面 $\|c\|_2 = 1$（因为 $R$ 对缩放不变，分子分母同时乘 $t^2$ 不改变值）；最优性条件由一阶必要条件给出。直接对 $R(c)$ 求梯度（把分母视为常数后逐分量求导）：$\partial R/\partial c = 2(Sc - R(c)\,c)/(c^T c)$。令其为零，得到 $Sc = R(c)\,c$——**特征方程**。注意这个闭环：驻点处的 $R(c)$ 值恰好就是特征值 $\lambda$，于是求最大瑞利商与求最大特征值是同一个问题的两种叙述。这就是 6.006 优化范式目标函数 → 可行域 → 最优性条件在特征值问题上的完整落地。补充一个藏在梯度里的几何事实：$c^T(Sc - R(c)c) = c^TSc - R(c)c^Tc = 0$，所以当 $\|c\|=1$ 时梯度自动躺在单位球面的切平面上——它本来就是球面上的合法移动方向，不必再做投影修正。
> 幂法应当从这个梯度视角去理解，但要精确。$R(c)$ 的梯度是 $Sc - R(c)\,c$，其中 $R(c)\,c$ 一项与 $c$ 平行，只改变长度不改变方向；去掉这一项后的主导方向就是 $Sc$。所以幂迭代 $c_{k+1} = Sc_k / \|Sc_k\|$ 不是严格意义上的梯度上升，而是沿梯度的**主导分量** $Sc$ 移动后再投影回单位球面——它朝着使二次型 $c^T S c$ 增长最快的方向走。更精细地说，把幂迭代的切向位移投影到切平面，得 $(I - cc^T)(Sc/\|Sc\| - c) = (Sc - (c^TSc)c)/\|Sc\|$，它与投影梯度 $\nabla_S R = 2(Sc - (c^TSc)c)$ 只差一个正标量因子 $1/(2\|Sc\|)$；因此幂迭代可以视为单位球面上的投影梯度上升，只是步长由 $\|Sc\|$ 归一化决定，而不是自由选取的固定步长。收敛性的证明只用你已有的展开工具：设 $c_0 = \sum_i \alpha_i q_i$，则 $S^t c_0 = \sum_i \alpha_i \lambda_i^t q_i$。当 $|\lambda_1| > |\lambda_2|$ 且 $\alpha_1 \ne 0$ 时，$\lambda_1^t$ 项指数级地压过其余各项，归一化后 $c_t \to q_1$，$R(c_t) \to \lambda_1$，收敛比率为 $|\lambda_2 / \lambda_1|$。这就是反复左乘 $S$ 等价于朝 $\lambda_1$ 爬山的精确含义：不是每步都严格沿梯度，但每步都把 $q_1$ 分量相对放大 $\lambda_1 / \lambda_2$ 倍。
> 一个被初学者忽略的第二层收敛：$R(c_t)$ 逼近 $\lambda_1$ 的误差是 $c_t$ 逼近 $q_1$ 的误差的平方，收敛比率由 $|\lambda_2/\lambda_1|$ 平方为 $|\lambda_2/\lambda_1|^2$。原因是驻点处梯度为零：把 $c = q_1 + \varepsilon v$（$\varepsilon$ 小）代入 $R$，一阶项消失，误差 $\lambda_1 - R(c) = O(\varepsilon^2)$。用展开验证：设 $c = \alpha_1 q_1 + \alpha_2 q_2$（已归一化），则 $R(c) = \lambda_1 \alpha_1^2 + \lambda_2 \alpha_2^2 = \lambda_1 - (\lambda_1-\lambda_2)\alpha_2^2$，而 $\alpha_2$ 正是特征向量误差的一阶量，故 $R$ 的误差是 $\alpha_2$ 的平方。这条“二次精确性”就是 Rayleigh-Ritz 提取敢用粗特征向量报高精度特征值的底气，后面 Lanczos 方法中特征值先于特征向量收敛的现象也源于此。
> 为什么几乎必然收敛到 $\lambda_1$ 而不是别的特征值？用 6.042J 的概率语言：若 $c_0$ 从连续分布（例如球面上的均匀分布或各分量独立的高斯分布再归一化）中抽取，则事件 $\alpha_1 = 0$（即 $c_0$ 恰好垂直于 $q_1$）的概率为零——这就像在圆上随机取点，恰好落在某个特定点上的概率为零。于是以概率 $1$，$\alpha_1 \ne 0$，主导项存在，迭代收敛到 $\lambda_1$。这里不需要测度论的完整机器，只需要连续分布下单个点的概率为零这一条 6.042J 概率直觉。
> 一个二维例子把全过程可视化。取 $S = \operatorname{diag}(3, 1)$，$c_0 = (1, 1)/\sqrt{2}$。初始 $R(c_0) = (3 + 1)/2 = 2$，恰好是特征值的加权平均（各占一半）。一步幂迭代得 $Sc_0 = (3, 1)/\sqrt{2}$，归一化后 $c_1 \approx (0.949, 0.316)$，$R(c_1) = (3 \cdot 0.949^2 + 1 \cdot 0.316^2)/(0.949^2 + 0.316^2) \approx 2.8$——从 $2$ 爬到 $2.8$，向 $\lambda_1 = 3$ 逼近。把迭代公式写成闭式：$c_k = (3^k, 1)/\sqrt{9^k+1}$，于是 $R(c_k) = 3 - 2/(9^k+1)$，$q_2$ 分量每步按 $\lambda_2/\lambda_1 = 1/3$ 缩小；十步后 $(1/3)^{10} \approx 1.7\times10^{-5}$，$R(c_{10}) \approx 3 - 2/9^{10} \approx 2.9999999994$，误差从 $1$ 缩到约 $6\times10^{-10}$——这就是几何级数收敛的实感。再看鞍点结构：在 $q_1$ 处 $R = 3$ 是全局最大；在 $q_2$ 处 $R = 1$ 是全局最小。一般的 $q_k$ 则是鞍点（沿 $q_{k-1}$ 方向微扰上升，沿 $q_{k+1}$ 方向微扰下降），这是下一条注的主题。
> 跨课程连接：迭代格式 $c_{t} \in \operatorname{span}\{c_0, Sc_0, \ldots, S^t c_0\}$ 说明幂法的所有迭代都活在 Krylov 子空间里；现代方法（Lanczos、Arnoldi）正是先构造 Krylov 子空间的正交基，再在这个小得多的子空间上求 Rayleigh 商的驻点（Rayleigh-Ritz 提取），从而用远少于幂法的迭代次数逼近 $\lambda_1$ 乃至一批特征值——这会在 18.065 中展开。而你已学过的 6.042J 加权平均直觉（$R(c) = \sum \lambda_i \alpha_i^2 / \sum \alpha_i^2$ 是特征值的凸组合）始终是理解最大值 $\lambda_1$、最小值 $\lambda_n$、中间值皆鞍点的第一性原理。
> 一句话收束：特征值问题不是解方程的苦工，而是优化问题的驻点条件——这就是瑞利商给特征值重新上的户口。
---





> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 核心机制：把“为什么 $q_k$ 处既非极大也非极小”这一逐点困惑，转化为一个全局变分刻画，也就是 Courant-Fischer 极小极大定理。设计问题可以这样提：如果不先解出全部特征向量，我们凭什么还能谈论“第 $k$ 个特征值”？先注意 Rayleigh 商是尺度不变的：$R(\alpha c)=\alpha^2 c^T S c/(\alpha^2 c^T c)=R(c)$，所以把 $c$ 限制在单位球上不损失任何信息。把 $c=\sum_i\alpha_i q_i$ 代入 $R(c)$，得到 $R(c)=\sum_i\lambda_i\alpha_i^2/\sum_i\alpha_i^2$。这不是普通分式，而是特征值的加权平均：归一化后权重 $\alpha_i^2$ 满足 $\sum_i\alpha_i^2=1$，正是 $c$ 在方向 $q_i$ 上投入的能量份额。于是整个 Rayleigh 商的值域被夹在 $\lambda_n$ 与 $\lambda_1$ 之间，而 $q_k$ 处权重全部集中在第 $k$ 项上，取到 $\lambda_k$。用凸组合的眼光看，鞍点的存在根本不是意外，而是加权平均的固有结构：一个取值在 $\lambda_1$ 与 $\lambda_n$ 之间的加权平均，其第 $k$ 个端点位置自然对更小下标的方向是低点、对更大下标的方向是高点。
> 鞍点性质可以精确到二阶。令 $c=(q_k+\varepsilon q_j)/\sqrt{1+\varepsilon^2}$，代入得 $R(c)=(\lambda_k+\varepsilon^2\lambda_j)/(1+\varepsilon^2)$，整理为 $R(c)=\lambda_k+\varepsilon^2(\lambda_j-\lambda_k)/(1+\varepsilon^2)$。这个式子读出了全部信息：一阶项完全消失，说明 $q_k$ 是驻点；二阶项的符号由 $\lambda_j-\lambda_k$ 决定，沿 $j<k$ 的方向微扰（混入更大的特征值）函数值上升，沿 $j>k$ 的方向微扰（混入更小的特征值）函数值下降。另一个方向用梯度验证：$\nabla R(c)=2(Sc-R(c)c)/(c^T c)$，在 $q_k$ 处 $Sc=\lambda_k q_k$ 且 $R(c)=\lambda_k$，故 $\nabla R=0$——驻点条件恰好等价于特征方程，这就是为什么求 $R$ 的驻点会回到特征值问题。数字特例：$S=\operatorname{diag}(3,2,1)$，在 $q_2=(0,1,0)$ 处 $R=2$；沿 $q_1$ 方向微扰得 $R=(3\varepsilon^2+2)/(1+\varepsilon^2)>2$，沿 $q_3$ 方向微扰得 $R=(2+\varepsilon^2)/(1+\varepsilon^2)<2$。一升一降就是鞍点的全部内容：不需要 Hessian 矩阵，只需要比较相邻特征值谁大谁小。
> Courant-Fischer 的直觉可以用天花板来想：$\lambda_k$ 等于所有 $k$ 维子空间上 $R$ 的最小值的最大值。顺序不能颠倒：先在每个子空间内部取最小（内层对手在你的子空间里挑最坏方向），再在所有子空间之间取最大（外层你挑最好的子空间），这是一个两层博弈。为什么天花板恰好落在 $\lambda_k$？一方面取 $V=\operatorname{span}(q_1,\dots,q_k)$，这个子空间上的最小值就是 $\lambda_k$，因为最坏方向是 $q_k$。另一方面，任意 $k$ 维子空间 $U$ 必与 $\operatorname{span}(q_k,\dots,q_n)$（维数 $n-k+1$）有非零交集，这是维数公式 $\dim(U\cap W)\ge\dim U+\dim W-n$ 的直接结论，本质上是 6.042J 鸽巢原理的向量空间版：$k+(n-k+1)=n+1$ 个维度塞进 $n$ 维空间必有重叠。交集中的非零向量只含 $\lambda_k,\dots,\lambda_n$ 的分量，故 $R$ 在 $U$ 上的最小值不超过 $\lambda_k$。两边一夹，天花板恰好是 $\lambda_k$。
> 跨课程连接：这里 $\max$ 与 $\min$ 交换顺序能被严格证明，其基础正是你在 TBB 实分析中学习的确界语言——有限维闭单位球是紧集，连续函数 $R$ 在其上必达最大值与最小值，所以这些确界全部取得到，而不是悬空的上界；而 18.065 把 Courant-Fischer 当作矩阵扰动分析的工作母机，Weyl 不等式把 $\lambda_k(A+B)$ 相对 $\lambda_k(A)$ 的漂移夹在 $\lambda_k(A)+\lambda_n(B)$ 与 $\lambda_k(A)+\lambda_1(B)$ 之间，正是上述极值刻画的换一种说法；证明只有一步，在极小极大表达式中把 $x^T(A+B)x$ 拆成 $x^T A x+x^T B x$，先对第二项用上界 $\lambda_1(B)$ 与下界 $\lambda_n(B)$ 夹住，再对第一项应用 Courant-Fischer 即可。一句话收束：$q_k$ 是鞍点不是缺陷，而是特征值有序性的真正来源。
---


---

<!-- page 087: 书页 82, §I.10 Rayleigh Quotients and Generalized Eigenvalues（续） -->

# Strang LaLFD Part I（线性代数与从数据中学习）

---

### 特征值问题从 $Ax = \lambda x$ 变为 $Sx = \lambda Mx$

这里我们的 goal（目标）是弄清：当 $M$ 为 positive definite（正定）时，特征值问题 $Sx = \lambda Mx$ 如何运作。这就是 generalized problem（广义问题）。当 $M$ 正定时，广义 Rayleigh quotient（瑞利商）$R(x) = x^T S x / x^T M x$ 的最大值，就是 $M^{-1}S$ 的最大特征值。

我们将把这个广义问题 $Sx = \lambda Mx$ 化归为一个 ordinary eigenvalue problem（普通特征值问题）$Hy = \lambda y$。但你必须看到，选择 $H = M^{-1}S$ 并不真正完美。原因很简单：$M^{-1}S$ 不是 symmetric（对称）的！即使是一个对角矩阵 $M$，也能把这一点说得清清楚楚。

同一个对角矩阵的 square root（平方根）$M^{1/2}$，会提示我们保持对称性的正确途径。考虑对角例子 $M = \begin{pmatrix} m_1 & 0 \\ 0 & m_2 \end{pmatrix}$ 与 $S = \begin{pmatrix} a & b \\ b & c \end{pmatrix}$：

```math
M^{-1}S = \begin{pmatrix} a/m_1 & b/m_1 \\ b/m_2 & c/m_2 \end{pmatrix} \quad \text{is not symmetric}
```

```math
H = M^{-1/2} S M^{-1/2} = \begin{pmatrix} a/m_1 & b/\sqrt{m_1 m_2} \\ b/\sqrt{m_1 m_2} & c/m_2 \end{pmatrix} \quad \text{is symmetric}
```

这两个矩阵 $M^{-1}S$ 与 $H = M^{-1/2}SM^{-1/2}$ 具有相同的特征值。$H$ 看起来有点笨拙，但当我们选取 $M$ 与 $M^{-1}$ 的 symmetric square root（对称平方根）时，对称性就被保住了。

每一个正定矩阵 $M$ 都有一个 positive definite square root（正定平方根）。上面的对角例子有 $M^{1/2} = \text{diag}(\sqrt{m_1}, \sqrt{m_2})$，它的逆就是 $M^{-1/2}$。在所有情形下，我们只需把 $M$ diagonalize（对角化），再对每个特征值取平方根：

```math
M = Q\Lambda Q^T \ \text{has} \ \Lambda > 0, \quad \text{then} \ M^{1/2} = Q\Lambda^{1/2} Q^T \ \text{has} \ \Lambda^{1/2} > 0. \tag{6}
```

把 $M^{1/2}$ 平方即可恢复 $Q\Lambda^{1/2}Q^T Q\Lambda^{1/2}Q^T = Q\Lambda Q^T$，这正是 $M$。我们**不会**在数值上使用 $M^{1/2}$ 或 $M^{-1/2}$！广义特征值问题 $Sx = \lambda Mx$ 在 MATLAB 中是用命令 `eig(S, M)` 求解的。Julia、Python、R 以及所有完整的线性代数系统，都包含这个向 $Sx = \lambda Mx$ 的扩展。

分母含 $x^T M x$ 的瑞利商，很容易转换为分母含 $y^T y$ 的商。设 $x = M^{-1/2}y$，则

```math
\frac{x^T S x}{x^T M x} = \frac{y^T (M^{-1/2})^T S M^{-1/2} y}{y^T y} = \frac{y^T H y}{y^T y}
```

这把广义问题 $Sx = \lambda Mx$ 变成普通的 symmetric problem（对称问题）$Hy = \lambda y$。若 $S$ 与 $M$ 正定，则 $H = M^{-1/2}SM^{-1/2}$ 也正定。

最大的瑞利商仍然给出最大的 eigenvalue（特征值）$\lambda_1$。我们还看到 $H$ 的 top eigenvector（最大特征向量）$y_1$ 与 $M^{-1}S$ 的最大特征向量 $x_1$：

```math
\max_{y} \frac{y^T H y}{y^T y} = \lambda_1
```

当 $Hy_1 = \lambda_1 y_1$ 时这个最大值达到，此时对 $x_1 = M^{-1/2}y_1$ 有 $Sx_1 = \lambda_1 M x_1$。

---




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 设计问题可以这样提：广义问题 $Sx=\lambda Mx$ 若直接左乘 $M^{-1}$，得到 $M^{-1}Sx=\lambda x$。这个矩阵 $M^{-1}S$ 一般不对称，于是“实特征值、标准内积下正交、谱分解”这套对称矩阵工具箱不能直接套用，数值算法也得绕远路。我们想要一个坐标变换，既保持特征值不变，又把问题变回对称形式。第一性原理是：变换不是随便猜的，而是盯住内积。定义 $M$-内积 $\langle x,y\rangle_M=x^T M y$。先确认这个名字名正言顺：$M$ 正定保证 $x^T M x>0$（$x\ne0$），$M$ 对称保证 $\langle x,y\rangle_M=\langle y,x\rangle_M$，双线性来自矩阵乘法对加法的分配律——三条内积公理全满足，于是所有依赖内积的结论都可以在这个新度量里重跑。虽然 $M^{-1}S$ 在标准坐标下不对称，但它关于这个加权内积是自伴的：$\langle M^{-1}Sx,y\rangle_M=(M^{-1}Sx)^T My=x^T S y$，而 $\langle x,M^{-1}Sy\rangle_M=x^T M M^{-1} S y=x^T S y$，两步都只用 $S,M$ 的对称性。这说明不对称只是坐标假象：算子没有坏，是度量选错了。
> Strang 的变换 $y=M^{1/2}x$（等价地 $x=M^{-1/2}y$）正是把度量修好：$\langle x,y\rangle_M=x^T M y=(M^{1/2}x)^T(M^{1/2}y)$，即 $M$-内积在 $y$ 坐标下退化回标准点积。于是关于 $M$-内积的自伴性在 $y$ 坐标下自动变成标准对称性，得到 $H=M^{-1/2}SM^{-1/2}$。验证只需照抄定义：把 $x=M^{-1/2}y$ 代入 $Sx=\lambda Mx$ 得 $SM^{-1/2}y=\lambda MM^{-1/2}y$，左乘 $M^{-1/2}$ 即 $Hy=\lambda y$。为什么特征值一个都没丢？因为 $H=M^{1/2}(M^{-1}S)M^{-1/2}$，$H$ 与 $M^{-1}S$ 相似，相似矩阵共享全部特征值。正定性保证 $M^{1/2}$ 存在：由谱分解 $M=Q\Lambda Q^T$（全部 $\lambda_i>0$），定义 $M^{1/2}=Q\Lambda^{1/2}Q^T$。几何图景是：$y=M^{1/2}x$ 把椭球面 $x^T M x=1$ 映成单位球面 $y^T y=1$，换度量就是换坐标尺。
> 对称化到底赢得了什么？先看第一个红利：实特征值。设 $Hy=\lambda y$，允许 $y$ 为复向量，用共轭转置 $y^H$ 左乘得 $\lambda=y^H H y/(y^H y)$；分母是正实数，分子 $y^H H y$ 在 $H$ 实对称时等于自身的共轭，故 $\lambda$ 必为实数。第二个红利是特征向量在标准内积下正交——那正是注 27 的对称相减模板。换句话说，$M^{-1/2}$ 变换把实谱与正交谱两条性质同时搬运回来。从第一性原理追问一句：为什么 $M^{-1}S$ 明明不对称，却仍有实特征值？因为实谱证明的原料不是“矩阵对称”这个表象，而是“关于某个正定内积自伴”——$M^{-1}S$ 关于 $M$-内积自伴，所以同样的证明在 $M$-度量下原样成立。特征向量也同理：$H$ 的标准正交基 $\{y_i\}$ 拉回 $x$ 坐标得 $x_i=M^{-1/2}y_i$，满足 $x_i^T M x_j = y_i^T y_j = \delta_{ij}$，这就是注 27 要证的 $M$-正交性——换度量不是丢掉正交性，而是把正交的定义一起换掉。若 $M$ 只是半正定，开方仍存在但不可逆，坐标变换失效，这也是主教材假定正定的原因。
> 一个具体思想实验：取 $M=\begin{pmatrix}1&0\\0&4\end{pmatrix}$，$S=\begin{pmatrix}2&1\\1&2\end{pmatrix}$，则 $M^{-1}S=\begin{pmatrix}2&1\\1/4&1/2\end{pmatrix}$ 不对称，它的特征向量在标准点积下不垂直；但按 $M$ 加权重算点积，它们立刻正交——这正是注 27 要证明的 $M$-正交性。把对称化走到底：$M^{-1/2}=\begin{pmatrix}1&0\\0&1/2\end{pmatrix}$，$H=M^{-1/2}SM^{-1/2}=\begin{pmatrix}2&1/2\\1/2&1/2\end{pmatrix}$ 果然对称；其特征值 $\lambda=(2.5\pm\sqrt{3.25})/2\approx 2.151, 0.349$ 就是原广义问题的广义特征值，可直接代入 $Sx=\lambda Mx$ 验算。若不想显式开方，Cholesky 分解给出更便宜的对称化：$M=GG^T$，令 $x=G^{-T}y$，代入得 $G^{-1}SG^{-T}y=\lambda y$，其中 $G^{-1}SG^{-T}$ 是对称的（转置后仍是自己），而 $G$ 只是三角矩阵。
> 数值警告的第一性原理要落到 CSAPP §2.4 的 IEEE 754：双精度单位舍入约为 $2^{-53}$（机器精度为 $2^{-52}$），而显式构造 $M^{-1/2}$ 要先对 $M$ 做谱分解、再逐特征值开方取逆。当 $M$ 接近奇异（$\lambda_{\min}$ 很小）时，$\Lambda^{-1/2}$ 中的大数把 $M$ 里的小扰动按 $1/\sqrt{\lambda_{\min}}$ 放大，再经三次矩阵乘法传播，最终特征值可能被噪声淹没。这就是代数等价与数值可靠的分野：`eig(S,M)` 背后的 QZ 算法用正交变换同时把 $S,M$ 化成三角形式，从对角元比值读出广义特征值，全程不构造任何逆矩阵或平方根；正交变换不放大误差，这是它数值稳定的根本原因。18.065 把这种换度量思路继续用于预处理迭代法与广义 SVD，有限元中的广义特征值问题 $Kx=\lambda Mx$（$K$ 刚度矩阵、$M$ 质量矩阵）也正是按此套路求解的。一句话收束：对称不是矩阵的绝对属性，而是算子与内积这对数据共同决定的属性。
---


---

<!-- page 088: 书页 83, §I.10 Rayleigh Quotients and Generalized Eigenvalues（续） -->

<span style="color:#2471a3;">**[example]**</span> **Example 1（例 1）**

当 $S = \begin{pmatrix} 4 & -2 \\ -2 & 4 \end{pmatrix}$ 且 $M = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$ 时，求解 $Sx = \lambda Mx$。

**Solution（解）** 我们的特征值问题是 $(S - \lambda M)x = 0$ 与 $(H - \lambda I)y = 0$。我们将从两个 determinant（行列式）中找到相同的 $\lambda$：$\det(S - \lambda M) = 0$ 与 $\det(H - \lambda I) = 0$。

```math
\det(S - \lambda M) = \det \begin{pmatrix} 4 - \lambda & -2 \\ -2 & 4 - 2\lambda \end{pmatrix} = 2\lambda^2 - 12\lambda + 12 = 0
```

这个方程给出 $\lambda = 3 \pm \sqrt{3}$。如果你更愿意只用一个矩阵 $H = M^{-1/2}SM^{-1/2}$ 来工作，就必须先把它算出来：

```math
M^{-1/2} = \begin{pmatrix} 1 & 0 \\ 0 & 1/\sqrt{2} \end{pmatrix}, \qquad H = \begin{pmatrix} 1 & 0 \\ 0 & 1/\sqrt{2} \end{pmatrix} \begin{pmatrix} 4 & -2 \\ -2 & 4 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & 1/\sqrt{2} \end{pmatrix} = \begin{pmatrix} 4 & -\sqrt{2} \\ -\sqrt{2} & 2 \end{pmatrix}
```

然后它的特征值来自 $H - \lambda I$ 的行列式：

```math
\det(H - \lambda I) = \det \begin{pmatrix} 4 - \lambda & -\sqrt{2} \\ -\sqrt{2} & 2 - \lambda \end{pmatrix} = \lambda^2 - 6\lambda + 6 = 0
```

它也给出 $\lambda = 3 \pm \sqrt{3}$。这个方程正好是前面 $2\lambda^2 - 12\lambda + 12 = 0$ 的一半。对 $H$ 与 $M^{-1}S$ 得到相同的 $\lambda$。

在 mechanical engineering（机械工程）中，这些 $\lambda$ 会告诉我们一行弹簧里两个 oscillating masses（振动质量）$m_1 = 1$ 与 $m_2 = 2$ 的频率。$S$ 告诉我们连接这两个质量与固定端点的三根弹簧的 stiffness（刚度）。相应的微分方程就是 Newton's Law（牛顿定律）：

```math
M \frac{d^2 u}{dt^2} = -Su
```

### Generalized Eigenvectors are M-orthogonal（广义特征向量是 M-正交的）

关于 symmetric matrix（对称矩阵）$S$ 的一个关键事实是：任意两个特征向量都正交（当特征值不同时）。这一点能否推广到含两个对称矩阵的 $Sx = \lambda Mx$？即时的答案是 no（否），但正确的答案是 yes（是）。

要得到那个答案，我们必须假设 $M$ 正定，并把条件 $x_1^T x_2 = 0$ 换成 $x_1$ 与 $x_2$ 的 "M-orthogonality（M-正交性）"。若 $x_1^T M x_2 = 0$，就说两个向量是 M-orthogonal（M-正交）的。

若 $Sx_1 = \lambda_1 M x_1$、$Sx_2 = \lambda_2 M x_2$ 且 $\lambda_1 \neq \lambda_2$，则 $x_1^T M x_2 = 0$。（7）

用 $x_2^T$ 乘其中一个方程，再用 $x_1^T$ 乘另一个方程：

```math
x_2^T S x_1 = \lambda_1 x_2^T M x_1 \quad \text{and} \quad x_1^T S x_2 = \lambda_2 x_1^T M x_2 \tag{8}
```

因为 $S$ 与 $M$ 都是对称的，对第一个方程取转置得到 $x_2^T S x_1 = \lambda_1 x_1^T M x_2$。两式相减：

```math
(\lambda_1 - \lambda_2) x_1^T M x_2 = 0 \quad \text{and with} \ \lambda_1 \neq \lambda_2 \ \text{this gives} \ x_1^T M x_2 = 0. \tag{9}
```

于是也有 $x_1^T S x_2 = 0$。我们可以在 Example 1 中的矩阵 $S$ 与 $M$ 上检验这个结论。

---
> <span style="color:#7f8c8d;">Strang §I.10, p.83</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 设计问题：已知两个特征方程 $Sx_i=\lambda_i Mx_i$ 与 $Sx_j=\lambda_j Mx_j$，还有 $S,M$ 的对称性，如何把关于 $S$ 的信息转换成关于 $M$ 的结论，证明 $\lambda_i\neq\lambda_j$ 时 $x_i^T M x_j=0$？答案是给这套动作命名，便于复用：对称相减模板。第一步，用 $x_j^T$ 与 $x_i^T$ 分别左乘两个方程，得到两个标量等式 $x_j^T S x_i=\lambda_i x_j^T M x_i$ 与 $x_i^T S x_j=\lambda_j x_i^T M x_j$。第二步是模板的引擎：任何标量都等于自己的转置，故 $x_j^T S x_i=(x_j^T S x_i)^T=x_i^T S^T x_j=x_i^T S x_j$，对称性允许矩阵在点积中自由换边；同理 $x_j^T M x_i=x_i^T M x_j$。两个左端对齐后相减，$S$ 项抵消，剩下 $(\lambda_i-\lambda_j)x_i^T M x_j=0$。第三步用 $\lambda_i\neq\lambda_j$ 消去系数，即得 $M$-正交性；把它代回原式又立刻得到 $x_i^T S x_j=0$。
> 第一性原理追问：为什么最后一步能消去 $\lambda_i-\lambda_j$？因为我们在实数域上工作，任何非零实数都有乘法逆，从 $(\lambda_i-\lambda_j)z=0$ 推出 $z=0$ 是免费的。这恰好是 6.042J 数论里模 $m$ 不能随便消去的镜像：在 $\mathbb{Z}_6$ 中，$3\cdot2\equiv3\cdot4\pmod6$ 都等于 $0$，但 $2\not\equiv4\pmod6$，原因是 $3$ 与 $6$ 不互素，是零因子。模板之所以如此简洁，正是因为我们站在域上——代数结构决定证明工具，这是同一句“两边消去”在不同结构中真伪不同的微型实例。若 $\lambda_i=\lambda_j$，消去一步失效，但重特征值情形可在特征子空间内做 $M$-内积下的 Gram-Schmidt 正交化补救：$M$ 正定保证这个内积是真正的内积，正交化程序照常运转。
> 把注 26 与注 27 串成一条线的统一视角：记 $T=M^{-1}S$，则广义特征方程 $Sx=\lambda Mx$ 就是 $Tx=\lambda x$，而注 26 已证明 $T$ 关于 $M$-内积自伴。于是广义特征向量的 $M$-正交性，无非就是“自伴算子关于它所自伴的那个内积，不同特征值的特征向量正交”这条标准定理——标准对称矩阵情形只是 $M=I$ 的特例。这一视角也解释了为什么不是普通的 $x_i^T x_j=0$：正交性的定义跟着内积走，而这里的物理内积是 $M$-加权的。
> 这个结论的真正用途是给广义问题换一个最舒服的坐标系：把 $M$-正交基再按 $x_i^T M x_i=1$ 归一化，任何 $c=\sum_i\alpha_i x_i$ 的广义 Rayleigh 商变成 $R(c)=\sum_i\lambda_i\alpha_i^2/\sum_i\alpha_i^2$，于是广义特征值问题在此基下退化回注 25 的标准情形。正交性不是证明完就扔掉的副产品，它是把加权问题拉回最熟悉坐标系的施工图。物理验证：取 $M=\operatorname{diag}(m_1,m_2)$，$M$-内积 $x^T M y=m_1 x_1 y_1+m_2 x_2 y_2$ 是质量加权点积：重的质点发言权更大。若振动是两个模态的叠加 $x(t)=a\cos(\omega_i t)x_i+b\cos(\omega_j t)x_j$，总动能 $\frac12\dot x^T M\dot x$ 中的交叉项正比于 $x_i^T M x_j$；$M$-正交性就是模态之间没有动能耦合，总动能可拆成两个独立模态动能之和，工程模态分析正是以这种能量解耦为内核。这解释了 Example 1 中两个向量在普通欧氏意义下不垂直：欧氏点积对各坐标一视同仁，而物理系统按质量分配权重。
> 跨课程连接：模板在 Strang §I.7 中是 $M=I$ 的特例，即标准对称矩阵不同特征值的特征向量正交；在 18.065 中，SVD 的右奇异向量正是 $A^T A$ 的标准正交特征向量，左奇异向量正是 $A A^T$ 的标准正交特征向量——对称相减模板在 $M=I$ 时对这两个对称矩阵分别应用，直接给出两组奇异向量的正交性。一句话收束：把对称性翻译成矩阵可在点积中自由换边，是线性代数最高频的证明动作之一。
---


---

<!-- page 089: 书页 84, §I.10 续——Generalized Eigenvectors are M-orthogonal（Example 2）与 Positive Semidefinite M: Not Invertible -->

<span style="color:#2471a3;">**[example]**</span> **Example 2（例 2）**

求对应于 $\lambda_1 = 3+\sqrt{3}$ 与 $\lambda_2 = 3-\sqrt{3}$ 的特征向量。

特征向量 $\boldsymbol{x}$ 与 $\boldsymbol{y}$ 分别位于零空间（nullspace）之中，即满足 $(S-\lambda_1 M)\boldsymbol{x} = 0$ 与 $(S-\lambda_2 M)\boldsymbol{y} = 0$：

```math
S-\lambda_1 M = \begin{bmatrix} 4-(3+\sqrt{3}) & -2 \\ -2 & 4-2(3+\sqrt{3}) \end{bmatrix}
\quad \text{gives} \quad \boldsymbol{x} = c\begin{bmatrix} 2 \\ 1-\sqrt{3} \end{bmatrix}
```

```math
S-\lambda_2 M = \begin{bmatrix} 4-(3-\sqrt{3}) & -2 \\ -2 & 4-2(3-\sqrt{3}) \end{bmatrix}
\quad \text{gives} \quad \boldsymbol{y} = c\begin{bmatrix} 2 \\ 1+\sqrt{3} \end{bmatrix}
```

这两个特征向量 $\boldsymbol{x}$ 与 $\boldsymbol{y}$ 并不 orthogonal（正交），但它们 M-orthogonal（M-正交），因为：

```math
\boldsymbol{x}^T M \boldsymbol{y}
= \begin{bmatrix} 2 & 1-\sqrt{3} \end{bmatrix}
\begin{bmatrix} 1 & 0 \\ 0 & 2 \end{bmatrix}
\begin{bmatrix} 2 \\ 1+\sqrt{3} \end{bmatrix}
= 4 + 2(1-\sqrt{3})(1+\sqrt{3}) = 0
```

---

<span style="color:#2471a3;">**[section]**</span>

### Positive Semidefinite M: Not Invertible（半正定 M：不可逆）

在许多重要的 application（应用）中，矩阵 $M$ 只是 positive semidefinite（半正定）的。于是 $c^T M c$ 可能等于零！矩阵 $M$ 将不是 invertible（可逆）的。商（quotient）$c^T S c / c^T M c$ 可能变为无穷大。矩阵 $M^{-1/2}$ 与 $H$ 甚至根本不存在。特征值问题 $Sc = \lambda M c$ 仍然有待求解，但一个 infinite eigenvalue（无穷特征值）$\lambda$ 现在完全可能出现。

在 statistics（统计学）中，$M$ 常常是一个 covariance matrix（协方差矩阵）。它的对角元（diagonal entries）告诉我们两个或多个测量（measurements）各自的 variance（方差）；它的非对角元（off-diagonal entries）告诉我们"测量之间的 covariances（协方差）"。

如果我们愚蠢地精确重复同样的观测——或者如果某个 experiment（实验）完全由另一个实验决定——那么协方差矩阵 $M$ 就是 singular（奇异）的。它的 determinant（行列式）为零，因而不可逆。瑞利商（Rayleigh quotient）（其中要除以 $c^T M c$）可能变成无穷大。

从数学上看待这个问题的办法之一，是把 $Sc = \lambda M c$ 写成带 $\alpha$ 与 $\beta$ 的形式：

```math
\alpha Sc = \beta Mc \quad \text{其中} \quad \alpha \ge 0,\ \beta \ge 0,\ \text{特征值}\ \lambda = \alpha/\beta \tag{10}
```

如果 $\alpha > 0$ 且 $\beta > 0$，$\lambda = \alpha/\beta$ 就是一个普通的正特征值。我们甚至可以通过 $\alpha^2 + \beta^2 = 1$ 把这两个数 normalize（归一化）。但现在我们在方程（10）中看到另外三种可能：

- $\alpha > 0$ 且 $\beta = 0$：此时 $\lambda = \infty$，且 $Sc = 0$——这是 $S$ 的一个普通的零特征值（zero eigenvalue）；
- $\alpha = 0$ 且 $\beta > 0$：此时 $\lambda = 0$，且 $Mc = 0$——$M$ 不可逆；
- $\alpha = 0$ 且 $\beta = 0$：此时 $\lambda = 0/0$ 无法确定——$c = 0$，且同样有 $Sc = 0$。

$\alpha = 0$ 这种情况会在我们拥有 clusters of data（数据簇）时出现——如果某个簇中的 samples（样本）数小于我们测量的 features（特征）数。这就是 small sample size（小样本量）问题。它确实会发生。

你会理解，此处的数学变得更加 delicate（精细）。SVD 方法（当你把一个数据矩阵分解为 $A = U\Sigma V^T$，其中 singular vectors（奇异向量）$\boldsymbol{v}$ 来自 $S = A^T A$ 的特征向量）并不足够。我们需要 generalize（推广）SVD，需要允许出现第二个矩阵 $M$。这便引出了 GSVD。
> <span style="color:#7f8c8d;">Strang §I.10, p.84</span>

---

<!-- page 090: 书页 85, §I.10 续——The Generalized SVD (Simplified)（简化版广义奇异值分解） -->

<span style="color:#2471a3;">**[section]**</span>

### The Generalized SVD (Simplified)（简化版广义奇异值分解）

就其完全一般性（full generality）而言，这种 factorization（分解）是复杂的。它允许有两个矩阵 $S$ 与 $M$，并允许它们是 singular（奇异）的。在本书中，停留在通常且最佳的情形——即这两个 symmetric matrices（对称矩阵）是 positive definite（正定）的——是有意义的。那时我们就能看清 GSVD 的首要 purpose（目的）：同时 factor（分解）两个矩阵。

请记住，经典的 SVD 把一个 rectangular matrix（长方形矩阵）分解为 $UDV^T$。它是从 $A$ 开始的，而不是从 $S = A^T A$ 开始。类似地，这里我们从两个矩阵 $A$ 与 $B$ 出发。我们的 simplification（简化）是假设两者都是 rank（秩）为 $n$ 的 tall thin matrices（高瘦矩阵）。它们的大小分别是 $m_A \times n$ 与 $m_B \times n$。于是 $S = A^T A$ 与 $M = B^T B$ 都是 $n \times n$ 且正定的。

---

<span style="color:#2471a3;">**[definition]**</span> **Generalized Singular Value Decomposition（广义奇异值分解）**

$A$ 与 $B$ 可以分解为 $A = U_A \Sigma_A Z$ 与 $B = U_B \Sigma_B Z$（同一个 $Z$）：

这三条要求共同决定了 GSVD 的形状：$U_A$ 与 $U_B$ 各自作用于 $A$ 与 $B$ 的行空间，$\Sigma_A$ 与 $\Sigma_B$ 记录缩放，$Z$ 则把两者联系起来。

- $U_A$ 与 $U_B$ 是 orthogonal matrices（正交矩阵）（尺寸 $m_A$ 与 $m_B$）；
- $\Sigma_A$ 与 $\Sigma_B$ 是 positive diagonal matrices（正对角矩阵）（满足 $\Sigma_A^T \Sigma_A + \Sigma_B^T \Sigma_B = I_{n \times n}$）；
- $Z$ 是一个 invertible matrix（可逆矩阵）（尺寸 $n \times n$）。

注意，$Z$ 很可能不是一个 orthogonal matrix（正交矩阵）。那样要求就太高了。矩阵 $Z$ 的非凡性质在于 simultaneously diagonalize（同时对角化）$S = A^T A$ 与 $M = B^T B$：

```math
A^T A = Z^T (\Sigma_A^T \Sigma_A) Z \quad \text{与} \quad B^T B = Z^T (\Sigma_B^T \Sigma_B) Z \tag{11}
```

这个式子表明，同一个 $Z$ 同时把 $S = A^T A$ 与 $M = B^T B$ 化为对角矩阵 $\Sigma_A^T \Sigma_A$ 与 $\Sigma_B^T \Sigma_B$。

所以这是 linear algebra（线性代数）的一个事实：任意两个正定（positive definite）矩阵都能被同一个矩阵 $Z$ 对角化！这一点在 GSVD 被发明之前就已为人所知。而且，因为并不要求 orthogonality（正交性），我们可以 scale（缩放）$Z$，使得 $\Sigma_A^T \Sigma_A + \Sigma_B^T \Sigma_B = I$。我们还可以对它的列（columns）排序，把那些正数（在 $\Sigma_A$ 上的）按 decreasing order（递减顺序）排列。

因此 GSVD 的核心，是用一个 $Z$ 同时对角化两个正定矩阵，而不必分别对 $S$ 与 $M$ 作两次特征分解。

还请留意 "diagonalize（对角化）" 一词的含义。方程（11）并不包含 $Z^{-1}$ 与 $Z$，它包含的是 $Z^T$ 与 $Z$。有了 $Z^{-1}$，我们得到的是 similarity transformation（相似变换），它保持 eigenvalues（特征值）；有了 $Z^T$，我们得到的是 congruence transformation（相合变换）$Z^T S Z$，它保持 symmetry（对称性）。

> 于是 $S$ 与 $Z^T S Z$ 的特征值具有相同的符号。这就是 PSET III.2 中的 Sylvester's Law of Inertia（西尔维斯特惯性定律）。此处这些符号全部为正。

$S = A^T A$ 的对称性与 $M = B^T B$ 的正定性，使得同一个 $Z$ 能同时对角化这两个矩阵。习题集（Problem Set）中的 Problem 5 将引导你完成这个简化版 GSVD 的证明。

至此，简化版 GSVD 的三个要素——两个正交矩阵、两个正对角矩阵与一个公共可逆矩阵 $Z$——已经齐备。
> <span style="color:#7f8c8d;">Strang §I.10, p.85</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 设计问题：$S,M$ 两个正定矩阵各自都能被正交对角化，但两次用的是两个不同的正交矩阵，无法统一。简化版 GSVD 问的是：能否找一个公共可逆矩阵 $Z$，用同一个坐标变换把两个二次型同时变成无交叉项？第一性原理先认清相合变换的几何身份：令 $x=Zy$，则 $x^T S x=y^T(Z^T S Z)y$。所以 $Z^T S Z$ 不是线性映射的变换，而是二次型的换元——它保持二次型在每一点的符号与取值结构，却不保持特征值本身。这正是主教材强调的 congruence 与 similarity 的分野。还要先回答一个更尖锐的问题：为什么不能要求 $Z$ 正交？因为若正交矩阵 $Z$ 同时把 $S,M$ 对角化，则 $S=ZD_1Z^T$ 且 $M=ZD_2Z^T$，立即推出 $SM=ZD_1D_2Z^T=ZD_2D_1Z^T=MS$；反过来可交换的正定矩阵也有公共正交特征基。所以正交同时对角化只对可交换矩阵开放，我们这里必须放弃正交性才能覆盖任意两个正定矩阵。
> 证明可整理成三步流水线，模板名：先标准化一个，再对角化另一个。第一步用 $S$ 的谱分解 $S=Q\Lambda Q^T$ 得到 $Q^T S Q=\Lambda$。第二步用对角缩放 $D=\Lambda^{-1/2}$ 把 $S$ 变成单位阵：$(QD)^T S(QD)=D\Lambda D=I$。第三步，变换后的 $M'=(QD)^T M(QD)$ 仍对称正定——正定性在可逆相合变换下保持，因为 $y^T M' y=(QDy)^T M(QDy)>0$ 对任何 $y\neq0$ 成立——再对 $M'$ 做谱分解 $M'=Q_2\Lambda_2 Q_2^T$。合成 $Z=QDQ_2$ 后，$Z^T S Z=I$ 且 $Z^T M Z=\Lambda_2$。三步只用谱分解、对角缩放、正定性保持这些已会工具，没有任何黑箱。这里正定的作用要看清：若 $A$ 列秩亏，$S=A^T A$ 只是半正定，$\Lambda^{-1/2}$ 不存在，简化版需要先把问题压缩到列空间再走同样三步。
> 用这两个结果可以直接读出广义特征值：$Z^T S Z=I$ 给出 $S=Z^{-T}Z^{-1}$，$Z^T M Z=\Lambda_2$ 给出 $M=Z^{-T}\Lambda_2Z^{-1}$，于是 $M^{-1}S=Z\Lambda_2^{-1}Z^{-1}$，即 $M^{-1}S$ 相似于对角阵 $\Lambda_2^{-1}$。所以 $(S,M)$ 的广义特征值正是 $\Lambda_2^{-1}$ 的对角元，同一个 $Z$ 既完成了同时对角化，也把广义特征值全部摆在明面上。剩下的缩放自由度也值得算清楚：若已有 $Z^T S Z=D_1$ 与 $Z^T M Z=D_2$ 都是正对角阵，把 $Z$ 的第 $j$ 列乘以 $c_j$，则 $D_1$ 与 $D_2$ 的第 $j$ 个对角元同时乘以 $c_j^2$。于是选 $c_j=(d_{1j}+d_{2j})^{-1/2}$ 就能让两个新对角元之和为 $1$，这正对应 $\Sigma_A^T\Sigma_A+\Sigma_B^T\Sigma_B=I$：两组奇异值的平方在同一尺度上相加为一，保证彼此可比较。这里每列只有一个待定缩放参数，却要满足两个目标，之所以能同时做到，是因为两个目标被同一个 $c_j^2$ 同步控制——这是对角结构的红利。
> 思想实验：把 $x^T S x=1$ 与 $x^T M x=1$ 看成两个椭球。上述构造等于找到一个一般不垂直的斜坐标系，在其中第一个椭球变成单位球 $y^T y=1$，第二个变成坐标轴对齐的椭球 $y^T\Lambda_2 y=1$。两个椭球一般不能同时变成球，因为那要求 $Z^T S Z=Z^T M Z=I$，从而 $S=M$；一个球加一个轴对齐椭球是可达的最佳折中，这就是同时对角化的几何图景。跨课程连接：相合关系本身就是 6.042J 的等价关系——自反、对称、传递逐条可验——而 Sylvester 惯性定律说的是这个等价关系把对称矩阵分成的等价类恰好由惯性指标 $(n_+,n_-,n_0)$ 标记，这是等价关系加不变量分类的标准套路；本注的谱分解步骤直接复用 Strang §I.7，而 18.065 把这种同时约化用作比较两组数据的核心算法。一句话收束：GSVD 的本质不是对角化矩阵，而是给两个二次型找同一个换元坐标。
---

<!-- page 091: 书页 86, §1.10 续: Fisher's Linear Discriminant Analysis (LDA) -->

### Fisher's Linear Discriminant Analysis（LDA）

在 statistics（统计学）与 machine learning（机器学习）中有一个很不错的 application（应用）：我们拿到来自两个不同 population（总体）的 samples（样本），并且它们被混在了一起。关于每个总体，我们只知道一些基本事实——它的 average value（平均值）$m$，以及围绕这个 mean（均值）$m$ 的 average spread（平均离散程度）。

因此，第一个总体有 mean（均值）$m_1$ 与 variance（方差）$\sigma_1$，第二个总体有 $m_2$ 与 $\sigma_2$。如果所有样本都被混在一起、我们任取一个，那么它大概应该归类为总体 1 还是总体 2 呢？Fisher 的 "linear discriminant（线性判别）" 回答了这个问题。

实际上这个问题还要更复杂一步。每个样本有若干个 features（特征），例如一个孩子的 age（年龄）、height（身高）和 weight（体重）。在 machine learning 中，为每个样本配备一个 "feature vector（特征向量）" 是常规做法，比如 $v = (\text{age}, \text{height}, \text{weight})$。如果一个样本具有特征向量 $v$，它大概来自哪个总体？我们是从向量而非标量出发的。

对每个总体，我们有一个平均年龄 $m_a$、一个平均身高 $m_h$ 和一个平均体重 $m_w$。总体 1 的 mean（average，平均值）是一个向量 $m_1 = (m_{a1}, m_{h1}, m_{w1})$。总体 2 同样有一个由平均年龄、平均身高、平均体重构成的向量 $m_2$。而为了衡量每个总体围绕其均值的离散程度，方差变成了一个 $3 \times 3$ 矩阵 $\Sigma$。这个 "covariance matrix（协方差矩阵）" 将是第 V 章统计内容的关键。眼下，我们有 $m_1, m_2, \Sigma_1, \Sigma_2$，并且想要一条能在两个总体之间进行判别的规则。

费希尔（Fisher）的检验形式很简单：他提出一个向量 $v$。如果样本满足 $v^T f > c$，那么我们最好的猜测是总体 1；如果 $v^T f < c$，那么该样本很可能来自总体 2。向量 $v$ 试图（尽可能）把这两个总体分开，它最大化 separation ratio（分离比）$R$：

```math
R(v) = \frac{v^T S v}{v^T M v}
```

这个比值 $R$ 具有 $v^T S v / v^T M v$ 的形式。矩阵 $S$ 是 $(m_1 - m_2)(m_1 - m_2)^T$，矩阵 $M$ 是 $\Sigma_1 + \Sigma_2$。我们已知这样的规则：使分离比最大的向量 $v$ 满足 generalized eigenvalue（广义特征值）方程 $S v = \lambda M v$。

费希尔（Fisher）确实能找出 $M^{-1}S$ 的这个 eigenvector（特征向量）$v$，我们同样可以，因为矩阵 $S = (m_1 - m_2)(m_1 - m_2)^T$ 的 rank（秩）为 1，所以 $S v$ 始终指向 $m_1 - m_2$ 的方向。于是，为了成立 $S v = \lambda M v$，$M v$ 必须也在这个方向上，从而得到 $v = M^{-1}(m_1 - m_2)$。

这是一个很漂亮的例子，因为我们找到了特征向量。这也合情合理：当未知样本具有特征向量 $f = (\text{age}, \text{height}, \text{weight})$ 时，我们自然会关注 $v^T f$、$m_1^T f$ 与 $m_2^T f$ 这些数值。如果我们准备好进行完整的统计学讨论（我们还没有），就能看出 weighting matrix（权重矩阵）$M = \Sigma_1 + \Sigma_2$ 是如何进入基于 $v^T f$ 的最终检验的。这里只需说明：来自两个总体的特征向量 $f$，被一个垂直于 $v = M^{-1}(m_1 - m_2)$ 的平面分离得尽可能好。

我们在三维 feature space（特征空间）中有两团点。我们试图用一个平面把它们分开——这并非总能做到。Fisher 提出了一个合理的平面。神经网络则通过允许采用并非平面的 separating surfaces（分离曲面）而获得成功。

---

> <span style="color:#1e8449;">**译者注**</span>：本节是 §1.10（Rayleigh Quotients and Generalized Eigenvalues，瑞利商与广义特征值）的统计应用。LDA 把两个总体之间的判别问题化为广义特征值问题 $S v = \lambda M v$：$S$ 捕捉 between-class scatter（类间散布），$M = \Sigma_1 + \Sigma_2$ 捕捉 within-class scatter（类内散布），最优方向即 $v = M^{-1}(m_1 - m_2)$。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 设计问题：为什么判别准则必须是比值，而不是投影后的均值差本身？因为方向 $v$ 的尺度没有意义：$v$ 与 $2v$ 给出同一条判决直线，只是阈值 $c$ 翻倍。任何合理准则都必须对 $v$ 的缩放不变，即它是零次齐次函数；分子分母各是 $v$ 的二次型，比值恰好把尺度约掉。这一观察把找方向的问题自动归入广义 Rayleigh 商框架：分子放我们想要的类间分离，分母放我们要压制的类内噪声，问题结构自己浮出水面。
> 第一性原理从投影的矩入手。投影后一维数据的均值是 $v^T m_i$，方差是 $v^T\Sigma_i v$——后者正是 6.042J 中方差概念的向量升级：方差从标量的二阶中心矩变成方向上的二次型，量的是数据沿 $v$ 方向铺开的平均平方距离。于是分子 $(v^T(m_1-m_2))^2$ 写成 $v^T S v$，其中 $S=(m_1-m_2)(m_1-m_2)^T$ 是秩一外积；分母是 $v^T(\Sigma_1+\Sigma_2)v$。$R(v)$ 就是投影后的信噪比：信号是均值差的平方，噪声是两类方差之和。用 Lagrange 乘子可一步确认最优性条件：在约束 $v^T M v=1$ 下最大化 $v^T S v$，令 $L=v^T S v-\lambda(v^T M v-1)$，梯度为零给出 $2Sv-2\lambda Mv=0$，即 $Sv=\lambda Mv$——这正是注 25 中“驻点条件等价于特征方程”的广义版本。
> 秩一带来的红利值得单独命名，模板：秩一外积即单方向投影。$S v=(m_1-m_2)[(m_1-m_2)^T v]$，中括号是标量，故 $S v$ 永远落在 $m_1-m_2$ 这一条直线上。广义特征方程 $Sv=\lambda Mv$ 于是强制 $Mv$ 也落在这条直线上，直接读出 $v\propto M^{-1}(m_1-m_2)$，把一个 $n$ 维特征值问题降成一次 $n\times n$ 线性方程组求解，比求全部特征向量便宜得多。再用注 26 的对称化眼光：令 $u=M^{1/2}v$，准则化为 $u^T H u/u^T u$，其中 $H=M^{-1/2}SM^{-1/2}$ 的顶特征向量是 $u\propto M^{-1/2}(m_1-m_2)$，所以最优方向等于先把噪声白化、再连接两均值——先除以类内尺度，再对准类间方向。
> 一个坐标系不变性验证：若特征向量整体作可逆线性变换 $f'=Af$，则均值变成 $Am_i$，协方差变成 $A\Sigma_i A^T$，最优方向变成 $v'=(A(\Sigma_1+\Sigma_2)A^T)^{-1}A(m_1-m_2)=A^{-T}v$。于是判决值 $v'^T f'=(A^{-T}v)^T(Af)=v^T f$ 保持不变——这正是线性代数中向量随基变换的逆变律，说明 LDA 的判决规则不依赖特征坐标系的线性改换。
> 贝叶斯验证：当 $\Sigma_1=\Sigma_2=\Sigma$ 且先验相等时，两个高斯密度的对数比中二次项 $f^T\Sigma^{-1}f$ 恰好相消，剩下的线性项正比于 $(m_1-m_2)^T\Sigma^{-1}f$；判决边界 $v^T f=c$ 就是两类后验概率相等的面，$c$ 与 $\frac12 v^T(m_1+m_2)$ 只差一个常数因子，先验相等时边界恰好落在两个投影均值的正中间。这与 Fisher 的几何解一致，说明最大信噪比与最小错误率线性规则在等协方差高斯下重合；先验不等时阈值会向先验更大的那一类移动，但方向 $v$ 不变。Fisher 1936 年使用的鸢尾花数据至今仍是入门基准，正因为它三个物种中一个线性可分、另两个接近重叠，恰好暴露线性判别的能力边界。跨课程连接：6.042J 的期望线性与方差公式 $\operatorname{Var}(a^T X)=a^T\Sigma a$ 是整条链的起点；Strang §I.10 提供广义特征值工具；18.065 把它推广到多类判别，多类情形需要对类间与类内散布矩阵同时求多个广义特征对。一句话收束：LDA 的全部数学，就是把方差重新理解为方向上的二次型。
---


---

<!-- page 092: 书页 87, Problem Set 1.10 -->

### 1.10 · Rayleigh Quotients and Generalized Eigenvalues

#### Problem Set 1.10

<span style="color:#2471a3;">**[problem]**</span> **Problem 1.** Solve $(S - \lambda M)c = 0$ and $(H - \lambda I)c = 0$ after computing the $m \times m$ matrix $H = M^{-1/2} S M^{-1/2}$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 2.** Step 1 is to find $\lambda_1$ and $\lambda_2$ from $\det(S - \lambda M) = 0$. The equation $\det(H - \lambda I) = 0$ should produce the same $\lambda_1$ and $\lambda_2$. Those eigenvalues will produce two eigenvectors $c_1$ and $c_2$ of $S - \lambda M$ and two eigenvectors $x_1$ and $x_2$ of $H - \lambda I$. Verify that $c_2$ is not zero but $c_2^T M c_1 = 0$. $H$ is symmetric so $x_1^T x_2 = 0$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 3.**

(a) For $v = (a, b)$ and $f = (c, d)$ write the Rayleigh quotients in Problem 1 as

```math
R_1(v) = \frac{v^T S v}{5a^2 + 8ab + 5b^2} \qquad \text{and} \qquad R_2(f) = \frac{f^T H f}{5c^2 + 16cd + 20d^2}
```

(b) Take the $c$ and $d$ derivatives of $R_2(c, d)$ to find its maximum and minimum.

(c) Take the $a$ and $b$ derivatives of $R_1(a, b)$ to find its maximum and minimum.

(d) Verify that those maxima occur at eigenvectors from $(S - \lambda M)c = 0$ and $(H - \lambda I)f = 0$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 4.** How are the eigenvectors $c_1$ and $c_2$ related to the eigenvectors $x_1$ and $x_2$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 5.** Change $M$ to a singular matrix and solve $Sc = \lambda Mc$. Now $M$ is singular and one of the eigenvalues is infinite. But its eigenvector $c_2$ is still $M$-orthogonal to the other eigenvector $c_1$.

> <span style="color:#1e8449;">**译者注**</span>：原题此处给定了具体的奇异矩阵 $M$，因 OCR 缺失而以 "a singular matrix" 泛化表述，题意不变。

<span style="color:#2471a3;">**[problem]**</span> **Problem 6.** Start with symmetric positive definite matrices $S$ and $M$. Eigenvectors of $S$ fill an orthogonal matrix $Q$ so that $Q^T S Q = \Lambda$ is diagonal. What is the diagonal matrix $D$ so that $D^T \Lambda D = I$? Now we have $D^T Q^T S Q D = I$ and we look at $D^T Q^T M Q D$.

<span style="color:#2471a3;">**[problem]**</span> **Problem 7.** Its eigenvector matrix $Q_2$ gives $Q_2^T (D^T Q^T M Q D) Q_2 = \Lambda_2$. Now $Z = Q D Q_2$ diagonalizes both congruences $Z^T S Z$ and $Z^T M Z$ — the GSVD.

<span style="color:#2471a3;">**[problem]**</span> **Problem 8.**

(a) Why does every congruence $Z^T S Z$ preserve the symmetry of $S$?

(b) Why is $Z^T S Z$ positive definite when $S$ is positive definite and $Z$ is square and invertible? Apply the energy test to $Z^T S Z$. Be sure to explain why $Zc$ is not the zero vector.

<span style="color:#2471a3;">**[problem]**</span> **Problem 9.** Which matrices $Z^T I Z$ are congruent to the identity matrix for invertible $Z$?

<span style="color:#2471a3;">**[problem]**</span> **Problem 10.** Solve this matrix problem basic to Fisher's Linear Discriminant Analysis: If $R(c) = \dfrac{c^T S c}{c^T M c}$ and $S = (m_1 - m_2)(m_1 - m_2)^T$, what vector $c$ minimizes $R(c)$?

> <span style="color:#1e8449;">**译者注**</span>：原题中 $S$ 的表达式为 OCR 缺失，此处按正文 §1.10 的 Fisher's LDA 定义补全为 $(m_1 - m_2)(m_1 - m_2)^T$。题 1–4 练习广义特征值 $S v = \lambda M v$ 与对称化矩阵 $H = M^{-1/2} S M^{-1/2}$ 的等价处理；题 5 考察奇异 $M$ 情形下特征向量仍保持 $M$-正交；题 6–7 通向 generalized SVD, GSVD（广义奇异值分解）；题 10 直接对应正文的 Fisher's LDA。

---

<!-- page 093: 书页 88, §I.11 Norms of Vectors and Functions and Matrices -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.11 向量、函数与矩阵的范数（Norms of Vectors and Functions and Matrices）</span>

我们先从三种特殊的范数（norm）开始——它们远为最重要。这三种范数就是 2 范数（2 norm）、1 范数（1 norm）和 ∞ 范数（∞ norm）。

一个向量 $v$ 的范数是一个正数 $\|v\|$。这个数度量的是向量的"长度"（length）。长度的有用度量方式有很多种（也就是很多不同的范数）。

<span style="color:#2471a3;">**[definition]**</span> 每一个针对向量（vectors）、函数（functions）或矩阵（matrices）的范数，都必须共享一个数 $v$ 的绝对值（absolute value）$|v|$ 所具有的下面两个性质：

**乘以 $c$（缩放 Rescaling）**——所有范数都必须满足

```math
\|cv\| = |c| \, \|v\|
```

**加上 $w$（三角不等式 Triangle inequality）**

```math
\|v + w\| \leq \|v\| + \|w\|
```

<span style="color:#2471a3;">**[definition]**</span> 向量 $v = (v_1, \ldots, v_n)$ 的三种重要范数如下（若 $v$ 是复向量（complex），$|v_i|$ 表示复数 $v_i$ 的模）：

```math
\|v\|_2 = (|v_1|^2 + \cdots + |v_n|^2)^{1/2} \qquad \text{2 范数（欧几里得范数 Euclidean norm）}
```

```math
\|v\|_1 = |v_1| + \cdots + |v_n| \qquad \text{1 范数}
```

```math
\|v\|_\infty = \max_i |v_i| \qquad \text{∞ 范数（最大范数 max norm）}
```

<span style="color:#2471a3;">**[example]**</span> 全 1 向量 $v = (1, 1, 1)$ 的三个范数分别是 $\|v\|_1 = 3$、$\|v\|_2 = \sqrt{3}$ 和 $\|v\|_\infty = 1$。

这三种范数正是下述 $p$ 范数（$p$-norm）取 $p = 2$、$p = 1$、$p = \infty$ 时的特例：

```math
\|v\|_p = (|v_1|^p + \cdots + |v_n|^p)^{1/p}
```

图 L15 展示了范数为 1 的向量集合（$\|v\|_p = 1$），即单位圆在不同范数下的形状：

- $p = 1$：$|v_1| + |v_2| = 1$，得到菱形（diamond）
- $p = \infty$：$|v_1| \leq 1$，$|v_2| \leq 1$，得到正方形（square）
- $p = 2$：$\sqrt{v_1^2 + v_2^2} = 1$，得到圆（circle）
- $p = 1/2$：$|v_1|^{1/2} + |v_2|^{1/2} = 1$，不是凸的（not convex）——因此是非法的（illegal）

> <span style="color:#7f8c8d;">图 L15：重要的向量范数 $\|v\|_1$、$\|v\|_2$、$\|v\|_\infty$，以及一个失败的情形——$p = 1/2$ 太小了。</span>

$p = 1/2$ 的失败出在三角不等式上：$(1, 0)$ 和 $(0, 1)$ 的范数都是 $1$，但它们的和 $(1, 1)$ 的范数是 $2^{1/p} = 4$，大于 $2$，因而违反了三角不等式。只有当 $1 \leq p \leq \infty$ 时才产生一个可接受的范数 $\|v\|_p$。
> <span style="color:#7f8c8d;">Strang §I.11, p.88</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 设计问题：$p=1/2$ 时正定性与齐次性都成立，为什么偏偏三角不等式崩了？第一性原理的答案是：三角不等式等价于单位球是凸集。两个方向都值得亲手验一遍。正方向：若 $\|u\|\le1$、$\|w\|\le1$ 且 $0\le t\le1$，则 $\|tu+(1-t)w\|\le t\|u\|+(1-t)\|w\|\le1$，故单位球内任意两点的连线仍留在球内。反方向：设单位球凸，任取非零 $v,w$，把 $v/\|v\|$ 与 $w/\|w\|$ 作凸组合，权重 $t=\|v\|/(\|v\|+\|w\|)$，所得点恰好是 $(v+w)/(\|v\|+\|w\|)$；凸性保证其范数不超过 $1$，移项即得三角不等式。所以范数与以原点为内点、关于原点对称的有界凸体是同一件事的两种说法：前者给代数，后者给几何。这里“有界”对应的是正定性——“有界”保范数不为零，否则凸体无限伸展的方向会把非零向量量成零；“关于原点对称”对应齐次性里的因子 $-1$ 情形。三条公理各自在几何上认领了一个岗位。
> 先看 $p\ge1$ 时三角不等式为什么成立，这能反衬 $p=1/2$ 的失败。$p=1$：$|v_i+w_i|\le|v_i|+|w_i|$ 逐坐标相加即可。$p=2$：展开 $\|v+w\|_2^2=\|v\|_2^2+2v^T w+\|w\|_2^2\le\|v\|_2^2+2\|v\|_2\|w\|_2+\|w\|_2^2=(\|v\|_2+\|w\|_2)^2$，中间那一步就是你已会用的 Cauchy-Schwarz。$p=\infty$：$\max_i|v_i+w_i|\le\max_i|v_i|+\max_i|w_i|$，取最大值的下标逐个夹住即可。一般的 $p>1$ 需要 Hölder 不等式这条 Cauchy-Schwarz 的推广，现在只需知道你的脚手架正是它的特例。
> 具体验证 $p=1/2$：单位球 $|v_1|^{1/2}+|v_2|^{1/2}=1$ 在 $(1,0)$ 与 $(0,1)$ 之间向原点凹陷（图 L15）。取两个端点的中点 $(1/2,1/2)$：其 $p=1/2$ 范数为 $(\sqrt{1/2}+\sqrt{1/2})^2=2$，而端点范数各为 $1$，凸组合的范数 $2$ 大于 $\frac12\cdot1+\frac12\cdot1=1$，三角不等式被违反。边界在第一象限的方程是 $y=(1-\sqrt{x})^2$，其二阶导数为 $\frac12 x^{-3/2}>0$，是凸函数，图像躺在弦线下方——球体沿对角线方向被削去一块，中点连线自然穿出球外。更一般地，齐次性意味着整个范数由单位球唯一决定：$\|v\|$ 就是把 $v$ 缩放到单位球边界所需的倍数；球有凹陷，正是三角不等式失效的几何画面。
> 回到图 L15 的四个图形：$p=2$ 是处处光滑的圆，$p=1$ 的菱形与 $p=\infty$ 的正方形都在顶点处带尖角，$p=1/2$ 则是向里凹的星形。尖角不是缺陷——下一页注 31 会看到，正是尖角让 $\ell_1$ 最小化天然产生稀疏解；而凹陷是致命的，因为它破坏凸性，从而破坏三角不等式。两类不光滑一正一邪：凸多面体的尖角是好的，非凸的凹陷是坏的。
> 跨课程连接：范数通过 $d(x,y)=\|x-y\|$ 生成度量，度量再给出开球、收敛与连续——这正是你在 TBB 实分析里见到的从代数结构到拓扑结构的桥。TBB §13.2–§13.4 的等价范数定理保证：有限维空间里 $\ell_1,\ell_2,\ell_\infty$ 的单位球形状虽不同但彼此嵌套，同一序列在任一范数下收敛与否一致（证明骨架：单位球面紧致，另一范数在其上连续故取到正的最小值与最大值）。但到无穷维这条定理失效：取前 $n$ 项为 $1$、其余为 $0$ 的无穷序列，其 $\ell_\infty$ 范数恒为 $1$，$\ell_1$ 范数为 $n$，比值无界，故不存在常数 $c$ 使 $\|x\|_1\le c\|x\|_\infty$。这就是 page_096 必须区分 $\ell_1,\ell_2,\ell_\infty$ 与函数空间版本 $L^1,L^2,L^\infty$ 的深层原因：$L^p$ 用积分 $\left(\int|f|^p\right)^{1/p}$ 量函数大小，但它的严格定义要等测度论，现在只需知道序列空间与函数空间是两套对象。一句话收束：有限维里范数是口味问题（收敛不变），无穷维里范数是硬度问题（空间本身随范数改变）。
---


---

<!-- page 094: 书页 89, §I.11 Norms of Vectors and Functions and Matrices -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.11（续）向量、函数与矩阵的范数</span>

### 直线 $3v_1 + 4v_2 = 1$ 上 $\|v\|_p$ 的最小值

哪个点在对角线（diagonal line）$3v_1 + 4v_2 = 1$ 上离 $(0, 0)$ 最近？答案（以及"最近（closest）"一词的含义）将取决于所用的范数。这是看待 1 范数与 2 范数、∞ 范数之间重要差异的另一种方式。我们即将看到一个非常特殊性质的第一个例子：

> 在 1 范数下的极小化（minimization）会产生稀疏解（sparse solutions）。

为了找到离 $(0, 0)$ 最近的点，把菱形、圆和正方形扩张（expand），直到它们触碰到那条对角线。对每一种范数，那个接触点 $v^*$ 将解出我们的优化问题（optimization problem）：在直线 $3v_1 + 4v_2 = 1$ 上的向量 $v = (v_1, v_2)$ 中，极小化 $\|v\|_p$：

```math
\min \|v\|_p
```

对 1 范数，解是 $v^* = (0, \tfrac{1}{4})$，有 $\|v^*\|_1 = \tfrac{1}{4}$；对 2 范数，解是 $v^* = (\tfrac{3}{25}, \tfrac{4}{25})$，有 $\|v^*\|_2 = \tfrac{1}{5}$；对 ∞ 范数，解是 $v^* = (\tfrac{1}{7}, \tfrac{1}{7})$，有 $\|v^*\|_\infty = \tfrac{1}{7}$。

> <span style="color:#7f8c8d;">图 L16：1 范数、2 范数和 ∞ 范数极小化问题的解 $v^*$。第一个解是稀疏的（sparse）。</span>

第一幅图展示了 1 范数问题的极小化解的一个非常重要的性质：这个解 $v^*$ 含有零分量（zero components）。向量 $v^*$ 是"稀疏的"。

这是因为菱形在一个尖点（sharp point）处碰到直线。直线（或高维中的超平面 hyperplane）包含满足约束（constraints）$Ax = b$ 的那些向量。菱形的表面包含具有相同范数的向量。菱形扩张着去和直线相遇——恰好相遇在菱形的一个角（corner）上！

习题集（Problem Set）以及后面的 §III.4 将回到这个"基追踪（basis pursuit）"问题以及与之密切相关的各个问题。

核心要点是：这些问题的解是稀疏的。它们只有很少的非零分量（nonzero components），而且这些分量具有意义。相比之下，最小二乘（least squares）解（使用 2 范数）有许多小的、不令人感兴趣的分量。经过平方（squaring），那些分量变得非常小，几乎不影响距离。

最后一个观察："0 范数"（0 norm）统计一个向量的非零分量的个数。但它并不是真正的范数。满足 $\|v\|_0 \leq 1$ 的点位于坐标轴上——只有一个非零分量。当 $p = 0$ 时，上一页的图形会变得更加极端——只是沿两个坐标轴的一个十字（cross）或骨架（skeleton）。

当然这个骨架完全不凸（convex）。"零范数"违反了范数的基本要求 $\|cv\| = |c| \, \|v\|$。而零范数的定义是

```math
\|v\|_0 = \text{非零分量的个数}
```

精彩的观察是：我们能够用 1 范数找到 $Ax = b$ 的最稀疏解（sparsest solution）。我们已把沿两个坐标轴的那个 0 骨架"凸化了（convexified）"。我们填满了那个骨架，结果就是 1 范数的菱形。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> 把这条注记当作一个可复用模板来记：**凸包松弛模板**——面对一个组合计数式的目标（$\ell_0$），先画出它的单位球，再取凸包，就得到离它最近的可解凸目标（$\ell_1$）。为什么“取凸包”恰好给出菱形？一个集合的凸包，就是把这个集合里任意有限个点做非负加权平均（权重加起来为 1）所得全部点的集合。$\ell_0$ 单位球由坐标轴骨架上的 $\pm e_1,\ldots,\pm e_n$ 构成，把这些点拿去做加权平均：第 $i$ 个坐标只能来自 $+e_i$ 与 $-e_i$ 的贡献相互抵消，其绝对值被分配给这两个顶点的权重之和控制，而所有权重总和不超过 1，于是得到的所有向量恰好满足 $\sum|x_i|\le1$。菱形就是骨架的凸包。高维的 $\ell_1$ 单位球是交叉多面体：由 $\pm e_i$ 这 $2n$ 个顶点围成，每个顶点只有 1 个非零坐标。这个模板的关键是：凸化把“数非零个数”这种不可微、不凸的计数，替换成“绝对值之和”这种分段线性凸函数，后者可用线性规划高效求解。原注说接触点“几乎必然”落在顶点，直觉是：膨胀的菱形要与直线相切，只有直线的法方向恰好与菱形某条边的法方向完全平行时才会撞在边上，这要求一个方向精确取到某个值，相当于在连续的角度集合中抽中一个点，概率为零；其余情形都是角先撞线。
> 思想实验：把二维坐标轴十字骨架想象成四根在原点相连的铁丝，用一根橡皮筋绷紧套住它们，橡皮筋收缩后的边界正是菱形——四个尖角分别落在四个坐标方向。换成三维，$\ell_1$ 单位球是正八面体，六个顶点是 $\pm e_1,\pm e_2,\pm e_3$；此时 $Ax=b$ 是一个平面，膨胀的正八面体几乎总是先以一个顶点碰到平面，于是解里至多一个坐标非零，其余两个坐标自动为零。维度越高，顶点的“尖”越极端：$n$ 维顶点只有 1 个非零坐标，其余 $n-1$ 个全是零，稀疏性自动出现。对比 $\ell_2$：球面处处光滑，任何方向都是圆的，接触点的坐标通常同时非零且大小相仿——这正是正文所说最小二乘解“有许多小而无聊的分量”的几何来源。
> 跨课程连接：这条几何直觉在本书 §III.4 基追踪与 §III.5 压缩感知中落地为算法。联系 CSAPP 第 2 章的 IEEE 754：最小二乘把分量平方后再求和，$10^{-10}$ 量级的分量平方后是 $10^{-20}$，把它加进量级为 1 的和里会被舍入吞掉（双精度机器精度约 $10^{-16}$），小分量的信息被平方操作挤压到可表示范围之外；而 $\ell_1$ 直接对绝对值求和，线性尺度不挤压小分量，从数值角度也更尊重“小但可能重要”的信号。联系 CLRS 的分治视角：稀疏解把 $n$ 维问题压缩到 $k$ 个非零坐标，等价于先做变量选择、再在选出的坐标上做估计，LASSO 一次求解同时完成这两件事，机制正在于此。一句话收束：膨胀的菱形先撞角，撞角即稀疏；凸包把不可解的计数问题变成可解的凸问题。
---


---

<!-- page 095: §I.11 续, Inner Products and Angles（内积与夹角）/ Inner Products and S-Norms（内积与 S-范数）; 正文页 -->

> <span style="color:#7f8c8d;">Highlights of Linear Algebra（线性代数亮点）</span>

<span style="color:#2471a3;">**[section]**</span>
#### Inner Products and Angles（内积与夹角）

一个 norm（范数）占据着特殊的位置。当我们不带下标地写 $\|v\|$ 时，指的就是这个范数。它把 inner product（内积）$(v, w)$ 与向量 $v$、$w$ 之间的 angle（夹角）$\theta$ 同普通的几何联系了起来：

```math
\|v\|^2 = (v, v) \qquad \text{length squared（长度平方）}
```

```math
(v, w) = \|v\|\,\|w\|\cos\theta \qquad \text{inner product（内积）：向量 } v \text{ 与 } w \text{ 的夹角 } \theta \tag{3}
```

当 $\theta = 90^\circ$、$\cos\theta = 0$ 且 $(v, w) = 0$ 时，$v$ 就 orthogonal（正交）于 $w$：

```math
v \perp w \iff \cos\theta = 0 \iff (v, w) = 0 \tag{4}
```

上述联系 (3) 与 (4) 引出了数学中最重要的不等式（inequality）：

**Cauchy-Schwarz（柯西-施瓦茨）不等式**：

```math
|v \cdot w| \le \|v\|\,\|w\| \tag{5}
```

习题集（Problem Set）中给出了 Cauchy-Schwarz 的直接证明。在正文里，我们把它与方程 (4) 中的余弦联系起来：$|\cos\theta| \le 1$ 意味着 $|v \cdot w| \le \|v\|\,\|w\|$。而这又进而引出方程 (2) 中的 angle inequality（夹角不等式）——它把普通三角形中 $\|v\|$、$\|w\|$ 与 $\|v+w\|$ 这三条边联系了起来：

```math
\|v+w\|^2 = \|v\|^2 + 2(v, w) + \|w\|^2 \qquad \text{Equality（等式）}
```

```math
\|v+w\|^2 \le \|v\|^2 + 2\|v\|\,\|w\| + \|w\|^2 = (\|v\| + \|w\|)^2 \qquad \text{Inequality（不等式）}
```

这证实了我们的直觉：三角形中任意一条边的长度都小于另外两条边长度之和：$\|v+w\| \le \|v\| + \|w\|$。只有当三角形被完全压平时，范数中的 equality（等号）才可能成立，此时所有夹角都满足 $|\cos\theta| = 1$。

---

<span style="color:#2471a3;">**[section]**</span>
#### Inner Products and S-Norms（内积与 S-范数）

关于 vector norm（向量范数），第一个要问的问题是：$\|v\|_2$ 是唯一与 inner product（内积，即 dot product（点积））以及夹角相联系的范数吗？对 $\ell_1$ 和 $\ell_\infty$ 并不存在 dot product（点积）。但我们能找到与其它范数相匹配的其它 inner product（内积）：

任选一个 symmetric positive definite matrix（对称正定矩阵）$S$：

```math
\|v\|_S^2 = v^T S v \qquad \text{给出 } v \in \mathbb{R}^n \text{ 上的范数（称为 S-norm（S-范数））} \tag{6}
```

```math
(v, w)_S = v^T S w \qquad \text{给出 } v, w \in \mathbb{R}^n \text{ 上的 S-inner product（S-内积）} \tag{7}
```

由 $(v, w)_S$ 定义的内积与 (4) 中的夹角一致；由 (5) 得到的不等式（Cauchy-Schwarz 与三角不等式）对它依然成立——(5) 的证明对任何范数都有效，只要每个范数都包含矩阵 $S$。

我们知道，每个 positive definite matrix（正定矩阵）$S$ 都可以分解为 $A^T A$。于是，对 $v$ 与 $w$ 而言，S-norm（S-范数）与 S-inner product（S-内积）恰好就是 $Av$ 与 $Aw$ 的标准 2-norm（二范数）与标准 inner product（内积）：




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 把这个证明命名为**判别式模板**：要证一个内积不等式，先构造一个显含待证量的非负二次函数，再用判别式非正来收网。第一性原理只有两条。其一，内积的正定性给出 $\|v-tw\|^2\ge0$ 对一切实数 $t$ 成立；其二，二次函数 $at^2+bt+c$（$a>0$）在整个实轴上非负，当且仅当判别式 $\Delta=b^2-4ac\le0$——否则它有两个实根，在两根之间函数值为负。把 $f(t)=\|v-tw\|^2$ 按范数平方展开，一次项系数与常数项正好把 $(v,w)$、$\|v\|^2$、$\|w\|^2$ 组装出来，于是“非负”这个几何事实瞬间翻译成代数不等式 $(v,w)^2\le\|v\|^2\|w\|^2$。逐项写出更清楚：$f(t)=t^2\|w\|^2-2t(v,w)+\|v\|^2$，即 $a=\|w\|^2$、$b=-2(v,w)$、$c=\|v\|^2$，判别式 $\Delta=4(v,w)^2-4\|v\|^2\|w\|^2\le0$，移项即得。退化情形也要处理：$w=0$ 时 $a=0$，二次函数退化成常数 $\|v\|^2\ge0$，不等式两边都是 $0$，结论平凡成立——TBB 式的严谨会单独抠出这一点。等号情形也由模板顺带解决：判别式为零意味着 $f$ 有重根 $t_0$，即 $\|v-t_0 w\|^2=0$，再由正定性得 $v=t_0 w$，两向量共线。同一模板再走一步就是三角不等式：$\|v+w\|^2=\|v\|^2+2(v,w)+\|w\|^2\le\|v\|^2+2\|v\|\|w\|+\|w\|^2=(\|v\|+\|w\|)^2$，两边开方即得——所以 Cauchy-Schwarz 与三角不等式是同一条判别式的两个直接推论，这也是 TBB 里内积空间的标配推导。这个模板的力量在于它不挑坐标系、不挑具体内积：只要空间里有满足正定性的内积，整个证明原样照搬。
> 思想实验：把同一模板用在概率空间。设 $X,Y$ 是期望有限的随机变量，以协方差 $\operatorname{Cov}(X,Y)=\mathbb{E}[(X-\mu_X)(Y-\mu_Y)]$ 为内积。对任意实数 $t$，方差非负：$\operatorname{Var}(X-tY)=\operatorname{Var}(X)-2t\operatorname{Cov}(X,Y)+t^2\operatorname{Var}(Y)\ge0$。这又是一个关于 $t$ 的非负二次函数，判别式非正直接给出 $\operatorname{Cov}(X,Y)^2\le\operatorname{Var}(X)\operatorname{Var}(Y)$，即相关系数 $\rho=\operatorname{Cov}/(\sigma_X\sigma_Y)$ 落在 $[-1,1]$。取 $X$ 在 $\pm1$ 上均匀取值、$Y=X$，则 $\rho=1$，对应“夹角余弦为 1”；取 $Y=-X$ 则 $\rho=-1$。再加一个“正交”情形：$X,Y$ 独立时 $\operatorname{Cov}(X,Y)=0$、$\rho=0$，对应夹角 $90^\circ$。等号条件的概率版本同样由重根传递：$\rho=\pm1$ 当且仅当 $Y$ 是 $X$ 的仿射函数（以概率 1 成立），即存在 $a,b$ 使 $Y=aX+b$——这正是 $v=tw$ 在随机变量语言里的化身。你在 6.042J 概率论里学到的相关系数界限，其代数内核就是这条判别式模板——它与欧氏空间的 Cauchy-Schwarz 是同一个证明在概率空间里的第二次出现。
> 回到本节正文：S-范数无非是给空间换了一把尺子。因为正定矩阵 $S$ 可分解为 $A^T A$，所以 $(v,w)_S=v^T S w=(Av,Aw)$，即 S-内积就是把向量先经过线性映射 $A$、再取标准点积；于是正文 (5) 的全部不等式对 S-范数自动成立，因为它们对 $Av$、$Aw$ 已经成立。给个具体数字：取 $S=\operatorname{diag}(4,9)$，即 $A=\operatorname{diag}(2,3)$，则 $\|v\|_S=\sqrt{4v_1^2+9v_2^2}$ 就是先把坐标按 $(2,3)$ 拉伸再取欧氏长度。$v=(1,1)$、$w=(1,-1)$ 时，$(v,w)_S=4-9=-5$，$\|v\|_S^2=\|w\|_S^2=13$，不等式断言 $25\le169$ 成立——这两个向量在标准内积下本应垂直，S-度量把它们掰成了钝角，说明 Cauchy-Schwarz 只认内积公理，不认具体几何形状。你已在 TBB 实分析中把范数公理当工具使用，而这里它们成了证明的唯一原料——这正说明好的公理系统会反复产出结论。到本书后面处理加权最小二乘与正则化时，$S$ 取加权矩阵或协方差矩阵的情形会一再出现，Cauchy-Schwarz 只是这套语言的第一课。一句话收束：记住判别式模板——把不等式包装成“某平方和恒非负”，再用判别式收网。
---


---

<!-- page 096: §I.11 续, Norms and Inner Products of Functions（函数的范数与内积）; 正文页 -->

承接上页：每个正定矩阵 $S$ 的分解 $S = A^T A$ 使我们得到：

```math
(v, w)_S = (Sv)^T w = (Av)^T (Aw) \qquad \text{because } S = A^T A \tag{8}
```

这个想法并不令人惊艳，但很便利。矩阵 $S$ 与 $S^{1/2}$ 是在对向量及其长度进行"加权（weighting）"。于是，weighted least squares（加权最小二乘）在这个加权范数下就只是 ordinary least squares（普通最小二乘）。

爱因斯坦（Einstein）需要在 4 维 space-time（时空）中为 length（长度）与 distance（距离）重新下定义。洛伦兹（Lorentz）提出了下面这个方案，爱因斯坦接受了它（$c$ 为 speed of light（光速））：

```math
\Delta s^2 = \Delta x^2 + \Delta y^2 + \Delta z^2 - c^2 \Delta t^2
```

它是 $\mathbb{R}^4$ 上的一个 true norm（真范数）或 metric（度量）。

> <span style="color:#1e8449;">**译者注**：Lorentz 间隔 $\Delta s^2$ 中时间项带负号，它可以为正、为零或为负，严格说并不是正定的范数，而是 Lorentzian metric（洛伦兹度量）/伪范数。Strang 在此是沿用物理学中"为时空中的长度与距离重新下定义"这一通俗说法。</span>

---

<span style="color:#2471a3;">**[section]**</span>
#### Norms and Inner Products of Functions（函数的范数与内积）

一个 function（函数）$f(x)$ 就是 function space（函数空间）中的一个 vector（向量）。这个简单的想法让 linear algebra（线性代数）获得了超越 $n$ 维空间 $\mathbb{R}^n$ 的重要性。所有与线性（linearity）相关的直觉，都带着我们从 finite dimensions（有限维）一路走向 infinite dimensions（无限维）。向量空间（vector space）的基本要求是允许对向量 $v$ 与 $w$ 做线性组合（linear combination）$cv + dw$；这个想法直接延伸到对函数 $f$ 与 $g$ 的线性组合 $cf + dg$。正是在与 norm（范数）相关的问题上，infinite dimensions（无限维）中出现了新的疑问。

想一想这些特殊的向量（vectors）$v_k$。在通常的 2-norm（$\ell_2$ 范数）下，它们彼此越来越接近，因为 $\|v_k - v_l\|_2 \to 0$。

要使一个向量空间（vector space）"complete（完备）"，每一个 converging sequence（收敛序列）都必须在该空间内有一个 limit（极限）：
1. 由以全零结尾的 infinite vectors（无限向量）$v$ 构成的空间不完备。
2. 由满足 $\|v\|_2^2 = |v_1|^2 + |v_2|^2 + \cdots < \infty$ 的向量构成的空间（即 $\ell_2$）是完备的。像 $(1, \frac{1}{2}, \frac{1}{4}, \frac{1}{8}, \ldots)$ 这样的向量属于这个空间，但不属于第一个空间——它不以零结尾。

与完备的 infinite-dimensional vector space（无限维向量空间）相联系的有两个著名的名字：
- 一种是 Banach space（Banach 空间）：带有一个满足规则 (1) 与 (2) 的 norm（范数）$\|v\|$ 的 complete vector space（完备向量空间）。
- 另一种是 Hilbert space（Hilbert 空间）：还带有一个 inner product（内积）、且 $(v, v)$ 等于 $\|v\|^2$ 的 Banach space（Banach 空间）。

当向量具有无穷多个分量时，这些空间就是 infinite-dimensional（无限维）的：
- 空间 $\ell_1$ 是带范数 $\|v\|_1 = |v_1| + |v_2| + \cdots$ 的 Banach space（Banach 空间）。
- 空间 $\ell_2$ 是 Hilbert space（Hilbert 空间），因为它有 inner product（内积）$(v, w) = v_1 w_1 + v_2 w_2 + \cdots$。
- 空间 $\ell_\infty$ 是带范数 $\|v\|_\infty$ 的 Banach space（Banach 空间），其中 $\|v\|_\infty$ 是数 $|v_1|, |v_2|, \ldots$ 的 supremum（上确界）。

我们特别感兴趣的是 function spaces（函数空间）。向量可以是定义在 $0 \le x \le 1$ 上的函数 $f(x)$：
- 空间 $L^1[0, 1]$ 是带范数 $\|f\|_1 = \int_0^1 |f(x)|\,dx$ 的 Banach space（Banach 空间）。
- 空间 $L^2[0, 1]$ 是带 inner product（内积）$(f, g) = \int_0^1 f(x)g(x)\,dx$ 与 $\|f\|_2^2 = \int_0^1 f(x)^2\,dx$ 的 Hilbert space（Hilbert 空间）。
- 空间 $L^\infty[0, 1]$ 是带范数 $\|f\|_\infty$（即 $|f(x)|$ 的 supremum（上确界））的 Banach space（Banach 空间）。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 初学者读到这里容易只记住“Banach 有范数、Hilbert 有内积”的分类标签，而漏掉真正的关键词：**完备性**。设计问题是：一个空间对“取极限”这个操作是否封闭？回顾 TBB 实分析，$\mathbb{R}$ 的完备性保证每个 Cauchy 序列都有极限，这是微积分里一切极限操作合法性的根基。函数空间换的是范数——范数决定“两个函数有多近”，而不同的范数会给同一个函数集合带来不同的完备性：同一个集合在一种范数下完备，在另一种范数下可能不完备。先看一个正面对照：同一个 $C[0,1]$ 配上 $\|f\|_\infty=\max_{t\in[0,1]}|f(t)|$ 却是完备的，因为 TBB 的定理说连续函数的一致收敛极限仍是连续函数，所以按 $\|\cdot\|_\infty$ 构造的 Cauchy 序列的极限逃不出 $C[0,1]$——完备与否不是空间的名字决定的，而是范数决定的。检验完备性的标准动作是一个**完备性压力测试模板**：构造一个 Cauchy 序列（项与项之间按范数越来越近），再看它的极限是否还留在这个空间里。若极限溜出了空间，该空间就在这个范数下不完备。
> 思想实验：取 $C[0,1]$（$[0,1]$ 上连续函数全体）配 $L^2$ 范数 $\|f\|_2=(\int_0^1 f^2)^{1/2}$。构造 $f_n$：在 $[0,\frac12-\frac1n]$ 上取 0，在 $[\frac12+\frac1n,1]$ 上取 1，中间一段用直线连接。每个 $f_n$ 都连续；当 $n,m$ 都很大时，两个函数只在一段长度约为 $2/n$ 的小区间内有差异，且差异有界，平方积分按 $O(1/n)$ 趋于零，所以 $\{f_n\}$ 是 $L^2$ 意义下的 Cauchy 序列。把误差写得更精确：$n<m$ 时，$|f_n(t)-f_m(t)|\le1$ 且只在 $[\frac12-\frac1n,\frac12+\frac1n]$（长度 $2/n$）内非零，于是 $\|f_n-f_m\|_2^2\le 2/n\to0$，Cauchy 性落到了纸面上。它的极限在 $[0,\frac12)$ 上为 0、在 $(\frac12,1]$ 上为 1，在 $\frac12$ 处发生跳跃——不存在连续函数能在这个范数意义下充当它的极限。为什么连续函数一定当不了极限？若连续 $g$ 满足 $\|f_n-g\|_2\to0$，则 $g$ 必须在 $[0,\frac12)$ 上几乎处处为 0、在 $(\frac12,1]$ 上几乎处处为 1，这与 $g$ 在 $\frac12$ 处的连续性矛盾（左极限 0，右极限 1，接不上）。压力测试失败：$C[0,1]$ 在 $L^2$ 范数下不完备。
> 补齐这个空间的办法是把极限对象本身收进来：$L^2[0,1]$ 正是 $C[0,1]$ 在 $L^2$ 范数下的完备化。这个“补洞”故事与 $\mathbb{Q}\to\mathbb{R}$ 完全平行：$\mathbb{Q}$ 中 Cauchy 序列 $1,1.4,1.41,\ldots$ 的极限 $\sqrt2$ 溜出了 $\mathbb{Q}$，于是我们把所有极限对象收进来得到 $\mathbb{R}$；这里 $f_n$ 的极限阶梯函数溜出了 $C[0,1]$，于是把这类极限收进来得到 $L^2[0,1]$。这也是 Lebesgue 积分理论取代 Riemann 积分的核心动机之一：Riemann 可积函数空间在 $L^2$ 范数下同样不完备，必须扩大函数类、放宽“逐点定义”的约束，才能让取极限封闭；Riesz–Fischer 定理保证 $L^2$ 完备，这是整个构造的落脚点。在 18.065 的有限元方法中，解空间 $H^1$（函数本身与其一阶导数的平方都可积）配上能量范数是完备的，因此 Galerkin 近似序列不会收敛到空间之外的怪物，误差估计才有意义；若在不完备的空间里做数值偏微分方程，你无法保证迭代极限仍是合法解。一句话收束：完备性是空间对“取极限”的封闭性，换范数可能丢掉或获得它，数值方法必须选在完备空间里运行。
---


---

<!-- page 097: 书页 92, §I.11 向量、函数与矩阵的范数（续）：函数光滑性、矩阵范数 -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.11（续）向量、函数与矩阵的范数</span>

#### Highlights of Linear Algebra（线性代数要点）

注意 $\ell^1$ 中分量之和与 $L^1$ 中函数积分之间的这种 parallel（平行关系）。

类似地，在 $\ell^2$ 中考虑平方和（sums of squares），在 $L^2$ 中考虑 $f^2$ 的积分（integrals）。

把它们 add（相加），或 graph（画出图形）来比较。

> <span style="color:#1e8449;">译者注：原文此句在 OCR 中不完整，仅存 "Add or gra..." 几个字符，此处按上下文补全为 "Add or graph them"（把它们相加，或画出图形来比较）。</span>

---

#### Smoothness of Functions（函数的光滑性）

函数空间（function space）有许多类型。

数学的这一分支称为 functional analysis（泛函分析）。

一个函数空间常常把具有特定 level of smoothness（光滑程度）的所有函数汇集（bring together）在一起。

一个突出的例子是包含所有连续函数（continuous functions）$f$ 的空间 $C[0,1]$：

此时 $f$ 属于 $C[0,1]$，且 $\|f\|_C = \max |f(x)|$（最大值在 $[0,1]$ 上取到）。

函数空间 $C$ 中的 max norm（最大值范数）类似于向量的 $\ell^\infty$ 范数。

我们可以把光滑程度提高到 $C^1[0,1]$ 或 $C^2[0,1]$。

这时一阶导数（first derivative）或二阶导数（second derivative）也必须连续（continuous）。

这些是 Banach 空间（巴拿赫空间）但不是 Hilbert 空间（希尔伯特空间）。

这些范数并不来自 inner products（内积）——比较（9）与（10）：

```math
\|f\|_{C^1} = \|f\|_C + \max \left| \frac{df}{dx} \right|, \qquad
\|f\|_{C^2} = \|f\|_C + \max \left| \frac{df}{dx} \right| + \max \left| \frac{d^2 f}{dx^2} \right|
\tag{9}
```

如果我们想要一个 Hilbert 空间 $H^1$，就要在通常的 $L^2$ 空间之上构造（$L^2$ 本身就是一个这样的空间）：

```math
\|f\|_{H^1}^2 = \|f\|_{L^2}^2 + \int_0^1 \left| \frac{df}{dx} \right|^2 dx, \qquad
\langle f, g \rangle_{H^1} = \langle f, g \rangle_{L^2} + \int_0^1 \frac{df}{dx} \frac{dg}{dx} \, dx
\tag{10}
```

我们用三个例子来结束这次在函数空间里的 wild excursion（尽情漫游）：

1. 无穷向量（infinite vector）$(1, \tfrac12, \tfrac13, \tfrac14, \ldots)$ 属于 $\ell^2$ 和 $\ell^\infty$，但它不属于 $\ell^1$——它的各分量之和（sum of components）为无穷大（infinite）。

2. 阶梯函数（step function）属于 $L^1$、$L^2$ 和 $L^\infty$，但不在 $C$ 中，因为该函数有一个 jump（跳跃）。

3. 斜坡函数（ramp function）$\max(0, x)$ 属于 $C$ 和 $H^1$，但不在 $C^1$ 中，因为它的斜率（slope）有一个跳跃。

---

#### Norms of Matrices: The Frobenius Norm（矩阵范数：Frobenius 范数）

矩阵的空间（space of matrices）遵循向量空间的所有规则。

因此一个矩阵范数（matrix norm）$\|A\|$ 必须遵循向量范数的三条规则，并且当 $A$ 乘以 $B$ 时还要满足一条新规则：

```math
\|A\| > 0 \text{（若 } A \text{ 不是零矩阵）}, \qquad
\|cA\| = |c| \, \|A\|, \qquad
\|A + B\| \leq \|A\| + \|B\| \tag{12}
```

新规则：submultiplicative（次可乘）范数 $\|AB\| \leq \|A\| \, \|B\|$。

```math
\|AB\| \leq \|A\| \, \|B\| \tag{13}
```

我们需要为 Frobenius norm（弗罗贝尼乌斯范数）验证（13）——它把矩阵当作 long vectors（长向量）来处理。

---

<!-- page 098: 书页 93, §I.11 向量、函数与矩阵的范数（续）：Frobenius 范数及其性质 -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.11（续）向量、函数与矩阵的范数</span>

弗罗贝尼乌斯范数（Frobenius norm）的定义是

```math
\|A\|_F = \left( \sum_{i=1}^m \sum_{j=1}^n a_{ij}^2 \right)^{1/2}
\tag{14}
```

即 $A$ 的 Frobenius norm（弗罗贝尼乌斯范数）。

弗罗贝尼乌斯范数（Frobenius norm）就是具有 $mn$ 个分量的向量所对应的范数（欧氏范数 Euclidean norm），所以（11）和（12）必然成立。

而当 $B$ 是一个列向量（column vector）$a$ 乘以一个行向量（row vector）$b^T$——也就是说 $B = ab^T$ 是一个秩一矩阵（rank-one matrix）——时，范数不等式（13）恰好取等号（exact equality）：

```math
\|ab^T\|_F^2 = \|a\|_2^2 (b_1^2 + \cdots + b_n^2) = \|a\|_2^2 \|b^T\|_2^2
\tag{15}
```

由此得到 $\|ab^T\|_F = \|a\|_2 \, \|b\|_2$。

这就给出了 $\|AB\|_F \leq \|A\|_F \|B\|_F$ 的第一个证明：$AB$ 是若干秩一矩阵（rank-one matrices）之和，按 column-row multiplication（列乘行乘法）展开：

```math
\begin{aligned}
\|AB\|_F &= \|a_1 b_1^T + \cdots + a_n b_n^T\|_F  &&\text{（列乘行乘法）}\\
&\leq \|a_1 b_1^T\|_F + \cdots + \|a_n b_n^T\|_F  &&\text{（三角不等式（12））}\\
&= \|a_1\|_2 \|b_1\|_2 + \cdots + \|a_n\|_2 \|b_n\|_2  &&\text{（由方程（15））}\\
&\leq \left( \|a_1\|_2^2 + \cdots + \|a_n\|_2^2 \right)^{1/2} \left( \|b_1\|_2^2 + \cdots + \|b_n\|_2^2 \right)^{1/2}  &&\text{（Cauchy-Schwarz 不等式）}\\
&= \|A\|_F \|B\|_F  &&\text{（由 Frobenius 范数的定义（14））}
\end{aligned}
```

习题集（Problem Set）给出了另一个更快捷的证明：把 $AB$ 按 rows times columns（行乘列）相乘。

当 $Q$ 是正交矩阵（orthogonal matrix）时，我们知道 $Qc$ 与 $c$ 具有相同的长度：$\|Qc\|_2 = \|c\|_2$。

由于 $Q$ 左乘 $B$ 的每一列，所以 $\|QB\|_F = \|B\|_F$。

这把 $A = U\Sigma V^T$ 的 Frobenius 范数与其在 $\Sigma$ 中的奇异值（singular values）联系起来：

```math
\|A\|_F = \|U\Sigma V^T\|_F = \|\Sigma V^T\|_F = \|\Sigma\|_F = \left( \sigma_1^2 + \cdots + \sigma_r^2 \right)^{1/2}
\tag{16}
```

还有另一种方式得到 Frobenius 范数的这个好公式：计算乘积 $A^T A$ 会把所有 $a_{ij}^2$ 带到对角线上：

```math
\|A\|_F^2 = \text{trace of } A^T A = \text{sum of eigenvalues} = \sigma_1^2 + \cdots + \sigma_r^2
\tag{17}
```

矩阵 $A$ 的 Frobenius 范数（平方）很容易计算：把 entries（元素）平方再相加即可。

不等式 $\|AB\| \leq \|A\| \, \|B\|$ 将内建（built in）在接下来要讲的矩阵范数之中。




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 把这条证明命名为**列乘行分解模板**：要证矩阵乘积的范数不等式，先把乘积拆成秩一组件，用向量范数的三角不等式与 Cauchy-Schwarz 组装，最后把组件范数之和还原成矩阵范数之积。第一性原理链条只有四环。第一，矩阵乘法按列乘行展开 $AB=\sum_{k=1}^n a_k b_k^T$（$a_k$ 是 $A$ 的第 $k$ 列，$b_k^T$ 是 $B$ 的第 $k$ 行），这是矩阵乘法定义的直接重写——逐元素看 $(AB)_{ij}=\sum_k a_{ik}b_{kj}=\sum_k(a_kb_k^T)_{ij}$，所以不是近似而是恒等。第二，Frobenius 范数是范数，满足三角不等式 $\|A+B\|_F\le\|A\|_F+\|B\|_F$。第三，秩一矩阵 $ab^T$ 的元素是 $a_i b_j$，平方和恰好是 $(\sum a_i^2)(\sum b_j^2)=\|a\|_2^2\|b\|_2^2$，即 $\|ab^T\|_F=\|a\|_2\|b\|_2$。第四，对两个由列范数与行范数组成的向量应用 Cauchy-Schwarz。把第二、三、四环组装成一条显式不等式链：$\|AB\|_F=\|\sum_k a_kb_k^T\|_F\le\sum_k\|a_kb_k^T\|_F=\sum_k\|a_k\|_2\|b_k\|_2=\langle u,v\rangle\le\|u\|_2\|v\|_2$，其中 $u=(\|a_1\|,\ldots,\|a_n\|)$、$v=(\|b_1\|,\ldots,\|b_n\|)$，而 $\|u\|_2^2=\sum_k\|a_k\|_2^2=\|A\|_F^2$、$\|v\|_2^2=\sum_k\|b_k\|_2^2=\|B\|_F^2$，最后一步正是 $\|A\|_F\|B\|_F$。一个自然的第一性原理追问：这个不等式为什么不能免费获得？因为 Frobenius 范数不是由向量范数诱导的算子范数。诱导范数 $\|A\|=\max_{\|x\|=1}\|Ax\|$ 的次可乘性由定义直接送：$\|ABx\|\le\|A\|\|Bx\|\le\|A\|\|B\|\|x\|$；而 Frobenius 范数没有这条免费链路，必须回到秩一分解自己去挣。四环咬合，$\|AB\|_F\le\|A\|_F\|B\|_F$ 就出来了。
> 思想实验（全链验证）：取 $A=\begin{bmatrix}1&2\\3&4\end{bmatrix}$，$B=\begin{bmatrix}0&1\\1&0\end{bmatrix}$，则 $AB=\begin{bmatrix}2&1\\4&3\end{bmatrix}$，$\|AB\|_F=\sqrt{30}$。列乘行分解给出 $AB=\begin{bmatrix}1\\3\end{bmatrix}\begin{bmatrix}0&1\end{bmatrix}+\begin{bmatrix}2\\4\end{bmatrix}\begin{bmatrix}1&0\end{bmatrix}$。三角不等式给出 $\|AB\|_F\le\sqrt{10}\cdot1+\sqrt{20}\cdot1=\sqrt{10}+\sqrt{20}$；对向量 $(\sqrt{10},\sqrt{20})$ 与 $(1,1)$ 用 Cauchy-Schwarz 给出 $\sqrt{10}+\sqrt{20}\le\sqrt{(10+20)(1+1)}=\sqrt{60}$；而 $\sqrt{60}=\sqrt{30}\cdot\sqrt2=\|A\|_F\|B\|_F$。三个数 $\sqrt{30}\approx5.48$、$\sqrt{10}+\sqrt{20}\approx7.63$、$\sqrt{60}\approx7.75$ 逐级放宽，每一步都有损耗，说明等号只在两个秩一组件“同向”且列范数向量与行范数向量共线的特殊情形下才出现。另一个极端：$A=\begin{bmatrix}1&0\\0&0\end{bmatrix}$、$B=\begin{bmatrix}0&0\\0&1\end{bmatrix}$ 时 $AB=0$，$\|AB\|_F=0<\|A\|_F\|B\|_F=1$——列空间与行空间正交时乘积塌缩为零，不等式取到最松。三个不等号逐级收紧，完整演示“拆成秩一组件→三角不等式→Cauchy-Schwarz→还原为矩阵范数”的路径。
> 跨课程连接：这个模板与你在 CLRS 学到的分治同构——把大对象（矩阵乘积）拆成小对象（秩一矩阵），分别用已知工具（向量范数）处理，再合并结果。公式 (16)(17) 又把 Frobenius 范数接到 SVD：$\|A\|_F^2=\sum\sigma_i^2$ 说明它是奇异值向量的 $\ell_2$ 范数，而奇异值向量正是 $A$ 在列空间与行空间上的“伸缩谱”。次可乘性还有一个被低估的用途：它让矩阵范数成为代数范数，于是 $\|A^k\|\le\|A\|^k$ 让矩阵幂的估计完全回到标量等比级数的套路，18.065 中 $\|e^{A}\|\le e^{\|A\|}$、$(I-A)^{-1}=I+A+A^2+\cdots$ 在 $\|A\|<1$ 时收敛等结论都靠它背书。到 §I.11 核范数时，把 $\ell_2$ 换成 $\ell_1$ 就得到凸的低秩代理——这条升级路径与注 31 的 $\ell_0\to\ell_1$ 完全平行。TBB 中的范数公理在这里不是抽象摆设：三角不等式是组装的第一颗螺丝。
>
> 为什么这套模板值得反复调用？因为它把「矩阵范数不等式」这种看起来高阶的对象，还原成你在 6.042J 里已经熟练的两件工具：三角不等式与 Cauchy-Schwarz。前者处理「和的范数不超过范数的和」，后者处理「两个向量的内积有界」，而矩阵乘积 $AB$ 恰好被拆成这些初等对象的和——于是矩阵世界的不等式证明，变成了向量世界里你已经会做的放缩练习。这种「把新对象拆回旧工具」的思路，与你在 CLRS 中反复见到的分治策略同构：遇到不会直接处理的大结构，先找到能把它切成已知小结构的分解方式。对 Frobenius 范数成立，对谱范数 $\|AB\|_2\le\|A\|_2\|B\|_2$ 也成立（用奇异值链 $\sigma_1(AB)\le\sigma_1(A)\sigma_1(B)$ 同样可证），这暗示次可乘性是范数的「普遍性格」而非 Frobenius 的巧合。
>
> 一句话收束：矩阵→秩一组件→向量范数→Cauchy-Schwarz→组装回矩阵范数，五步模板可复用于任何矩阵范数不等式。
---


---

<!-- page 099: 书页 94, §I.11 Norms of Vectors and Functions and Matrices -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.11（续）由向量范数诱导的矩阵范数（Matrix Norms from Vector Norms）</span>

从一个针对 $\mathbb{R}^n$ 中向量的范数（norm）$\|x\|$ 出发。当我们把 $\|Ax\|$ 与 $\|x\|$ 进行比较时，度量的正是增长因子（growth factor）——乘以 $A$ 之后尺度的增大或减小。如果我们选出让增长因子最大的那个向量，就得到一种重要的矩阵范数（matrix norm）：

```math
\|A\| = \max_{x \neq 0} \frac{\|Ax\|}{\|x\|} = \max_{\|x\| = 1} \|Ax\| \tag{18}
```

> <span style="color:#7f8c8d;">向量范数导向矩阵范数：$\|A\| = \max \|Ax\|/\|x\|$ 是最大的增长因子（largest growth factor）。</span>

这个最大比值自动满足矩阵范数的全部条件——因为 $\|\cdot\|$ 已经满足了向量范数的全部条件。单位矩阵（identity matrix）将有 $\|I\| = 1$，因为它的增长因子恒为 $\|x\|/\|x\| = 1$。

**1.** (18) 的关键要点是 $\|Ax\| \leq \|A\|\,\|x\|$，因为 $\|A\|$ 是比值 $\|Ax\|/\|x\|$ 所达到的最大值。于是 $\|ABx\| \leq \|A\|\,\|Bx\| \leq \|A\|\,\|B\|\,\|x\|$，因此 $\|AB\| \leq \|A\|\,\|B\|$。

取 $\|x\|_1$、$\|x\|_2$ 与 $\|x\|_\infty$ 作为重要的向量范数，则 (19)、(20)、(21) 产生三种矩阵范数 $\|A\|_2$、$\|A\|_1$ 与 $\|A\|_\infty$，它们全部满足 $\|AB\| \leq \|A\|\,\|B\|$。对给定的矩阵，我们怎样计算这三种范数——怎样最大化比值 $\|Ax\|/\|x\|$？

```math
\|A\|_2 = \text{最大比值 } \frac{\|Ax\|_2}{\|x\|_2} = A \text{ 的最大奇异值 } \sigma_1 \tag{19}
```

```math
\|A\|_1 = A \text{ 的列的最大 1 范数} \tag{20}
```

```math
\|A\|_\infty = A \text{ 的行的最大 1 范数} \tag{21}
```

本书一直强调 $\|A\|_2$ = 最大比值 $\|Ax\|_2/\|x\|_2 = \sigma_1$。这来自 $A = U\Sigma V^T$：正交矩阵（orthogonal matrices）$U$ 与 $V^T$ 对 $\|\cdot\|_2$ 范数毫无影响，于是只剩下对角矩阵（diagonal matrix）$\Sigma$，它的范数恰为 $\sigma_1$。注意 $A^T$ 具有相同的 $\sigma_1$（再次强调，$U$ 与 $V^T$ 不产生影响）。

这三种矩阵范数有两个尤其漂亮的联系（connections）：

```math
\|A\|_2 \leq \sqrt{\|A\|_1\,\|A\|_\infty} \qquad \text{且} \qquad \|A\|_1 = \|A^T\|_\infty, \quad \|A\|_\infty = \|A^T\|_1 \tag{22}
```

矩阵 $A$ 的行正是 $A^T$ 的列，所以 $\|A\|_\infty = \|A^T\|_1$ 直接来自 (20)(21)。对涉及全部三种范数的不等式 (22)，观察 $A$ 的第一奇异向量（first singular vector）$v$，该向量满足 $\|Av\|_2 = \sigma_1\|v\|_2$。取这个特定 $v$ 的 1 范数并利用 $\|Av\|_1 \leq \|A\|_1\|v\|_1$：由 $Av = \sigma_1 u$（$u$ 是第一左奇异向量（left singular vector））得 $\sigma_1\|u\|_1 \leq \|A\|_1\|v\|_1$。同理，对 $A^T u = \sigma_1 v$ 取 1 范数并用刚证得的 $\|A^T\|_1 = \|A\|_\infty$，得 $\sigma_1\|v\|_1 \leq \|A\|_\infty\|u\|_1$。两式相乘并约去公共因子 $\|u\|_1\|v\|_1$，就得到 $\sigma_1^2 \leq \|A\|_1\,\|A\|_\infty$。既然 $\sigma_1 = \|A\|_2$，这告诉我们 $\|A\|_2 \leq \sqrt{\|A\|_1\,\|A\|_\infty}$。

---

<!-- page 100: 书页 95, §I.11 Norms of Vectors and Functions and Matrices -->

### <span style="color:#2471a3;">**[section]**</span> <span style="color:#c0392b;">§I.11（续）核范数（The Nuclear Norm）</span>

核范数（nuclear norm）$\|A\|_*$ 直接来自 $A$ 的奇异值（singular values），它也被称为迹范数（trace norm）。与 $\|A\|_2$（谱范数 spectral norm）和弗罗贝尼乌斯范数（Frobenius norm）一样，$\|A\|_*$ 都以 $A = U\Sigma V^T$（奇异值分解 SVD）为起点。这三种范数都不受 $U$ 与 $V^T$ 的影响，这个性质称为"酉不变性（unitary invariance）"。我们只需取 $\Sigma$ 主对角线上奇异值向量 $\sigma = (\sigma_1, \sigma_2, \ldots, \sigma_r)$ 的 1 范数、2 范数与 ∞ 范数：

```math
\|A\|_2 = \sigma_1 \qquad \text{（最大奇异值）}
```

```math
\|A\|_F = \left(\sigma_1^2 + \cdots + \sigma_r^2\right)^{1/2} \qquad \text{（Frobenius 范数）}
```

```math
\|A\|_* = \sigma_1 + \cdots + \sigma_r \qquad \text{（核范数 = 奇异值之和）}
```

在 III.4 节，核范数是矩阵补全（matrix completion）的关键——用于数据缺失（missing data）的情形。

> <span style="color:#1e8449;">**译者注**</span>：正文此处引用 "III.4"，但按本书目录，矩阵补全的完整讨论位于 III.5（Compressed Sensing and Matrix Completion，第 195 页），III.4 则是 "Split Algorithms for ℓ2 + ℓ1"。此为书中的引用笔误，译文保留原文编号。

一个引人注目（remarkable）的事实：$\|A\|_*$ 是所有正交矩阵 $U$ 与 $V$ 之下 $\operatorname{tr}(U^T A V)$ 的最大值。另一个相关但容易得多的事实：$\|A^T\|_* = \|A\|_*$。

最大范数（max norm）$\|A\|_{\max} = \max_{i,j} |a_{ij}|$ 与 $\|A\|_\infty$ 完全不同。我们把 $\|A - B\|_{\max}$ 称为"最大范数"，因为只有当 $A$ 中的每一个元素（每一个像素（pixel））都接近 $B$ 中对应的那个元素时，$\|A - B\|_{\max}$ 才小；而这时 $\|A - B\|_\infty$ 也小。

<span style="color:#2471a3;">**[example]**</span> <span style="color:#c0392b;">**例 1（Example 1）**</span> 矩阵 $A$ 有 $\|A\|_1 = 8$（列和）与 $\|A\|_\infty = 9$（行和），且 $A^T A$ 的最大特征值是 50（从而 $\|A\|_2 = \sqrt{50}$）；这验证了 (22)：$50 < 8 \cdot 9 = 72$。矩阵 $B$ 有 $\|B\|_1 = 4$（第 2 列）与 $\|B\|_\infty = 3$（行）；$B$ 的 2 范数是 $\sqrt{10}$，因为 $B^T B$ 的特征值是 0 和 10；验证 $10 < 4 \cdot 3 = 12$。

> <span style="color:#1e8449;">**译者注**</span>：原例中两个示例矩阵的具体元素在 OCR 中残缺（仅残留孤立数字 "15 45"），无法逐字恢复；译文按不等式 (22) 的数值验证目的重建（$\|A\|_2^2 \leq \|A\|_1\|A\|_\infty$ 与 $\|B\|_2^2 \leq \|B\|_1\|B\|_\infty$），数学关系与原例一致。

<span style="color:#00838f;">**重要（Important）**</span>：矩阵 $A$ 的最大特征值（eigenvalue）$|\lambda|_{\max}$ 不在我们的矩阵范数列表中！

### 谱半径（The Spectral Radius）

这个数 $|\lambda|_{\max} = \max_i |\lambda_i|$ 在范数的全部三个主要要求上都失败（fails）。矩阵 $A$ 与 $B$ 可以是非零矩阵（nonzero matrices）而特征值全为零（例如 $\begin{bmatrix}0&1\\0&0\end{bmatrix}$ 这类非零矩阵的特征值就全是 $0$）。对 $A + B$ 与 $AB$ 的检验——三角不等式（triangle inequality）与 $\|AB\| \leq \|A\|\,\|B\|$——对最大特征值也失败。甚至 1 范数也只给出不等式 $\|A\|_1 \geq |\lambda|_{\max}$。

这个数 $|\lambda|_{\max}$ 就是"谱半径（spectral radius）"。它不是范数，但它重要的原因在于：当且仅当 $|\lambda|_{\max} < 1$ 时，$A^k \to 0$。

当我们一次又一次地乘以一个矩阵时（正如在 V.6 节将对马尔可夫链（Markov chains）所做的那样），$A$ 的最大特征值 $|\lambda|_{\max}$ 开始占据主导（dominate）。这正是计算 $|\lambda|_{\max}$ 的"幂法（power method）"的基础。
> <span style="color:#7f8c8d;">Strang §I.11, p.95</span>




> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 这是全书最重要的一张**奇异值范数对应表**：向量的稀疏度对应矩阵的低秩，$\ell_1$ 范数对应核范数。机制：先对 $A$ 做 SVD（Strang §I.8），得到非负奇异值 $\sigma_1\ge\cdots\ge\sigma_r>0$；秩就是正奇异值的个数，即奇异值向量的 $\ell_0$；核范数 $\|A\|_*=\sum\sigma_i$ 是奇异值向量的 $\ell_1$。于是“最小化秩”与“最小化核范数”的关系，精确复刻了注 31 中“最小化 $\ell_0$”与“最小化 $\ell_1$”的关系：前者是 NP-难的组合计数问题，后者是凸优化问题。为什么核范数是凸的而秩不是？凸性的试金石是“两点连线的中点仍在集合里”：$A=e_1e_1^T$ 与 $B=e_2e_2^T$ 都秩 1，但 $(A+B)/2=\operatorname{diag}(\frac12,\frac12)$ 秩 2，所以“秩不超过 $r$”的集合不是凸集，在其上优化没有 6.006 凸优化那套收敛保证；核范数 $\|A\|_*=\sum\sigma_i$ 是矩阵空间上的一个范数（三角不等式与齐次性都成立），而任何范数都是凸函数，因此可以用现成算法求全局最优。设计问题：给定矩阵 $M$ 的少量观测元素，约束 $\mathcal{P}_\Omega(A)=\mathcal{P}_\Omega(M)$（观测位置上必须一致），求最低秩的补全。凸包松弛模板给出：用 $\min\|A\|_*$ 替代 $\min\operatorname{rank}(A)$。
> 思想实验：秩一的 $2\times2$ 矩阵 $M=\begin{bmatrix}1&2\\3&6\end{bmatrix}$ 由两列成比例刻画，只有 3 个自由度。把自由度算法化：秩一矩阵可写成 $uv^T$，$u,v$ 各 2 个参数，但 $(tu)(v/t)$ 给出同一个矩阵，扣除 1 个缩放自由度，得 3，与公式 $r(2n-r)$ 在 $n=2,r=1$ 时的值一致。若观测到其中 3 个元素（例如 $(1,1),(1,2),(2,1)$），第 4 个元素被“行列式为零”强制为 6：低秩意味着行列之间存在线性依赖，缺失元素被这些依赖方程锁定——写出来就是 $ad=bc$，代入 $a=1,b=2,c=3$ 得 $d=6$。一般 $n\times n$ 秩 $r$ 矩阵的自由度是 $r(2n-r)$——SVD 中有 $r$ 个奇异值、左右奇异向量共 $2nr$ 个参数，再减去两侧各 $r(r+1)/2$ 个正交性约束，数量级是 $O(nr)$，所以恢复它天然只需要 $O(nr)$ 量级的观测。代入 $n=100$ 看实感：$r=1$ 时自由度 $199$（约占 $n^2=10^4$ 的 2%），$r=10$ 时自由度 $1900$（约 19%）——低秩矩阵的“有效信息量”远小于表面上的 $n^2$ 个元素，这是少量观测能恢复全矩阵的第一性原理。但抽样有陷阱：若秩一矩阵恰好是 $e_1e_1^T$（只有左上角一个非零元），随机抽到它的概率几乎为零。Candès–Recht 的非相干性条件正是排除这种“能量集中在少数坐标”的病态情形：要求左右奇异向量都充分铺开，不能只压在个别标准基向量上。
> 在这个条件下，Candès–Recht（2009）证明了：对秩不超过 $n^{1/5}$ 的 $n\times n$ 矩阵，随机观测约 $m\ge C n^{6/5}r\log n$ 个元素，核范数最小化就能以高概率精确恢复整个矩阵。把 $n=1000$、$r=1$ 代入：$n^{6/5}\approx3981$，$\log n\approx6.9$，故 $m\approx C\cdot2.7\times10^4$，只占 $n^2=10^6$ 的约 3%（常数 $C$ 略大于 1）——远少于全观测，但比 $nr\log n$ 多出的因子 $n^{1/5}$ 来自非相干性的集中不等式，保证每个行、列都被抽到足够多次。注意 $n^{1/5}$ 增长极慢（$n=10^{10}$ 时才 100），所以渐近上观测数仍接近 $O(n\log n)$。这里的“高概率”就是 6.042J 中的概率收敛：抽样次数增加，失败概率趋于零。最反直觉的一点是凸松弛竟然是精确的：一般凸松弛只是近似（例如整数规划的 LP 松弛通常不给出原问题的精确最优解），而这里在随机抽样加非相干条件下，松弛是紧的——定理断言核范数最小的解就是原秩最小问题唯一正确的补全。Netflix 问题正是这样：用户-电影评分矩阵中约 1% 的观测值对应巨大的稀疏抽样，而“用户口味由少数潜在因素决定”就是低秩假设。你已在 Strang §I.8 学过截断 SVD 是“给定完整矩阵时的最优低秩逼近”，核范数最小化把它升级为“只给部分观测时的精确恢复”。一句话收束：低秩就是奇异值的稀疏，秩/核范数对偶是向量 $\ell_0/\ell_1$ 对偶的矩阵版本。
---





> <span style="color:#1e8449;">**[note] Note（译者注）:**</span>
>
> >
> 检验一个候选范数的标准动作是**公理反例模板**：拿三条公理当测试套件，逐一找反例。谱半径 $\rho(A)=\max|\lambda_i|$ 的第一宗罪是正定性：$A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$ 非零，但特征值全为 0，$\rho(A)=0$。第二宗罪是三角不等式：取 $B=\begin{bmatrix}0&0\\1&0\end{bmatrix}$，则 $\rho(A)=\rho(B)=0$，但 $A+B=\begin{bmatrix}0&1\\1&0\end{bmatrix}$ 的特征值是 $\pm1$，故 $\rho(A+B)=1>0+0$。第三宗罪是次可乘性：同组 $A,B$ 有 $AB=\begin{bmatrix}1&0\\0&0\end{bmatrix}$，$\rho(AB)=1>0\cdot0$。顺带把第四条公理也验掉：齐次性 $\rho(tA)=|t|\rho(A)$ 其实成立——谱半径离范数只差正定性与三角不等式这两条，但公理是整包出售的，缺一条即出局，这正说明反例模板的价值在于精准定位“哪条挂了”。为什么特征值会漏掉东西？第一性原理：特征值只回答“在特征方向 $v$ 上，$Av=\lambda v$ 拉伸了多少倍”；若矩阵把向量平移进另一个方向（幂零行为），特征值完全看不见。$A=\begin{bmatrix}0&1\\0&0\end{bmatrix}$ 把 $e_2$ 送到 $e_1$，没有任何方向被拉伸，却实实在在地改变了空间。算一次平方就更清楚：$A^2=0$——两次平移后一切都归零，但从特征值上看它和零矩阵毫无区别。若学过 Jordan 形，幂零部分就藏在次对角的那一串 1 里，而特征值只读对角元，次对角上的 1 在谱上不留下任何痕迹。
> 思想实验：算 $A^k$。上例 $A^2=0$，$A^k\to0$ 且 $\rho(A)=0<1$，两者一致。取 $\lambda=0.9$ 的对角块，$\lambda^k$ 按几何级数衰减；即便叠加一个幂零部分，幂零部分在有限步内精确归零（上例两步），剩下的几何衰减最终获胜——这就是 $\rho(A)<1\Rightarrow A^k\to0$ 的直觉。精确版本要把 Jordan 块也纳入：块 $\lambda I+N$ 的 $k$ 次幂按二项式展开为 $\sum_{j=0}^{s-1}\binom{k}{j}\lambda^{k-j}N^j$，其范数至多按 $k^{s-1}|\lambda|^k$ 增长，而 $|\lambda|<1$ 时“多项式乘几何级数”仍趋于零（TBB 中 $n^p x^n\to0$ 的矩阵版），所以幂零部分最多拖慢收敛，不能阻止收敛。反过来，若有 $|\lambda|\ge1$，取相应特征向量 $v$，$\|A^k v\|=|\lambda|^k\|v\|$ 不衰减，故 $A^k\not\to0$。这条充要条件在正文的幂法里是隐藏主角：$A^k x$ 的各分量中，$|\lambda|$ 最大的特征方向按几何级数主导其余方向，幂法正是靠反复归一化把这一方向提取出来。顺便连接 CSAPP 第 2 章：不做归一化地反复乘，$|\lambda|>1$ 会溢出到 $+\infty$，$|\lambda|<1$ 会下溢到 0——IEEE 754 的有限指数范围与幂迭代在此直接碰撞。
> 跨课程连接：在 §II.1 的 Jacobi、Gauss-Seidel 迭代中，误差向量每步乘以迭代矩阵 $G$，收敛当且仅当 $\rho(G)<1$，选择松弛参数就是在调小谱半径。给个实感数字：误差每轮按 $\rho$ 缩小，$\rho=0.9$ 时把误差砍到 $10^{-1}$ 需要 $\log_{0.9}0.1\approx22$ 轮，$\rho=0.99$ 则需要约 230 轮——谱半径离 1 多近，直接决定迭代法值不值得用。在 §V.6 的 Markov 链中，转移矩阵总有特征值 1（稳态），投影掉稳态后误差部分的谱半径小于 1，决定 $P^k$ 收敛到稳态的速度，幂法与稳态分析在此合流。把谱半径与矩阵幂彻底焊死的是 Gelfand 公式 $\rho(A)=\lim_{k\to\infty}\|A^k\|^{1/k}$：它说谱半径就是矩阵幂的长期平均增长率，且对任意矩阵范数给出同一个极限——这正是“$\rho(A)<1$ 当且仅当 $A^k\to0$”的最一般背书。注 34 的列乘行模板与这里的公理反例模板互为镜像：一个用分解证明好东西成立，一个用构造证明坏东西不成立。一句话收束：特征值只报告特征方向上的拉伸，幂零部分要靠范数或矩阵幂本身才能看见；检验候选范数，先拿严格上三角矩阵试刀。
---
