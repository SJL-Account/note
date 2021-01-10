
# 排序算法
参考文献：
https://www.cnblogs.com/onepixel/articles/7674659.html
https://www.cnblogs.com/chengxiao/p/6104371.html
![allsort.png](attachment:allsort.png)

## 1.冒泡排序

时间复杂度

最好 O(n)

最坏 O(n^2)

平均


空间复杂度 O(n)

![bubblesort.gif](attachment:bubblesort.gif)


```python
def bubble_sort(array):
    m = len(array)
    for i in range(m):
        for j in range(m-i-1):
            if array[j] > array[j+1]:
                array[j], array[j+1] = array[j+1], array[j]

array = [100,2,10,3,5,4,3,45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time bubble_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (array)
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    CPU times: user 35 µs, sys: 23 µs, total: 58 µs
    Wall time: 42 µs
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 10, 45, 100]


# 2.选择排序

时间复杂度

最好 O(n)

最坏 O(n^2)

平均


空间复杂度 O(n)

ACTION

![selectsort.gif](attachment:selectsort.gif)


```python
def choose_sort(array):
    m = len(array)
    for i in range(m):
        min_index = i
        for j in range (i+1, m):
            if array[j] < array[min_index]:
                min_index = j
        array[min_index], array[i] = array[i], array[min_index]
                
array = [100,2,10,3,5,4,3,45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time choose_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (array)
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    CPU times: user 33 µs, sys: 14 µs, total: 47 µs
    Wall time: 40.1 µs
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 10, 45, 100]


# 3.插入排序

时间复杂度

最好 O(n)

最坏 O(n^2)

平均


空间复杂度 O(n)

ACTION

![insertsort.gif](attachment:insertsort.gif)


```python
def insert_sort(array):
    m = len(array)
    for i in range(m):
        crt_val = array[i] 
        pre_i = i - 1
        while pre_i >=0 and array[pre_i] > crt_val:
            array[pre_i + 1] = array[pre_i]
            pre_i -= 1
        array[pre_i + 1] = crt_val
                
array = [100, 2, 10 ,3, 5, 4, 3, 45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time insert_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (array)
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    CPU times: user 22 µs, sys: 8 µs, total: 30 µs
    Wall time: 26.9 µs
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 10, 45, 100]


# 4.希尔排序

![shellsort.gif](attachment:shellsort.gif)


```python
def shell_sort(array):
    m = len(array)
    gap = m / 2
    while gap > 0:
        for i in range(gap, m):
            crt_val = array[i] 
            pre_i = i - gap
            while pre_i >=0 and array[pre_i] > crt_val:
                array[pre_i + gap] = array[pre_i]
                pre_i -= gap
            array[pre_i] = crt_val
        gap /= 2
                
array = [100, 2, 10 ,3, 5, 4, 3, 45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time shell_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (array)
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    CPU times: user 120 µs, sys: 112 µs, total: 232 µs
    Wall time: 121 µs
    -----------------------------------------
    after sorted array is [100, 100, 100, 100, 100, 100, 100, 5]


# 5.归并排序

![mergesort.gif](attachment:mergesort.gif)


```python
def merge_sort(array):
    """
    This function purpose is sort array by merge method.
    
    """
    m = len(array)
    if m < 2:
        return array
    mid = m / 2
    # divide 
    left_array = array[:mid]
    right_array = array[mid:]
    
    # inner sorted , outer unsorted
    left_sorted_array = merge_sort(left_array)
    right_sorted_array = merge_sort(right_array)
    
    #merge
    return merge(left_sorted_array, right_sorted_array)
    
def merge(left_array, right_array):
    
    merge_array = []
    left_len = len(left_array)
    right_len = len(right_array)
    
    i, j = 0, 0
    while i < left_len and j < right_len:
        if left_array[i] < right_array[j]:
            merge_array.append(left_array[i])
            i += 1
        else:
            merge_array.append(right_array[j])
            j += 1
    
    if i < left_len:
        merge_array.extend(left_array[i:])
    
    if j < right_len:
        merge_array.extend(right_array[j:])
    
    return merge_array

array = [100, 2, 10 ,3, 5, 4, 3, 45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time array = merge_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (array)

```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    CPU times: user 42 µs, sys: 13 µs, total: 55 µs
    Wall time: 46 µs
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 10, 45, 100]


