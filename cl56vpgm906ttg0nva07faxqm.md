## Solving LeetCode Day 1(4th July, 2022)

## Motive

So I am preparing for a switch for which I have started with my preparation. And who can skip solving [LeetCode](https://leetcode.com/) problems and so I have decided the same.

### Goals
My goal is to solve 500 questions in the next 3-4 months.

### Status
`2/500` Questions solved.

#### [Question 1](https://leetcode.com/problems/running-sum-of-1d-array/)

##### Problem Statement :-

> Given an array nums. We define a running sum of an array as runningSum[i] = sum(nums[0]…nums[i]).
> Return the running sum of nums.

Example 1:
```
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
Explanation: Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].
```

Example 2:
```
Input: nums = [1,1,1,1,1]
Output: [1,2,3,4,5]
Explanation: Running sum is obtained as follows: [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1].
```

Example 3:
```
Input: nums = [3,1,2,10,1]
Output: [3,4,6,16,17]
```

Constraints:
$$ 1 <= nums.length <= 1000 $$
$$ -10^6 <= nums[i] <= 10^6 $$

#### Solution :-

```
class Solution(object):
    def runningSum(self, nums):
        temp = 0
        result = []
        for n in nums:
            result.append(temp+n)
            temp=temp+n
        return result
``` 

#### Thought Process and Time and Space Complexity :-
It's a pretty straight forward problem where you have to just keep track for the sums till last index as being taken care here by `temp` variable. As far as time complexity is concern it is `O(n)` and space complexity is also same.



#### [Question 2](https://leetcode.com/problems/find-pivot-index/solution/)

##### Problem Statement :-

> Given an array of integers nums, calculate the pivot index of this array.
> 
> The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.
> 
> If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.
> 
> Return the leftmost pivot index. If no such index exists, return -1.


Example 1:
```
Input: nums = [1,7,3,6,5,6]
Output: 3
Explanation:
The pivot index is 3.
Left sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11
Right sum = nums[4] + nums[5] = 5 + 6 = 11
```

Example 2:
```
Input: nums = [1,2,3]
Output: -1
Explanation:
There is no index that satisfies the conditions in the problem statement.
```

Example 3:
```
Input: nums = [2,1,-1]
Output: 0
Explanation:
The pivot index is 0.
Left sum = 0 (no elements to the left of index 0)
Right sum = nums[1] + nums[2] = 1 + -1 = 0
```


Constraints:
$$ 1 <= nums.length <= 10^4 $$
$$ -1000 <= nums[i] <= 1000 $$


#### Solution :-

```
class Solution(object):
    def pivotIndex(self, nums):
        sumR = sum(nums)
        sumL= 0
        for i in range(len(nums)):
            sumR -=  nums[i]
            if sumR == sumL:
                return i
            sumL += nums[i]
        return -1 
``` 

#### Thought Process and Time and Space Complexity :-
So earlier I thought of solving it using binary search  by selecting middle element with index selection logic as this `1.5(after diving by 2) -> 1` and `2(after diving by 2) -> 1` and which side has more weightage with sum will be selected and middle element from that side will be selected. But if you observe more its a pretty straightforward task you have to perform basically 3 task :-

1. Find the entire sum and assign it as starting sum of right side, as being done by this `sumR = sum(nums)`
2. So when you select a index then the entire sum minus that index will be the new sumR
3. Now you have to just compare that new sumR with sumL if equal, you have your index else move to next sumR with sumL will be sumL + previous index value.

Time Complexity and Space Complexity is :- `O(N)` and `O(1)`










 