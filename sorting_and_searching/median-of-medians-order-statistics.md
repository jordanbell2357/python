# Median of medians order statistics

<https://online.stanford.edu/courses/soe-ycsalgorithms1-algorithms-design-and-analysis-part-1>

BFPRT (Blum, Floyd, Pratt, Rivest, Tarjan)

```python3
import statistics

def get_ith_smallest_element_and_index(A, i, pivot_indices=None):
    """
    Find the i-th order statistic in A using the median-of-medians method.
    Tracks the pivot index of the i-th element in the input array.
    
    Args:
    - A: List of elements
    - i: Index of the order statistic to find (0-based)
    - pivot_indices: List of pivot indices corresponding to elements in A
    
    Returns:
    - (value, pivot_index): The i-th order statistic and its pivot index
    """
    # Initialize pivot indices if not provided
    if pivot_indices is None:
        pivot_indices = list(range(len(A)))

    # Decompose A into batches each of length 5 (last batch has <= 5 elements)
    batches = [A[j:j+5] for j in range(0, len(A), 5)]
    # Find median of each batch
    medians = [statistics.median(batch) for batch in batches]
    
    # Recursively find the median of the medians
    if len(medians) <= 5:  # Base case
        pivot = statistics.median(medians)
    else:  # Recursive case
        pivot_index = len(medians) // 2
        pivot = get_ith_smallest_element_and_index(medians, pivot_index)[0]
    
    # Partition the list into elements less than, equal to, and greater than the pivot
    lt_pivot, eq_pivot, gt_pivot = [], [], []
    lt_indices, eq_indices, gt_indices = [], [], []

    for idx, a in enumerate(A):
        if a < pivot:
            lt_pivot.append(a)
            lt_indices.append(pivot_indices[idx])
        elif a == pivot:
            eq_pivot.append(a)
            eq_indices.append(pivot_indices[idx])
        else:
            gt_pivot.append(a)
            gt_indices.append(pivot_indices[idx])
    
    # Determine where the i-th element lies
    k = len(lt_pivot)
    m = len(eq_pivot)
    if i < k:  # The i-th element is in the less-than-pivot group
        return get_ith_smallest_element_and_index(lt_pivot, i, pivot_indices=lt_indices)
    elif i < k + m:  # The i-th element is in the equal-to-pivot group
        return (pivot, eq_indices[i - k])
    else:  # The i-th element is in the greater-than-pivot group
        return get_ith_smallest_element_and_index(gt_pivot, i - k - m, pivot_indices=gt_indices)


A = [3, 0, 0, 3, 2, 1, 3, 1, 3, 4]
print(get_ith_smallest_element_and_index(A, len(A) // 2))
# (3, 0)
print(statistics.median(A))
# 2.5
```
