> ALMOST linear for non-negative weights (SSSP)

## Idea of Dijkstra

> **Observation 1**
> If weights $\ge$ then distance increases along **shortest paths**

![[Pasted image 20250505171814.png]]
Idea is to use some increasing frontier / sphere to explore the graph.

> **Observation 2**
> Solve SSSP faster if given order of vertices in increasing distance.

## Dijkstra's algorithm

> **Idea**
> Relax edges from vertices in increasing distance from s

> **Idea**
> Find next vertice efficiently using a *Changeable priority queue*


> [!NOTE] Changeable Priority Queue
> - Q.build(X)
> - Q.delete_min()
> - Q.decrease_key(id, k)
> Implementation:
> Use Priority Queue Q' and cross link with a dictionary D (maps ids with their locations in Q'). Could use IDs of 0 to v-1 to get O(1) lookups in dict (not expected!)


#### Algorithm
1. Set $d(s,v) = \infty$ for $v \in V$, set $d(s,s) = 0$
2. Build CPQ Q with item $(v, d(s,v))$ for each $v \in V$
3. While Q not empty:
	1. delete $(u, d(s,u))$ from Q (that has min distance)
	2. For $v \in Adj^+(u)$:
		1. if $d(s,v) > d(s,u) + w(u,v)$:
			1. Relax (u, v)
			2. Decrease key of v in Q to the new d(s,v)

### Correctness of Dijkstra's algorithm

> **Claim**
> $d(s,v) = \delta(s,v)$  $\forall   v \in V$ at the end.

##### Part 1
If relaxation sets $d(s,v) = \delta(s,v)$ at some point, then it is still true at the end.
- Relax only decreases $d(s,v)$, but relaxation is safe, so EOD.

-> Enough to show that $d(s,v) = \delta(s,v)$, when $v$ is removed from Q.

##### Part 2
Induction on first ==k== vertices removed from ==Q==.
Base case: (k=1) True - When we pop first vertex (source) it has correct min distance (0)
Inductive Step: 
1. Assume true for k < k', consider k'th vertex v' removed from Q
2. Consider some shortest path $\pi$ from s to v', with $w(\pi) = \delta(s, v')$
3. Let $(x, y)$ be the first edge in $\pi$ where y is not among first $k'-1$ (perhaps $y=v'$)
4. When x was removed from Q, $d(s,x) = \delta(s,x)$ by induction, so:
![[Pasted image 20250527163027.png]]

Explanations:
Step 3: Basically considers a vertice in shortest path to v' which hasn't been removed from Q during processing.
Step 4:
0. From induction we know that all vertices removed prior to ==v'== from Q had their shortest path distances set correctly
1. We set $d(s,y) = d(s,x) + w(x,y) =  \delta(s,x) + w(x,y)$ when we pop ==x== and process outgoing edges from x.
2. Shortest-path property
3. From Observation 1, as weights are non-negative, distance cannot decrease down the path, and y is no later than v'
4. As relaxation is safe, the SP distance is bounded by set distance by relaxation
5. As v' is popped before (or at the same time if y=v') y, this means that  $d(s,y) \ge d(s,v')$ as we always pop smallest distance, which forces all inequalities to become equalities.

### Running Time analysis
![[Pasted image 20250527163918.png]]

> [!NOTE] Running Time of Dijkstra
> O(B + |V|M + |E|D)
> **Explanation**
>1st term - build CPQ in Step 2
>2nd term during step 3 we delete each vertice once
>3rd term at worst we reduce shortest path estimate when we process every edge


In Practice:
![[Pasted image 20250527164344.png]]

