Sortowanie topologiczne polega na posortowaniu wierzchołków w grafie skierowanym (bez cykli)  tak aby kolejne wierzchołki nie posiadały krawędzi skierowanych wstecz

## BFS

Na wejściu posiadamy listę wierzchołków.

Tworzymy pustą listę posortowanych elementów.

Przechodzimy po wejściowej liście wierzchołków i przenosimy do posortowanej listy te wierzchołki które nie mają krawędzi wejściowych.

Ustawiamy `queue_pointer = 0`.

Póki wejściowa lista nie jest pusta:
		Bierzemy wierzchołek z posortowanej listy na indeksie `queue_pointer`
		Zmniejszamy liczbę krawędzi wejściowych w wierzchołkach w wejściowej liście.
		Jeśli wierzchołek posiada ich liczbę równą 0, to przenosimy go do posortowanej listy.
		Zwiększamy `queue_pointer`

Złożoność czasowa to $O(|V| + |E|)$ ponieważ musimy przejść po wszystkich wierzchołkach i przeprowadzamy sałą czasowo operację inkrementacji `queue_pointer`'a -ergo $|V|$

Do tego przechodzimy po wszystkich krawędziach i je usuwamy, co można wykonać w czasie stałym ergo $|E|$

## DFS

Algorytm DFS będzie polegać na tym, że szukamy nim wierzchołkach o `indegree = 0` i dodajemy go do listy posortowanej i usuwamy z przyszłych rozważań. Powtarzamy do skutku

Złożoność czasowa to również będzie $O(|V| + |E|)$
