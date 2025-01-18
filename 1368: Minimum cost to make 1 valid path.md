# 1368: Minimum Cost to Make 1 Shortest Valid Path

**Status:** Solved  
**Difficulty:** Hard  
**Topics:** Array, BFS, Heap, Priority Queue
---------

## Problem Description

Given an m x n grid. Each cell of the grid has a sign pointing to the next cell you should visit if you are currently in this cell. The sign of grid[i][j] can be:

1 which means go to the cell to the right. (i.e go from grid[i][j] to grid[i][j + 1])
2 which means go to the cell to the left. (i.e go from grid[i][j] to grid[i][j - 1])
3 which means go to the lower cell. (i.e go from grid[i][j] to grid[i + 1][j])
4 which means go to the upper cell. (i.e go from grid[i][j] to grid[i - 1][j])
Notice that there could be some signs on the cells of the grid that point outside the grid.

You will initially start at the upper left cell (0, 0). A valid path in the grid is a path that starts from the upper left cell (0, 0) and ends at the bottom-right cell (m - 1, n - 1) following the signs on the grid. The valid path does not have to be the shortest.

You can modify the sign on a cell with cost = 1. You can modify the sign on a cell one time only.

Return the minimum cost to make the grid have at least one valid path.

---

## Examples

### Example 1
![Alt Text](https://assets.leetcode.com/uploads/2020/02/13/grid1.png)
**Input:**

```c

Input: grid = [[1,1,1,1],[2,2,2,2],[1,1,1,1],[2,2,2,2]]
Output: 3
Explanation: You will start at point (0, 0).
The path to (3, 3) is as follows. (0, 0) --> (0, 1) --> (0, 2) --> (0, 3) change the arrow to down with cost = 1 --> (1, 3) --> (1, 2) --> (1, 1) --> (1, 0) change the arrow to down with cost = 1 --> (2, 0) --> (2, 1) --> (2, 2) --> (2, 3) change the arrow to down with cost = 1 --> (3, 3)
The total cost = 3.
```

```class Solution {

    public int minCost(int[][] grid) {
        int numRows = grid.length, numCols = grid[0].length;
        int[][] minChanges = new int[numRows][numCols];

        // Initialize all cells with max value
        for (int[] row : minChanges) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        minChanges[0][0] = 0;

        while (true) {
            // Store previous state to check for convergence
            int[][] prevState = new int[numRows][numCols];
            for (int row = 0; row < numRows; row++) {
                prevState[row] = Arrays.copyOf(minChanges[row], numCols);
            }

            // Forward pass: check cells coming from left and top
            for (int row = 0; row < numRows; row++) {
                for (int col = 0; col < numCols; col++) {
                    // Check cell above
                    if (row > 0) {
                        minChanges[row][col] = Math.min(
                            minChanges[row][col],
                            minChanges[row - 1][col] +
                            (grid[row - 1][col] == 3 ? 0 : 1)
                        );
                    }
                    // Check cell to the left
                    if (col > 0) {
                        minChanges[row][col] = Math.min(
                            minChanges[row][col],
                            minChanges[row][col - 1] +
                            (grid[row][col - 1] == 1 ? 0 : 1)
                        );
                    }
                }
            }

            // Backward pass: check cells coming from right and bottom
            for (int row = numRows - 1; row >= 0; row--) {
                for (int col = numCols - 1; col >= 0; col--) {
                    // Check cell below
                    if (row < numRows - 1) {
                        minChanges[row][col] = Math.min(
                            minChanges[row][col],
                            minChanges[row + 1][col] +
                            (grid[row + 1][col] == 4 ? 0 : 1)
                        );
                    }
                    // Check cell to the right
                    if (col < numCols - 1) {
                        minChanges[row][col] = Math.min(
                            minChanges[row][col],
                            minChanges[row][col + 1] +
                            (grid[row][col + 1] == 2 ? 0 : 1)
                        );
                    }
                }
            }

            // If no changes were made in this iteration, we've found optimal solution
            if (Arrays.deepEquals(prevState, minChanges)) {
                break;
            }
        }

        return minChanges[numRows - 1][numCols - 1];
    }
}
                
            
        
