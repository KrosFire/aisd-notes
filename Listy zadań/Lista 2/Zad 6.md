![[Screenshot 2023-06-16 at 20.27.39.png]]

Możemy wykorzystać do tego zwykły DFS, który wybiera krawędzie jedynie mniejsze wagowo od $e$. Jeśli odwiedzimy w taki sposób wszystkie wierzchołki, to to oznacza, że żadne MST, nie zawiera $e$. Algorytm ten działa w czasie $O(|V|+|E|)$, ponieważ odwiedzi on każdą krawędź i każdy wierzchołek maksymalnie raz.

```python
def dfs(T, pos, dest, maximum, visited):
	if pos == dest:
		return True
	for (dest_vertex, weight) in edges(pos):
		if weight < maximum and dest_vertex not in visited:
			visited.push(dest_vertex)
			if dfs(T, dest_vertex, dest, maximum, visited)
				return True
	return False
def e_in_mst(T, e):
	
```