---
title: Two Sum
excerpt: "Given an array of integers, return indices of the two numbers such that they add up to a specific target."

levels:
  - Beginner

topics:
  - Algorithm
  - Data Structure
  - Array
  - Hash Table

related:
  - 3sum
  - 4sum

heat: 1000
---

<div id="problem" class="tabcontent" markdown="1">

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

</div>
<div id="solutions" class="tabcontent" markdown="1">

### Solution 1: Two-pass Hash Table
A simple implementation uses two iterations. In the first iteration, we add each element's value and its index to the table. Then, in the second iteration we check if each element's complement (target - nums[i]) exists in the table. Beware that the complement must not be nums[i] itself!

Java Solution:

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

**Complexity Analysis**

* Time complexity : O(n). We traverse the list containing nn elements exactly twice. Since the hash table reduces the look up time to O(1), the time complexity is O(n).
* Space complexity: O(n). The extra space required depends on the number of items stored in the hash table, which stores exactly nn elements.

### Solution 2: One-pass Hash Table

It turns out we can do it in one-pass. While we iterate and inserting elements into the table, we also look back to check if current element's complement already exists in the table. If it exists, we have found a solution and return immediately.

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

**Complexity Analysis**

* Time complexity : O(n). We traverse the list containing nn elements only once. Each look up in the table costs only O(1) time.
* Space complexity : O(n). The extra space required depends on the number of items stored in the hash table, which stores at most nn elements.

</div>