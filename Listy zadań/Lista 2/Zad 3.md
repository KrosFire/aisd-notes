Nieprzecinające się odcinki
![[Screenshot 2023-06-16 at 16.56.29.png]]

```python
def max_set(I):
	sorted = sort_by_k(I) # n log(n)
	last_i = -INF
	max_set = []
	for i in sorted:
		if i.p > last_i:
			max_set.push(i)
			last_i = i.k
	return max_set
```

Algorytm działa w czasie $O(n\log n)$ z powodu sortowania.

Dowód:

Niech zbiór odcinków zwrócony przez ten algorytm będzie $A$. Niech bardziej optymalny zbiór będzie zbiorem $B$.

Niech $i$ będzie pierwszym miejscem w którym $A[i] \neq B[i]$. Możliwości:

$B[i]$  kończy się wcześniej niż $A[i]$. Jest to sprzeczność, ponieważ wtedy nasz algorytm wybrałby odcinek $B[i]$ zamiast $A[i]$

$B[i]$ kończy się wtedy co $A[i]$. Jest tak samo dobre

$B[i]$ kończy się później co $A[i]$. Potencjalnie $B[i]$ blokuje nam odcinek, którego $A[i]$ nie blokuje. Ergo $B$ jest potnecjalnie gorsze od $A$.

