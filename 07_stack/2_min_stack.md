## Min Stack

### Problem Description
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:
- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

### Example
```python
minStack = MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   // return -3
minStack.pop();
minStack.top();      // return 0
minStack.getMin();   // return -2
```

### Solution Approach
To implement a stack that supports retrieving the minimum element in constant time, we can use an auxiliary stack to keep track of the minimum values.

### Steps in Detail

1. **Use Two Stacks**:
   - Use a primary stack to store all elements.
   - Use an auxiliary stack to keep track of the minimum values.

2. **Push Operation**:
   - Push the value onto the primary stack.
   - If the auxiliary stack is empty or the value is less than or equal to the top of the auxiliary stack, push the value onto the auxiliary stack.

3. **Pop Operation**:
   - Pop the value from the primary stack.
   - If the value is equal to the top of the auxiliary stack, pop the top of the auxiliary stack.

4. **Top Operation**:
   - Return the top value of the primary stack.

5. **GetMin Operation**:
   - Return the top value of the auxiliary stack, which is the minimum value.

### Python Code
```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        if self.stack:
            if self.stack[-1] == self.min_stack[-1]:
                self.min_stack.pop()
            self.stack.pop()

    def top(self) -> int:
        if self.stack:
            return self.stack[-1]

    def getMin(self) -> int:
        if self.min_stack:
            return self.min_stack[-1]
```

### Java Code
```java
import java.util.Stack;

public class MinStack {

    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        if (!stack.isEmpty()) {
            if (stack.peek().equals(minStack.peek())) {
                minStack.pop();
            }
            stack.pop();
        }
    }

    public int top() {
        if (!stack.isEmpty()) {
            return stack.peek();
        }
        return -1; // or throw an exception
    }

    public int getMin() {
        if (!minStack.isEmpty()) {
            return minStack.peek();
        }
        return -1; // or throw an exception
    }
}
```

### Explanation

1. **Use Two Stacks**:
   - In both Python and Java, we use two stacks: one for storing all elements (`stack`) and one for storing the minimum values (`min_stack` in Python and `minStack` in Java).

2. **Push Operation**:
   - We push the value onto the primary stack (`self.stack.append(val)` in Python and `stack.push(val)` in Java).
   - If the auxiliary stack is empty or the value is less than or equal to the top of the auxiliary stack, we push the value onto the auxiliary stack (`self.min_stack.append(val)` in Python and `minStack.push(val)` in Java).

3. **Pop Operation**:
   - We pop the value from the primary stack (`self.stack.pop()` in Python and `stack.pop()` in Java).
   - If the value is equal to the top of the auxiliary stack, we pop the top of the auxiliary stack (`self.min_stack.pop()` in Python and `minStack.pop()` in Java).

4. **Top Operation**:
   - We return the top value of the primary stack (`self.stack[-1]` in Python and `stack.peek()` in Java).

5. **GetMin Operation**:
   - We return the top value of the auxiliary stack, which is the minimum value (`self.min_stack[-1]` in Python and `minStack.peek()` in Java).

This approach ensures that we efficiently manage the stack operations while keeping track of the minimum element in constant time, making it an O(1) solution for each operation. This guarantees an efficient and straightforward implementation of the Min Stack.