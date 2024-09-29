## Best Time to Buy and Sell Stock II

### Problem Description
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day. You want to maximize your profit by choosing a series of buy and sell transactions. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

### Example
```
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4. Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```
```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
```
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done, and the max profit = 0.
```

### Solution Approach
The key idea to maximize profit in this problem is to capture all the upward price movements. In other words, you should buy before every upward slope and sell at the peak. This can be achieved by simply adding up all the positive differences between consecutive days.

### Steps in Detail

1. **Initialization**:
   - Initialize `max_profit` to 0 to keep track of the total profit.

2. **Iteration**:
   - Iterate through the prices array from the first day to the last day.
   - For each day, if the price of the next day is higher than the current day's price, add the difference to `max_profit`.

3. **Completion**:
   - After iterating through the array, `max_profit` will hold the maximum profit that can be achieved through multiple transactions.

### Python Code
```python
def max_profit(prices):
    max_profit = 0
    
    for i in range(1, len(prices)):
        if prices[i] > prices[i - 1]:
            max_profit += prices[i] - prices[i - 1]
    
    return max_profit
```

### Java Code
```java
public class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                maxProfit += prices[i] - prices[i - 1];
            }
        }
        
        return maxProfit;
    }
}
```

### Explanation

1. **Initialization**:
   - We start by setting `max_profit` to 0 because initially, we have no profit.

2. **Iteration**:
   - We iterate through the prices array starting from the second element (`i = 1`).
   - For each day, we compare the current price (`prices[i]`) with the previous day's price (`prices[i - 1]`).
   - If the current price is higher than the previous day's price, it means there is an upward movement, and we add the difference to `max_profit`.

3. **Completion**:
   - After iterating through the entire array, `max_profit` will contain the sum of all positive differences between consecutive days, representing the maximum profit achievable through multiple transactions.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the `max_profit` variable.