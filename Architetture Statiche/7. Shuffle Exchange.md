![[Pasted image 20260315155654.png]]

La rete ha numero di nodi proporzionali a $r$ , infatti ha:
$2^r$ nodi e quindi ogni nodo è identificato da una sequenza di bit.

Il grado dei nodi è costante e massimo 3:
tecnicamente è < $3\cdot2^{r-1}$

La particolarità risiede nei due tipi di archi (connessioni) che definiscono la topologia:
  - **Archi di Exchange** (quelli tratteggiati) : collegano due nodi che differiscono nell'ultimo bit. ES: 000 - 001 // 101-100
  - **Archi di Shuffle**: che collegano un nodo a quello che si ottiene shiftando 1 bit a destro o sinistra. Ad esempio: 110 , lo collego a 011 e 101

La bisezione è sempre $\theta(N/logN)$ ma non la dimostriamo, ci fidiamo.

### Routing (Diametro)
----
Supponiamo di voler passare dal nodo $s$ al nodo $t$

L'algoritmo è :

```
current = s;
for (i = r-1 to 0){
	if(current_i != t_i)
		current = exchange(current)
	current = shuffle(current)
}
```

La complessita è $2r = \theta(logN)$










