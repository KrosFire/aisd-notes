
```python
for i in range(len(A)):
      
    # Find the minimum element in remaining 
    # unsorted array
    min_idx = i
    for j in range(i+1, len(A)):
        if A[min_idx] > A[j]:
            min_idx = j
              
    # Swap the found minimum element with 
    # the first element        
    A[i], A[min_idx] = A[min_idx], A[i]
```

Prosty algorytm sortujący, który przechodzi po kolejnych indeksach listy i znajduje najmniejszy element, a następnie go ustawia na końcu posortowanej części listy.