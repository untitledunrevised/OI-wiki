# 上升幂多项式 | 下降幂多项式

本文将介绍上升幂，下降幂，上升幂多项式和下降幂多项式。

## 上升幂与下降幂

### 定义

**下降幂** 是具有如下形式的一种多项式：

$$
x^{\underline n} = x(x-1)(x-2)\dots(x-n+1) = \prod_{k=0}^{n-1}(x-k)
$$

**上升幂** 是具有如下形式的一种多项式：

$$
x^{\overline n} = x(x+1)(x+2)\dots(x+n-1) = \prod_{k=0}^{n-1}(x+k)
$$

特别地，当 $n = 0$ 时，定义 $x^{\underline n} = x^{\overline n} = 1$。

### 展开式

上升幂和下降幂的展开式分别为：

$$
\begin{aligned}
x^{\overline n} &= \sum_{k = 0}^{n} s_u(n, k) = \sum_{k = 0}^{n} \begin{bmatrix} n \\ k \end{bmatrix} \\
x^{\underline n} &= \sum_{k = 0}^{n} s_s(n, k)
\end{aligned}
$$

其中 $s_u(n,k)$ 和 $\begin{bmatrix} n \\ k \end{bmatrix}$ 都表示无符号第一类斯特林数，$s_s(n,k)$ 表示有符号第一类斯特林数。

因此求出上升幂或下降幂的展开式，就得到了同一行无符号 / 有符号第一类斯特林数。

#### 暴力法

直接一项一项暴力相乘即可。时间复杂度 $O(n^2)$。

注意直接使用 FFT 无法降低时间复杂度，因为 FFT 得将每一项都输出到长度为 $O(n)$ 的向量，反而使总时间复杂度退化到了 $O(n^2 \log n)$。

#### 分治法

上升幂 / 下降幂有如下性质：

$$
\begin{aligned}
x^{\overline{n + m}} &= x^{\overline n}(x + n)^{\overline m} \\
x^{\underline{n + m}} &= x^{\underline n}(x - n)^{\underline m}
\end{aligned}
$$

设待求的上升幂 / 下降幂阶数为 $N$，取 $n = \lfloor N/2 \rfloor$，$m = \lceil N/2 \rceil$，递归求出两个部分的展开形式后相乘即可。

使用 FFT 可以将一次多项式乘法的时间复杂度降到 $O(n \log n)$。

总时间复杂度

$$
T(n) = 2T(n / 2) + O(n \log n) = O(n \log^2 n)
$$

#### 分治法 + 多项式平移优化

前置知识：[多项式平移](https://oi-wiki.org/math/poly/shift/#%E5%A4%9A%E9%A1%B9%E5%BC%8F%E5%B9%B3%E7%A7%BB)

如果已经求出了上升幂 $x^{\overline n}$ 或下降幂 $x^{\underline n}$ 的展开形式，则使用多项式平移可以在 $O(n \log n)$ 的时间求出 $(x + n)^{\overline n}$ 或 $(x - n)^{\underline n}$ 的展开形式。如果 $\lfloor N/2 \rfloor \not = \lceil N/2 \rceil$，则对 $(x + n)^{\overline n}$ 或 $(x - n)^{\underline n}$ 的展开形式再暴力乘上 $(x + 2n)$ 或 $(x - 2n)$ 即可。

总时间复杂度

$$
T(n) = T(n / 2) + O(n \log n) = O(n \log n)
$$

## 上升幂多项式与下降幂多项式

### 定义

**下降幂多项式** 是具有如下形式的一种多项式：

$$
F^{\downarrow}(x) = a_0 + a_1x + a_2x^{\underline 2} + a_3x^{\underline 3} + \dots
$$

**上式幂多项式** 是具有如下形式的一种多项式：

$$
F^{\uparrow}(x) = a_0 + a_1x + a_2x^{\overline 2} + a_3x^{\overline 3} + \dots
$$

### 下降幂多项式乘法

给定两个下降幂多项式 $F^{\downarrow}(x)$ 和 $G^{\downarrow}(x)$，求下降幂多项式 $H^{\downarrow}(x)$ 使得 $H^{\downarrow}(x) = F^{\downarrow}(x)G^{\downarrow}(x)$。

首先，扩展一下排列数和组合数的运算：

$$
\begin{aligned}
\mathrm{A}_c^k &= c^{\underline k} \\
\mathrm{C}_c^k &= \binom{c}{k} = \frac{\mathrm{A}_c^k}{k!} = \frac{c^{\underline k}}{k!}
\end{aligned}
$$

其中 $c \in \mathbf C$，$k \in \mathbf N$。
