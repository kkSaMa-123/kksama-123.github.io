---
title: "南京大学智软院数据结构与算法复习"
date: 2025-01-11 00:00:00 +0800
category: "学习笔记"
excerpt: "数据结构与算法课程复习整理，覆盖伪代码、算法复杂度、基础数据结构、树、图、最短路、动态规划等内容。"
description: "数据结构与算法课程复习整理。"
---

## 伪代码
1. 为伪代码过程提供一个有效的名称，在开头指定输入和输出变量的名称（以及类型）。
2. 对块结构中的每个语句使用适当的缩进。
3. 对于流控制语句，使用 if-else。始终以 end-if 结束 if 语句。if、else 和 end-if 都应该在同一行垂直对齐。
4. 使用 ← 或者 ：= 运算符进行赋值语句， 使用 = 进行相等检查
5. 数组元素可以通过指定数组名称后跟方括号中的索引来表示。例如，A[i]
6. 循环使用 for 或 while 语句。始终以 end-for 结束 for 循环，以 end-while 结束 while
7. 两个或多个条件可以与 and 或 or 连接。使用not表示否。



```plain
Procedure  Insertion-Sort(A) 
In: An array A of n integers. 
Out: A permutation of that array A that is sorted (monotonic).

for i := 2 to A.length
   key := A[i]
   // Insert A[i] into the sorted subarray A[1 : i - 1] 
   j := i - 1 
   while j > 0 and A[j] > key 
         A[j + 1] := A[j]
         j := j - 1
   A[j + 1] := key
return A
```

## 算法基础分析
### Big O notation(符号)
###### Definition (O)
Given a function g(n) , we denote by O(g(n)) the following set of functions:O(g(n)) = {f(n) ∣ ∃c > 0,∃n<sub>0</sub> > 0,∀n ≥ n<sub>0</sub> : 0 ≤ f(n) ≤ c⋅g(n)}

Asymptotic upper bounds（渐近上界） — when we say f(n) is O(g(n)), we mean that f(n) grows no faster than a certain rate —> is asymptotically at most g(n).

• Ex.  
$ f(n) = 32n^2 + 17n + 1 $.  
$ f(n) $ is $ O(n^2 $).   



###### Big O notation abuses
O(g(n)) is actually a set of functions, but computer scientists often write f(n) = O(g(n)) instead of f(n)  ∈  O(g(n)).  
常常写等号而不是 $ \in $.

• Ex.  
Consider  f1(n) = 5n<sup>3</sup>  and f2(n) = 3n<sup>2</sup>.  
 We have f1(n) = O(n<sup>3</sup>) and f2(n) = O(n<sup>3</sup>).  
 But, do not conclude f1(n) = f2(n).

###### Big O notation with multiple variables
 f(m, n) is O(g(m, n)) if there exist constants c > 0, m<sub>0</sub>  ≥  0,and n<sub>0</sub> ≥  0 such that 0 ≤  f(m, n)  ≤  c · g (m, n)  for all n  ≥  n<sub>0</sub> and m  ≥  m<sub>0</sub>.

 • Ex.  f(m, n) = 32mn<sup>2</sup> + 17mn + 32n<sup>3</sup>.  
 ‣ f(m, n) is both O(mn<sup>2</sup> + n<sup>3</sup>) and O(mn<sup>3</sup>).  
 ‣ f(m, n) is neither O(n<sup>3</sup>) nor O(mn<sup>2</sup>)

### Big Ω notation
 Asymptotic lower bounds（渐近下界） — when we say f(n) is Ω(g(n)), we mean that f(n) grows at least as fast as a certain rate —>  is asymptotically at least g(n).

 Ex.  f(n) = 32n2 + 17n + 1.  
 ‣ f(n) is both Ω(n<sup>2</sup>) and Ω(n).

