![[Screenshot 2023-06-05 at 18.55.06.png]]

```python
def number_of_v(T):
	if T == null:
		return 0

	left_tree = number_of_v(T.left)
	right_tree = number_of_v(T.right)

	return left_tree + right_tree + 1
```

```python
def get_furthest_vs(T):
	if T == null:
		return (0, 0) # (open, closed)
	
	max_open_left, max_closed_left = get_furthest_vs(T.left)
	max_open_right, max_closed_right = get_furthest_vs(T.right)
	
	return (max(max_open_left, max_open_right)+1, max(max_closed_left, max_closed_right, max_open_left+max_open_right+1))
```