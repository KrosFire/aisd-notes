Pierwszy leksykograficznie porządek topologiczny
![[Screenshot 2023-06-15 at 16.16.08.png]]

```python
def leksy_top_sort(V):
	p_queue = make_heap([])
	sorted_v = []
	
	for v in V:
		if in_degree(v) == 0:
			p_queue.push(v)
	
	while not p_queue.is_empty():
		v = p_queue.delete_min()
		sorted_v.push(v)
		for u in neighbours(v):
			delete_edge((v, u), u)
			if in_degree(u) == 0:
				p_queue.push(u)
	
	return sorted_v
```

Złożoność: $O(|V|\log|V|)$

