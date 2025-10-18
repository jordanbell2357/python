# Quicksort using median of three

<https://online.stanford.edu/courses/soe-ycsalgorithms1-algorithms-design-and-analysis-part-1>

```python3
import statistics

def partition(array, left, right, num_comparisons):
    """
    Partitions the array around a pivot chosen as the median-of-three element.
    Elements smaller than the pivot are moved to its left,
    and elements larger or equal are moved to its right.
    """
    # Find the pivot using the median-of-three rule
    midpoint = (left + right) // 2
    pivot = statistics.median([array[left], array[midpoint], array[right]])
    
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
