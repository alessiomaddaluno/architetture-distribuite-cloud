![[Pasted image 20260313164111.png|554]]

La Butterfly è una variante dell'ipercubo. Considrando la dimensione $r$ è costituita da $2^r$ righe e $r+1$ colonne. Ne consegue che ha:

- $2^r\cdot (r+1)$  nodi;
- Gli archi sono $r*2^{r+1}$ perché:
	- $r$ perché l’ultima colonna non ha archi uscenti;
	- 2 perché ogni nodo ha 2 archi _uscenti_;
	- $2^r$ numero di righe
	$2\cdot2^r\cdot r=r\cdot2^{r+1}$

 Ogni nodo è identificato da una coppia (w,i) dove:
 - w = label della riga 
 - i = numero di colonna

Due nodi $u$ e $u'$  sono connessi se:
- $i=i'$ (Si trovano su colonne successiva)
- $w=w'$ (arco diretto) oppure:
	- $w$ e $w'$ differiscono all'i-esimo bit (arco incrociato)

Algoritmo di routing:

Fase 1: Andra a sinistra finché si può, impiega al più $r$ passi;
Fase 2: Guardo l'etichetta e se l'i-esimo bit differisce allora seguo l'arco incrociato altrimenti quello diretto. Impiego al più $r$ passi;
Fase 3: A questo punto mi trovo sulla riga corretta, mi movo a sinistra per ritrovarmi anche sulla stessa colonna;

$r+r+r = 3\cdot r = \theta(logN)$

Bisezione:

Partiamo dal numero dei nodi: $2^r\cdot(r+1)$

Per ottenerla dobbiamo tagliare gli archi orizzontali tra due livelli che sono $2^r$

Quindi:

$B=2^r=N/(r+1)$  (Praticamente lo scrivo rispetto ad N e per farlo moltiplico e divido per r+1)

Il denominatore è r che posso scrivere come LogN quindi $r+1=O(logN)$

quindi $B = (N/logN)$




