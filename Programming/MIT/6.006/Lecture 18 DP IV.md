### Polynomial time

Is $\theta(L^2)$ polynomial time? (Rod cutting exercise)

> (Strongly) **polynomial time** = polynomial in **input size** measured in words!

Input size is L+1 so $\theta(L^2)$ is polynomial in input size!

Now in **Subset sum**:

Is $\theta(nT)$ polynomial time? No.
Input size is n+1, but running time is a function of n and T!
- Know that $T\le2^w$,  because T fits to a word. Also, we always assume $w \ge \log n$
- But we don't know anything on upper bound, it's possible that  $w >> \log n$
  E.g when w = n, nT is exponential in n+1
- This is called **pseudo-polynomial**

### Pseudo-polynomial time

> **Pseudo-polynomial time**
> O(1) degree polynomial in input size and input integers!

Pseudo-polynomial implies polynomial, if input integers $\le$ polynomial in input size ($T < n^c$)
Also pseudo-polynomial:
- Counting sort
- DAA
- Fibionacci
- Radix sort (technically weakly polynomial, as has $\log_n u$)

### Main features of DP
- Subproblems:
	- prefixes/suffixes:
		  Bowling, LCS, LIS, Floyd-Warshall, (Rod Cutting), Subset sum
	- substrings:
		  Alternating coin game, Parenthisation, 
	- multiple sequences:
		  LCS
	- integers:
		  Rod cutting, Subset sum, Fibonacci
		- pseudo-polynomial:
			   Subset sum, Fibonacci
	- vertices:
		  All shortest paths problems
- Subproblem constraints / expansion:
	- nonexpansive contraint: 
		  LIS
	- $2 \times$: Alternative coin game, Parenthisation
	- $\theta(1) \times$ Piano fingering
	- $\theta(n) \times$ Bellman-Ford
- Relation:
	- $\theta(1)$ branching:
		  Fib, Bowl, LCS, ACG, F-W, SS
	- $\theta(degree)$ branching:
		  DAG SP, B-F
	- $\theta(n)$ branching
		  LIS, Parenth, Rod
	- Combine multiple solutions (**not** path in DAG):
		  Fib (just add), F-W (concat paths), Parenth (multiply or add!)
- original: combine multiple subproblems:
	  DAG SP, LIS, B-F, F-W





