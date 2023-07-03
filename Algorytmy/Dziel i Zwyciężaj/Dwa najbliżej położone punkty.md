Mając na wejściu $n$ punktów: $p_1,p_2,...,p_n$, znaleźć spośród nich dwa najbliższe sobie.

Naiwne podejście, polegające na porównywaniu wszystkich punktów ze sobą, zajmie nam co najmniej $O(n^2)$ czasu. Spróbujemy więc rozwiązać ten problem metodą dziel i zwyciężaj.

## Przebieg algorytmu

1. Sortujemy punkty po $x$ i wstawiamy do tablicy $X$
2. Sortujemy po $y$ i wstawiamy do tablicy $Y$
3. Znajdujemy prostą $l$, która dzieli punkty, na dwa równe zbiory (z dokładnością do jednego punktu). Można taką prostą znaleźć, poprzez wybranie środkowego punktu w tablicy $X$.
   Punkty po lewej stronie $l$ zapisujemy do tablicy $P_L$, a po prawej do $P_R$.
4. Wywołujemy się rekurencyjnie, aż do momentu, gdy w zbiorze znajdą się 2, lub 3 punkty i znajdujemy te, które są najbliżej siebie.
5. Z wywołań rekurencyjnych otrzymujemy **pary** punktów z lewej i prawej strony: $(i_1,j_1);(i_2,j_2)$. Wybieramy parę $(i',j')$, która jest najbliżej siebie.
6. Sprawdzamy, czy istnieje para punktów $(t,s)$ gdzie $t \in P_L$, a $s \in P_R$ taka że ich dystans, jest krótszy od dystansu $(i', j')$ - $d$

Ostatni punkt algorytmu jest kluczowy, ponieważ bez kluczowej obserwacji, narazimy się na wysoką złożoność obliczeniową.

Wiemy że punkty $t$ i $s$ znajdują się maksymalnie o $d$ od lini $l$. Zbiór tych punktów, nazwijmy $P_C$. Następnie usuńmy z $Y$, wszystkie punkty, które się nie znajdują w tym polu. Niech to będzie $Y'$. Ponieważ $Y'$ jest posortowane, to możemy iść punkt po punkcie w tej przestrzeni, z dołu na górę porównując dany punkt z resztą.

Możemy to poszukiwanie przyspieszyć, ponieważ punkty w muszą być w odległości co najwyżej $d$, również na płaszczyźnie $Y$. Czyli w każdym kroku, chodzenie z dołu na górę, mamy prostokąt, o wymiarach $2d/d$ ($2d$ - szerokość, $d$ - w górę od danego punktu). Na takim prostokącie może znaleźć się maksymalnie $8$ punktów - po $4$ na każdy kwadrat o wymiarach $d/d$.

Dzięki tym obserwacjom, dla każdego punktu w tej przestrzeni, przeiterujemy się stałe $7$ razy, dzięki czemu zejdziemy do liniówki.

Dodatkowo, zamiast sortować nadmiarowo tablice $X$ i $Y$ w każdym wywołaniu, zrobimy to raz.

## Złożoność obliczeniowa

Sortowanie elementów do tablic $X,Y$ oczywiście zajmie nam $O(n\log n)$

Znajdowanie prostej $l$ - proste $O(1)$ poprzez podział zbioru $X$ na pół

Mergowanie zajmuje nam liniowy czas: $O(7n)=O(n)$

Zatem wzór rekurencji wygląda następująco:
$$
T(n) = 2T(\frac{n}{2})+O(n)
$$
$$
n^{\log_ba}=n=f(x)
$$
$$
\Theta(n\log n)
$$