---
title: Longest Substring Without Repeating Characters
excerpt: Given a string, find the length of the longest substring without repeating characters.

levels:
  - Intermediate

topics:
  - Algorithm
  - Data Structure
  - String
  - Hash Table

related:
  - longest-substring-with-at-most-two-distinct-characters
  - longest-substring-with-at-most-k-distinct-characters
  - subarrays-with-k-different-integers
---

## Problem

Given a string, find the length of the longest substring without repeating characters.

Example 1:

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

Example 2:

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

Example 3:

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

<div class="accordion">Solutions</div>
<div class="accordion-panel" markdown="1">

**Sliding Window**

A sliding window is an abstract concept commonly used in array/string problems. A window is a range of elements in the array/string which usually defined by the start and end indices, i.e. [i, j) (left-closed, right-open). A sliding window is a window "slides" its two boundaries to the certain direction. For example, if we slide [i, j) to the right by 1 element, then it becomes [i+1, j+1) (left-closed, right-open).

We could define a mapping of the characters to its index. Then we can skip the characters immediately when we found a repeated character.  The reason is that if s[j] has a duplicate in the range [i, j) with index j', we don't need to increase i little by little. We can skip all the elements in the range [i, j'] and let i to be j' + 1 directly.

**Complexity Analysis**

Time complexity : O(n). Index j will iterate n times.
Space complexity (HashMap) : O(min(m, n)).

Java Solution:

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>(); // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```

Python Solution:
```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        dicts = {}
        maxlength = start = 0
        for i,value in enumerate(s):
            if value in dicts:
                sums = dicts[value] + 1
                if sums > start:
                    start = sums
            num = i - start + 1
            if num > maxlength:
                maxlength = num
            dicts[value] = i
        return maxlength
```

JavaScript Solution:

```javascript
var lengthOfLongestSubstring = function(s) {
    let max_len = 0;
    let curr = 0;
    let hash = {}; 
    if(s.length < 2) {
        return s.length;
    }
    for(let i = 0; i < s.length;  i++) {
        if(hash[s[i]] == null) {
            curr += 1;
        } else {
            curr = Math.min(i - hash[s[i]], curr + 1);
        }
        max_len = Math.max(max_len, curr);
        hash[s[i]] = i; //save the index
    }
    return max_len;
};
```

</div>