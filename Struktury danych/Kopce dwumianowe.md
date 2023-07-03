Kopce dwumianowe, to drzewiasta struktura danych, wykorzystywana do tworzenia np. kolejek priorytetowych, tak samo jak [[Kopiec binarny]]. Jest on jednak zoptymalizowany, pod względem inserta

**Kopiec** dwumianowy, to zbiór stworzony z **drzew** dwumianowych.

## Drzewa dwumianowe

Drzewa dwumianowe, to drzewa o stopniu $k$, które posiadają następujące cechy:
1. $2^k$ wierzchołków 
2. posiadają $k$ dzieci, które są drzewami dwumianowymi  o stopniach kolejno: $k-1,k-2,...,0$
3. Są wysokości $k$ (ilość krawędzi)
4. Na $i$-tej wysokości istnieje ${k \choose i}$ wierzchołków

## Cechy kopca

Kopiec dwumianowy, to **zbiór** drzew dwumianowych. Każdy wierzchołek/węzeł w kopcu dwumianowym posiada pointer do:

1. Swojego lewego i prawego rodzeństwa
2. Swojego dziecka najbardziej po lewej

Posiada on dodatkowo informacje o wartości swego klucza, oraz o ilości dzieci, które posiada - czyli swoim stopniu.

**Kopiec może posiadać wyłącznie jedno drzewo dwumianowe danego stopnia**

Dzięki tym właściwościom, kopiec dwumianowy, posiada $\le \log_2n+1$ drzew dwumianowych i wysokość $\le \log_2n = k$

Jak możemy zauważyć kopiec dwumianowy, przez swoją zależność od potęgi $2$, ma dużo wspólnego z systemem binarnym. Dzięki temu jesteśmy w stanie łatwo stwierdzić jakiego typu drzewa dwumianowe posiada w swoim zbiorze na podstawie jego rozmiaru.

Np. jeśli kopiec dwumianowy posiada $63$ elementy, to musi się on składać z drzew o stopniu: $1,2,3,4,5$ i $6$. Ponieważ $63_{10}=111111_2$

## Przykład

![[Pasted image 20230501163411.png]]
![[Pasted image 20230501163416.png]]

## Funkcje

### Znalezienie minimum

Z każdym kopcem dwumianowym wiążemy wskaźnik MIN wskazujący na minimalny element. Operacja finddmin polega na odczytaniu tego elementu. Stąd jej koszt wynosi $O(1)$

### Łączenie dwóch drzew

Gdy wystąpi sytuacja niszcząca cechę kopca dwumianowego - wystąpięnie dwóch drzew o tym samym stopniu, musimy temu zaradzić, łącząc je w jedno drzewo, o jeden stopień większe tj.:

$$
2^0+2^0=2^1
$$
$$
2^1+2^1=2^2
$$
$$
2\cdot2^k=2^{k+1}
$$

![[Screenshot 2023-05-01 at 19.00.55.png]]

Jak widzimy operacja ta sprowadza się do przepięcia pointerów, jej złożoność to $O(1)$

### Meld - operacja łączenia dwóch kopców

### Opcja gorliwa

Możemy naprawiać kopiec po każdej operacji insert'a i delete'a.

Funkcja ta, przyjmuje dwa kopce i przechodzi po wszystkich drzewach w obu kopcach.
Jeśli natrafi na dwa drzewa tego samego stopnia, wykonuje ich połączenie, do drzewa stopnia o jeden większego. Czas działania tego algorytmu to $O(\log n)$ ponieważ tyle jest maksymalnie drzew w kopcach, a operacja $join$ jest wykonywane w czasie stałym.

#### Delete min

Używając opcji gorliwej, usuwanie najmniejszego elementu będzie wykonywane w czasie stałym $O(1)$. Schemat działania:

1. $B_i$ - drzewo zawierające najmniejszy element w naszym kopcu $h$
2. Usuwamy $B_i$ z $h$ i usuwamy jego korzeń - $min_{elem}$.
3. Dzieci $B_i = B_0,B_1,...,B_{i-1}$. Będą one tworzyć nowy kopiec dwumianowy $h'$
4. Zwracamy $min_{elem}$

