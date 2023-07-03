Algorytm ten wykorzystuje numerowanie/hashowanie podsłów w unikalny sposób, dzięki czemu jesteśmy w stanie w łatwy sposób sprawdzić czy w tekście znajduje się nasz wzorzec.

Numerowanie to odbywa się w następujący sposób:

Zaczynamy od podciągów rozmiaru $1$ i każdej literze przyporządkowujemy liczbę naturalną zgodną z jej porządkiem leksykograficznym. Jesteśmy w stanie to zrobić w czasie liniowym.

Mając podstawę - numerowanie wzorców o rozmiarze $k$, jesteśmy w stanie łatwo ponumerować podciągi o długości $2k$. Osiągamy to poprzez wzięcie podciągów o długości $2k$ i stworzenie krotki numerów przyporządkowanym dwóm podciągów długości $k$, z których jest zrobiony. Następnie posortowanie leksykograficznie tej pary i przyporządkowanie jej odpowiedniej liczby.

Przykład:

![[Screenshot 2023-05-26 at 21.51.06.png]]

Algorytm ten działa w czasie $O(n\log n)$

Gdy mamy do dyspozycji numeracje słów $8$ literowych i tekst $15$ literowy możemy nadać liczbę ciągowi $15$ literowemu poprzez parę dwóch nachodzących na siebie słów $8$ literowych.