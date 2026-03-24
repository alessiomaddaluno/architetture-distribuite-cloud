
![[Pasted image 20260324185534.png]]


La reti P2P non strutturate di 1° e 2° generazione:
- Sono basate su TCP/IP
- I contenuti sono distribuiti in maniera casuale nella rete;
- Il trasferimento abbiene attraverso connessioni separate dirette over HTTP;

**Peer**: 
- Nodo che partecipa attivamente nella costruzione della rete di overlay;
- Fa da provider di contenuti, utilizzatore e da router della rete di overlay;

Ci sono due tipologie di richieste:
- Richiesta di contenuti (**lookup**) che non si traduce necessariamente del download;
	- Include un contatore, un TTL e un ID;
	- Solitamente basato di flooding: ogni nodo inoltra il messaggio a tutti i suoi vicini tranne quell dal quale ha ricevuto il messaggio;
	La risposta è chiamata **query-hit**: ma a differenza sua la richiesta segue il percorso all'indietro (non fa flooding)
- Messaggi di Keep-alive;


## Bootstrapping

Consiste nell'entrare nella rete P2P: è un problema non affatto banale che viene solitamente risolto usando una delle seguenti modalità:
- **Bootstrap cache**: ci si collega ad un nodo a cui si è precedente collegato;
- **Boostrap server:** utilizza una lista di well-known host;
- **Broadcast over ip**: Usa tecniche di broadcast, non applicabile su rete internet. Possibile su rete locale (in certe condizioni);
