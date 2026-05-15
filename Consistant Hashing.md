Non possiamo usare la funzione hash lineare perché otterremo bilanciamento del carico ma nel momento
in cui varia n (numero di client collegati al server) allora si deve riposizionare tutto.
$$ id = ax+b \mod n$$
In un sistema P2P $n$ varia continuamente, quindi non può essere usato come parametro, inoltre non possiamo stabilire quanto vale n.

Dato un insieme di risorse $I$ 
Vogliamo una funzione $f$ che mappi 