Do hashowania zazwyczaj używa się tablicy, $m$ elementowej niekoniecznie proporcjonalnej do wielkości uniwersum $U$, w której zapisujemy elementy z danego $U$.

Cała zabawa polega na odpowiedniej funkcji hashującej $h: U \to \{0,1,...,m-1\}$, która określa indeks elementu z $U$ w tablicy $T$.

## Przykłady funkcji hashujących

$h(k) = k \;\mathrm{mod}\; m$

Najlepszym $m$ jest liczba pierwsza, która jest daleko od potęgi dwójki.

$h(k) = m\lfloor kA - \lfloor kA\rfloor\rfloor$

Tutaj ważnym wyborem jest $A \in (0, 1)$. Najczęściej spotykaną wartością jest $A=\frac{\sqrt{5}-1}{2}$

## Metody pamiętanie elementów

### Lista $2D$

$T[i]$ jest listą (czy też wskaźnikiem na pierwszy element listy) elementów $x$, takich że $h(x)=i$.

To sprawia, że wszystkie operacje słownikowe oprócz $SEARCH$ są w czasie $O(1)$, a $SEARCH$ jest w czasie $O(Length(T[i]))$

Przy założeniu, że każdy element z $U$ ma równą szansę trafienia do każdego z kluczy, to $SEARCH$ działa w czasie $\Theta(1+\frac{n}{m})$

**WAŻNE** $\alpha=\frac{n}{m}$ - to współczynnik wypełnienia tablicy hashującej ^165a2f

###  Zapełnianie tablicy

W tej metodzie zapisujemy w tablicy $T$ elementy z $U$, nie bawiąc się w tablice. Do tego funkcja hashująca, ma znaleźć nam wolne miejsce w tablicy $T$, aby nie wystąpił konflikt.

Dlatego funkcję $h$ musimy zdefiniować następująco:

$$
h: U \times \{0,1,...,m-1\} \to \{0,1,...,m-1\}
$$

#### Metody implementacji:

$h'$ - jedna z [[#Przykłady funkcji hashujących]]
$h_1,h_2$ - pomocnicze funkcje hashujące

