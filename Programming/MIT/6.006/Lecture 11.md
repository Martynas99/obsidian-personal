## Lecture 11

Ways to store the weights of edges?
	1. Store it with each adjacency (e.g like a tuple)
	2. Any separate set data structure, mapping edges to their weights

Definitions of weight of path and shortest weighted path
	Formula for shortest path weight between two vertices
		Caveat when path doesn't exist
		Caveat with path weight when there is a negative loop

Negative-weight cycles caveat:
	If there exsits a path from s to v that goes through a vertex on a negative weight cycle, then delta(s,v) = - inf

Using BFS for weighted graphs
	Works if all weights are equal
	Also can replace weighted edges with multiple unweighted edges (not a good idea but works)

#### Shortest-path trees 
- for weighted, only need parent pointers P(v) for v with finite delta(s,v)
- Showing that distances are sufficient to reconstruct parent pointers in linear time (distances, for subset of graph reachable from s, that do not go through negative weight cycles)
**Algorithm**
	Initatiate P (parent pointer data structure) to be empty, P(s) = None
	For each u in V, where $\delta(s,v)$ is fininte:
		For each v in Ajd+(u):
			if v not in P and $\delta(s,v)$ == $\delta(s,u) + w(u,v)$:
				set P(v) = u
				Because there exists a shortest path that uses (u,v)

This allows us to just focus on computing distances, without worrying about parent pointers!

#### DAG relaxation
- Maintain estimates $d(s,v)$ (initialise at inf)
- $d(s,v)$ upperbound $\delta(s,v)$, gradually lower until equal

**Traingle inequality**
$\delta(u,v)\le\delta(u,x)+\delta(x,v)$
```
U ----> V
 \     ◥
  \   /
   ◢ /
    X
```

If there is $(u,v)\in E$ such that $d(s,v) > d(s,u)+w(u,v)$ (the triangle eq. is violated (for estimates!)), then we **lower the estimate ("relax the edge")** to $d(s,v) = d(s,u)+w(u,v)$ 

Relaxation is SAFE: 
- each $d(s,v) is wieght of some path s to v (or infinite)
- Relax (u,v), assign d(s,v) to weight of some path
(because d(s,u) was weight of some path, hence adding w(u,v) maintains it weight of some path, so nothing is broken)

#### Algorithm
1. set $d(s,v) = inf$
2. set $d(s,s) = 0$
3. process each vertex u in a topological sort order
	For each $v\in Adj^+(u)$: (outgoing neighbour of u)
		if  $d(s,v) > d(s,u)+w(u,v)$: (if estimate violates triangle inequality)
			set $d(s,v) = d(s,u)+w(u,v)$ (relax (u,v))

**Analysis**
Claim: At end, $d(s,v) = \delta(s,v)$
By induction, by the time we came to u, we already have shortest path to 


#### DAG relaxation implementation
![[Pasted image 20250322141656.png]]

Questions for Anki:
1. How to compute parent pointers and shortest paths from distances?
2. DAG relaxation algorithm
3. DAG relaxation implementation
4. Complexity of DAG relaxation (calculation)
5. Complexity of BFS + corner cases