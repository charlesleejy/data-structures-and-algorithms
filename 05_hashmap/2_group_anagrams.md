## Group Anagrams

### Problem Description
Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

### Example
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```
```
Input: strs = [""]
Output: [[""]]
```
```
Input: strs = ["a"]
Output: [["a"]]
```

### Solution Approach
To group anagrams together, we can use a hashmap to store lists of words that are anagrams of each other. The key to the hashmap will be a sorted version of each word, which ensures that all anagrams will have the same key.

### Steps in Detail

1. **Initialize Hashmap**:
   - Use a hashmap to store lists of words that are anagrams of each other. The key will be the sorted version of the word.

2. **Group Anagrams**:
   - Iterate through each word in the input list.
   - For each word, sort its characters to get the key.
   - Add the original word to the list corresponding to the sorted key in the hashmap.

3. **Return the Result**:
   - Return the values of the hashmap as the grouped anagrams.

### Python Code
```python
def group_anagrams(strs):
    anagrams = {}
    
    for word in strs:
        sorted_word = ''.join(sorted(word))
        if sorted_word not in anagrams:
            anagrams[sorted_word] = []
        anagrams[sorted_word].append(word)
    
    return list(anagrams.values())
```

### Java Code
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> anagrams = new HashMap<>();
        
        for (String word : strs) {
            char[] charArray = word.toCharArray();
            Arrays.sort(charArray);
            String sortedWord = new String(charArray);
            
            if (!anagrams.containsKey(sortedWord)) {
                anagrams.put(sortedWord, new ArrayList<>());
            }
            anagrams.get(sortedWord).add(word);
        }
        
        return new ArrayList<>(anagrams.values());
    }
}
```

### Explanation

1. **Initialize Hashmap**:
   - In both Python and Java, we use a hashmap to store lists of words that are anagrams of each other. The key is the sorted version of the word.

2. **Group Anagrams**:
   - We iterate through each word in the input list.
   - In Python, we sort the characters of the word using `sorted(word)` and join them back to a string to get the key. In Java, we convert the word to a character array, sort it using `Arrays.sort(charArray)`, and convert it back to a string to get the key.
   - We then add the original word to the list corresponding to the sorted key in the hashmap. If the key is not already in the hashmap, we create a new list.

3. **Return the Result**:
   - We return the values of the hashmap as the grouped anagrams. In Python, we use `list(anagrams.values())`. In Java, we use `new ArrayList<>(anagrams.values())`.

This approach ensures that we efficiently group the anagrams together by using a sorted version of each word as the key in the hashmap, making it an O(n * k * log(k)) solution where n is the number of words and k is the maximum length of a word. This guarantees an efficient and straightforward solution to the problem.