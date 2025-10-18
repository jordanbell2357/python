# Quicksort using median of medians

<https://online.stanford.edu/courses/soe-ycsalgorithms1-algorithms-design-and-analysis-part-1>

BFPRT (Blum, Floyd, Pratt, Rivest, Tarjan)

```python3
import statistics

def median_of_medians_order_statistic(A, i):
    # Decompose A into batches each of length 5 (last batch has <= 5 elements)
    batches = [A[j:j+5] for j in range(0, len(A), 5)]
    # Find median of each batch
    medians = [statistics.median(batch) for batch in batches]
    
    # Recursively find the median of the medians
    if len(medians) <= 5: # Base case
        pivot = statistics.median(medians)
    else: # Recursive case
        pivot = median_of_medians_order_statistic(medians, len(medians) // 2)
    
    # Partition the list into elements less than, equal to, and greater than the pivot
    lt_pivot = [a for a in A if a < pivot]
    eq_pivot = [a for a in A if a == pivot]
    gt_pivot = [a for a in A if a > pivot]
    
    # Determine where the i-th element lies
    k = len(lt_pivot)
    m = len(eq_pivot)
    if i < k: # The i-th element is in the less-than-pivot group
        return median_of_medians_order_statistic(lt_pivot, i)
    elif i < k + m: # The i-th element is in the equal-to-pivot group
        return pivot  
    else: # The i-th element is in the greater-than-pivot group
        return median_of_medians_order_statistic(gt_pivot, i - k - m)


def partition(array, left, right, num_comparisons):
    """
    Partitions elements of array[left:right] around a pivot.
    Elements smaller than the pivot are moved to its left,
    and elements larger or equal are moved to its right.
    """
    # Find the pivot using median-of-medians
    pivot = median_of_medians_order_statistic(array[left:right], right - left)

    # Swap the pivot element to the first position
    if pivot == array[midpoint]:
        pivot_index = midpoint
    elif pivot == array[right]:
        pivot_index = right
    else:
        pivot_index = left
    array[left], array[pivot_index] = array[pivot_index], array[left]

    i = left + 1

    for j in range(left + 1, right + 1):
        # Count comparisons
        num_comparisons += 1
        if array[j] < pivot:
            array[i], array[j] = array[j], array[i]
            i += 1

    # Place the pivot in its correct position
    array[left], array[i - 1] = array[i - 1], array[left]

    return i - 1, num_comparisons  # Return pivot's index and updated comparison count


def quicksort(array, left, right, num_comparisons):
    """
    Recursively applies quicksort on subarrays, partitioning them
    and counting the number of comparisons made.
    """
    if left < right:
        # Partition the array and get the pivot's final position
        pivot_index, num_comparisons = partition(array, left, right, num_comparisons)

        # Recursively sort the left and right subarrays
        num_comparisons = quicksort(array, left, pivot_index - 1, num_comparisons)
        num_comparisons = quicksort(array, pivot_index + 1, right, num_comparisons)

    return num_comparisons


# Load the integer array from the input file
integer_array = []

with open("QuickSort.txt", "r") as reader:
    for line in reader:
        integer_array.append(int(line.strip()))

# Initialize the comparison count
num_comparisons = 0

# Perform quicksort and count comparisons
num_comparisons = quicksort(integer_array, 0, len(integer_array) - 1, num_comparisons)

print("Number of comparisons:", num_comparisons)
```
