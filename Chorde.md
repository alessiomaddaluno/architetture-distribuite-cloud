Creiamo un anello nel quale inserire i nostri peer e poi creiamo delle corde nell’anello in maniera efficace, garantendo la possibilità di raggiungere tutti i punti con un algortimo decentralizzato. Quello che ricerchiamo è il bilanciamento del carico, ovvero vogliamo essere equilibrati nell'assegnazione delle risorse ai nodi.
### Lookup 
Chord fornisce una sola API, chiamata Lookup, prende un identificatore (160 bit) e restituisce un IP address.
Il nodo deve fare due cose o risponderci o fornirci un IP di un nodo che ne sa più di lui.
L’assegnazione di ID è fatto con SHA, non invertibile, non è possibile per un nodo sapere il suo identificatore. SHA bilancia bene lo spazio delle chiavi, quindi già grazie a questo avremo una equa
distribuzione delle risorse.

### Consistent Hashing
