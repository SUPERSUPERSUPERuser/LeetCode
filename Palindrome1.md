# 128. Palindrome

**Status:** Solved  
**Difficulty:** Easy  
**Topics:** Array, Two Pointer
---

## Problem Description

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

---

## Examples

### Example 1

**Input:**

```c
Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

``class Solution {
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
                
            
        
