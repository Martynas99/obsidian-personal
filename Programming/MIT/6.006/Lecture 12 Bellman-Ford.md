Today: SSSP in cyclic graph with negative weights

- For undirected graph, a single negative weight edge means there exists a negative weight cycle.
	- Today we restrict to directed graphs


### Simple Shortest Paths
**CLAIM 2** #claim
> If $\delta(s,v)$ if finite, $\exists$ a shortest path $s-v$ that is ==simple== (contains no cycles)

**Proof**:
If path is not simple and finite, a node must be there twice. We split the distance into three parts a (source to node) + b (cycle) + c (node to target). Given the path is finite and shortest, b = 0, hence we can remove it and have a simple path.

> Simple paths have at most $\le|V| - 1$ edges.

#### k-Edge distances
> $\delta_k(s,v)$ shortest s-v path using $\le k$ edges

> If $\delta_{|V|}(s,v) < \delta_{|V| - 1}(s,v)$, then $\delta(s,v) = -\infty$, v is ==witness==


**CLAIM 2** #claim
> If $\delta(s,v) = -\infty$, then $v$ is reachable from a witness.

**Proof:**
- Let's prove a stronger statement - every negative weight cycle contains a witness.
- Let's consider a negative weight directed cycle C. 
- Let's call two consecutive nodes v' and v (v' is predecessor to v). 
- We know the following holds: $\delta_{|V|}(s,v) \le \delta_{|V| - 1}(s,v) + w(v', v)$:
	**This is because $\delta_{|V|}(s,v) = min( \delta_{|V| - 1}(s,v) + w(v', v)| v)$, as path going through v' is one of the possible paths, but not guaranteed to be smaller!!**
 
- Summing this for all $v \in C$, gives that $\delta_{|V|}(s,v) < \delta_{|V| - 1}(s,v)$ as $\sum_{V\in C}w(v',v) < 0$ as cycle is negative weight, however if C would contain no witness,  $\delta_{|V|}(s,v) \ge \delta_{|V| - 1}(s,v)$ for all $v \in C$, this is contradiction.

### Bellman-Ford (modified)
IDEA: GRAPH DUPLICATION
- Make $|V| + 1$ levels, $v_k$ in level $k$ represents reaching vertex $v$ using $\le k$ edges.
- If we connect edges from one level to only higher levels, then DAG!
- Also we create 0 weight loops to stay at vertice.
![[Pasted image 20250421182811.png]]

#### Bellman-Ford:
1. Construct $G'$ from G:
	-  with $|V|(|V|+1)$ vertices $v_k$, for all $v \in V$ and $k \in \{0,...,|V|\}$  $|V|(|V| + |E|)$ Edges
	- G' has $|V|(|V|+|E|)$ edges:
		- |V| edges $(v_{k-1}, v_k)$ for $k \in \{0,...,|V|\}$ of weight zero for each $v\in V$ (edge to itself in next step)
		- |V| edges $(u_{k-1}, v_k)$ for $k \in \{0,...,|V|\}$ of weight $w(u,v)$ for each $(u,v) \in E$ (edges from original graph between vertices)
	
2. Run DAG Relaxation from $s_0$, computing $\delta(s_0, v_k) \ \  \forall k=\{0, ..., |V|\}$
3. For each vertex, $v$:
	   set $d(s,v) = \delta(s_0,v_{|V| - 1})$
   
4. For each witness $u \in V$ (defined as $\delta(s_0,u_{|V|}) < \delta(s_0,u_{|V| - 1})$)
	   For each $v$ reachable from $u$:
		   set $d(s,v) = -\infty$

Explanations of:
- Step 4: Each node than can be reached by witness, can be reached via negative weight cycle, hence $\delta(s,u) = \infty$
- Step 3: This means we correctly set shortest path distances for finite distances (from Claim 4)

**Claim 4** #claim 
> $\delta(s_0,v_k) = \delta_k(s,v)$ ($\delta_k$ is k-edge distance)
> 
> Shortest-path from $s_0$ to $v_k$ in $G'$ corresponds to shortest $k$ edge path in original graph between $s$ and $v$


This claim means that we correctly set finite distances  in Step 3 of Bellman-Ford. (combined with claim 2 and k-edge distance idea that if # of edges in shortest path is less than |V|, then it is finite).

Proof of Claim 4:
Induct on k
Base Case: k = 0, True as all distances are $\infty$ as they are not reachable.
Inductive step:

$$
\delta(s_0, v_{k'}) = min\{\delta(s_0, u_{k'-1}) + w(u_{k'-1},v_{k'})\ |\  u_{k'-1}\in Adj^-(v_{k'})\} \ \ \ \ (1)
$$
$$
= min\{\delta(s_0, u_{k'-1}) + w(u,v)\ |\  u\in Adj^-(v)\} \cup \{\delta(s_0, v_{k'-1})\} \ \ \ \ (2)
$$
$$
= \delta_{k'}(s,v)  \ \ \ \ (3)
$$
Logic:
1. Definition of shortest distance (min of all incoming paths (paths to nodes with edge to current node + weight of that edge))
2. Take out zero weight path to itself;
3. Definition of k edge shortest path: all paths of length k $\cup$ k-1 edge shortest path 

#### Bellman-Ford runtime
Step 1: to construct G' |V|(|V| + 1) + |V|(|V| + |E|)
Step 2: DAG relaxation takes linear time in the size of G' (|V|(|V|+|E|))
Step 3: for each vertice we do constant work (|V|)
Step 4: for each witness (at most |V|) we find connected components (at most |E| with DFS) |V||E|
Total |V|(|V|+|E|)

## Questions
1. Alg A solves SSSP in O(V * (V + E)), show how to solve SSSP in O(V+E)
2. 

