![[Screenshot 2023-06-21 at 21.23.44.png]]

Dzielimy wzorzec na części, które nie są od siebie odseparowana _gc_ - gap character.

Czyli dla wzoru: $ab\text{[gc]}ba\text{[gc]}c$ posiadać będziemy $3$ oddzielne wzory:

$ab$, $ba$ oraz $c$. Wykorzystamy algorytm [[KMP - Knutha-Morrisa-Pratta | KMP]].

Czyli dla każdego wzoru obliczymy tabelę $\pi$, co sumarycznie zajmie nam $O(m)$ czasu.

Następnie przejdziemy się po tekście i będziemy wpierw szukać wzoru $ab$ i po jego znalezieniu, w tekście na prawo będziemy szukać $ba$ itd.

Algorytm KMP poradzi sobie z tym w czasie liniowym. A zatem ostateczna złożoność to:
$O(n+m)$