# 73. Set Matrix Zeroes

## Problem Description

Given an `m x n` matrix, if an element is `0`, set its entire row and column to `0`. Do it in place.

### Input
```plaintext
matrix = [[1,1,1], [1,0,1], [1,1,1]]
```

### Output
```plaintext
[[1,0,1], [0,0,0], [1,0,1]]
```

## C++ Solution

```cpp
class Solution { 
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int n = matrix.size(); // Number of rows
        int m = matrix[0].size(); // Number of columns

        // Flags to check if the first row or column should be set to zero
        bool flag1 = false, flag2 = false;

        // Check if the first column contains any zeros
        for (int i = 0; i < n; i++) {
            if (matrix[i][0] == 0) {
                flag1 = true;
            }
        }

        // Check if the first row contains any zeros
        for (int j = 0; j < m; j++) {
            if (matrix[0][j] == 0) {
                flag2 = true;
            }
        }

        // Use the first row and column to mark zeros
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = matrix[0][j] = 0;
                }
            }
        }

        // Set matrix cells to zero based on marks in the first row and column
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Zero out the first column if needed
        if (flag1 == true) {
            for (int i = 0; i < n; i++) {
                matrix[i][0] = 0;
            }
        }

        // Zero out the first row if needed
        if (flag2 == true) {
            for (int j = 0; j < m; j++) {
                matrix[0][j] = 0;
            }
        }
    }
};
```

## Algorithm Trace with Example

### Input
```plaintext
matrix = [[1,1,1], [1,0,1], [1,1,1]]
```

### Steps

1. **Initialization:**
   - `n = 3`, `m = 3`
   - `flag1 = false`, `flag2 = false`

2. **Check the first column:**
   - Iterating through rows:
     - `matrix[0][0] != 0` → `flag1 = false`
     - `matrix[1][0] != 0` → `flag1 = false`
     - `matrix[2][0] != 0` → `flag1 = false`

3. **Check the first row:**
   - Iterating through columns:
     - `matrix[0][0] != 0` → `flag2 = false`
     - `matrix[0][1] != 0` → `flag2 = false`
     - `matrix[0][2] != 0` → `flag2 = false`

4. **Mark zeros in the first row and column:**
   - Iterating through the rest of the matrix:
     - `matrix[1][1] == 0` → Mark `matrix[1][0] = 0` and `matrix[0][1] = 0`

5. **Set cells to zero based on marks:**
   - Iterating through the matrix:
     - `matrix[1][0] == 0` → Set entire row 1 to zeros
     - `matrix[0][1] == 0` → Set entire column 1 to zeros

6. **Zero out the first column (if `flag1` is true):**
   - `flag1 = false`, so skip this step.

7. **Zero out the first row (if `flag2` is true):**
   - `flag2 = false`, so skip this step.

### Final Matrix
```plaintext
[[1,0,1], [0,0,0], [1,0,1]]
