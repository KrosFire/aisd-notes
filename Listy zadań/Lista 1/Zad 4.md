![[Screenshot 2023-06-15 at 16.49.29.png]]

```python
def paths(V, u, v):
	distances = Dijktra(V, v)
	visited = {
		v: True
	}
	paths = {
		v: 1
	}

	explore(u, visited, paths, distances)
	return paths[u]

def explore(v, visited, paths, distances):
	for u in neighbours(v):
		if distances[u] >= distances[v]:
			continue
		else if not visted[u]:
			explore(u, visited, paths, distances)
		paths[v] += paths[u]
	visited[v] = True
```

Ogólna idea jest następująca:

Lecimy Dijkstrą z wierzchołka $v$ i w ten sposób znamy dystans każdego wierzchołka do wierzchołka docelowego $v$.

Następnie idziemy DFS'em od $u$ do $v$, wybierając na naszej ścieżce tylko te wierzchołki, które mają dystans do $v$ mniejszy niż wierzchołek, na którym się obecnie znajdujemy. Czyli innymi słowy, nie wybieramy ścieżek na około.