## Valid Palindrome

### Problem Description
Given a string `s`, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

### Example
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```
```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

### Solution Approach
To solve this problem, we can use a two-pointer approach. We need to traverse the string from both ends towards the center, comparing characters while ignoring non-alphanumeric characters and case differences.

### Steps in Detail

1. **Normalize the String**:
   - Convert the entire string to lowercase to handle case insensitivity.
   - Remove non-alphanumeric characters from the string.

2. **Two-Pointer Technique**:
   - Initialize two pointers, `left` at the beginning of the string and `right` at the end of the string.
   - Move the `left` pointer to the right and the `right` pointer to the left, skipping non-alphanumeric characters.
   - Compare the characters at `left` and `right` pointers.
   - If the characters do not match, return `false`.
   - If they match, move both pointers towards the center.
   - Continue until the `left` pointer is greater than or equal to the `right` pointer.

3. **Return the Result**:
   - If all characters matched, return `true`.

### Python Code
```python
def is_palindrome(s):
    left, right = 0, len(s) - 1
    
    while left < right:
        while left < right and not s[left].isalnum():
            left += 1
        while left < right and not s[right].isalnum():
            right -= 1
        if s[left].lower() != s[right].lower():
            return False
        left += 1
        right -= 1
    
    return True
```

### Java Code
```java
public class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }
            left++;
            right--;
        }
        
        return true;
    }
}
```

### Explanation

1. **Normalize the String**:
   - In Python, we do not explicitly normalize the string but handle case insensitivity and non-alphanumeric characters within the loop.
   - In Java, we use `Character.isLetterOrDigit()` to check for alphanumeric characters and `Character.toLowerCase()` for case insensitivity within the loop.

2. **Two-Pointer Technique**:
   - Initialize `left` pointer at the start of the string and `right` pointer at the end.
   - Use a while loop to move `left` and `right` pointers towards the center.
   - Skip non-alphanumeric characters using nested while loops:
     - In Python, use `s[left].isalnum()` and `s[right].isalnum()`.
     - In Java, use `Character.isLetterOrDigit(s.charAt(left))` and `Character.isLetterOrDigit(s.charAt(right))`.
   - Compare the characters at `left` and `right` pointers after converting them to lowercase:
     - In Python, use `s[left].lower()` and `s[right].lower()`.
     - In Java, use `Character.toLowerCase(s.charAt(left))` and `Character.toLowerCase(s.charAt(right))`.
   - If the characters do not match, return `false`.
   - If they match, increment `left` and decrement `right`.

3. **Return the Result**:
   - If the loop completes without finding any mismatch, return `true`.

This approach ensures that we efficiently check for palindrome properties by comparing characters from both ends of the string towards the center, making it an O(n) solution where n is the length of the string. This guarantees an efficient and straightforward solution to the problem.
