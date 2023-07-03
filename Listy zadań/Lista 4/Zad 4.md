![[Screenshot 2023-06-17 at 19.21.44.png]]

Długość LCS z liniową pamięciówką: ^c9bc4e

Jeśli chodzi o znalezienie samej długości, to proste zadanie. Wystarczy trzymać w pamięci aktualnie przerabiany wiersz, który na samym początku jest wypełniony zerami. Obecna komórka nad którą pracujemy, posiada informację tą samą, co posiadałaby komórka o wiersz wyżej w klasycznym rozwiązaniu, a w komórce po lewej nic się nie zmienia. Jedynym problemem jest komórka po przekątnej, ale ją wystarczy zapisywać w zmiennej zawsze przed nadpisaniem wartości w komórce.

Samo LCS:

Będziemy wywoływać się rekurencyjnie na jednym z napisów. Jeśli na wejściu dostaniemy dwa napisy: $X$ o długości $m$ i $Y$ o długości $n$, to $k$ będzie indeksem litery w $Y$ - $y_k$, takiej że jest ona ostatnią, która odpowiada w relacji LCS - $S$, literze w $X$ z przedziału $X[1...\frac{m}{2}]$. Jeśli żadna litera w $S$ nie odpowiada literze w pierwszej połowie $X$, to $k=0$.

![[Screenshot 2023-06-17 at 21.02.16.png]]

Wracając do klasycznego rozwiązania. Liczyliśmy wtedy podciąg idąc od lewej do prawej strony po napisach. Funkcję liczącą w klasyczny sposób nazwijmy $lcs(i, j)$. Zdefiniujmy sobie $lcs'(i,j)$, która liczy na odwrót - od końca.

$$
lcs'(i,j) = \max(lcs'(i+1, j), lcs'(i, j+1)) \;\lor\; lcs'(i+1, j+1)+1
$$

Gdy podzielimy $X$ na pół, będziemy liczyć lewą górną macierz poprzez $lcs$, a prawą dolną poprzez $lcs'$.

W każdym momencie, potrzebujemy tylko dwóch list $n$ elementowych

![[Screenshot 2023-06-17 at 21.14.00.png]]

A zatem
$$
LCS(X,Y) = \max_{0\le l \le n}\{lcs(m/2, l),\; lcs'(m/2+1,l+1)\}
$$

Przebieg algorytmu:

Na początku wypełniamy wiersz $m/2$ oraz $m/2+1$, w sposób pokazany [[#^c9bc4e | tutaj]]. Zajmie to nam $O(mn)$ czasowo i $O(n)$ pamięciowo.

Następnie znajdujemy $k'$ - czyli indeks ostatniego znaku słowa $Y$, znajdującego się w pierwszej połowie $X$'a i będącego w LCS. Możemy go znaleźć w czasie $O(n)$ przechodząc po tych dwóch tablicach.

Następnie wywołujemy się rekurencyjnie na $LCS(X[1...m/2], Y[1...k'])$ oraz $LCS(X[m/2+1...m], Y[k'+1...n])$. Base case jest taki, że dzieląc $X$ na pół zostanie nam jeden znak, który możemy porównać z $Y$ i go zwrócić, bądź nie, albo może być pusty napis, który oczywiście możemy zwrócić. W fazie mergowania, po prostu będziemy konkatenować te napisy.

W każdym wywołaniu będziemy musieli policzyć następujące wiersze i kolumny macierzy:

![[Screenshot 2023-06-17 at 22.11.33.png]]
![[Screenshot 2023-06-17 at 22.10.56.png]]

Czyli czasowo w każdym wywołaniu będziemy robić $O(mn)$ roboty.

Sumarycznie wyjdzie to nas:
$$
O(mn)\cdot\sum_{i=0}^\infty\bigg(\frac{1}{2}\bigg)^i = O(mn)\cdot2=O(mn)
$$

Pamięciowo zaś, nigdy nie spamiętujemy więcej rzeczy niż dwa wiersze macierzy i napis + stałe. Także mamy $O(n)$ pamięciowo. **Essa.**

Paperek:
![[Hirschberg.pdf]]