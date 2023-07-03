```python
def MinMax(S)
	Smaller = []
	Bigger = []
	n = len(S)
	for i in range(n // 2):
		if a[i] > a[n-i]:
			Smaller.append(a[n-i])
			Bigger.append(a[i])
		else:
			Smaller.append(a[i])
			Bigger.append(a[n-i])
	smallest = min(Smaller)
	biggest = max(Bigger)
	if n % 2 == 0:
		return (smallest, biggest)
	return (min(smallest, a[n//2+1]), max(biggest, a[n//2+1]))
```

Ilość porównań:

Główna pętla `for`:
$$
\lfloor \frac{n}{2}\rfloor
$$

znalezienie największego i najmniejszego:
$$
\lfloor n\rfloor
$$

Sumarycznie:

$$
\frac{3}{2}n
$$

porównań