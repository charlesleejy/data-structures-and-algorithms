## Insert Interval

### Problem Description
You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [start_i, end_i]` represent the start and the end of the `i`-th interval and `intervals` is sorted in ascending order by `start_i`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `start_i` and `intervals` still do not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

### Example
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

### Solution Approach
To insert the new interval into the list of intervals and merge any overlapping intervals, we can follow these steps:

1. **Initialize Variables**:
   - Create an empty list to store the result intervals.
   - Use an index to iterate through the given intervals.

2. **Add Non-Overlapping Intervals**:
   - Add all intervals that end before the new interval starts to the result list.

3. **Merge Overlapping Intervals**:
   - For all intervals that overlap with the new interval, merge them into a single interval.

4. **Add Remaining Intervals**:
   - Add all intervals that start after the new interval ends to the result list.

5. **Return the Result**:
   - Return the list of merged intervals.

### Python Code
```python
def insert(intervals, newInterval):
    result = []
    i = 0
    n = len(intervals)
    
    # Add all intervals that end before the new interval starts
    while i < n and intervals[i][1] < newInterval[0]:
        result.append(intervals[i])
        i += 1
    
    # Merge all overlapping intervals with the new interval
    while i < n and intervals[i][0] <= newInterval[1]:
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i += 1
    result.append(newInterval)
    
    # Add the remaining intervals
    while i < n:
        result.append(intervals[i])
        i += 1
    
    return result
```

### Java Code
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> result = new ArrayList<>();
        int i = 0;
        int n = intervals.length;
        
        // Add all intervals that end before the new interval starts
        while (i < n && intervals[i][1] < newInterval[0]) {
            result.add(intervals[i]);
            i++;
        }
        
        // Merge all overlapping intervals with the new interval
        while (i < n && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
            newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
            i++;
        }
        result.add(newInterval);
        
        // Add the remaining intervals
        while (i < n) {
            result.add(intervals[i]);
            i++;
        }
        
        return result.toArray(new int[result.size()][]);
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we initialize an empty list `result` to store the merged intervals.
   - We use an index `i` to iterate through the given intervals.

2. **Add Non-Overlapping Intervals**:
   - We iterate through the intervals and add all intervals that end before the new interval starts to the result list.
   - In Python, we use a while loop: `while i < n and intervals[i][1] < newInterval[0]:`.
   - In Java, we use a similar while loop: `while (i < n && intervals[i][1] < newInterval[0]) {`.

3. **Merge Overlapping Intervals**:
   - For all intervals that overlap with the new interval, we merge them into a single interval by updating the start and end of `newInterval`.
   - In Python, we use a while loop: `while i < n and intervals[i][0] <= newInterval[1]:`.
   - In Java, we use a similar while loop: `while (i < n && intervals[i][0] <= newInterval[1]) {`.

4. **Add Remaining Intervals**:
   - We iterate through the remaining intervals and add them to the result list.
   - In Python, we use a while loop: `while i < n:`.
   - In Java, we use a similar while loop: `while (i < n) {`.

5. **Return the Result**:
   - In Python, we return the `result` list directly.
   - In Java, we convert the `ArrayList` to an array and return it using `result.toArray(new int[result.size()][]);`.

This approach ensures that we efficiently insert the new interval and merge overlapping intervals by iterating through the intervals and performing the necessary operations in O(n) time complexity where n is the number of intervals. This guarantees an efficient and straightforward solution to the problem.