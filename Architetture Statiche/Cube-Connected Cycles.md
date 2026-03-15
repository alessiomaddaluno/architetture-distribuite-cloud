
![[Pasted image 20260315122442.png]]

Si ottiene a partire da un ipercubo di $r$ dimensioni, sostituendo ad ogni nodo un ciclo di $r$ elementi.

Il numero di nodi è:
$N = 2^r \cdot r$

Ogni nodo ha grado 3, 

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

