# What does $x_k \in \mathbb{R}^n$ mean?

In that picture, $X$ is a data matrix whose **columns** are training examples:

$$
X = \big[ x_1, x_2, \cdots, x_m \big]
$$

So each $x_k$ is the **k-th example** (a feature vector).

## What does $x_k \in \mathbb{R}^n$ mean?

It means:

* $x_k$ is a vector with **n real-valued components**
* i.e.

$$
x_k =
\begin{bmatrix}
x_{1k}\\
x_{2k}\\
\vdots\\
x_{nk}
\end{bmatrix}
\quad \text{where each } x_{ik} \in \mathbb{R}
$$

So $x_k$ "belongs to" $\mathbb{R}^n$ because it's an element of the n-dimensional real vector space.

## Dimensions (to connect to the matrix)

If you have $m$ examples and each example has $n$ features:

* $x_k \in \mathbb{R}^n$ (a column vector)
* $X \in \mathbb{R}^{n \times m}$ (n rows, m columns)

**Example:** if an image is $64\times64$ grayscale, then $n=4096$. Each image flattened into a vector is $x_k \in \mathbb{R}^{4096}$.
