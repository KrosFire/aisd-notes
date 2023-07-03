3 możliwe złożoności wynikające ze wzoru:

1.  $f(n) = O(n^{\log_ba-\epsilon}) \implies T(n) = \Theta(n^{\log_ba})$
2.  $f(n) = \Theta(n^{\log_ba}) \implies T(n) = \Theta(n^{\log_ba}\cdot \log{n})$
3.  $f(n) = \Omega(n^{log_ba+\epsilon}) \implies T(n) = \Theta(f(n))$

Gdzie $\epsilon>0$ jest pewną stałą.