![[Screenshot 2023-06-19 at 21.22.28.png]]

Strategia adwersarza będzie opierać się na warunku:
$a_1<b_1<a_2<b_2<a_3<b_3<a_4<b_4<...<a_n<b_n$

Zapiszmy nasz ciąg jako zestaw $2n-1$ par stworzonych z sąsiadujących ze sobą elementów

$<(a_1, b_1), (b_1, a_2), (a_2, b_2)\dots, (a_k, b_k), (b_k, a_{k+1}), (a_{k+1}, b_{k+1})\dots,(a_n, b_n)>$

Mamy $3$ przypadki:

1. $i=j$ adwersarz odpowie, że $a_i<b_j$ i wyeliminuje jeden ciąg, taki w którym była zamieniana para $(a_i,b_j)$, czyli $(a_i, b_i)$

2. $i=j+1$ adwersarz odpowie, że $b_j<a_i$ i wyeliminuje jeden ciąg, taki w którym była zamieniana para $(a_i, b_j)$, czyli $(b_j, a_{j+1})$  np. $(b_1, a_2)$

3. w p. p. Nie zmniejsza to ilości zestawów/ciągów, bo $a_i$ i $b_j$ nie są w tej samej parze.

Za każdym razem pozbywamy się maksymalnie jednego ciągu.
Czyli mamy $2n-1$ swapów - porównań.