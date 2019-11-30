---
title: Search Binary
date: 2019-07-02 19:43:00
tags: [algorithm, search]
---
## 问题
在一个有序的数组中,下标为l~r的区间内，查找value等于x的值出现的下标。

## 思路
- 函数头定义为:

    ```
    def binary_search(arr, l, r, x)：
    ```

- 结束条件为：

    如果找到则返回下标，如果没有找到返回-1

- 主要步骤：
    1. 获取l~r区间的中间位置下标mid，比较arr\[mid]与x
    2. 如果arr\[mid]大于x,则说明x只可能出现在左半边区间中
    3. 如果arr\[mid]小于x,则说明x只可能出现在右半边区间中
    4. 在待查找子区间中继续步骤1～4