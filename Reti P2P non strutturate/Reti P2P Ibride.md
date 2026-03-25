![[Pasted image 20260325181844.png]]

Sistema basato su due layer: peer e superpeer; possiamo considerare la rete come un insieme du hub connessi tra di loro. 

**Peer**: si connettono a uno o più Superpeer (grado < 7) mentre i **superpeer** hanno grado alto (>>20) e sono scelti per elezione o volontà.

Il bootstrapping abbiene con boostrap-server cache. La registrazione è necessaria: ogni peer si registra presso un superpeer e annuncia la lista dei file da condividere.

Il routing è parzialmente decentralizzato, il peer invia la richiesta ad un superpeer. Il super pper risolve la richiesta come se fosse un proxy.

**Esempio**: Gnutella 0.6 

Gnutella organizza i nodi in un sistema gerarchico a 2 livelli in cui i nodi ad alta capacità chiamati Hub rispondono alle richieste delle componenti foglie (peer). Per evitare che si centralizzi troppo gli Hub hanno un grado massimo fissato (uguale a a 150). 

La comunicazione tra foglie e hub è diretta ma è presente 
