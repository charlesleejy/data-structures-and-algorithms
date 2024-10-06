## Is Subsequence

### Problem Description
Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters.

### Example
```
Input: s = "abc", t = "ahbgdc"
Output: true
```
```
Input: s = "axc", t = "ahbgdc"
Output: false
```

### Solution Approach
To solve this problem, we can use a two-pointer technique. We need to traverse both strings using pointers and check if all characters of `s` can be found in `t` in the same order.

### Steps in Detail

1. **Edge Case Handling**:
   - If `s` is an empty string, return `true` because an empty string is a subsequence of any string.
   - If `t` is an empty string but `s` is not, return `false`.

2. **Initialize Pointers**:
   - Initialize a pointer `i` for the string `s` and a pointer `j` for the string `t`.

3. **Traverse Both Strings**:
   - Iterate through the string `t` using the pointer `j`.
   - For each character in `t`, check if it matches the current character in `s` (i.e., `s[i]`).
   - If a match is found, move the pointer `i` to the next character in `s`.
   - Continue until all characters in `s` are found in `t` or `t` is fully traversed.

4. **Check Result**:
   - If the pointer `i` reaches the end of `s`, return `true`.
   - Otherwise, return `false`.

### Python Code
```python
def is_subsequence(s, t):
    if not s:
        return True
    if not t:
        return False
    
    i, j = 0, 0
    
    while j < len(t):
        if s[i] == t[j]:
            i += 1
            if i == len(s):
                return True
        j += 1
    
    return False
```

### Java Code
```java
public class Solution {
    public boolean isSubsequence(String s, String t) {
        if (s.isEmpty()) {
            return true;
        }
        if (t.isEmpty()) {
            return false;
        }
        
        int i = 0, j = 0;
        
        while (j < t.length()) {
            if (s.charAt(i) == t.charAt(j)) {
                i++;
                if (i == s.length()) {
                    return true;
                }
            }
            j++;
        }
        
        return false;
    }
}
```

### Explanation

1. **Edge Case Handling**:
   - In Python, we check if `s` is an empty string using `if not s:` and return `true`. Similarly, we check if `t` is empty using `if not t:` and return `false`.
   - In Java, we use `s.isEmpty()` and `t.isEmpty()` for the same checks.

2. **Initialize Pointers**:
   - In both Python and Java, we initialize `i` and `j` to 0 to start from the beginning of `s` and `t`, respectively.

3. **Traverse Both Strings**:
   - We use a while loop to iterate through `t` with the pointer `j`.
   - For each character in `t`, we check if it matches `s[i]`.
   - If a match is found, we increment `i` to check the next character in `s`. If `i` reaches the end of `s`, we return `true`.
   - Regardless of a match, we always increment `j` to continue checking the next character in `t`.

4. **Check Result**:
   - If the loop completes without `i` reaching the end of `s`, we return `false`.

This approach ensures that we efficiently check for the subsequence property by comparing characters from both strings using pointers, making it an O(n + m) solution where n is the length of `s` and m is the length of `t`. This guarantees an efficient and straightforward solution to the problem.