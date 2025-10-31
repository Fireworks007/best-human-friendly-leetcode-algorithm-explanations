# Remove Duplicates from Sorted Array II  
**Category / 分类:** Array / Two Pointers  
**Difficulty / 难度:** Medium  
**LeetCode:** [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

---

## 💡 Problem Statement / 题目描述  

**English:**  
Given an integer array `nums` sorted in non-decreasing order,  
remove some duplicates **in-place** such that each unique element appears at most twice.  
Return the new length of the modified array.

**中文：**  
给定一个按非递减顺序排序的整数数组 `nums`，  
要求原地删除部分重复元素，使得每个元素最多出现两次。  
返回修改后数组的新长度。

---

## 🧠 Idea / 解题思路  

**English:**  
We use the **Two Pointers** technique — one pointer (`fast`) scans the array,  
and the other pointer (`slow`) writes the next valid element.  
A counter `count` tracks how many times the current number has appeared.  
When a new number appears, reset `count = 1`.

**中文：**  
采用 **双指针法**：  
一个指针 `fast` 遍历数组，另一个指针 `slow` 负责写入下一个合法元素。  
`count` 用于统计当前数字出现的次数。  
当遇到新数字时，将 `count` 重置为 1。

**Key idea / 核心思想：**  
> 保留每个数字的前 `k` 次出现，丢弃第 `k+1` 次及之后的重复项。

---

## 🧩 Code / 代码实现  

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        n = len(nums)
        if n <= 1:
            return n

        # 双指针法 (Two Pointers):
        # slow → 指向下一个可写入位置 (next valid position)
        # fast → 遍历扫描整个数组 (used to scan the array)
        # count → 当前数字组的出现次数 (occurrence count for current number)
        # k → 每个数字最多允许出现的次数 (max allowed duplicates)
        slow, fast = 1, 1
        count = 1
        k = 2  

        # 主循环 (Main loop): 从第二个元素开始遍历 (start from index 1)
        while fast < n:
            # 当前元素与前一个相同 → 属于同一数字组
            # If nums[fast] == nums[fast - 1], it belongs to the same group
            if nums[fast] == nums[fast - 1]:
                # 若未超过允许次数 k，则保留该元素
                # Keep the element if it appears less than k times
                if count < k:
                    nums[slow] = nums[fast]
                    slow += 1
                    count += 1
            else:
                # 遇到新数字 → 重置计数并保留新数字
                # New number encountered → reset count and record it
                nums[slow] = nums[fast]
                slow += 1
                count = 1

            # fast 每轮都向前移动，继续扫描数组
            # Move fast forward in every iteration
            fast += 1

        # slow 最终指向下一个可写入位置，即合法元素的个数
        # slow points to the next valid position → equals the new length
        return slow

🧾 Explanation / 详细解释

Step-by-step (English):
1️⃣ Compare each element with the previous one.
2️⃣ If it’s the same number → increment count.
3️⃣ If count ≤ k → keep it.
4️⃣ If new number → reset count = 1.
5️⃣ Continue until the end of the array.

逐步说明（中文）：
1️⃣ 依次比较每个元素与前一个元素；
2️⃣ 若相同，count += 1；
3️⃣ 当 count ≤ k 时保留该元素；
4️⃣ 遇到新数字时重置 count = 1；
5️⃣ 重复直到扫描完整个数组。

Complexity / 复杂度分析：

⏱️ Time: O(n) — single traversal

💾 Space: O(1) — in-place modification

🪪 License & Copyright

### 🪪 License & Copyright

© 2025 Fireworks007  
Licensed under [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)

You are free to **read and share** this material with proper credit.  
However, **commercial use, modification, or redistribution** is **not allowed**.  

（版权所有 © 2025 Fireworks007。  
本题解受 [CC BY-NC-ND 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh) 保护，  
仅供学习与分享，禁止商用、修改或再分发。）  

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)
