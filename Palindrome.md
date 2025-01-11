# 1400. Construct K Palindrome Strings

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** String, Greedy, Counting
---

## Problem Description

Given a string s and an integer k, return true if you can use all the characters in s to construct k palindrome strings or false otherwise.

---

## Examples

### Example 1

**Input:**

```c
Example 1:

Input: s = "annabelle", k = 2
Output: true
Explanation: You can construct two palindromes using all characters in s.
Some possible constructions "anna" + "elble", "anbna" + "elle", "anellena" + "b"
```

```class Solution {
    public boolean canConstruct(String s, int k) {
        if(s.length()<k) return false;
        if(s.length() == k) return true;
        int[] freq new int[26];
        int oddCount = 0;
        for(char chr : s.toCharArray()){
            freq[chr-'a']++;
        }
        for(int count: freq){
            if(count %2 ==1){
                oddCount++;
            }
    }
    return oddCount <=k;
            }
        }
        
                
            
        
