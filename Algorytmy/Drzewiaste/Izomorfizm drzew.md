Na wejściu posiadamy dwa drzewa. Naszym celem jest sprawdzenie, czy są one izomorficzne - czyli że istnieje bijekcja z jedno drzewo na drugie.

Aby to osiągnąć w liniowym czasie, skorzystamy z szybkiego algorytmu [[Sortowanie leksykograficzne | sortowania leksykograficznego]].

Zaczniemy więc tak samo jak w sortowaniu leksykograficznym - od końca. Czyli od największej głębokości, do najmniejszej.

Na każdej głębokości drzewa porównamy ilość liści na danym poziomie i jeśli jest różna, to oznacza, że nie są izomorficzne.

Każdy liść, będzie mieć kod $0$.

Następnie posortujemy leksykogrficznie klucze wierzchołków, które nie są liścmi, tworząc ciąg $L_i$

Jeśli listy $L_i$ obu drzew są różne, to oznacza, że nie są izomorficzne.

Następnie ustawimy wszystkim wierzchołkom, które nie są liśćmi odpowiedni kod, na podstaie klucza.

Ponieważ mamy w tym miejscu posortowane wszystkie wierzchołki z tego poziomu, to jesteśmy w liniowym czasie, stworzyć klucze rodziców, poziom wyżej.

Powtarzamy tą procedurę, aż do korzenia.

## Złożoność

Złożoność tego algorytmu jest liniowa, gdyż, najbardziej czasochłonne, jest sortowanie leksykograficzne wierzchołków na danej wysokości. Zajmuje to sumarycznie $O(n+k)$, gdzie $k$ jest długością słownika. Jednakże, długość słownika $k \le n$. Także złożoność będzie wynosić $O(n)$

## Drzewa nieukorzenione

Drzewa nieukorzenione, należ po prostu ukorzenić, wybierając centroid, czyli wierzchołek najdalej położony od liści, gdzie każda krawędź ma wagę $1$.