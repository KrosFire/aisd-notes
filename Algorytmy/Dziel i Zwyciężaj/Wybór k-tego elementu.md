
## Problem

Na wejściu otrzymujemy listę liczb $T$ oraz liczbę $k$. Naszym celem jest zwrócenie $k$-tej co do wielkości liczby z $T$.

## Algorytm magicznych piątek

Prosty przypadek, jest wtedy, gdy $T$ jest dosyć małe. Np. gdy zawiera tylko $5$ elementów. Wtedy posortujemy takie $T$ i zwrócimy $k$-ty element.

Jeśli $T$ jest duże wybieramy jakiś element $p$ z $T$ i tworzymy listę $U$, elementów mniejszych od $p$. Dzięki temu dzielimy listę $T$ na dwie grupy i na podstawie ich wielkości, jesteśmy w stanie ocenić, w której grupie, znajduje się $k$-ty element.

Wykonujemy się rekurencyjnie, na odpowiedniej liście:

```python
if k <= U.len():
	return SELECT(k, U)
return SELECT(k-U.len(), T-U)
```

Jednakże widzimy, że wszystko zależy od wyboru pivota. Najlepszym możliwym pivotem, byłaby mediana $T$, ponieważ podzieliłaby go na pół.

Optymalnym sposobem na znalezienie mediany w liście, jest podzielenie sobie $T$, na $5$ elementowe listy $C_i$.

Następnie znalezienie median tych list $m_i$ w prosty sposób, gdyż są to bardzo małe listy.
Z median tych, tworzymy zbiór $M$, który przekazujemy do funkcji $SELECT(M, \frac{M}{2})$

## Złożoność

Okazuje się, że gdy funkcja $SELECT$, wykorzystuje algorytm szybkiego znajdowania mediany, to znajduje ona $k$-ty element w czasie liniowym. 🤯

### Dowód

Gdy mamy $p$ wybrane metodą magicznych piątek, to istnieje $\lceil\frac{1}{2}\frac{n}{5}\rceil$ grup, których mediana jest nie mniejsza od $p$.

W każdej z tych grup, istnieje co najmniej $3$ elementy, które są mniejsze od $p$, poza ostatnią, która zawiera samo $p$. Jest tak ponieważ ostatnie dwa elementy, mogą być skrajnie większe od $p$, gdyż dzieliliśmy te grupy po kolei bez sortowania.

A więc mamy $3(\lceil\frac{n}{10}\rceil - 1)$ elementów mniejszych od $p$.

Tyle elementów odrzucamy, w każdym wywołaniu. A zatem wzór rekurencji jest następujący.

$$
T(n)=T(\frac{n}{5})+T(\frac{7}{10}n)+\Theta(n)
$$
$T(\frac{n}{5})$ wynika z tego że wywołujemy funkcję $SELECT$ aby znaleźć medianę median. Czyli na zbiorze o wielkości $\frac{n}{5}$

$T(\frac{7}{10}n)$ wynika z tego że usuwamy zawsze $\frac{3}{10}n$ elementów, co do których mamy pewność, że nie ma w nich $k$.

Jeśli rozwiniemy ten ciąg otrzymamy:
$$
T(n)=...+\frac{89}{100}n+\frac{9}{10}n+n
$$
Jest to więc ciąg geometryczny. A zatem jego suma jest równa:
$$
O\bigg(
\frac{n}
{1-\frac{9}{10}}
\bigg)=

O(n)
$$
$$
T(n)=O(n)
$$

## Przypadek podziału na 3

Gdy podzielimy listę na $3$ elementy, zamiast $5$, otrzymamy następującą rekurencję

$$
T(n)=T(\frac{n}{3})+T(\frac{4}{6}n)+\Theta(n)=
T(\frac{n}{3})+T(\frac{2}{3}n)+\Theta(n)
$$
Gdy rozwiniemy otrzymamy:
$$
T(n)=...+\frac{n}{3}+\frac{2}{3}n+n=...+2n \to O(n\log_{\frac{3}{2}n})
$$

Możemy też tego nie rozwijać i zauważyć że na każdej wysokości wykonujemy do $n$ operacji i wysokość tego drzewa wynosi w najdalszej krawędzi $log_\frac{3}{2}n$

Możemy też zastosować pewną optymalizację, która stworzy nam optymalny scenariusz. Mianowicie, gdy ustalimy że $k$-ty element znajduje się w pewnym zbiorze, możemy bez straty złożoności czasowej (będziemy przechodzić po $O(n)$ elementach wykonując operacje w czasie stałym) sprawdzić czy na pewno elementy potencjalnie skrajnie małe/duże, są takowe. Sprawi to, że w optymalnej sytuacji, zawsze będziemy się wywoływać na zbiorze $\frac{n}{3}$.

Wtedy nasz wzór rekurencyjny będzie wyglądał tak:
$$
T(n)=T(\frac{n}{3})+T(\frac{n}{3})+n=2T(\frac{n}{3})+n
$$

Z [[Master theorem]]
$$
n^{\log_32+\epsilon}=n
$$
$$
O(n)
$$

## Algorytm Hoar'a

Zamiast wyboru magicznych piątek, szukamy pivota w sposób losowy

## Lazy select

Przebieg algosa:

![[Screenshot 2023-04-16 at 20.24.24.png]]

![[Screenshot 2023-04-16 at 20.25.08.png]]

### Właściwości

Jeśli do próbki $R$ trafi tylko jeden element, to algorytm ten zawsze zawiedzie, gdyż zbiór $P$ będzie równy zbiorowi $S$, a zatem:

$$
|P|=n > 4n^{\frac{3}{4}}+2
$$

### Znalezienie drugiego co do wielkości elementu

Wpierw za pomocą drzewa porównań, znajdujemy pierwszy co do wielkości element. Zajmuje to nam $n-1$ porównań.

Następnie musimy znaleźć największy z elementów, które przegrały z pierwszym elementem. Jest ich $\lceil \log n \rceil$. A zatem potrzebujemy $\lceil \log n \rceil - 1$ dodatkowych porównań. Czyli sumarycznie mamy $\lceil \log n \rceil + n - 2$ porównań