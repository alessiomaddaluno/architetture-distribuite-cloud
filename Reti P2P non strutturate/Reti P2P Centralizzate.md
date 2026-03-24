![[Pasted image 20260324190454.png|432]]

Tutti i peer sono collegati ad un'unità centrale il cui unico compito è quello di fare la lookup (in sostanza è una specie di database).

Il central server fa anche da boostrapping server (essendo well-known).

Chiaramente è un single point of failure della rete e rappresenta un collo di bottiglia dal momento che tutte le richieste di lookup sono fatte verso tale server.

La comunicazione Peer <-> Server avviene per:
- Richiedere un contenuto;
- Accedere/Registrarsi alla rete;
- Aggiornare le informazioni in merito ai contenuti condivisi;

Lo scambio Peer <-> Peer è effettuato solo per lo scambio dei dati (della risorsa vera a propria).
## Esempio: Napster

Fornisce 4 operazioni:
- **PUSH** - Caricamento della lista dei file condivisa sul Server
- **QUERY** - Si invia una richiesta al Server contenente una serie di keyword ed alcuni requirement
- **SELECT** - Si scelgono le migliori risposte
- **DOWNLOAD** - Ci si connette ai peer che dispongono della risorsa richiesta


È possibile fare qualsiasi operazione in soli 5 passaggi:  Connessione al server (autenticazione), Push dei propri contenuti, Query per il file ricercato, Select dalle risposte del server (Ricordiamoci che il server invia un messaggio per singola entry), e Download per scaricare il file direttamente con il Peer.

**Svantaggi**: facili da attaccare poiché il server rappresenta l’anello debole e un collo di bottiglia per il sistema a causa delle lookup, nessun incentivo a collaborare.
**Vantaggi**: veloce, non sono necessari messaggi di keep-alive, un’unica autorità fidata che gestisce il database.