### Big Θ notation
Given a function g(n) , we denote by Θ(g(n)) the following set of functions: Θ(g(n)) = {f(n) ∣ ∃c<sub>1</sub> > 0,∃c<sub>2</sub> > 0,∃n<sub>0</sub> > 0,∀n ≥ n<sub>0</sub> : c<sub>1</sub>⋅g(n) ≤ f(n) ≤ c<sub>2</sub>⋅g(n)}



Asymptotic tight bounds（渐近紧确界）  When we say f(n) is Θ(g(n)), we mean that f(n) grows precisely at a certain rate  —> it is asymptotically equal to g(n)

### Small o and ω notation
o(g(n)) 是任意比g(n)严格小的，大于等于0  
$ o(g(n)) = \{f(n) ∣ ∀c > 0,∃n0 > 0,∀n ≥ n0 : 0 ≤ f(n) < c⋅g(n)\} $  
ω(g(n)) 是任意比g(n)严格大的  
$ ω(g(n)) = \{f(n) ∣ ∀c > 0,∃n0 > 0,∀n ≥ n0 : f(n) > c⋅g(n)\} $

### Asymptotic bounds and limits
Proposition.  If   $ \lim\limits_{n \rightarrow \infty} \frac{f(n)}{g(n)}=c $ for some constant $ 0  <  c  <  \infty $ then f(n) is Θ(g(n)).

## 基本数据结构
### Abstract Data Type (ADT)
A data structure usually provides an interface.

1. Often, the interface is also called an Abstract Data Type (ADT).
2. An ADT specifies what a data structure “can do” and “should do”, but not “how to do” them.

#### queue
1. first-in-first-out (FIFO) 
2. last-in-first-out (LIFO) 也就是 Stack
3. Double-Ended Queue (Deque) 前后都可以进出AddFirst(), AddLast(), RemoveFirst(), RemoveLast()

#### list
包括以下操作  
Size()  
Get(i)  
Set(i,x)  
Add(i,x)  
Remove(i)

如果用数组实现list，时间复杂度：  
Size()：always Θ(1)  
Get(i)：always Θ(1)  
Set(i,x)：always Θ(1)  
Add(i,x)：Θ(1) to Θ(n)  
Remove(i)：Θ(1) to Θ(n)  
利于做stack 不利于做FIFO或者Deque（可以用环形数组）

如果用链表实现list：  
Size()：always Θ(1)  
Get(i)：Θ(1) to Θ(n)  
Set(i,x)：Θ(1) to Θ(n)  
Add(i,x)：Θ(1) to Θ(n)  
Remove(i)：Θ(1) to Θ(n)  
适合stack（push pop head）和 FIFO ，不太适合Deque（删除最后一个节点的时间复杂度高）

deque可以用双链表。

### 应用
#### FIFO
```plain
ProcessIn(x): 
    FIFOqueue.add(x)
ProcessOut(): 
    FIFOqueue.remove()
```

#### Stack
括号匹配

```plain
 CheckParen(str):
    Stack s
    int i := 1
 while str[i] != NULL
    if str[i] is ‘(’ or ‘[’  or ‘{’
        s.push(str[i])
    if  str[i] is ‘)’ or ‘]’ or ‘}’
        if  s.empty()
            return false
        if  s.pop() and str[i] mismatch 
            return false 
    i++
 return s.empty()
```

函数的递归调用。使用尾递归可以减少内存开销。如下求最大公约数

```plain
EuclidGCDRec(m, n):
 if n = 0 
    return m
 else
    rem := m % n
return EuclidGCDRec(n, rem)
```

尾递归可以化为迭代：

```plain
EuclidGCDRec(m, n):
 while  true
    if  n = 0
        return m
    else
        rem := m % n
        m := n
        n := rem
```

