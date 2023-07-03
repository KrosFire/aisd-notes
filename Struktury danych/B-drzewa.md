Gdy chcemy stworzyć duże słowniki, na tyle duże nie mieszczą się one w pamięci operacyjnej komputera, idealną strukturą danych będzie zbalansowane B-drzewo, które są zoptymalizowane do wyszukiwania danych znajdujących się na pamięci dyskowej.

## Cechy

1. Wszystkie liście znajdują się na tej samej głębokości
2. Każdy węzeł, zawiera kilka uporządkowanych elementów zbioru
3. Nowe elementy zapisywane są w liściach
4. Drzewo rośnie od liści do korzenia. Gdy dany węzeł zostanie zapełniony, to dzieli się on na dwa węzły po połowie danych. Środkowy element jest zaś przydzielany do rodzica (Jeśli go nie ma jest on tworzony. Rodzic może mieć wiele dzieci, gdyż **nie jest to drzewo binarne**). Środkowy element jest jednocześnie wskaźnikiem na dwójkę liści. Jeśli rodzic zostanie przepełniony, następuje taka sama sytuacja podziału.

## Formalny opis

Cechy wierzchołka $v$ można oznaczyć jako

* $n(v)$ - liczba kluczy obecnie pamiętanych w $v$
* $2t-1$ - liczba pól na klucze - maximum capacity.
* $leaf(v)$ - wartość boolowska czy $v$ jest liściem

Jeśli $v$ jest rodzicem, to posiada również $2t$ pól $c_i(v)$ na wskaźniki na dzieci 

$t \ge 2$ jest ustaloną liczbą całkowitą określającą dolną i górną granicę na liczbę kluczy pamiętanych w węzłach:

Musi mieć $t-1 \le k \le 2t-1$ kluczy. Lub też $t \le c \le 2t$ wskaźników na dzieci.

## Find

Find jest taki sam jak w BST, z tym że mamy wiele dzieci. więc po kolei porównujemy wartość poszukiwaną z obecnymi kluczami w wierzchołku. Jeśli zachodzi równość, to zwracamy indeks klucza, oraz wierzchołek. Jeśli nie udało nam się znaleźć, klucza to jeśli nie jesteśmy w liściu to wykonujemy $disc\_read(c_i(v))$ - odczytujemy dane z pamięci dyskowej i wykonujemy się rekurencyjnie na poddrzewie $c_i(v)$. Gdy jesteśmy jednak w liściu, zwracamy $NULL$

## Split

Gdy chcemy rozdzielić zbyt duży wierzchołek $y$ o rodzicy $x$ na dwa, musimy wykonać następujące działania:

1. Stworzyć nowy wierzchołek $z$ z odpowiednimi parametrami (liść, $t-1$ elem.)
2. Przekazać $z$ $t-1$ kluczy z $y$ oraz $t$ wskaźników
3. Usunąć z wierzchołka $y$ przekazane wierzchołki i wskaźniki
4. Przekazać rodzicowi $x$ środkowy klucz spośród całkowitych $2t$ kluczy oraz wskaźniki.
5. Zapisać wszystkie wierzchołki na dysku

## Koszt operacji
![[Screenshot 2023-05-01 at 11.30.56.png]]
![[Screenshot 2023-05-01 at 11.30.46.png]]

## Ilość wierzchołków przy wysokości h i stopniu t

Jeśli mamy wysokość $h$ - liczba krawędzi w pionie, to ile maksymalnie i minimalnie możemy mieć wierzchołków przy danym stopniu $t$?

### Maksimum

Zacznijmy od korzenia. W tym przypadku będzie on mieć $2t$ dzieci. Każde z tych dzieci również będzie mieć $2t$ dzieci. Otrzymamy więc taką sumę ciągu geometrycznego:

$$
1+2t+(2t)^2+(2t)^3+...+(2t)^h=\frac{1-(2t)^{h+1}}{1-2t}
$$

Jest $1$ korzeń $2t$ dzieci korzenia, itd.

### Minimum

Ponownie zaczniemy od korzenia. Tym razem będzie on mieć jak najmniejszą liczbę wskaźników, czyli dwa. Dzieci, na które wskazuje ten korzeń muszą mieć jednak co najmniej $t-1$ kluczy, czyli $t$ dzieci. Jest tak ponieważ mają rodzica, który powstał z przepełnienia ich limitu, w wyniku czego podzielili się po połowie kluczami. Każde kolejne dziecko, będzie musiało mieć minimum $t$ dzieci.

Czyli mamy taką sumę:

$$
1+2+2\cdot t+2\cdot t^2+...+2\cdot t^{h-1}=1+2\frac{1-t^h}{1-t}
$$

Jest to suma ciągu geometrycznego, ponieważ drugi wyraz spełnia równanie: $2=2\cdot t^0$

## B-drzewo po wypełnieniu

![[IMG_0048.png]]