1. Liniowa
		$$
	h(k,i) = {(h'(k)+i)\;\mathrm{mod}\; m}
	$$
2. Kwadratowa
		$$
	h(k,i)=( h'(k) + c_1i + c_2i^2) \;\mathrm{mod}\; m
	$$
3. Podwójna
		$$
	h(k,i)=( h_1(k) + h_2(k)i) \;\mathrm{mod}\; m
	$$

Najelepszą metodą jest metoda podwójnego hashowania. Liniowa i kwadratowa mają tendencje do preferowania jednych adresów nad drugimi, co tworzy klastry i spowalnia hashowanie.

**Ważne**

Gdy usuwamy element z tablicy (operacja $DELETE$), to wstawwiamy w usunięte miejsce flagę, mówiącą o tym, że ten adres był już użyty.

Robimy to dlatego że funkcja hashująca ma wiele wariantów wartości dla danego klucza.
Załóżmy, że szukamy klucza $D$. Idąc funkcją haszującą przechodzimy przez ciąg $A \to B \to C \to D$.
Wywalmy $B$ ze słownika. Mamy teraz $A \to$ (puste) $\to C \to D$.
Ponieważ każdy taki ciąg kończy się znakiem pustym (i nie rozróżniamy pustych pustych i pustych usuniętych), uznamy, że ten składa się tylko z A i nie odnajdziemy nigdy C i D.

#### Analiza

Załóżmy, że [[#^165a2f | wspołczynnik wypełnienia]] jest $< 1$.

Wtedy liczba prób znalezienia wolnego miejsca w tablicy hashującej wynosi:

$$
\frac{1}{1-\alpha}
$$

Czyli gdy tablica jest wypełniona w $90\%$, to znajdziemy w niej wolne miejsce w **średnio mniej niż**:
$$
\frac{1}{1-\frac{9}{10}}=\frac{1}{\frac{1}{10}}=10
$$

próbach.

Gdy zaś chcemy znaleźć jakiś element w niepustej tablicy, to zajmie nam to średnio nie więcej niż:

$$
\frac{1}{\alpha}(\ln{\frac{1}{1-\alpha}}+1)
$$

prób.

Prawdopodobieństwo wystąpienia kolizji:

Wiemy że funkcja liniowa i kwadratowa, mają tendencję do tworzenia zlepków kluczy. Gdy wstawimy więc do tablicy $n$ elementowej, $m$ elementów, to może się utworzyć $k$ zlepków. W takim razie, istnieje prawdopodobieństwo, że $m+1$ element natrafi na kolizję z prawdopodobieństwem $\frac{m}{k}$

## Rodziny uniwersalne

Aby zmniejszyć prawdopodobieństwo tego, że dla pewnych danych funkcja hashująca będzie zwracać te same wyniki, możemy wykorzystać uniwersalne funkcje hashujące. Czyli takie, które należą do rodziny uniwersalnych funkcji hashujących $H$. Z definicji musi posiadać taką własność:

$$
|\{h \in H \;:\; \forall x,y\in U;x \neq y \;\; h(x) = h(y)\}| \le \frac{|H|}{m}
$$

Czyli na ludzki: Ilość funkcji hashujących w tej rodzinie, takich które zwrócą ten sam klucz dla wszystkich danych z $U$, jest co najwyżej tyle ile ilość wszystkich funkcji w $H$ podzielona przez rozmiar tablicy hashującej.

Dzięki tej włąściwości ilość kolizji, w której bierze udział dowolny klucz, jest średnio mniejsza od $1$.

### Przykłady

1.
$m$ jest liczbą pierwszą oraz $|U| < m^{r+1}$.
$$
\forall 0 \le a \le m^{r+1}
$$
$$
h_a(x)=\sum_{i=0}^{r}a_ix_i \;\mathrm{mod}\; m
$$

2.

Niech $p$ będzie liczbą pierwszą $|U| < p$ i $m$ rozmiarem tablicy hashującej.
Dla dowolnego $a \in \mathbb{Z}_p$ (bez $0$) i $b \in \mathbb{Z}_p$

$\mathbb{Z}_p$ - to zbiór liczb całkowitych z przedziału $[0, p)$

$$
h_{ab} = ((ax+b) \;\mathrm{mod}\; p) \;\mathrm{mod}\; m
$$

### Analiza kolizij

Jaka jest szansa na to, że używając uniwersalnej funkcji hashującej, z tablicą o rozmiarze $m$, wystąpi jakiś konflikt kiedy wstawimy $n$ elementów?

Odpowiedź jest bardzo prosta. Wstawiając $n$ elementów, istnieje ${n \choose 2}$ możliwych konfliktów. Ponieważ używamy uniwersalnej funkcji hashującej, to prawdopodobieństwo wystąpięnia konfliktu wynosi średnio $\frac{1}{m}$. A zatem odpowiedzią na nasze pytanie jest:

$$
{n \choose 2}\frac{1}{m}
$$

## Słownik statyczny

Algorytm:

1. Z rodziny uniwersalnych funkcji hashujących losowo wybieramy $h$ i używamy jej do przyporządkowania $n$ kluczy, do $n$ elementowej listy kubełków.
2. Z prawdopodobieństwem $\frac{1}{2}$, zachodzi:
	$$
	\sum_{i=0}^{n-1}n_i^2 \le 4n
  $$
	Gdzie $n_i$ to ilość kluczy w $i$-tym kubełku.
3. Następnie dla każdego kubełka, który zawiera elementy, losujemy uniwersalną funkcję hashującą i używamy jej, do rozdzielenia kluczy do tablicy o rozmiarze $n_i^2$

Z prawdopodobieństwem co najmniej $\frac{1}{2}$ funkcja wybrana losowo z rodziny uniwersalnej bez-koniktowo umieszcza $n=\sqrt{m}$ kluczy w tablicy $m$ elementowej.