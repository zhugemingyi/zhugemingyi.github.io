---
title: python查找算法
date: 2021-07-07 10:33:55
tags: [python,数据结构]
categories:
  - [python,数据结构,查找算法]
---

- 二分查找

<!--more-->

# 二分查找

```python
# 返回 x 在 arr 中的索引，如果不存在返回 -1
def binarySearch (arr, 0, len(arr)-1, x): 
    # 基本判断
    if r >= l: 
        mid = int(l + (r - l)/2)
        # 元素整好的中间位置
        if arr[mid] == x: 
            return mid 
        # 元素小于中间位置的元素，只需要再比较左边的元素
        elif arr[mid] > x: 
            return binarySearch(arr, l, mid-1, x) 
        # 元素大于中间位置的元素，只需要再比较右边的元素
        else: 
            return binarySearch(arr, mid+1, r, x) 
    else: 
        # 不存在
        return -1
```



![Binary_search_into_array](Binary_search_into_array.png)

# 参考文章

https://www.runoob.com/python3/python-binary-search.html