# 6.快速排序

![quicksort.gif](attachment:quicksort.gif)


```python
def quick_sort(array, low, high):
    
    if low < high:
        pivot_i = partition(array, low, high)
        quick_sort(array, low, pivot_i - 1)
        quick_sort(array, pivot_i + 1, high)
    return array

def partition(array, low, high):
    
    i = low
    j = high
    pivot = i
    while i < j:
        print i, j
        # find first less than pivot
        while i < j and array[i] <= array[pivot]:
            i += 1
        array[j] = array[j]
        # find first great than pivot
        while i < j and array[j] >= array[pivot]:
            j -= 1
        array[i] = array[j]
    array[pivot], array[i] = array[i], array[pivot]
    return i
array = [100, 2, 10 ,3, 5, 4, 3, 45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time quick_sort(array, 0, len(array)-1)
print "-----------------------------------------"
print "after sorted array is %s" % (array)  
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    0 7
    0 6
    0 5
    0 1
    3 5
    CPU times: user 606 µs, sys: 600 µs, total: 1.21 ms
    Wall time: 625 µs
    -----------------------------------------
    after sorted array is [2, 10, 3, 5, 3, 4, 45, 100]

快速排序和归并排序的区别：
1.快速排序：前序遍历 归并排序：后序遍历
2.快速排序节点：外部有序，内部无序，归并排序节点：内部有序，外部无序
3.快速排序：轴点随机选 归并排序：轴点为二分中心
# 7.堆排序算法

堆化的步骤

![heapify.png](attachment:heapify.png)


```python
class HeapPriorityQueue:
    """
    Max heap priority queue.
    
    """
    def __init__(self, array):
        """
        The Constructor.
        
        """
        self.array = array
        self.heapify()
        
    def heapify(self,):
        """
        Heapify the array.
        
        """
        self.n = len(self.array)
        # 从非叶子节点开始遍历
        for i in range(self.n/2, -1, -1):
            self.adjust_heap(i, self.n)
    
    def remove_top(self,):
        
        if self.is_empty():
            return
        self.swap(0, self.n - 1)
        self.array.pop()
        self.n = len(self.array) 
        self.adjust_heap(0, self.n - 1)
        
    def is_empty(self, ):
        
        return len(self.array) == 0
    
    def swap(self, crt_i, crt_j):
        """
        Swap the value of index: i and j.
        
        """
        self.array[crt_i], self.array[crt_j] = self.array[crt_j], self.array[crt_i]
    
    def adjust_heap(self, crt_i, border_i):
        """
        Adjust the heap array order according to heap struct.
        
        """
        # 初始化节点数据
        left_node_i = crt_i * 2 + 1
        right_node_i = crt_i * 2 + 2
        bigger_i = crt_i
        
        # 选出最大的子节点
        if -1 < left_node_i < border_i:
            if self.array[left_node_i] > self.array[bigger_i]:
                bigger_i = left_node_i
            print "current node value :%s , left_node value: %s, bigger value: %s" \
                %(self.array[crt_i], self.array[left_node_i], self.array[bigger_i],)
        
        if -1 < right_node_i < border_i:
            if self.array[right_node_i] > self.array[bigger_i]:
                bigger_i = right_node_i
            print "current node value :%s , right_node value: %s, bigger value: %s" \
                %(self.array[crt_i], self.array[right_node_i], self.array[bigger_i],)
        
        # 与最大的子节点交换数据
        if crt_i != bigger_i:
            self.swap(crt_i, bigger_i)
            print "we have changed the order between crt node (index: %s, value: %s) " \
                    "and bigger leaf node (index: %s, value: %s)" \
                    % (crt_i, self.array[crt_i], bigger_i, self.array[bigger_i])
            self.adjust_heap(bigger_i, border_i)
    

    def heap_sort(self,):
        """
        Sort by heap.
        
        """
        m = self.n
        print "--------------sorted starting --------------- "
        while m > 0:
            self.array[0], self.array[m-1] = self.array[m-1], self.array[0]
            m -= 1
            print "after adjust sorted array: %s " % (self.array)
            self.adjust_heap(0, m)
            print "current sorted array: %s " % (self.array)
        print "--------------sorted ended --------------- "
