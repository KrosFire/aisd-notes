![[Screenshot 2023-06-15 at 17.19.19.png]]

Idea jest prosta. Liczby $a_i$ są całkowitymi, więc najmniejsza liczba, którą można potencjalnie wykreślić wraz z $a_1$ jest na indeksie $\lceil \frac{n}{2}\rceil$.

Najwięcej liczb wykreślimy, gdy liczba co najmniej dwa razy większa, jest minimalną liczbą w ciągu, która spełnia ten warunek.

```python
def count(A):
	counter = 0
	left = 0
	right = ceil(n/2)
	while left < ceil(n/2) and right < n:
		if 2*A[left] <= A[right]:
			counter++
			left++
		right++

	return counter
```

Dowód:

Weźmy optymalne usuwanie: $u$, i niech $u$ zawiera usunięcie pary $(a,2a)$, której my nie usunęliśmy

Są $3$ przypadki.

1. $(a,2a)$ są w pierwszej połówce

W takim razie, na pewno byliśmy w stanie przyporządkować $a$ do jakiejś innej liczby w drugiej połówce, ponieważ zawiera ona liczby $\le 2a$

2. $(a,2a)$ są w drugiej połówce

Skoro $2a$ i $a$ są po prawej stronie, to oznacza, że w pierwszej połowce, musi być liczba którą byliśmy w stanie przyporządkować albo $a$, a na pewno $2a$.

3. $(a,2a)$ są w różnych połówkach

 Jeśli są w różnych połówkach, to musi oznaczać, że nasz algorytm przyporządkował $2a$ jakiejś liczbie przed $a$ i potencjalnie przyporządkował $a$ jakiejś liczbie $\ge 2a$

W każdym przypadku nasze rozwiązanie jest conajmniej tak samo optymalne.