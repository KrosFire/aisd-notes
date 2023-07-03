Algorytm zachłanny znajdujący [[Grafy#^148579| MDR]] dla spójnego grafu

Jest bardzo podobny do [[Algorytm Kruskala | algorytmu Kruskala]]

## Przebieg algorytmu
-   Utwórz las L z wierzchołków oryginalnego grafu – każdy wierzchołek jest na początku osobnym drzewem.
- Utwórz pusty zbiór S
- Dopóki las posiada więcej niż jedno drzewo:
	- Znajdź najtańszą krawędź, która łączy dwa różne lasy
	- Jeśli krawędzi nie ma w MST S, dodajemy ją do S

Po zakończeniu $S$ jest naszym MST

## Dowód

Taki sam jak np. w [[Algorytm Kruskala | Algorytmie Kruskala]]

## Złożoność

Algorytm Boruvki działa w czasie $E\log(V)$

Uzasadnienie:

W każdej iteracji przechodzimy przez $E$ krawędzi

W najgorszym przypadku, w każdym kroku dla $X$ komponentów, otrzymamy $\lceil\frac{X}{2}\rceil$ komponentów.
Będzie tak ponieważ znajdziemy dla każdego komponentu krawędź minimalną, łączącą ją z innym komponentem. W najgorszym przypadku, najtańsza krawędź komponentu $x$, łącząca ten komponent z komponentem $y$, będzie również najtańszą krawędzią komponentu $y$. 

Oznacza to, że główna pętla, wykona się $O(\log(V))$ razy. A zatem, złożoność będzie wynosić $O(E\log(V))$

W każdej operacji, musimy sprawdzić również przynależność dwóch wierzchołków do zbiorów oraz połączyć zbiory, jednak operacje te zajmują $\log(V)$ czasu, czyli mniej niż $E$.