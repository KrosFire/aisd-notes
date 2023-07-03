![[Screenshot 2023-06-17 at 18.24.30.png]]

Omówione już tutaj: [[LPS - Longest Palindrom Substring]]

Tworzymy macierz $n\times n$, gdzie $n$ to długość słowa.

Przekątną wypełniamy jedynkami, a całą macierz dolnotrójkątną (lewą) uznajemy za zera.

Przechodzimy po kolejnych przekątnych w górę i uzupełniamy komórki w następujący sposób:

```python
if w[i] == w[j]:
	m[i][j] = m[i-1][j-1]+2
else:
	m[i][j] = max(m[i-1][j], m[i][j+1])
```