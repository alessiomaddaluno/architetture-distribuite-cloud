Un grafo $G=(V,E)$ è costituito da:
- $V$ nodi;
- $E$ archi. Un arco è definito come $e = (v,w)$
#### Path
Un path è un percorso tra due nodi ed è definito come $P(u,v)$ la sua lunghezza corrisponde al numero di archi.
#### Distanza
La distanza $d(u,v)$ fra due nodi u e v è data dalla lunghezza della **minima** path fra questi due nodi.
#### Diametro
ll diametro di un grafo è definito come la distanza massima fra tutte le possibili coppie di nodi nel grafo.

$$  
D(G) = \max_{(u,v)\in V \times V} d(u,v)  
$$
#### Avarage Path Length APL
L'APL (Avarage Path Length) è la distanza media considerando tutte le coppie di nodi.

$$
APL(G) = \frac{\sum_{(u,v)\in V \times V} d(u,v)}{n^2}
$$
#### Coefficiente di Clustering

Il coefficiente di clustering del nodo $v$ è chiamato $C(v)$ e corrisponde a:

$$ 
C(v)= \frac{e(v)}{k(v)(k(v)-1)/2}
$$
Dove $e(v)$ è il numero di vicini connessi tra di loro e 