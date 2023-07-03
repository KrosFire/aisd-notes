![[Pasted image 20230617165329.png]]

Bardzo prosty algorytm: przechodzimy po każdym wierzchołku i przypisujemy mu indeks.

Następnie wywołujemy na każdym wierzchołku BFS'a, który będzie szukał odległości innych wierzchołków od danego wierzchołka.

Na koniec BFS wypisze te pary $(v, u)$, które są od siebie w odległości $C$ i jednocześnie $\text{index}(v) > \text{index}(u)$. Dzięki temu unikniemy duplikatów.