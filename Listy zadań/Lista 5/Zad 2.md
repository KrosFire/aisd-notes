![[Screenshot 2023-06-19 at 20.35.10.png]]

Opisany w treści zadania problem sprowadza się do sprawdzenia czy w danym ciągu istnieją $3$ liczby, po których dodaniu otrzymamy liczbę $0$.

W wierzchołkach wewnętrznych znajdować się będą kombinację liniowe elementów ciągu wejściowego, a trzy krawędzie prowadzące do synów odpowiadają trzem różnym przyrównaniom: $>0$, $<0$ oraz $=0$

Idea jest taka, że chcemy sobie stworzyć liniowe drzewo decyzyjne i dużo instancji problemów rzędu $n!$. Pokażemy, że odpowiedź na każde z tych problemów, musi wylądować w innym liściu, czyli to drzewo ma dużo liści.

Weźmy sobie niedogodny przykład danych wejściowych:

$$
x = 1, 3, 5, \cdots, n-1, 2n, -(2n+2), -(2n+4),\cdots, -(2n+n)
$$

Może być tych danych więcej, ale wpierw skupmy się na nich.

Jeśli nasze drzewo wpadnie w te właśnie pod problemy, będzie chciało sprawdzić, czy dla jakiejś kombinacji, nie uzyskamy odpowiedzi "TAK". Jednak jest to niemożliwe, ponieważ jeśli weźmiemy, dwie największe liczby dodatnie (z pominięciem $2n$): $n-1$ oraz $n-3$, otrzymamy sumę: $2n-4$. Mimo wszystko jest to wciąż zbyt mała suma, aby ją móc zniwelować.

Próby:
$$
(n-1)+(n-3)-(2n+2)=(2n-4)-(2n+2)=-6
$$
$$
(n-1)+(n-3)-(2n+4)=(2n-4)-(2n+4)=-8
$$
$$
...
$$

Gdy weźmiemy jednak liczbę $2n$, to po zsumowaniu ją z inną liczbą dodatnią, otrzymamy liczbę nieparzystą, co ponownie zniweluje nasze szanse na sumę równą $0$.

Ostatecznie, będziemy mieli $\frac{n}{2}!$ problemów, każdy z odpowiedzią "NIE"

Każda z odpowiedzi na te problemy ląduje w osobnym liściu.
Każdy punkt ma $3$ współrzędne, odpowiadające wartościom sumy. Zał. że istnieją dwa punkt $P_i$ i $P_j$ różniące się na $k$-tej współ. będąc w tym samym liściu. Oznacza to, że na prostej $P_iP_j$ znajdują się tylko punkty z odpowiedzią "NIE".

Weźmy więc punkt $P$, który na $k$-tej współ. ma liczbę parzystą. Okazuje się, że musi się on znajdować na płaszczyźnie, gdzie odpowiedzią jest "TAK", ponieważ istnieje na niej również punkt:
$$
P(k) + 2n -(2n+P(K)) = 0
$$

który ma oczywiście odpowiedź "TAK". A to oznacza, że mamy $\frac{n}{2}!$ liści, czyli drzewa ma $\log_3\frac{n}{2}!$ wysokości. A wiemy że:

$$
n\log n = \log n^n \le \log n! 
$$
