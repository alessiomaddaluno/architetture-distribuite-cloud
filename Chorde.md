Creiamo un anello nel quale inserire i nostri peer e poi creiamo delle corde nell’anello in maniera efficace, garantendo la possibilità di raggiungere tutti i punti con un algortimo decentralizzato. Quello che ricerchiamo è il bilanciamento del carico, ovvero vogliamo essere equilibrati nell'assegnazione delle risorse ai nodi.


![[Pasted image 20260501113749.png]]

### Consistent Hashing
L'architettura è basata su $2^m$ identificatori dove $m$ è il numero di bit che costituiscono l'identificatore (di solito 160). Utilizza un algoritmo di hash che garantisce la distribuzione delle chiavi e permette il bilanciamento del carico sui nodi (con n nodi e k risorse), ogni nodo gestisce circa $\frac{(1+\epsilon)k}{n}$ risorse dove $\epsilon$ è nell'ordine di $O(logn)$.

Anche le risorse sono mappate sull'anello e una risorsa (chiave) viene assegnata al **primo nodo con ID ≥ chiave**, andando in senso circolare.

### Lookup 
Chord fornisce una sola API, chiamata Lookup, prende un identificatore (160 bit) e restituisce un IP address.
Il nodo deve fare due cose o risponderci o fornirci un IP di un nodo che ne sa più di lui.

Ogni nodo ha un link verso:
- $logn$ successori;
- 1 predecessore;
- $m$ fingers, whp $O(logn)$ 
	- I possibili m fingers hanno id = $u+2^{i-1}$

In totale mantiene dunque $logn + 1 + O(logn) = O(logn)$ link verso altri nodi.

![[Pasted image 20260501114706.png]]

### Algoritmo di Lookup

![[Pasted image 20260501120245.png]]

### Teorema per la distribuzione degli id

**Lemma**:
Dato un qualunque intervallo di ampiezza $2^{m}/N$, il numero di ID
di nodi atteso in questo intervallo è 1 in media e **O(log N)**
w.h.p.

Quindi ci sta dicendo sostanzialmente che gli ID dei nodi sono distribuiti “quasi uniformemente” sull’anello.

**Dimostrazione**:

Per dimostrarlo abbiamo prima bisogno di definire il **Chernoff Bound**:

Se ci troviamo difronte a un esperimento, per il quale facciamo $N$ prove, ogni prova ha una probabilità di successo $p_i$ e probabilità di insuccessi $1-p_i$, allora la media dei successi è la
somma delle $p_i$, e la probabilità di discostarsi di un fattore δ (delta) rispetto alla media ($\mu$), è minore di questa quantità:

![[Pasted image 20260501123412.png]]

Se δ > 4, la funzione possiamo scriverla anche nel seguente modo:
![[Pasted image 20260501123330.png]]

Tale quantità rappresenta un upperbound del fenomeno.

Ritornando a chorde il fenomeno è modellato come se i nodi fossero delle biglie e le sezioni del cerchio come contenitori.

**Se consideriamo una fetta, la probabilità che il nodo cada in quella fetta è $1/n$ se ripetiamo l'esperimento $n$ volte in media sarà 1.**

La probabilità che la media sia $klogn$  (che è come scrivere $O(logn)$ da quale relazione è delimitata? 

Per capirlo dobbiamo vedere quanto vale $δ$ :

$$(1+δ)\mu = klogN$$

La media $\mu$ è 1, quindi:

$$(1+δ) = klogN$$

Se lo sostituiamo alla formula:

$$2^{-\mu(1+\delta)}$$

otteniamo:

$$2^{-klogN} = \frac{1}{2^{klogN}}$$
  
Per la proprietà dei logaritmi:
$$ \frac{1}{n^k}$$
