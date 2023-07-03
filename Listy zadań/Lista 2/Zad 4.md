Wydawanie reszty
![[Screenshot 2023-06-16 at 18.10.11.png]]

Algorytm zachłanny:

```python
def get_change(a,b):
	mianowniki = []
	i = 1
	suma = 0
	while suma < a/b:
		if 1/i + suma <= a/b:
			 suma += 1/i
			 mianowniki.push(i)
		i++
	return mianowniki
```

Algorytm zachłanny zawsze znajdzie rozwiązanie, ponieważ w każdym kroku suma będzie się zwiększać. Jeśli odejmowalibyśmy sumę od ułamka $\frac{a}{b}$, to licznik $a$ cały czas zmniejszałby się conajmniej o $1$. A więc w którymś momencie, algorytm by się zakończył.

Niekoniecznie byłoby to rozwiązanie optymalne. Przykład:

$$
\frac{1}{4}+\frac{1}{5}=\frac{9}{20}=\frac{1}{3}+\frac{1}{9}+\frac{1}{180}
$$