## Problem

Na wejściu dostajemy słowo - ciąg znaków i musimy sprawdzić, czy przynależy ono do danej gramatyki.

Gramatyka składa się z 4 zbiorów:
1. $V_N$ - symbole nieterminalne. Takie które rekursywnie rozwijają się do innych symboli
2. $V_T$ - symbole terminalne. Ostateczne symbole w gramatyce
3. $P$ - zbiór zasad rozwijania symboli nieterminalnych
4. $S$ - symbol startowy

## Rozwiązanie

Należy stworzyć macierz, w której będziemy po kolei zapisywać, jakie symbole nieterminalne, są w stanie stworzyć dany podciąg.

Komórka $m[i][j]$ będzie zawierać zbiór symboli nieterminalnych, za których pomocą jesteśmy w stanie wygenerować podciąg: $a_i,a_{i+1},...,a_j$

Wzór zatem będzie następujący:
$$
m[i][i] = \{A : A \in V_N \land A \to a_i \}
$$
$$
m[i][j] =  \{A : (A \to BC) \in P \land
(\exists k \quad B \in m[i][k] \land C \in m[k+1][j])\} = \cup_{k=i}^{j-1} m[i][k] \otimes m[k+1][j]
$$

## Złożoność obliczeniowa

Ponieważ przechodzimy przez macierz, to mamy główną pętlę $O(n^2)$

Jednakże w każdym kroku musimy sprawdzić sumę mnożeń kartezjańskich podzbiorów, co nam zajmuje czas liniowy.

Zatem mamy: $O(n^3)$