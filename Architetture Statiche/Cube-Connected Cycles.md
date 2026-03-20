
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

Per poter raggiungere il nodo $t$ a partire da $s$ per prima cosa è necessario raggiungere il ciclo di destinazione.

![[Pasted image 20260315130341.png]]

Per farlo partiamo da comparare il bit nella posizione k (Cioè quello nella posizione del ciclo). Se è diverso si segue l'arco dell'ipercubo. Successivamente si sposto anche sull'arco del ciclo.

Il motivo per cui parto da quello è che così posso subito spostarmi e non mi devo muovere nel ciclo di nuovo.

La complessità dell'algoritmo è 
$2\cdot r\cdot+r/2 = O(r) = O(logN)$

### Bisezione

Sempre lo stesso conto. 
La bisettrice è $2^r=N/r=N/log(N)$



