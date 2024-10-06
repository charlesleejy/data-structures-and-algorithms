## Word Pattern

### Problem Description
Given a pattern and a string `s`, find if `s` follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in `s`.

### Example
```
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```
```
Input: pattern = "abba", s = "dog cat cat fish"
Output: false
```
```
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false
```
```
Input: pattern = "abba", s = "dog dog dog dog"
Output: false
```

### Solution Approach
To determine if the string `s` follows the given pattern, we need to ensure there is a one-to-one correspondence between each character in the pattern and each word in the string. We can use two hashmaps to track the mappings between characters and words in both directions.

### Steps in Detail

1. **Split the String**:
   - Split the string `s` into words using spaces as the delimiter.

2. **Check Lengths**:
   - If the length of the pattern and the number of words in `s` are not equal, return `false` since they cannot match.

3. **Initialize Hashmaps**:
   - Use two hashmaps to store the mapping from pattern characters to words and from words to pattern characters.

4. **Iterate Through Pattern and Words**:
   - For each character in the pattern and the corresponding word in the split string:
     - Check if the current character is already mapped to a different word.
     - Check if the current word is already mapped to a different character.
     - If either check fails, return `false`.
     - If the checks pass, add the mappings to the respective hashmaps.

5. **Return the Result**:
   - If all character and word pairs are consistent, return `true`.

### Python Code
```python
def word_pattern(pattern, s):
    words = s.split()
    if len(pattern) != len(words):
        return False
    
    char_to_word = {}
    word_to_char = {}
    
    for char, word in zip(pattern, words):
        if char in char_to_word and char_to_word[char] != word:
            return False
        if word in word_to_char and word_to_char[word] != char:
            return False
        char_to_word[char] = word
        word_to_char[word] = char
    
    return True
```

### Java Code
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");
        if (pattern.length() != words.length) {
            return false;
        }
        
        Map<Character, String> charToWord = new HashMap<>();
        Map<String, Character> wordToChar = new HashMap<>();
        
        for (int i = 0; i < pattern.length(); i++) {
            char charPattern = pattern.charAt(i);
            String word = words[i];
            
            if (charToWord.containsKey(charPattern) && !charToWord.get(charPattern).equals(word)) {
                return false;
            }
            if (wordToChar.containsKey(word) && wordToChar.get(word) != charPattern) {
                return false;
            }
            
            charToWord.put(charPattern, word);
            wordToChar.put(word, charPattern);
        }
        
        return true;
    }
}
```

### Explanation

1. **Split the String**:
   - In Python, we use `s.split()` to split the string `s` into a list of words.
   - In Java, we use `s.split(" ")` to achieve the same.

2. **Check Lengths**:
   - We compare the length of the pattern with the number of words in the split string. If they are not equal, we return `false`.

3. **Initialize Hashmaps**:
   - In both Python and Java, we initialize two hashmaps: one to map pattern characters to words (`char_to_word`) and one to map words to pattern characters (`word_to_char`).

4. **Iterate Through Pattern and Words**:
   - We iterate through each character in the pattern and the corresponding word in the split string:
     - We check if the current character is already mapped to a different word in `char_to_word`.
     - We check if the current word is already mapped to a different character in `word_to_char`.
     - If either condition is true, we return `false`.
     - If the checks pass, we add the mappings to the respective hashmaps.

5. **Return the Result**:
   - After processing all character and word pairs, if no inconsistencies are found, we return `true`.

This approach ensures that we efficiently check if the string `s` follows the given pattern using two hashmaps to track the character-to-word and word-to-character mappings, making it an O(n) solution where n is the length of the pattern. This guarantees an efficient and straightforward solution to the problem.