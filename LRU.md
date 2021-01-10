

```python
class LinkNode:
    
    def __init__(self, key, val):
        self.key = key
        self.value = value
        self.pre = None
        self.next =  None
        

class LRUCache:
    
    def __init__(self, capicity):
        
        self.capicity = capicity
        self.map = {}
        self.head = LinkNode(0)
        self.tail = LinkNode(0)
        
    def get(self, key):
        
        if key in self.map:
            crt_node = self.map[key]
            self.pop_to_tail(crt_node)
            return crt_node
        return -1
    
    def put(self, key, value):
        
        if key in self.map:
            if len(self.map) == capicity:
                self.remove_first()
            crt_node = self.map[key]
            crt_node.value = value
            self.pop_to_tail(crt_node)
        else:
            node = LinkNode(key, value)
            self.map[key] = node
            self.add_to_tail(node) 
            
    
    def add_to_tail(self, node):
        
        last = self.tail.pre
        
        self.tail.next = node
        node.pre = self.tail
        
        node.next = last
        last.pre =  node
    
    def pop_to_tail(self, node)
        
        # 断链
        pre = node.pre
        next = node.next
        pre.next = next
        next.pre = pre 
        
        last = self.tail.pre
        # 链接
        last.next = node
        node.pre = last
        node.next =  self.tail
        self.tail.pre = node
        
        
    def remove_first(self,):
        pass
        
```


```python

```
