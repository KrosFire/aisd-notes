![[Screenshot 2023-06-20 at 16.45.10.png]]

Pierwsza rzecz - ukorzenienie. Czyli znajdujemy centroid/y i ustalamy je, jako korzenie.

Aby je znaleźć wystarczy iść od liści do środka drzewa, dopóki nie ostanie się mniej niż $2$ wierzchołki - centroidy.

Jeśli ilość centroidów w drzewach się różni, to od razu możemy uznać je za nieizomorficzne.

W p. p. dla wszystkich centroidów:

ukorzeniamy drzewa w danym centroidzie.

Idziemy od liści w górę.

Dla wierzchołka na danej wysokości, sprawdzamy klucze jego dzieci (liczby) i tworzymy posortowany wektor. Jeśli wierzchołek nie ma dzieci, posiadać będzie wektor: $[0]$

Następnie dla danej wysokości, sortujemy leksykograficznie wszystkie wektory i przypisujemy im klucz, zgodny z ich pozycją.

Jeżeli uporządkowany ciąg wektorów dwóch drzew, nie zgadza się na danej wysokości, to oznacza, że drzewa nie są izomorficzne.

Złożoność obliczeniowa to $O(|V|+|E|)$

Dlaczego?

Znalezienie centroidów zajmuje nam $O(|V|+|E|)$ - dfs/bfs znajdziemy liście, a potem będziemy wstawiać iteracyjnie na koniec tablicy następne wierzchołki do sprawdzenia.

Ukorzenienie również zajmie nam $O(|V|+|E|)$, ponieważ jest to zwykłe ukierunkowanie krawędzi, też można zrobić dfs'em.

Sprawdzanie samego izomorfizmu będzie wykonywane w czasie liniowym, ponieważ sortowanie leksykograficzne, sumarycznie zajmie $O(n)$ razy, tak samo jak przejście po wszystkich wierzchołkach, warstwa po warstwie.