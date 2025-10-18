# Cayley distance

<https://ncatlab.org/nlab/show/Cayley+distance>

<https://docs.sympy.org/latest/modules/combinatorics/permutations.html>

```python3
from sympy.combinatorics import Permutation

def cycle_decomposition(perm):
    """Decomposes a permutation into disjoint cycles."""
    n = len(perm)
    visited = [False] * n
    cycles = []

    for i in range(n):
        if not visited[i]:
            cycle = []
            while not visited[i]:
                cycle.append(i)
                visited[i] = True
                i = perm[i]
            if len(cycle) > 1:
                cycles.append(cycle)
    return cycles

def cayley_distance_and_sort(perm):
    """Calculates the Cayley distance and sorts the permutation with minimal transpositions."""
    cycles = cycle_decomposition(perm)

    cayley_distance = 0 # Cayley distance is n - c: len(perm) - len(cycles)

    transpositions = []
    perm_copy = perm[:]  # Make a mutable copy of the permutation

    for cycle in cycles:
        # Break each cycle into singletons with transpositions
        for i in range(1, len(cycle)):
            # Transpose elements to break the cycle
            transpositions.append((cycle[0], cycle[i]))
            perm_copy[cycle[0]], perm_copy[cycle[i]] = perm_copy[cycle[i]], perm_copy[cycle[0]]
            cayley_distance += 1

    return cayley_distance, transpositions, perm_copy

# Example Usage
perm = [2, 0, 1, 4, 3, 7, 6, 5]  # Permutation
cayley_distance, transpositions, sorted_perm = cayley_distance_and_sort(perm)

perm_sympy = Permutation(perm)

print("Permutation:", perm)
print("Cycle decomposition:", cycle_decomposition(perm))
print("Cycle decomposition by SymPy:", perm_sympy.cyclic_form)
print("Cayley distance:", cayley_distance)
print("Transpositions performed:", transpositions)
print("Sorted permutation:", sorted_perm)
```
