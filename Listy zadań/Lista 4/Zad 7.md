![[Screenshot 2023-06-18 at 21.37.46.png]]

Możemy ten problem zmapować, na LIS'a - Longest increasing subsequence.

Mianowicie, prostym nadamy wartość numeryczną zgodną z tym, która pierwsza przecina prostą $l'$ a następnie stworzymy listę, w jakiej kolejności przecinają $l''$.

Dzięki temu będziemy mieli listę liczb ($arr$), w której jeśli dwie liczby nie są w odpowiedniej rosnącej kolejności, to oznacza że się przecinają.

Tablica $dp$ będzie tablicą o długości $n =|arr|$. Będzie ona przechowywać stosy.

Top $dp[i]$ będzie przechowywać najmniejszą liczbę, na której może skończyć się ciąg o długości $i$, oraz pointer do indeksu wcześniejszego stosu, który oznaczać będzie wcześniejszą liczbę w sekwencji.

Algorytm wygląda następująco:

```python
def lcs(arr):
	n = len(arr)
	dp[n]
	dp[1] = stack((arr[1], None))
	l = 1
	for i in range(2, n):
		if arr[i] > dp[l].top()[1]:
			l++
			dp[l] = stack((arr[i], dp[l-1].size()))
		else:
			index = bin_search(dp, arr[i])
			dp[index].push((arr[i], dp[index-1].size()))
	return go_back(arr, l)
```

Aby spełnić podpunkt b, wystarczy przejść się po wszystkich elementach w stosach i idąc za ich pointerami zebrać ich ścieżki.

Dla podpunktu a, złożoność czasowa to $O(n\log n)$ dzięki bin search. Zaś pamięciowa to $O(n)$, ponieważ nie robimy dwuwymiarowej listy, jedynie grupujemy $n$ elementów.

Dla podpunktu b, jedynie złożoność czasowa się rozszerzy do $O(n^2)$, ponieważ będziemy przechodzić po wszystkich elementach, i cofać się do liniowo.

Materiał pomocniczy:
https://www.youtube.com/watch?v=0wT67DOzqBg