W tym miejscu kończy się $delete_min$ a zaczyna się $meld(h,h')$

#### Insert

Insert sprowadzi się tutaj do stworzenia wierzchołka z wprowadzanym elementem, a następnie przeprowadzenie operacji $meld$. Z tego powodu, koszt działania tej operacji wyniesie nas $O(\log n)$

### Opcja lazy

To w tej opcji ta struktura nabiera dużego sensu. Dzięki niemu, wszelkie operacje poza $delete$ będą wykonywane w czasie stałym.

Funkcja $lazy\_meld(h,h')$ będzie więc polegać więc na wybraniu najmniejszego elementu z obu list i połącznie ich wskaźnikami. Zatem będzie się wykonywać w czasie $O(1)$.

Cała odpowiedzialność za poprawę struktury tegoż kopca spadnie na operację $delete\_min$. W bardzo pesymistycznym przypadku - gdy kopiec składa się wyłącznie z drzew pierwszego stopnia, musimy znaleźć nowe minimum spośród $O(n)$ wierzchołków.

Jednakże jesteśmy w stanie zamortyzować ten koszt do $O(\log n)$. Wszystko to za sprawą systemu kredytów.

Musimy zachować następujący niezmiennik:

"Każde drzewo w kopcu posiada $1$ kredyt"

Każda operacja będzie miała swój koszt.

$make\_heap - 2$
$insert - 2$
$meld - 1$
$find\_min - 1$
$delete\_min - 2 \log n$

Operacje $meld$ i $find\_min$ nie dodają/usuwają wierzchołków i są wykonywane w czasie stałym, więc ich koszt to $1$

$make\_heap$ i $insert$ są wykonywane w czasie stałym, lecz dodają drzewo. Jeden kredyt zostaje przydzielony dla nowego drzewa w kopcu, a jeden zużyty na wykonanie danej operacji.

$delete\_min$ jeśli usunie największe drzewo w kopcu, stworzy $\log n$ nowych drzew. Każdemu z nich zostanie przydzielony $1$ kredyt. Pochłonie więc to połowę budżetu tej operacji.

Następnie będziemy musieli pomergować wszystkie drzewa (na razie bez nowo stworzonych $\log n$). Koszt tej operacji jest dosyć drogi - liniowy. Jednak zostanie on w pełni pokryty przez kredyty w domergowywanym drzewie.

Po zmergowaniu ich, mamy dwa kopce dwumianowe, oba posiadające $O(\log n)$ drzew dwumianowych. Operacja mergowania ich, będzie nas kosztować $\log n$ środków. Pokryjemy to w pełni z pozostałego budżetu operacji $delete\_min$.

Dzięki takiej analizie, widzimy że operację $delete\_min$ wykonujemy w czasie $O(\log n)$

## Słowo o amortyzacji

Powyższa analiza, mogła być trochę niejasna. Jednak idea jest w miarę prosta. W materiałach pomocniczych zamieszczony jest film wyjaśniający tą idee na przykładzie [[Kopce Fibonacciego]].

Chodzi tutaj o to, że w naszej analizie czasu poświęconego na daną operację, chcemy brać pod uwagę **wyłącznie** działania na nowych strukturach. Czas operowania na starszych strukturach, przerzucamy na operacje które wcześniej je dodały.

To znaczy, że gdy mergujemy ze sobą $n$ drzew stopnia $0$ w kopcu, to koszt tej operacji zrzucamy na $insert$, który je dodał, a nie na $delete$, podczas którego jest to wykonywane.

Dobrym sposobem na zapamiętanie ile dana operacja będzie kosztować kredytów i jaką będzie miała złożoność jest ta formuła:

$$
O(\# [new\ roots\ after] + [extra\ work])
$$

Jak widzimy idealnie się to pokrywa z tym co jest wyżej i jest w łatwe do zapamiętania. Potrzebujemy $\# [new\ roots\ after]$ kredytów, aby rozdać je nowo powstałym drzewom i móc pomijać ich koszt w kolejnych operacjach, a do tego potrzebujemy wystarczająco kredytów, aby zając się nowymi strukturami, które jeszcze nie mają kredytów: $[extra\ work]$.

Suma tych kredytów, pod notacją asymptotyczną, daje nam złożoność danej operacji.

Możemy też o tym pomyśleć tak: robimy burdel w kopcu, więc weźmiemy odpowiedzialność za jego naprawienie. Jak wrzucam na stertę drzew bezmyślnie jakiś wierzchołek to biorę na siebie odpowiedzialność, że jak Loryś przyjdzie zobaczyć czy jest porządek, to go posprzątam.

## Postscriptum

W sieci można znaleźć wiele różnych implementacji kopca dwumianowego. Również takiego, w którym wierzchołki mają wskaźniki na swego rodzica i są w stanie wykonać operację $decrement$ vel $decrease\_key$. Może być to jednak mylące na egzaminie, ponieważ Loryś będzie zakładał tą wersję pokazaną na wykładzie.

## Materiały pomocnicze

https://web.stanford.edu/class/archive/cs/cs166/cs166.1146/lectures/06/Small06.pdf

Analiza kopca Fibonacciego
https://www.youtube.com/watch?v=6JxvKfSV9Ns