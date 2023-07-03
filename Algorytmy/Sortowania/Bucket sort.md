Bucket sort bierze idee [[Counting sort]] i aplikuje ją dla kluczy, których nie da się od razu zgrupować.

Bucket sort zmiast tablicy indeksów, tworzy $n$  kubełków - czyli list, do których wrzucamy elementy o indeksach z pewnego zakresu.

Na przykład gdy na wejściu dostajemy do posortowania listę kluczy z przedziału: $[0,1)$.
Wtedy możemy zdefiniować $n$ kubełków, którym przydzielamy liczby w taki sposób:
$\lfloor A[i]\cdot n\rfloor=\text{bucket}$

Oczywiście, wartości w tych kubełkach nie będą posortowane, dlatego na każdym z nich zastosujemy, jakiś prosty algorytm sortujący stabilnie. Np: [[Insert sort]].

Po posortowaniu każdego kubełka, łączymy je w całość.

Przez zastosowanie algorytmu sortującego, działającego w czasie $O(n^2)$, możliwą złożonością tego algorytmu jest właśnie $O(n^2)$.

Jednakże musimy wziąć pod uwagę to, że prawdopodobnie, przy dużej ilości kubełków, każdy z nich będzie miał niewiele wartości i prosty algorytm sortujący, działający nawet w czasie $O(n^2)$, na małej ilości danych, będzie działał w $O(n)$

Prawdopodobieństwo złożoności tego algorytmu można obliczyć w następujący sposób:

Niech $Y$ będzie zmienną losową równą liczbie wszystkich porównań. $Y_i$ jest zmienną losową równą liczbie porównań w $i$-tym kubełku
$$
Y = Y_1+Y_2+...+Y_n
$$

Wartość $Y_i$ zależy od wartości $X_i$, czyli prawdopdobieństwa liczby elementów w $i$-tym kubełku.
Ponieważ używamy insertion sorta:
$$
Y_i=X_i^2
$$

$X_i$ ma rozkład dwumianowy, mamy dwa wybory - albo jest w kubełku, albo go nie ma. I jest to robione dla $m$ elementów.

Czyli:
$$
E[X^2_i]=
(n\cdot\frac{1}{n})^2+n\cdot\frac{1}{n}(1-\frac{1}{n})=
2-\frac{1}{n}=
\frac{2n-1}{n}\to
2
$$
$$
E[Y]=
\sum_{i=1}^nE[Y_i]=
\sum_{i=1}^nE[X^2_i]=
\sum_{i=1}^n2=
O(2n)=
O(n)
$$

