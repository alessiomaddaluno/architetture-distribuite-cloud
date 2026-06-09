## Tapestry

L'idea di fondo è simulare un ipercubo in un contesto P2P dove i nodi entrano ed escono continuamente, rendendo la struttura fault-tolerant e adattiva.

### Identificatori e struttura

Ogni nodo ha un ID in **base k** con **d digit**, dove $n = k^d$, quindi $d = \log_k n$. Il routing corregge **un digit alla volta**: ad ogni hop si porta un digit della sorgente al valore corretto della destinazione, allungando progressivamente il prefisso comune tra il nodo corrente e la destinazione.

### Tabella di routing

Ogni nodo costruisce e mantiene la propria tabella personale con **d colonne** e **k-1 righe**.

La **colonna j** contiene nodi che condividono i primi $j-1$ digit con il nodo corrente, ma hanno il $j$-esimo digit diverso. La **riga i** contiene il nodo reale più vicino con quel prefisso e quel particolare valore di digit.

Il `*` nelle entry del template indica che il valore residuo non importa: si cerca il nodo reale esistente che meglio approssima il prefisso richiesto. La dimensione totale della tabella è $(k-1) \times \log_k n$ entry, pari a $O(\log n)$ nodi.

**Esempio** - tabella del nodo `1323` in base 4:

Colonna 1 (primo digit diverso da 1):
- $(2, *, *, *)$ → nodo reale più vicino che inizia con 2
- $(3, *, *, *)$ → nodo reale più vicino che inizia con 3
- $(0, *, *, *)$ → nodo reale più vicino che inizia con 0

Colonna 2 (primo digit = 1, secondo diverso da 3):
- $(1, 0, *, *)$
- $(1, 1, *, *)$
- $(1, 2, *, *)$

E così via per le colonne 3 e 4.

### Algoritmo di routing

Dati sorgente e destinazione, si confrontano i digit uno per uno. Si individua la **prima posizione in cui divergono**: quella è la colonna da usare. Si sceglie poi la **riga corrispondente al valore del digit nella destinazione** e si forwarda a quel nodo. Il processo si ripete finché si arriva a destinazione.

**Esempio**: `1323` deve trovare `1333`.

I primi due digit coincidono (`1` e `3`), il terzo diverge (`2` vs `3`). Si usa la colonna 3, riga con digit = 3, e si forwarda a `1332`. Il nodo `1332` ha `1333` nella propria colonna 4: un solo hop e si arriva.

### Complessità

Il **grado** di ogni nodo è $(k-1) \times \log_k n = O(\log n)$ e il **diametro** è $\log_k n = O(\log n)$, esattamente come Chord ma con un meccanismo di routing completamente diverso (prefix matching invece di dimezzamento della distanza numerica).

### Fault tolerance

La tabella è robusta ai fallimenti perché ogni cella rappresenta una **classe di nodi equivalenti** — tutti i nodi con un determinato prefisso — e non un nodo unico e insostituibile come nell'ipercubo classico. Se un nodo in tabella fallisce, può essere rimpiazzato da qualsiasi altro nodo vivo con lo stesso prefisso richiesto. In pratica si mantengono candidati alternativi per ogni cella, e il protocollo aggiorna le tabelle quando rileva un fallimento.
