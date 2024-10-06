## Evaluate Reverse Polish Notation

### Problem Description
Evaluate the value of an arithmetic expression in Reverse Polish Notation (RPN). Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

Note that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

### Example
```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```
```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```
```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

### Solution Approach
To evaluate an expression in Reverse Polish Notation, we can use a stack to keep track of the operands. When we encounter an operator, we pop the necessary operands from the stack, perform the operation, and push the result back onto the stack.

### Steps in Detail

1. **Initialize a Stack**:
   - Use a stack to keep track of the operands.

2. **Iterate Through the Tokens**:
   - For each token in the input list:
     - If the token is an operand (number), push it onto the stack.
     - If the token is an operator, pop the necessary number of operands from the stack, perform the operation, and push the result back onto the stack.

3. **Return the Result**:
   - The result of the expression will be the only element left in the stack.

### Python Code
```python
def eval_rpn(tokens):
    stack = []
    
    for token in tokens:
        if token in "+-*/":
            b = stack.pop()
            a = stack.pop()
            if token == '+':
                result = a + b
            elif token == '-':
                result = a - b
            elif token == '*':
                result = a * b
            elif token == '/':
                result = int(a / b)  # Truncate toward zero
            stack.append(result)
        else:
            stack.append(int(token))
    
    return stack[0]
```

### Java Code
```java
import java.util.Stack;

public class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        
        for (String token : tokens) {
            if (token.equals("+") || token.equals("-") || token.equals("*") || token.equals("/")) {
                int b = stack.pop();
                int a = stack.pop();
                switch (token) {
                    case "+":
                        stack.push(a + b);
                        break;
                    case "-":
                        stack.push(a - b);
                        break;
                    case "*":
                        stack.push(a * b);
                        break;
                    case "/":
                        stack.push(a / b);  // Integer division truncates toward zero in Java
                        break;
                }
            } else {
                stack.push(Integer.parseInt(token));
            }
        }
        
        return stack.pop();
    }
}
```

### Explanation

1. **Initialize a Stack**:
   - In both Python and Java, we use a stack to keep track of the operands.
   - In Python, we use a list as a stack: `stack = []`.
   - In Java, we use a `Stack` object: `Stack<Integer> stack = new Stack<>();`.

2. **Iterate Through the Tokens**:
   - We iterate through each token in the input list.
   - If the token is an operand (number), we push it onto the stack.
     - In Python, we use `stack.append(int(token))`.
     - In Java, we use `stack.push(Integer.parseInt(token));`.
   - If the token is an operator, we pop the necessary number of operands from the stack, perform the operation, and push the result back onto the stack.
     - In Python, we pop the operands and use if-elif statements to perform the operations: `if token == '+':`, `elif token == '-':`, etc.
     - In Java, we pop the operands and use a switch statement to perform the operations: `switch (token) { case "+":`, `case "-":`, etc.

3. **Return the Result**:
   - The result of the expression will be the only element left in the stack.
   - In Python, we return the first element of the stack: `return stack[0]`.
   - In Java, we return the top element of the stack: `return stack.pop();`.

This approach ensures that we efficiently evaluate the expression in Reverse Polish Notation using a stack to manage the operands and perform operations in constant time, making it an O(n) solution where n is the length of the input list. This guarantees an efficient and straightforward solution to the problem.
