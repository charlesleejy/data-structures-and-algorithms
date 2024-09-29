## Best Time to Buy and Sell Stock

### Problem Description
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

### Example
```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6 - 1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done, and the max profit = 0.
```

### Solution Approach
To solve this problem, we need to keep track of the minimum price we have seen so far and calculate the maximum profit we can achieve by selling on each day. This can be done in a single pass through the array.

Here are the detailed steps:

1. **Initialization**:
   - Initialize `min_price` to a very high value (infinity).
   - Initialize `max_profit` to 0.

2. **Iteration**:
   - Iterate through each price in the array.
   - Update `min_price` to be the minimum of the current `min_price` and the current price.
   - Calculate the profit if we were to sell at the current price, which is the difference between the current price and `min_price`.
   - Update `max_profit` to be the maximum of the current `max_profit` and the calculated profit.

3. **Completion**:
   - After iterating through the array, `max_profit` will hold the maximum profit that can be achieved.

### Python Code
```python
def max_profit(prices):
    min_price = float('inf')
    max_profit = 0
    
    for price in prices:
        if price < min_price:
            min_price = price
        elif price - min_price > max_profit:
            max_profit = price - min_price
    
    return max_profit
```

### Java Code
```java
public class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;
        
        for (int price : prices) {
            if (price < minPrice) {
                minPrice = price;
            } else if (price - minPrice > maxProfit) {
                maxProfit = price - minPrice;
            }
        }
        
        return maxProfit;
    }
}
```

### Explanation

1. **Initialization**:
   - We start by setting `min_price` to a very high value (`float('inf')` in Python and `Integer.MAX_VALUE` in Java) so that any price we encounter will be lower and thus update `min_price`.
   - We set `max_profit` to 0 because initially, we have no profit.

2. **Iteration**:
   - As we iterate through each price:
     - We update `min_price` to be the minimum of the current `min_price` and the current price.
     - We calculate the potential profit by subtracting `min_price` from the current price.
     - If this potential profit is greater than `max_profit`, we update `max_profit`.

3. **Completion**:
   - After iterating through all the prices, `max_profit` will contain the maximum profit that can be achieved by buying and selling the stock on different days.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the variables `min_price` and `max_profit`.