G(n,m) è un grafo scelto casualmente nell‘insieme G(n,m) di tutti i grafi con esattamente n vertice e m archi.

**Ha senso studiare il grafo solo se m è funzione di n**

In base a come si sceglie m il grafo avrà $whp$ le seguenti caretteristiche:

- G(n,m) ha una componente connessa O(n) whp se m è maggiore di n/2 (c’è un arco per ogni vertice);
- G(n,m) è connesso whp se m è maggiore di n log n. (cioè è connesso se ogni nodo ha circa log n archi) e il diametro atteso è O(log n);