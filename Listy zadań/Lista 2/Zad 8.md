![[Screenshot 2023-06-16 at 21.16.02.png]]

Dowolne rozwiązanie musi zawierać ścieżkę przechodzącą przez centroid.
Algorytm można podzielić na 3 kroki:
1. Znaleźć centroid
2. Znaleźć dwa najbardziej oddalone liście od centroidu (w różnych kierunkach)
3. Znaleźć trzeci liść, który jest najbardziej oddalony od ścieżki dwóch wcześniej znalezionych punktów.

Punkt pierwszy, jest prosty do wykonania poprzez iteracyjne odcinanie liści. Wykona się więc w czasie $O(|V|+|E|)$. W sytuacji kiedy centroidem mogą być dwa wierzchołki wybieramy losowo jeden z nich.

Drugi punkt będzie polegał na tym, aby DFS'em odpalonym z centroidu, znaleźć dwie największe odnogi i ustalić liście tych odnóg jako dwa punkty - $a$ i $b$. DFS zajmie oczywiście $O(|V|+|E|)$

W trzecim punkcie będziemy przechodzić po wszystkich wierzchołkach na ścieżce pomiędzy $a$i $b$ i będziemy odapalać DFS'a, na odnogach które nie znajdują się na ścieżce. Liść najdłuższej odnogi jest naszym trzecim punktem. Jest tak dlatego, że nie ma znaczenia, w którym miejscu znajduje się odnoga w relacji do $a$ czy $b$, ponieważ jeśli odnoga jest o $1$ bliżej $a$, to jest o $1$ dalej od $b$. Jedyne co jest ważne, to ile krawędzi, jeszcze jesteśmy w stanie wcisnąć.

