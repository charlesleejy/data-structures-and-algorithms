## Basic Calculator

### Problem Description
Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, non-negative integers, and empty spaces.

### Example
```
Input: s = "1 + 1"
Output: 2
```
```
Input: s = " 2-1 + 2 "
Output: 3
```
```
Input: s = "(1+(4+5+2)-3)+(6+8)"
Output: 23
```

### Solution Approach
To solve this problem, we can use a stack to handle the parentheses and manage the intermediate results. The main idea is to iterate through the string and evaluate the expression by keeping track of the current number, the current sign, and using the stack to store intermediate results when encountering parentheses.

### Steps in Detail

1. **Initialize Variables**:
   - Use a stack to keep track of intermediate results and signs.
   - Use variables to keep track of the current number, the result, and the current sign.

2. **Iterate Through the String**:
   - For each character in the string:
     - If it is a digit, build the current number.
     - If it is a plus or minus sign, update the result with the current number and reset the current number, updating the current sign.
     - If it is an open parenthesis, push the current result and the current sign onto the stack and reset the result and sign.
     - If it is a closing parenthesis, update the result with the current number, then pop the sign and the intermediate result from the stack, and update the result.

3. **Final Update**:
   - After iterating through the string, update the result with the last number.

4. **Return the Result**:
   - Return the final result.

### Python Code
```python
def calculate(s):
    stack = []
    current_number = 0
    result = 0
    sign = 1  # 1 means positive, -1 means negative

    for char in s:
        if char.isdigit():
            current_number = current_number * 10 + int(char)
        elif char == '+':
            result += sign * current_number
            current_number = 0
            sign = 1
        elif char == '-':
            result += sign * current_number
            current_number = 0
            sign = -1
        elif char == '(':
            stack.append(result)
            stack.append(sign)
            result = 0
            sign = 1
        elif char == ')':
            result += sign * current_number
            current_number = 0
            result *= stack.pop()  # sign
            result += stack.pop()  # intermediate result

    result += sign * current_number
    return result
```

### Java Code
```java
import java.util.Stack;

public class Solution {
    public int calculate(String s) {
        Stack<Integer> stack = new Stack<>();
        int currentNumber = 0;
        int result = 0;
        int sign = 1; // 1 means positive, -1 means negative
        
        for (char ch : s.toCharArray()) {
            if (Character.isDigit(ch)) {
                currentNumber = currentNumber * 10 + (ch - '0');
            } else if (ch == '+') {
                result += sign * currentNumber;
                currentNumber = 0;
                sign = 1;
            } else if (ch == '-') {
                result += sign * currentNumber;
                currentNumber = 0;
                sign = -1;
            } else if (ch == '(') {
                stack.push(result);
                stack.push(sign);
                result = 0;
                sign = 1;
            } else if (ch == ')') {
                result += sign * currentNumber;
                currentNumber = 0;
                result *= stack.pop(); // sign
                result += stack.pop(); // intermediate result
            }
        }
        
        result += sign * currentNumber;
        return result;
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we use a stack to keep track of intermediate results and signs.
   - We use `current_number` to build numbers from the characters, `result` to store the cumulative result, and `sign` to keep track of the current sign (`1` for positive and `-1` for negative).

2. **Iterate Through the String**:
   - We iterate through each character in the string:
     - If the character is a digit, we build the current number (`current_number = current_number * 10 + int(char)` in Python and `currentNumber = currentNumber * 10 + (ch - '0')` in Java).
     - If the character is a plus or minus sign, we update the result with the current number and reset the current number and update the sign (`result += sign * current_number` in Python and `result += sign * currentNumber` in Java).
     - If the character is an open parenthesis, we push the current result and the current sign onto the stack, then reset the result and sign (`stack.append(result)` and `stack.append(sign)` in Python, `stack.push(result)` and `stack.push(sign)` in Java).
     - If the character is a closing parenthesis, we update the result with the current number, then pop the sign and intermediate result from the stack, and update the result (`result *= stack.pop()` and `result += stack.pop()` in both Python and Java).

3. **Final Update**:
   - After iterating through the string, we update the result with the last number (`result += sign * current_number` in Python and `result += sign * currentNumber` in Java).

4. **Return the Result**:
   - We return the final result (`return result` in Python and `return result` in Java).

This approach ensures that we efficiently evaluate the expression by handling parentheses and keeping track of the current number and sign, making it an O(n) solution where n is the length of the string. This guarantees an efficient and straightforward solution to the problem.