Algorytm sortujący podobny do merge sort'a.

Polega on na wyborze odpowiedniego pivota - elementu, który będzie decydował o podziale listy. Elementy mniejsze od wybranego pivota, będą w jednej liście, a elementy większe, w drugiej. Następnie rekurencyjnie wywołujemy się na podzielonych listach do momentu, aż będzie mało elementów. Wtedy możemy wykonać np. [[Insert sort]].

Rzeczami decydującymi o szybkości quicksorta, jest wybór pivota i podział na dwie listy.

Podział na dwie listy, można wykonać w prosty sposób liniowo:
```python
def partion(A,p,r):
	i = p-1
	j = r+1
	while i < j:
		repeat j = j-1 until A[j] <= A[p]
		repeat i = i+1 until A[i] >= A[p]
		
		if i<j:
			swap(A[i], A[j])
		else:
			return j

```

Polega to na jednoczesnym przejściu po liście z obu stron aż nie


Optymalny wybór pivota jest trudniejszy.

Jeśli wybierzemy optymalny pivot, to głębokość drzewa wywołań będzie wynosić jedynie $\log n$. Jeśli jednak będzie słaby, to będziemy odejmować tylko jeden element i ostatecznie narazimy się na złożoność $n^2$.

## Metody wyznaczania pivota

### Deterministyczny

Wybieramy zawsze $k$-ty element listy, np. pierwszy jako pivot. Jest to bardzo szybka metoda i efektywna przy zrandomizowanych danych. Jeśli jednak lista jest już posortowana, to czas quicksorta będzie wynosić $O(n^2)$

### Wybór zrandomizowany

Pivot jest wybierany losowo. Niwelujemy dzięki temu problem z faworyzacją jednych list nad drugimi, jak w przypadku metody deterministycznej, aczkolwiek teraz każda lista może być potencjalnie zła czasowo. Jednak jest na to bardzo małe prawdopodobieństwo.

### Mediana z małej próbki

Wybieramy medianę z małej próbki liczb, np. 3. Możemy to robić deterministycznie (pierwszy, środkowy, ostatni) bądź losowo.

Udokumentowano, że jest to bardzo dobrze działający sposób, potrafiący przyspieszyć algorytm nawet o kilkanaście procent.

## Analiza złożoności

### Najlepsza złożoność

Najlepsze złożoność jest wtedy, gdy zawsze dzielimy listę na pół:

$$
T(n) = 2T(\frac{n}{2})+\Theta(n) \implies \Theta(n\log n)
$$

### Najgorsza złożoność

Najgorsza złożoność jest wtedy gdy tworzymy skrajnie nierówne listy:

$$
T(n) = T(0)+T(n-1)+\Theta(n) \implies \Theta(n^2)
$$

### Średnia złożoność

Jeśli wybieramy pivot losowo, to praktycznie zawsze, będzie dzielił listę od $1:3$ do $2:3$.

To znaczy, że najgorszy - skrajny podział, będzie wynosił: $T(n)=T(\frac{n}{3})+T(\frac{2n}{3})+\Theta(n)$

Maksymalna wysokość tego drzewa to: $\log_{\frac{3}{2}}n$

Na każdym poziomie, wykonujemy do $n$ obliczeń

Oznacza to, że złożoność tego quicksorta jest ograniczona: $O(n\log_{\frac{3}{2}}n)$.

Wiemy że:

$$
\log_an=\frac{\log_bn}{\log_ba}
$$
$$
\log_{\frac{3}{2}}n=\frac{\log_2n}{\log_2\frac{3}{2}}
$$

Czyli złożoność quicksorta wynosi:

$$
O(n\frac{\log_2n}{\log_2\frac{3}{2}})=O(n\log_2n)
$$