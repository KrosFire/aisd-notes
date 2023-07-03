https://www.youtube.com/watch?v=TLaGwTnd3HY

## Problem

Posiadając napis, chcemy znaleźć jego najdłuższy podciąg, który jest jednocześnie palindromem.

## Rozwiązanie 1

Najprostrzym rozwiązaniem, jest skorzystanie z algorytmu [[LCS - Longest Common Substring]], poprzez podanie mu wejściowego napisu, oraz jego odwrotności.

## Rozwiązanie 2

Możemy policzyć długość rekurencyjnie - metodą dziel i zwyciężaj. Funkcja $L(i,j)$ - zwraca nam długość LPS od indeksu $i$ do indeksu $j$.

W każdym kroku mamy dwie możliwości:
1. Jeśli $*i = *j$
   Zatem długość tego palindromu wynosi już co najmniej $2$. Zatem końcowa wartość będzie wynosić: $L(i-1,j-1)+2$
2. Jeśli $*i \neq *j$
   Zatem długość tego palindromu wynosi $max(L(i,j-1), L(i-1, j))$


![[Screenshot 2023-03-25 at 16.04.01.png]]

Możemy zauważyć, że w tej metodzie nasze obliczenia się powtarzają. Np w tym przykładzie powtarza się obliczanie wartości: $L(1, 5)$

Skorzystajmy więc z algorytmu **dynamicznego**.

## Rozwiązanie 3

Zacznijmy od zpamiętanie podstawowych wartości rekursji i wspinajmy się wyżej.

Będziemy mieli dwa wektory: $i$ oraz $j$. W głównej iteracji programu, będziemy zwiększać ich odległość od siebie, począwszy od $d = 0$. W ten sposób, policzymy kolejno wartości 

$L(0,0);L(1,1);...;L(n,n)$ - $n$
$L(0,1);L(1,2);...;L(n-1,n)$ - $n-1$
...
$L(0,n)$ - $1$

Wszystkie te wyniki możemy zapamiętać w macierzy $n \times n$ górnotrójkątnej.

Na przekątnej będą wartości $1$.

Następnie w każdej następnej iteracji będziemy mieli wartości zgodne z rekursją w poprzednim rozwiązaniu, czyli:

$\forall d \ge 1 \quad L(i,j) = L(i+1;j-1)+2 \lor L(i,j)=max(L(i;j-1), L(i+1,j))$

Czyli tak samo jak w [[LCS - Longest Common Substring]], będziemy patrzeć po przekątnej jeśli wartości się zgadzają, albo na boki w p. p.

![[Pasted image 20230325163325.png]]