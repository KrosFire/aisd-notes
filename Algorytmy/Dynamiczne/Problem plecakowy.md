## Problem

Na wejściu mamy zbiór $n$ rzeczy o wagach $w_i$ i wartości $v_i$ oraz maksymalną wagę $W$. Naszym celem jest stworzenie zbioru, lub też multizbioru elementów, których sumaryczna wage nie przekracza $W$ a sumaryczna wartość jest największa możliwa.

## Wariant z powtórzeniami

Możemy zapakować wiele tych samych elementów do plecaka.

Tworzymy więc listę $k$ o długości $W$.

Przechodzimy po niej kursorem $i$ od zera do $W$ i w każdym kroku, wybieramy z listy $n$ elementów, te elementy, o wadze $w \le i$.
Następnie sprawdzamy, który z tych elementów da nam maksymalną wartość.

Czyli:
$K[0] = 0$
$K[i] = max_{1\le k \le n}(K[i-w_k]+v_k)$

Zatem złożoność naszego algorytmu wynosi: $O(Wn)$

Jest więc to złożoność **pseudo wielomianowa** ponieważ jej wartość jest zależna od wartości jednego z parametrów $W$, a nie ilości danych.

## Wariant bez powtórzeń

W tym przypadku stworzymy macierz $n \times W$, gdzie każda kolumna będzie oznaczać dostępną wagę, a wiersz, że mamy do wyboru dany $i$-ty produkt i wszystkie inne z wierszy wyżej.

Będziemy uzupełniać tą macierz od góry do dołu, od lewej do prawej, gdzie w każdej krotce będzie wartość najbardziej optymalnej konfiguracji przedmiotów w plecaku, dla danej wagi i danych możliwych produktów

Będzie się to wyrażać następującym wzorem:
$$
m[i][j] = max(m[i-1][j-w_i]+v_i,\;\; m[i-1][j])
$$

Czyli sprowadza się to do tego, że w każdym kroku sprawdzamy, co jest bardziej opłacalne:

1. Dodanie i-tego elementu i wybranie najbardziej optymalnej konfiguracji dla przestrzeni która nam została
2. Albo zadowolenie się obecnie najlepszą konfiguracją rzeczy, bez tego elementu.

Algorytm ma taką samą złożoność jak poprzednio, czyli: $O(nW)$