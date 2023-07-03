![[Screenshot 2023-06-16 at 20.42.51.png]]

Tworzymy dwie listy: $N^{+} = \{(a_i,b_i) : a_i\le b_i\}$ i $N^-=\{(a_i,b_i) : a_i > b_i\}$.

$N^+$ sortujemy niemalejąco względem $a_i$

$N^-$ sortujemy nierosnąco względem $b_i$

Następnie łączymy te dwie kolejki, co tworzy nasze ustawienie: $N^+N^- = Schedule$

Pomyślmy teraz o tych zadaniach jak o projektach, których koszt wykonania wynosi: $a_i$ a przychód wynosi: $b_i$. Kapitał początkowy, potrzebny na wykonanie wszystkich $N$ zadań jest równy ilości czasu, gdy druga maszyna jest bezczynna. Minimalizując czas bezczynności (kapitał początkowy), minimalizujemy całkowity budżet potrzebny na wykonanie wszystkich zadań. Ponieważ przychód z wszystkich zadań jest stały, więc jedyne oszczędności jakie możemy wykonać są na naszym “kapitale zakładowym”. Czyli minimalizując czas bezczynności maszyny drugiej, minimalizujemy ogólny czas wykonania wszystkich zadań.

Nasz algorytm wybiera zadania, które najszybciej dadzą nam przychód, a następnie wykonuje projekty które dają od największego do najmniejszego przychodu (przy czym generując straty).

Niech $J_i \le_JJ_j$ będzie oznaczać, że według naszego algorytmu zadanie $J_i$ jest wykonywane przed zadaniem $J_j$

Załóżmy że istnieje lepsze ustawienie projektów $S$.

$J_i\le_J J_j$ lecz $J_j$ występuje przed $J_i$ w $S$

1. $J_i, J_j \in N^+$
    
    Wiemy że $a_i \le a_j$ i $b_i-a_i \ge 0$. Zatem po zamianie $v_j$ - budżet przed $J_j \implies v_j \ge a_j$ $(J_j,J_{j_1},J_{j_2},...,J_{j_k},J_i)$ na $(J_i,J_j,J_{j_1},...,J_{j_k})$ ($\forall j' (1 \le j' \le k) J_j\le_JJ_{j_{j'}}$) budżet początkowy się nie zwiększy, ponieważ musiał pokryć $a_j$, więc jest w stanie pokryć również $a_i$. A $b_i$ sprawi że wszystkie straty przez $a_i$ zostaną pokryte, może nawet z zyskiem. A zatem po zakończeniu pracy $J_i$ może być tyle samo, lub więcej zapasów na $J_j$ i zadania po nim. Co sprawi że kapitał zakładowy może się tylko zmniejszyć.
    
2. $J_i,J_j \in N^-$
    
    Niech budżet przed $J_j$ wynosi $v_j$. Po wykonaniu wykonaniu $J_j$ będzie on wynosić: $v_j-a_j+b_j \ge a_i \ge 0 \implies v_j\ge a_i$. Ponieważ $J_i$ występuje po $J_j$ więc budżet musi być wystarczający na pokrycie prac nad $i$ - tym projektem. Wiemy że $b_i \ge b_j$, a zatem:
    
    $$
	b_i \ge b_j
	$$
	$$ v_j+b_i \ge v_j+b_j $$
	$$ (v_j-a_i+b_i)-a_j \ge (v_j-a_j+b_j)-a_i \ge 0 $$
    
    Widzimy więc, że budżet po wpierw wykonaniu pracy $i$ będzie wystarczająco duży na późniejsze wykonanie pracy $j$. A zatem po zmianie tych zadań będziemy mieścić się w budżecie. A nawet jesteśmy w stanie zminimalizować stratę.
    
3. $J_i\in N^+, J_j\in N^-$
    
    Ponieważ $J_j$ zmniejsza budżet, a $J_i$ go zwiększa. Jeśli wpierw wykonamy $J_i$ czyli zamienimy te dwie prace, to będziemy w stanie potencjalnie zminimalizować kapitał zakładowy.