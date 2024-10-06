## Happy Number

### Problem Description
Write an algorithm to determine if a number `n` is happy.

A happy number is a number defined by the following process:
- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle that does not include 1.
- Those numbers for which this process ends in 1 are happy.

Return `true` if `n` is a happy number, and `false` if not.

### Example
```
Input: n = 19
Output: true
Explanation:
1² + 9² = 82
8² + 2² = 68
6² + 8² = 100
1² + 0² + 0² = 1
```
```
Input: n = 2
Output: false
```

### Solution Approach
To determine if a number is happy, we need to detect cycles in the process of calculating the sum of the squares of its digits. If we encounter the same number again, it means we are in a cycle, and the number is not happy. We can use a set to keep track of numbers we have seen to detect cycles.

### Steps in Detail

1. **Helper Function**:
   - Define a helper function to calculate the sum of the squares of the digits of a number.

2. **Main Function**:
   - Initialize a set to keep track of numbers we have seen.
   - Repeat the process of calculating the sum of the squares of the digits.
   - If the number becomes 1, return `true`.
   - If the number is already in the set, return `false` because we have encountered a cycle.
   - Add the number to the set.

### Python Code
```python
def get_next(n):
    total_sum = 0
    while n > 0:
        digit = n % 10
        n = n // 10
        total_sum += digit * digit
    return total_sum

def is_happy(n):
    seen = set()
    while n != 1 and n not in seen:
        seen.add(n)
        n = get_next(n)
    return n == 1
```

### Java Code
```java
import java.util.HashSet;
import java.util.Set;

public class Solution {
    private int getNext(int n) {
        int totalSum = 0;
        while (n > 0) {
            int digit = n % 10;
            n = n / 10;
            totalSum += digit * digit;
        }
        return totalSum;
    }

    public boolean isHappy(int n) {
        Set<Integer> seen = new HashSet<>();
        while (n != 1 && !seen.contains(n)) {
            seen.add(n);
            n = getNext(n);
        }
        return n == 1;
    }
}
```

### Explanation

1. **Helper Function**:
   - In both Python and Java, we define a helper function `get_next` to calculate the sum of the squares of the digits of a number.
   - We use a while loop to extract each digit of the number, square it, and add it to the total sum.
   - The function returns the total sum of the squares of the digits.

2. **Main Function**:
   - We initialize a set `seen` to keep track of numbers we have seen.
   - We use a while loop to repeatedly calculate the sum of the squares of the digits of the number.
   - If the number becomes 1, we return `true`.
   - If the number is already in the set, we return `false` because we have encountered a cycle.
   - We add the number to the set and update the number using the `get_next` function.
   - Finally, we return `n == 1`, which will be `true` if the loop exited because `n` became 1, and `false` otherwise.

This approach ensures that we efficiently determine if a number is happy by detecting cycles using a set, making it an O(log(n)) solution in terms of space complexity due to the number of digits involved and the frequency of their occurrence in the set. This guarantees an efficient and straightforward solution to the problem.