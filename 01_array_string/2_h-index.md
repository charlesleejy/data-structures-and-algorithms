## H-Index

### Problem Description
Given an array of integers `citations` where `citations[i]` is the number of citations a researcher received for their `i-th` paper, return the researcher's h-index.

The h-index is defined as the maximum value `h` such that the given researcher has published `h` papers that have each been cited at least `h` times.

### Example
```
Input: citations = [3,0,6,1,5]
Output: 3
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively. Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, their h-index is 3.
```
```
Input: citations = [1,3,1]
Output: 1
```

### Solution Approach
To solve this problem, we can sort the array of citations in descending order and then find the maximum `h` such that the `i-th` paper has at least `i + 1` citations.

### Steps in Detail

1. **Sorting**:
   - Sort the array of citations in descending order.

2. **Finding the H-Index**:
   - Iterate through the sorted array.
   - For each index `i`, check if the citation count at that index is greater than or equal to `i + 1`.
   - The maximum `i + 1` for which this condition holds true is the h-index.

### Python Code
```python
def h_index(citations):
    citations.sort(reverse=True)
    h = 0
    
    for i, citation in enumerate(citations):
        if citation >= i + 1:
            h = i + 1
        else:
            break
    
    return h
```

### Java Code
```java
import java.util.Arrays;

public class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int n = citations.length;
        int h = 0;
        
        for (int i = 0; i < n; i++) {
            int citation = citations[n - 1 - i];
            if (citation >= i + 1) {
                h = i + 1;
            } else {
                break;
            }
        }
        
        return h;
    }
}
```

### Explanation

1. **Sorting**:
   - In Python, we use `citations.sort(reverse=True)` to sort the citations array in descending order.
   - In Java, we use `Arrays.sort(citations);` followed by iterating from the end of the array to achieve a similar effect.

2. **Finding the H-Index**:
   - In Python, we initialize `h` to 0. We then iterate through the sorted array with `enumerate`, which gives both the index `i` and the citation count. For each citation, if it is greater than or equal to `i + 1`, we update `h` to `i + 1`. If the condition fails, we break the loop.
   - In Java, we similarly initialize `h` to 0. We iterate through the array from the end (`n - 1 - i`), checking if the citation count is greater than or equal to `i + 1`. If so, we update `h` to `i + 1`. If not, we break the loop.

3. **Completion**:
   - The final value of `h` after the loop completes is the h-index. It represents the maximum number of papers that have been cited at least `h` times.

This approach ensures that we sort the array first (O(n log n)) and then perform a linear scan (O(n)), making the overall time complexity O(n log n). The space complexity is O(1) since we are using only a few extra variables.