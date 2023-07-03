![[Screenshot 2023-06-05 at 19.10.32.png]]

Niech kopiec min-max będzie zdefiniowany następująco:

Elementy kopca MAX, będą znajdować się na nie parzystych indeksach (zaczynając od $1$), a kopca MIN, na parzystych.

Przez co, dziećmi elementu kopca MAX o indeksie $i$ będą: $2i+1$ oraz $2i+3$
A dziećmi elementu kopca MIN o indeksie $i$ będą: $2i$ oraz $2i+2$

```python
def delete_min(H):
	n = len(H)
	min = H[2]
	H[2] = H[n]
	sift_down(2, H)
```

```python
def delete_max(H):
	n = len(H)
	min = H[1]
	H[1] = H[n]
	sift_down(1, H)
```

```python
def sift_down(index, H):
	n = len(H)
	is_min_level = index % 2 == 0
	
	if 2*index+is_min_level > n
		return
	
	if is_min_level:
		min_of_children = 2*index if H[2*index] < H[2*index+2] else 2*index+2
		if H[index] > H[min_of_children]:
			swap(H[index], H[min_of_children])
			sift_down(min_of_children, H)
	else:
		# analogicznie
```

```python
def sift_up(index, H):
	n = len(H)
	is_min_level = index % 2 == 0
	
	if (index / 2) - ((index/2) % 2) == 1 and is_min_level:
		return
	elif not is_min_level and index == 1:
		return
		
	if is_min_level:
		parent = (index / 2) - ((index/2) % 2)
		
```

----------

Druga wersja

Niech kopiec min-max będzie zdefiniowany następująco:

Elementy kopca MIN, będą znajdować się na nie parzystych poziomach (zaczynając od korzenia $1$), a kopca MAX, na parzystych.

```python
def delete_min(H):
	n = len(H)
	H[1] = H[n]
	delete H[n]
	sift_down(1, H)
```

```python
def delete_max(H):
	n = len(H)
	max_index = 2 if H[2] > H[3] else 3
	H[max_index] = H[n]
	delete H[n]
	sift_down(max_index, H)
```

```python
def sift_down(index, H):
	n = len(H)
	is_min_level = index % 2 == 1

	if is_min_level:
		min_granchild = min_index(grandchildren(index))
		if H[min_granchild] < H[index]:
			swap(min_granchild, index)
			sift_down(min_grandchild, H)
	else:
		# analogicznie
```