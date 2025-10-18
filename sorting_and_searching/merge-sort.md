# Merge sort with counting inversions

<https://realpython.com/sorting-algorithms-python/>

```python3
def merge_and_count_inversions(left, left_inversion_count, right, right_inversion_count):
    split_inversion_count = 0
    result = []
    index_left = index_right = 0

    while index_left < len(left) and index_right < len(right):
        if left[index_left] <= right[index_right]:
            result.append(left[index_left])
            index_left += 1
        else:
            result.append(right[index_right])
            index_right += 1
            # Add the number of remaining elements in left as split inversions
            split_inversion_count += len(left) - index_left

    # Append remaining elements
    result += left[index_left:]
    result += right[index_right:]

    inversion_count = left_inversion_count + right_inversion_count + split_inversion_count

    return result, inversion_count

def merge_sort_and_count_inversions(array):
    # If the input array contains 0 or 1 elements, return it as is
    if len(array) <= 1:
        return array, 0

    midpoint = len(array) // 2

    # Recursively split and sort the array
    left, left_inversion_count = merge_sort_and_count_inversions(array[:midpoint])
    right, right_inversion_count = merge_sort_and_count_inversions(array[midpoint:])
    return merge_and_count_inversions(left, left_inversion_count, right, right_inversion_count)

def count_inversions(array):
    result, inversion_count = merge_sort_and_count_inversions(array)
    return inversion_count

# apply to data
integer_array = []

with open("IntegerArray.txt", "r") as reader:
    line = reader.readline()
    while line != '':
        integer_array.append(int(line.rstrip('\n')))
        line = reader.readline()

print(count_inversions(integer_array))
```
