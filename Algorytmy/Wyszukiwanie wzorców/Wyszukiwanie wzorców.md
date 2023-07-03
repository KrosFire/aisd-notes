Naszym zadaniem jest znalezienie wszystkie wystąpienia pewnego napisu $P$ o długości $m$ w słowie $T$ o długości $n$, stworzonych na słowniku $\Sigma$.

## Algorytm naiwny

Oczywiste rozwiązanie które się nasuwa to przechodzenie po $T$ i sprawdzanie, czy od tego momentu występuję słowo $S$. Niestety złożoność tego algorytmu jest dosyć duża, mianowicie:
$O((n-m+1)m)$

