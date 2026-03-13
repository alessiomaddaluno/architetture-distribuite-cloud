![[Pasted image 20260313182359.png]]

Rete che offre dei path di backup.

Si ottiene facendo un merge di due butterfly back to back, infatti i nodi sono:
### Nodi
$N=2^r\cdot2r+1$  (Ricordiamoci che l'ultima colonna non ha archi uscenti per questo +1 e non +2!)
### Archi
Per il numero di archi, analogamente alla Butterfly:

Si parte da $2r$ perchè l'ultima colonna non ha archi uscenti moltiplicato il numero di colonne $2^r$ moltiplicato per 2 perché gli archi uscenti sono 2 per ogni nodo che può averne;

$$2\cdot2r\cdot2^r = 2r\cdot2^{r+1} $$
### Diametro

Il diametro segue lo stesso algoritmo della butterfly normale, con i medesimi ragionamenti quindi ne segue che è $\theta(logN)$

### Bisezione

Nono stante dobbiamo tagliare il doppio degli archi rispetto alla butterfly, asintoticamente non cambia:

$$
N=2^r\cdot2r+1
$$
$$
B=2\cdot2^r= 2\cdot N/(2r+1)= \theta(N/logN)
$$


