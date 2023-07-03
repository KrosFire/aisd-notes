![[Screenshot 2023-06-17 at 15.49.18.png]]

Algorytm jest następujący:

Na początku odkrywamy wartości w korzeniu i lewym dziecku.

Jeśli wartość lewego dziecka jest mniejsza od wartości korzenia, to rekurencyjnie schodzimy do lewego poddrzewa.

W p. p. schodzimy do prawego poddrzewa, lecz nie odkrywamy wartości w korzeniu tego poddrzewa.

Ostatecznie otrzymamy siatkę wierzchołków odkrytych i nieodkrytych. Będziemy dzięki temu wstanie wyizolować najmniejszy z odkrytych elementów w sąsiedztwie i następnie odkryć dwa nieodkryte dotychczas wierzchołki, znajdujące się obok najmniejszego z odkrytych, aby znaleźć minimum lokalne.

Ilustracja:

![[IMG_0208.jpeg]]