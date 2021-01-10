
参考链接：https://blog.csdn.net/qq_29519041/article/details/81428934
        https://blog.csdn.net/lzq20115395/article/details/78906863


```python
class Node:
    """
    Huffman tree node.
    
    """
    def __init__(self, key, value):
        # store the node key
        self._key = key
        self._value = value
        self.left = None
        self.right = None

        
class HuffmanTree:
    """
    Huffman tree data struct.
    
    """
    def __init__(self, char_weight):
        """
        The Constructor.
        
        """
        self.nodes = [Node(key, char_weight[key]) for key in char_weight]
        self.dict_bin_by_key = {}
        self.init_tree()
        self.root = self.nodes[0] 
    
    def init_tree(self, ):
        """
        Initialize the tree.
        
        """
        
        # 迭代只剩一个根节点
        while len(self.nodes) != 1:
            # 根据权重值大小进行排序
            self.nodes.sort(key = lambda x: x._value, reverse=True)
            # 归并最小的2个节点
            crt_node = Node(key = self.nodes[-1]._key + self.nodes[-2]._key, 
                            value = self.nodes[-1]._value + self.nodes[-2]._value)
            # 将归并后的节点与字符节点建立关系 2 -> 1
            crt_node.left = self.nodes.pop(-1)
            crt_node.right = self.nodes.pop(-1)
            self.nodes.append(crt_node) 

        
    def bin_encode(self, node, bin_list):
        """
        binary encode.
        
        """
        # 叶子节点，字符节点
        if node and not node.left and not node.right:
            self.dict_bin_by_key[node._key] = bin_list[:]
            return
            
        bin_list.append(0)
        self.bin_encode(node.left, bin_list)
        bin_list.pop()
        
        bin_list.append(1)
        self.bin_encode(node.right, bin_list)
        bin_list.pop()
    
    def get_bin_codes(self, ):
        """
        Get all char bin binary.
        
        """
        self.bin_encode(self.root, [])
        return self.dict_bin_by_key
```


```python
word_dict = {'a': 20, 'b': 30, 'c': 200, 'd':12, 'e': 300}
hft = HuffmanTree(word_dict)
hft.get_bin_codes()
```




    {'a': [0, 0, 1, 1], 'b': [0, 0, 0], 'c': [0, 1], 'd': [0, 0, 1, 0], 'e': [1]}


