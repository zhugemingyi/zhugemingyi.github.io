---
title: python排序算法
date: 2021-07-05 09:19:10
tags: [python,数据结构]
categories:
  - [python,数据结构,排序算法]
---

- 快速排序
- 冒泡排序
- 归并排序
- 希尔排序
- 排序算法复杂度总结

<!--more-->

# 快速排序



```python
def bubbleSort(arr):
    n = len(arr)
    # 遍历所有数组元素
    for i in range(n):
        # Last i elements are already in place
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1] :
                arr[j], arr[j+1] = arr[j+1], arr[j]
```

快速排序使用分治法策略来把一个序列分为较小和较大的2个子序列，然后递归地排序两个子序列。

步骤为：

<!--more-->

- 挑选基准值：从数列中挑出一个元素，称为"基准";
- 分割：重新排序数列，所有比基准值小的元素摆放在基准前面，所有比基准值大的元素摆在基准后面（与基准值相等的数可以到任何一边）。在这个分割结束之后，对基准值的排序就已经完成;
- 递归排序子序列：递归地将小于基准值元素的子序列和大于基准值元素的子序列排序。

递归到最底部的判断条件是数列的大小是零或一，此时该数列显然已经有序。

选取基准值有数种具体方法，此选取方法对排序的时间性能有决定性影响。

![quickSort](quickSort.gif)

# 冒泡排序

```python
def bubbleSort(arr):
    n = len(arr)
    # 遍历所有数组元素
    for i in range(n):
        # Last i elements are already in place
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1] :
                arr[j], arr[j+1] = arr[j+1], arr[j]
```

冒泡排序重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢"浮"到数列的顶端。

![bubbleSort](bubbleSort.gif)

# 堆排序

```python
def heapify(arr, n, i): 
    largest = i  
    l = 2 * i + 1     # left = 2*i + 1 
    r = 2 * i + 2     # right = 2*i + 2 
    if l < n and arr[i] < arr[l]: 
        largest = l 
    if r < n and arr[largest] < arr[r]: 
        largest = r 
    if largest != i: 
        arr[i],arr[largest] = arr[largest],arr[i]  # 交换
        heapify(arr, n, largest) 
def heapSort(arr):	# main
    n = len(arr) 
    # Build a maxheap. 
    for i in range(n, -1, -1): 
        heapify(arr, n, i) 
    # 一个个交换元素
    for i in range(n-1, 0, -1): 
        arr[i], arr[0] = arr[0], arr[i]   # 交换
        heapify(arr, i, 0) 
```

堆积是一个近似完全二叉树的结构，并同时满足堆积的性质：即子结点的键值或索引总是小于（或者大于）它的父节点。堆排序可以说是一种利用堆的概念来排序的选择排序。

![heapSort](heapSort.gif)

# 归并排序

```python
def merge(arr, l, m, r): 
    n1 = m - l + 1
    n2 = r- m 
    # 创建临时数组
    L = [0] * (n1)
    R = [0] * (n2)
    # 拷贝数据到临时数组 arrays L[] 和 R[] 
    for i in range(0 , n1): 
        L[i] = arr[l + i] 
    for j in range(0 , n2): 
        R[j] = arr[m + 1 + j] 
    # 归并临时数组到 arr[l..r] 
    i = 0     # 初始化第一个子数组的索引
    j = 0     # 初始化第二个子数组的索引
    k = l     # 初始归并子数组的索引
    while i < n1 and j < n2 : 
        if L[i] <= R[j]: 
            arr[k] = L[i] 
            i += 1
        else: 
            arr[k] = R[j] 
            j += 1
        k += 1
    # 拷贝 L[] 的保留元素
    while i < n1: 
        arr[k] = L[i] 
        i += 1
        k += 1
    # 拷贝 R[] 的保留元素
    while j < n2: 
        arr[k] = R[j] 
        j += 1
        k += 1
def mergeSort(arr,l,r):	# eg:mergeSort(arr,0,len(arr)-1)
    if l < r: 
        m = int((l+(r-1))/2)
        mergeSort(arr, l, m) 
        mergeSort(arr, m+1, r) 
        merge(arr, l, m, r) 
```

归并排序是创建在归并操作上的一种有效的排序算法。该算法是采用分治法（的一个非常典型的应用。

分治法:

- 分割：递归地把当前序列平均分割成两半。
- 集成：在保持元素顺序的同时将上一步得到的子序列集成到一起（归并）。

![mergeSort](mergeSort.gif)

# 希尔排序

```python
def shellSort(arr): 
    n = len(arr)
    gap = int(n/2)
    while gap > 0: 
        for i in range(gap,n): 
            temp = arr[i] 
            j = i 
            while  j >= gap and arr[j-gap] >temp: 
                arr[j] = arr[j-gap] 
                j -= gap 
            arr[j] = temp 
        gap = int(gap/2)
```

希尔排序，也称递减增量排序算法，是插入排序的一种更高效的改进版本。但希尔排序是非稳定排序算法。

希尔排序的基本思想是：先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录"基本有序"时，再对全体记录进行依次直接插入排序。

![Sorting_shellsort_anim](Sorting_shellsort_anim.gif)

# 拓扑排序

# 计数排序

# 排序算法复杂度总结

![排序算法复杂度总结](排序算法复杂度总结.png)

# 参考文章

https://www.runoob.com/python3/python-quicksort.html

https://www.runoob.com/python3/python-bubble-sort.html

https://www.runoob.com/python3/python-heap-sort.html

https://www.runoob.com/python3/python-merge-sort.html

https://www.runoob.com/python3/python-shellsort.html

https://blog.csdn.net/z_feng12489/article/details/94634897	shellsort

https://blog.csdn.net/str_lyc/article/details/109273738	总结

