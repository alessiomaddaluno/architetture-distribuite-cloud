![[Pasted image 20260324190454.png|432]]

Tutti i peer sono collegati ad un'unità centrale il cui unico compito è quello di fare la lookup (in sostanza è una specie di database).

Il central server fa anche da boostrapping server (essendo well-known).

Chiaramente è un single point of failure della rete e rappresenta un collo di bottiglia dal momento che tutte le richieste di lookup sono fatte verso tale server.

La comunicazione Peer <-> Server avviene per:
- Richiedere un contenuto;
- Accedere/Registrarsi alla rete;
- Aggiornare le informazioni in merito ai contenuti condivisi;

Lo scambio Peer <-> Peer è effettuato solo per lo scambio dei dati (della risorsa vera a propria).

Un esempio è **Napster** :

