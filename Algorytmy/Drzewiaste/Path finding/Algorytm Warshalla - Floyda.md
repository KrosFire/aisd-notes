Algorytm znajduje najkrótsze ścieżki z każdego punktu, do każdego innego

Algorytm operuje na macierzach.

## Przebieg działania

- Posiadamy na początku macierz A wag połączeń bezpośrednich w grafie
- iterujemy |V| razy i uzyskujemy wierzchołek pośredni v:
	- Iteracja |V| razy i uzyskujemy wierzchołek źródłowy s:
		- Iteracja |V| razy i uzyskujemy wierzchołek docelowy d:
			- Liczymy dystans A\[s,d\] = min{A\[s, d\], A\[s, v\] + A\[v, d\]}

## Złożoność obliczeniowa

Widać że złożoność obliczeniowa to O(n^3)