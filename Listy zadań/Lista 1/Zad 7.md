![[Screenshot 2023-06-30 at 20.13.51.png]]

```python
for k=1..n:
	for i=1...n:
		for j = 1...n:
			d[i][j] = min(d[i][j], d[i][k]+d[k][j])
```

Pętla działa w następujący sposób:

Sprawdzamy najkrótszą ścieżkę od $i$ do $j$ i patrzymy, czy przebiega ona przez $k$.

Jest to oparte na algorytmie [[Algorytm Warshalla - Floyda | Foyda Warshalla]]

