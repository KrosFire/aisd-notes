![[Pasted image 20230617170810.png]]

A)
Macierz Teoplitza wygląda następująco:
![[Pasted image 20230617170846.png]]

Dzięki temu, możemy ją łatwo zapisać w formie wektora o długości $2n-1$
![[Pasted image 20230617170954.png]]

Czyli wystarczy że dodamy do siebie dwa wektory o długości $2n-1$, zatem wykona się to w czasie $O(n)$.

B)

Macierz Teoplitza możemy podzielić na 4 mniejsze macierze, gdzie macierz w lewym górym i prawym dolny rogu, są takie same.

$$
\bigg[
\begin{array}{cc}
A & B \\
C & A
\end{array}
\bigg]
\bigg[
\begin{array}{cc}
u \\
v
\end{array}
\bigg]
=
$$
$$
=
\bigg[
\begin{array}{cc}
Au + Bv \\
Cu + Av
\end{array}
\bigg]
=
$$
$$
=
\bigg[
\begin{array}{cc}
Au + Bv + (Av - Av) \\
Cu + Av + (Au - Au)
\end{array}
\bigg]
=
$$
$$
=
\bigg[
\begin{array}{cc}
A(u + v) + v(B - A) \\
A(v + u) + u(C - A)
\end{array}
\bigg]
$$

Wystarczy więc że policzymy te trzy rzeczy:
$$
X = A(u + v)
$$
$$
Y = v(B - A)
$$
$$
Z = u(C - A)
$$

Jeśli $n$ nie jest potęgą dwójki, to rozszerzymy ją, do najbliższej potęgi dwójki: $n' = 2^{\lceil\log_2n\rceil}$

Przy rozszerzaniu macierzy, w niewiadome wartości wstawimy $0$, a przekątne możemy wypisać zgodnie z poprzednimi wiadomymi. Wektor zaś rozszerzymy o same zera. Dzięki zerom w wektorze, kolumny nie zaburzą nam wyniku, a dodatkowych wierszy, nie będziemy po prostu czytać.

![[Pasted image 20230617175243.png]]

W każdym wywołaniu, będziemy odjemować/dodawć do siebie macierze o rozmiarch $\frac{n}{2}$. Oraz będziemy się wywoływać trzy razy na macierzach o rozmiarze $\frac{n}{2}$. Czyli wzór rekurencyjny wygląda następująco:

$$
T(n) = 3T(\frac{n}{2})+O(n)
$$
$$
n^{\log_ba} = n^{\log_23}
$$
$$
n^{\log_23-\epsilon} = n
$$
Czyli z [[Master theorem]]:
$$
O(n^{\log_23})
$$