Un grafo casuale di Gilbert denotato con G(n,p) è costituito da n vertici, dove ogni possibile arco fra due vertici è presente con probabilità p.

In questo caso non è necessario che p sia funzione di m (qualunque valore tra 0 e 1 può essere analizzato).

I grafi di Gilbert e di Eros si equivalgono se scelgo m come: 
$$ M=\binom{n}{2}p $$

Il diametro atteso è $O(log(N))$ se il grafo è connesso.

L'APL è circa log n / log k dove k = pn che rappresenta il grado medio dei nodi e segue la distribuzione di Poisson.

Il coefficiente di clustering del grafo di Gilber è circa p whp.

I grafi casuali hanno due problemi:
- Nono stante il diametro piccolo, non esiste un algoritmo di routing efficiente;
- Coefficente clustering basso (p);
- 



