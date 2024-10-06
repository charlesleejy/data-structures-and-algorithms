## Substring with Concatenation of All Words

### Problem Description
You are given a string `s` and an array of strings `words` of the same length. Return all starting indices of substring(s) in `s` that is a concatenation of each word in `words` exactly once, in any order, and without any intervening characters.

You can return the answer in any order.

### Example
```
Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```
```
Input: s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
Output: []
```
```
Input: s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
Output: [6,9,12]
```

### Solution Approach
To solve this problem, we need to use a sliding window approach combined with a hashmap to keep track of the count of words. The key steps involve:
1. Determining the total length of the concatenation of all words.
2. Using a sliding window to check substrings of this length in the string `s`.

### Steps in Detail

1. **Initialize Variables**:
   - Calculate the length of each word (`word_length`).
   - Calculate the number of words (`num_words`).
   - Calculate the total length of all concatenated words (`total_length`).

2. **Count Words**:
   - Use a hashmap to count the frequency of each word in `words`.

3. **Sliding Window Approach**:
   - Use a sliding window of size `total_length` to check each possible starting index in `s`.
   - For each starting index, use a nested loop to extract each word-length substring and compare its frequency with the hashmap.

4. **Check Validity**:
   - If the substring matches the frequency of words in the hashmap, record the starting index.
   - Continue sliding the window to the right.

### Python Code
```python
def find_substring(s, words):
    if not s or not words:
        return []
    
    word_length = len(words[0])
    num_words = len(words)
    total_length = word_length * num_words
    word_count = {}
    
    for word in words:
        word_count[word] = word_count.get(word, 0) + 1
    
    result = []
    
    for i in range(word_length):
        left = i
        right = i
        current_count = {}
        count = 0
        
        while right + word_length <= len(s):
            word = s[right:right + word_length]
            right += word_length
            
            if word in word_count:
                current_count[word] = current_count.get(word, 0) + 1
                count += 1
                
                while current_count[word] > word_count[word]:
                    left_word = s[left:left + word_length]
                    left += word_length
                    current_count[left_word] -= 1
                    count -= 1
                
                if count == num_words:
                    result.append(left)
            else:
                current_count.clear()
                count = 0
                left = right
    
    return result
```

### Java Code
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> result = new ArrayList<>();
        if (s == null || words == null || words.length == 0) {
            return result;
        }
        
        int wordLength = words[0].length();
        int numWords = words.length;
        int totalLength = wordLength * numWords;
        Map<String, Integer> wordCount = new HashMap<>();
        
        for (String word : words) {
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }
        
        for (int i = 0; i < wordLength; i++) {
            int left = i, right = i, count = 0;
            Map<String, Integer> currentCount = new HashMap<>();
            
            while (right + wordLength <= s.length()) {
                String word = s.substring(right, right + wordLength);
                right += wordLength;
                
                if (wordCount.containsKey(word)) {
                    currentCount.put(word, currentCount.getOrDefault(word, 0) + 1);
                    count++;
                    
                    while (currentCount.get(word) > wordCount.get(word)) {
                        String leftWord = s.substring(left, left + wordLength);
                        left += wordLength;
                        currentCount.put(leftWord, currentCount.get(leftWord) - 1);
                        count--;
                    }
                    
                    if (count == numWords) {
                        result.add(left);
                    }
                } else {
                    currentCount.clear();
                    count = 0;
                    left = right;
                }
            }
        }
        
        return result;
    }
}
```

### Explanation

1. **Initialize Variables**:
   - In both Python and Java, we calculate the length of each word (`word_length`), the number of words (`num_words`), and the total length of all concatenated words (`total_length`).
   - We use a hashmap (`word_count`) to store the frequency of each word in `words`.

2. **Sliding Window Approach**:
   - We use a sliding window approach to check substrings of size `total_length` in `s`.
   - In Python, we use a for loop with range `word_length` to ensure we check all possible starting points.
   - In Java, we use a similar for loop structure.

3. **Count Words**:
   - As we slide the window, we extract each word-length substring and compare its frequency with `word_count`.
   - We maintain a hashmap (`current_count`) to track the frequency of words within the current window.

4. **Check Validity**:
   - If the frequency of a word exceeds its count in `word_count`, we adjust the window by moving the left pointer.
   - If the current window contains all words with the correct frequency, we add the starting index to the result.

5. **Return the Result**:
   - After checking all possible windows, we return the list of starting indices.

This approach ensures that we efficiently find all starting indices using the sliding window technique and hashmap, making it an O(n * m) solution where n is the length of `s` and m is the total length of concatenated words. This guarantees an efficient and straightforward solution to the problem.