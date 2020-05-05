---
title: Roman to Integer
excerpt: "Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999."

levels:
  - Beginner

topics:
  - Algorithm
  - Data Structure
  - String
  - Math

related:
  - integer-to-roman

heat: 659
---

## Problem

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

| Symbol    |   Value |
|-----------|---------|
| I         |    1    |
| V         |    5    |
| X         |    10   |
| L         |    50   |
| C         |    100  |
| D         |    500  |
| M         |    1000 |

For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

* I can be placed before V (5) and X (10) to make 4 and 9. 
* X can be placed before L (50) and C (100) to make 40 and 90. 
* C can be placed before D (500) and M (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

Example 1:

```
Input: "III"
Output: 3
```

Example 2:

```
Input: "IV"
Output: 4
```

Example 3:

```
Input: "IX"
Output: 9
```

Example 4:

```
Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

Example 5:

```
Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

---

<div class="accordion">Solutions</div>
<div class="accordion-panel" markdown="1">

The simplest algorithm is to use a pointer to scan through the string, at each step deciding whether to add the current symbol and go forward 1 place, or add the difference of the next 2 symbols and go forward 2 places. Here is this algorithm in pseudocode.

```
total = 0
i = 0
while i < s.length:
    if at least 2 symbols remaining AND value of s[i] < value of s[i + 1]:
        total = total + (value of s[i + 1]) - (value of s[i])  
        i = i + 2
    else:
        total = total + (value of s[i])
        i = i + 1
return total
```

Java Solution:

```java
class Solution {
    
    static Map<String, Integer> values = new HashMap<>();

    static {
        values.put("I", 1);
        values.put("V", 5);
        values.put("X", 10);
        values.put("L", 50);
        values.put("C", 100);
        values.put("D", 500);
        values.put("M", 1000);
        values.put("IV", 4);
        values.put("IX", 9);
        values.put("XL", 40);
        values.put("XC", 90);
        values.put("CD", 400);
        values.put("CM", 900);
    }

    public int romanToInt(String s) {
        
        int sum = 0;
        int i = 0;
        while (i < s.length()) {
            if (i < s.length() - 1) {
                String doubleSymbol = s.substring(i, i + 2);
                // Check if this is the length-2 symbol case.
                if (values.containsKey(doubleSymbol)) {
                    sum += values.get(doubleSymbol);
                    i += 2;
                    continue;
                }
            }
            // Otherwise, it must be the length-1 symbol case.
            String singleSymbol = s.substring(i, i + 1);
            sum += values.get(singleSymbol);
            i += 1;
        }
        return sum;
    }
}
```

Python Solution:

```python
values = {
    "I": 1,
    "V": 5,
    "X": 10,
    "L": 50,
    "C": 100,
    "D": 500,
    "M": 1000,
    "IV": 4,
    "IX": 9,
    "XL": 40, 
    "XC": 90,
    "CD": 400,
    "CM": 900
}

class Solution:
    def romanToInt(self, s: str) -> int:
        total = 0
        i = 0
        while i < len(s):
            # This is the subtractive case.
            if i < len(s) - 1 and s[i:i+2] in values:
                total += values[s[i:i+2]] 
                i += 2
            else:
                total += values[s[i]]
                i += 1
        return total
```

**Complexity Analysis**

* Time complexity : O(1). As there is a finite set of roman numerals, the maximum number possible number can be 3999, which in roman numerals is MMMCMXCIX. As such the time complexity is O(1). If roman numerals had an arbitrary number of symbols, then the time complexity would be proportional to the length of the input, i.e. O(n). This is assuming that looking up the value of each symbol is O(1).
* Space complexity : O(1). Because only a constant number of single-value variables are used, the space complexity is O(1).

</div>