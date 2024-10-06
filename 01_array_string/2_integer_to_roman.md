## Integer to Roman

### Problem Description
Given an integer, convert it to a Roman numeral. Input is guaranteed to be within the range from 1 to 3999.

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
- There are a few exceptions:
  - `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
  - `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
  - `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

### Example
```
Input: num = 3
Output: "III"
```
```
Input: num = 4
Output: "IV"
```
```
Input: num = 9
Output: "IX"
```
```
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3
```
```
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90, IV = 4
```

### Solution Approach
To convert an integer to a Roman numeral, we can use a greedy approach. This approach involves repeatedly subtracting the largest possible Roman numeral value until the entire integer has been converted.

### Steps in Detail

1. **Create Mappings**:
   - Create arrays to map integer values to their corresponding Roman numeral strings.

2. **Initialize Result**:
   - Initialize an empty string `result` to store the resulting Roman numeral.

3. **Greedy Conversion**:
   - Iterate through the integer values from largest to smallest.
   - For each value, while the current integer is greater than or equal to the value, append the corresponding Roman numeral string to `result` and subtract the value from the integer.

4. **Return Result**:
   - After processing all values, `result` will contain the converted Roman numeral.

### Python Code
```python
def int_to_roman(num):
    val = [
        1000, 900, 500, 400,
        100, 90, 50, 40,
        10, 9, 5, 4,
        1
        ]
    syms = [
        "M", "CM", "D", "CD",
        "C", "XC", "L", "XL",
        "X", "IX", "V", "IV",
        "I"
        ]
    result = ""
    for i in range(len(val)):
        while num >= val[i]:
            result += syms[i]
            num -= val[i]
    return result
```

### Java Code
```java
public class Solution {
    public String intToRoman(int num) {
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        
        StringBuilder result = new StringBuilder();
        
        for (int i = 0; i < values.length; i++) {
            while (num >= values[i]) {
                result.append(symbols[i]);
                num -= values[i];
            }
        }
        
        return result.toString();
    }
}
```

### Explanation

1. **Create Mappings**:
   - In both Python and Java, we create two arrays: one for the integer values (`val` in Python, `values` in Java) and one for the corresponding Roman numeral strings (`syms` in Python, `symbols` in Java).
   - These arrays are ordered from the largest value to the smallest value to facilitate the greedy approach.

2. **Initialize Result**:
   - In Python, we initialize `result` as an empty string.
   - In Java, we initialize `result` as a `StringBuilder` for efficient string concatenation.

3. **Greedy Conversion**:
   - We iterate through the `val`/`values` array.
   - For each value, while the current integer (`num`) is greater than or equal to the value:
     - In Python, we append the corresponding Roman numeral string from `syms` to `result` and subtract the value from `num`.
     - In Java, we append the corresponding Roman numeral string from `symbols` to `result` using `result.append(symbols[i])` and subtract the value from `num`.

4. **Return Result**:
   - In Python, we return `result` as the final Roman numeral string.
   - In Java, we return `result.toString()` as the final Roman numeral string.

This approach ensures that we efficiently convert the integer to a Roman numeral by repeatedly subtracting the largest possible Roman numeral values, making it an O(1) solution due to the fixed number of Roman numeral values.
