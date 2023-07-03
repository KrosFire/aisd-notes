![[Screenshot 2023-06-30 at 20.24.18.png]]

Idea jest taka:

Idziemy po wszystkich listach jednocześnie. W każdym kroku, spośród obecnie wskazywanych wartości w listach, wybieramy minimum i maksimum.

Usuwamy z kopca minmaxowego, w którym przechowujemy te wartości znalezione minimum. Sprawdzamy czy (Maximum wśród minimów - minimum minimów), daje nam mniejsze $r$ niż obecnie mamy wyliczone i jeśli tak to je aktualizujemy. Do tego aktualizujemy pointer na tablicy, która miała minimum minimów i dodajemy jego następny element.

Intuicja jest taka, że chcemy znaleźć największą wartość w pewnym zbiorze, który zaczyna się wcześnie na osi X, która zbliży nas najbardziej do minimalnej wartości w zbiorze zaczynającym się późno na osi X.

Złożoność to: $O(n\log k + k)$ - ponieważ przejdziemy przez potencjalnie $n$ elementów, zdejmując min i max z kopca o wysokości $\log k$. Do tego stworzymy kopiec w czasie $O(k)$

Cudos dla Oli Stępniewskiej:
![[Pasted image 20230630202712.png]]
![[Pasted image 20230630202719.png]]