## Longest Substring Without Repeating Characters

### Problem Description
Given a string `s`, find the length of the longest substring without repeating characters.

### Example
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

### Solution Approach
To solve this problem efficiently, we can use the sliding window technique along with a hash map (or dictionary) to keep track of the characters and their indices.

### Steps in Detail

1. **Initialize Variables**:
   - Initialize a hash map (or dictionary) to store the characters and their latest indices.
   - Initialize two pointers, `left` and `right`, both set to 0.
   - Initialize a variable `max_length` to store the length of the longest substring found.

2. **Traverse the String**:
   - Use the `right` pointer to traverse the string.
   - For each character `s[right]`, check if it is already in the hash map and its index is greater than or equal to `left`. If so, update `left` to `map[s[right]] + 1` to ensure the substring does not have repeating characters.
   - Update the hash map with the current character and its index.
   - Update `max_length` to be the maximum of `max_length` and `right - left + 1`.

3. **Return the Result**:
   - After traversing the string, return `max_length` as the length of the longest substring without repeating characters.

### Python Code
```python
def length_of_longest_substring(s):
    char_index_map = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        if s[right] in char_index_map and char_index_map[s[right]] >= left:
            left = char_index_map[s[right]] + 1
        char_index_map[s[right]] = right
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> charIndexMap = new HashMap<>();
        int left = 0;
        int maxLength = 0;
        
        for (int right = 0; right < s.length(); right++) {
            if (charIndexMap.containsKey(s.charAt(right)) && charIndexMap.get(s.charAt(right)) >= left) {
                left = charIndexMap.get(s.charAt(right)) + 1;
            }
            charIndexMap.put(s.charAt(right), right);
            maxLength = Math.max(maxLength, right - left + 1);
        }
        
        return maxLength;
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we use a dictionary (hash map) to store characters and their latest indices.
   - We initialize `left` and `right` pointers to 0, and `max_length` to 0.

2. **Traverse the String**:
   - We use a for loop to traverse the string with the `right` pointer.
   - For each character `s[right]`, we check if it is already in the dictionary and if its index is greater than or equal to `left`. If so, we update `left` to `char_index_map[s[right]] + 1` to ensure the substring does not have repeating characters.
   - We update the dictionary with the current character and its index.
   - We update `max_length` to be the maximum of `max_length` and `right - left + 1`.

3. **Return the Result**:
   - After traversing the string, we return `max_length` as the length of the longest substring without repeating characters.

This approach ensures that we efficiently find the longest substring without repeating characters using the sliding window technique and a hash map, making it an O(n) solution where n is the length of the string. This guarantees an efficient and straightforward solution to the problem.