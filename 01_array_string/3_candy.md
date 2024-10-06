## Candy

### Problem Description
There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

1. Each child must have at least one candy.
2. Children with a higher rating get more candies than their neighbors.

Return the minimum number of candies you need to have to distribute the candies to the children.

### Example
```
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the children with the following configuration [2,1,2].
```
```
Input: ratings = [1,2,2]
Output: 4
Explanation: You can allocate to the children with the following configuration [1,2,1].
The second child has a higher rating than the first child, so the second child gets more candies than the first one.
The third child has the same rating as the second child, so the third child can have 1 candy.
```

### Solution Approach
To solve this problem, we can use a two-pass approach. The idea is to ensure that each child gets more candies than their neighbor if they have a higher rating. We do this by making two passes through the array: one from left to right and another from right to left.

### Steps in Detail

1. **Initialization**:
   - Initialize an array `candies` with the same length as `ratings` and fill it with 1s, as each child must get at least one candy.

2. **Left to Right Pass**:
   - Traverse the `ratings` array from left to right.
   - For each child, if the current child's rating is higher than the previous child's rating, give the current child one more candy than the previous child.

3. **Right to Left Pass**:
   - Traverse the `ratings` array from right to left.
   - For each child, if the current child's rating is higher than the next child's rating, and if the current child does not already have more candies, give the current child one more candy than the next child.

4. **Sum Up Candies**:
   - Sum up all the values in the `candies` array to get the minimum number of candies required.

### Python Code
```python
def candy(ratings):
    n = len(ratings)
    candies = [1] * n
    
    # Left to right pass
    for i in range(1, n):
        if ratings[i] > ratings[i - 1]:
            candies[i] = candies[i - 1] + 1
    
    # Right to left pass
    for i in range(n - 2, -1, -1):
        if ratings[i] > ratings[i + 1]:
            candies[i] = max(candies[i], candies[i + 1] + 1)
    
    return sum(candies)
```

### Java Code
```java
public class Solution {
    public int candy(int[] ratings) {
        int n = ratings.length;
        int[] candies = new int[n];
        Arrays.fill(candies, 1);
        
        // Left to right pass
        for (int i = 1; i < n; i++) {
            if (ratings[i] > ratings[i - 1]) {
                candies[i] = candies[i - 1] + 1;
            }
        }
        
        // Right to left pass
        for (int i = n - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candies[i] = Math.max(candies[i], candies[i + 1] + 1);
            }
        }
        
        int totalCandies = 0;
        for (int candy : candies) {
            totalCandies += candy;
        }
        
        return totalCandies;
    }
}
```

### Explanation

1. **Initialization**:
   - In Python, we initialize `candies` with `[1] * n`, ensuring each child gets at least one candy.
   - In Java, we use `Arrays.fill(candies, 1)` for the same purpose.

2. **Left to Right Pass**:
   - We iterate through the `ratings` array from the second element to the end.
   - If the current rating is higher than the previous rating, we increase the current child's candies by one more than the previous child's candies.

3. **Right to Left Pass**:
   - We iterate through the `ratings` array from the second-to-last element to the beginning.
   - If the current rating is higher than the next rating, we update the current child's candies to be the maximum of its current candies or one more than the next child's candies.

4. **Sum Up Candies**:
   - In Python, we simply return `sum(candies)`.
   - In Java, we iterate through the `candies` array and sum up the values to get the total number of candies required.

This approach ensures that we traverse the array twice, making it an O(n) solution, and we use O(n) extra space for the `candies` array. This guarantees that each child receives the correct number of candies according to the problem constraints.
