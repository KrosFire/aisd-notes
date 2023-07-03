Chcemy dowieść że znajdowanie min i max, zajmuje co najmniej $\lceil \frac{3}{2}n-2 \rceil$ porównań.

Aby to zrobić załóżmy że zbiorem liczb operuje zły adwersaż, który może zmieniać wartości tego zbioru, nie niszcząć jednak relacji pomiędzy już sprawdzonymi liczbami. Czyli większa liczba, pozostaje większa itd.

Możemy sobie wtedy zdefiniować 4 zbiory:

$A$ - zawiera elementy, których jeszcze nie porównaliśmy
$B$ - zawiera elementy, o których wiemy tylko tyle że są większe
$C$ - zawiera elementy, o których wiemy tylko tyle że są mniejsze
$D$ - zawiera elementy, o których wiemy, że są większe od innych, a mniejsze od jeszcze innych

Aby algorytm mógł rozwiązać zadanie, to zbiór $A$ musi być pusty, a zbiory $B$ i $C$ mogą zawierać wyłącznie po jednym elemencie.

Adwersaż więc będzie dążyć do tego, żeby zbiory $B$ i $C$ były jak największe.

A zatem, gdy porównujemy ze sobą elementy ze zbioru $A$, to zawsze jeden z nich trafi do zbioru $B$, a drugi do $C$.

Czyli na opróżnienie zbioru $A$ potrzebujemy co najmniej $\lceil \frac{n}{2} \rceil$ porównań

Gdy algorytm będzie chciał porównać ze sobą liczby ze zbiorów $B$ i $C$, to adwersaż zawsze będzie twierdził, że $b\in B > c \in C$. A zatem takie porównania nic algorytmowi nie dadzą.

Najbardziej optymalnym rozwiązaniem będzie więc porówynywanie elementów, w ramach jednego zbioru $B$ lub $C$, co zajmie $\lceil 2\frac{n}{2} - 2 \rceil$ porównań aby zbić liczbę elementów w tych zbiorach do jednego.

A zatem minimalna liczba porównań podczas walki z adwersażem wynosi sumarycznie:
$$
\lceil \frac{3}{2}n - 2 \rceil
$$