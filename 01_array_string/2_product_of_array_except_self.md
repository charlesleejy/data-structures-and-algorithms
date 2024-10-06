## Product of Array Except Self

### Problem Description
Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`. The solution should run in O(n) time and without using the division operation.

### Example
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Explanation:
- The product of all elements except nums[0] is 2*3*4 = 24.
- The product of all elements except nums[1] is 1*3*4 = 12.
- The product of all elements except nums[2] is 1*2*4 = 8.
- The product of all elements except nums[3] is 1*2*3 = 6.
```
```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

### Solution Approach
To solve this problem without division and in O(n) time, we can use a two-pass approach where we build the result array using prefix and suffix products.

### Steps in Detail

1. **Initialization**:
   - Initialize the result array `answer` with ones, which will store the final product except self for each index.

2. **First Pass (Left Product)**:
   - Traverse the array from left to right to calculate the prefix products (products of all elements to the left of the current element).
   - Store these products in the `answer` array.

3. **Second Pass (Right Product)**:
   - Traverse the array from right to left to calculate the suffix products (products of all elements to the right of the current element).
   - Multiply the suffix product with the prefix product stored in `answer` to get the final result.

### Python Code
```python
def product_except_self(nums):
    n = len(nums)
    answer = [1] * n
    
    # First pass: calculate left product
    left_product = 1
    for i in range(n):
        answer[i] = left_product
        left_product *= nums[i]
    
    # Second pass: calculate right product and final answer
    right_product = 1
    for i in range(n - 1, -1, -1):
        answer[i] *= right_product
        right_product *= nums[i]
    
    return answer
```

### Java Code
```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] answer = new int[n];
        
        // First pass: calculate left product
        answer[0] = 1;
        for (int i = 1; i < n; i++) {
            answer[i] = nums[i - 1] * answer[i - 1];
        }
        
        // Second pass: calculate right product and final answer
        int rightProduct = 1;
        for (int i = n - 1; i >= 0; i--) {
            answer[i] *= rightProduct;
            rightProduct *= nums[i];
        }
        
        return answer;
    }
}
```

### Explanation

1. **Initialization**:
   - In Python, we initialize the `answer` list with `[1] * n`.
   - In Java, we initialize the `answer` array with `new int[n]`.

2. **First Pass (Left Product)**:
   - In Python, we initialize `left_product` to 1 and iterate through the array from left to right. For each index `i`, we set `answer[i]` to `left_product` and then update `left_product` to be the product of `left_product` and `nums[i]`.
   - In Java, we initialize the first element of `answer` to 1 and iterate through the array from the second element. For each index `i`, we set `answer[i]` to the product of the previous element in `answer` and `nums[i - 1]`.

3. **Second Pass (Right Product)**:
   - In Python, we initialize `right_product` to 1 and iterate through the array from right to left. For each index `i`, we multiply `answer[i]` by `right_product` and then update `right_product` to be the product of `right_product` and `nums[i]`.
   - In Java, we initialize `rightProduct` to 1 and iterate through the array from the last element to the first. For each index `i`, we multiply `answer[i]` by `rightProduct` and then update `rightProduct` to be the product of `rightProduct` and `nums[i]`.

This approach ensures that we traverse the array twice, making it an O(n) solution, and we use only O(n) extra space for the `answer` array and O(1) extra space for the `left_product` and `right_product` variables.
