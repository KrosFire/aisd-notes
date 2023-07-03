Na wejściu, dostajemy ciąg instrukcji $UNION(A,B,C)$ i $FIND(i)$ - $\sigma$.

$UNION(A,B,C)$ konstruuje zbiór $C = A \cup B$ i usuwa zbiory $A$ i $B$.
$FIND(i)$ zwraca podzbiór, do którego należy $i$.

Wszystkie te zbiory należą do jednego wielkiego zbioru $U$. Na początku każdy element w $U$ należy do podzbioru, który jest singletonem.

Naszym zadaniem jest stworzenie takiej struktury danych, dzięki której będziemy w stanie wykonać te operacje w bardzo szybki sposób.

## Zastosowania

Struktura danych, która jest w stanie wykonać takie instrukcje w szybki sposób jest bardzo użyteczna np. przy [[Algorytm Kruskala]], czy też [[Algorytm Boruvki]], które operują na zbiorach.

## Pierwsza próba rozwiązania

Stwórzmy po prostu tablicę $R$, o rozmiarze takim samym co zbiór $U$. Wartościami w tej tablicy będzie nazwa zbioru, do którego przynależy $i$-ty wierzchołek.

Dzięki temu $FIND(i)$ będzie się wykonywać w $O(1)$, ponieważ wystarczy zwrócić $R[i]$

Zaś $UNION(A,B,C)$ będzie w czasie liniowym $O(n)$, ponieważ będziemy musieli się przejść po całej liście $R$ i zamienić wszystkie nazwy $A$ i $B$, na $C$.

## Ulepszenie

Niestety liniowość dla $UNION$ jest dosyć problematyczna, spróbujmy coś z tym zrobić.

Problematycznym obecnie w operacji $UNION$ jest to, że nie wiemy gdzie znajdują się w $R$ elementy danego zbioru. Spróbujmy więc temu zaradzić tworząc następujące listy:

$List[j]$ - wskaźnik na pierwszy element w zbiorze o nazwie $j$.
$Next[i]$ - następny po $i$ element w tym samym zbiorze.
$Size[j]$ - rozmiar zbioru o nazwie $j$.

Dzięki takiemu rozwiązaniu, jesteśmy w stanie od razu przejść się po zbiorze $A$ i $B$ i stworzyć zbiór $C$, za pomocą kilku operacji:

$Size[C] = Size[A] + Size[B]$
$List[C] = List[A]$
$Next[last(A)] = List[B]$

Zauważmy jednak że wcale nie musimy przechodzić przez cały zbiór $B$. Przy założeniu że $|A| \le |B|$, możemy wszystkie wierzchołki w $A$ przypisać do $B$. Dzięki temu zaoszczędzimy potencjalnie mnóstwo czasu jeśli $B$ jest bardzo duże.

Problemem jest oczywiście to, że my nie chcemy przypisać $B$ elementów z $A$, tylko stworzyć kompletnie nowy zbiór. Odpowiedź to: Ale czy ktokolwiek musi o tym wiedzieć?

Możemy stworzyć dwie dodatkowe tablice:

$ExtName[j]$ - nazwa zewnętrzna zbioru, o nazwie wewnętrznej $j$
$IntName[j]$ - nazwa wewnętrzna zbioru, o nazwie zewnętrznej $j$.

Czyli teraz, wystarczy że na początku i na końcu $UNION$ przetłumaczymy sobie adresy i zapiszemy, że nasze wewnętrzne $B$ jest dla świata zewnętrznego zbiorem $C$.

Dzięki takiej strukturze jesteśmy w stanie wykonać dowolny ciąg instrukcji $\sigma$ w czasie $O(n\log n)$

## Struktura drzewiasta

Do rozwiązania tego problemu, możemy również stworzyć nową strukturę drzewiastą. Będziemy posiadali las drzew, w którym każdy wierzchołek ma wskaźnik **wyłącznie** na swego ojca. Zapamiętywać będziemy również listę wskaźników na $i$-ty wierzchołek ($Element[i]$) oraz tablicę wskaźników na **korzeń** drzewa, danego zbioru $Root[j]$.

Tylko w korzeniu drzewa, będziemy przechowywać informację na temat przynależności do zbioru. Zatem początkowa struktura, to będzie las jednoelementowych drzew.

Jak w takiej sytuacji będą wyglądać operacje?

Operacja $UNION(A,B,C)$ będzie polegać na podejrzeniu korzeni zbiorów $A$ i $B$ z tablicy $Root$, a następnie podwieszenie mniejszego (pod względem ilości wierzchołków) drzewa, do drzewa większego. Na koniec oczywiście aktualizujemy nazwy zborów w tablicy $Root$ oraz w korzeniu większego drzewa.

Operacja $Find(i)$ będzie polegać na podejrzeniu wierzchołka $i$ z tablicy $Element$ oraz przejście na samą górę drzewa, do którego należy i zwróceniu nazwy zbioru tegoż korzenia. Na sam koniec, podwiesimy każdy wierzchołek na drodze której przeszliśmy pod sam korzeń, aby przyszłe poszukiwania były szybsze.

## Definicje

1. Niech $\bar{\sigma}$ będzie ciągiem instrukcji $UNION$ po usunięciu z $\sigma$ instrukcji $FIND$. **Rząd** wierzchołka $v$ względem $\sigma$ to jego wysokość w lesie, po wykonaniu $\bar{\sigma}$ ^06bae8
2. $\log^*(n)=\min\{k |F(k) \ge n\}$ gdzie $F(0)=1$ $F(k)=2^{F(k-1)}$
3. Grupa rzędu $r$ - $\log^*(r)$

