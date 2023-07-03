Sposób działania insertion sorta można skojarzyć sobie z wkładaniem (insert) kart do ręki w odpowiedniej kolejności.
Na początku mamy pustą rękę i stos kart. Wybieramy kartę ze stosu i wstawiamy ją w odpowiednim miejscu w ręce. Aby znaleźć odpowiednie miejsce dla tej karty, porównujemy ją z kartami kolejno od prawej do lewej.
Jest to banalnie prosta metoda i jak można się łatwo domyślić ma wysoką złożoność O(n^2)

```python
for i in range(1, len(arr)):
	sorted_element = arr[i]
	j = i-1

	while j >= 0 and arr[j] > sorted_element:
		arr[j+1] = arr[j]
		j -= 1

	arr[j+1] = sorted_element
```