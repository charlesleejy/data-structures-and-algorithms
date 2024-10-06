## Find the Index of the First Occurrence in a String

### Problem Description
Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

### Example
```
Input: haystack = "hello", needle = "ll"
Output: 2
```
```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```
```
Input: haystack = "", needle = ""
Output: 0
```

### Solution Approach
To solve this problem, we need to find the index of the first occurrence of the substring `needle` in the string `haystack`. There are multiple approaches to solve this, but a simple and efficient method is to use the sliding window technique.

### Steps in Detail

1. **Edge Case Handling**:
   - If `needle` is an empty string, return `0` since an empty string is trivially found at the start of any string.
   - If the length of `needle` is greater than the length of `haystack`, return `-1` since `needle` cannot be a substring of `haystack`.

2. **Sliding Window Technique**:
   - Iterate through `haystack` with a window of size equal to the length of `needle`.
   - For each position in `haystack`, check if the substring of `haystack` starting at the current position and of length equal to `needle` matches `needle`.
   - If a match is found, return the starting index of the window.
   - If no match is found after checking all possible positions, return `-1`.

### Python Code
```python
def strStr(haystack, needle):
    if not needle:
        return 0
    if len(needle) > len(haystack):
        return -1
    
    for i in range(len(haystack) - len(needle) + 1):
        if haystack[i:i + len(needle)] == needle:
            return i
    return -1
```

### Java Code
```java
public class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty()) {
            return 0;
        }
        if (needle.length() > haystack.length()) {
            return -1;
        }
        
        for (int i = 0; i <= haystack.length() - needle.length(); i++) {
            if (haystack.substring(i, i + needle.length()).equals(needle)) {
                return i;
            }
        }
        return -1;
    }
}
```

### Explanation

1. **Edge Case Handling**:
   - In Python, we use `if not needle:` to check if `needle` is an empty string and return `0`.
   - In Java, we use `if (needle.isEmpty())` for the same check.
   - Both in Python and Java, we check if the length of `needle` is greater than the length of `haystack` and return `-1` if true.

2. **Sliding Window Technique**:
   - We iterate through `haystack` with a loop.
   - In Python, the loop is `for i in range(len(haystack) - len(needle) + 1):`.
   - In Java, the loop is `for (int i = 0; i <= haystack.length() - needle.length(); i++)`.
   - At each iteration, we extract a substring from `haystack` starting at `i` and of length equal to `needle`.
   - In Python, we use `haystack[i:i + len(needle)]` to get the substring and check if it equals `needle`.
   - In Java, we use `haystack.substring(i, i + needle.length())` and check if it equals `needle`.
   - If a match is found, we return the current index `i`.
   - If no match is found after the loop, we return `-1`.

This approach ensures that we efficiently find the first occurrence of `needle` in `haystack` by checking each possible position with a sliding window, making it an O(n*m) solution where n is the length of `haystack` and m is the length of `needle`. This guarantees a straightforward and efficient solution to the problem.