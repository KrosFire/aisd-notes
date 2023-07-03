Chcemy stworzyć taką strukturę danych, która wskaże name w bardzo szybkim czasie poprzednika i następce tj: największą liczbę mniejszą od $x$ i najmniejszą liczbę większą od $x$, która jest w zbiorze $S$. Zbiór $S$ zaś jest podzbiorem uniwersum $U=\{0,1,...,\mu-1\}$. Jest to bardzo przydatne gdy chcemy się dowiedzieć, czy i gdzie dany element zmieści się w zbiorze $S$.

## Wektor bitowy

Przynależność liczb z uniwersum $U$, do zbioru $S$, możemy przedstawić za pomocą wektora bitowego $v$, gdzie $\forall i \in U\; v[i] = 0 \lor 1$.

Następnie możemy podzielić sobie wektor $v$ na $\sqrt{u}$ sekcji, posiadających $\sqrt{u}$ elementów. Dla każdej takiej grupy, dodamy flagę, czy grupa ta jest pusta.

Teraz, gdy będziemy chcieli znaleźć następce/poprzednika liczby $k$, wpierw przeszukamy sekcję, do której należy $k$. Zajmie nam to $O(\log \sqrt{u})$. Jeśli nie znajdziemy tam poszukiwanego elementu, sprawdzimy flagi pustości innych grup i przeszukamy pierwszą napotkaną niepustą grupę. Zapewni nam to, że znajdziemy tam następce/poprzednika i to ponownie w czasie $O(\log \sqrt{u})$.

![[Screenshot 2023-05-27 at 12.46.34.png]]

## Rekursja

$O(\log \sqrt{u})$ nas nie zadowala. Chcielibyśmy jeszcze bardziej dokręcić śrubę. WIemy że możemy się wywoływać na zbiorach o rozmiarze $\sqrt{u}$. Jeśli dobrze to rozegramy, jesteśmy w stanie wykręcić czas $O(\log \log u)$.

Załóżmy że szukamy następcy $x$-a, w zbiorze $S$. Pomocne nam będą następujące funkcje:

$$
high(x) = \bigg\lfloor\frac{x}{\sqrt{u}}\bigg\rfloor
$$
$$
low(x) = x \;\mathrm{mod}\; \sqrt{u}
$$

Funkcja $high(x)$ mówi nam w jakim podzbiorze znajduje się $x$, a funkcja $low(x)$ na jakim indeksie w tym podzbiorze.

Zapamiętujmy również, jaka największą i najmniejszą wartość posiada każdy podzbiór $S$ w tablicach $max$ i $min$.

Dzięki tej informacji jesteśmy w stanie uniknąć nadmiarowych przeszukiwań podzbiorów.

Do tego lista flag pustych zbiorów będzie się nazywać: $summary$

Popatrzmy na algorytm:

```python
def Successor(x, S):
	x_sub_struct = sub[high(x)]
	x_sub_index = low(x)
	if x_sub_index < max[x_sub_struct]:
		successor_in_sub = Successor(low(x), x_sub_struct)
		return high(x)*sqrt(size(S))+successor_in_sub
	else:
		sub_index_with_successor = Successor(high(x), summary)
			return sub_index_with_successor*sqrt(size(S)) + min[sub[sub_index_with_successor]]
```

Wzór rekrurencyjny tego algorytmu wygląda następująco:
$$
T(u)=T(\sqrt{u})+O(1)
$$
$$
T'(\log u)=T'(\log \sqrt{u})+O(1)=T'(\frac{1}{2}\log u)+O(1)
$$
[[Master theorem]]
$$
(\log u)^{\log_21}=(\log u)^0=1=f(n)
$$
$$
O(\log\log u)
$$

Ostateczna struktura drzewa Van Emde Boasa wygląda następująco:

![[Screenshot 2023-05-27 at 18.03.19.png]]

### Insert

Algorytm odpowiedzialny za wstawianie elementów do zbioru $S$ wygląda następująco:

```python
def Insert(x, S):
	if x < min[S]:
		min[S], x = x, min[S]
	if summary[sub[high(x)]] == 0: # empty
		min[high(x)] = x
		Insert(high(x), summary)
	else:
		Insert(low(x), sub[high(x)])
	if x > max[S]:
		max[S] = x
```

Algorytm ten, również wywołuje się tylko raz na zbiorze o rozmiarze $\sqrt{n}$, a więc ma złożoność $O(\log\log n)$