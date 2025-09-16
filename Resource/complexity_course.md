# Python算法复杂度完整教程
*Time Complexity & Space Complexity 深度解析*

---

## 📚 课程目录

1. [什么是算法复杂度](#1-什么是算法复杂度)
2. [时间复杂度详解](#2-时间复杂度详解)
3. [空间复杂度详解](#3-空间复杂度详解)
4. [Big O 记号法](#4-big-o-记号法)
5. [复杂度分析方法](#5-复杂度分析方法)
6. [实例分析](#6-实例分析)
7. [常见数据结构复杂度](#7-常见数据结构复杂度)
8. [练习题目](#8-练习题目)

---

## 1. 什么是算法复杂度

### 1.1 定义
算法复杂度是衡量算法效率的重要指标，分为两个维度：
- **时间复杂度（Time Complexity）**：算法执行所需的时间
- **空间复杂度（Space Complexity）**：算法执行所需的内存空间

### 1.2 为什么要学习复杂度分析？
```python
# 例子：两种查找最大值的方法

# 方法1：遍历查找 - O(n)
def find_max_v1(arr):
    max_val = arr[0]
    for i in range(1, len(arr)):
        if arr[i] > max_val:
            max_val = arr[i]
    return max_val

# 方法2：排序后取最后一个 - O(n log n)
def find_max_v2(arr):
    sorted_arr = sorted(arr)
    return sorted_arr[-1]

# 哪种方法更好？复杂度分析告诉我们答案！
```

---

## 2. 时间复杂度详解

### 2.1 什么是时间复杂度
时间复杂度描述了算法执行时间与输入规模 n 之间的关系。

### 2.2 常见时间复杂度类型

#### 📈 复杂度增长图表
```
执行时间
    ↑
    |     O(n!)
    |    /
    |   O(2^n)
    |  /
    | O(n²)
    |/
    |     O(n log n)
    |    O(n)
    |   O(log n)
    |  O(1)
    |_________________→ 输入规模 n
   0
```

#### 2.2.1 O(1) - 常数时间
```python
def get_first_element(arr):
    """无论数组多大，都只需要一步操作"""
    return arr[0] if arr else None

# 执行时间不随输入规模变化
```

#### 2.2.2 O(log n) - 对数时间
```python
def binary_search(arr, target):
    """二分查找：每次都将搜索范围减半"""
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# 时间复杂度：O(log n)
# 1000个元素最多需要10次比较 (log₂1000 ≈ 10)
```

#### 2.2.3 O(n) - 线性时间
```python
def linear_search(arr, target):
    """线性查找：需要遍历所有元素"""
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# 最坏情况下需要检查所有n个元素
```

#### 2.2.4 O(n log n) - 线性对数时间
```python
def merge_sort(arr):
    """归并排序：分治算法的典型例子"""
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])      # T(n/2)
    right = merge_sort(arr[mid:])     # T(n/2)
    
    return merge(left, right)         # O(n)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# 时间复杂度：T(n) = 2T(n/2) + O(n) = O(n log n)
```

#### 2.2.5 O(n²) - 平方时间
```python
def bubble_sort(arr):
    """冒泡排序：双重循环的典型例子"""
    n = len(arr)
    for i in range(n):           # 外循环 n 次
        for j in range(0, n-i-1):  # 内循环 n-i-1 次
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

# 总操作次数：n × n = n²
```

#### 2.2.6 O(2^n) - 指数时间
```python
def fibonacci_recursive(n):
    """递归斐波那契：指数时间的典型例子"""
    if n <= 1:
        return n
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)

# 每个调用都产生两个子调用，形成二叉树
# 时间复杂度：O(2^n)
```

### 2.3 时间复杂度对比表

| 复杂度 | n=1 | n=10 | n=100 | n=1000 | 增长速度 |
|--------|-----|------|-------|--------|----------|
| O(1) | 1 | 1 | 1 | 1 | 常数 |
| O(log n) | 1 | 3 | 7 | 10 | 很慢 |
| O(n) | 1 | 10 | 100 | 1000 | 线性 |
| O(n log n) | 1 | 33 | 700 | 10000 | 中等 |
| O(n²) | 1 | 100 | 10000 | 1000000 | 快 |
| O(2^n) | 2 | 1024 | 2^100 | 2^1000 | 极快 |

---

## 3. 空间复杂度详解

### 3.1 什么是空间复杂度
空间复杂度描述了算法执行过程中所需的内存空间与输入规模的关系。

### 3.2 空间复杂度的组成
- **输入空间**：存储输入数据所需的空间
- **辅助空间**：算法执行过程中额外需要的空间
- **输出空间**：存储输出结果所需的空间

**空间复杂度 = 辅助空间复杂度**（通常我们关注的是辅助空间）

### 3.3 常见空间复杂度类型

#### 3.3.1 O(1) - 常数空间
```python
def reverse_array_inplace(arr):
    """原地反转数组，只使用常数额外空间"""
    left, right = 0, len(arr) - 1
    
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    
    return arr

# 只使用了两个额外变量，空间复杂度：O(1)
```

#### 3.3.2 O(n) - 线性空间
```python
def reverse_array_copy(arr):
    """创建新数组来反转，需要线性额外空间"""
    return arr[::-1]  # 创建了一个新的数组

def fibonacci_dp(n):
    """动态规划解斐波那契，使用数组存储中间结果"""
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)  # 需要 n+1 个空间
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

# 空间复杂度：O(n)
```

#### 3.3.3 O(log n) - 对数空间
```python
def binary_search_recursive(arr, target, left, right):
    """递归二分查找，调用栈深度为 log n"""
    if left > right:
        return -1
    
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)

# 递归深度：log n，空间复杂度：O(log n)
```

---

## 4. Big O 记号法

### 4.1 什么是 Big O
Big O 记号法是描述算法复杂度的数学符号，关注的是增长的趋势。

### 4.2 Big O 的特点
1. **忽略常数**：O(2n) = O(n)
2. **忽略低阶项**：O(n² + n) = O(n²)
3. **关注最坏情况**：描述算法性能的上界

### 4.3 实例分析
```python
def example_algorithm(arr):
    # Step 1: 常数时间操作
    result = 0                    # O(1)
    
    # Step 2: 单层循环
    for i in range(len(arr)):     # O(n)
        result += arr[i]
    
    # Step 3: 双层循环
    for i in range(len(arr)):     # O(n²)
        for j in range(len(arr)):
            if arr[i] > arr[j]:
                result += 1
    
    # Step 4: 常数时间操作
    return result                 # O(1)

# 总时间复杂度：O(1) + O(n) + O(n²) + O(1) = O(n²)
```

---

## 5. 复杂度分析方法

### 5.1 分析步骤
1. **识别基本操作**：找出算法中的核心操作
2. **计算执行次数**：分析基本操作的执行频率
3. **用Big O表示**：忽略常数和低阶项

### 5.2 循环分析法则

#### 5.2.1 单层循环
```python
# 简单循环：O(n)
for i in range(n):
    print(i)

# 步长为2的循环：仍然是O(n)
for i in range(0, n, 2):
    print(i)
```

#### 5.2.2 嵌套循环
```python
# 双层循环：O(n²)
for i in range(n):
    for j in range(n):
        print(i, j)

# 三角形循环：仍然是O(n²)
for i in range(n):
    for j in range(i):
        print(i, j)
```

#### 5.2.3 分治算法
```python
def power(base, exp):
    """快速幂算法：O(log n)"""
    if exp == 0:
        return 1
    elif exp % 2 == 0:
        temp = power(base, exp // 2)
        return temp * temp
    else:
        return base * power(base, exp - 1)

# 每次递归都将问题规模减半，深度为log n
```

---

## 6. 实例分析

### 6.1 查找算法对比
```python
# 1. 线性查找
def linear_search(arr, target):
    """
    时间复杂度：O(n) - 最坏情况需要遍历所有元素
    空间复杂度：O(1) - 只使用常数额外空间
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# 2. 二分查找（要求数组有序）
def binary_search(arr, target):
    """
    时间复杂度：O(log n) - 每次将搜索范围减半
    空间复杂度：O(1) - 只使用常数额外空间
    """
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# 3. 哈希查找
def hash_search_setup(arr):
    """
    预处理：时间复杂度O(n)，空间复杂度O(n)
    查找：时间复杂度O(1)，空间复杂度O(1)
    """
    hash_map = {}
    for i, val in enumerate(arr):
        hash_map[val] = i
    return hash_map

def hash_search(hash_map, target):
    return hash_map.get(target, -1)
```

### 6.2 排序算法对比
```python
# 1. 冒泡排序
def bubble_sort(arr):
    """
    时间复杂度：O(n²) - 双层循环
    空间复杂度：O(1) - 原地排序
    """
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

# 2. 快速排序
def quick_sort(arr):
    """
    时间复杂度：平均O(n log n)，最坏O(n²)
    空间复杂度：O(log n) - 递归调用栈
    """
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quick_sort(left) + middle + quick_sort(right)

# 3. 归并排序
def merge_sort(arr):
    """
    时间复杂度：O(n log n) - 稳定的分治算法
    空间复杂度：O(n) - 需要额外数组存储
    """
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)
```

### 6.3 动态规划实例
```python
# 斐波那契数列的三种实现

# 1. 递归实现（效率极低）
def fib_recursive(n):
    """
    时间复杂度：O(2^n) - 指数级增长
    空间复杂度：O(n) - 递归调用栈深度
    """
    if n <= 1:
        return n
    return fib_recursive(n-1) + fib_recursive(n-2)

# 2. 动态规划（自底向上）
def fib_dp(n):
    """
    时间复杂度：O(n) - 线性计算
    空间复杂度：O(n) - 存储所有中间结果
    """
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

# 3. 空间优化的动态规划
def fib_optimized(n):
    """
    时间复杂度：O(n) - 线性计算
    空间复杂度：O(1) - 只存储前两个值
    """
    if n <= 1:
        return n
    
    prev2, prev1 = 0, 1
    
    for i in range(2, n + 1):
        current = prev1 + prev2
        prev2, prev1 = prev1, current
    
    return prev1
```

---

## 7. 常见数据结构复杂度

### 7.1 数组（Array/List）
| 操作 | 时间复杂度 | 空间复杂度 |
|------|------------|------------|
| 访问 | O(1) | O(1) |
| 搜索 | O(n) | O(1) |
| 插入 | O(n) | O(1) |
| 删除 | O(n) | O(1) |

```python
class Array:
    def __init__(self):
        self.data = []
    
    def get(self, index):        # O(1)
        return self.data[index]
    
    def search(self, value):     # O(n)
        for i, val in enumerate(self.data):
            if val == value:
                return i
        return -1
    
    def insert(self, index, value):  # O(n)
        self.data.insert(index, value)
    
    def delete(self, index):     # O(n)
        del self.data[index]
```

### 7.2 链表（Linked List）
| 操作 | 时间复杂度 | 空间复杂度 |
|------|------------|------------|
| 访问 | O(n) | O(1) |
| 搜索 | O(n) | O(1) |
| 插入 | O(1) | O(1) |
| 删除 | O(1) | O(1) |

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def search(self, value):     # O(n)
        current = self.head
        while current:
            if current.data == value:
                return current
            current = current.next
        return None
    
    def insert_at_head(self, value):  # O(1)
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node
    
    def delete_node(self, node):      # O(1) - 给定节点
        if node.next:
            node.data = node.next.data
            node.next = node.next.next
```

### 7.3 栈（Stack）
| 操作 | 时间复杂度 | 空间复杂度 |
|------|------------|------------|
| Push | O(1) | O(1) |
| Pop | O(1) | O(1) |
| Peek | O(1) | O(1) |
| Search | O(n) | O(1) |

```python
class Stack:
    def __init__(self):
        self.items = []
    
    def push(self, item):        # O(1)
        self.items.append(item)
    
    def pop(self):               # O(1)
        if not self.is_empty():
            return self.items.pop()
        return None
    
    def peek(self):              # O(1)
        if not self.is_empty():
            return self.items[-1]
        return None
    
    def is_empty(self):          # O(1)
        return len(self.items) == 0
```

### 7.4 队列（Queue）
| 操作 | 时间复杂度 | 空间复杂度 |
|------|------------|------------|
| Enqueue | O(1) | O(1) |
| Dequeue | O(1) | O(1) |
| Front | O(1) | O(1) |
| Search | O(n) | O(1) |

```python
from collections import deque

class Queue:
    def __init__(self):
        self.items = deque()
    
    def enqueue(self, item):     # O(1)
        self.items.append(item)
    
    def dequeue(self):           # O(1)
        if not self.is_empty():
            return self.items.popleft()
        return None
    
    def front(self):             # O(1)
        if not self.is_empty():
            return self.items[0]
        return None
```

### 7.5 哈希表（Hash Table）
| 操作 | 平均时间复杂度 | 最坏时间复杂度 | 空间复杂度 |
|------|---------------|---------------|------------|
| 搜索 | O(1) | O(n) | O(n) |
| 插入 | O(1) | O(n) | O(n) |
| 删除 | O(1) | O(n) | O(n) |

```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]
    
    def _hash(self, key):        # O(1)
        return hash(key) % self.size
    
    def put(self, key, value):   # 平均 O(1)
        index = self._hash(key)
        bucket = self.table[index]
        
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return
        
        bucket.append((key, value))
    
    def get(self, key):          # 平均 O(1)
        index = self._hash(key)
        bucket = self.table[index]
        
        for k, v in bucket:
            if k == key:
                return v
        
        raise KeyError(key)
```

### 7.6 二叉搜索树（Binary Search Tree）
| 操作 | 平均时间复杂度 | 最坏时间复杂度 | 空间复杂度 |
|------|---------------|---------------|------------|
| 搜索 | O(log n) | O(n) | O(1) |
| 插入 | O(log n) | O(n) | O(1) |
| 删除 | O(log n) | O(n) | O(1) |

```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

class BST:
    def __init__(self):
        self.root = None
    
    def search(self, val):       # 平均 O(log n)
        return self._search(self.root, val)
    
    def _search(self, node, val):
        if not node or node.val == val:
            return node
        
        if val < node.val:
            return self._search(node.left, val)
        else:
            return self._search(node.right, val)
    
    def insert(self, val):       # 平均 O(log n)
        self.root = self._insert(self.root, val)
    
    def _insert(self, node, val):
        if not node:
            return TreeNode(val)
        
        if val < node.val:
            node.left = self._insert(node.left, val)
        else:
            node.right = self._insert(node.right, val)
        
        return node
```

### 7.7 数据结构选择指南

```python
# 根据需求选择合适的数据结构

def choose_data_structure():
    """
    选择指南：
    
    1. 需要快速随机访问 → 数组/列表
    2. 频繁插入删除 → 链表
    3. 后进先出 → 栈
    4. 先进先出 → 队列
    5. 快速查找 → 哈希表
    6. 有序数据 → 二叉搜索树
    7. 优先级处理 → 堆
    """
    pass

# 性能对比示例
import time
import random

def performance_comparison():
    """比较不同数据结构的性能"""
    n = 10000
    data = list(range(n))
    random.shuffle(data)
    
    # 列表查找
    start = time.time()
    for i in range(1000):
        target = random.randint(0, n-1)
        target in data  # O(n) 查找
    list_time = time.time() - start
    
    # 集合查找
    data_set = set(data)
    start = time.time()
    for i in range(1000):
        target = random.randint(0, n-1)
        target in data_set  # O(1) 查找
    set_time = time.time() - start
    
    print(f"列表查找时间: {list_time:.4f}秒")
    print(f"集合查找时间: {set_time:.4f}秒")
    print(f"性能提升: {list_time/set_time:.1f}倍")
```

---

## 8. 练习题目

### 8.1 基础练习

#### 题目1：分析复杂度
```python
def mystery_function_1(n):
    result = 0
    for i in range(n):
        for j in range(i):
            result += 1
    return result

# 问题：分析上述函数的时间复杂度和空间复杂度
# 答案：时间复杂度 O(n²)，空间复杂度 O(1)
```

#### 题目2：优化算法
```python
def find_duplicates_v1(arr):
    """找出数组中的重复元素 - 版本1"""
    duplicates = []
    for i in range(len(arr)):
        for j in range(i+1, len(arr)):
            if arr[i] == arr[j] and arr[i] not in duplicates:
                duplicates.append(arr[i])
    return duplicates

# 任务：优化上述算法，提高时间复杂度
# 提示：使用哈希表
```

#### 题目3：递归复杂度
```python
def mystery_function_2(n):
    if n <= 1:
        return 1
    return mystery_function_2(n-1) + mystery_function_2(n-2) + mystery_function_2(n-3)

# 问题：分析上述递归函数的时间复杂度
# 答案：O(3^n) - 每次递归产生3个子调用
```

### 8.2 中级练习

#### 题目4：两数之和
```python
def two_sum_v1(nums, target):
    """暴力解法"""
    for i in range(len(nums)):
        for j in range(i+1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
    return []

# 任务1：分析时间和空间复杂度
# 任务2：设计O(n)时间复杂度的解法
# 任务3：比较两种方法的优缺点
```

#### 题目5：数组去重
```python
def remove_duplicates_v1(arr):
    """保持原顺序的数组去重 - 版本1"""
    result = []
    for item in arr:
        if item not in result:
            result.append(item)
    return result

# 任务：设计更高效的去重算法
# 要求：保持元素的原始顺序
# 提示：考虑使用哈希表 + 列表
```

#### 题目6：矩阵搜索
```python
def search_matrix_v1(matrix, target):
    """在m×n矩阵中搜索目标值 - 版本1"""
    for row in matrix:
        for element in row:
            if element == target:
                return True
    return False

# 已知：矩阵每行从左到右递增，每列从上到下递增
# 任务：设计O(m+n)的搜索算法
# 提示：从右上角或左下角开始搜索
```

### 8.3 高级练习

#### 题目7：第K大元素
```python
def find_kth_largest_v1(nums, k):
    """找到数组中第k大的元素 - 版本1"""
    nums.sort()
    return nums[len(nums) - k]

# 任务1：分析上述解法的复杂度
# 任务2：设计平均O(n)时间复杂度的解法
# 提示：使用快速选择算法
```

#### 题目8：LRU缓存
```python
class LRUCache:
    """设计LRU(最近最少使用)缓存"""
    def __init__(self, capacity):
        self.capacity = capacity
        # 任务：实现get()和put()方法
        # 要求：两个操作都必须在O(1)时间内完成
        pass
    
    def get(self, key):
        # 获取key对应的value
        # 如果存在，将其移动到最前面
        pass
    
    def put(self, key, value):
        # 插入或更新key-value对
        # 如果超过容量，删除最久未使用的项
        pass

# 提示：使用哈希表 + 双向链表
```

#### 题目9：合并K个排序链表
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def merge_k_lists_v1(lists):
    """合并k个排序链表 - 版本1"""
    result = None
    for lst in lists:
        result = merge_two_lists(result, lst)
    return result

def merge_two_lists(l1, l2):
    dummy = ListNode(0)
    current = dummy
    
    while l1 and l2:
        if l1.val <= l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    
    current.next = l1 or l2
    return dummy.next

# 任务1：分析版本1的时间复杂度
# 任务2：设计O(n log k)的优化解法
# 提示：使用分治算法或最小堆
```

### 8.4 实战练习答案

#### 答案1：find_duplicates优化
```python
def find_duplicates_v2(arr):
    """优化版本：使用哈希表"""
    seen = set()
    duplicates = set()
    
    for item in arr:
        if item in seen:
            duplicates.add(item)
        else:
            seen.add(item)
    
    return list(duplicates)

# 时间复杂度：O(n) -> 比原来的O(n³)大幅提升
# 空间复杂度：O(n) -> 用空间换时间
```

#### 答案2：two_sum优化
```python
def two_sum_v2(nums, target):
    """哈希表解法"""
    num_map = {}  # 值 -> 索引
    
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_map:
            return [num_map[complement], i]
        num_map[num] = i
    
    return []

# 时间复杂度：O(n) -> 从O(n²)优化到O(n)
# 空间复杂度：O(n) -> 需要额外哈希表存储
```

#### 答案3：remove_duplicates优化
```python
def remove_duplicates_v2(arr):
    """高效去重，保持顺序"""
    seen = set()
    result = []
    
    for item in arr:
        if item not in seen:
            seen.add(item)
            result.append(item)
    
    return result

# 时间复杂度：O(n) -> 从O(n²)优化到O(n)
# 空间复杂度：O(n) -> 需要集合和结果列表
```

#### 答案4：search_matrix优化
```python
def search_matrix_v2(matrix, target):
    """从右上角开始搜索"""
    if not matrix or not matrix[0]:
        return False
    
    row, col = 0, len(matrix[0]) - 1
    
    while row < len(matrix) and col >= 0:
        current = matrix[row][col]
        if current == target:
            return True
        elif current > target:
            col -= 1  # 当前值太大，向左移动
        else:
            row += 1  # 当前值太小，向下移动
    
    return False

# 时间复杂度：O(m + n) -> 从O(m × n)优化
# 空间复杂度：O(1)
```

#### 答案5：find_kth_largest优化
```python
def find_kth_largest_v2(nums, k):
    """快速选择算法"""
    def quickselect(left, right, k_smallest):
        if left == right:
            return nums[left]
        
        # 分区操作
        pivot_index = partition(left, right)
        
        if k_smallest == pivot_index:
            return nums[k_smallest]
        elif k_smallest < pivot_index:
            return quickselect(left, pivot_index - 1, k_smallest)
        else:
            return quickselect(pivot_index + 1, right, k_smallest)
    
    def partition(left, right):
        pivot = nums[right]
        i = left
        
        for j in range(left, right):
            if nums[j] <= pivot:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
        
        nums[i], nums[right] = nums[right], nums[i]
        return i
    
    # 第k大 = 第(n-k+1)小
    return quickselect(0, len(nums) - 1, len(nums) - k)

# 平均时间复杂度：O(n) -> 从O(n log n)优化
# 最坏时间复杂度：O(n²)
# 空间复杂度：O(1)
```

#### 答案6：LRU缓存实现
```python
class Node:
    def __init__(self, key=0, val=0):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

class LRUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}  # key -> node
        
        # 创建虚拟头尾节点
        self.head = Node()
        self.tail = Node()
        self.head.next = self.tail
        self.tail.prev = self.head
    
    def add_to_head(self, node):
        """在头部添加节点"""
        node.prev = self.head
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node
    
    def remove_node(self, node):
        """删除节点"""
        node.prev.next = node.next
        node.next.prev = node.prev
    
    def move_to_head(self, node):
        """移动节点到头部"""
        self.remove_node(node)
        self.add_to_head(node)
    
    def remove_tail(self):
        """删除尾部节点"""
        last_node = self.tail.prev
        self.remove_node(last_node)
        return last_node
    
    def get(self, key):
        """O(1)时间获取"""
        if key in self.cache:
            node = self.cache[key]
            self.move_to_head(node)
            return node.val
        return -1
    
    def put(self, key, value):
        """O(1)时间插入/更新"""
        if key in self.cache:
            # 更新现有节点
            node = self.cache[key]
            node.val = value
            self.move_to_head(node)
        else:
            # 添加新节点
            new_node = Node(key, value)
            
            if len(self.cache) >= self.capacity:
                # 删除尾部节点
                tail = self.remove_tail()
                del self.cache[tail.key]
            
            self.cache[key] = new_node
            self.add_to_head(new_node)

# 时间复杂度：get()和put()都是O(1)
# 空间复杂度：O(capacity)
```

### 8.5 性能测试工具

#### 复杂度测试框架
```python
import time
import matplotlib.pyplot as plt
import random

class ComplexityTester:
    """算法复杂度测试工具"""
    
    def __init__(self):
        self.results = {}
    
    def test_algorithm(self, func, data_generator, sizes, name):
        """测试算法在不同输入规模下的性能"""
        times = []
        
        for size in sizes:
            data = data_generator(size)
            
            # 预热
            func(data)
            
            # 测试
            start_time = time.perf_counter()
            func(data)
            end_time = time.perf_counter()
            
            times.append(end_time - start_time)
        
        self.results[name] = (sizes, times)
        return sizes, times
    
    def plot_results(self):
        """绘制性能对比图"""
        plt.figure(figsize=(12, 8))
        
        for name, (sizes, times) in self.results.items():
            plt.plot(sizes, times, marker='o', label=name)
        
        plt.xlabel('输入规模 (n)')
        plt.ylabel('执行时间 (秒)')
        plt.title('算法性能对比')
        plt.legend()
        plt.grid(True)
        plt.show()
    
    def compare_complexity(self, sizes, times, expected_complexity):
        """验证实际复杂度是否符合预期"""
        # 计算增长率
        ratios = []
        for i in range(1, len(sizes)):
            time_ratio = times[i] / times[i-1]
            size_ratio = sizes[i] / sizes[i-1]
            ratios.append(time_ratio / size_ratio)
        
        avg_ratio = sum(ratios) / len(ratios)
        
        print(f"平均增长率: {avg_ratio:.2f}")
        print(f"预期复杂度: {expected_complexity}")
        
        # 复杂度验证
        if expected_complexity == "O(1)":
            return avg_ratio < 1.1
        elif expected_complexity == "O(n)":
            return 0.9 < avg_ratio < 1.1
        elif expected_complexity == "O(n²)":
            return 1.5 < avg_ratio < 2.5
        else:
            return True

# 使用示例
def test_sorting_algorithms():
    """测试排序算法性能"""
    tester = ComplexityTester()
    
    def random_data(size):
        return [random.randint(1, 1000) for _ in range(size)]
    
    sizes = [100, 200, 400, 800, 1600]
    
    # 测试冒泡排序
    tester.test_algorithm(
        lambda arr: bubble_sort(arr.copy()),
        random_data,
        sizes,
        "冒泡排序 O(n²)"
    )
    
    # 测试快速排序
    tester.test_algorithm(
        lambda arr: quick_sort(arr.copy()),
        random_data,
        sizes,
        "快速排序 O(n log n)"
    )
    
    # 测试Python内置排序
    tester.test_algorithm(
        lambda arr: sorted(arr),
        random_data,
        sizes,
        "内置排序 O(n log n)"
    )
    
    tester.plot_results()
```

### 8.6 面试常见问题

#### Q1: 如何选择合适的算法？
```python
def algorithm_selection_guide():
    """
    选择算法的考虑因素：
    
    1. 时间复杂度 vs 空间复杂度
       - 时间敏感：选择时间复杂度低的算法
       - 空间受限：选择空间复杂度低的算法
    
    2. 数据规模
       - 小数据集：简单算法可能更好
       - 大数据集：必须考虑复杂度
    
    3. 数据特征
       - 已排序：可以使用二分查找
       - 随机分布：哈希表效果好
       - 有重复：需要考虑去重策略
    
    4. 硬件限制
       - CPU密集：优化时间复杂度
       - 内存受限：优化空间复杂度
       - 缓存友好：考虑数据局部性
    """
    
    # 实际决策示例
    def choose_search_algorithm(data_size, is_sorted, memory_limit):
        if data_size < 100:
            return "线性查找 - 简单有效"
        elif is_sorted:
            return "二分查找 - O(log n)"
        elif memory_limit > data_size:
            return "哈希表 - O(1)查找"
        else:
            return "线性查找 - 内存受限"
```

#### Q2: 如何优化算法性能？
```python
def optimization_strategies():
    """
    算法优化策略：
    
    1. 时间优化技巧
       - 预处理：提前计算常用结果
       - 缓存：避免重复计算
       - 早期终止：满足条件立即返回
       - 分治：将问题分解为子问题
    
    2. 空间优化技巧
       - 原地算法：复用输入空间
       - 滚动数组：只保存必要的历史数据
       - 位操作：用位来压缩存储
    
    3. 实用优化示例
    """
    
    # 示例1：斐波那契优化
    def fib_optimized_demo():
        # 原始递归：O(2^n)时间，O(n)空间
        def fib_recursive(n):
            if n <= 1: return n
            return fib_recursive(n-1) + fib_recursive(n-2)
        
        # 备忘录优化：O(n)时间，O(n)空间
        def fib_memo(n, memo={}):
            if n in memo: return memo[n]
            if n <= 1: return n
            memo[n] = fib_memo(n-1, memo) + fib_memo(n-2, memo)
            return memo[n]
        
        # 空间优化：O(n)时间，O(1)空间
        def fib_space_optimized(n):
            if n <= 1: return n
            prev2, prev1 = 0, 1
            for i in range(2, n+1):
                curr = prev1 + prev2
                prev2, prev1 = prev1, curr
            return prev1
    
    # 示例2：字符串匹配优化
    def string_matching_demo():
        # 暴力匹配：O(nm)
        def brute_force(text, pattern):
            for i in range(len(text) - len(pattern) + 1):
                if text[i:i+len(pattern)] == pattern:
                    return i
            return -1
        
        # KMP算法：O(n+m)
        def kmp_search(text, pattern):
            # 构建前缀表
            def build_lps(pattern):
                lps = [0] * len(pattern)
                length = 0
                i = 1
                
                while i < len(pattern):
                    if pattern[i] == pattern[length]:
                        length += 1
                        lps[i] = length
                        i += 1
                    else:
                        if length != 0:
                            length = lps[length - 1]
                        else:
                            lps[i] = 0
                            i += 1
                return lps
            
            lps = build_lps(pattern)
            i = j = 0
            
            while i < len(text):
                if text[i] == pattern[j]:
                    i += 1
                    j += 1
                
                if j == len(pattern):
                    return i - j
                elif i < len(text) and text[i] != pattern[j]:
                    if j != 0:
                        j = lps[j - 1]
                    else:
                        i += 1
            return -1

# 学习建议和总结
def learning_summary():
    """
    复杂度分析学习要点：
    
    1. 理论基础
       - 掌握Big O记号法
       - 理解最坏、平均、最好情况
       - 熟悉常见复杂度类型
    
    2. 分析技巧
       - 识别循环结构
       - 分析递归关系
       - 考虑数据结构操作
    
    3. 实践应用
       - 比较不同算法
       - 选择合适的数据结构
       - 优化瓶颈代码
    
    4. 持续提升
       - 多做算法题
       - 分析开源代码
       - 关注性能测试
    """
    
    print("🎯 学习目标检查清单：")
    checklist = [
        "✅ 能够分析简单算法的时间复杂度",
        "✅ 能够分析简单算法的空间复杂度", 
        "✅ 理解常见数据结构的复杂度",
        "✅ 能够选择合适的算法解决问题",
        "✅ 能够优化算法性能",
        "✅ 能够进行算法性能测试"
    ]
    
    for item in checklist:
        print(item)

if __name__ == "__main__":
    print("🚀 Python算法复杂度课程完成！")
    print("📖 继续练习，加深理解")
    learning_summary()
```

---

## 📝 课程总结

### 核心概念回顾
1. **时间复杂度**：衡量算法执行时间与输入规模的关系
2. **空间复杂度**：衡量算法所需内存空间与输入规模的关系  
3. **Big O记号法**：描述算法复杂度上界的数学工具
4. **复杂度分析**：通过分析算法结构来确定其复杂度

### 学习要点
- 掌握常见复杂度：O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ)
- 理解不同数据结构的复杂度特征
- 学会选择合适的算法和数据结构
- 培养优化算法的思维

### 下一步学习建议
1. **深入学习**：动态规划、图算法、高级数据结构
2. **实践练习**：LeetCode、HackerRank等平台刷题
3. **性能调优**：学习profiling工具，实际项目优化
4. **算法设计**：学习算法设计技巧和模式

**记住**：复杂度分析是算法学习的基础，熟练掌握后将大大提升你的编程能力和问题解决能力！

---