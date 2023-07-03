Drzewo AVL, jest zbilansowanym drzewem BST. Dzięki czemu jesteśmy w stanie wykonywać operacje typu $find$ czy $delete$ w czasie $O(\log n)$.

Niestety będzie to kosztem $insert$'a, który będzie wykonywany w czasie większym niż $O(1)$, mianowicie $O(\log n)$.

Wysokość drzewa AVL jest mniejsza niż: $1.4405\log (n+2)$ - golden ratio.

## Implementacja

![[Pasted image 20230417160419.png]]

Wartość balansu, to liczba, która jest różnicą wysokości lewego i prawego poddrzewa tj:

$$
b=h_r-h_l
$$

Jest ona użyteczna przy balansowaniu drzewa poprzez rotacje i jest na przedziale $[-2,2]$

## Rotacja

Dla drzewa, o korzeniu $v$, wierzchołku prawym $v_r$ i wierzchołku lewym $v_l$, będziemy przeprowadzać rotacje na wierzchołku $v$.

Istnieją 4 możliwe sytuacje zaburzonego balansu, które musimy zaadresować:

1. $balance(v)=2 \land balance(v_r)=1$
   Czyli prawe poddrzewo jest wyższe od lewego o dwa stopnie i jednocześnie, prawe poddrzewo prawego wierzchołka, jest wyższe o $1$, od lewego poddrzewa prawego wierzchołka.
   To oznacza, że rotacja w lewo załatwia nam sprawę.
   ![[Pasted image 20230417161730.png]]
2.  $balance(v)=-2 \land balance(v_l)=-1$
   Mamy tutaj symetryczną sytuację do pierwszej. Czyli jak się domyślamy, rotacja w prawo zbalansuje nam drzewo.
   ![[Pasted image 20230417162352.png]]
3. $balance(v)=2 \land balance(v_r)=-1$
   Wracamy do pierwszej sytuacje, lecz teraz to lewo poddrzewo prawego wierzchołka jest wyższe. Możemy sobie z tym poradzić w banalny sposób, mianowicie zmienić tą sytuację na taką, z którą wiemy jak sobie poradzić - pierwszą. Czyli na prawym poddrzewie, którego korzeniem jest $v_r$, wykonujemy rotację w prawo, dzięki czemu balans, zmienia się $(-1 \to 1)$. A teraz wykonujemy rotację w lewo, względem głównego korzenia $v$.
   ![[Screenshot 2023-04-17 at 16.32.37.png]]![[Screenshot 2023-04-17 at 16.32.51.png]]![[Screenshot 2023-04-17 at 16.33.04.png]]
4.  $balance(v)=2 \land balance(v_l)=1$
   Lustrzana sytuacja jak w trzecim punkcje. Wykonujemy rotację w lewo na lewym poddrzewie, a następnie w prawo, na głównym drzewie.

## Insert

Chcemy dodać wartość $k$ do drzewa $T$. Przechodzimy od korzenia do liści ($\log n$) i porównujemy wartość $k$ z obecnym korzeniem. Jeśli $k < v$, przechodzimy do lewego poddrzewa, a w p. p. do prawego.

Dodajemy $k$, zamiast pustego pointera na dole drzewa.

Następnie idziemy do góry, aż nie napotkamy na swej drodze korzenia poddrzewa, którego balans został zachwiany. Po naprawieniu balansu tego poddrzewa, nie musimy iść wyżej, ponieważ rotacjami spłaszczyliśmy to drzewo, a zatem naprawiliśmy balans również na wyższych szczeblach.

Ostatecznie insert zajmuje nam pesymistycznie $O(2\log n) = O(\log n)$ czasu.

## Delete

Chcemy usunąć wartość $k$ z drzewa $T$. Najpierw musimy go więc znaleźć, funkcją $find$, która wykona się maksymalnie $\log n$.

