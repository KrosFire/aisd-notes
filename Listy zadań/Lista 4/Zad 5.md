![[Screenshot 2023-06-18 at 15.29.48.png]]

Mając $5$-literowe słowo "matma", tworzymy $6$ tablic $n\times n$. Tak aby pokryć każdy stan w maszynie stanowej

Musimy również stworzyć następujące automaty skończone, które będą nam mówić, na jaką tabelę mamy się przenieść.

W wariancie, gdy "matma" **jest podciągiem**:

![[IMG_0189.jpeg]]

W wariancie, gdy "matma" **jest napisem**:

![[IMG_0191.jpeg]]

Gdy będziemy chcieli zrobić maszynę dla przypadków negujących, wystarczy że zanegujemy stany w maszynie stanowej - z akceptujących na nieakceptujące.

Tablice będziemy wypełniać w następujący sposób:

```python
for row in range(n):
	for col in range(n):
		for s in range(6):
			if X[row] == Y[row]:
				tab[row][col][state_m(s, X[row])] = tab[row-1][col-1][s]+1
			else:
				tab[row][col][state_m(s, X[row])] = max(tab[row][col-1][s], tab[row-1][col][s])
```

Stany początkowe:

Dla tablicy stanu początkowego będzie wypełnione $0$

Dla reszty $-\infty$

Rozwiązaniem będą ostatnie komórki stanów akceptujących:
$$
\forall{s\in \text{Accept States}}\; tab[n][n][s]
$$

Złożoność:

$O(n^2s)$