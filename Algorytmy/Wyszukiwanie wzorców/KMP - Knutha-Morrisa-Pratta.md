Problem z algorytmem naiwnym jest taki, że gdy sprawdzimy czy dany odcinek tekstu jest naszym podsłowem, to kompletnie zapominamy o tym, co przeczytaliśmy. Przez co po przesunięciu sprawdzamy wcześniej już przeczytane znaki.

Bazą algorytmu KMP jest wykonanie funkcji $\pi$, która stworzy nam tablicę długości suffixów słowa $P$, które są zgodne z prefixem $P$.

![[Screenshot 2023-05-16 at 15.19.12.png]]

Dzięki takiej tabelce, gdy napotkamy mismatch przechodząc po słowie $T$, nie musimy cofać się w słowie $T$, ponieważ wiemy czy istnieje możliwość, że słowo $P$ dopiero się zaczyna.

Przykład:

$$
T = abababd
$$
$$
P = ababd
$$

Tablica słowa $P$ wygląda następująco:
$$
0,0,1,2,0
$$

Przechodząc po słowie $T$, napotkamy mismatch przy indeksie $4$ (litera $a$ zamiast $d$). Sprawdzimy wtedy czy nie znajdujemy się obecnie na prefixie słowa $P$. Patrzymy w tabelkę słowa $P$ i widzimy, że rzeczywiście, znajdujemy się na drugiej literze prefixu $P$. Cofamy się jedynie w słowie $P$ do drugiej litery $P$ (litery $b$) i kontynuujemy podróż w słowie $T$. 

Jak widzimy, algorytm ten jest bardzo szybki. Sprawdzanie czy słowo $P$ występuje w $T$ zajmuje nam $O(n)$ czasu, ponieważ nie cofamy się w $T$ i porównujemy w czasie stałym. Przygotowanie tabeli, zajmuje nam jedynie $O(m)$ czasu. Czyli ostatecznie KMP działa w $O(m+n)$

Przygotowanie tabeli działa w czasie $O(m)$ ponieważ będziemy się cofać maksymalnie o tyle razy, o ile zbudowaliśmy najdłuższy suffix. Czyli sumaryczna ilość upadków jest równa $m$, a zatem pesymistycznie, algorytm ten będzie działał w $O(2m)=O(m)$.

Inaczej: suma długości wszystkich suffixów, równych prefixowi w $P$, jest mniejsza od $m$, ergo wewnętrzna pętla wykona się sumarycznie mniej niż $m$ razy.