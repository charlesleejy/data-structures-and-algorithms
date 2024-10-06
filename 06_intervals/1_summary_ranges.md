## Summary Ranges

### Problem Description
You are given a sorted unique integer array `nums`.

A range `[a,b]` is a continuous sequence of integers starting at `a` and ending at `b` (inclusive). The range `[a,b]` is represented as `"a->b"` if `a != b`, and `"a"` if `a == b`.

Return the smallest sorted list of ranges that cover all the numbers in the array exactly. That is, each element of `nums` is covered by exactly one of the ranges, and there is no integer `x` such that `a <= x <= b` is not in `nums`.

### Example
```
Input: nums = [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: The ranges are:
[0,2] --> "0->2"
[4,5] --> "4->5"
[7,7] --> "7"
```
```
Input: nums = [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: The ranges are:
[0,0] --> "0"
[2,4] --> "2->4"
[6,6] --> "6"
[8,9] --> "8->9"
```

### Solution Approach
To solve this problem, we need to iterate through the array and identify continuous sequences of numbers. We can keep track of the start and end of each range and add it to the result list.

### Steps in Detail

1. **Initialize Variables**:
   - Create an empty list `result` to store the ranges.
   - Use a variable `start` to mark the beginning of each range.

2. **Iterate Through the Array**:
   - Iterate through the array and check if the current number is not consecutive to the previous number.
   - If it is not consecutive, add the current range to the result and update `start`.

3. **Add the Last Range**:
   - After the loop, add the last range to the result list.

4. **Format the Ranges**:
   - For each range, if the start is equal to the end, add the single number to the result.
   - If the start is not equal to the end, format it as "start->end".

### Python Code
```python
def summary_ranges(nums):
    if not nums:
        return []
    
    result = []
    start = nums[0]
    
    for i in range(1, len(nums)):
        if nums[i] != nums[i - 1] + 1:
            if start == nums[i - 1]:
                result.append(str(start))
            else:
                result.append(f"{start}->{nums[i - 1]}")
            start = nums[i]
    
    if start == nums[-1]:
        result.append(str(start))
    else:
        result.append(f"{start}->{nums[-1]}")
    
    return result
```

### Java Code
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> result = new ArrayList<>();
        if (nums.length == 0) {
            return result;
        }
        
        int start = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i - 1] + 1) {
                if (start == nums[i - 1]) {
                    result.add(String.valueOf(start));
                } else {
                    result.add(start + "->" + nums[i - 1]);
                }
                start = nums[i];
            }
        }
        
        if (start == nums[nums.length - 1]) {
            result.add(String.valueOf(start));
        } else {
            result.add(start + "->" + nums[nums.length - 1]);
        }
        
        return result;
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we create an empty list `result` to store the ranges.
   - We use a variable `start` to mark the beginning of each range. It is initialized to the first element of the array.

2. **Iterate Through the Array**:
   - We iterate through the array starting from the second element.
   - For each element, we check if it is not consecutive to the previous element (`if nums[i] != nums[i - 1] + 1` in Python and `if (nums[i] != nums[i - 1] + 1)` in Java).
   - If it is not consecutive, we add the current range to the result:
     - If `start` is equal to the previous element, it means the range contains only one number, so we add it as a single number.
     - If `start` is not equal to the previous element, we format it as "start->end".
   - We then update `start` to the current element.

3. **Add the Last Range**:
   - After the loop, we add the last range to the result list:
     - If `start` is equal to the last element, we add it as a single number.
     - If `start` is not equal to the last element, we format it as "start->end".

4. **Return the Result**:
   - We return the `result` list containing all the ranges.

This approach ensures that we efficiently find and format the ranges of consecutive numbers in the array, making it an O(n) solution where n is the length of the array. This guarantees an efficient and straightforward solution to the problem.
