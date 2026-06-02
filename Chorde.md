Creiamo un anello nel quale inserire i nostri peer e poi creiamo delle corde nell’anello in maniera efficace, garantendo la possibilità di raggiungere tutti i punti con un algortimo decentralizzato. Quello che ricerchiamo è il bilanciamento del carico, ovvero vogliamo essere equilibrati nell'assegnazione delle risorse ai nodi.


![[Pasted image 20260501113749.png]]

### Consistent Hashing
L'architettura è basata su $2^m$ identificatori dove $m$ è il numero di bit che costituiscono l'identificatore (di solito 160). Utilizza un algoritmo di hash che garantisce la distribuzione delle chiavi e permette il bilanciamento del carico sui nodi (con n nodi e k risorse), ogni nodo gestisce circa $\frac{(1+\epsilon)k}{n}$ risorse dove $\epsilon$ è nell'ordine di $O(logn)$.

Anche le risorse sono mappate sull'anello e una risorsa (chiave) viene assegnata al **primo nodo con ID ≥ chiave**, andando in senso circolare.

### Lookup 
Chord fornisce una sola API, chiamata Lookup, prende un identificatore (160 bit) e restituisce un IP address.
Il nodo deve fare due cose o risponderci o fornirci un IP di un nodo che ne sa più di lui.

Ogni nodo ha un link verso:
- $logn$ successori;
- 1 predecessore;
- $m$ fingers, whp $O(logn)$ 
	- I possibili m fingers hanno id = $u+2^{i-1}$

In totale mantiene dunque $logn + 1 + O(logn) = O(logn)$ link verso altri nodi.

![[Pasted image 20260501114706.png]]

### Algoritmo di Lookup

![[Pasted image 20260501120245.png]]

### Teorema per la distribuzione degli id

**Lemma**:
Dato un qualunque intervallo di ampiezza $2^{m}/N$, il numero di ID di nodi atteso in questo intervallo è 1 in media e **O(log N)** w.h.p.

Quindi ci sta dicendo sostanzialmente che gli ID dei nodi sono distribuiti “quasi uniformemente” sull’anello.

**Dimostrazione**:

Per dimostrarlo abbiamo prima bisogno di definire il **Chernoff Bound**:

Se ci troviamo difronte a un esperimento, per il quale facciamo $N$ prove, ogni prova ha una probabilità di successo $p_i$ e probabilità di insuccessi $1-p_i$, allora la media dei successi è la somma delle $p_i$, e la probabilità di discostarsi di un fattore δ (delta) rispetto alla media ($\mu$), è minore di questa quantità:

![[Pasted image 20260501123412.png]]

Se δ > 4, la funzione possiamo scriverla anche nel seguente modo:
![[Pasted image 20260501123330.png]]

Tale quantità rappresenta un upperbound del fenomeno.

Ritornando a chorde il fenomeno è modellato come se i nodi fossero delle biglie e le sezioni del cerchio come contenitori.

**Se consideriamo una fetta, la probabilità che il nodo cada in quella fetta è $1/n$ se ripetiamo l'esperimento $n$ volte in media sarà 1.**

