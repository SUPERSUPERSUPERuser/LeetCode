# Count Prefix-Suffix Pairs

This document describes the implementation of a Java method to count the number of prefix-suffix pairs in an array of strings.

## Problem Statement

Given an array of strings `words`, count the number of pairs `(i, j)` where `i < j` and:
1. `words[i]` is a **prefix** of `words[j]`, and
2. `words[i]` is a **suffix** of `words[j]`.

### Example Inputs and Outputs

- Input: `["a", "aa", "aaa"]`
  - Output: `3`  
    - Pairs: `("a", "aa")`, `("a", "aaa")`, `("aa", "aaa")`.

- Input: `["abc", "abcabc", "def"]`
  - Output: `1`
    - Pair: `("abc", "abcabc")`.

- Input: `["x", "y", "z"]`
  - Output: `0`

---

## Code Implementation

```java
class Solution {

    public int countPrefixSuffixPairs(String[] words) {
        int n = words.length; // Number of words in the array
        int count = 0; // Initialize the count of prefix-suffix pairs

        // Iterate through all possible pairs of words
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                String str1 = words[i];
                String str2 = words[j];

                // Check if str1 is both a prefix and suffix of str2
                if (str1.length() <= str2.length() && str2.startsWith(str1) && str2.endsWith(str1)) {
                    ++count; // Increment count if both conditions are met
                }
            }
        }
        return count; // Return the total count
    }
}
