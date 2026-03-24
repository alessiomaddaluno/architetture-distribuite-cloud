![[Pasted image 20260324231001.png]]

Ogni entità sono solo peer, non è presente alcuna componente centralizzata. Le connessioni vengono instaurate randomicamente (PING / PONG). Il modo di comunicare è il flooding e vengono inviati numerosi messaggi di keep-alive, il motivo è che un nodo non può permettersi di isolarsi altrimenti non fa più parte della rete p2p.

Per la parte di bootstrapping o si procede con cache o di well-known host. 
Non essendoci una componente centralizzata di lookup il routing è effettuato attraverso il flooding per poi effettuare la back-route in caso troviamo il file.

## Esempio: Gnutella 0.4

C’è latenza a causa del flooding, poiché poteva capitare di passare per peer lontani dal nodo sorgente per poi tornare indietro (Zig Zag).

**Funzionamento**:
**connessione** ad almeno un peer già connesso alla rete, **esplorazione** del vicinato
(tramite messaggi **PING** e risposte **PONG** per avere più connessioni da mantenere), query si invia una richiesta a tutti i vicini contenete una serie di keyword ed alcuni requirment, **select**: si scelgono le migliori risposte, download: ci si connette ai peer che dispongono la risorsa richiesta.

Una volta inviata la query non è più possibile fermarla, si controlla solo numero degli hop e TTL se non sono uguali fa il foreword.

**Vantaggi**: non c’è un singolo punto da attaccare, forniscono anonimia, permettono la creazione di gruppi diinteresse. Rete resiliente.
**Svantaggi**: possibile congestione della rete dovuta alla grosse mole di messaggi, peer poco efficienti possono rappresentare un collo di bottiglia, sono possibili rotte di tipo zigzag, rete di overlay non ottimale (non esiste vista completa della rete, non esiste coordinatore)