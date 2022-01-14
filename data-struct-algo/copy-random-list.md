### 【时间】

2022年1月14日

#### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

#### 【难度】

简单

#### 【题目】

请实现` copyRandomList `函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个` next `指针指向下一个节点，还有一个` random `指针指向链表中的任意节点或者` null`。




#### 【需要考虑的问题】

- random指针的复制



【方法一】

时间复杂度：O(n^2)

1、迭代链表，复制原始链表的每个节点，记录链表头节点和其random指针节点间的距离

2、设置链表的random指针



【方法二】

时间复杂度： O(n)，空间复杂度：O(n)

方法二使用空间获取时间的方式。

和方法一类似，只不过在第一次迭代链表时，使用hash表存储每个节点对应random节点，读取时，时间复杂度O(1)。



【方法三】

时间复杂度：O(n)

第一步：在链表的每个节点后N，复制一个N' ，组成链表：A -> A' -> B -> B' -> C -> C' -> D -> D'

第二步：复制random指针

第三步：拆分链表



#### 【解决过程】

方法三：

```go
/**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Next *Node
 *     Random *Node
 * }
 */

// 第一步：复制链表
func cloneNode(head *Node) {
	node := head
	for node != nil {
		temp := node.Next
		nodeClone := Node{
			Val: node.Val,
			Next: node.Next,
			Random: nil,
		}
		node.Next = &nodeClone
		nodeClone.Next = temp
		node = nodeClone.Next
	}
}


// 第二步：复制random
func connectRandomNode(head *Node) {
	node := head
	for node != nil {
		nodeClone := node.Next
		if node.Random != nil {
			nodeClone.Random = node.Random.Next
		}
		node = nodeClone.Next
	}
}

// 第三步：拆分链表
func reConnectList(head *Node) *Node {
	pNode := head
	var pCloneHead, pCloneNode *Node
	if pNode != nil {
		pCloneHead, pCloneNode = pNode.Next, pNode.Next
		pNode.Next = pCloneNode.Next
		pNode = pNode.Next
	}

	for pNode != nil {
		pCloneNode.Next = pNode.Next
		pCloneNode = pCloneNode.Next
		pNode.Next = pCloneNode.Next
		pNode = pNode.Next
	}
	return pCloneHead
}

func copyRandomList(head *Node) *Node {
	cloneNode(head)
	connectRandomNode(head)
	return reConnectList(head)
}
```