## 分治
### MergeSort
```plain
MergeSort (A[1…n]): 
   if  n = 1: 
         sol[1…n]  :=  [1…n]   
   else
        solLeft[1…(n/2)] := MergeSort(A[1…(n/2)]) 
        solRright[1…(n/2)] := MergeSort(A[(n/2+1)…n])
        sol[1…n] :=  Merge(solLeft[1…(n/2)], solRight[1…(n/2)])  
   return sol[1…n]

Merge (A[1…n], B[1…m]): 
   Aindex := 1, Bindex := 1,  Result := []

   while Aindex <= A.length  and  Bindex <= B.length 
       if A[Aindex] <= B[Aindex]
            Result.AddLast(A[Aindex])
            Aindex := Aindex + 1
        else
            Result.AddLast(B[Bindex])
            Bindex := Bindex + 1
 // Copy the remaining elements of  A and B
   while  Aindex <= A.length
         Result.AddLast(A[Aindex])
         Aindex := Aindex + 1
    while  Bindex <= B.length
         Result.AddLast(B[Bindex])
         Bindex := Bindex + 1
    return Result
```

时间复杂度：  Θ(n ⋅ log n)

### 矩阵乘法
直接乘 $ Θ(n^3) $  
Strassen’s algorithm $ O(n^{\log_27}) $

### 主定理 Simple version of Master Theorem
$ T(n)=aT(\frac{n}{b})+f(n)\\ $

1. n是问题规模大小；
2. a是原问题的子问题个数；
3. n/b是每个子问题的大小，这里假设每个子问题有相同的规模大小；
4. f(n)是将原问题分解成子问题和将子问题的解合并成原问题的解的时间。

对于$ T(n)=aT(\frac{n}{b})+Θ(n^d)\\ $  
Then T(n) has the following asymptotic bounds:  
 $ T(n) =\begin{cases}Θ(n^d\lg n), a=b^d \\Θ(n^d), a<b^d\\ Θ(n^{\log_ba}),a>b^d\end{cases} $

### Reduce-and-Conquer
#### Binary Search
```plain
BinarySearch(A, x):
    left := 1, right := n
    while left <= right
        middle :=  (left+right)/2
        if  A[middle] = x
            return middle
        else if  A[middle] < x
            left := middle + 1
        else
            right := middle - 1
    return -1 //没找到
```

 T(n) = O(logn)

#### peak finding
```plain
PeakFinding(A):
    left := 1, right := n
    while left <= right
        middle :=  (left+right)/2
        if  middle > left  and  A[middle - 1] > A[middle]
            right := middle - 1
        else if  middle < right  and  A[middle + 1] > A[middle]
            left := middle + 1
        else
            return A[middle]
```

 in 2D 找最外圈加中间十字，来确定四个区域。

## 堆
### binary heap
We can use an array to represent a binary heap. Obtaining parent and children are easy:  
Parent of node u : $  ⌊idx_u/2⌋ $  
Left child of u : $ 2⋅idx_u $  
Right child of u : $  2⋅idx_u+1 $  
All in $ O(1) $ time!

以大根堆为例

1. 插入 在最末端插入一个数，这个数和父节点比较，如果这个数比上面大，往上交换，继续重复。
2. 删除根节点 删除后把最后一个节点提到这里，往下交换，交换两个子节点中大的那个，继续往下。

```plain
HeapExtractMax(A):
    max_item := A[1]
    A[1] = A[heap_size--]
    MaxHeapify(1, A)
    return max_item
MaxHeapify(idx, A):
    idx_l :=  2*idx,  idx_r := 2*idx + 1
    idx_max :=  ( idx_l <= heap_size and A[idx_l] > A[idx] ) ? idx_l : idx
    idx_max :=  ( idx_r <= heap_size and A[idx_r] > A[idx_max] ) ? idx_r : idx_max
    if idx_max != idx
        Swap (A[idx_max], A[idx])
        MaxHeapify(idx_max, A)

//heapsort
BuildMaxHeap(A):
    heap_size := n
    for i := Floor(n/2) down to 1
        MaxHeapify(i, A)
HeapSort(I):
    heap := BuildMaxHeap(I)
    for i := n down to 2
        cur_max := heap.HeapExtractMax()
        I[i] := cur_max
```

