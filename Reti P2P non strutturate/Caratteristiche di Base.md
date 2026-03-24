
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
- **Bootstrap cache**: assumendo che la prima volta riusciamo ad ottenere una connessione, possiamomantenere una cache e le volte successive possiamo usare la cache per vedere se un nodo con cuiabbiamo interagito in passato è accessibile nella rete.
- **Bootstrap server**: ci si connette un host che è sempre nella rete, ma non ci piace usare un serverpoiché basta spegnerlo per far cadere la rete, in generale si chiede al server l’indirizzo di un nodonella rete.
- **Bootstrap on the IP layer**: usa multicast chanel, e uso di broadcast IP (onerosi e sempre se a rete ciperette di usare il broadcast IP, solitamente è limitato).
