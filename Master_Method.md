# Master Method

If $T(n) \leq a \cdot T\left(\frac{n}{b}\right) + O(n^d)$ then

$$
T(n) = \begin{cases}
O(n^d)&a < b^d\\
O(n^d \log n)&a = b^d\\
O(n^{\log_b(a)})&a > b^d
\end{cases}
$$
