Problem wyszukiwania wzorców możemy też rozwiązać za pomocą automatu skończonego. Czyli takiego algorytmu, o którym możemy myśleć jak o maszynie, która przechodzi z jednego stanu w drugi, na podstawie pewnych zasad.

Na początku parę definicji:

$Q$ - zbiór stanów naszej maszyny. Będą to liczby ze zbioru $\{1,2,...,m\}$, które będą reprezetnować, do którego momentu dany napis się zgadza.

$q_0 = 0$ - stan początkowy.

$A = \{m\}$ - zbiór stanów końcowych.

$\sigma(x)$ - długość najdłuższego prefixa $P$, który jest suffixem $x$-a.

$\delta(q, a) = \sigma(P_qa)$ - funkcja obliczająca stan po uwzględnieniu $a$.

Nie biorąc pod uwagę obliczania $\delta$, uzyskamy złożoność $O(n)$

Koszt $\delta$ zaś można ograniczyć przez $O(m|\Sigma|)$