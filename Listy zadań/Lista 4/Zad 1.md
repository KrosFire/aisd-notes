![[Screenshot 2023-06-17 at 18.11.15.png]]

Proste dynamiczne programowanie:

Wypełniamy pierwszą kolumnę

Potem dla każdej kolejnej, wypełniamy ją od góry do dołu, patrząc na wartości z góry i z poprzedniej kolumny.

Następnie musmy jeszcze raz się przez nią przejść, tym razem od dołu i zaktualizować wagi biorą pod uwagę ruch z dołu na górę.

Wynik będzie w komórce o najmniejszej wartości w ostatniej kolumnie.

Algorytm:

```python
def fill_matrix(M, start_col, end_col):
	dp = matrix_of_dim(M)
	col = start_col
	while col <= end_col:
		for row in M.rows():
			if col == start_col:
				dp[col][row] = M[col][row]
			else:
				dp[col][row] = M[col][row] + min(dp[col][row-1], dp[col-1][row], dp[col-1][row+1], dp[col-1][row-1])
		if col > start_col:
			for row in M.rows():
				dp[col][row] = min(dp[col][row], M[col][row] + dp[col][row+1])
	path = [index_of_min(dp[end_col])]
	while col > start_col:
		cost = dp(path[-1]) - M(path[-1])
		path.append(element_of_cost(dp, cost))
	return path
```
