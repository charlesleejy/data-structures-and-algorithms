## Longest Common Prefix

### Problem Description
Write a function to find the longest common prefix string amongst an array of strings. If there is no common prefix, return an empty string `""`.

### Example
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

### Solution Approach
To solve this problem, we need to find the longest prefix that is common to all strings in the array. There are several approaches to solve this problem, but a simple and efficient method is to use a horizontal scanning approach. This approach compares characters of each string one by one until the common prefix is found.

### Steps in Detail

1. **Edge Case Handling**:
   - If the input list is empty, return an empty string `""`.

2. **Initialize the Prefix**:
   - Set the first string in the list as the initial prefix.

3. **Compare with Each String**:
   - Iterate through each string in the list starting from the second string.
   - For each string, update the prefix by comparing characters until the characters match.
   - If at any point the prefix becomes an empty string, return `""`.

4. **Return the Result**:
   - After comparing with all strings, return the common prefix.

### Python Code
```python
def longest_common_prefix(strs):
    if not strs:
        return ""
    
    prefix = strs[0]
    
    for s in strs[1:]:
        while s.find(prefix) != 0:
            prefix = prefix[:-1]
            if not prefix:
                return ""
    
    return prefix
```

### Java Code
```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        
        String prefix = strs[0];
        
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) {
                    return "";
                }
            }
        }
        
        return prefix;
    }
}
```

### Explanation

1. **Edge Case Handling**:
   - In Python, we check `if not strs` to handle the case when the list is empty.
   - In Java, we check `if (strs == null || strs.length == 0)` to handle the case when the list is null or empty.

2. **Initialize the Prefix**:
   - In both Python and Java, we set the first string (`strs[0]`) as the initial prefix.

3. **Compare with Each String**:
   - In Python, we iterate through each string in the list starting from the second string using `for s in strs[1:]`.
   - In Java, we use a for loop starting from the second element (`for (int i = 1; i < strs.length; i++)`).
   - For each string, we use a while loop to check if the current prefix is at the start of the string:
     - In Python, we use `s.find(prefix) != 0` to check if the prefix is not at the start.
     - In Java, we use `strs[i].indexOf(prefix) != 0` for the same check.
   - If the prefix is not at the start, we reduce the prefix by one character from the end (`prefix = prefix[:-1]` in Python and `prefix = prefix.substring(0, prefix.length() - 1)` in Java).
   - If the prefix becomes an empty string, we return `""`.

4. **Return the Result**:
   - After comparing with all strings, we return the prefix.

This approach ensures that we efficiently find the longest common prefix by reducing the prefix size whenever a mismatch is found, making it an O(n * m) solution where n is the number of strings and m is the length of the shortest string in the list. This guarantees a straightforward and efficient solution to the problem.