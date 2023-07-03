Algorytm zachłanny wyznaczający [[Grafy#^88c0fc | MDR]]

## Przebieg algorytmu
- Wybierz dowolny wierzchołek grafu
- Utwórz kolejkę priorytetową z wierzchołkami osiągalnymi z obecnego MDR (na początku 1 wierzchołek)
- Powtarzaj:
	- Wybierz wierzchołek z kolejki, którego nie ma w MDR
	- Dodaj do MDR wierzchołek i krawędź
	- Zaktualizuj kolejkę o nowe krawędzie i wierzchołki

## Dowód poprawności:

W każdym momencie algorytmu Prima, drzewo stworzone przez ten algorytm jest drzewem MDR.

Gdy w pierwszym kroku dodajemy dowolny wierzchołek, to jest to MDR, ponieważ każde MDR zawiera każdy wierzchołek drzewa - trywialne

w $n > 1$ kroku posiadamy graf $G_{n-1}$ który jest poddrzewem MDR, drzewa MDR $Y_{n-1}$ i algorytm Prima wybrał krawędź $e$ łączącą wierzchołek $v_e$ w grafie $G_{n-1}$ z wierzchołkiem $u_e$ poza grafem $G_{n-1}$.
1. e istnieje w $Y_{n-1}$ ergo $Y_{n} = Y_{n-1}$
2. e nie istnieje w $Y_{n-1}$
	1. Istnieje ścieżka w drzewie $Y_{n}$ łącząca graf $G_{n-1}$ z wierzchołkiem $u_e$. Ścieżka ta zawiera krawędź $f$ łączącą wierzchołek $v_f$ należący do $G_{n-1}$ i $u_f$ nienależący do $G_{n-1}$. Krawędź f musi mieć wagę większą lub równą krawędzi $e,$ w p. p. algorytm Prima wybrał by właśnie krawędź $f$. To oznacza że po usunięciu z drzewa $Y_n$ krawędzi $f$ i dodaniem krawędzi $e$, drzewo $Y_n$ nie staje się cięższe i nie tworzy się cykl.

## Złożoność

Używając kopca, wstawiamy tam wszystkie wierzchołki z wagami $+\infty$ i z czym się łączą - na start $NULL$. Początkowemu wierzchołkowi nadajemy wagę $0$ - jest korzeniem kopca.

Inicjalizacja zajmuje nam $O(V)$ - przechodzimy po wszystkich wierzchołkach i wpierdalamy do listy

Następnie dla obecnego wierzchołka znajdujemy sąsiadów i aktualizujemy wagi. Aktualizacja wagi jednego wierzchołka zajmuje nam $\log V$.

Szukanie sąsiadów sprowadza się do sprawdzenia wszystkich krawędzi, możliwe że pod koniec działania algorytmu przejdziemy po wszystkich dwukrotnie, także sprawdzimy $2E$ krawędzi.

Oznacza to, że złożoność aktualizacji kopca jest następująca: $O(2E \log V) \implies O(E \log V)$

Główna pętla iterująca się po kopcu i usuwająca z niego najmniejsze wartości wykonuje się $V$ razy i przeprowadza operację kosztującą $\log V$: $O(V \log V)$

Ostateczna złożoność:
$$
O(V \log V + E \log V) \implies O((V + E)\log V) \implies O(E \log V)
$$

https://stackoverflow.com/questions/20430740/time-complexity-of-prims-algorithm

