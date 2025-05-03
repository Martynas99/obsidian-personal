## Lecture 2

1. What is the difference between interface (API) vs Data Structure?

| Interface                                        | Data Structure                     |
| ------------------------------------------------ | ---------------------------------- |
| What you want to do                              | How you are doing                  |
| - Specification                                  | - Representation                   |
| - What data can store                            | - How to store data                |
| - What operations are supported & what they mean | - Algorithms to support operations |
| - Problem                                        | - Solution                         |

### Lecture 6
Define subtree of a Btree
Define the height of a Btree
Descendents and ancestors of a Node
Define depth of a node in BTree
Define traversal order of node items and algo to iterate them


Binary tree queries ()
Binary tree modification operations (insert_before, insert_after, delete)
How to make Btree from a sequence (list)
How to make Btree from a set (dict)


## Lecture 7
- definition of subtree_find(node = root, k):
```
subtree_find(node, k):
	if node is None: return
	if k < node.item.key: subtree_find(node.left, k)
	if k = node.item.key: return Node
	if k > node.item.key: subtree_find(node.right, k)
```

- Set binary tree again (Binary Search Tree);
- Sequence binary tree subtree_at(node, i)
```
subtree_at(node, i):
n_l = size(node.left)
if i < n_l: subtree_at(node.left, i)
if i = n_l: return node
if i > n_l: subtree_at(node.right, i - n_l - 1)
```
- What is a size(node)?
	-  # nodes in subtree; How is size(node) computed
- What is a subtree property? Give some examples and counter examples
- Explain subtree augmentation
- What is rotation, in binary tree?
- What is skew (node)?
	- the Difference in heights of children: height(node.right) - height(node.left) (we want it to be {0,1,-1} for height balance)

##### Why does height balance imply balance in BTrees?#
![[Pasted image 20250129200610.png]]
Minimum # of nodes in a height balanced binary tree
$$
N_h = N_{h-1} + N_{h-2} + 1 \ge 2 * N_{h_2} = 2^{h/2}
$$
which means
$$h \le 2\log n$$Hence height balanced trees are quite balanced!



## Lecture 8
Operations of **priority queue** interface
- build(X): init to items in X
- insert(X): add item x
- delete_max(): delete and return max-key item
- find_max(): return max-key item

Priority queue sort
Implementations of priority queue (array, sorted array, set AVL, Heap)
Complete Binary Tree
Implicit data structure
Binary Heap defn
- insert algo + max_heapify_up
- indexing (left, right, parent)
- delete_max + max_heapify_down
How does binary heap achieve in place sort?
How does binary heap use linear build?

## Lecture 9

### Graphs review

What is a graph?

Definition of Simple Graph

Directed, undirected graph number of edge formulas

Sum of degrees (inward/outward vs just degrees for undirected graph)

Breadth-First Search Algo



