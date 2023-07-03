![[Screenshot 2023-06-21 at 15.32.29.png]]

Będzie to drzewo AVL, a więc drzewo BST zbalansowane.

Gdy będziemy chcieli znaleźć $min\_diff$ wykonamy następującą operację w czasie $O(\log n)$

```python
def min_dif(T):
	if T.left == T.right == None:
		return +inf
	return min(min_diff(T.left), min_diff(T.right), T.root.value-max_val(T.left), min_val(T.right)-T.root.value)
```

Dobrym rozwiązaniem jest również [drzewo przedziałowe](https://en.wikipedia.org/wiki/Interval_tree), którego nie mam pokrytego w notatkach.

Drzewo to ma wiele nazw: Interval tree, range tree, segment trees. Tutaj miły Pan Hindus opowiada:

https://www.youtube.com/watch?v=ZBHKZF5w4YU
