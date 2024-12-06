# 2337. Max number Range

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** Strings, Simulation  
---

## Problem Description

You are given an integer array banned and two integers n and maxSum. You are choosing some number of integers following the below rules:

The chosen integers have to be in the range [1, n].
Each integer can be chosen at most once.
The chosen integers should not be in the array banned.
The sum of the chosen integers should not exceed maxSum.
Return the maximum number of integers you can choose following the mentioned rules.

---

## Examples

### Example 1

**Input:**

```c
Input: banned = [1,6,5], n = 5, maxSum = 6
Output: 2
Explanation: You can choose the integers 2 and 4.
2 and 4 are from the range [1, 5], both did not appear in banned, and their sum is 6, which did not exceed maxSum.
___
```
class Solution {
    public int maxCount(int[] banned, int n, int maxSum) {
        Arrays.sort(banned);
        int count = 0;
        for(int num=1; num<=n; num++){
            if(customBinarySearch(banned,num)) continue;
            maxSum-=num;
            if(maxSum<0) break;
            count++;
        }
        return count;
        
    }
    private boolean customBinarySearch(int[] arr, int target){
        int left = 0;
        int right = arr.length - 1;
        while(left<=right){
            int mid = left+(right - left)/2;
            if(arr[mid]==target) return true;
            if(arr[mid]>target){
                right = mid - 1; 
            }
            else{
                left = mid+1;
            }
            }
            return false;
        }
    }

```
