![[Screenshot 2023-07-02 at 13.45.41.png]]

Liniowy zamortyzowany czas UNION FIND'a można udowodnić w następujący sposób.

UNION jak zawsze, jest w czasie stałym.

FIND'a obarczamy kosztem tylko w trzech przypadkach:

1. Wierzchołek jest korzeniem
2. Wierzchołek jest dzieckiem korzenia.
3. FIND, podpina wierzchołek pod korzeń

Wszystkie inne przypadki, to wierzchołek ponosi koszt.

Koszt Finda jest w takim razie nie większy, niż dwukrotna ilość operacji FIND. Ponieważ zakłądając najgorszy scenariusz, że zawsze występuje przypadek drugi i trzeci, to FIND ponosi koszt równy $2$, ponieważ najpierw koszt odwiedzenia danego wierzchołka, a potem korzenia.

Zapisując to matematycznie:
$$
\text{COST}(\forall\; \text{FIND}) \le 2|\text{FIND}| \le 2|\sigma|
$$

Czyli mamy liniowy koszt operacji FIND, a co z kosztem wierzchołków?
Będzie ich co najwyżej tyle, co wierzchołków, które nie są korzeniami. Ilość korzeni zmniejsza się o $1$, z każdą operacją UNION. Początkowo jest ich $n$. Zatem:

$$
\text{COST}(\forall\; v) \le n - (\#\text{liczba korzeni}) = n - (n-|\text{UNION}|) \le n
$$

A zatem całkowity koszt zamortyzowany FIND'ów wynosi:
$$
O(2n+n)=O(n)
$$