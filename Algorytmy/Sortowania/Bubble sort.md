Prosty algorytm sortujący, który porównuje i zamienia pary obok siebie, do momentu posortowania

```python
def bubble_sort(arr):
	while true:
		swapped = False
		i = 0
		
		while i < len(arr)-1:
			if arr[i] > arr[i+1]:
				swap(arr[i], arr[i+1])
				swapped = True
		
		if not swapped:
			break
	
	return arr
		
```