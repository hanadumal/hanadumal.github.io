---
title: Sort Heap
date: 2019-07-02 16:11:53
tags: [algorithm, sort]
---

## 建堆的过程
1. 当前节点的，左右子节点，分别为2i+1, 2i + 2
2. (arr, n, i) arr为输入数组，n为数组大小，i为当前节点的index
3. 先比较i, 2i + 1节点的大小, 获取largest
4. 再比较largest和2i + 2节点的大小
5. 如果largest不等于i, 那么交换largest和i, 并且针对largest节点继续进行heapify

## 查找的过程
1. 从n-1至0], 也就是从底向顶，建立堆。
2. i 从n-1到0), 交换0和i的数据，恢复节点0的堆。
3. 结果为增序

## bin heap的定义
1. bin heap是一个完全二叉树，或近似完全二叉树
2. 父节点的value大于（小于)子节点的value
3. 每个节点的左右子树都是一个二叉堆（因为这条，所以建立堆的时候需要从bottom到top建立)

## 堆排序的时间复杂度，为什么比快排慢？
时间复杂度为O(nlog), heapify的时间复杂度为O(logn), 建立堆的复杂度为O(nlogn), 排序的时候需要n-1次循环，所以复杂度O(nlog), 整体复杂度O(nlogn)

堆排序需要将A[0]与A[n-1]进行交换，将A[0]重新下沉到合适的位置。每次新交换上来的A[0]十分小，能够呆在A[0]不需要交换的概率很低，需要经过多次比较和交换才能到达合适的位置。更好的办法是，每次只有1/2的概率需要移动。堆排序和快排虽然都是O(nlog)的时间复杂度，但是堆排序的常数更大。

## 参考
推荐这个网站上学算法：
> https://www.geeksforgeeks.org/heap-sort/

> https://blog.csdn.net/linkedin_39403967/article/details/75304241

> https://blog.csdn.net/MoreWindows/article/details/6709644

> https://ictar.xyz/2015/12/07/%E4%B9%9D%E5%A4%A7%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E5%8F%8A%E5%85%B6Python%E5%AE%9E%E7%8E%B0%E4%B9%8B%E5%A0%86%E6%8E%92%E5%BA%8F/

