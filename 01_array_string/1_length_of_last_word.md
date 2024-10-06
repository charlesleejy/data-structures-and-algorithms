## Length of Last Word

### Problem Description
Given a string `s` consisting of words and spaces, return the length of the last word in the string. A word is a maximal substring consisting of non-space characters only.

### Example
```
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```
```
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```
```
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

### Solution Approach
To solve this problem, we can start by trimming any trailing spaces from the string and then traverse the string from the end to find the last word and its length.

### Steps in Detail

1. **Trim Trailing Spaces**:
   - Use string trimming methods to remove any trailing spaces from the string.

2. **Initialize Variables**:
   - Initialize a variable `length` to 0 to store the length of the last word.
   - Initialize a pointer `i` to point to the last character of the string.

3. **Traverse the String from the End**:
   - Use a while loop to traverse the string from the end until a space is encountered or the beginning of the string is reached.
   - For each non-space character encountered, increment the `length` variable.

4. **Return the Result**:
   - After the loop, `length` will contain the length of the last word.

### Python Code
```python
def length_of_last_word(s):
    s = s.rstrip()  # Trim trailing spaces
    length = 0
    for i in range(len(s) - 1, -1, -1):
        if s[i] == ' ':
            break
        length += 1
    return length
```

### Java Code
```java
public class Solution {
    public int lengthOfLastWord(String s) {
        s = s.trim();  // Trim trailing spaces
        int length = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == ' ') {
                break;
            }
            length++;
        }
        return length;
    }
}
```

### Explanation

1. **Trim Trailing Spaces**:
   - In Python, we use `s.rstrip()` to remove trailing spaces from the string.
   - In Java, we use `s.trim()` to achieve the same effect.

2. **Initialize Variables**:
   - In both Python and Java, we initialize `length` to 0 to store the length of the last word.
   - We also initialize a pointer `i` to point to the last character of the string (`len(s) - 1` in Python and `s.length() - 1` in Java).

3. **Traverse the String from the End**:
   - In both Python and Java, we use a for loop to traverse the string from the end.
   - For each character, if it is a space, we break the loop.
   - If it is not a space, we increment the `length` variable.

4. **Return the Result**:
   - In both Python and Java, we return the `length` variable, which contains the length of the last word.

This approach ensures that we efficiently find the length of the last word by trimming the string and traversing it from the end, making it an O(n) solution where n is the length of the string. This guarantees an efficient solution to the problem.