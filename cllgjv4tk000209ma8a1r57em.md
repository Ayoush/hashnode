---
title: "LeetCode Problem Solutions Array Part 0: Explained and Analyzed"
datePublished: Fri Aug 18 2023 12:11:39 GMT+0000 (Coordinated Universal Time)
cuid: cllgjv4tk000209ma8a1r57em
slug: leetcode-problem-solutions-array-part-0-explained-and-analyzed
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/TpG2TBiclik/upload/dbbd1fd4119ec93ea589247b682140d3.jpeg
tags: interview, algorithms, software-development, data-structures, software-engineering

---

In the world of competitive programming and technical interviews, LeetCode has become a household name. With a plethora of coding challenges spanning a wide range of difficulties and topics, it's an excellent platform to enhance your problem-solving skills and coding prowess. In this blog post, we'll walk through the solutions to five LeetCode problems, along with their time and space complexities.

## **Problem 1: Majority Element**

[**Link to the problem**](https://leetcode.com/problems/majority-element/)

### **Problem Statement**

Given an array of integers, find the majority element (appears more than `n/2` times), and assume that the array is non-empty and the majority element always exists in the array.

### **Solution Explanation**

Sorting the array allows the majority element to always be at the middle index after sorting. By sorting the array, we can then directly access the element at index `n//2` to find the majority element.

### **Time Complexity: O(n log n)**

The sorting operation dominates the time complexity.

### **Space Complexity: O(1)**

No additional space is used, as the sorting is done in-place.

```python
pythonCopy codeclass Solution(object):
    def majorityElement(self, nums):
        nums.sort()
        n = len(nums)
        return nums[n//2]
```

## **Problem 2: Two Sum**

[**Link to the problem**](https://leetcode.com/problems/two-sum/)

### **Problem Statement**

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

### **Solution Explanation**

We can use a hashmap to store the values encountered so far and their corresponding indices. While iterating through the array, we calculate the complement of the current number with respect to the target. If the complement is already in the hashmap, we found the two numbers that add up to the target.

### **Time Complexity: O(n)**

We iterate through the array once.

### **Space Complexity: O(n)**

In the worst case, we might need to store all elements in the hashmap.

```python
pythonCopy codeclass Solution(object):
    def twoSum(self, nums, target):
        mapp = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in mapp and mapp[complement] != i:
                return [mapp[complement], i]
            mapp[nums[i]] = i
```

## **Problem 3: Best Time to Buy and Sell Stock**

[**Link to the problem**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

### **Problem Statement**

Given an array representing stock prices on different days, find the maximum profit that can be achieved by buying and selling a stock.

### **Solution Explanation**

We iterate through the array while maintaining the minimum price encountered so far and the maximum profit achievable. By calculating the difference between the current price and the minimum price, we track the potential profit.

### **Time Complexity: O(n)**

We iterate through the array once.

### **Space Complexity: O(1)**

No additional space is used apart from a few variables.

```python
pythonCopy codeclass Solution(object):
    def maxProfit(self, prices):
        if len(prices) == 1:
            return 0
        else:
            max_profit = prices[1] - prices[0]
            min_price = prices[0]
            for i in range(1, len(prices)):
                max_profit = max(max_profit, prices[i] - min_price)
                min_price = min(min_price, prices[i])
            if max_profit < 0:
                return 0
            else:
                return max_profit
```

## **Problem 4: Move Zeroes**

[**Link to the problem**](https://leetcode.com/problems/move-zeroes/)

### **Problem Statement**

Given an array of integers, move all the zeroes to the end of the array while maintaining the relative order of the non-zero elements.

### **Solution Explanation**

We can maintain a pointer that points to the position where the next non-zero element should be placed. As we iterate through the array, we replace each encountered zero with the next non-zero element and move the pointer accordingly.

### **Time Complexity: O(n)**

We iterate through the array once.

### **Space Complexity: O(1)**

No additional space is used apart from a few variables.

```python
pythonCopy codeclass Solution(object):
    def moveZeroes(self, nums):
        if len(nums) == 1:
            return nums
        non_zero_ptr = 0
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[non_zero_ptr] = nums[i]
                if non_zero_ptr != i:
                    nums[i] = 0
                non_zero_ptr += 1
        return nums
```

Alternatively:

```python
pythonCopy codeclass Solution(object):
    def moveZeroes(self, nums):
        if len(nums) == 1:
            return nums
        zero_count = nums.count(0)
        for i in range(len(nums) - zero_count):
            if nums[i] == 0:
                nums.pop(i)
                nums.append(0)
        return nums
```

## **Problem 5: Squares of a Sorted Array**

[**Link to the problem**](https://leetcode.com/problems/squares-of-a-sorted-array/)

### **Problem Statement**

Given an array of integers sorted in non-decreasing order, return an array of the squares of each number, also in non-decreasing order.

### **Solution Explanation**

We can use two pointers starting from the beginning and end of the array. The larger of the absolute values of the two elements is squared and placed in the last position of the result array. The pointer of the larger element is then moved accordingly.

### **Time Complexity: O(n)**

We iterate through the array once.

### **Space Complexity: O(n)**

We create a result array of the same length as the input array.

```python
pythonCopy codeclass Solution:
    def sortedSquares(self, nums):
        n = len(nums)
        result = [0] * n
        left, right = 0, n - 1
        result_index = n - 1
        while result_index >= 0:
            if abs(nums[left]) >= nums[right]:
                result[result_index] = abs(nums[left]) ** 2
                left += 1
            else:
                result[result_index] = nums[right] ** 2
                right -= 1
            result_index -= 1
        return result
```