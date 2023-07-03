Jest to algorytm, który działa podobnie do algorytmu naiwnego, ale wykorzystuje parę fajnych sztuczek, aby zaoszczędzić sobie pracy. W algorytmie BM porównujemy wzór z tekstem od końca.

Algorytm ten posiada **2 zasady**:

1. Gdy podczas porównania, natrafimy na mismatch, przesuwamy wzór w prawo tak długo, aż znajdziemy match i dopiero wtedy porównujemy z powrotem
2. Porównując wzór z tekstem, czasami uda nam się stworzyć suffix, który pasuje do wzoru. Czyli posiadamy wiedzę jaki suffix jest w tekście. Możemy więc wyszukać najdłuższy suffix tego suffixa we wzorze i o tyle przesunąć ten wzór, aby ponownie spinał się z tekstem.

Algorytm BM działa w bardzo prosty sposób. Używa tej heurystyki, która pominie najwięcej porównań.
Przykład:

![[Screenshot 2023-05-26 at 21.15.18.png]]