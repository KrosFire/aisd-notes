## Problem

Na wejściu mamy listę macierzy macierzy. Jeśli macierz $M_i$ ma wymiary: $b \times c$, to macierz $M_{i-1}$ ma wymiary $a \times b$ a $M_{i+1}$ wymiary $c \times d$

Naszym celem jest znalezienie optymalnego nawiasowania - kolejności mnożenia, który zminimalizuje nam ilość operacji.

Cena operacji mnożenia macierzy $M_iM_{i+1} = b\cdot c\cdot d$

## Rozwiązanie

Zróbmy to dynamicznie, czyli zacznijmy od podstawowych operacji i iteracyjnie zwiększajmy nasz zakres.

Stwórzmy 2 macierze: $m$ i $p$. W macierzy $m$ będziemy przechowywać minimalny koszt mnożenia macierzy od wiersza $i$, do kolumny $j$. A w macierzy $p$, indeks ostatniej macierzy w pierwszym nawiasie.

Na początku wypełnimy macierz diagonalę $m$ zerami - ponieważ nie mnożymy macierzy przez samą siebie.

Następnie iteracyjnie zwiększamy zakresy mnożenia macierzy i obliczamy ich cenę na podstawie tego wzoru:

$m_{ij}=min_{i\le k<j}(m_{ik}+m_{(k+1)j}+d_{i-1}d_kd_j)$
$p_{ij}=k$ dla którego osiągamy minimum

Gdzie $d_i$ jest równe ilości kolumn $i$-tej macierzy.
Uznajemy że $d_0$ jest równe ilości wierszy pierwszej macierzy.

## Złożoność

Ponieważ iterujemy się po górnym trójkącie, to złożoność będzie wynosiła tyle ile suma ciągu arytmetycznego, czyli $O(n^2)$. Do tego w każdym kroku, liczymy do $n$ sum, aby znaleźć minimum. A zatem ostateczna złożoność wynosi: $O(n^3)$

Odtworzenie kolejności mnożeń zajmie nam $O(n)$, ponieważ sprowadzi się do schodzenia w lewo w dół, lub po przekątnej.

Pamięciowo mamy dwie macierze, także: $O(n^2)$