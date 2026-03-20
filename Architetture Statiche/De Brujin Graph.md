
![[Pasted image 20260320112349.png]]

Costituito da $N=2^r$ nodi. Ogni nodo è identificato da una sequenza binaria da $r$ bit.

Si tratta dell'unica architettura che abbiamo visto che contiene archi diretti. Infatti per calcolare il numero degli archi partiamo dall'assunto che il grado è 2, quindi sono:
$$ 2\cdot2^r=2^{r+1} $$
La bisezione è sempre $\theta(N/logN)$ ma non la dimostriamo (ci fidiamo).

Dato un nodo $u$, abbiamo 2 archi uscenti che lo collgano a:

- $2u \mod r$
- $2u+1 \mod r$

In soldoni collego il nodo u ai nodi shiftando verso sinistra verso sinistra perdendo il bit più significativo e concateno 0 e 1.

Ad esempio il nodo 101 lo collego a: 010 e 011.

### Routing / Diametro

L'algoritmo di routing segue questa logica: 

Devo raggiungere il nodo t da s l'algoritmo è il seguente:

```
lookup(src,dst){
	if (src == dst){
		return src;
	}
	shift_sx(src)
	src = src ° topbit(dst)
	lookup(src,dst)
}
```

In pratica formo ad ogni passo la destinazione s. Questo implica che l'algoritmo è $O(r)=O(LogN)$.

Possiamo ottimizzarlo se calcoliamo il massimo prefisso della sorgente che corrisponde al massimo suffisso destinazione e utilizziamo come starting point quello