La probabilità che la media sia $klogn$  (che è come scrivere $O(logn)$ da quale relazione è delimitata? 

Per capirlo dobbiamo vedere quanto vale $δ$ :

$$(1+δ)\mu = klogN$$

La media $\mu$ è 1, quindi:

$$(1+δ) = klogN$$

Se lo sostituiamo alla formula:

$$2^{-\mu(1+\delta)}$$

otteniamo:

$$2^{-klogN} = \frac{1}{2^{klogN}}$$
  
Per la proprietà dei logaritmi:
$$ \frac{1}{n^k}$$

### Teorema efficenza Lookup

**Lemma**:
Il numero dei nodi che deve essere contattato per risolvere una lookup è O(log n) w.h.p.

**Parte 1** - Dimostriamo che ad ogni hop dimezziamo

Supponiamo che il nodo $u$ deve risolvere una lookup per l’id $k$. Siano $p$ e $s$, rispettivamente, il predecessore e il successore dell’id $k$. 

Se $u\neq s$ e $u \neq p$ allora non è in grado di risolvere la lookup, di conseguenza deve contattare il finger più grande che non va oltre $k$ , questo perché a noi è sufficiente conoscere il predecessore del nodo che gestisce la risorsa per come funziona la lookup.

Tale finger lo chiamiamo $f$ ed è l'$i-esimo$ finger di $u$. 

![[Pasted image 20260501152639.png]]

$f$ copre questo intervallo: 
$$ [u+2^{i-1},u+2^{i} )$$
E in questo intervallo c'è necessariamente anche $p$. 

La distanza che c'è tra $u$ e $f$ è almeno $2^{i-1}$ per come abbiamo definito i fingers. Inoltre dal momento che $p$ appartiene all'intervallo, esso dista da $f$ al più $2^{i-1}$ , quindi ad ogni passo nel caso peggiore andiamo a selezionare un nodo che dimezza la distanza.

**Parte 2 - Si riesce a raggiungere qualunque destinazione con O(log n) con alta probabilità**

Sappiamo che la distanza tra sorgente e destinazione si dimezza ad ogni hop.
Supponiamo di effettuare $log n$ hops, dopo questi passi la distanza della destinazione si riduce ad al più 
$$\frac{2^{m}}{2^{logn}} = \frac{2^m}{n} $$
Dal teorema precedente di distribuzione uniforme degli id sappiamo che in quell'intervallo abbiamo al più $O(logn)$ quindi anche se andiamo a usare esclusivamente i successori faremo al più $logn$ passi.

$$logn + O(logN) = O(logn) passi $$

### Join e Stabilization

Solo il primo nodo chiama la funzione create che crea un "anello" (anche se tecnicamente non lo è) impostando se stesso come *successor* e come precedessor a null. Tutti gli altri nodi chiamano la join e per farlo devono necessariamente conoscere un nodo appartenente alla rete. La migrazione delle risorse non è gestita dal protocollo stesso.

![[Pasted image 20260506113806.png]]

I nodi devono continuamente scambiarsi informazioni per verificare che i nodi sono ancora attivi e correggere poi la struttura. Periodicamente vengono quindi eseguita l'operazione di stabilization che si occupa di verificare se il predecessore del successore è il nodo corrente e nel caso tenerlo aggiornato. A quel punto viene chiamata la notify sul successore che si occupa di aggiornare il predecessore:

![[Pasted image 20260506115332.png]]

Altre operazioni periodiche ma utilizzate con frequenza minore sono fix.finger e check.predecessor
![[Pasted image 20260602120829.png]]

La correttezza dei link al successore basta a garantire la correttezza delle lookup.
Lazy Join
- Inizializza solo il successore
- Periodicamente verifica successore e predecessore
- Periodicamente (ma meno spesso) rinfresca il contenuto della tavola dei finger

Cosa succede alla lookup a seguito di operazioni di Join?

- L’operazione di Join è completamente terminata -> nessun problema
- L’operazione di Join è parzialmente terminata -> la lookup potrebbe essere rallentata
- L’operazione di Join è incompleta (puntatori errati oppure le risorse si trovano in una posizione inconsistente rispetto ai link nella rete) -> la lookup potrebbe fallire

**Come dimostriamo la correttezza della join?**

Se ad un certo tempo $t$ siamo in grado di percorrere l'anello, o meglio di andare da $x$ a $y$ allora in qualunque tempo $t^i$ maggiore di $t$ saremo in grado di andare da $x$ e $y$. 

Se guardiamo la stabilize, ci accorgiamo che l'istante in cui l'eventuale nuovo nodo crea il link verso il suo successore  è sempre precedente all'instante in cui il nodo $p$ crea il link verso $u$. 

![[Pasted image 20260511121904.png]]

Per come è fatta la rete, inoltre ricordiamo che: 

Se abbiamo una rete stabile con n nodi ed effettuiamo n join alla rete, e se tutti i puntatori ai successori sono corretti, allora il Lookup di una risorsa avrà necessità di O(log n) hops con alta probabilità.

### Failure and replication

In **Chord** un nodo non mantiene un solo successore, ma una **lista di r = log n successori**, per rendere la rete più robusta ai guasti.
Se il successore immediato fallisce, il nodo se ne accorge e lo sostituisce con il primo successore attivo presente nella lista, aggiornandola durante la procedura di **stabilize**. La nuova lista si ottiene copiando quella del proprio successore, eliminando l’ultimo elemento e inserendo il successore corrente in testa.
Per interrompere il funzionamento della rete dovrebbero fallire **r nodi consecutivi** tra due operazioni di stabilize. Se la probabilità che un nodo fallisca è $p$, la probabilità di perdere $r$ successori consecutivi è $p^r$. Scegliendo $r=log⁡n$, tale probabilità diventa molto piccola (circa $1/n$).
La **lookup** può sfruttare sia i **finger** sia i successori per raggiungere il nodo destinazione. Se durante il percorso un nodo non risponde, basta ripetere il passo: grazie agli aggiornamenti del protocollo, sarà disponibile un percorso alternativo. Questa proprietà è detta **routing locale**, perché ogni hop porta comunque più vicino alla destinazione.

### Resource Replication

Può sempre accadere che un nodo senza volerlo cade, e se non abbiamo repliche delle risorse tutte le risorse del nodo si perdono. Replichiamo le risorse, e si fanno con varie strategie, solitamente 3:

1. Le repliche vanno su r successori;
2. Prevede la possibilità di usare diverse funzioni hash, ad esempio r, ogni nodo non ha una sola id ma ne ha r, e viene memorizzate in tutte le sue chiavi, si posiziona in r nodi nella rete;
3. Creare repliche speculari a distanze univormi;

### Leave

Dal momento che il protocollo è robusto ai fallimenti, potremmo ipotizzare di gestire la leave come un fallimento del nodo, tuttavia è preferibile, per migliorare le prestazioni del sistema, adottare alcuni accorgimenti, quando un nodo si disconnette volontariamente dalla rete. Il nodo che lascia la rete deve:
1. trasferisce le proprie risorse al suo successore;
2. notifica ai propri vicini (predecessore e successore) che sta uscendo dal sistema.


## Analisi Chord

Da ora stiamo considerando una rete chord piena, ovvero con tutti gli id assegnati a dei nodi.

![[Pasted image 20260514112554.png]]

Da notare come i vicini puntano ai nodi che differiscono di un solo bit, simile all'ipercubo (Lo è tecnicamente).

Consideriamo dunque sia composta da: $n=2^m$ nodi, dove $m$ è il numero di bit utilizzati per l'identificativo.
I suoi vicini sono $m$ e sono $(x+2^i)\mod2^m$ con i che va da 1 a m;

Quello che ci chiediamo è:

- Quant' è il grado? 
	- Il **grado** è banalmente $m = log n$, ricordiamoci che stiamo dicendo che l'anello è completo;
	- Dati due nodi x e y la loro distanza d(x,y) è uguale al numero di “1” che ci sono nella stringa binaria (y-x) mod 2m. Se prendiamo ad esempio 000 e 111 la distanza sarà 3, ne consegue che il **diametro** è $m = log n$;
	- **APL** dovremmo calcolare la distanza tra tutte le coppie dei nodi e dividere per $n^2$ ma essendo il protocollo chord uniforme questa formula può essere semplificata in quanto il protcollo è uniforme e invece di prendere tutte le distanze, le possiamo fare solo per un determinato nodo e traslare il tutto per quanto sono i nodi:
	- 
	  ![[Pasted image 20260514113748.png]]
	- Scegliamo come nodo sorgente a= 00..0 la distanza fra a e il generico nodo x è uguale al numero di bit 1 nella codifica binaria di x, pertanto se costruiamo una matrice con tutti gli identificatori essa avrà $2^m$ righe e $m$ colonne ma solo la metà dei suoi bit sarà 1, ed è il dato che ci serve. Dunque abbiamo che:
	  
	  ![[Pasted image 20260514114501.png]]

In conclusione, quali sono i vantaggi e gli svantaggi dei sistemi P2P uniformi?

Vantaggi:
- Facili da implementare e analizzare;
- Algoritmo di routing semplice (greedy);
- Routing locale, la procedura di lookup interessa solo i nodi che si trovano fra sorgente e destinazione (non c'è overshooting);
- Fast bootstrap: Poiché tutti i nodi utilizzano gli stessi jump, è possibile utilizzare la tabelladi routing del proprio predecessore per velocizzare notevolmente l’operazione di join;
Svantaggi:
- Non ci sono algoritmi più efficienti;