```

![heapsort.gif](attachment:heapsort.gif)


```python
array = [100, 2, 10 ,3, 5, 4, 3, 45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
hpq = HeapPriorityQueue(array)
%time hpq.heap_sort()
print "-----------------------------------------"
print "after sorted array is %s" % (array)  
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    current node value :3 , left_node value: 45, bigger value: 45
    we have changed the order between crt node (index: 3, value: 45) and bigger leaf node (index: 7, value: 3)
    current node value :10 , left_node value: 4, bigger value: 10
    current node value :10 , right_node value: 3, bigger value: 10
    current node value :2 , left_node value: 45, bigger value: 45
    current node value :2 , right_node value: 5, bigger value: 45
    we have changed the order between crt node (index: 1, value: 45) and bigger leaf node (index: 3, value: 2)
    current node value :2 , left_node value: 3, bigger value: 3
    we have changed the order between crt node (index: 3, value: 3) and bigger leaf node (index: 7, value: 2)
    current node value :100 , left_node value: 45, bigger value: 100
    current node value :100 , right_node value: 10, bigger value: 100
    --------------sorted starting --------------- 
    after adjust sorted array: [2, 45, 10, 3, 5, 4, 3, 100] 
    current node value :2 , left_node value: 45, bigger value: 45
    current node value :2 , right_node value: 10, bigger value: 45
    we have changed the order between crt node (index: 0, value: 45) and bigger leaf node (index: 1, value: 2)
    current node value :2 , left_node value: 3, bigger value: 3
    current node value :2 , right_node value: 5, bigger value: 5
    we have changed the order between crt node (index: 1, value: 5) and bigger leaf node (index: 4, value: 2)
    current sorted array: [45, 5, 10, 3, 2, 4, 3, 100] 
    after adjust sorted array: [3, 5, 10, 3, 2, 4, 45, 100] 
    current node value :3 , left_node value: 5, bigger value: 5
    current node value :3 , right_node value: 10, bigger value: 10
    we have changed the order between crt node (index: 0, value: 10) and bigger leaf node (index: 2, value: 3)
    current node value :3 , left_node value: 4, bigger value: 4
    we have changed the order between crt node (index: 2, value: 4) and bigger leaf node (index: 5, value: 3)
    current sorted array: [10, 5, 4, 3, 2, 3, 45, 100] 
    after adjust sorted array: [3, 5, 4, 3, 2, 10, 45, 100] 
    current node value :3 , left_node value: 5, bigger value: 5
    current node value :3 , right_node value: 4, bigger value: 5
    we have changed the order between crt node (index: 0, value: 5) and bigger leaf node (index: 1, value: 3)
    current node value :3 , left_node value: 3, bigger value: 3
    current node value :3 , right_node value: 2, bigger value: 3
    current sorted array: [5, 3, 4, 3, 2, 10, 45, 100] 
    after adjust sorted array: [2, 3, 4, 3, 5, 10, 45, 100] 
    current node value :2 , left_node value: 3, bigger value: 3
    current node value :2 , right_node value: 4, bigger value: 4
    we have changed the order between crt node (index: 0, value: 4) and bigger leaf node (index: 2, value: 2)
    current sorted array: [4, 3, 2, 3, 5, 10, 45, 100] 
    after adjust sorted array: [3, 3, 2, 4, 5, 10, 45, 100] 
    current node value :3 , left_node value: 3, bigger value: 3
    current node value :3 , right_node value: 2, bigger value: 3
    current sorted array: [3, 3, 2, 4, 5, 10, 45, 100] 
    after adjust sorted array: [2, 3, 3, 4, 5, 10, 45, 100] 
    current node value :2 , left_node value: 3, bigger value: 3
    we have changed the order between crt node (index: 0, value: 3) and bigger leaf node (index: 1, value: 2)
    current sorted array: [3, 2, 3, 4, 5, 10, 45, 100] 
    after adjust sorted array: [2, 3, 3, 4, 5, 10, 45, 100] 
    current sorted array: [2, 3, 3, 4, 5, 10, 45, 100] 
    after adjust sorted array: [2, 3, 3, 4, 5, 10, 45, 100] 
    current sorted array: [2, 3, 3, 4, 5, 10, 45, 100] 
    --------------sorted ended --------------- 
    CPU times: user 3.15 ms, sys: 2.17 ms, total: 5.32 ms
    Wall time: 3.61 ms
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 10, 45, 100]


