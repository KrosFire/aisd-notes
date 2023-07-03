![[Screenshot 2023-06-21 at 16.40.00.png]]

Dane są punkty:
$$
p_1,p_2,…,p_{i-1}
$$

Załóżmy, że najmniejsza odległość między nimi to $d$

Dzielimy płaszczyznę na kwadraty o boku $d/2$. W każdym takim kwadracie jest co najwyżej jeden z punktów $p_1,p_2,...,p_{i-1}$

Będziemy pamiętać w tablicy hashującej w jakim kwadracie znajdują się te punkty.

Rozpatrując punkt $p_i$ musimy wziąć pod uwagę $25$ kwadratów. (rozrysuj sobie).

Gdy znajdziemy $d'<d$, musimy ponownie podzielić przestrzeń na kwadraty, co będzie również liniowe.

Problemem jest, gdy będziemy musieli to robić za każdym razem, ponieważ wejdziemy w $O(n^2)$.

Dlatego na samym początku, losowo przemieszamy kolejność punktów. Dzięki temu, prawdopodobieństwo, że w $i$-tym kroku, znajdziemy $d'<d$ wynosi $\frac{2}{i}$, ponieważ albo znajdziemy, albo nie.

Zatem złożoność wynosi:
$$
\sum_{i=2}^n (O(1)+\frac{2}{i}O(i))=O(n)
$$

Bardzo dobry pdf pomocniczy:

![[Aisd_L7_zad_2-1.pdf]]