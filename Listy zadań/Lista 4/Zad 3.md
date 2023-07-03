![[Screenshot 2023-06-17 at 18.44.04.png]]

Aby znaleźć optymalne rozwiązanie, spróbujemy rozważyć wszystkie możliwe wybory. Zbudujemy w tym celu dwie macierze $n\times n$. Będziemy szli po przekątnych i w jednej macierzy ($dp$) będziemy zapisywać ile nas będzie kosztował algorytm w najgorszym przypadku, a w drugiej macierzy ($s$), jakie elementy odkryliśmy. W pierwszej przekątnej macierzy $\forall_{i=1...n}\;dp[i][i]$ wartościami będą oczywiście $c_i$. Zaś w $s[i][i]$ będą wartości $i$.

Następnie będziemy szli przekątnymi i wstawiali do komórek $dp$ wartości:

$$
dp[i][j] = \min_{i\le m\le j}\{c_m+\max(dp[i][m-1],\; dp[m+1][j])\}
$$

A do komórek $s$, te indeksy komórek, które wybraliśmy do $dp$.

Komórka $dp[i][j]$ przechowuje średni koszt odkrycia komórek od $i$ do $j$

Dlaczego to działa?

Odkrywając komórkę $m$ $A[m]$ może być większe, bądź mniejsze od $k$. Czyli pójdziemy, albo do $dp[m+1][j]$ albo do $dp[i][m-1]$. 

Czas: $O(n^3)$ - przez znajdowanie $\min_m$
Pamięć: $O(n^2)$