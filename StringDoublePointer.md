# 2337. Move Pieces to Obtain a String

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** Strings, Simulation  
---

## Problem Description

You are given two strings `start` and `target`, both of length `n`. Each string consists only of the characters `'L'`, `'R'`, and `'_'` where:

- The characters `'L'` and `'R'` represent pieces, where a piece `'L'` can move to the left only if there is a blank space directly to its left, and a piece `'R'` can move to the right only if there is a blank space directly to its right.
- The character `'_'` represents a blank space that can be occupied by any of the `'L'` or `'R'` pieces.

Return `true` if it is possible to obtain the string `target` by moving the pieces of the string `start` any number of times. Otherwise, return `false`.

---

## Examples

### Example 1

**Input:**

```c
start = "_L__R__R_"
target = "L______RR"
___
### Code Snippet:-
```
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

bool canChange(char* start, char* target) {
    int n = strlen(start);
    int i = 0, j = 0;

    // Traverse both strings
    while (i < n && j < n) {
        // Skip blanks in both strings
        while (i < n && start[i] == '_') i++;
        while (j < n && target[j] == '_') j++;

        // If both reach the end, strings are transformable
        if (i == n && j == n) return true;

        // If one reaches the end before the other, transformation is impossible
        if (i == n || j == n) return false;

        // Check if characters match
        if (start[i] != target[j]) return false;

        // Check movement rules
        if (start[i] == 'L' && i < j) return false; // 'L' can only move left
        if (start[i] == 'R' && i > j) return false; // 'R' can only move right

        // Move to next characters
        i++;
        j++;
    }

    // Ensure the remaining characters in both strings are blanks
    while (i < n) {
        if (start[i] != '_') return false;
        i++;
    }
    while (j < n) {
        if (target[j] != '_') return false;
        j++;
    }

    return true;
}

// Example usage
int main() {
    char start[] = "_L__R__R_";
    char target[] = "L___R__R_";

    if (canChange(start, target)) {
        printf("True\n");
    } else {
        printf("False\n");
    }

    return 0;
}
```
