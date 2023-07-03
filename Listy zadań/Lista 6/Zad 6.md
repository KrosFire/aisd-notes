![[Screenshot 2023-06-20 at 17.59.29.png]]

Weźmy dwa drzewa BST: $T1$ i $T2$ przechowujące te same wartości.

Porównajmy ich korzenie. Jeśli są różne powiedzmy: $T1.root < T2.root$ to oznacza, że wartość korzenia $T1$ znajduje się w lewym poddrzewie $T2$.

Znajdźmy więc ten wierzchołek w lewym poddrzewie $T2$. Jeśli wierzchołek ten jest lewym dzieckiem, to rotacja w lewo wyniesie go do góry, jednocześnie nie zaburzając porządku. Analogicznie dla prawej strony.

Po wykonaniu odpowiedniej ilości rotacji, wierzchołek ten stanie się korzeniem $T2$. Oznacza to, że korzenie $T1$ i $T2$ są te same oraz elementy w ich lewych i prawych poddrzewach, ponieważ wciąż są to drzewa BST.

Możemy się teraz wykonać rekurencyjnie na lewym i prawym poddrzewie $T1$ i $T2$ wykonując te same kroki co dla korzeni. Tym sposobem uzyskamy te same drzewa.

Dowodzi to, że dowolne drzewo BST, możemy przekształcić za pomocą jedynie rotacji w inne drzewo BST.