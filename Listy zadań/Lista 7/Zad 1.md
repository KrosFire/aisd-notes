![[Screenshot 2023-06-21 at 15.51.58.png]]

Czas wykonania operacji na słowniku wyraża się wzorem:
$$
\sum_i p_i \cdot h_i
$$
$h$ - wysokość, czas oczekiwany na wykonanie polecenia
$p$ - prawdopodobieństwo odpowiadającej liczbie zapytań

Aby odnaleźć drzewo, które minimalizuje koszty odpytań, skorzystamy z programowania dynamicznego i stworzymy tabelkę $dp$ o wymiarach $n \times n$.

Przekątną wypełniamy po prostu prawdopodobieństwem wyboru danego elementu:
$$
dp[i][i] = p_i
$$

Będziemy dalej szli przekątnymi wypełniając je wartościami, które minimalizują koszt drzewa:
$$
dp[i][j] = \min_{i\le k\le j}(
\bigg[dp[i][k-1]+\sum_{l=i}^{k-1}p_l\bigg]
+p_k+
\bigg[dp[k+1][j]+\sum_{l=k+1}^jp_l\bigg])
$$
$$
dp[i][j] = \min_{i\le k\le j}(dp[i][k-1]+dp[k+1][j])+\sum_{l=i}^jp_l
$$

Powyższe równanie zapewnia nam minimum, ponieważ to co robimy to sprawdzamy jakie dwa drzewa podpiąć pod jaki wierzchołek ($k$-ty), tak aby sumaryczny koszt był najmniejszy. Podpinając jednak drzewa pod $k$-ty wierzchołek, koszt odpytania każdego innego zwiększa się o $1$, ponieważ schodzą one niżej w drzewie.

Aby zrobić backtracking, możemy stworzyć albo nową tablicę, która zapamiętuje $k$, albo zapamiętywać krotki $(value, k)$

Algorytm działa w czasie $O(n^3)$