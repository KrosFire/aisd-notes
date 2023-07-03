Sieci sortujące to struktura danych podobna do [[Sieć przełączników]], tylko zbudowana jest z sieci komparatorów. Przykład takowej sieci:

![[Screenshot 2023-05-27 at 20.30.22.png]]

Zadaniem naszym jest stowrzenie optymalnych sieci sortujących, czyli takich które sortują ciąg przy użyciu jak najmniejszej ilości komparatorów i głębokości.

## Zasada zero-jedynkowa

Zasada ta mówi, że jeśli dana sieć potrafi poprawnie posortować dowolny ciąg $n$ zer i jedynek, to potrafi posortować dowolny ciąg innych $n$ wartości.

Zasada ta opiera się na lematcie, że dla dowolnej **niemalejącej** funkcji $f$, sieć która posortuje ciąg $a = <a_1,a_2,...,a_n>$ na $b=<b_1,b_2,...,b_n>$, to posortuje ciąg $f(a) = <f(a_1),f(a_2),...,f(a_n)>$ na $f(b)=<f(b_1),f(b_2),...,f(b_n)>$.

Dowód lematu:

Jeśli na wejściu do sieci mamy dwa argumenty $a_1$ i $a_2$, to na górnym wyjściu sieci będzie znajdować się $min(a_1,a_2)$ a na dolnym $max(a_1,a_2)$. Analogicznie z $f(a_1), f(a_2)$. Na górze będzie $min(f(a_1), f(a_2))$ a na dole $max(f(a_1),f(a_2))$. Ponieważ $f$ jest funkcją niemalejącą $min(f(a_1), f(a_2)) = f(min(a_1, a_2))$. 

Jest to prawdziwe rekurencyjnie schodząc głębiej w sieci.

Dowód zasady 0/1:

Załóżmy nie wprost, że sieć dobrze sortuje ciągi zero jedynkowe, ale istnieje ciąg $a=<a_1,a_2,...,a_n>$, który jest sortowany niepoprawnie, ponieważ istnieje liczba $a_i$ która jest mniejsza od $a_j$, a niemniej sieć ustanawia $a_j$ przed $a_i$.

Weźmy na warsztat taką funkcję:
$$
f(x) = 0 \;iff\; x \le a_i
$$
$$
f(x) = 1 \;iff\; x > a_i
$$

Sieć ta posortuje poprawnie ciąg $f(a)$, ponieważ jest to ciąg zer i jedynek. A zgodnie z lematem o tym, że porządek wyników funkcji, jest taki sam jak ich argumentów, dla funkcji niemalejących (f jest funkcją niemalejącą). Mamy więc sprzeczność, ponieważ to oznacza, że sieć ta zwróci nam ciąg, w którym $a_i$ jest przed $a_j$, ponieważ $f(a_i)=0$ a $f(a_j)=1$.

## Sieć bitoniczna

Aby zaprojektować sieć sortującą, musimy wpierw zaprojektować sieci które sortują ciągi bitoniczne, czyli takie, które np. są wpierw rosnące, potem malejące, a na koniec znów rosnące (i na odwrót).

Projektując tą sieć skupimy się na ciągach zero jedynkowych, dla łatwiejszej analizy.

Sieć ta będzie się składać z $half-cleaner$-ów. Czyli takich sieci, które dla ciągu o długości $n$, tworzą oczyszczony ciąg $\frac{n}{2}$ górny, lub dolny. A pozostała połowa jest wciąż bitoniczna.

Jak możemy zauważyć, połączenie takich sieci rekurencyjnie na połówkach tworzy nam sieć sortującą o głębokości $\log n$.

Pojedyńczy $half-cleaner$ wykonuje operację sortowania w jednej jednostce czasu.

![[Screenshot 2023-05-27 at 21.39.59.png]]

Dowód że $half-cleaner$ dobrze sortuje:
![[Screenshot 2023-05-27 at 21.40.26.png]]

![[Screenshot 2023-05-27 at 21.41.39.png]]

## Sieć scalająca

No dobrze, a co jeśli na wejściu ciąg nie jest bitoniczny? To go zróbmy bitonicznym.
![[Screenshot 2023-05-27 at 22.14.57.png]]

Następnie będziemy używać half cleanerów, aby ogarnęły dwa bitoniczne podciągi.
![[Screenshot 2023-05-27 at 22.15.47.png]]

Ostatecznie cała sieć będzie tak wyglądać:
![[Screenshot 2023-05-27 at 22.16.18.png]]

Ostateczna głębokość, czyli też złożoność obliczeniowa takowej sieci wynosi: $O(\log^2n)$