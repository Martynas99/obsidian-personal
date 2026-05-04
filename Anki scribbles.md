##### Johnsons complexity analysis
1. Building Gs is O(V + 1 + E + V)
2. Running BF on Gs is O(VE)
3. Checking if any are inf O(V)
4. V x Running DIjkstra O(VE + V^2 logV)
5. Building D in O(V^2)

SS reachability optimal is O(E) (not V as only explores connected component)



##### Dijkstra
1. init stuff, d[s] = 0 
2. Create and populate CPQ with node, d[node]
3. While Q not empty
	1. Extract_min distance node u from Q
		1. for nodes v in adj+[u]
			1. try to relax
			2. update d in Q for v


#### node delete
```
def delete_node(node):
if node.left:
	B = node.predecessor()
elif node.right:
	B = node.successor()
B.val, node.val = node.val, B.val
return B.delete_node()
if node.parent:
	if node is node.parent.left:
		node.parent.left = None
	else:
		node.parent.right = None
	return node
```



#### sorting table

| sort           | time      | in place | stable | comms                                         |
| -------------- | --------- | -------- | ------ | --------------------------------------------- |
| insertion sort | n^2       | y        | y      | the one where keep shifting to left           |
| selection sort | n^2       | y        | n      | the one where find min/max and move to front  |
| Merge sort     | nlogn     | n        | y      | merging two arrays (and again(and again(..))) |
| AVL sort       | nlogn     | n        | y      | Keep inserting into AVL tree and then pop out |
| Heap sort      | nlogn     | y        | n      | Same w heap but give all in advance!          |
| Counting sort  | u + n     | n        | y      | daa size of largest element                   |
| Radix Sort     | n + nlogu | n        | y      | tuple sort + size of n, if u=n^c, then linear |

#### SRTBOT
S - define a subproblem
R - relate it to original problem
T - Argue that it is acyclic and subproblems form a DAG
B - base case (usually i = 0)
O - original problem
T - Time analysis

Points hitting set of sticks I (lec game)
S - points hiting some set X
R - points relation max(X and 1, X-1 and 2) = X + 1
T - incerasing l to r
B P\[1] = Xi
O P\[n]
T = O(n) (visit each once)

#### Bheap in linear
Give all in advance
for i in (n//2, -1, -1):
	max_heapify_down(i)

#### Dijkstra's algo
1. init all to inf
2. CPQ with node, distance to source
3. While Q not empty:
	1. Pop smallest, get du
	2. for every neighbour
		1. try to relax
		2. update Q (if relaxed)
4. done

#### SRTBOT
S - define a subproblem that can help solve the problem recursively
R - relate it to original problem (or some other subproblem)
T - argue that computation graph is a DAG 
B - base case (all cases not covered by S + R)
O - original problem
T - time analysis (O(W) = work per node * N of nodes in work DAG)
#### What is top-down (memoization) approach in dynamic progr?
top down - From final problem to subproblems
memoization - keep previously calculated items in

The idea is to recursively define the problem while keeping track of already calculated results, e.g 
memory(i) = fibionacci(i-1, memory) + fibionacci(i-2, memory)
return memory(i)

It's recursive approach htat starts with the main problem and breaks it down. Solve when you need it strategy
#### Agg analysis in alg
We can do stuff once every n so on av take 1

#### JOhnsons running time analysis
1. s mapping -> BF, O(VE)
2. rescaling -> O(E)
3. N x DIJ = (|V| * (|V| + |E|log|E|)))
4. rescale all SP, |V|^2

#### DAG relaxation proof
1. init to inf so unreachable stay inf
2. process in TSO, so all distances are calcualted by the time reached
3. Sets to valid path
4. 

#### Pros and Cons of memoization
1. Pro - don't overcalculate
2. pro (?) easier to write logically

Con - stack can overflow
Con - recursion overhead

#### what is cpq:
PQ (e.g heap) with editable order!

so all same, but has update_key method
#### p and c of me
intuitive, only calc what need
stack overflow, recursive overhead
#### srtbot
- Sub-problem definitoin (can be sub-index, firs/last n (O(n)))
- relate subproblem to original (how do we proceed with increasing/decreasing/changing i/j)
- Need to argue that the order builds a dag (no loops), so that we could proceed in recusrive fashion
- base case (any cases not following the original, e.g i=0, i=n, etc.)
- original problem
- time complexity, if constant time per work item, then just n x O(w), assume O(1) for recursive
#### seq operations
Array: O(n) 1, O(n), O(n), O(n)
LL: n,n,1,1,n
DA, n, 1, 1a, 1a, n
n, logn, logn, logn, logn
#### Dijkstra Time com
- Tb + E Tu + V Td
- VlogV, E x 1, V x lgV
#### set sheet
array n, n, n, n, n
nlogn, n, n, 1, 1
n, 1, 1, u, u
n, 1e, 1e, 1e, n
nlogn, logn, logn, 1. logn
#### it is spary and pary, does not establish connections or resend packets
- No handshake or connection 
- No guarantee of delivering
- No ordering
- Low latency
#### UDP caveats
UDP is not supported by many browsers, so browser users need to have their own soln for this

#### Layer 3
adressing and routing, packet forwarding over network and data splitting into packets
IP is the protocol

#### UDP
- Conectionless no handshake
- Not guaranteed delivery
- Not guaranteed order
- low latency

#### TCP char
- Guaranteed order
- connection oriented - establishes connection beefore transfer
- Flow control - prevents overwhelming receivers with too much data
- COngestion control - adapts to netwrok congestion to prevent collapse
















