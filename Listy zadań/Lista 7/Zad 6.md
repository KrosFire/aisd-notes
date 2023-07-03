![[Screenshot 2023-06-30 at 19.02.25.png]]

Z wykładu wiemy, że wstawianie do tablicy hashującej wymaga średnio:

$$
\le \frac{1}{1-\alpha}
$$

prób.

Jeśli więc klucz $k$ był $i+1$ wartością wstawianą do tablicy, to oczekiwana liczba sprawdzeń jest nie większa niż:
$$
\frac{1}{1-\frac{i}{m}}
$$
$$
\frac{m}{m-i}
$$

Uśredniając:
$$
\frac{1}{n}\sum_{i=0}^{n-1}\frac{m}{m-i}
$$
$$
\frac{m}{n}\sum_{i=0}^{n-1}\frac{1}{m-i}
$$
$$
\frac{1}{\alpha}\sum_{k=m-(n-1)}^{m}\frac{1}{k} \le
$$
$$
\frac{1}{\alpha}\int_{m-n}^m\frac{1}{x}dx
$$
$$
\frac{1}{\alpha}\ln\frac{1}{1-\alpha}
$$