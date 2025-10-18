# Bubble sort and Kendall tau distance

<https://ncatlab.org/nlab/show/Kendall+tau+distance>

<https://realpython.com/sorting-algorithms-python/>

```python3
def bubble_sort(array):
    n = len(array)
    swap_count = 0

    for i in range(n):
        # Create a flag that will allow the function to
        # terminate early if there's nothing left to sort
        already_sorted = True

        # Start looking at each item of the list one by one,
        # comparing it with its adjacent value. With each
        # iteration, the portion of the array that you look at
        # shrinks because the remaining items have already been
        # sorted.
        for j in range(n - i - 1):
            if array[j] > array[j + 1]:
                # If the item you're looking at is greater than its
                # adjacent value, then swap them
                array[j], array[j + 1] = array[j + 1], array[j]
                swap_count += 1
                # Since you had to swap two elements,
                # set the `already_sorted` flag to `False` so the
                # algorithm doesn't finish prematurely
                already_sorted = False

        # If there were no swaps during the last iteration,
        # the array is already sorted, and you can terminate
        if already_sorted:
            break

    return array, swap_count

X = [2, 5, 1, 9, 4, 3, 8, 7, 6]

print(bubble_sort(X))
# ([1, 2, 3, 4, 5, 6, 7, 8, 9], 13)
```
