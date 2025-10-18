# Master Method

If $T(n) \leq a \cdot T\left(\frac{n}{b}\right) + O(n^d)$ then

$$
T(n) = \begin{cases}
O(n^d)&a < b^d\\
O(n^d \log_b n) = O(n^d \log n)&a = b^d\\
O(a^{\log_b n)} = O(n^{\log_b a})&a > b^d
\end{cases}
$$

```python
def countdown(n):
    def countdown_from_starting_point(n, starting_point):
        if n == 0:
            return starting_point
        else:
            return countdown_from_starting_point(n - 1, starting_point)
    return countdown_from_starting_point(n, n)
```

```python
from sys import getrecursionlimit
getrecursionlimit()
# 3000

countdown(2969)
# 2969

countdown(2970)
# RecursionError: maximum recursion depth exceeded in comparison
```

```python
from sys import setrecursionlimit
setrecursionlimit(4000)
getrecursionlimit()
# 4000

countdown(3969)
# 3969

countdown(3970)
# RecursionError: maximum recursion depth exceeded in comparison
```
