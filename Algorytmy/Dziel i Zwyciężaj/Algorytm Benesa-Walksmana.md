Algorytm typu dziel i zwyciężaj, który konstruuje sieć przełączników, zdolną do implementacji dowolnej permutacji sygnałów wejściowych.

![[Screenshot 2023-03-19 at 20.04.15.png]]

Głębokość takiej sieci wyraża się równaniem:

$$
D(1) = 1
$$
$$
D(2^k)=D(2^{k-1})+2
$$
$$
D(n)=D(\frac{n}{2})+2
$$
$$
O(n^{\log_21})=O(1)=f(x) \implies \Theta(\log n)
$$

Dokładna jednak ilość warstw wynosi: $2\log n-1$, ponieważ każda z $\log n$ podsieci posiada $2$ warstwy, prócz ostatniej - środkowej, która posiada $1$.

Ilość przełączników wyraża się równaniem:
