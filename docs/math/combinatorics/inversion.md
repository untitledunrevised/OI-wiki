# 序列反演

本文将介绍一些常用的序列反演。

## 定义

为了方便，在本文，通过序列 $\left\langle f_n \right\rangle$ 推导出序列 $\left\langle F_n \right\rangle$ 的过程称作 **正演**，通过序列 $\left\langle F_n \right\rangle$ 反推出序列 $\left\langle f_n \right\rangle$ 的过程称作 **反演**。

首先定义序列正演：

$$
F_n = \sum_{k} a_{n,k}f_k
$$

可知这是一个从序列 $\left\langle f_n \right\rangle$ 到序列 $\left\langle F_n \right\rangle$ 的线性映射，则其反演也是一个线性映射。定义序列反演：

$$
f_n = \sum_{k} b_{n,k}F_k
$$

## 二项式反演

正演：

$$
F_n = \sum_{k = 0}^{n}\binom{n}{k}f_k
$$

反演：

$$
f_n = \sum_{k = 0}^{n}\binom{n}{k}(-1)^{n-k}F_k
$$

## 斯特林反演

正演：

$$
F_n = \sum_{k = 0}^{n}\begin{Bmatrix}n \\ k\end{Bmatrix}f_k
$$

反演：

$$
f_n = \sum_{k = 0}^{n}\begin{bmatrix}n \\ k\end{bmatrix}(-1)^{n-k}F_k
$$

其中 $\begin{bmatrix}n \\ k\end{bmatrix}$ 和 $\begin{Bmatrix}n \\ k\end{Bmatrix}$ 分别表示第一类斯特林数、第二类斯特林数。

## 莫比乌斯反演

正演：

$$
F_n = \sum_{d | n}f_d
$$

反演：

$$
f_n = \sum_{d | n}F_d \mu \left(\frac{n}{d}\right)
$$

其中 $\mu(n)$ 表示莫比乌斯函数。

## 离散傅里叶变换

正演：

$$
F_n = \sum_{k = 0}^{n - 1}\omega^{-k}f_k
$$

反演：

$$
f_n = \frac{1}{n}\sum_{k = 0}^{n - 1}\omega^{k}F_k
$$

其中 $\omega = e^{2\pi i/n}$。
