## All-pairs Shortest Paths problem

#### Input
Weighted graph $G=(V,E)$   $w:E \rightarrow \mathbb{Z}$ 

#### Output
$\delta(u,v)\ \forall\ u,v\in V$ 
or
Abort if G contains neg-weight cycle

#### Possible algorithms

| Algo                 | Complexity                        | Comment                                      |
| -------------------- | --------------------------------- | -------------------------------------------- |
| \|V\| x Bellman-Ford | $O(\|V\|^2\|E\|)$                 | Only relevant for directed graphs            |
| \|V\| x Dijkstra     | $O(\|V\|^2log\|V\| + \|V\|\|E\|)$ | No neg weights                               |
| ???                  |                                   | Closer to Dijkstra but with negative weights |

> ==If graph is undirected, only need to check if exists a neg weight edge== and then can run Dijkstra if does not (or return that has neg weight cycle if exists)

>**IDEA!**      
>We can make edge weights non-negative while preserving shortest paths

> **CLAIM**    
> We can compute distances in G from distances in G' (with non-neg edge weights) in $O(|V|\times(|V| + |E|))$
> Proof by sketch..

> **Claim**
> Not possible if G contains a neg-weight cycle. 
> Proof by looking at neg weight cycle and simple vs non-simple paths

> ~~**IDEA**~~
> Add large # to each edge => BAD, makes weights non-neg but does not preserve shortest paths (bias towards paths with fewer edges)

> **IDEA**
> Given vertex v:
> - add weight h to all outgoing edges
> - subtract weight h from all incoming edges

> **CLAIM**
> Shortest Paths are preserved under this transformation

Proof by cases:
1. v is not passed for some path (w(path) does not change)
2. v is passed in the middle for some path (w(path) does not change)
3. v is start (end) vertex - all paths leaving/coming to v are changed by the same amount, the shortest path stays the same.

 --General argument when all v are "augmented"--
![[Pasted image 20250529222223.png]]
#### Does there exists h, such all modified weights are non-negative?
$\exists\ h \quad s.t. \quad w'(u,v) = w(u,v) + h(u) - h(v) \ge 0$
from here $h(v)\le h(u) + w(u,v)$

But these nodes need to be reachable to compare!

> **Idea**
> Add new vertex s with 0-weight edge to every vertex v in V

![[Pasted image 20250529214822.png]]

Run SSSP from s on Gs
- if $\delta(s,v) = -\infty$, then there's a negative weight cycle in G => ABORT!
- else: reweight with $h(v)=\delta(s,v)$ ??????

## Johnson's Algorithm
1. Construct Gs from G
2. Compute $\delta(s,v)\ \forall \ v \in V$ (e.g by Bellman-Ford)
3. If $\exists\ \delta(s,v) = -\infty$: 
	1. ABORT
4. else:
	1. Make G' by reweighting each $(u,v) \in E$  $w'(u,v) = w(u,v) + \delta(s,u) - \delta(s,v)$
5. Solve APSP on G' with Dijsktra;
6. Compute distances of G from distances in G'

#### Correctness


#### Complexity Analysis
Step 1: O(|V| + |E|)
Step 2: O(|V||E|)
Step 3: O(|V|)
Step 4: O(|E|)
Step 5: |V| x Dijkstra = O(|V| x (|E| + |V|log|V|))  
Step 6: O(|V| x (|V| + |E|))