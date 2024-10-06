## Valid Parentheses

### Problem Description
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

### Example
```
Input: s = "()"
Output: true
```
```
Input: s = "()[]{}"
Output: true
```
```
Input: s = "(]"
Output: false
```
```
Input: s = "([)]"
Output: false
```
```
Input: s = "{[]}"
Output: true
```

### Solution Approach
To solve this problem efficiently, we can use a stack to keep track of the open brackets. As we iterate through the string, we push open brackets onto the stack. When we encounter a closing bracket, we check if it matches the top of the stack. If it does, we pop the top of the stack; otherwise, the string is invalid.

### Steps in Detail

1. **Initialize a Stack**:
   - Use a stack to keep track of the open brackets.

2. **Iterate Through the String**:
   - For each character in the string:
     - If it is an open bracket, push it onto the stack.
     - If it is a closing bracket, check if the stack is not empty and the top of the stack matches the corresponding open bracket. If it does, pop the stack. If it does not, the string is invalid.

3. **Check the Stack**:
   - After iterating through the string, check if the stack is empty. If it is, the string is valid; otherwise, it is invalid.

### Python Code
```python
def is_valid(s):
    stack = []
    bracket_map = {')': '(', '}': '{', ']': '['}
    
    for char in s:
        if char in bracket_map:
            top_element = stack.pop() if stack else '#'
            if bracket_map[char] != top_element:
                return False
        else:
            stack.append(char)
    
    return not stack
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;
import java.util.Stack;

public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        Map<Character, Character> bracketMap = new HashMap<>();
        bracketMap.put(')', '(');
        bracketMap.put('}', '{');
        bracketMap.put(']', '[');
        
        for (char c : s.toCharArray()) {
            if (bracketMap.containsKey(c)) {
                char topElement = stack.empty() ? '#' : stack.pop();
                if (topElement != bracketMap.get(c)) {
                    return false;
                }
            } else {
                stack.push(c);
            }
        }
        
        return stack.isEmpty();
    }
}
```

### Explanation

1. **Initialize a Stack**:
   - In both Python and Java, we use a stack to keep track of the open brackets.
   - In Python, we use a list (`stack = []`), and in Java, we use a `Stack` object (`Stack<Character> stack = new Stack<>();`).

2. **Bracket Map**:
   - We create a dictionary/map to store the corresponding open brackets for each closing bracket.
   - In Python, we use a dictionary (`bracket_map = {')': '(', '}': '{', ']': '['}`).
   - In Java, we use a `HashMap` (`Map<Character, Character> bracketMap = new HashMap<>();`).

3. **Iterate Through the String**:
   - We iterate through each character in the string.
   - If the character is a closing bracket:
     - We check if the stack is not empty and if the top of the stack matches the corresponding open bracket.
     - If it matches, we pop the top of the stack. If it does not match, we return `false`.
   - If the character is an open bracket, we push it onto the stack.

4. **Check the Stack**:
   - After iterating through the string, we check if the stack is empty. If it is empty, it means all open brackets have been matched and closed correctly, so we return `true`. If it is not empty, we return `false`.

This approach ensures that we efficiently determine if the input string contains valid parentheses using a stack to track open brackets and ensuring they are closed in the correct order, making it an O(n) solution where n is the length of the string. This guarantees an efficient and straightforward solution to the problem.