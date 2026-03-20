

Costituito da $N=2^r$ nodi. Ogni nodo è identificato da una sequenza binaria da $r$ bit.

Si tratta dell'unica architettura che abbiamo visto che contiene archi diretti. Infatti per calcolare il numero degli archi partiamo dall'assunto che il grado è 2, quindi sono:
$$ 2\cdot2^r=2^{r+1} $$
La bisezione è sempre $\theta(N/logN)$ ma non la dimostriamo (ci fidiamo).

Dato un nodo $u$, abbiamo 2 archi uscenti che lo collgano a:

- $2u \mod r$
- $2u+1 \mod r$

In soldoni collego il nodo u ai nodi shiftwando verso sinistra 