### Analiza

Możemy zauważyć, że wykonując instrukcję $UNION$, to każde drzewo o wysokości $h$, będzie mieć co najmniej $2^h$ elementów.

## Przypadki

Gdy wszystkie operacje $UNION$ poprzedzają operację $FIND$, koszt działania algorytmu względem $n$ instrukcji w $\sigma$ to: $O(n)$. Przykład to ilustrujący:

![[IMG_0053 1.png]]

Jeśli $UNION$ nie byłoby robione w zbalansowany sposób, istniałaby sytuacja prostej ścieżki, co sprawiałoby, że złożoność czasowa wzrosła by do kwadratowej. Przykład to ilustrujący:

![[IMG_0054.png]]

Jeśli chcemy zbudwować najwyższe drzewo, należy się przyjżeć jak jest ono budowane - czyli jak działa operacja $UNION$.

Operacja $UNION$ podpina pod drzewo większe, drzewo mniejsze. A zatem wysokość drzewa końcowego będzie wynosić wysokości drzewa mniejszego (dokładnie niewiększego) plus $1$.

Będziemy więc chcieli łączyć ze sobą drzewa o tej samej wysokości, które zostały stworzone z minimalną ilością wierzchołków. W ten sposób powstanie drzewo o wysokości o $1$ większej przy użyciu minimalnej ilości wierzchołków. Zatem jest to prosta relacja rekurencyjna.
$T(h)$ - minimalne drzewo o wysokości $h$

$$
T(0) = \{v | v \in C\}
$$
$$
T(h) = UNION(T(h-1), T(h-1))
$$

Inaczej $H(n)$ - maksymalna wysokość drzewa o $n$ wierzchołkach

$$
H(1) = 1
$$
$$
H(n) = H(\frac{n}{2})+1
$$

Czyli $max(h) = \log_2n$

Wiemy więc, że jeśli drzewo ma wysokość $k$, to musi posiadać **co najmniej** $2^k$ wierzchołków. Jest to łatwiejsze do sprawdzania podczas łączenia drzew.

## Koszt zamortyzowany

Wierzchołków o [[#^06bae8 | rzędzie]] $r$, może być co najwyżej $\frac{n}{2^r}$. Wynika to prosto z operacji $UNION$. Na początku gdy mamy las niepołączonych $n$ wierzchołków, to wysokość każdego jest równa $0$.  Czyli jest co najwyżej $\frac{n}{2^0}=\frac{n}{1}=n$ wierzchołków o takim rzędzie. A na koniec, gdy wszystkie połączymy w jedno drzewo, to mamy maksymalnie   $\frac{n}{2^{\log n}}=1$  wierzchołek - korzeń o wysokości $\log n$.

Wiemy, że istnieje $\log^*n$ grup rzędów. Obciążać będziemy funkcję $Find(v)$ w 3 przypadkach:

1. Gdy $w$ jest korzeniem
2. Gdy ojcem $w$ jest korzeń
3. Gdy $w$ i jego ojciec są w różnych grupach

Dwa pierwsze przypadki wydarzą tylko raz. Ostatni, wydarzy się tyle razy ile jest grup, czyli $O(\log^*n)$.

W p.p. obciążymy wierzchołek $w$. Ostateczny koszt $Find$ wynosi:

$$
\# \text{obciążenia Find}+\#\text{obciążenia }w
$$

Jest $m$ operacji $Find$ i maksymalnie będzie obciążona $O(\log^*n)$. Czyli $\# \text{obciążenia Find} = O(m\log^*n)$

Teraz ile wyniesie obciążenie wierzchołków? Jest $\log^*n$ grup rzędów. Tak one wyglądają:

$\log^*0 = 0; F(0)=1$
$\log^*1 = 0; F(0)=1$
$\log^*2 = 1; F(1)=2^1=2$
$\log^*3 = 2; F(2)=2^2=4$
$\log^*4 = 2; F(2)=2^2=4$
$\log^*5 = 3; F(3)=2^4=16$

Czyli rzędów w grupie $g$ jest: 

$$
F(g-1)+1,...,F(g)
$$

A w każdym rzędzie jest $\frac{n}{2^r}$ wierzchołków. Sumarycznie wyjdzie ich:
$$
\sum_{r=F(g-1)+1}^{F(g)}\frac{n}{2^r}=\frac{n}{2^{F(g-1)+1}}(1+\frac{1}{2}+\frac{1}{4}+...)\le 2\frac{n}{2^{F(g-1)+1}} = \frac{n}{2^{F(g-1)}}= \frac{n}{F(g)}
$$

Grupa $g$ posiada $F(g)-F(g-1)$ rzędów. Obarczamy wierzchołki kosztami, gdy idziemy w górę drzewa i zmieniają się jedynie rzędy, a nie grupy. Robimy to tylko raz, ponieważ po tej operacji, będą one pod korzeniem. Czyli $\frac{n}{F(g)}$ wierzchołków w grupie $g$, obarczymy nie więcej niż  $F(g)-F(g-1)$ razy. Czyli sumarycznie:

$$
\sum_{g=0}^{\log^*n}\frac{n}{F(g)}(F(g)-F(g-1))\le\sum_{g=0}^{\log^*n}n\le n\log^*n
$$