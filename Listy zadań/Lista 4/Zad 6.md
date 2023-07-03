![[Screenshot 2023-06-18 at 19.48.30.png]]

Stworzymy tablicę dwuwymiarową $T[i][j]$, która będzie miała wymiary sumy wszystkich elementów, zbioru $a$ - $S$. Czyli $S\times S$.

Komórka $T[i][j]$ będzie mieć wartość $true$, jeśli rozłączne zbiory o sumie $i$ oraz $j$ są możliwe. Dzięki temu wynikiem będzie $T[S/3][S/3]$.

Algorytm:

```python
S = sum(A)
n = len(A)

if S/3 is not int:
	return False

dp[0][0] = true
for k in 1..n:
	for i in -C*k..C*k:
		for j in -C*k..C*k:
			if dp[i][j]:
				dp[i+A[k]][j] = true
				dp[i][j+A[k]] = true
return dp[S/3][S/3]
```

Złożoność czasowa:
$O(C^2n^3)$

Algorytm działa, ponieważ możemy na wejściu dostać $n$ liczb równych $-C$ lub $C$. Sprawdzamy więc po kolei, jeśli istnieje zbiór sumujący się do obecnie odwiedzanej wartości, to istnieje również zbiór który się sumuje do wartości powiększonej przez obecnie analizowaną liczbę ze listy $arr$.

