# Insert, Remove, getRandom by O(1)

#### Description

Design a data structure which provides `insert`, `remove`, and `getRandom` methods. All three methods should run in O(1) runtime complexity.

Methods specifications:

- `insert`: Inserts a value to the data structure only if the value doesn't present.
- `remove`: Removes a value from the data structure only if the value presents.
- `getRandom`: Returns a value randomly from the current values present in the data structure. All values should have the same probability to be picked up.

#### Example

```
# initializes
randomSet = RandomizedSet()

# inserts 1, which returns True
randomSet.insert(1)

# removes 2, which returns False
randomSet.remove(2)

# inserts 2, which returns True
randomSet.insert(2)

# gets a value randomly, which returns either 1 or 2
randomSet.getRandom()

# removes 1, which returns True
randomSet.remove(1)

# inserts 2, which returns False
randomSet.insert(2)

# gets a value randomly, which should return 2
randomSet.getRandom()
```

#### How to Solve

The requirement of O(1) is tricky. The method, `getRandom`, to run in O(1), values should be saved in the list. The reason is that a random choice needs index access.
The `remove` method to run in O(1), it needs a dictionary. 

Given that, the data structure will have the list and dictionary to manage values. These two should treat values consistently, especially, when a value is removed.
The solution here uses the dictionary to save a value-index pair. When the value is removed, the specified value in the list is replaced by the last value. At the same time, the index in the dictionary is updated.

#### Solution

- Python

```python
import random

class RandomizedSet:
    
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.vals, self.valToIdx = [], {}

    def insert(self, val: int) -> bool:
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        """
        if val in self.valToIdx:
            return False
        else:
            self.vals.append(val)
            self.valToIdx[val] = len(self.vals) - 1
            return True

    def remove(self, val: int) -> bool:
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        """
        if val not in self.valToIdx:
            return False
        else:
            idx, lastVal = self.valToIdx[val], self.vals.pop()
            del self.valToIdx[val]
            if val == lastVal: return True
            self.vals[idx] = lastVal
            self.valToIdx[lastVal] = idx
            return True

    def getRandom(self) -> int:
        """
        Get a random element from the set.
        """
        return random.choice(self.vals)
```

#### Complexity

- Time: O(1)
- Space: O(n) -- n is the length of values saved in the data structure