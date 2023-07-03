![[Screenshot 2023-06-15 at 17.05.08.png]]

```python
def max_len(V):
	sorted_v = top_sort(V)
	distances = [0 for i in range(0, |V|)]
	for v in sorted_v:
		for u in neighbours(v):
			distances[u] = max(distances[u], distances[v]+1)
	return max(distances)
```

```python
def max_path(V):
	sorted_v = top_sort(V)
	paths = [(1, [v]) for v in V]
	for v in sorted_v:
		for u in neighbours(v):
			max_path = paths[u][1]
			if paths[v][0]+1 > paths[u][0]:
				max_path = (paths[v][0]+1, paths[v][1]+[u])
	return max_first_arguments(paths)[1]
```