# 2337. Longest Substring 3X

**Status:** Solved  
**Difficulty:** Medium  
**Topics:** Strings, HashMapping  
---

## Problem Description

You are given a string s that consists of lowercase English letters.

A string is called special if it is made up of only a single character. For example, the string "abc" is not special, whereas the strings "ddd", "zz", and "f" are special.

Return the length of the longest special substring of s which occurs at least thrice, or -1 if no special substring occurs at least thrice.

A substring is a contiguous non-empty sequence of characters within a string.

---

## Examples

### Example 1

**Input:**

```c
Input: s = "aaaa"
Output: 2
Explanation: The longest special substring which occurs thrice is "aa": substrings "aaaa", "aaaa", and "aaaa".
It can be shown that the maximum length achievable is 2.
___
```

class Solution {

    public int maximumLength(String s) {
        // Create a map to store the count of all substrings
        Map<Pair<Character, Integer>, Integer> count = new HashMap<>();
        int substringLength = 0;

        for (int start = 0; start < s.length(); start++) {
            char character = s.charAt(start);
            substringLength = 0;

            for (int end = start; end < s.length(); end++) {
                // If the current character matches the initial character, increment the count
                if (character == s.charAt(end)) {
                    substringLength++;
                    Pair<Character, Integer> key = new Pair<>(
                        character,
                        substringLength
                    );
                    count.put(key, count.getOrDefault(key, 0) + 1);
                } else {
                    break;
                }
            }
        }

        // Variable to store the longest substring length with frequency at least 3
        int ans = 0;
        for (Map.Entry<
            Pair<Character, Integer>,
            Integer
        > entry : count.entrySet()) {
            int length = entry.getKey().getValue();
            if (entry.getValue() >= 3 && length > ans) {
                ans = length;
            }
        }

        return ans == 0 ? -1 : ans;
    }
}
