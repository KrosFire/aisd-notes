Zad 6 2010
$$
\begin{gathered}
T(1) = 1 \\
T(2) = 3 \\
T(n) = T(n-2) + 2n - 1 \text{ dla } n > 2 \\ \\
T(n) = T(n-2) +2n -1 = \\
T(n-2) + n + (n - 1) = \\
T(n-4) + 2(n-2) - 1 + (n + (n-1)) = \\
T(n-4) + 2n - 5 + (n + (n-1)) = \\
T(n-4) + n + (n -1) + (n-2) + (n - 3) \\
 ... \\
n\frac{n+1}{2} = O(n^2)
\end{gathered}
$$

Zad 15 2018

$T(n) = T(n^{1/2}) + O(1)$

$n = 2^k$

$T(2^k) = T(2^{k/2}) + O(1)$

$S(k) = T(2^k) = S(\frac{k}{2})+O(1)$

Master theorem:

$a = 1\; b = 2\; n = k$

$k^{\log_21} = 1 = f(x) \implies S(k) = \Theta(\log k)$ 

$k = \log n$

$\Theta(\log (\log n))$