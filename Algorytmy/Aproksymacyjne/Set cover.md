Na wejściu otrzymujemy zbiór - uniwersum $U$ oraz $m$ podzbiorów $s_1,s_2,...,s_m$, gdzie $\forall s_i \in U$ posiada koszt $c_i$.

Celem algorytmu jest stworzenie zbioru $X$ zbirów $s_i$, który pokrywa $U$ najmniejszym kosztem.

## Prosta heurystyka

Naturalnym pomysłem będzie użycie zachłannego algorytmu, który w każdym kroku rozważy dany zbiór na podstawie relacji jego kosztu $c_i$ do ilości elementów, które nam pokryje $u_i$, czyli nasza heurystyka będzie wyglądać: $\frac{c_i}{u_i}$

### Optymalność

Niech $k$ będzie liczbą niepokrytych elementów w danym kroku, przed wyborem zbioru. Istnieje pewien optymalny zbiór, który używa części z pozostałych zbiorów, do pokrycia reszty uniwersum. Niech $T_{OPT}$ będzie zbiorem indeksów tego optymalnego zbioru. Niech $OPT$ będzie kosztem optymalnego rozwiązania. Oczywistym jest więc, że:
$$
min\bigg(\frac{c_i}{u_i}\bigg)\le
\frac{\sum_{i\in T_{OPT}} c_i}{\sum_{i\in T_{OPT}} u_i}\le
\frac{OPT}{k}
$$

$$
\sum_{i\in T_{OPT}} c_i \le OPT
$$
zachodzi ponieważ te zbiory są podzbiorem optymalnego rozwiązania.

$$
\sum_{i\in T_{OPT}} u_i \ge k
$$
zachodzi ponieważ w danym momencie istnieje $k$ nie pokrytych elementów, a wiemy, że $\sum_{i\in T_{OPT}} u_i$ pokrywa taką ilość.

W każdym kroku, po wybraniu $i$-tego zbioru, koszt tego zbioru, rozdzielimy koszt tego zbioru równo po nowo pokrytych elementach. Koszt dla $j$-tego elementu będzie wynosić maksymalnie $\frac{OPT}{n-j+1}$, ponieważ w momencie pokrycia $j$ elementu, będzie maksymalnie $n-j+1$ niepokrytych elementów. Jeżeli rozwiniemy tę sumę, to zauważymy, że sprowadza się ona do takiej sumy:
$$
OPT\sum_{j=1}^n\frac{1}{j}=OPT\cdot H_n = OPT\cdot O(\log n) 
$$