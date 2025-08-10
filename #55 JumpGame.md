# 55: Jump Game

**Status:** Solved  
**Difficulty:** Medium 
---------

## Problem Description

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

---

## Examples

### Example 1
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

### Example 2:

Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

```
    class Solution {
    public boolean canJump(int[] nums) {
        int len = nums.length;
        int farthest = 0; // farthest index we can reach
        
        for (int i = 0; i < len; i++) {
            // If the current index is beyond the farthest reachable, we fail
            if (i > farthest) return false;

            // Update the farthest reachable index from here
            farthest = Math.max(farthest, i + nums[i]);

            // If we can reach the end, return true early
            if (farthest >= len - 1) return true;
        }
        return true;
    }
}
## Concept
Using Greedy technique, we used a variable *Farthest* to keep track of the last possible reachable index in the array. This helps in dealiing with cases easily where a 0 might occur in the middle of the array compared to the old method we were using.
The rest is self explanatory         
            
        
