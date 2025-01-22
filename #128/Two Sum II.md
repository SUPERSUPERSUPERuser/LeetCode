class Solution {
    public int[] twoSum(int[] numbers, int target) {
        // Initialize two pointers
        int lb = 0; // Lower bound (left pointer)
        int up = numbers.length - 1; // Upper bound (right pointer)
        
        // Iterate until the two pointers meet
        while (lb < up) {
            int sum = numbers[lb] + numbers[up];
            
            if (sum < target) {
                lb++; // Move the left pointer right to increase the sum
            } else if (sum > target) {
                up--; // Move the right pointer left to decrease the sum
            } else {
                // Found the pair, return 1-based indices
                return new int[]{lb + 1, up + 1};
            }
        }
        
        // This point should not be reached because the problem guarantees a solution
        return new int[]{-1, -1};
    }
}
