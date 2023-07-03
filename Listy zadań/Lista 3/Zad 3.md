![[Screenshot 2023-06-17 at 15.39.14.png]]

```python
def merge_figures(P, Q):
	i, j = closest_points(P, Q)
	while (y(i, j+1) > y(i,j) or y(i+1,j) > y(i,j)):
		if y(i, j+1) > y(i,j):
			j += 1 mod q
		else:
			i += 1 mod p
	return (a[i], b[j]) - uppper bound O(n)
```

Analogicznie dla lower bound.

Cały pomysł polega na tym, aby wybrać dwa najbliższe punkty dwóch figur, aby mieć pewność, że nie odcinek je łączący nie przecina żadnej z figur. A następnie pójście w górę i w dół jak najdalej można po punktach obu figur. 