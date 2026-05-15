Non possiamo usare la funzione hash lineare perché otterremo bilanciamento del carico ma nel momento
in cui varia n (numero di client collegati al server) allora si deve riposizionare tutto.
$$ id = ax+b \mod n$$
In un sistema P2P $n$ varia continuamente, quindi non può essere usato come parametro, inoltre non possiamo stabilire quanto vale n.
Dato un insieme di risorse $I$ (ovvero i dati che vogliamo mappare) e $B$ l'insieme degli identificatori, il numero possibile di configurazione è $2^B$. 

Vogliamo una funzione $f$ che mappi a partire da una configurazione un id su un nodo attivo.

Questa funzione ricerca le seguenti proprietà:

- **Bilanciamento** : Se il numero di ist 