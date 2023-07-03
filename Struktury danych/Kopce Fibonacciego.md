Sprytna implementacja kopca, dzięki której jesteśmy w stanie wykonać operację $decrement$ w czasie $O(1)$. Dzięki temu możemy zaimplementować [[Algorytm Dijkstry]] w bardzo wydajny sposób.

## Struktura

Kopiec Fibonacciego posiada strukturę lasu drzew. Tak samo jak [[Kopce dwumianowe]], z tą różnicą że drzewa w tym lesie mogą być dowolne.

Tak samo jak kopce dwumianowe operacje łączenia kopców jak i wstawiania do kopca wykonujemy leniwie w czasie $O(1)$.

Wierzchołki poza tradycyjnymi wskaźnikami na swoje dzieci, rodzica i rodzeństwo oraz wartością klucza, posiadają flagę $loser$. Flaga ta mówi nam o tym, czy dany wierzchołek nie stracił dziecka.

Kopiec Fibonacciego nosi nazwę Fibonacciego ponieważ spełnia on ciekawą cechę. Każde drzewo w tym kopcu o rzędzie $k$ posiada co najwyżej $\phi^k$ wierzchołków. Gdzie $\phi$ to złoty podział Fibonacciego $\frac{1+\sqrt{5}}{2}$. Oznacza to, że rząd $k = \log_{\phi}n$, co dzięki magii logarytmów i notacji dużego O możemy oszacować jako: $O(\log n)$

## Wycięcie wierzchołka $cut$

Wycinając dany wierzchołek, wycinamy go z wszystkimi jego dziećmi z przynależnego drzewa i wstawiamy ponownie do kopca jako nowe drzewo. Usuwamy też temu wierzchołkowi (korzeń wyciętego drzewa) flagę $loser$.

Następnie sprawdzamy, czy rodzic usuniętego wierzchołka nie stracił już wcześniej dziecka. Jeśli tak, to wykonujemy tą operację ponownie, tym razem na danym rodzicu.

Operacja będzie się wykonywać aż nie natrafimy na korzeń lub wierzchołek, który nie stracił jeszcze dzieci. W takim przypadku ustawiamy mu flagę $loser$.

## Operacja $decrement$

Operacja ta zmniejsza wartość wskazanego wierzchołka. Jeśli w wyniku zmiany tej wartości, zakłócimy porządek kopcowy, wykonamy operację $cut$

## Operacja $delete\_min$

Wykonujemy podobnie jak w kopcu dwumianowym - łącząc drzewa o tym samym **rzędzie - liczbie dzieci**

## Pozostałe operacje

Tak jak w [[Kopce dwumianowe]]

## Analiza złożoności

Ponownie wykorzystamy analogię kredytów i następujący niezmiennik:
"Każde drzewo w kopcu posiada dokładnie jeden kredyt na koncie"

Operacja $decrement$ posiada $4$ kredyty. Pierwszy kredyt pójdzie na zwykłe instrukcje, oraz na przyłączenie węzła do korzeni tego kopca - koszt operacji $meld$. Drugi kredyt przydzielamy nowo powstałemu drzewu w kopcu. Jeżeli usunięty węzeł, był pierwszym dzieckiem, które jego rodzic stracił, to przekazujemy mu pozostałe dwa kredyty. Jednostki te zostaną **w przyszłości** wykorzystane by opłacić kaskadowe usuwanie loserów.

Operacja $delete\_min$ będzie posiadać $2\log n$ kredytów, tak samo jak w kopcach dwumianowych. Pierwszymi $\log n$ kredytów opłacimy wpłaty na konto nowo utworzonych drzew w kopcu, po usunięciu korzenia, z minimalną wartością. Wiemy że będzie ich $\log n$ dzięki wspomnianej wcześniej właściwości kopców Fib. - każde drzewo ma rząd co najwyżej $\log_\phi n$. Reszta analizy jest taka sama jak w kopcach dwumianowych.

Czyli: $delete\_min$ tworzy $\log_{\phi}n$ nowych drzew i musi wziąć za nie odpowiedzialność w przyszłości. Odpowiedzialność za naprawę reszty drzew, biorą operacje które je stworzyły. Czyli złożoność $delete\_min$ to $O(\log n)$

## Dowód stopnia $\log_\phi n$

Weźmy pewne drzewo w kopcu Fibonacciego. Niech posiada ono $y_1,y_2,...,y_n$ dzieci uporządkowanych w kolejności dodania ich do tegoż drzewa.

$k$-te dziecko, było dodane do tego drzewa, gdy miało one stopień co najmniej $k-1$. Oznacza to, że drzewo $y_k$ w momencie przyłączenia, miało również stopień co najmniej $k-1$. W wyniku operacji $decrease\_key$, $y_k$ mógł stracić co najwyżej jedno dziecko. A zatem $degree(y_k)\ge k-2 \ge 0$.

Niech $F_i$ będzie najmniejszym drzewem, które spełnia tą zależność. Czyli $F_0$ składa się wyłącznie z korzenia, a $F_i$ z korzenia i dzieci: $F_0,F_0,F_1,F_2,F_3,....,F_{i-2}$. Jest tak ponieważ $F_i$ przed posiadaniem $F_{i-2}$ miało stopień $F_{i-1}$. A ponieważ bierzemy pod uwagę najmniejsze drzewa, to usunęliśmy jedno dziecko $F_{i-2}$, czyli oryginalnie był drzewem $F_{i-1}$.

Widzimy że $F_j$ jest tworzone z poprzednich dwóch najmniejszych drzew. Czyli spełnia się relacja Fibonacciego. Każde kolejne takie drzewo, jest większe od drugiego $\phi$ razy.

Czyli liczba wierzchołków $F_i$ jest równa:
$$
|F_i| = 1 + \sum_{j=0}^{i-2}|F_j| = \phi^{i-2}
$$

## Tworzenie kopca o wysokości $n$

Dodaj $3$ wierzchołki i usuń najmniejszy. Dwa pozostałe złączą się w drzewo o wysokości $2$.

```
A
|
B
```

Dodaj kolejne $3$ wierzchołki, gdzie jeden z nich ma najmniejszą możliwą wartość i usuń najmniejszy. Ponownie złączą nam się dwa pozostałe, nowo wstawione wierzchołki. Lecz tym razem, połączą się również z już istniejącym drzewem.

```
A
|\
B C
  |
  D
```

Usuńmy teraz B

```
A*
|
C
|
D
```

Możemy ten proces powtarzać w nieskończoność, ponieważ będziemy zwiększać wysokość drzewa o degree $1$, który zawsze jesteśmy w stanie skonstruować dodając $3$ elementy i usuwając najmniejszy z nich.

## Materiały pomocnicze

https://www.youtube.com/watch?v=6JxvKfSV9Ns
https://www.youtube.com/watch?v=fRpsjKCfQjE
https://www.youtube.com/watch?v=RCCUrmklzjg