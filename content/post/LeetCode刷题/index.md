---
title: "LeetCode刷题"
date: 2025-06-30T12:19:55+08:00
draft: false
author: "acyanbird"
summary: "LeetCode刷题"
# tags: [""]
---

## 面试 150 题目
[链接](https://leetcode.cn/studyplan/top-interview-150/)

### 一些小tips
#### 时间和空间复杂度

### 合并两个有序数组
给你两个按 非递减顺序 排列的整数数组 nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。

请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。

有三个解法，目前用 py 先写着吧比较简单
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums1[m:] = nums2
        nums1.sort()
```

把 nums2 放到结尾，直接用快速排序

或者直接建立一个 sorted 数组
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        sorted = []
        p1, p2 = 0, 0
        while p1 < m or p2 < n:
            if p1 == m: # put rest of p2 in sorted
                sorted.append(nums2[p2])
                p2 += 1
            elif p2 == n:
                sorted.append(nums1[p1])
                p1 += 1
            elif nums1[p1] < nums2[p2]:# smaller one into sorted
                sorted.append(nums1[p1])
                p1 += 1
            else:
                sorted.append(nums2[p2])
                p2 += 1
        nums1[:] = sorted
```

四种情况，在第一或者第二数组跑完之后把另一个数组直接往后加，下面的两个看哪个小就append

#### 27 移除元素
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。

假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：

    更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。
    返回 k。

对于 Python3 使用双指针。说是删除，其实删除很费时间。

双指针其实就是两个数，分别代表两个 index，表示数组中第几个数的意思。
比如这里，我们让 a 代表一个 index，b 代表一个index
然后我们让 a 一直往后移动，相当于 nums[a] 从数组第一个数遍历到最后一个数。
当且仅当我们发现 nums[a] != val 的时候，我们把这个数拷贝到 b 指向的位置，默认 b 是从 0 开始的，然后 b += 1 指向下一个位置。

这样我们就保证了前 b 个数，就是我们要的结果。不重复的数。反正就是 a 不等于 val 就赋值到前面 b 指向的数字。然后计算 b 的大小就知道有不等于 val 的输出了
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        a = 0
        b = 0
        while a < len(nums):
            if nums[a] != val:# should move forward
                nums[b] = nums[a]
                b += 1
            a += 1
        return b
```