# 8.计数排序


```python
def counter_sort(array, max_val):
    
    m = max_val + 1
    bucket = [0] * m
    sorted_index = 0
    
    for elem in array:
        bucket[elem]+=1
    
    for i in range(m):
        while bucket[i] > 0:
            array[sorted_index] = i
            sorted_index += 1
            bucket[i] -= 1
            
array = [100, 2, 10 ,3, 5, 4, 3, 45] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time counter_sort(array, 100)
print "-----------------------------------------"
print "after sorted array is %s" % (array)          
```

    origin array is [100, 2, 10, 3, 5, 4, 3, 45]
    -------------- cost time  ---------------
    CPU times: user 51 µs, sys: 25 µs, total: 76 µs
    Wall time: 57 µs
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 10, 45, 100]


# 9.桶排序

![bucketsort.png](attachment:bucketsort.png)


```python
def bucket_sort(array, bucket_size=5):
    
    array_max = max(array)
    array_min = min(array)
    
    bucket_count = ((array_max - array_min) / bucket_size)+ 1
    print "bucket count: %s " % bucket_count
    buckets = [[] for _ in range(bucket_count)]
    for elem in array:
        print "current elem is %s ,index is %s" % (elem, (elem - array_min) / bucket_size)
        buckets[(elem - array_min) / bucket_size].append(elem)
    print buckets
    re_array = []
    for bucket in buckets:
        bucket.sort()
        re_array.extend(bucket)
    
    return re_array
        
array = [10, 2, 7 ,3, 5, 4, 3, 8] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time re_array = bucket_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (re_array) 
```

    origin array is [10, 2, 7, 3, 5, 4, 3, 8]
    -------------- cost time  ---------------
    bucket count: 2 
    current elem is 10 ,index is 1
    current elem is 2 ,index is 0
    current elem is 7 ,index is 1
    current elem is 3 ,index is 0
    current elem is 5 ,index is 0
    current elem is 4 ,index is 0
    current elem is 3 ,index is 0
    current elem is 8 ,index is 1
    [[2, 3, 5, 4, 3], [10, 7, 8]]
    CPU times: user 1.93 ms, sys: 1.32 ms, total: 3.26 ms
    Wall time: 2.03 ms
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 7, 8, 10]


# 10.基数排序

![radix_sort.gif](attachment:radix_sort.gif)


```python
def radix_sort(array):
    
    crt_b = 0
    max_num = max(array)
    max_b = len(str(max_num))
    
    while crt_b < max_b:
        buckets = [[] for _ in range(10)]
        for elem in array:
            buckets[int(elem / 10 ** crt_b) % 10].append(elem)
        
        array=[]
        for bucket in buckets:
            for elem in bucket:
                array.append(elem)
        crt_b += 1
    
    return array 
```


```python
array = [10000, 2, 7 ,3, 5, 4, 3, 8] # 排序数组
print "origin array is %s" % (array)
print "-------------- cost time  ---------------"
%time re_array = radix_sort(array)
print "-----------------------------------------"
print "after sorted array is %s" % (re_array) 
```

    origin array is [10000, 2, 7, 3, 5, 4, 3, 8]
    -------------- cost time  ---------------
    CPU times: user 134 µs, sys: 45 µs, total: 179 µs
    Wall time: 141 µs
    -----------------------------------------
    after sorted array is [2, 3, 3, 4, 5, 7, 8, 10000]

