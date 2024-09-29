## Insert Delete GetRandom O(1)

### Problem Description
Design a data structure that supports all following operations in average O(1) time.

1. `insert(val)`: Inserts an item `val` into the set if not already present.
2. `remove(val)`: Removes an item `val` from the set if present.
3. `getRandom()`: Returns a random element from the current set of elements. Each element must have the same probability of being returned.

### Example
```
Input: 
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
Output: 
[null, true, false, true, 2, true, false, 2]
Explanation:
RandomizedSet randomSet = new RandomizedSet();
randomSet.insert(1); // Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomSet.remove(2); // Returns false as 2 does not exist in the set.
randomSet.insert(2); // Inserts 2 to the set, returns true. Set now contains [1,2].
randomSet.getRandom(); // getRandom() should return either 1 or 2 randomly.
randomSet.remove(1); // Removes 1 from the set, returns true. Set now contains [2].
randomSet.insert(2); // 2 was already in the set, so return false.
randomSet.getRandom(); // Since 2 is the only number in the set, getRandom() will always return 2.
```

### Solution Approach
To achieve O(1) time complexity for `insert`, `remove`, and `getRandom` operations, we use a combination of a list and a dictionary.

1. **List**:
   - Stores the elements.
   - Provides O(1) access to any element.

2. **Dictionary (HashMap)**:
   - Maps each element to its index in the list.
   - Provides O(1) insert and delete operations.

### Steps in Detail

1. **Insert Operation**:
   - Check if the element is already in the dictionary.
   - If not, add it to the end of the list and update the dictionary with its index.

2. **Remove Operation**:
   - Check if the element is in the dictionary.
   - If so, swap the element with the last element in the list, update the dictionary for the swapped element, remove the element from the list, and delete it from the dictionary.

3. **GetRandom Operation**:
   - Use Python's `random.choice` or Java's `Random` class to return a random element from the list.

### Python Code
```python
import random

class RandomizedSet:

    def __init__(self):
        self.dict = {}
        self.list = []

    def insert(self, val: int) -> bool:
        if val in self.dict:
            return False
        self.dict[val] = len(self.list)
        self.list.append(val)
        return True

    def remove(self, val: int) -> bool:
        if val not in self.dict:
            return False
        # Move the last element to the place of the element to delete
        last_element = self.list[-1]
        index_to_remove = self.dict[val]
        self.list[index_to_remove] = last_element
        self.dict[last_element] = index_to_remove
        # Remove the last element
        self.list.pop()
        del self.dict[val]
        return True

    def getRandom(self) -> int:
        return random.choice(self.list)
```

### Java Code
```java
import java.util.*;

public class RandomizedSet {
    private Map<Integer, Integer> dict;
    private List<Integer> list;
    private Random rand;

    public RandomizedSet() {
        dict = new HashMap<>();
        list = new ArrayList<>();
        rand = new Random();
    }

    public boolean insert(int val) {
        if (dict.containsKey(val)) {
            return false;
        }
        dict.put(val, list.size());
        list.add(val);
        return true;
    }

    public boolean remove(int val) {
        if (!dict.containsKey(val)) {
            return false;
        }
        int lastElement = list.get(list.size() - 1);
        int indexToRemove = dict.get(val);
        list.set(indexToRemove, lastElement);
        dict.put(lastElement, indexToRemove);
        list.remove(list.size() - 1);
        dict.remove(val);
        return true;
    }

    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}
```

### Explanation

1. **Insert Operation**:
   - In Python, the `insert` method checks if `val` is already in the dictionary (`self.dict`). If not, it adds `val` to the end of `self.list` and updates `self.dict` with the index of `val`.
   - In Java, the `insert` method uses `dict.containsKey(val)` to check for existence and `list.size()` to get the index.

2. **Remove Operation**:
   - In Python, the `remove` method checks if `val` is in `self.dict`. If so, it swaps the element with the last element in `self.list`, updates the dictionary for the swapped element, and removes `val` from both the list and dictionary.
   - In Java, the `remove` method performs similar steps using `list.get(list.size() - 1)` for the last element and `list.set(indexToRemove, lastElement)` to perform the swap.

3. **GetRandom Operation**:
   - In Python, the `getRandom` method uses `random.choice(self.list)` to return a random element.
   - In Java, the `getRandom` method uses `rand.nextInt(list.size())` to get a random index and returns the element at that index from `list`.

This approach ensures that all operations (`insert`, `remove`, `getRandom`) run in O(1) average time, making the data structure efficient for dynamic set operations.