## Koorde

Koorde è un protocollo chord-like che combina l'anello di Chord con il routing dei grafi di de Bruijn, ottenendo APL $O(\log n)$ con grado costante, oppure APL $O(\log n / \log \log n)$ con grado $O(\log n)$.

### Grafo di de Bruijn

Prima di capire Koorde è necessario capire il grafo di de Bruijn. Un grafo di de Bruijn con $b$ bit ha un nodo per ogni numero binario di $b$ bit, quindi $2^b$ nodi totali. Ogni nodo $m$ ha esattamente due archi uscenti verso i nodi $2m \mod 2^b$ e $2m+1 \mod 2^b$, che corrispondono allo shift a sinistra di $m$ con l'aggiunta di 0 oppure 1. Il diametro è $b = \log n$ con grado 2.

Il routing nel de Bruijn è semplice: per andare dal nodo $s = (s_0, s_1, \ldots, s_{b-1})$ al nodo $t = (t_0, t_1, \ldots, t_{b-1})$, ad ogni passo si calcola $t = m \circ \text{topbit}(ks)$, ovvero si shiftano a sinistra i bit di $m$ eliminando il MSB e si appende il bit più significativo di $ks$. Dopo $b$ passi si sono sostituiti tutti i bit di $m$ con i bit di $t$.

Il problema è che il de Bruijn richiede che tutti i $2^b$ nodi esistano. Con $b = 160$ (SHA) servirebbero $2^{160}$ nodi, ma nella realtà ci sono solo $n$ nodi reali.

### Struttura di Koorde

Koorde mantiene l'anello di Chord con consistent hashing e aggiunge due link per ogni nodo:

- un **link verde** al successore nell'anello
- un **link giallo** al predecessore di $2m \mod 2^b$ nell'anello reale

Il nodo $2m \mod 2^b$ è un nodo immaginario de Bruijn che quasi certamente non esiste nell'anello reale. Si punta quindi al suo predecessore reale, cioè il primo nodo reale che viene prima di $2m \mod 2^b$ sull'anello. Non serve un link separato per il predecessore di $2m+1 \mod 2^b$ perché quel nodo è raggiungibile tramite i successor pointer a partire dal predecessore di $2m \mod 2^b$: $2m$ e $2m+1$ sono adiacenti nello spazio degli ID.

Il grado totale è quindi **2**, costante e indipendente da $n$.

### Algoritmo di routing

```
m.lookup(k, ks, i)
1. if k ∈ (m, m.successor]  →  return successor
2. else if i ∈ (m, m.successor]
3.     return d.lookup(k, ks<<1, i◦topbit(ks))
4. else
5.     return m.successor.lookup(k, ks, i)
```

dove `k` è la destinazione, `ks` sono i bit rimanenti di `k` da consumare (inizializzato a `k`), `i` è il nodo immaginario de Bruijn corrente (inizializzato a `m`) e `d` è il link giallo al predecessore di $2m \mod 2^b$.

Il parametro `i` è un cursore nel grafo de Bruijn immaginario: avanza di un passo ogni volta che si esegue il passo 3, mentre nell'anello reale ci si avvicina ad esso con i successor pointer.

Il routing alterna due fasi:

**Fase verde (passo 5)**: il nodo immaginario `i` non cade ancora nella zona $(m, \text{successor}]$, quindi non si è ancora il predecessore di `i`. Si passa la lookup al successore tenendo `i` invariato, avanzando sull'anello verso il predecessore di `i`.

**Fase gialla (passo 3)**: si è il predecessore di `i`. Si usa il link giallo per saltare al predecessore di $2m \mod 2^b$, e il nuovo nodo immaginario diventa $i \circ \text{topbit}(ks)$: si è consumato un bit di `ks` e `i` ha avanzato di un hop nel de Bruijn.

Il passo 1 termina la lookup quando la destinazione `k` cade nella zona del nodo corrente.

### Complessità

Il passo 3 viene eseguito al massimo $b$ volte. Per ogni hop de Bruijn (freccia gialla), quante frecce verdi servono in media? I nodi attraversati tra due frecce gialle sono quelli nell'intervallo $(2m, 2i+1)$, il cui numero è $|I| = (2i - 2m)/(2^b/n)$. Sapendo che il valore atteso di $i - m \leq 2^b/n$, si ottiene $|I| \approx 2$. Quindi per ogni freccia gialla vi sono in media 2 frecce verdi, per un totale di $3b = O(\log n)$ passi.

### Ottimizzazione

La distanza tra $m$ e il suo successore è con alta probabilità maggiore di $2^b/n^2$. Questo significa che $m$ è responsabile di nodi immaginari con tutte le possibili combinazioni degli ultimi $\log(2^b/n^2) = b - 2\log n$ bit. Scegliendo come nodo immaginario iniziale il nodo che ha gli ultimi $b - 2\log n$ bit uguali ai primi $b - 2\log n$ bit della destinazione, si devono effettuare soltanto $(b - (b - 2\log n)) \times 3 = 6 \log n$ passi.

### Koorde base k

Utilizzando de Bruijn in base $k$, ogni nodo ha $k+1$ link: 1 successore e $k$ link ai predecessori dei rispettivi vicini immaginari. Con grado $k$ il routing ha APL $O(\log_k n)$. Scegliendo $k = O(\log n)$ si ottiene:

$$\text{Grado} = O(\log n) \qquad \text{APL} = O\!\left(\frac{\log n}{\log \log n}\right)$$

che raggiunge il lower bound generale $\Omega(\log n / \log \log n)$.

### Svantaggi

Bisogna stimare $n$ a priori per scegliere $k$. Non è possibile cambiare il grado in un sistema attivo. La stabilizzazione della rete è molto più complessa rispetto a Chord.
