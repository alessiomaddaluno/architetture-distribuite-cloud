L’immersione di una architettura in un’altra è una funzione che mappa i nodi di una architettura (ospite) nei nodi dell’altra (ospitante).

Ad esempio è possibile mappare un array in un Ipercubo:

![[Pasted image 20260316152927.png]]

Le linee tratteggiate sono collegamenti che dopo la mappatura non sono utilizzati in quanto non seguono le caratteristiche della rete ospitante.

Per poter valutare la qualità di un'immersione è necessario verificare i seguenti parametri:

- **Dilatazione**: la dilatazione di un arco (dell’architettura ospite) è la lunghezza delle path che simula l’arco sulla architettura ospitante. La dilatazione di una immersione è la massima dilatazione su tutti gli archi dell’architettura di ospite. 
  
  In pratica risponde alla domanda "quanto è lungo il path che simula un arco dell'ospite"? In questo caso dovendo trovare il massimo è 3, ad esempio quello tra 011-100 perchè per poterlo simulare in un ipercubo devo fare 3 hop.

- La **congestione** di un arco (dell’architettura ospitante) è il numero delle path che utilizzano tale arco per simulare gli archi dell’architettura ospite. La congestione di una immersione è la massima congestione su tutti gli archi dell’architettura ospitante

- L'**espansione** è il rapporto tra numero di nodi dell’architettura ospitante e numero di nodi dell’architettura ospite

- Il **carico** è il numero massimo di processori dell’architettura ospite che vengono simulati da un solo processore dell’architettura ospitante.


Parametri ottimali:
- Dilatazione <= 2
- Congestione <= 6
- Espansione <= 2
-  Carico = 1