buildmaxheap Time Complexity: O(n)  
Time complexity of HeapSort is O(n·lg n)

### Priority Queue
## 排序
### Selection Sort
每次选出数组中最小的放在最前面

```plain
//迭代
SelectionSort(A):
    for i := 1 to A.length
        minIdx := i
        for j := i + 1 to A.length 
            if A[j] < A[minIdx]
                minIdx := j
        Swap(i, minIdx)
//递归
SelectionSortRec(A):
    if |A| = 1
        return A
    else 
        min := GetMinElement(A)
        A’ := RemoveElement(A, min)
        return Concatenate(min, SelectionSortRec(A’))
```

时间复杂度 Θ(n<sup>2</sup>)  
不是稳定排序（ppt这么说的）  
稳定排序是指在排序过程中，如果存在两个元素具有相同的值，则它们在排序前后的相对位置保持不变。换句话说，对于一组数据中相等的元素，如果在排序之前某个元素位于另一个元素之前，在排序之后这个顺序仍然保持不变。

### Bubble Sort
```plain
BubbleSort(A):
    for  i := A.length down to 2      
        for  j := 1 to i - 1
            if A[j] > A[j+1]
                Swap(A[j],  A[j+1])
```

Time complexity:Θ(n<sup>2</sup>)

注意到没有swap的时候代表前面已经排序好，可以优化

```plain
BubbleSortImporved(A):
    n := A.length
    repeat 
        swapped := false
        for  j := 1 to n - 1
            if A[j] > A[j+1]
                Swap(A[j],  A[j+1])
                swapped := true
        n := n - 1 
    until swapped = false
```

### Quick Sort
```plain
InplacePartition(A, p, r):
    i := p - 1
    for  j := p to r - 1
        if  A[j] <= A[r]
            i := i + 1
            Swap(A[i], A[j])
    Swap(A[i+1], A[r])
    return i + 1

QuickSort(A, p, r):
    if  p < r
        q := InplacePartition(A, p, r)
        QuickSort(A, p, q - 1)
        QuickSort(A, q + 1, r)
```

The performance of the best is Θ(n log n) , while the worst is Θ(n<sup>2</sup>)  
the average runtime of QuickSort is O(n log n)

random 随机取一个数组中的值作为中间值  
randomized quick sort is Θ(nlgn) , the expected running time is Θ(nlgn)  
In fact, runtime of RndQuickSort is O(nlogn) with high probability!

### Non-comparison-based sorting
#### Bucket sort
```plain
BucketSort(A, d):
    <L1, L2, ..., Ld>  = CreateBuckets(d)
    for  i :=1 to  A.length
        AssignToBucket(A[i])
    CombineBuckets(L1, L2, ..., Ld)
```

Total time complexity is Θ(n + d)

### Radix sort
```plain
RadixSort(A, d):
    for  i := 1 to d
       use-a-stable-sort-to-sort-A-on-digit-i
```

## 选择
### Selection Problem
找第i大的数

```plain
RndSelect(A,i):
    if  A.size = 1
        return A[1]
    else 
        q := RandomPartition(A)
        if  i = q
            return A[q]
    else if  i < q
        return RndSelect(A[1 … (q-1)], i)
    else
        return RndSelect(A[(q + 1) … A.size], i - q)
```

## 树
### binary tree (二叉树)
**binary tree (二叉树)**：有左右两个子节点  
**full binary tree （满二叉树）**：每一个节点有两个或没有子节点  
**complete binary tree (完全二叉树)**：每个级别（可能除了最后一个级别）都已完全填充，并且最后一个级别中的所有节点都尽可能靠左  
**perfect binary tree (完美⼆叉树)**：其中所有非叶节点都有两个子节点，并且所有叶子具有相同的深度  
**tree traversals 树的遍历**：   
Preorder traversal (先序遍历) 先root 再root.left 最后root.right  
Postorder traversal (后序遍历) 先root 再root.right 最后root.left  
Inorder traversal (中序遍历) 先root.left 再root 最后root.right

