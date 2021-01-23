

```python
class LinkNode:
    
    def __init__(self, key, value):
        
        self.key = key
        self.value = value
        self.pre = None
        self.next =  None
    
    def __str__(self,):
        
        return "{%s: %s}" % (self.key, self.value)
        
class LRUCache:
    
    def __init__(self, capicity):
        
        self.capicity = capicity
        self.map = {}
        self.head = LinkNode(0, 0)
        self.tail = LinkNode(0, 0)
        self.head.next = self.tail
        self.tail.pre = self.head
        
    def get(self, key):
        
        if key in self.map:
            crt_node = self.map[key]
            self.pop_to_tail(crt_node)
            return crt_node.value
        return -1
    
    def put(self, key, value):
        
        # key 在 map中
        if key in self.map:
            # 容量不够了
            if len(self.map) == self.capicity:
                # 删除头节点，最少使用的节点
                self.remove_first()
            crt_node = self.map[key]
            crt_node.value = value
            self.pop_to_tail(crt_node)
        else:
            node = LinkNode(key, value)
            self.map[key] = node
            self.add_to_tail(node) 
            
    
    def add_to_tail(self, node):
        """
        Add current node to last node.
        """
        
        # 求解最后一个节点
        last = self.tail.pre
        
        # 插入，将node插入last和最后的哑节点之间
        last.next = node
        node.pre = last
        node.next =  self.tail
        self.tail.pre = node
    
    def pop_to_tail(self, node):
        """
        Pop current node to last node.
        
        """
        
        # 断链 断掉当前node节点
        pre = node.pre
        next = node.next
        pre.next = next
        next.pre = pre 
        
        self.add_to_tail(node)
        
        
    def remove_first(self,):
        """
        Remove first node.
        
        """
        second = self.head.next.next
        self.head.next = second
        second.pre = self.head
    
    def print_link_list(self,):
        """
        Show double direction link list.
        
        """
        crt_node  = self.head
        node_str_list = []
        while crt_node.next:
            node_str_list.append("{%s: %s} " % (crt_node.key, crt_node.value))
            crt_node = crt_node.next
        print "<->".join(node_str_list)
            
        
```

结果展示


```python
lru = LRUCache(10)
lru.put('a', 10)
lru.put('b', 11)
lru.put('c', 12)
lru.put('d', 13)
lru.put('e', 14)
lru.put('f', 15)
lru.put('a', 16)
lru.get('e')
lru.print_link_list()
```

    {0: 0} <->{b: 11} <->{c: 12} <->{d: 13} <->{f: 15} <->{a: 16} <->{e: 14} 



```python

```
