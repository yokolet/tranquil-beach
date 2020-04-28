# First Unique Number

#### Description

Implement the algorithm which keeps a queue of integers and is able to retrieve the first unique integer in the queue. The class should have the constructor and methods described below:

- Definition
    - Constructor: initializes the object with an array of integers
    - `showFirstUnique` method: returns the value of the first unique integer in the queue. If no such intger exists, returns -1
    - `add` method: insert a value to the queue

#### Example 1

```python
firstUnique = FirstUnique([2,3,5])   # -> queue = [2,3,5]
firstUnique.showFirstUnique()        # -> returns 2
firstUnique.add(5)                   # -> queue = [2,3,5,5]
firstUnique.showFirstUnique()        # -> returns 2
firstUnique.add(2)                   # -> queue = [2,3,5,5,2]
firstUnique.showFirstUnique()        # -> returns 3
firstUnique.add(3)                   # -> queue = [2,3,5,5,2,3]
firstUnique.showFirstUnique()        # -> returns -1
```

#### Example 2

```python
firstUnique = FirstUnique([7,7,7,7,7,7])   # -> queue = [7,7,7,7,7,7]
firstUnique.showFirstUnique()              # -> returns -1
firstUnique.add(7)                         # -> queue = [7,7,7,7,7,7,7]
firstUnique.add(3)                         # -> queue = [7,7,7,7,7,7,7,3]
firstUnique.add(3)                         # -> queue = [7,7,7,7,7,7,7,3,3]
firstUnique.add(7)                         # -> queue = [7,7,7,7,7,7,7,3,3,7]
firstUnique.add(17)                        # -> queue = [7,7,7,7,7,7,7,3,3,7,17]
firstUnique.showFirstUnique()              # -> returns 17
```

#### Example 3

```python
firstUnique = FirstUnique([809])   # -> queue = [809]
firstUnique.showFirstUnique()      # -> returns 809
firstUnique.add(809)               # -> queue = [809,809]
firstUnique.showFirstUnique()      # -> returns -1
```

#### How to Solve

This problem requires a good performance. The naive solution will get the Time Limited Exceeded error.

Python has `OrderedDict` which retains the orders of elements added. This is a good data structure for this problem. Save unique values to the ordered dictionary as a key with counts as the value. At the same time, save all values seen so far. When the duplicated value comes in, the value will be removed from the dictionary. But later, the same value may be added. In such a case, the value doesn't exist in the dictionary but should not be added to the dictionary. For this reason, all values should be saved to know whether it appeared previously or not. 

#### Solution
- Python

```python
from collections import OrderedDict

class FirstUnique:
    def __init__(self, nums: 'List[int]'):
        self.n_dict = OrderedDict()
        self.seen = set()
        for v in nums:
            self.seen.add(v)
            self.n_dict[v] = self.n_dict.get(v, 0) + 1
        for k in list(self.n_dict.keys()):
            if self.n_dict[k] > 1:
                self.n_dict.pop(k)
        print('class creates')

    def showFirstUnique(self) -> int:
        return next(iter(self.n_dict)) if self.n_dict else -1

    def add(self, value: int) -> None:
        if value not in self.seen:
            self.seen.add(value)
            self.n_dict[value] = 1
        elif value in self.n_dict:
            self.n_dict.pop(value)
```

#### Complexity
- Time:
    - Constructor: `O(n)` -- n is a length of the given array
    - `showFirstUnique`: `O(1)`
    - `add`: `O(1)`
- Space: `O(n)`