```plain
PreorderTrav(r):
    if r != NULL
        Visit(r)
        for each child u of r 
            PreorderTrav(u)

PostorderTrav(r):
    if r != NULL
        for each child u of r 
            PostorderTrav(u)
        Visit(r)

InorderTrav(r):
    if r != NULL
        InorderTrav(r.left)
        Visit(r)
        InorderTrav(r.right)
```

用迭代

```plain
InorderTravIter(r):
    Stack s
    s.push(Frame(r,  false))
    while  !s.empty()
        f = s.pop()
        if  f.node != NULL
            if  f.visit
                Visit(f.node)
            else
                s.push(Frame(f.node.right,  false))
                s.push(Frame(f.node, true))
                s.push(Frame(f.node.left,  false))
```

Level-order traversal of trees

```plain
LevelorderTrav(r):
    if r != NULL 
    Queue q
    q.add(r)
    while  !q.empty()
        node := q.remove()
        if  node != NULL
            Visit(node)
            q.add(node.left)
            q.add(node.right)
```

## 搜索树
### 二叉搜索树
1. 二叉搜索树是二叉树，满足：
    1. 若它的左子树不为空，则左子树上所有节点的值都小于根节点的值
    2. 若它的右子树不为空，则右子树上所有节点的值都大于根节点的值
    3. 它的左右子树也分别为二叉搜索树
2. 插入
    1. 树为空，则直接新增节点，赋值给root指针
    2. 树不为空，按二叉搜索树性质查找插入的位置，插入新节点（记录父节点，判断插入的节点应该在父节点的左子树还是右子树）
3. 删除  
首先查找元素是否在二叉搜索树中，如果不存在，则返回, 否则要删除的结点可能分下面四种情况：  
a. 要删除的结点无孩子结点  
b. 要删除的结点只有左孩子结点  
c. 要删除的结点只有右孩子结点  
d. 要删除的结点有左、右孩子结点

看似删除节点有4种情况，但实际上a和b和c可以合并，这样就只有2种情况了：  
a:待删除的结点无孩子/只有一个孩子：删除结点并使父亲结点指向被删除结点的孩子结点（无孩子视为孩子是空结点，任意指向一个即可）  
b:待删除的结点有左右孩子：采用替换法，寻找删除结点右子树的最小结点（右子树最左结点），将最小结点的值和删除结点的值替换，然后删除最小结点（此时最小结点，要么没有孩子，要么只有一个孩子，符合a情况可以直接删除）

