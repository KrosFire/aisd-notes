
Kopiec binarny jest drzewiastą strukturą danych implementowaną przez listę. Można go wykorzystać do implementacji kolejki priorytetowej, dzięki czemu możemy wyciągać wartości w $O(log(n))$ czasie. 

## Właściwości
W kopcu minimum, każde dziecko, ma wartość większą bądź równą wartości rodzica.

Index lewego i prawego dziecka: $2i+1; 2i+2$.
Index rodzica: $\lfloor\frac{i-1}{2}\rfloor$

## Funckcje

### Heapify (sift down)

Operacja ta służy do zachowania właściwości kopca. Sprawdza ona, czy rodzic ma wartość mniejszą od jego dzieci i jeśli nie ma, to zamienia on rodzica z największym dzieckiem i wywołuje się rekurencyjnie na poddrzewie, do którego został przeniesiony rodzic.

Złożoność to: $O(\log(n))$

### Build heap

Operacja ta, w prostym rozwiązaniu, polegałaby na iteracji przez każdy wierzchołek i wywoływaniu na nim operacji `Heapify`. Wtedy miałaby złożoność $O(n\log(n))$.

Jednak jeśli zaczniemy od dołu drzewa, to zauważymy, że możemy pominąć wszystkie liście.
Zaczniemy więc operacje `Heapify` od pierwszego wierzchołka, który nie jest liściem.

Możemy zauważyć że na wysokości $h$ (licząc od liści - $1$) występuje:
$$
\frac{n}{2^h}
$$
wierzchołków.

Dzięki temu złożoność budowy kopca będzie wynosić:
$$
\sum_{h=0}^{\lfloor\log(n)\rfloor}\frac{n}{2^{h+1}}O(h)
$$
$$
n\sum_{h=0}^{\lfloor\log(n)\rfloor}\frac{h}{2\cdot2^h}
$$
$$
n\sum_{h=0}^{\infty}\frac{h}{2^h}
$$

Do czego zmierza $\sum_{h=0}^{\infty}\frac{h}{2^h}$

Wiemy że:
$$
\sum_{h=0}^{\infty}\frac{1}{2^h}=\frac{1}{1-\frac{1}{2}}
$$

Jeśli teraz weźmiemy pochodną to mamy:
$$
x^h = \frac{1}{2^h}
$$
$$
\frac{d}{dx}\sum_{h=0}^{\infty}x^h=\frac{d}{dx}\frac{1}{1-x}
$$
$$
\sum_{h=0}^{\infty}\frac{h}{2^{h-1}}=\frac{1}{(1-\frac{1}{2})^2}
$$
Wystarczy teraz że przemnożymy przez $\frac{1}{2}$
$$
\sum_{h=0}^{\infty}\frac{h}{2^{h}}=\frac{\frac{1}{2}}{(1-\frac{1}{2})^2}
$$
$$
\sum_{h=0}^{\infty}\frac{h}{2^{h}}=4\frac{1}{2}=2
$$

A zatem złożoność obliczeniowa wynosi:
$$
O(n\cdot2)=O(n)
$$

Algorytm możemy zacząć od pierwszego rodzica czyli od indeksu: $\lfloor\frac{n-1}{2}\rfloor$ do $0$

### Insert (sift up)

Wkładamy element na koniec kopca i rekurencyjnie porównujemy z jego rodzicem. Czas $\log(n)$

### Znajdowanie minimum

Minimum jest zawsze na indeksie 0, czyli $O(1)$

### Zdejmowanie minimum

Swapujemy ostatni element z pierwszym. Usuwamy ostatni - czyli minimum. A następnie robimy sift down. Zajmuje nam to więc $O(\log(n))$

Jest tylko jeden problem z tym algorytmem. Robi on $2\log(n)$ porównań, ponieważ wpierw porównuje on dwójkę dzieci, a następnie najmniejsze dziecko z rodzicem.

Lepszy pod tym względem jest następujący algorytm:
1. Zdejmij najmniejszą wartość i zostaw dziurę - może nią być $+\infty$
2. sift_down(K, 0)
3. Zastąp $+\infty$ ostatnim wierzchołkiem
4. sift_up ostatni wierzchołek

Dzięki temu, że $+\infty$ schodzi na dół, nie musimy porównywać go z dziećmi, dzięki czemu osiągamy $O(\log(n))$ porównań. Problemem jest jedynie wchodzenie na szczyt ostatniego elementu. Podczas tego procesu, porównujemy go jedynie z rodzicem, jednakże w najgorszym przypadku, może on dojść do wysokości $log(n)-1$, co sprawi że będziemy mieli $O(2\log(n))$ porównań, ale w rzeczywistości jest to mało prawdopodobne. Dlatego w większości przypadków, złożoność porównań będzie wynosić $O(\log(n))$

### Połączenie dwóch kopców

Dwie techniki:
1. Połączyć dwie listy i je ponownie zbudować - $O(n)$
2. Jeśli jedna lista jest znacznie mniejsza od drugiej, przenieść $k$ elementów z mniejszej listy do drugiej. Zajmie to nam $k\log(n)$

