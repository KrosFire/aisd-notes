## Problem

Mając dwa ciągi:
$A=a_1,a_2,...,a_n$
$B=b_1,b_2,...,b_m$

Chcemy znaleźć najdłuższy ciąg $C$ takie że:
1. $\forall c \in C \quad c\in A\cap B$
2. Elementy w $C$ zachowują porządek ciągów $A$ i $B$

Przykład:
```
A = b b a b a a b b a
B = a b b a c d a g

----

C = b b a a
```

## Rozwiązanie Part 1

Tworzymy macierz (tablicę dwuwymiarową) $m \times n$

Uzupełniamy tą macierz w taki sposób, że komórka $T[i][j]$ zawiera długość LCS, dla podciągów: $A[1,...,i]$ i $B[1,...,j]$.

Mamy do rozpatrzenia wartość w kratce $T[i][j]$. Mamy dwie możliwości:
1. $A[i] = B[j]$
	Wstawiamy zatem w pole $T[i][j]$ wartość o $1$ większą od wartości w polu $T[i-1][j-1]$ - zwiększamy długość LCS.
	Gdybyśmy dodali wartość o jeden większą z kratki powiedzmy $T[i][j-1]$, to narazilibyśmy się na sytuację, w której $A[i] = B[j-1]$, a więc zduplikowalibyśmy wartość ciągu $A$. Jeśli zaś wybierzemy pole $T[i-1][j-1]$, to będzie w nim długość LCS, dla wszystkich wyrazów ciągu, od początku ciągów, do elementów (z wyłączeniem) obecnie rozważanych.
2.  $A[i] \neq B[j]$
   Skoro te dwa elementy nie są takie same, to nie możemy zwiększyć długości LCS. Będziemy zatem jedynie propagować obecny LCS, czyli $T[i][j] = max(T[i-1][j],T[i][j-1])$

Przez taką tablicę iterujemy się i wypełniamy od lewej do prawej, od góry do dołu. Dzięki czemu na koniec otrzymujemy w komórce $T[n][m]$ długość LCS.

![[Pasted image 20230325150623.png]] ![[Pasted image 20230325150628.png]] ![[Pasted image 20230325150633.png]]

**ALE MY CHCEMY WIEDZIEĆ JAK WYGLĄDA LCS, A NIE JAKĄ MA DŁUGOŚĆ**

## Rozwiązanie Part 2

Jak to rozwiązać? Bardzo łatwo.

Wiemy, że jeśli $A[i] \neq B[j]$, to wartość w polu $T[i][j]$ jest taka sama, jak w polu na górze, lub po lewej ($T[i-1][j]$, $T[i][j-1]$). Zatem możemy pominąć te pole i iść w lewo albo w górę, na pole o tej samej wartości.

Gdy jednak pola $T[i-1][j]$, $T[i][j-1]$ mają mniejszą wartość od $T[i][j]$, to oznacza, że $A[i] = B[j]$, a zatem ten element, należy do LCS. Dodajemy go więc na początek ciągu wynikowego i przechodzimy do pola $T[i-1][j-1]$ i powtarzamy kroki.

## Złożoność

Czasowo, mamy oczywiście $O(n\times m)$, czyli powiedzmy $O(n^2)$ - oczywiście pomijając razy $2$, przy aproksymacji.

Pamięciowo mamy również $O(n^2)$ ponieważ musimy zpamiętywać tablicę długości

## Optymalizacje

Gdy chcemy wyznaczyć jedynie długość LCS, nie musimy zapamiętywać wszystkich wyników. Możemy stworzyć jedynie dwa wektory o długości $m$ i $n$ i na nich prowadzić wszelkie obliczenia. Dzięki czemu pamięć zmniejszy nam się do $O(n+m)$

