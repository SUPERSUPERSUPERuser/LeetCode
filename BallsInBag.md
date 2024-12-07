# 2337. Balls in Bag

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** Array, Binary Search
---

## Problem Description

You are given an integer array nums where the ith bag contains nums[i] balls. You are also given an integer maxOperations.

You can perform the following operation at most maxOperations times:

Take any bag of balls and divide it into two new bags with a positive number of balls.
For example, a bag of 5 balls can become two new bags of 1 and 4 balls, or two new bags of 2 and 3 balls.
Your penalty is the maximum number of balls in a bag. You want to minimize your penalty after the operations.

Return the minimum possible penalty after performing the operations.

---

## Examples

### Example 1

**Input:**

```c
Input: nums = [9], maxOperations = 2
Output: 3
Explanation: 
- Divide the bag with 9 balls into two bags of sizes 6 and 3. [9] -> [6,3].
- Divide the bag with 6 balls into two bags of sizes 3 and 3. [6,3] -> [3,3,3].
The bag with the most number of balls has 3 balls, so your penalty is 3 and you should return 3.
```

```class Solution {
    public int minimumSize(int[] nums, int maxOperations) {
        int left = 1;
        int right = 0;
        for(int num: nums){
            right = Math.max(right,num);
        }
        while(left<right){
            int middle = (left + right)/2;
            if(isPossible(middle,nums,maxOperations)){
                right = middle;
            }
            else{
                left = middle +1;
            }
        }
        return left;
            }
          private boolean isPossible(
            int maxBallsInBag, int[] nums, int maxOperations){
                int totalOperations = 0;
                for(int num : nums){
                    int operations = (int) Math.ceil(num/(double) maxBallsInBag) - 1;
                    totalOperations += operations;
                    if(totalOperations > maxOperations){
                        return false;
                    }
                }
                return true;
                }
}
                
            
        
