## itertools.repeat with an iterator

```python3
import itertools as it

for x in it.repeat(iter([1, 2, 3]), times=2):
    print(list(x))

# [1, 2, 3]
# []
```

<https://realpython.com/python-itertools/#analyzing-the-sp500>

itertools.dropwhile drops initial non-positive entries, then itertools.takewhile takes a maximal run of positive entries, and this repeats
until the iterator is exhausted.

```python3
import itertools as it

def consecutive_positives(sequence, zero=0):
    def _consecutives(sequence):
        for subsequence in it.repeat(iter(sequence)):
            yield tuple(it.takewhile(lambda p: p > zero,
                                     it.dropwhile(lambda p: p <= zero, subsequence)))
    return it.takewhile(lambda t: len(t) > 0, _consecutives(sequence))

list(consecutive_positives([1, -1, 0, 2, 3, -1, 1, 1]))
# [(1,), (2, 3), (1, 1)]
```

## itertools.groupby for Run-Length Encoding (RLE)

<https://realpython.com/python-itertools/>

```python3
data = [0, 1, 0, 0, 0, 1, 1, 0, 1, 0, 0, 1, 1, 1, 1]

grouped_data = it.groupby(data, key=lambda x: x)

for key, grp in grouped_data:
    print(key, len(list(grp))) # run-length encoding (RLE)
```

```
0 1
1 1
0 3
1 2
0 1
1 1
0 2
1 4
```

## itertools.batched and textwrap.wrap

```python3
import itertools as it

list(it.batched('ABCDEFG', n=3))
# [('A', 'B', 'C'), ('D', 'E', 'F'), ('G',)]
```

```
import textwrap

textwrap.wrap('ABCDEFG', width=3)
# ['ABC', 'DEF', 'G']
```
