## Reverse Words in a String

### Problem Description
Given an input string `s`, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in `s` will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

### Example
```
Input: s = "the sky is blue"
Output: "blue is sky the"
```
```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```
```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

### Solution Approach
To solve this problem, we need to follow these steps:
1. Split the input string into words.
2. Reverse the list of words.
3. Join the reversed list of words with a single space.

### Steps in Detail

1. **Trim Leading and Trailing Spaces**:
   - Remove leading and trailing spaces from the string.

2. **Split the String**:
   - Split the string by spaces into a list of words.

3. **Reverse the List**:
   - Reverse the list of words.

4. **Join the Words**:
   - Join the reversed list of words with a single space.

### Python Code
```python
def reverse_words(s):
    # Split the string into words
    words = s.strip().split()
    # Reverse the list of words
    words.reverse()
    # Join the words with a single space
    return ' '.join(words)
```

### Java Code
```java
public class Solution {
    public String reverseWords(String s) {
        // Split the string into words
        String[] words = s.trim().split("\\s+");
        // Reverse the list of words
        Collections.reverse(Arrays.asList(words));
        // Join the words with a single space
        return String.join(" ", words);
    }
}
```

### Explanation

1. **Trim Leading and Trailing Spaces**:
   - In Python, `s.strip()` is used to remove leading and trailing spaces.
   - In Java, `s.trim()` is used for the same purpose.

2. **Split the String**:
   - In Python, `s.strip().split()` splits the string into a list of words, automatically handling multiple spaces.
   - In Java, `s.trim().split("\\s+")` splits the string by one or more spaces using a regular expression, handling multiple spaces between words.

3. **Reverse the List**:
   - In Python, `words.reverse()` reverses the list of words in place.
   - In Java, `Collections.reverse(Arrays.asList(words))` reverses the list of words.

4. **Join the Words**:
   - In Python, `' '.join(words)` joins the reversed list of words with a single space.
   - In Java, `String.join(" ", words)` joins the reversed list of words with a single space.

This approach ensures that we handle leading, trailing, and multiple spaces between words efficiently, making it an O(n) solution where n is the length of the string. This guarantees an efficient and straightforward solution to the problem.