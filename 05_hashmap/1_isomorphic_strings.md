## Isomorphic Strings

### Problem Description
Given two strings `s` and `t`, determine if they are isomorphic.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

### Example
```
Input: s = "egg", t = "add"
Output: true
```
```
Input: s = "foo", t = "bar"
Output: false
```
```
Input: s = "paper", t = "title"
Output: true
```

### Solution Approach
To determine if two strings are isomorphic, we need to ensure that there is a one-to-one mapping between every character of `s` and `t`. We can use two hashmaps to track the mappings from `s` to `t` and from `t` to `s`.

### Steps in Detail

1. **Check Lengths**:
   - If the lengths of `s` and `t` are not equal, they cannot be isomorphic, so return `false`.

2. **Initialize Hashmaps**:
   - Use two hashmaps (or dictionaries) to store the character mappings from `s` to `t` and from `t` to `s`.

3. **Iterate Through Characters**:
   - For each character pair `(char_s, char_t)` in `s` and `t`:
     - Check if `char_s` is already mapped to a different character than `char_t` in the `s_to_t` hashmap.
     - Check if `char_t` is already mapped to a different character than `char_s` in the `t_to_s` hashmap.
     - If either check fails, return `false`.
     - Otherwise, add the mappings `char_s -> char_t` and `char_t -> char_s` to the respective hashmaps.

4. **Return the Result**:
   - If all character pairs are consistent, return `true`.

### Python Code
```python
def is_isomorphic(s, t):
    if len(s) != len(t):
        return False
    
    s_to_t = {}
    t_to_s = {}
    
    for char_s, char_t in zip(s, t):
        if (char_s in s_to_t and s_to_t[char_s] != char_t) or (char_t in t_to_s and t_to_s[char_t] != char_s):
            return False
        s_to_t[char_s] = char_t
        t_to_s[char_t] = char_s
    
    return True
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        
        Map<Character, Character> sToT = new HashMap<>();
        Map<Character, Character> tToS = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char charS = s.charAt(i);
            char charT = t.charAt(i);
            
            if ((sToT.containsKey(charS) && sToT.get(charS) != charT) || 
                (tToS.containsKey(charT) && tToS.get(charT) != charS)) {
                return false;
            }
            
            sToT.put(charS, charT);
            tToS.put(charT, charS);
        }
        
        return true;
    }
}
```

### Explanation

1. **Check Lengths**:
   - In both Python and Java, we check if the lengths of `s` and `t` are different. If they are, we return `false` because the strings cannot be isomorphic if they have different lengths.

2. **Initialize Hashmaps**:
   - We initialize two hashmaps: `s_to_t` for storing the mapping from characters in `s` to characters in `t`, and `t_to_s` for storing the reverse mapping.

3. **Iterate Through Characters**:
   - We iterate through each character pair `(char_s, char_t)` from `s` and `t`:
     - We check if `char_s` is already mapped to a different character than `char_t` in the `s_to_t` hashmap.
     - We check if `char_t` is already mapped to a different character than `char_s` in the `t_to_s` hashmap.
     - If either condition is true, we return `false` because the mappings are inconsistent.
     - If the checks pass, we add the mappings `char_s -> char_t` and `char_t -> char_s` to the respective hashmaps.

4. **Return the Result**:
   - After processing all character pairs, if no inconsistencies are found, we return `true`, indicating that the strings are isomorphic.

This approach ensures that we efficiently determine if the two strings are isomorphic by using two hashmaps to track the character mappings, making it an O(n) solution where n is the length of the strings. This guarantees an efficient and straightforward solution to the problem.