
# 1.判断2个链表是否有交集


```python
def getIntersectionNode(self, headA, headB):
    """
    :type head1, head1: ListNode
    :rtype: ListNode
    """

    lA = headA
    lB = headB
    # a+c+b = b+c+a
    while lA != lB:
        lA =  lA.next if lA else headB
        lB =  lB.next if lB else headA

    return lA
```

# 2.反转链表


```python
def reverseList(self, head):
    """
    :type head: ListNode
    :rtype: ListNode
    """

    pre = None
    cur = head
    while cur:
        next = cur.next
        cur.next = pre
        pre = cur
        cur = next

    return pre
```

# 3.合并2个有序链表


```python
def mergeTwoLists(self, l1, l2):
    """
    :type l1: ListNode
    :type l2: ListNode
    :rtype: ListNode
    """

    if not l1:
        return l2
    if not l2:
        return l1

    if l1.val < l2.val :
        l1.next = self.mergeTwoLists(l1.next, l2)
        return l1
    else:
        l2.next = self.mergeTwoLists(l2.next, l1)
        return l2

            
```

# 4.链表去重


```python
def deleteDuplicates(self, head):
    """
    :type head: ListNode
    :rtype: ListNode
    """

    cur = head
    while cur and cur.next:
        if cur.val == cur.next.val:
            cur.next = cur.next.next
        else:
            cur = cur.next

    return head
```

# 5.删除倒数第n个节点


```python
def removeNthFromEnd(self, head, n):
    """
    :type head: ListNode
    :type n: int
    :rtype: ListNode
    """

    p_fast = head
    p_slow = head
    while n >= 0:
        p_fast = p_fast.next
        n -= 1
    while p_fast:
        p_fast = p_fast.next
        p_slow = p_slow.next
    p_slow.next = p_slow.next.next

    return head       
```

# 6.交换相邻的2个节点


```python
def swapPairs(self, head):
    """
    :type head: ListNode
    :rtype: ListNode
    """

    if not head or not head.next:
        return head
    tmp = head.next
    head.next = self.swapPairs(tmp.next)
    tmp.next = head

    return tmp
```

# 7.链表排序

## 7.1 冒泡排序


```python
def swap(node1, node2):
    """
    swap the value of node1 and node2.
    
    """
    
    node1.data, node2.data = node2.data, node1.data
```


```python
def bubble_sort(head):
    """
    bubble sort link list version.
    
    """
    i_node = head
    j_node = None
    # 第一层驱动循环，什么都不做
    while i_node:
        j_node = head
        # 第二层比较循环，和数组相比不能定位尾部坐标
        while j_node.next:
            if j_node.data > j_node.next.data:
                swap(j_node, j_node.next)
            j_node = j_node.next
        i_node = i_node.next   
```

## 7.2 选择排序


```python
def choose_sort(head):
    """
    choose sort link list version.
    
    """
    
    i_node = head
    j_node = None
    min_node = None
    
    # 外层驱动节点
    while i_node:
        min_node = i_node
        j_node = i_node.next
        while j_node:
            if min_node.data > j_node.data:
                min_node = j_node
            j_node = j_node.next
        swap(min_node, i_node)
        i_node = i_node.next


```

## 7.3 归并排序


```python
def merge(left, right):
    
    # 哑节点
    head = LinkNode(-1)
    tmp = head
    
    while left and right:
        
        if left.data < right.data:
            tmp.next = left
            # current point move 1 step
            tmp = tmp.next
            # left link point move 1 step
            left = left.next
        else:
            tmp.next = right
            # current point move 1 step
            tmp = tmp.next
            # right link point move 1 step
            right = right.next 
    
    # left节点有剩余
    if left:
        tmp.next = left
    
    # right节点有剩余
    if right:
        tmp.next = right
        
        
    return head.next

def merge_sort(head):
    
    if not head or not head.next:
        return head
    
    p_slow = head
    p_fast = head
    
    # 快慢指针搜索中心位置
    while p_fast.next and p_fast.next.next:
        p_fast = p_fast.next.next
        p_slow = p_slow.next
    
    mid = p_slow.next
    p_slow.next = None
    
    left_head = merge_sort(head)
    right_head = merge_sort(mid)
    
    return merge(left_head, right_head)
```


```python

```
