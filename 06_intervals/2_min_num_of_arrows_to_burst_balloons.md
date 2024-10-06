## Minimum Number of Arrows to Burst Balloons

### Problem Description
You are given an array of `points` where `points[i] = [start_i, end_i]` represents the start and end of the `i`-th balloon. Balloons can be shot with arrows. An arrow can be shot exactly at any point `x` and it will burst all balloons whose range includes `x`. 

Return the minimum number of arrows that must be shot to burst all balloons.

### Example
```
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: One way is to shoot one arrow at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the balloons [10,16] and [7,12]).
```
```
Input: points = [[1,2],[3,4],[5,6],[7,8]]
Output: 4
```
```
Input: points = [[1,2],[2,3],[3,4],[4,5]]
Output: 2
```

### Solution Approach
To solve this problem efficiently, we can use a greedy algorithm by first sorting the intervals by their end points. Then, we iterate through the sorted intervals and keep track of the end point of the current arrow shot. If the start of the next interval is greater than the end point of the current arrow shot, it means we need to shoot a new arrow.

### Steps in Detail

1. **Sort the Intervals**:
   - Sort the intervals based on their end points.

2. **Initialize Variables**:
   - Use a variable to keep track of the number of arrows needed.
   - Use a variable to keep track of the end point of the current arrow shot.

3. **Iterate Through the Intervals**:
   - For each interval, check if the start of the current interval is greater than the end point of the current arrow shot.
   - If it is, increment the number of arrows and update the end point of the current arrow shot to the end point of the current interval.

4. **Return the Result**:
   - Return the number of arrows needed.

### Python Code
```python
def find_min_arrow_shots(points):
    if not points:
        return 0
    
    points.sort(key=lambda x: x[1])
    arrows = 1
    end = points[0][1]
    
    for start, end in points[1:]:
        if start > end:
            arrows += 1
            end = end
    
    return arrows
```

### Java Code
```java
import java.util.Arrays;

public class Solution {
    public int findMinArrowShots(int[][] points) {
        if (points.length == 0) {
            return 0;
        }
        
        Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));
        int arrows = 1;
        int end = points[0][1];
        
        for (int i = 1; i < points.length; i++) {
            if (points[i][0] > end) {
                arrows++;
                end = points[i][1];
            }
        }
        
        return arrows;
    }
}
```

### Explanation

1. **Sort the Intervals**:
   - In both Python and Java, we sort the intervals based on their end points.
   - In Python, we use `points.sort(key=lambda x: x[1])`.
   - In Java, we use `Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));`.

2. **Initialize Variables**:
   - We initialize a variable `arrows` to keep track of the number of arrows needed (`arrows = 1`).
   - We initialize a variable `end` to keep track of the end point of the current arrow shot (`end = points[0][1]`).

3. **Iterate Through the Intervals**:
   - We iterate through the sorted intervals starting from the second interval.
   - For each interval, we check if the start of the current interval is greater than the end point of the current arrow shot (`if start > end:` in Python and `if (points[i][0] > end) {` in Java).
   - If it is, we increment the number of arrows (`arrows += 1` in Python and `arrows++;` in Java) and update the end point of the current arrow shot (`end = end` in Python and `end = points[i][1];` in Java).

4. **Return the Result**:
   - We return the number of arrows needed (`return arrows` in Python and `return arrows;` in Java).

This approach ensures that we efficiently find the minimum number of arrows needed to burst all balloons by sorting the intervals and using a greedy algorithm to find the optimal points to shoot arrows, making it an O(n log n) solution due to the sorting step. This guarantees an efficient and straightforward solution to the problem.