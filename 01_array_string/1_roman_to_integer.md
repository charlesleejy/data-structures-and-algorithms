## Roman to Integer

### Problem Description
Given a Roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

### Roman Numerals
Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D`, and `M`.

| Symbol | Value |
|--------|-------|
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

### Rules
- Roman numerals are usually written largest to smallest from left to right.
- However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four.
- The same principle applies to the number nine, which is written as `IX`.
- There are six instances where subtraction is used:
  - `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
  - `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
  - `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

### Example
```
Input: s = "III"
Output: 3
```
```
Input: s = "IV"
Output: 4
```
```
Input: s = "IX"
Output: 9
```
```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V = 5, III = 3
```
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90, IV = 4
```

### Solution Approach
To convert a Roman numeral to an integer, we need to consider the value of each symbol and handle the subtraction cases properly. We can do this by iterating through the string and comparing the current symbol with the next symbol.

### Steps in Detail

1. **Create a Dictionary**:
   - Create a dictionary to map Roman symbols to their integer values.

2. **Initialize Variables**:
   - Initialize a variable `total` to store the resulting integer.
   - Initialize a variable `prev_value` to keep track of the value of the previous symbol.

3. **Iterate Through the String**:
   - Iterate through the string from right to left.
   - For each symbol, get its value from the dictionary.
   - If the current value is less than `prev_value`, subtract the current value from `total` (this handles the subtraction cases).
   - Otherwise, add the current value to `total`.
   - Update `prev_value` to the current value.

4. **Return the Result**:
   - After the loop, return `total` as the converted integer.

### Python Code
```python
def roman_to_int(s):
    roman_to_int_map = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    }
    
    total = 0
    prev_value = 0
    
    for symbol in reversed(s):
        value = roman_to_int_map[symbol]
        if value < prev_value:
            total -= value
        else:
            total += value
        prev_value = value
    
    return total
```

### Java Code
```java
public class Solution {
    public int romanToInt(String s) {
        Map<Character, Integer> romanToIntMap = new HashMap<>();
        romanToIntMap.put('I', 1);
        romanToIntMap.put('V', 5);
        romanToIntMap.put('X', 10);
        romanToIntMap.put('L', 50);
        romanToIntMap.put('C', 100);
        romanToIntMap.put('D', 500);
        romanToIntMap.put('M', 1000);
        
        int total = 0;
        int prevValue = 0;
        
        for (int i = s.length() - 1; i >= 0; i--) {
            char symbol = s.charAt(i);
            int value = romanToIntMap.get(symbol);
            if (value < prevValue) {
                total -= value;
            } else {
                total += value;
            }
            prevValue = value;
        }
        
        return total;
    }
}
```

### Explanation

1. **Create a Dictionary**:
   - In Python, we use a dictionary `roman_to_int_map` to map Roman symbols to their integer values.
   - In Java, we use a `HashMap<Character, Integer>` for the same purpose.

2. **Initialize Variables**:
   - In both Python and Java, we initialize `total` to 0 and `prev_value` to 0.

3. **Iterate Through the String**:
   - We iterate through the string from right to left. In Python, we use `reversed(s)` to reverse the string, and in Java, we use a for loop starting from `s.length() - 1`.
   - For each symbol, we get its integer value from the dictionary/map.
   - If the current value is less than `prev_value`, it indicates a subtraction case, so we subtract the current value from `total`.
   - Otherwise, we add the current value to `total`.
   - We update `prev_value` to the current value to use it for comparison in the next iteration.

4. **Return the Result**:
   - After processing all symbols, `total` contains the converted integer, which we return.

This approach ensures that we traverse the string only once, making it an O(n) solution, and we use O(1) extra space for the dictionary/map and the variables. This guarantees an efficient and straightforward solution to the problem.