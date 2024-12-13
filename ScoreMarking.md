# 2593. Find Score of an Array After Marking All Elements

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** Heap (Priority Queue), Sorting
---

## Problem Description

You are given an array nums consisting of positive integers.

Starting with score = 0, apply the following algorithm:

Choose the smallest integer of the array that is not marked. If there is a tie, choose the one with the smallest index.
Add the value of the chosen integer to score.
Mark the chosen element and its two adjacent elements if they exist.
Repeat until all the array elements are marked.
Return the score you get after applying the above algorithm.

---

## Examples

### Example 1

**Input:**

```c
Input: nums = [2,1,3,4,5,2]
Output: 7
Explanation: We mark the elements as follows:
- 1 is the smallest unmarked element, so we mark it and its two adjacent elements: [2,1,3,4,5,2].
- 2 is the smallest unmarked element, so we mark it and its left adjacent element: [2,1,3,4,5,2].
- 4 is the only remaining unmarked element, so we mark it: [2,1,3,4,5,2].
Our score is 1 + 2 + 4 = 7.
```

class Solution {
    public long findScore(int[] nums) {
        long ans = 0;
        int[][] sorted = new int [nums.length][2];
        boolean [] marked = new boolean[nums.length];
        for(int i = 0; i< nums.length; i++){
            sorted[i][0] = nums[i];
            sorted[i][1] = i;
        }
        Arrays.sort(sorted, (arr1,arr2) -> arr1[0] - arr2[0]);
        for(int i =0; i<nums.length; i++){
            int number = sorted[i][0];
            int index = sorted[i][1];
            if(!marked[index]){
                ans +=number;
                marked[index]=true;
                if(index -1>=0){
                    marked[index-1] = true;
                }
                if(index +1<nums.length){
                    marked[index+1] = true;
                }
                }
            }
            return ans;
        }
        }
        
