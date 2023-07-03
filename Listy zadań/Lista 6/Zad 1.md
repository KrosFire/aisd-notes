![[Screenshot 2023-06-20 at 16.16.21.png]]

Istnieje modyfikacja czyniąca algorytm quicksort działającym w miejscu. W oryginalnym sortowaniu szybkim używa się rekursji lub stosu (_de facto_ oba sposoby niewiele się różnią – rekursja w uproszczeniu jest niejawnym stosem) do zapamiętywania miejsc podziału. Więc chociaż algorytm w obu wersjach nie korzysta z dodatkowych tablic o rozmiarze zależnym od rozmiaru danych wejściowych, to nie można nazywać go działającym w miejscu, gdyż wysokość, a więc i wymagania pamięciowe wywołań rekursji/stosu są ściśle zależne od rozmiaru danych początkowych.

Załóżmy, że dla sortowanej tablicy _A_ funkcja _PodzielTablice(l,p)_ zwróciła wartość _s_. W oryginalnym algorytmie quicksort powinno zostać wykonane wywołania _Quicksort(l,s-1)_ i _Quicksort(s+1,p)_. Zamiast tego „zajmujemy się” tylko _Quicksort(l,s-1)_, a pozycje _s+1_ i _p_ zapamiętujemy w następujący sposób:

- s+1: jest jednoznacznie wyznaczona przez koniec ciągu (_l,s-1_) → _(s+1) = (s-1) + 2_
- p: znajdujemy maksimum ciągu (_s+1,p_) i zamieniamy tę pozycję z pozycją _s_. Aby odtworzyć pozycję _p_, wystarczy przeszukiwać ciąg w prawo do znalezienia elementu większego od wartości stojącej na pozycji _s_. Wtedy indeks elementu o najmniejszej wartości większej od _A[s]_ to _p+1_.

Metoda ta sprowadza koszt pamięciowy algorytmu do wartości stałej, _O_(1), wymaga jednak dodatkowego nakładu czasu na wyszukiwanie maksymalnych elementów kolejno sortowanych fragmentów tablicy. Ujmuje więc algorytmowi jego główną zaletę, wpisaną nawet w jego nazwę – szybkość działania.

```python
def quicksort(arr):
	n = len(arr)
	l = 1
	r = n
	while(true):
		if l - r < 3: # base case
			sort(arr[l:r])
			l = r+1
			r = r+2
			while arr[r] <= arr[l] and r <= n:
				r++
			if r > n:
				break
		else:
			s = partition(arr, l, r)
			m = maximum(arr, s+1, r)
			swap(arr, s, m)
			r = s-1
```