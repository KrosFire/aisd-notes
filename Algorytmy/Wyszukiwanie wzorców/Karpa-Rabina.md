Algorytm ten wykorzystuje hashowanie, aby wstępnie wyeliminować dużą ilość porównań słów, które są kosztowne.

Algorytm działa następująco:

- Hashujemy słowo $P$
- Przechodzimy po słowie $T$ i sprawdzamy po kolei hashe ciągów o długości $m$
- Jeśli hash podsłowa jest taki sam jak hash $P$, to sprawdzamy czy na pewno jest to to samo słowo.

Algorytm ten średnio działa bardzo dobrze, w złożoności $O(m+n)$. Niestety może się zdarzyć sytuacje, że wszystkie podciągi w $T$ mają ten sam hash co $P$ (niekoniecznie muszą być one równe $P$), co sprawi że złożoność może wynosić nawet $O((n-m+1)m)$.

Przykładowa funkcja hashująca:
$d$ - rozmiar słownika
$p$ - hash
$s_i$ - $i$-ta litera w słowie
$q$ - liczba pierwsza
$$
p = (dp+s_i)\;\mathrm{mod}\; q
$$