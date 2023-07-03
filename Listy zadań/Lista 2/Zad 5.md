![[Screenshot 2023-06-16 at 18.39.03.png]]

Algorytm działa następująco:

```python
def color_tree(T, k):
	if k == 0:
		return []
	if k == 1:
		return random_v(T)
	colored = leafs(T)
	return colored+color_tree(T-colored, k-2)
```

Dlaczego tak?

Dwa pierwsze ify są oczywiste.

Kolorujemy liście, czyli kolorujemy sobie proste ścieżki od końców, ergo zmniejszamy sobie liczbę kolorowań wymaganych w rekurencyjnym wywołaniu o $2$.

Zróbmy dowód indukcyjny optymalności:
$S_{k}$ - Zbiór wierzchołków pokolorowanych przez nasz algorytm

$S_0$ i $S_1$ - naturalnie są optymalne

$S_{k-2}$ - zakładamy że jest optymalne.

$S_k = S_{k-2} \cup \text{Leafs}(T)$

Niech istnieje $S_k'$ taki, że $|S_k'| > |S_k|$.

Jeśli w $S_k'$ nie ma jakiegoś liścia, to musi oznaczać, że ten pokolorowany wierzchołek, jest na jedynej drodze która prowadzi wyłącznie do tego liścia. W przeciwnym przypadku, bylibyśmy w stanie pokolorować kilka liści, do których jesteśmy w stanie dojść z tego wierzchołka (idąc oczywiście wyłącznie w dół drzewa).

A zatem możemy przekolorować ten wierzchołek na liścia.

To oznacza, że $S_k' \;\setminus\; \text{Leafs}(T) = S_{k-2}'$. Ale wiemy, że $S_{k-2}$ jest najbardziej optymalne, zatem $|S_{k-2}'| \le |S_{k-2}|$. Czyli $|S_k'| \le |S_k|$

![[IMG_0188.jpeg]]