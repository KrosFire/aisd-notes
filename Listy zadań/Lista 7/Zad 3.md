![[Screenshot 2023-06-21 at 16.45.25.png]]

Do tablicy $n$-elementowej wstawiamy $n$ kluczy. 

Prawdopodobieństwo, że klucz **trafił** do listy wynosi:
$$
\frac{1}{n}
$$

Wynika z tego, że szansa **nie trafienia** wynosi:
$$
1-\frac{1}{n} = \frac{n-1}{n}
$$

Prawdopodobieństwo, ze klucz trafi do listy jest dla każdej listy takie samo.

Oznacza to, że oczekiwana ilość pustych list wynosi:
$$
E=n\cdot P
$$
(z liniowości wartości oczekiwanej)

$P$ to prawdopodobieństwo tego, że dana lista jest pusta (prawdopodobieństwo łączne)

List jest $n$ więc:
$$
P=\bigg(\frac{n-1}{n}\bigg)^n
$$

A zatem:
$$
E=n\cdot\bigg(\frac{n−1}{n}\bigg)^n
$$