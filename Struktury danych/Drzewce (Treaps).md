
Struktura ta, jest ciekawą hybrydą drzewa BST oraz Kopca. Mianowicie każdy wierzchołek w tym drzewie, posiada dwie wartości $(key, priority) - (k,p)$. Jest on zbudowany w taki sposób, że przestrzega zasad BST i Kopca. Czyli:

1. Lewe poddrzewo posiada klucze mniejsze od korzenia, a prawe poddrzewo klucze większe.
2. Priorytet korzenia, jest większy od priorytetu wszystkich wierzchołków poniżej.

## Tworzenie

Drzewce zawsze można stworzyć i to w banalny sposób. Musimy mianowicie znaleźć wierzchołek, który obecnie ma największy priorytet i ustawić go jako korzeń. Następnie wywołamy się rekurencyjnie na zbiorze wierzchołków, których klucze są mniejsze od tegoż korzenia i wynikowy drzewiec ustawimy jako lewe poddrzewo. Analogicznie dla zbioru wierzchołków, których klucze są większe od korzenia.

Zauważmy, że taki drzewiec nie musi być wcale zbalansowany. W krytycznym przypadku, gdy kolejno największe priorytety posiadają wierzchołki z najmniejszym/największym kluczem, otrzymamy drzewo o wysokości $n$.

## Operacje

### Insert

Gdy chcemy wstawić element do drzewca, zrobimy to na początku tak samo jak w drzewie BST. Czyli przejdziemy od korzenia i wstawimy nowy wierzchołek jako liść.

Następnie musimy wziąć poprawkę na to, że priorytet nowego wierzchołka, może być bardzo wysoki. Wykonamy więc serię rotacji, które będą wynosić ten wierzchołek do góry, jednocześnie nie psując panującego już porządku.

### Delete

Gdy chcemy usunąć pewien wierzchołek, musimy go wpierw znaleźć. Po tym jak nam się to udało, musimy go sprowadzić do parteru. Jednak musimy to robić z uwagą, ponieważ nie dzieci mają różne priorytety. Załóżmy że $j$ i $k$ są odpowiednio lewym i prawym dzieckiem usuwanego wierzchołka. Jeśli $p(j) > p(k)$, musimy wykonać rotację w prawo. Wtedy wierzchołek $j$ o wyższym priorytecie trafi na górę, co nie zaburzy naszego porządku, a nasz usuwany element schodzi niżej.