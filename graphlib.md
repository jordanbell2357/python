# graphlib

A DAG must have a sink vertex. If a DAG G did not have a sink vertex, every vertex has an outgoing arc. Start from any vertex. Follow an arc from it, and get to a vertex which by assumption
has an outgoing arc, etc. Let N be the number of vertices of G. Do this N times, which is an itinerary of N+1 vertices. By the pigeonhole principle, two of the vertices are the same, so there
is a cycle, a contradiction.

Removing a vertex from a DAG yields a DAG.

To compute topological ordering f of a DAG G, let v be a sink vertex of G. Let f(v) = n. Define f by recursion using G - {v}.

```python
from graphlib import TopologicalSorter

graph = {"D": {"B", "C"}, "C": {"A"}, "B": {"A"}}
ts = TopologicalSorter(graph)
tuple(ts.static_order())

ts = TopologicalSorter()
ts.add('D', 'B', 'C')
ts.add('C', 'A')
ts.add('B', 'A')
tuple(ts.static_order())
```
