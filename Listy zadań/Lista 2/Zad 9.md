![[Screenshot 2023-06-17 at 14.48.56.png]]

Mamy dwie permutacje. Obecna: $\pi$ i docelowa: $\sigma$.
Tworzymy tablicę, w której będziemy przechowywać, na jakiej pozycji w $\sigma$ jest liczba na danej pozycji w $\pi$. Tablica: $\text{target}[n]$.

Sam algorytm wygląda tak:

```python
for x=n...1:
	while sigma[x] != pi[x]:
		current_pos = pos_in_pi(sigma[x])
		for i=current_pos+1...x:
			if target[i] <= current_pos:
				swap(pi[current_pos], pi[i])
				swap(target[current_pos], target[i])
				break
```

Czyli idziemy od końca po naszej kombinacji roboczej $\pi$.
Jeśli elementy się nie zgadzają na tej pozycji z kombinacją końcową, to musimy to poprawić.

W tym celu znajdujemy pozycję w $\pi$ elementu, który ma się tam znaleźć. Następnie idziemy na prawo od niego, w kierunku jego pozycji docelowej. Za każdym razem, gdy znajdziemy element, który chce się znaleźć na jego pozycji, bądź też dalej na lewo od niego, to zamieniamy się miejscami.

Dojdziemy tym sposobem zawsze do celu, ponieważ jeśli element nie jest na docelowej pozycji, to na jego drodze do docelowej pozycji, musi być element, który powinien być na obecnej pozycji naszego rozpatrywanego elementu, bądź jeszcze dalej.

Jest to optymalne rozwiązanie, ponieważ minimalny koszt wszystkich swapów, jest równy ilości przesunięć o $1$ w prawo/lewo tych elementów. My nigdy nie "przestrzelimy", czyli nigdy nie zamienimy ze sobą elementów w taki sposób, aby przynajmniej jeden z nich przeskoczył przez swoją pozycję docelową. Zapewnia nam to ten warunek: `target[i] <= current_pos`

Złożoność: $O(n^2)$