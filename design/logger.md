# Logger Rate Limiter

#### Description

Design a logger system that receives stream of messages along with its timestamp (seconds granularity) and returns true if the message should be printed out in the given timestamp.

- Definition

    Each message should be printed out if and only if it is not printed out in the last 10 seconds. It is possible several messages arrive roughly at the same time.

#### Example

```
logger = Logger();

// logging string "foo" at timestamp 1
logger.shouldPrintMessage(1, "foo"); returns True; 

// logging string "bar" at timestamp 2
logger.shouldPrintMessage(2,"bar"); returns True;

// logging string "foo" at timestamp 3
logger.shouldPrintMessage(3,"foo"); returns False;

// logging string "bar" at timestamp 8
logger.shouldPrintMessage(8,"bar"); returns False;

// logging string "foo" at timestamp 10
logger.shouldPrintMessage(10,"foo"); returns False;

// logging string "foo" at timestamp 11
logger.shouldPrintMessage(11,"foo"); returns True;
```

#### How to Solve

Use dictionary to save a message and timestamp pair. When previously seen message comes in, check the dictionary whether the message's timestamp is older than 10 seconds compared to the current timestamp. If older, replace the timestamp and return True. If not older than 10 seconds, return False. If the message is new, save it to the dictionary and return True.

#### Solution

- Python

```python
class Logger:
    
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.log = {}

    def shouldPrintMessage(self, timestamp: int, message: str) -> bool:
        """
        Returns true if the message should be printed in the given timestamp, otherwise returns false.
        If this method returns false, the message will not be printed.
        The timestamp is in seconds granularity.
        """
        if message not in self.log:
            self.log[message] = timestamp
            return True
        elif timestamp - self.log[message] < 10:
            return False
        else:
            self.log[message] = timestamp
            return True
```

#### Complexity
- Time: `O(1)`
- Space: `O(n)` -- n is a number of unique messages
