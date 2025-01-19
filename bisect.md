# bisect

```
import bisect
import timeit

def load_txt_list(path):
    with open(path) as text_file:
        return text_file.read().splitlines()

names = load_txt_list('names.txt')
sorted_names = load_txt_list('names_sorted.txt')

name_to_find = 'John Belushi'

print(bisect.bisect_left(sorted_names, name_to_find))

print(sorted_names[6356854])

print(timeit.timeit(lambda: name_to_find in sorted_names))

print(timeit.timeit(lambda: bisect.bisect_left(sorted_names, name_to_find)))
```