Gdy już znaleźliśmy ten element w wierzchołku powiedzmy $v$, musimy go usunąć. Jeśli $v$ jest liściem, to nie ma problemu. Jeśli zaś $v$ posiada dzieci, to zastępujemy go albo skrajnie prawym wierzchołkiem w lewym poddrzewie, albo symetrycznie, skrajnie lewym wierzchołkiem w prawym poddrzewie. Nazwijmy taki wierzchołek $v'$ i zauważmy, że wybór takiego wierzchołka, sprawia że nie niszczymy relacji BST, ponieważ wybieramy największy z najmniejszych, bądź największy z najmniejszych elementów.

Wykonujemy ten krok podmiany rekurencyjnie na $v'$, aż nie natrafimy na liść, który następnie usuwamy.

Zauważmy że nie wykonamy tej rekursji więcej niż $2$ razy, ponieważ drzewo jest zbalansowane.

Na sam koniec, musimy się upewnić że nie zniszczyliśmy balansu, więc idziemy od usuniętego liścia, aż do korzenia, balansując rotacjami drzewo.

Zauważmy że pierwszy i drugi krok - find i delete, sumarycznie schodzą na sam dół drzewa, czyli wykonują $\log n$ operacji. Trzeci krok - balance, ponownie wykonuje $\log n$ operacji, wracając się na górę, z pewną małą stałą - optymistycznie równą $1$.

Czyli czas wykonania wynosi: $O(2\log n) = O(\log n)$

Maksymalna ilość rotacji jest równa wysokości drzewa, czyli: $1.4405\log n$

## Minimalne drzewo AVL

### Standardowy przypadek

Gdy chcemy oszacować wysokość drzewa AVL musimy wziąć pod uwagę minimalne drzewo AVL, czyli  takie o największej wysokości przy użyciu najmniejszej ilości wierzchołków. Czyli będzie to drzewo skrajnie niezbalansowane w ramach zasad balansu (różnica wysokości wynosi 1).

Aby oszacować wysokość takiego drzewa wykorzystamy fakt że ilość pustych wskaźników jest o $1$ większa od ilości wierzchołków.

Niech $p(h)$ będzie liczbą pustych wskaźników w minimalnym drzewie AVL o wysokości $h$.

$$
p(1)=2
$$
$$
p(2)=3
$$
$$
p(h\ge3)=p(h-1)+p(h-2)
$$

Równanie rekurencyjne wynika z tego, że korzeń posiada $0$ pustych wskaźników, więc sumujemy puste wskaźniki z minimalnych AVL, które różnią się wysokością o $1$.

Jak widzimy jest to ciąg Fibonacciego z offsetem równym $2$

$$
p(h)=F_{h+2}
$$

$$
n+1>F_{h+2}
$$
$$
h \le 1,5\log{n}
$$

### Przypadek niezbalansowania równego 2

W tym przypadku równanie rekurencyjne wygląda następująco:

$$
p(1)=2
$$
$$
p(2)=3
$$
$$
p(3)=4
$$
$$
p(h\ge4)=p(h-1)+p(h-3)
$$

Jak możemy zauważyć jest to znowu podobne do Fibonacciego i możemy to oszacować jako:

$$
F_{h+2}\ge p(h) \ge F_{h+1}
$$

Czyli jak wiemy z poprzedniego przypadku, wysokość będzie wynosić $\Theta(\log{n})$

## Pesymistyczne usuwanie wierzchołka

Najbardziej pesymistycznym usunięciem wierzchołka jest takie, gdy zepsujemy balans drzewa aż do korzenia. Jest to możliwe tylko wtedy, gdy posiadamy minimalne drzewo AVL i usuniemy liść z najmniejszego poddrzewa. Gdybyśmy usunęli wierzchołek z jakiegoś większego poddrzewa, to balans zepsułby się wyłącznie w pod przypadkach, gdzie usunięty wierzchołek znajdował się w mniejszym poddrzewie.

Skoro więc usuwamy liść z najmniejszego poddrzewa, to znajdował się on na wysokości ok. $1,5\log(n)-1$. $-1$ ponieważ był w mniejszym poddrzewie. Czyli po jego usunięciu, wykonym mniej niż $1,5\log(n)-2$ operacji rotacji, aby naprawić drzewo AVL.

### 3 rotacje po usunięciu
![[IMG_0047 1.png]]