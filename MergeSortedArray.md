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
   class Solution {
public:
    bool isPalindrome(string s) {
        int l = 0;
        int e = s.size() - 1;

        while (l <= e) {
            // Skip non-alphanumeric characters
            if (!isalnum(s[l])) {
                l++;
            } else if (!isalnum(s[e])) {
                e--;
            } else {
                // Compare characters after converting to lowercase
                char t1 = tolower(s[l]);
                char t2 = tolower(s[e]);
                if (t1 != t2) return false;
                l++;
                e--;
            }
        }
        return true;
    }
};
                
            
        
