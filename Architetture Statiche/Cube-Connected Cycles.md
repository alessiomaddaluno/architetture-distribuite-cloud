
![[Pasted image 20260315122442.png]]

Si ottiene a partire da un ipercubo di $r$ dimensioni, sostituendo ad ogni nodo un ciclo di $r$ elementi.

Il numero di nodi è:
$N = 2^r \cdot r$

Ogni nodo ha grado 3, sappiamo che ci sono $r$ nodi per ogni $2^r$ cicli allora è molto semplice dire che: 

$3*r*2^{r-1}$

$2^{r-1}$ perché dobbiamo considerarne la metà in quanto gli archi non sono orientati.

#### Identificare un nodo
---
Ogni nodo è identificato da una coppia $(w,i)$ dove:
- $w$ è la label del ciclo (ex label del nodo)
- $i$ è la posizione all'interno del ciclo (che va da $0$ a $r-1$)
(Nell'immagine è al contrario ma vabbè)

### Connessione
---
Due nodi sono connessi se:
- Appartengono allo stesso ciclo quindi $w = w'$ e $i = i'+1 \bmod r$
- Si trovano nella stessa posizione nel ciclo, quindi $i=i'$ e differiscono nella label di $w$ solo nel bit i-esimo;

### Diametro (Routing)

Per poter raggiungere il nodo $(w',i')$ a partire da $(w,i)$ per prima cosa è necessario raggiungere il ciclo di destinazione. 