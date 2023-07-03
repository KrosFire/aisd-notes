Celem zadania z siecią przełączników, jest stworzenie sieci przełączników, o najmniejszej możliwej głębokości, która dla danej liczby $n$ wejść będzie implementować wszelkie możliwe permutacje tych wejść: $\pi(n)$

Zazwyczaj dla ułatwienia, zakłada się że $n=2^k$.

Jeden przełącznik jest w stanie wygenerować $2$ permutacje

Parametrami sieci są:
- Ilość przełączników - $S(n)$
- Ilość warstw przełączników - głębokość - $D(n)$

Celujemy w minimalizowanie tych parametrów. Niestety jednak, muszą one wynosić co najmniej:

$$
2^{S(n)}\ge n! \implies S(n) \ge \log n!
$$
Czyli:
$$
S(n) \ge n\log n
$$

Jest tak ponieważ jeden przełącznik generuje $2$ permutacje, a $\pi(n)=n!$

$$
D(n)\ge \log n
$$

Jest tak ponieważ $k$ warstwa sieci, sprawia że ilość drutów, na której może się znaleźć jedno wejście, jest równe $2^k$, a my chcemy, aby dane wejście, mogło się znaleźć na wszystkich $n$ drutach wyjściowych.

$$
2^k \ge n
$$
$$
k \ge \log n
$$
