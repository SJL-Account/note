
参考资料：https://blog.csdn.net/m0_37896278/article/details/105961824


```python
class Node(object):
    def __init__(self, node, char):
        self.childrens = {}
        self.parent = node
        self.has_word = False
        self.word = ""
        self.char = char
    def __str__(self,):
        return "parent: %s childrents: %s" % (self.parent, self.childrens)
```


```python
class Trie(object):
    
    def __init__(self,):
        
        self.root = Node(None, '/')
        self.__size = 0
        
    def add(self, word):
        
        crt_node = self.root
        for char in word:
            if char not in crt_node.childrens:
                crt_node.childrens[char] = Node(crt_node, char)
            crt_node = crt_node.childrens.get(char)
        
        crt_node.has_word = True
        crt_node.word = word
        self.__size += 1
        
    
    def show_tree(self, root):
        
        if not root.childrens:
            print root.word
            return
        
        for char in root.childrens:
            node = root.childrens[char] 
            self.show_tree(node)
    
    def contains(self, key):
        
        return bool(self.get_node(key))
    
    
    def get_node(self, key):
        
        crt_node = self.root
        for char in key:
            crt_node =  crt_node.childrens.get(char)
            if not crt_node:
                return None
        return crt_node if crt_node.has_word else None
    
    def start_with(self, prefix):
        
        crt_node = self.root
        for char in prefix:
            crt_node =  crt_node.childrens.get(char)
            if not crt_node:
                return False
        return True   
        
    def remove(self, key):
        """
            删除key对应节点
        """
        node = self.get_node(key)
        if not node:
            return
        self.__size -= 1
        # 存在子节点
        if node.childrens:
            node.has_word = False
            node.word = ""
        # 不存在子节点时从尾部开始删除
        else:
            while node.parent:
                del node.parent.childrens[node.char]
                if node.parent.has_word or node.parent.childrens:
                    break
                node = node.parent
```


```python
trie = Trie()
trie.add('abc')
trie.add('abd')
trie.add('ab2323')
trie.add('3223')
trie.start_with('ab4')
trie.remove('abc')
tire.show_tree(tire.root)
```
