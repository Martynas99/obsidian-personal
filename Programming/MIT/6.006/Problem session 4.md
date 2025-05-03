- performance is points / number of games for each jersey 
- Need to store points p for jersey r in game g
- Need to remove jersey r playing game g
- Need to return kth highest performing jersey


Store performances in a AVL tree (ranked by performance)

ranked_receiver(k):
	traverse the tree to find kth item
	tree needs to store n-items and values (mix of sequence and set avl tree)

we store a tree per game with scores for each jersey that played (set AVL tree with jersey as key)

then record(g, r, p):
	look up game root in dictionary of pointers (implemented in sequence AVL tree) O(log n )
	insert score into game for a set AVL tree O(log n)
	Update performance table by removing current node and adding it back with updated performance (it stores number of games, total points and we use cross multiplication for comparisons) O(log n)

clear(g, r):
	look up game root in dictionary of pointers O(log n)
	delete r from tree for g O(log n)
	update performance O(log n)
	