[https://blog.csdn.net/bang___bang_/article/details/130869356](https://blog.csdn.net/bang___bang_/article/details/130869356)

### treaps
Given a set of nodes with distinct key values and distinct priority values, a unique Treap is determined.  
插入时，先按照二叉树规则插入，后进行旋转，使权重小的在上面。

### Red-Black Tree
红黑树：

1. 节点是红色或黑色
2. 根是黑色
3. 叶子节点（外部节点，空节点）都是黑色，这里的叶子节点指的是最底层的空节点（外部节点），下图中的那些null节点才是叶子节点，null节点的父节点在红黑树里不将其看作叶子节点
4. 红色节点的子节点都是黑色
    1. 红色节点的父节点都是黑色
    2. 从根节点到叶子节点的所有路径上不能有 2 个连续的红色节点
5. 从任一节点到叶子节点的所有路径都包含相同数目的黑色节点

红黑树的查找，插入和删除操作，时间复杂度都是O(logN)。  
[https://blog.csdn.net/cy973071263/article/details/122543826](https://blog.csdn.net/cy973071263/article/details/122543826)



### Skip List
```plain
Insert(L,x):
    level := 1, done := false
    while !done
        Insert x into level k list.
        Flip a fair coin:
        With probability 1/2   done := true
        With probability 1/2   k := k + 1
```

## 散列表（哈希表）
hash函数就是根据key计算出应该存储地址的位置，而哈希表是基于哈希函数建立的一种查找表  
两个key有同样的哈希值可以用链表存储。

### Design hash functions
考虑因素：  
1.计算散列地址所需要的时间（即hash函数本身不要太复杂）  
2.关键字的长度  
3.表长  
4.关键字分布是否均匀，是否有规律可循  
5.设计的hash函数在满足以上条件的情况下尽量减少冲突

### open addressing
如果一个对应位置已经有值了，再重新计算存到另外的位置。  
删除操作时要用一个delete状态防止出错。

## 平摊分析
Amortized analysis  
[https://blog.csdn.net/touzani/article/details/1696399](https://blog.csdn.net/touzani/article/details/1696399)

## 并查集
### Linked-list implementation
find和union速度慢

### Rooted-tree implementation
注意可以在find的时候把中途的都指向root，节约后续查找的时间。

## 图
### 图的表示
邻接矩阵、邻接表各有优劣选择使用。

### BFS
```plain
BFSSkeleton(G, s):
    for  each u in V
        u.dist := INF,  u.discovered := False  
        s.dist := 0,  s.discovered := True
    Q.enque(s)
    while  !Q.empty()
        u := Q.dequeue()
        for each edge (u, v) in E
            if !v.discovered
                v.dist := u.dist + 1
                v.discovered := True
                Q.enque(v)
```

### DFS
```plain
DFSSkeleton(G, s):
    s.visited := True
    for each edge (s, v) in E
        if  !v.visited
            DFSSkelecton(G, v)
DFSIterSkeleton(G, s):
    Stack Q
    Q.push(s)
    while !Q.empty()
        u := Q.pop()
        if  !u.visited
            u.visited := True
            for each edge (u, v) in E
                Q.push(v)
```

## DFS的应用
### Directed Acyclic Graphs (有向无环图)
输出DAG的拓扑序  
用DFS，把离开节点的顺序由大到小排序即可

**A source node** is a node with no incoming edges;  
**A sink node** is a node with no outgoing edges.

### (Strongly) Connected Components
## 最小生成树
Minimum Spanning Trees (MST)

### Kruskal
从所有边中找最小边，连通两个还没连通元素，直到连接了所有的元素。

```plain
KruskalMST(G,w):
    A :=  ∅
    Sort edges into weight increasing order
    for each edge (u,v) taken in weight increasing order
        if  adding edge (u,v) does not form cycle in A
            A := A ∪{(u,v)} 
    return A
```

### Prim
从一个点出发，找最小边，然后组成一个集合，每次找集合中的最小边连通外面的点，直到全部的点都在集合中。

```plain
PrimMST(G,w):
    A := ∅
    Cx := {x}
    while  Cx is not a spanning tree
        Find MWOE (u, v) of Cx
        A := A∪{(u, v)} 
        Cx := Cx∪{v}
    return A
```

### Borůvka
从所有点出发找各自最小边，组成集合，再从各自集合出发找。

## 贪心策略
given a problem, build up a solution piece by piece, always choosing the next piece that offers the most obvious and immediate benefit.  
每一步选最优。

## 单源最短路径
Single-Source Shortest Path (SSSP)

### Dijkstra
无负边

```plain
DijkstraSSSP(G, s):
    for each u in V
        u.dist := INF, u.parent := NIL
    s.dist := 0
    Build priority queue Q based on dist
    while  !Q.empty()
        u := Q.ExtractMin()
        for each edge (u,v) in E
            if  v.dist > u.dist + w(u, v) 
                v.dist := u.dist + w(u, v)
                v.parent := u
                Q.UpdateKey(v)
```

### Bellman-Ford
可以有负边，重复n-1次，如果最后还能出现更短路径，说明有负边。

```plain
BellmanFordSSSP(G, s): 
    for  each u in V
        u.dist := INF, u.parent := NIL
    s.dist := 0
    repeat n - 1 times
        for each edge (u, v) in E
            if v.dist > u.dist + w(u, v)
                v.dist := u.dist + w(u, v)
                v.parent := u
        for each edge (u, v) in E
            if v.dist > u.dist + w(u, v)
                return “negative circles”
```

## 全源最短路径
All-Pairs Shortest Path

### Floyd-Warshall
```plain
//这里是弗洛伊德算法的核心部分 
    //k为中间点 
    for(k = 0; k < G.vexnum; k++){//G.vexnum为顶点数
        //v为起点 
        for(v = 0 ; v < G.vexnum; v++){
            //w为终点 
            for(w =0; w < G.vexnum; w++){
                if(D[v][w] > (D[v][k] + D[k][w])){
                    D[v][w] = D[v][k] + D[k][w];//更新最小路径 
                    P[v][w] = P[v][k];//更新最小路径中间顶点 
                }
            }
        }
    }
```

## 动态规划
Dynamic Programming

### 编辑距离
```plain
EditDistDP(A[1…m],B[1…n]): 
    for i := 0 to m
        dist[i, 0] := i
    for j := 0 to n
        dist[0, j] := j
    for i := 1 to m
        for j := 1 to n
            delDist := dist[i - 1, j] + 1
            insDist := dist[i, j - 1] + 1
            subDist := dist[i - 1, j - 1] + Diff(A[i], B[j])
            dist[i, j] := Min(delDist, insDist, subDist)
    return dist
```

### 作业题coins
题目：给定一个金额和一些硬币面值，找到有多少种不同的方式可以使用这些硬币组合成这个金额。  
INPUT：

> 5  
1 2 5
>

OUTPUT：

> 4
>

> 5 = 5  
5 = 2 + 2 + 1  
5 = 2 + 1 + 1 + 1  
5 = 1 + 1 + 1 + 1 + 1
>

设 dp[i] 表示使用给定硬币可以组合成金额 i 的不同方式的数量。这里 i 的取值范围是从 0 到目标金额 amount，所以会创建一个长度为 amount + 1 的数组（比如目标金额是 5，那数组长度就是 6，对应表示金额 0 到 5 的情况）来存储这些状态值。dp[0]=1,因为0元只有一种组合。  
当我们有了 coin 这个面值的硬币后，要去思考如何用它来凑出不同的金额。从 coin 这个金额本身开始（因为金额小于 coin 的话，当前这枚硬币就没办法参与组合了），一直到目标金额 amount，对于每一个金额 i（i >= coin）：能组成金额 i 的不同方式数量 dp[i] 应该等于在没考虑当前这枚 coin 硬币时能组成金额 i 的方式数量（也就是 dp[i] 原来的值），再加上如果使用了这枚 coin 硬币后能组成金额 i 的方式数量，而使用了这枚 coin 硬币后，其实就是之前已经算好的能组成金额 i - coin 的方式数量（因为 i - coin 的组合方式再加上这枚 coin 硬币就可以组成金额 i 了），所以状态转移方程就是 dp[i] += dp[i - coin]。

```cpp
#include <iostream>
using namespace std;
bool dp[100005];
int main()
{
    int n = 0;
    int *a = new int[n + 5];
    int sum = 0;
    while (cin >> a[n])
    {
        sum += a[n];
        n++;
    }
    if (sum % 2 == 1)
    {
        cout << "0";
        return 0;
    }
    else
    {
        int target = sum / 2;

        dp[0] = true;
        for (int i = 0; i < n; i++)
        {
            for (int j = target; j >= a[i]; j--)
            {
                dp[j] |= dp[j - a[i]];
            }
        }
        cout << dp[target];
    }
}
```

