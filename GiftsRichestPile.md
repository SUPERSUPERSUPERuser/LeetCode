# 2558. Take Gifts From the Richest Pile

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** Heap(Priority Queue), Sorting  
---

## Problem Description

You are given an integer array gifts denoting the number of gifts in various piles. Every second, you do the following:

Choose the pile with the maximum number of gifts.
If there is more than one pile with the maximum number of gifts, choose any.
Leave behind the floor of the square root of the number of gifts in the pile. Take the rest of the gifts.
Return the number of gifts remaining after k seconds.

---

## Examples

### Example 1

**Input:**
gifts = [25,64,9,4,100], k = 4
**Output:**
29
```c
Explanation: 
The gifts are taken in the following way:
- In the first second, the last pile is chosen and 10 gifts are left behind.
- Then the second pile is chosen and 8 gifts are left behind.
- After that the first pile is chosen and 5 gifts are left behind.
- Finally, the last pile is chosen again and 3 gifts are left behind.
The final remaining gifts are [5,8,9,4,3], so the total number of gifts remaining is 29.
```
public class Solution {

    public long pickGifts(int[] gifts, int k) {
        int n = gifts.length;

        // Create a list from the gifts array and sort it
        List<Integer> sortedGifts = new ArrayList<>();
        for (int gift : gifts) {
            sortedGifts.add(gift);
        }
        Collections.sort(sortedGifts);

        // Perform the operation k times
        for (int i = 0; i < k; i++) {
            // Get the largest element (last element in the sorted list)
            int maxElement = sortedGifts.get(n - 1);
            sortedGifts.remove(n - 1);

            // Calculate the square root of the max element
            int sqrtElement = (int) Math.floor(Math.sqrt(maxElement));

            // Find the index where the square root should be inserted
            int spotOfSqrt = Collections.binarySearch(sortedGifts, sqrtElement);

            // If the value isn't found, binarySearch returns a negative index
            if (spotOfSqrt < 0) {
                spotOfSqrt = -(spotOfSqrt + 1);
            }

            sortedGifts.add(spotOfSqrt, sqrtElement); // Insert the square root at the correct index
        }

        // Calculate the sum of the remaining gifts in the array
        long numberOfRemainingGifts = 0;
        for (int gift : sortedGifts) {
            numberOfRemainingGifts += gift;
        }

        return numberOfRemainingGifts;
    }
}
