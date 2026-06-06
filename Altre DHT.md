## Tapestry

Implementazione dinamica dell'algoritmo di Plaxton (che non si adattava a sistemi dinamici). Simula un ipercubo in un contesto P2P dove i nodi entrano ed escono continuamente.

### Idea di base

Ogni nodo ha un ID in **base k** con **d digit**, dove $n = k^d$ quindi $d = \log_k n$.

Il routing corregge **un digit alla volta**: ad ogni hop si porta un digit della sorgente al valore corretto della destinazione, allungando il prefisso comune.

### Tabella di routing

Ogni nodo costruisce e mantiene la propria tabella personale: **d colonne** × **(k-1) righe**.

- **Colonna j** → nodi che condividono i primi j-1 digit con te, ma hanno il j-esimo digit diverso
- **Riga i** → il nodo reale più vicino con quel prefisso e quel valore di digit

Il `*` nelle entry indica che non importa il valore residuo: si sceglie il nodo reale esistente che meglio approssima quel prefisso.

**Dimensione tabella**: $(k-1) \times \log_k n$ entry totali = $O(\log n)$ nodi

### Come funziona il routing

Dati sorgente e destinazione, si confrontano digit per digit:
1. Si individua la **prima posizione in cui divergono** → quella è la colonna da usare
2. Si sceglie la **riga corrispondente al valore del digit nella destinazione**
3. Si forwarda a quel nodo e si ripete

**Esempio**: `1323` → `1333` (base 4)
- Primi due digit uguali, terzo diverge (2 vs 3) → colonna 3, riga con digit=3 → forward a `1332`
- `1332` ha `1333` nella sua colonna 4 → un hop e si arriva

### Complessità

| | |
|---|---|
| Grado | $(k-1) \times \log_k n = O(\log n)$ |
| Diametro | $\log_k n = O(\log n)$ |

### Fault tolerance

La tabella è robusta ai fallimenti perché ogni cella rappresenta una **classe di nodi equivalenti** (stesso prefisso richiesto), non un nodo unico e insostituibile come nell'ipercubo classico. Se un nodo in tabella fallisce, può essere rimpiazzato da qualsiasi altro nodo vivo con lo stesso prefisso. In pratica si mantengono candidati alternativi per ogni cella.
