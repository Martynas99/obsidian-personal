
## Recursive Algorithm Design Paradigm

### SRTBT
- **Subproblem** definition
- **Relate** subproblem solutions recursively
- **Topological** order on subproblems to guarantee acyclic
	- (subproblem/call DAG)
- **Base** cases of relation
- **Original** problem: solve via subproblems
- **Time** analysis

Hardest steps are 1-2 (and are related heavily)

#### SRTBT analysis of merge_sort(A)
- Subproblems: S(i,j) = sorted array on A\[i:j]
- Relate: S(i,j) = merge(S(i,m),S(m,j)), where $m=\lfloor\frac{i+j}{2}\rfloor$
- Top. Order: increasing j-i
- Base cases: S(i,i) = \[ ]
- Original prob.: S($\emptyset$, n)
- Time: T(n) = 2T(n/2)+ O(n) = O(n logn);           n=j-i

