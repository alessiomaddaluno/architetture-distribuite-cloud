
![[Pasted image 20260313155650.png]]

Data la dimensione $r$ , l'ipercubo ha:
- $N = 2^r$ nodi;
- $r\cdot2^{r-1}$ archi 

Ogni nodo è etichettato in $r$ bit.
Due nodi sono connessi se la loro etichetta differisce di un solo bit. 

Il grado di un nodo è $r$ nonché $logN$ .

**Diametro** 
$$ r = logN $$
Ricordiamoci che il diametro la possiamo vedere come la distanza massima tra due nodi. Nel nostro caso possiamo vedere la distanza di Hamming che può essere alpiù r. Infatti l'algoritmo di routing è abbasta semplice:

Date due qualsiasi codifiche binarie $u$ e $v$ possiamo passare da una all'altra al più in $r$ passi:

```
	for i=0 to r:
		if u_i != v_i:
			attraversa l'arco di dimensione i
```

Dove attraversa l'arco di dimensione r significa attraversare l'arco che modifica il bit all'i-esima posizione;

**Bisezione**

Il **numero minimo di archi da tagliare** per dividere la rete in **due metà con lo stesso numero di nodi**.

In questo caso basta eliminare tutti gli archi lungo una generica dimensione k, ovvero fisso k e divido i nodi i due gruppi (tutti quelli con 0 e 1). Quanti archi devo tagliare? Sicuramente almeno 1 per nodo. Considerando che gli archi non sono orientati allora avrò che la bisezione è $N/2$.

Lo svantaggio principale dell'ipercubo è il gradi non costante da qui lo sviluppo di varianti.