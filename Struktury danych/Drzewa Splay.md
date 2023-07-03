Jest to drzewo samoorganizujące - czyli naprawia swoją strukturę za pomocą prostych heurystyk, która nie potrzebuje zapisywać dodatkowych informacji w wierzchołkach.

## Operacja $Splay$

Celem tej operacji, jest przesunięcie za pomocą rotacji, wierzchołek $x$ do korzenia tegoż drzewa. Jeśli zaś $x$ nie istnieje w tym drzewie, to ostatni wierzchołek który odwiedziliśmy, szukając $x$-a (liść).

Aby zapewnić sobie niski nakład pracy przy częstym szukaniu elementów danym drzewie, chcielbyśmy aby drzewo się w miarę spłaszczało. Aby to osiągnąć musimy brać pod uwagę 3 przypadki:

1. $x$ ma ojca, ale nie ma dziadka. Prosty przypadek, wykonujemy odpowiednią rotację w lewo/prawo
2. $x$ ma ojca $p(x)$ i dziadka. $x$ oraz $p(x)$ są obaj lewymi/prawymi dziećmi. W takim razie podwójna rotacja z góry na dół załatwi sprawę
3. Jeśli zaś $x$ jest lewym dzieckiem $p(x)$, które jest prawym dzieckiem (i na odwrót), to robimy to samo co w [[Drzewa AVL]]. Czyli sprowadzamy do formy 2.

## Analiza złożoności

Ponownie przeprowadzimy analizę kosztu za pomocą kredytów

Wpierw definicje:

$S(x)$ - drzewo, którego korzeniem jest $x$
$|S|$ - liczba wierzchołków drzewa $S$
$\mu(S) = \lfloor \log|S| \rfloor$
$\mu(x) = \mu(S(x))$

Niezmiennikiem dla każdego wierzchołka $x$ będzie to, że posiada co najmniej $\mu(x)$ kredytów. Czyli conajmniej logarytm swojego rozmiaru.

$insert$ daje wierzchołkowi $1$ kredyt.

$Splay(x)$ wymaga $\le 3(\mu(S)-\mu(x))+1$ do wykonania się oraz zachowania niezmiennika.

Dowód:

Musimy rozpatrzeć trzy wcześniej wspomniane przypadki podczas promocji $x$-a do korzenia.

$x$ - opracowywany wierzchołek
$y$ - jego rodzic
$z$ - jego dziadek

### Zwykła rotacja

$\mu$ - wartość kredytów przed wykonaniem operacji
$\mu'$ - wartość kredytów po wykonaniu operacji

Robiąc jedną rotację w lewo/prawo, jedynie drzewa $S(x)$ i $S(y)$ zmieniają swoją wielkość.

A zatem koszt jaki musimy ponieść to:

$$
\mu'(x)+\mu'(y)-\mu(x)-\mu(y)
$$

Ponieważ $\mu'(x)$ to wartość jaką musi mieć $x$, a $\mu(x)$ to wartość jaką obecnie ma.

Zauważmy, że przed rotacją, pod $y$-kiem były wszystkie wierzchołki, a po rotacji wszystkie wierzchołki są pod $x$-em. Czyli $\mu'(x)=\mu(y)$.

A zatem prawdziwe są też te nierówności: $\mu'(x) \ge \mu(x)$ i $\mu'(y)\le\mu'(x)$.

Teraz możemy ładnie wszystko skrócić i poprzekształcać:
$$
\mu'(x)+\mu'(y)-\mu(x)-\mu(y)=
\mu(y)+\mu'(y)-\mu(x)-\mu(y)=
\mu'(y)-\mu(x)\le
\mu'(x)-\mu(x)\le
3(\mu'(x)-\mu(x)) + 1
$$

Czyli wszystko się zgadza 😎

### Podwójna rotacja z góry na dół

Ponownie mamy taki koszt operacji:

$$
\mu'(x)+\mu'(y)+\mu'(z)-\mu(x)-\mu(y)-\mu(z)
$$

Ponownie widzimy, że $x$ jest korzeniem poddrzewa o takim samym rozmiarze, jakiego korzeniem było $z$. Zatem $\mu'(x)=\mu(z)$

Następujące nierówności również z tego wynikają:
$$
\mu(x)\le\mu'(x)
$$
$$
\mu'(z)\le\mu'(x)
$$
$$
\mu'(y)\le\mu'(x)
$$
$$
\mu(y)\le\mu'(x)
$$

Teraz przekształcamy:
$$
\mu'(x)+\mu'(y)+\mu'(z)-\mu(x)-\mu(y)-\mu(z)=
\mu(z)+\mu'(y)+\mu'(z)-\mu(x)-\mu(y)-\mu(z)=
\mu'(y)+\mu'(z)-\mu(x)-\mu(y)=
[\mu'(y)-\mu(x)]+[\mu'(z)-\mu(y)]\le
[\mu'(x)-\mu(x)]+[\mu'(x)-\mu(y)]
$$

Tutaj również ważna obserwacja, że ponieważ $y$ jest rodzicem $x$-a, to $\mu(x)\le\mu(y)$

$$
[\mu'(x)-\mu(x)]+[\mu'(x)-\mu(y)]\le
2[\mu'(x)-\mu(x)]\le
3(\mu'(x)-\mu(x))+1
$$

### Zyg zag

Tak samo jak w drugim przypadku.

Dodatkowa analiza znajduje się w tutaj:
![[Notatka 17 Drzewa Splay.pdf]]

### Podsumowanie

Koszt operacji $Splay(x)$ (zamortyzowany) wynosi $O(\log n)$