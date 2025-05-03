
## Reverse linked list

#### 1.Iteratively (O(n) time, O(1) space)

```
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
	previous = None
	current = head
	while current:
		nxt = current.next
		current.next = previous
		previous = current
		current = nxt
	return previous
```


## Merging two linked lists

Nice idea of using dummy to start!

```
def mergeLinkedList(l1, l2):
	dummy = LinkedNode()
	tail = dummy
	while l1 and l2:
		if <condition to select l1>:
			tail.next = l1
			l1 = l1.next
		else:
			tail.next = l2
			l2 = l2.next
		tail = tail.next
	if l1:
		tail.next = l1
	else:
		tail.next = l2
	return dummy.next
```