Algorytm polegający na zliczaniu ilości wystąpień danej liczby w liście i na tej podstawie oblicza indeks, od którego powinna występować ta liczba.

Algorytm można podzielić na 3 fazy.

### Faza 1 - zliczanie

W tablicy wszystkich unikalnych liczb zapisujemy liczbę ich wystąpień przechodząc się po oryginalnej tablicy

![[Screenshot 2023-03-28 at 19.35.56.png]]

### Faza 2 - obliczanie indeksu startowego

Skoro mamy liczbę wystąpień danych liczb, to łatwo nam jest obliczyć od jakiego miejsca powinny się one zaczynać. Mianowicie musimy przejść po liście ilości wystąpień kluczy i zsumowywać ze sobą pary. Dzięki czemu obliczymy ile jest elementów o indeksach mniejszych od danego elementu.

Następnie wystarczy jedynie przesunąć te wartości o jeden w prawo, ponieważ chcemy mieć na tamtych miejscach indeksy rozpoczęcia a nie zakończenia i ta faza jest gotowa.

![[Screenshot 2023-03-28 at 19.43.20.png]]

### Faza 3 - sortowanie

Przechodzimy od lewej do prawej po oryginalnej tablicy i sprawdzamy w naszej tabeli indeksów, gdzie w wynikowej tablicy powinniśmy wstawić element. Za każdym razem gdy dany element wstawimy, inkrementujemy indeks początkowy dla danego klucza.

Algorytm jak widzimy jest dzięki temu szybki i stabilny

Jego złożoność to zaskakujące $O(n+k)$, gdzie $n$ jest długością tablicy, a $k$ ilością unikalnych kluczy.

Pamięciowo również wychodzi: $O(n+k)$.

Nie jest on ograniczony $\Omega(n\log n)$ ponieważ nie porównuje on ze sobą elementów.

Jednakże jest on niewydajny dla tablic z dużą ilością różnych kluczy