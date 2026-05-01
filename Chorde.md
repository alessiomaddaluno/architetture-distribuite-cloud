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

