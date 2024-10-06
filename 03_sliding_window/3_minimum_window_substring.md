## Minimum Window Substring

### Problem Description
Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

### Example
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring is "BANC".
```
```
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string is the minimum window.
```
```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a' characters from t are not present in s, so it's impossible to form a substring.
```

### Solution Approach
To solve this problem efficiently, we can use the sliding window (two-pointer) technique along with a hashmap to keep track of the count of characters in `t`.

### Steps in Detail

1. **Initialize Variables**:
   - Use a hashmap `dict_t` to count the frequency of each character in `t`.
   - Initialize two pointers, `left` and `right`, both set to 0.
   - Initialize variables `formed`, `required`, `window_counts`, `ans` to store the number of unique characters in `t` that need to be present in the window, and the resulting window details (start index and length).

2. **Expand the Window**:
   - Use the `right` pointer to expand the window by moving it to the right.
   - For each character `s[right]`, update the `window_counts` hashmap.
   - If the current character's count matches the required count in `dict_t`, increment the `formed` variable.

3. **Contract the Window**:
   - While `formed` is equal to `required` (all characters in `t` are present in the window), try to contract the window from the left:
     - Update the `ans` if the current window is smaller than the previously recorded window.
     - Move the `left` pointer to the right and update `window_counts`.
     - If the count of the character at `left` becomes less than the required count, decrement the `formed` variable.

4. **Return the Result**:
   - After processing all characters, return the substring of `s` defined by the start and end indices in `ans`. If no such window exists, return `""`.

### Python Code
```python
from collections import Counter

def min_window(s, t):
    if not s or not t:
        return ""
    
    dict_t = Counter(t)
    required = len(dict_t)
    
    left, right = 0, 0
    formed = 0
    window_counts = {}
    
    ans = float("inf"), None, None
    
    while right < len(s):
        char = s[right]
        window_counts[char] = window_counts.get(char, 0) + 1
        
        if char in dict_t and window_counts[char] == dict_t[char]:
            formed += 1
        
        while left <= right and formed == required:
            char = s[left]
            
            if right - left + 1 < ans[0]:
                ans = (right - left + 1, left, right)
            
            window_counts[char] -= 1
            if char in dict_t and window_counts[char] < dict_t[char]:
                formed -= 1
            
            left += 1
        
        right += 1
    
    return "" if ans[0] == float("inf") else s[ans[1]:ans[2] + 1]
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public String minWindow(String s, String t) {
        if (s.length() == 0 || t.length() == 0) {
            return "";
        }
        
        Map<Character, Integer> dictT = new HashMap<>();
        for (int i = 0; i < t.length(); i++) {
            int count = dictT.getOrDefault(t.charAt(i), 0);
            dictT.put(t.charAt(i), count + 1);
        }
        
        int required = dictT.size();
        int left = 0, right = 0;
        int formed = 0;
        Map<Character, Integer> windowCounts = new HashMap<>();
        int[] ans = {-1, 0, 0}; // {window length, left, right}
        
        while (right < s.length()) {
            char c = s.charAt(right);
            int count = windowCounts.getOrDefault(c, 0);
            windowCounts.put(c, count + 1);
            
            if (dictT.containsKey(c) && windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
                formed++;
            }
            
            while (left <= right && formed == required) {
                c = s.charAt(left);
                
                if (ans[0] == -1 || right - left + 1 < ans[0]) {
                    ans[0] = right - left + 1;
                    ans[1] = left;
                    ans[2] = right;
                }
                
                windowCounts.put(c, windowCounts.get(c) - 1);
                if (dictT.containsKey(c) && windowCounts.get(c).intValue() < dictT.get(c).intValue()) {
                    formed--;
                }
                
                left++;
            }
            
            right++;
        }
        
        return ans[0] == -1 ? "" : s.substring(ans[1], ans[2] + 1);
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we use a hashmap to count the frequency of each character in `t`.
   - We initialize two pointers, `left` and `right`, both set to 0.
   - We use variables `formed` to track how many unique characters in `t` are currently in the window and `required` to store the total number of unique characters in `t`.
   - `window_counts` is used to store the frequency of characters in the current window.
   - `ans` is a tuple/array to store the minimum window length and its starting and ending indices.

2. **Expand the Window**:
   - We use the `right` pointer to expand the window.
   - For each character `s[right]`, we update `window_counts`.
   - If the character's count matches the required count in `dict_t`, we increment `formed`.

3. **Contract the Window**:
   - While `formed` is equal to `required` (all characters in `t` are present in the window), we try to contract the window from the left:
     - Update `ans` if the current window is smaller than the previously recorded window.
     - Move the `left` pointer to the right and update `window_counts`.
     - If the count of the character at `left` becomes less than the required count, decrement `formed`.

4. **Return the Result**:
   - After processing all characters, return the substring of `s` defined by the start and end indices in `ans`. If no such window exists, return `""`.

This approach ensures that we efficiently find the minimum window substring using the sliding window technique and hashmap, making it an O(n) solution where n is the length of `s`. This guarantees an efficient and straightforward solution to the problem.