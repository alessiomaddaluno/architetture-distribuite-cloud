Una rete è considerata Small World se:
- Ha un numero elevato di nodi (n>>1)
- Il grado dei nodi è basso (grado  media k << n)
- Ha un coefficente di clustering elevato
- Ha un APL basso

## Modello Watts and Strogatz 

Si parte dalla creazione di un anello con n nodi. Ogni nodo è connesso con i k nodi più vicini ad esso.

Infine alcuni archi vengono reindirizzati con probabilità p, vale a dire, si prende ogni arco e con probabilità p si cambia la destinazione dell’arco con un nodo a caso.

![[Pasted image 20260529170341.png]]

##  Modello di Kleinberg 

Consideriamo $N$ nodi su una matrice d-dimensionale. Ogni nodo ha:

- $2d$ vicini sulla grgilia;
- $k$ contatti detti long-range. Ogni nodo v stabilisce k link indipendentemente utilizzando una distribuzione di probabilità $p(d(u,v))$

Di solito questa probabilità è propozionale a $d(u,v)^{-\alpha}$  dove $\alpha$ **controlla la forma della distribuzione**, cioè _quanto velocemente decresce la probabilità con la distanza_.

**Teorema**: L‘algoritmo di routing greedy è capace di trovare delle path brevi, vale a dire, path di lunghezza $O(log^2 n)$, da ogni sorgente a ogni destinazione se $\alpha = d$ .

L'idea è che se $\alpha > d$ abbiamo troppi pochi archi casuali da utilizzare per raggiungere più velocemente il target, mentre se $\alpha < d$ i sono troppi archi casuali, e quindi troppe scelte da effettuare.

Lo dimostreremo nel caso di 1 dimensione, ovvero $d=1$

![[Pasted image 20260529173458.png]]

Calcoliamo la probabilità $\theta$ che u ha un long range a distanza maggiore di d/2 e minore di d