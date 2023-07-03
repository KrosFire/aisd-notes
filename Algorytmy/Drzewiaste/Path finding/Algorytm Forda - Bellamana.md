Znajduje najkrótszą ścieżkę ze źródła do celu w grafie skierowanym z ujemnymi wagami krawędzi

## Przebieg
- Ustawiamy wszystkim wierzchołkom dystans +nieskończoność oprócz źródłowego któremu dajemy 0
- Iterujemy się |V|-1 razy - ponieważ to jest najkrótszy dystans dzielący najdalsze wierzchołki:
	- iterujemy się po każdym wierzchołku - musimy sprawdzić wszystkie ścieżki
		- aktualizujemy dystans do danego wierzchołka v, do najmniejszej wartości

## Złożoność obliczeniowa

podwójny loop: $O(|V||E|) = O(n$[[Grafy#^13ce3b | n(n-1)/2$]]$) = O(n^3)$


## Problem

Jeśli są negatywne cykle - czyli z każdym przejściem tego cyklu dystans się zmniejsza, to algorytm nie zwróci poprawnej wartości.

Może on za to je znaleźć poprzez wykonanie dodatkowej iteracji i jeśli jakaś waga się zmniejszy, to oznacza, że mamy negatywny cykl
