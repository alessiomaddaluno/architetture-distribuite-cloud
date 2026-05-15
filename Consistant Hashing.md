Non possiamo usare la funzione hash lineare perché otterremo bilanciamento del carico ma nel momento
in cui varia n (numero di client collegati al server) allora si deve riposizionare tutto.
$$ id = ax+b \mod n$$
In un sistema P2P $n$ varia continuamente, quindi non può essere usato come parametro, inoltre non possiamo stabilire quanto vale n.
Dato un insieme di risorse $I$ (ovvero i dati che vogliamo mappare) e $B$ l'insieme degli identificatori, il numero possibile di configurazione è $2^B$. 

Vogliamo una funzione $f$ che mappi a partire da una configurazione un id su un nodo attivo.

Questa funzione ricerca le seguenti proprietà:

- **Bilanciamento** : Preso il numero di posizioni attive V e l'insieme dei dati I, i nodi devono avere in media $O(I/V)$;
- **Monotonicità**: Abbiamo un sistema con un certo numero V di nodi e supponiamo di aggiungere altri nodi al sistema. Le risorse devono migrare a partire dai nodi vecchi verso i nodi nuovi;
- **Spread**: Al variare di n, il numero di posizioni che un dato può assumere è limitato
- **Carico**: Al variare di n, il numero di dati che una posizione accoglie è limitato