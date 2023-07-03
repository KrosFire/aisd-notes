![[Screenshot 2023-06-20 at 18.09.21.png]]

Algorytm będzie miał dwie fazy: _Split_ i _Merge_

W fazie _Split_ przejdziemy się od korzenia drzewa, aż do liści. Jeśli na naszej drodze napotkamy wierzchołek z wartością $<k$, pójdziemy w prawo, w p. p. w lewo. Za każdym razem, gdy zmienimy kierunek schodzenia w dół drzewa (czyli kiedy rodzic ma wartość $<k$ a dziecko $>=k$ i na odwrót), będziemy odcinać poddrzewo, którego korzeniem jest wierzchołek, na którym obecnie się znajdujemy i wstawimy go, do odpowiedniego zbioru drzew.

Przykład:
![[IMG_0193.jpeg]]

Operacja ta zajmie nam $O(\log n)$ czasu, ponieważ taką wysokość ma drzewo AVL.

Mamy teraz mały problem, ponieważ drzewa w tych zbiorach, niekoniecznie są drzewami AVL i jest ich wiele.

Musimy je zmergować i naprawić. Samo mergowanie będzie polegać na podczepieniu niższego drzewa pod wyższe.

Takie podczepianie zawsze zachowa własności BST, ponieważ jeśli drzewa są w tej samej grupie i jedno z nich jest niższe od drugiego, to drzewo niższe zostało odcięte w poddrzewie drzewa wyższego. Własność ta będzie zachowana podczas mergowania wielu drzew, gdy będziemy mergować dwa najmniejsze drzewa ze sobą. Podpinając drzewo niższe pod korzeń wyższego, nie zwiększamy wysokości, a ewentualne rotacje, jedynie zmniejszą wysokość.

Ilość rotacji potrzebnych do naprawienia zmergowanych drzew jest równy różnicy ich wysokości.

Oznaczmy wysokość drzew od najmniejszego do najwyższego: $h_1,h_2,...,h_k$, gdzie $h_k \le \log n$.

$h_i' \le h_i$ - to wysokość $i$-tego co do wielkości drzewa po zmergowaniu go z $1,...,i-1$ mniejszymi drzewami.

Policzmy wszystkie rotacje:

$$
(h_2-h_1)+(h_3-h_2')+...+(h_k-h_{k-1}') \le h_k-h_1+c\cdot\log n
$$
$$
h_k-h_1 \le h_k
$$
$$
h_k \le \log n
$$

Także sumaryczny czas to: $O(\log n)$