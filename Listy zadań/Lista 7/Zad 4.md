![[Screenshot 2023-06-21 at 17.07.26.png]]

_Insert_ będzie mieć $2$ kredyty. $1$ na insert i $1$ na konto wierzchołka.

_DeleteMin_ będzie mieć $2\log n$ kredytów. Pierwszy $\log n$ pójdzie na dzieci usuniętego korzenia, z wartością minimalną. Drugie $\log n$ na przywrócenie porządku. Koszt usunięcia minimum zostanie pokryty z kredytów w wierzchołki z minimum.

_DecreaseKey_ będzie mieć $4$ kredyty. Pierwszy na decrease key i operację _Cut_ (potencjalne). Drugi na konto nowo powstałego korzenia. $2$ pozostałe zostaną odłożone na konto rodzica, jeśli ten nie stracił jeszcze dziecka.

Kiedy operacja _Cut_ się wykona i rodzic okaże się podwójnym loserem, to go odcinamy.

_Meld_ i _FindMin_ po jednej nutce.

_DeleteMin_ ma złożoność $\log n$ ponieważ każdy wierzchołek w kopcu, ma co najwyżej $\log n$ dzieci.

Dowód:

Weźmy dowolne drzewo w kopcu. Jego dziećmi są: $y_1,y_2,...y_k$, gdzie $k$ oznacza kolejność dodania ich do tegoż drzewa. Oznacza to, że $y_k$ zostało dodane do danego drzewa, gdy miało ono stopień $k-1$.

Możemy bezkarnie usunąć dwójkę dzieci danego wierzchołka. Czyli w najgorszym przypadku $y_k$ ma stopień $k-3$.

A to oznacza, że nasze drzewa składać się będzie z wierzchołków o stopniach co najmniej:
$$
0,0,0,1,2,...,k-3
$$

Niech $F_k$ oznacza drzewo o stopniu $k$.
$F_0$ składa się tylko z korzenia.
$F_k = F_{k-1}+F_{k-1}$. Czyli relacja Fibonnaciego się nie zmieniła, jedynie została przestawiona w lewo o $3$ zamiast o $2$.