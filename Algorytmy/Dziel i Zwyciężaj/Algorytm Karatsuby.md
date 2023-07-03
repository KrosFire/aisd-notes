Algorytm szybkiego mnożenia, dzięki któremu jesteśmy w stanie zejść ze złożoności $O(n^2)$ do $O(n^{\log_23})$.

## Przebieg

Na wejściu dostajemy $2$ liczby $n$ bitowe $x$ i $y$

Dzielimy bity tych liczb na pół i otrzymujemy $x_H,x_L,y_H,y_L$

Następnie, rekurencyjnie wywołujemy się na połowach tych liczb, do momentu, gdy nie staną się one jedno bitowe. W tym momencie zwracamy ich iloraz.

Wynik rekurencyjnie przemnożonych połówek zapisujemy do zmiennych:
$a = karatsuba(x_H,y_H)$
$d = karatsuba(y_L,y_L)$
$e = karatsuba(x_H+x_L, y_H+y_L) - a - d$
$xy = a2^n+e2^{\frac{n}{2}}+d$

## Złożoność

Dzięki podziałowi obliczeń na 3 części, nasza funkcja rekurencyjna ma następujący wzór:

$$
T(n) = 3T(\frac{n}{2})+O(1)
$$

$O(1)$ - ponieważ operacje $2^n$ sprowadzają się do operacji: `2 << n`, a dodawanie liczb tutaj przesuniętych, również może być zoptymalizowane bit-wise or-em. Zwykły sumator też sobie poradzi bez problemu.

A zatem zgodnie z  [[Master theorem]]:
$$
O(n^{\log_23-\epsilon})=O(1) \implies T(n) = \Theta(n^{\log_23})
$$

## Rozwiązanie dla dowolnego $k$

### Przykład $k = 2$

$$
a = a_0+a_12^{\frac{n}{2}}
$$
$$
b = b_0+b_12^{\frac{n}{2}}
$$
$$
ab = a_0b_0+(a_0b_1 + b_0a_1)2^{\frac{n}{2}}+a_1b_12^n
$$

Zauważmy że składowe $(a_0b_1 + b_0a_1)$ możemy poznać jednym mnożeniem:

$$
(a_0+a_1)(b_0+b_1) = a_0b_0+a_1b_1+a_0b_1+a_1b_0
$$

Złożoność:
$$
3T(\frac{n}{2})+O(1)
$$

### Przykład $k = 3$

$$
a = a_0 + a_12^{\frac{n}{3}} + a_22^{\frac{2n}{3}}
$$
$$
b = b_0 + b_12^{\frac{n}{3}} + b_22^{\frac{2n}{3}}
$$
$$
ab =
a_0b_0 +
(a_0b_1+b_0a_1)2^{\frac{n}{3}} +
(a_0b_2+b_0a_2+a_1b_1)2^{\frac{2n}{3}} +
(a_1b_2+b_1a_2)2^{n} +
a_2b_22^{\frac{4n}{3}}
$$


Wiemy, że składowe drugiej i czwartej sumy, możemy poznać tymi mnożeniami:
$$
x=(a_0+a_1+a_2)(b_0+b_1+b_2)=
a_0b_0+
a_0b_1+
a_0b_2+
a_1b_0+
a_1b_1+
a_1b_2+
a_2b_0+
a_2b_1+
a_2b_2
$$
$$
y=(a_0-a_1+a_2)(b_0-b_1+b_2)=
a_0b_0-
a_0b_1+
a_0b_2-
a_1b_0+
a_1b_1-
a_1b_2+
a_2b_0-
a_2b_1+
a_2b_2
$$
$$
z=(a_0+2a_1+4a_2)(b_0+2b_1+4b_2)=
a_0b_0+
2a_0b_1+
4a_0b_2+
2a_1b_0+
4a_1b_1+
8a_1b_2+
4a_2b_0+
8a_2b_1+
16a_2b_2
$$

Po odpowiednim zsumowaniu $x,y,z,a_0b_0,a_2b_2$, otrzymamy wszystkie potrzebne nam wyrażenia.

Mamy zatem $5$ mnożeń liczb o długości $\frac{n}{3}$.
$$
5T(\frac{n}{3})+O(1) \implies \Theta(n^{\log_35})
$$

### Dla dowolnego $k$

Dla dowolnego $k$ mamy $2k-1$ komponentów. Stoją przy nich:

$$
2^{\frac{0n}{k}},2^{\frac{1n}{k}},...,2^{\frac{(2k-2)n}{k}}
$$

Skoro mamy $2k-1$ komponentów - liczb, to ich wartość jesteśmy w stanie wyliczyć na podstawie układu $2k-1$ równań, w których ustawimy odpowiednie wagi przy każdej części składowej danej liczby - używamy macierzy Vandermonda. Dzięki czemu, uzyskamy $2k-1$ zamiast $k^2$ mnożeń.
![[Screenshot 2023-03-19 at 19.46.47.png]]
A zatem ostateczna złożoność będzie wynosić:
$$
(2k-1)T(\frac{n}{k})+O(1) \implies \Theta(n^{\log_k(2k-1)})
$$