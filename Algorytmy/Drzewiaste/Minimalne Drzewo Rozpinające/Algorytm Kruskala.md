Algorytm zachłanny znajdujący [[Grafy#^148579| MDR]] dla spójnego grafu

## Przebieg algorytmu:
-   Utwórz las L z wierzchołków oryginalnego grafu – każdy wierzchołek jest na początku osobnym drzewem.
-   Utwórz zbiór S zawierający wszystkie krawędzie oryginalnego grafu.
-   Dopóki S nie jest pusty oraz L nie jest jeszcze drzewem rozpinającym:
    -   Wybierz i usuń z S jedną z krawędzi o minimalnej wadze.
    -   Jeśli krawędź ta łączyła dwa różne drzewa, to dodaj ją do lasu L, tak aby połączyła dwa odpowiadające drzewa w jedno.
    -   W przeciwnym wypadku odrzuć ją.

Po zakończeniu algorytmu L jest minimalnym drzewem rozpinającym.

Kruskal's algorithm is a minimum-spanning-tree algorithm which
finds an edge of the least possible weight that connects any two
trees in the forest. It is a greedy algorithm in graph theory
as it finds a minimum spanning tree for a connected weighted
graph adding increasing cost arcs at each step. This means it
finds a subset of the edges that forms a tree that includes every
vertex, where the total weight of all the edges in the tree is
minimized. If the graph is not connected, then it finds a
minimum spanning forest (a minimum spanning tree for each
connected component).

![Kruskal Algorithm](https://upload.wikimedia.org/wikipedia/commons/5/5c/MST_kruskal_en.gif)

![Kruskal Demo](https://upload.wikimedia.org/wikipedia/commons/b/bb/KruskalDemo.gif)

A demo for Kruskal's algorithm based on Euclidean distance.

## Dowód

Niech F będzie zbiorem krawędzi uzyskanym przez algorytm Kruskala w dowolnym jego momencie.

Teza: Istnieje mst T, takie że zawiera ono wszystkie krawędzie zbioru F i żadnych, których nie wybrał algorytm Kruskala

Przeprowadźmy indukcję po rozmiarze tego zbioru - n.

Gdy n = 0, zbiór ten jest pusty, więc dowolne minimalne drzewo rozpinające zawiera ten zbiór krawędzie.

Załóżmy że minimalne drzewo rozpinające T zawiera podzbiór krawędzi F, o rozmiarze n.
Niech e będzie krawędzią wybraną przez algorytm Kruskala w następnym kroku.

1. Drzewo T posiada krawędź e, więc teza jest prawdziwa
2. Drzewo T nie posiada krawędzi e. Oznacza to, że T+e tworzy cykl - ponieważ drzewo rozpinające nie może mieć więcej krawędzi nie tworząc jednocześnie cyklu. Ponieważ e jest krawędzią o najmniejszej możliwej wadze, to musi istnieć w T krawędź e', która posiada taką samą wagę lub większą co krawędź e. Oznacza to, że T - e' + e będzie wciąż MST.
3. Co dowodzi tezie, że zbiór F tworzy minimalne drzewo rozpinające

## Złożoność

Algorytm Kruskala działa w czasie $O(E\log(V))$

Uzasadnienie:

Sortowanie wszystkich krawędzie jest w czasie $O(E\log(E))$.

Żeby sobie ładnie zamienić $\log(E)$ na $\log(V)$ robimy coś takiego:

[[Grafy#^13ce3b| E < V^2 ]]
$\log(E) < \log(V^2)$
$\log(E) < 2\log(V)$

Ergo samo sortowanie krawędzi daje nam naszą złożoność.

Następnie przechodzimy po liście tych krawędzi: złożoność $O(E)$

Sprawdzenie czy dodanie danej krawędzi stworzy cykl sprowadzi się do sprawdzenia przynależności dwóch wierzchołków w drzewiastym setcie: $2\log(V) \implies \log(V)$

Operacja union kosztuje jedynie $O(1)$