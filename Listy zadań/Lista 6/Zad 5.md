![[Screenshot 2023-06-20 at 17.34.38.png]]

Chcemy stworzyć kolejkę priorytetową, czyli taką, w której rodzic ma większą wartość od każdego z jego dzieci. Dodatkowym wymogiem jest to, aby najkrótsza ścieżka z liści w lewym poddrzewie, była conajmniej tak długa, jak najkrótsza ścieżka z liści w prawym poddrzewie.

Innymi słowy, wszystkie gałęzie lewego poddrzewa, są conajmniej tak duże jak gałęzie prawego poddrzewa.

Musimy obsługiwać operację:

_DeleteMax()_

_Find(x)_

_Insert(x)_

_Find(x)_ jest trywialny.

_DeleteMax()_ wykonamy poprzez rozdzielenie dzieci korzenia na dwa drzewa, które scalimy i zwrócimy wartość w korzeniu.

_Insert(x)_ dokonamy ten sam trick, czyli stworzymy wierzchołek z wartością $x$ i scalimy z główny, drzewem.

Problemem jest oczywiście operacja scalania. Będzie ono dokonywane w następujący sposób:

```python
def merge(T1, T2):
	if T1 is None:
		return T2
	if T2 is None:
		return T1

	if T1.root > T2.root:
		merge(T1.right, T2)
		if T1.left.height < T1.right.height:
			swap_children(T1)
		return T1
	else:
		merge(T2.right, T1)
		if T2.left.height < T2.right.height:
			swap_children(T2)
		return T2	
```

Dzięki priorytetyzowaniu scalania w prawą stronę, balansujemy drzewo. Musimy oczywiście sprawdzić zawsze, czy czasem nie przerzuciliśmy za dużo wierzchołków na prawą stronę i tym samym zaburzyliśmy porządek.