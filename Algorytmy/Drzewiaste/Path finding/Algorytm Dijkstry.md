## przebieg algorytmu:
- zaznacz wszystkie wierzchołki jako nieodwiedzone i zrób z nich zbiór
- ustaw wszystkim wierzchołkom dystans $+\infty$ oprócz wierzchołka początkowego, któremu damy dystans 0
- powtarzaj:
	- Dla obecnego wierzchołka sprawdź wszystkie nie odwiedzone wierzchołki sąsiadujące z nim i policz ich odległość, poprzez sumę odległości obecnego wierzchołka i wagę krawędzi. Jeśli suma ta jest większa bądź równa obecnie przypisanej odległości danego wierzchołka, to ją zostaw, w p. p. zamień ją.
	- Po analizie wszystkich sąsiadów, ustaw obecny wierzchołek jako odwiedzony i usuń ze zbioru nieodwiedzonych
	- Jeśli odwiedzony wierzchołek był wierzchołkiem docelowym, lub najmniejszy dystans ze zbioru wierzchołków nieodwiedzonych ma wartość $+\infty$ to essa
	- Jeśli nie to wybieramy wierzchołek o najmniejszej odległości.


```python
def dijkstra(graph, source):
	for v in graph.Vertices:
	    dist[v] = INFINITY
	    prev[v] = UNDEFINED
	    queue.add(v)
	
	dist[source] ← 0
      
	while queue is not empty:
	    u = queue.dequeue()

        for v in u.neighbours_in(graph):
			if v not in queue:
				queue.add(v)
	        alt = dist[u] + graph.Edges(u, v)
	        if alt < dist[v]:
		        dist[v] = alt
		        prev[v] = u
			
      return dist[], prev[]
```

## Dowód poprawności:

Indukcja:

Dystans ustawiony dla odwiedzonych wierzchołków jest najmniejszym dystansem ze źródła do tego wierzchołka, a dystans dla nieodwiedzonych wierzchołków jest najmniejszym dystansem ze źródła **wyłącznie** poprzez odwiedzone już wierzchołki.

Dla n = 1

Gdy jest tylko jeden odwiedzony wierzchołek twierdzenie jest trywialnie prawdziwe

Dla n+1

Wybieramy wierzchołek u, nieodwiedzony u jako nasz następny wybór.

Załóżmy że dany wierzchołek u, nie jest najbliższym nieodwiedzonym wierzchołkiem w tym momencie.

Mamy dwie możliwości:

1. Najkrótsza ścieżka zawiera wierzchołek nieodwiedzony:
		Niech pierwszy nieodwiedzony wierzchołek na krótszej drodze do u, będzie wierzchołkiem w. W takim razie dist(u) <= dist(w), ponieważ algorytm wybrał u. Do tego ścieżka z w do u kosztuje co najmniej dist(w) + x. Gdzie x to długość najkrótszej ścieżki z w do u. Mamy zatem sprzeczność że dist(w) + x < dist(u), gdy dist(u) <= dist(w)
2. Najkrótsza ścieżka nie zawiera wierzchołka nieodwiedzonego
		To oznacza że istnieje wierzchołek nieodwiedzony w, którego dist(w) < dist(u), co jest sprzeczne, ponieważ algorytm wybrałby w tej sytuacji wierzchołek w.

Gdy przejdziemy już do wierzchołka w i zaktualizujemy wagi nieodwiedzonych wierzchołków, to wagi te będą najmniejsze możliwe na ten moment, ponieważ jeśli waga byłaby mniejsza, to zamienilibyśmy ją na mniejszą.

## Złożoność obliczeniowa

Ponieważ będziemy przechodzić po każdym wierzchołku i zdejmować go z listy nieodwiedzonych, to cała to operacja zajmie nam O(V log V) czasu.

Odwiedzimy również wszystkie krawędzie jeden raz, ponieważ pomijamy krawędzie z wierzchołkami już odwiedzonymi i aktualizujemy wagi w czasie stałym.

Końcowa złożoność obliczeniowa wynosi: O(E + V log V)