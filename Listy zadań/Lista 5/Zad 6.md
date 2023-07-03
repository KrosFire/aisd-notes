![[Screenshot 2023-06-20 at 15.58.12.png]]

**Wystarczy**:

Aby znaleźć największy element musimy wykonać $n-1$ porównań. Drzewa porównań, będzie mieć $\log n$ wysokości. Aby znaleźć drugi co do wielkości, musimy wrócić się do góry i wybrać największy z przegranych - $\log n - 1$ porównań.

Sumarycznie:
$n+\log n -2$

**Potrzeba**:

Wiemy, że aby stwierdzić, że element jest mniejszy od MAX2 musimy go z nim porównać lub porównać go z elementem, który wiemy, że jest mniejszy niż MAX2.  
Takich porównań będzie $n-2$.

Niech $L(x)$ oznacza liczność zbioru składającego się elementów mniejszych lub równych $x$

Po $k$ porównaniach $L(x)\le 2^k$

$L(MAX1) = n \le 2^k$ bo MAX1 jest maximum zbioru
$$
\log n \le k
$$

Sumarycznie:
$\log n + n - 2$
