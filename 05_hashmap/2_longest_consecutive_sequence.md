## Longest Consecutive Sequence

### Problem Description
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

### Example
```
Input: nums = [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```
```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

### Solution Approach
To solve this problem in O(n) time, we can use a set to store the elements of the array. This allows us to efficiently check for the presence of consecutive elements.

### Steps in Detail

1. **Convert the Array to a Set**:
   - Convert the array `nums` to a set to allow O(1) time complexity for lookups.

2. **Initialize Variables**:
   - Use a variable to keep track of the longest consecutive sequence length.

3. **Iterate Through the Array**:
   - For each number in the set, check if it is the start of a sequence (i.e., the previous number is not in the set).
   - If it is the start of a sequence, initialize a counter and use a loop to count the length of the sequence by checking for consecutive numbers.

4. **Update the Longest Sequence Length**:
   - Update the longest sequence length if the current sequence is longer than the previously recorded longest sequence.

5. **Return the Result**:
   - Return the length of the longest consecutive sequence.

### Python Code
```python
def longest_consecutive(nums):
    num_set = set(nums)
    longest_streak = 0
    
    for num in num_set:
        if num - 1 not in num_set:
            current_num = num
            current_streak = 1
            
            while current_num + 1 in num_set:
                current_num += 1
                current_streak += 1
            
            longest_streak = max(longest_streak, current_streak)
    
    return longest_streak
```

### Java Code
```java
import java.util.HashSet;
import java.util.Set;

public class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }
        
        int longestStreak = 0;
        
        for (int num : numSet) {
            if (!numSet.contains(num - 1)) {
                int currentNum = num;
                int currentStreak = 1;
                
                while (numSet.contains(currentNum + 1)) {
                    currentNum += 1;
                    currentStreak += 1;
                }
                
                longestStreak = Math.max(longestStreak, currentStreak);
            }
        }
        
        return longestStreak;
    }
}
```

### Explanation

1. **Convert the Array to a Set**:
   - In both Python and Java, we convert the array `nums` to a set (`num_set = set(nums)` in Python and `Set<Integer> numSet = new HashSet<>();` followed by `numSet.add(num);` in Java) to allow O(1) time complexity for lookups.

2. **Initialize Variables**:
   - We initialize a variable `longest_streak` to keep track of the longest consecutive sequence length (`longest_streak = 0` in Python and `int longestStreak = 0;` in Java).

3. **Iterate Through the Array**:
   - We iterate through each number in the set.
   - For each number, we check if it is the start of a sequence by verifying if the previous number is not in the set (`if num - 1 not in num_set:` in Python and `if (!numSet.contains(num - 1)):` in Java).
   - If it is the start of a sequence, we initialize a counter (`current_streak = 1` in Python and `int currentStreak = 1;` in Java) and use a while loop to count the length of the sequence by checking for consecutive numbers.

4. **Update the Longest Sequence Length**:
   - We update the longest sequence length if the current sequence is longer than the previously recorded longest sequence (`longest_streak = max(longest_streak, current_streak)` in Python and `longestStreak = Math.max(longestStreak, currentStreak);` in Java).

5. **Return the Result**:
   - After processing all numbers, we return the length of the longest consecutive sequence (`return longest_streak` in Python and `return longestStreak;` in Java).

This approach ensures that we efficiently find the longest consecutive sequence using a set to track the numbers and a linear scan to find the sequences, making it an O(n) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.