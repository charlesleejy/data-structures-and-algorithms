## Text Justification

### Problem Description
Given an array of words and a width `maxWidth`, format the text such that each line has exactly `maxWidth` characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly `maxWidth` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified and no extra space is inserted between words.

### Example
```
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```
```
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
   "What   must   be",
   "acknowledgment  ",
   "shall be        "
]
```
```
Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
   "Science  is  what we",
   "understand      well",
   "enough to explain to",
   "a  computer.  Art is",
   "everything  else  we",
   "do                  "
]
```

### Solution Approach
To solve this problem, we need to construct each line by packing as many words as possible while ensuring each line is fully justified (except the last line, which should be left-justified).

### Steps in Detail

1. **Initialization**:
   - Initialize an empty list `result` to store the final lines of text.
   - Initialize an empty list `current_line` to store the words for the current line.
   - Initialize a variable `current_length` to keep track of the length of the current line (excluding spaces).

2. **Pack Words into Lines**:
   - Iterate through each word in the `words` list.
   - For each word, check if adding the word to the `current_line` (with necessary spaces) would exceed `maxWidth`.
   - If it does, justify the `current_line` and add it to the `result`, then reset `current_line` and `current_length`.
   - If it doesn't, add the word to the `current_line` and update `current_length`.

3. **Justify Lines**:
   - To justify a line, calculate the number of spaces needed and distribute them as evenly as possible.
   - For the last line or a line with only one word, left-justify it.

4. **Handle the Last Line**:
   - After the loop, justify the last `current_line` and add it to the `result`.

5. **Return the Result**:
   - Return the `result` list containing all justified lines.

### Python Code
```python
def full_justify(words, maxWidth):
    result = []
    current_line = []
    current_length = 0
    
    for word in words:
        if current_length + len(word) + len(current_line) > maxWidth:
            for i in range(maxWidth - current_length):
                current_line[i % (len(current_line) - 1 or 1)] += ' '
            result.append(''.join(current_line))
            current_line, current_length = [], 0
        current_line.append(word)
        current_length += len(word)
    
    result.append(' '.join(current_line).ljust(maxWidth))
    return result
```

### Java Code
```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> result = new ArrayList<>();
        List<String> currentLine = new ArrayList<>();
        int currentLength = 0;
        
        for (String word : words) {
            if (currentLength + word.length() + currentLine.size() > maxWidth) {
                for (int i = 0; i < maxWidth - currentLength; i++) {
                    currentLine.set(i % (currentLine.size() - 1 == 0 ? 1 : currentLine.size() - 1), currentLine.get(i % (currentLine.size() - 1 == 0 ? 1 : currentLine.size() - 1)) + " ");
                }
                result.add(String.join("", currentLine));
                currentLine.clear();
                currentLength = 0;
            }
            currentLine.add(word);
            currentLength += word.length();
        }
        
        result.add(String.join(" ", currentLine) + " ".repeat(maxWidth - currentLength - currentLine.size() + 1));
        return result;
    }
}
```

### Explanation

1. **Initialization**:
   - In both Python and Java, we initialize `result` to store the final justified lines.
   - We use `current_line` to store the words for the current line and `current_length` to keep track of the length of the current line.

2. **Pack Words into Lines**:
   - We iterate through each word in `words`.
   - For each word, we check if adding it to `current_line` would exceed `maxWidth`.
   - If it would exceed, we justify the `current_line` and add it to `result`. Then, we reset `current_line` and `current_length`.

3. **Justify Lines**:
   - To justify a line, we calculate the number of spaces needed and distribute them as evenly as possible among the words.
   - For the last line or a line with only one word, we left-justify it using `.ljust()` in Python or appending spaces in Java.

4. **Handle the Last Line**:
   - After iterating through all words, we justify the last `current_line` and add it to `result`.

5. **Return the Result**:
   - We return the `result` list containing all justified lines.

This approach ensures that we efficiently justify each line by distributing spaces evenly and handling edge cases, making it an O(n) solution where n is the total number of characters in the input words. This guarantees a clear and efficient solution to the problem.