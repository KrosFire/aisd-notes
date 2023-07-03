Porządek leksykograficzny, to porządek napisów. Czyli porównujemy po prefixie, do momentu poróżnienia $k$-tego znaku i sprawdzamy porządek tego znaku.

## Radix sort

Jest to algorytm, który sortuje leksykograficznie ciągi o tej samej długości.

Na wejściu mamy $n$ ciągów, o długości $d$, na alfabecie $\Sigma$, o wielkości $k$.

Zaczniemy od ostatniego elementu w tych ciągach i będziemy sortować je aż do pierwszego znaku. Dzięki temu będziemy sortować od najmniej znaczących znaków i z każdą iteracją, będziemy poprawiać nasze sortowanie, dzięki braniu pod uwagę coraz to ważniejszych elementów.

Jako metodę sortującą w każdej iteracji wybierzemy jakiś szybki algorytm sortujący stabilnie. Idealnie nada się counting sort, ponieważ wiemy, że znaki należą do $k$ elementowego zbioru.

Ostateczna złożoność będzie wynosić: $O((n+k)d)$, ponieważ counting sort ma złożoność $O(n+k)$ i wykonujemy go $d$ razy.

Gdy $k = O(n)$, to koszt będzie liniowy.

## Niejednakowa długość

Gdy ciągi nie są jednakowej długości, sprawa się trochę komplikuje, jeśli chcemy zachować dobrą złożoność względem całkowitej długości wszystkich ciągów.

### Faza 1

Na początku stwórzmy sobie $l_{max}$ kubełków, w których będziemy przechowywać posortowane znaki, na $l$-tej pozycji. Nazwijmy te kubełki: $np$.

Możemy je utworzyć poprzez iterację się po wszystkich ciągach, i stworzenie nowych ciągów dwuelementowych, w których pierwszym elementem będzie pozycja znaku, a drugim sam znak.

Następnie posortujemy nowo utworzone ciągi `radix-sort`, dzięki czemu zajmie nam to: $O((k+l_{total})2)=O(k+l_{total})$

Następnie przechodząc od lewej do prawej, powstawiamy elementy w odpowiednie kubełki.

### Faza 2

W tej fazie stworzymy listę: `ciągi`, taką że na $i$-tej jej pozycji będą znajdować się ciągi o długości $i$.

Zajmie nam to $l_{total}$

### Faza 3 - Sortowanie

Mamy już wszystko czego potrzebujemy. Wiemy jakie znaki na jakiej pozycji wygrywają, dzięki pierwszej fazie. Wiemy również które ciągi, w danej iteracji należy sprawdzić.

Pomysł jest ten sam co w `radix-sort`, czyli idziemy od końca.

Iterujemy się po $l = l_{max} \to 1$

Weźmiemy więc na początku wszystkie ciągi o największej długości - $l_{max}$.

Zapiszemy je **na początek** listy ciągów do tej pory przeanalizowanych: $kol\_slow$. Będzie ona na początku pusta. Zapiszemy je na początku, aby zapewnić stabilność sortowania

Będziemy się iterować po każdym ciągu w $kol\_slow$.

Następnie weźmiemy $l$-ty znak danego ciągu i w kubełku $q$ o kluczu tego $l$-tego znaku, zapiszemy cały ten ciąg.

Będziemy robić tak, póki nie przypiszemy każdego ciągu do kubełka z kluczem interesującego nas obecnie znaku.

Skoro mamy każdy ciąg, przystosowany do znaku rozpatrywanego w danej iteracji oraz znamy kolejność znaków na danej pozycji, dzięki fazie pierwszej, to jesteśmy w stanie łatwo wszystko posortować.

Będziemy się mianowicie iterować po wszystkich znakach, w kubełku $np[l]$. Następnie do listy przeanalizowanych ciągów $kol\_slow$, będziemy zapisywać kolejne ciągi znajdujące się w kubełkach $q[np[l]]$

Złożoność tej fazy będzie zależna od pętli wewnętrznych.

Pierwsza pętla, która przypisuje wszystkie ciągi o długości co najmniej $l$ do odpowiednich kubełków, będzie się wykonywać sumarycznie $O(l_{total})$ razy, ponieważ przejdziemy się po wszystkich znakach we wszystkich ciągach.

Druga pętla, wyjmująca ciągi w odpowiedniej kolejności, wykona się również sumarycznie $O(l_{total})$ razy, ponieważ będziemy przechodzić przez każdy element w kubełkach $np$, czyli po wszystkich elementach ciągów.

Ostatecznie więc, złożoność tego algorytmu wynosi: $O(l_{total}+k)$ - przez pierwszą fazę.