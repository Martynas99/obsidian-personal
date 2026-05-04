## Longest common subsequence (LCS)
Example:
```
HIEROGLYPHOLOGY
	vs.
MICHAELANGELO 
	  V
	HELLO
```

**Problem**
Given two sequences A & B, find longest sequence L, that's subsequence of both A & B;

**Trick**
> **Subproblems for multiple inputs**: multiply subproblem spaces.

LCS: 
- Subproblems:
   $L(i, j) = LCS(A[i:], B[j:])$ for $0 \le i \le |A|$, $0 \le j \le |B|$
- Relate:
  L(i,j) = 
	- if A\[i] = B\[j]:
		- 1 + L(i + 1, j + 1)
	- else:
		- max{L(i + 1, j), L(i, j + 1)}
		- *One of A\[i] & B\[j] is not in LCS*

Logic for when equal:
1. A\[i] & B\[j] are not paired -> contradiction as if we pair, we get longer subsequence!
2. One of them is paired -> can just "unpair" and pair them together, then "1+" still holds
3. Paired to each other -> "1+" holds


## Longest increasing subsequence (LIS)

```
CARBOHYDRATE -> ABORT
```

Given seq A, find LIS(A), strictly increasing.

- Subproblem: L(i) = LISA(A\[ i : ]), that starts with A\[i]
- Relate: $L(i) = 1 + max(L(j)\: |\:  i < j < n,\: A[i] < A[j])$ + {0}
- Original problem: $max(L(i) \:|\: 0\le i \le |A|)$
- Top order for i=|A|, ... , 0
- BC: L(|A|) = 0
- Time: $\theta(|A|)$ subproblems x $\theta(|A|)$ non recursive work doing in subproblem = $\theta(|A|^2)$ ( + $\theta(|A|)$ to solve original problem)


IDEA: We could write these dynamic programs as graph + DAG shortest path (but what we do is simpler..)

## Alternating coin game
- given sequence of n coins of value $v_0, ... , v_{n-1}$