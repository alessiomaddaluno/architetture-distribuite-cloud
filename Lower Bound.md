
### Teorema (bound di Moore)

**Lemma**
Dato un grafo $G = (V,E)$ con $|V|$ (Numero di Nodi) uguale a $N$ e grado $k = O(logN)$, allora il diametro è $l = \Omega(logn/log(logN)$

(Possiamo un attimo semplificarlo dimostrando il tutto con un generico grado k.)

**Dimostrazione**
Proviamo a costruire un albero dal momento che ogni nodo ha grado k.  Ogni nodo quanti nodi può raggiungere? (Ci stiamo chiedendo da quanti nodi è composto l'albero).  

Dal momento che l'albero ha altezza $l$ (che è il diametro) sappiamo che il numero totale di nodi deve essere:
$$ 
\sum_{i=0}^{l} k^i = \frac{k^{l+1}-1}{k-1} < k^{l+1}
$$
Da notare che la sommatoria si risolve matematicamente con quella quantità, ma possiamo applicare un upper bound a tale quantità, ovvero $k^{l+1}$. Dal momento che il grafo è necessariamente connesso allora abbiamo che:
$$
k^{l+1} > N 
$$
$$
l+1 > log_kN 
$$
$$
l > log_kN = \Omega(logN/log(logN))
$$

### Lower Bound sistemi uniformi
Il lower bound può essere ancora più stringente nel caso di sistemi uniformi, ovvero: dato una rete P2P con N nodi e di grado K allora il diametro della rete è $\Omega(logN)$ se $k=\Omega(logN)$

(Se volessimo essere ancora più precisi dovremo dire che è 1/2 logN)

