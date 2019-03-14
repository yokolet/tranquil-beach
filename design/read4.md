# Read N Characters Given Read4 API - Call multiple times

#### Description

Given a file and API, `read4`, implement a method, `read`, to read n characters. The `read` method to be implemented may be called multiple times.

- API definition

    reads 4 consecutive characters from the file, then writes those characters into the given buffer.

    ```
    Parameter: char[] buf
    Returns: int
    ```

- API Example

    ```
    File file("abcdefghijk") # File is "abcdefghijk", initially file pointer (fp) points to 'a'
    char[] buf = new char[4] # buffer for destination
    read4(buf) # returns 4, buf = "abcd", fp points to 'e'
    read4(buf) # returns 4, buf = "efgh", fp points to 'i'
    read4(buf) # returns 3, buf = "ijk", fp points to end of file
    ```

- Method definition

    Use `read4` API. Read n characters from the file and store it in the given buffer and return a number of charactes read.

    ```
    Parameters: char[] buf, int n
    Returns: int
    ```

#### Example 1

```
File file("abc")
Solution sol
sol.read(buf, 1) # returns 1, buf[0] = 'a'
sol.read(buf, 2) # returns 2, buf[0] = 'b', buf[1] = 'c'
sol.read(buf, 1) # return 0
```

#### Example 2

```
File file("abc")
Solution sol
sol.read(buf, 4) # returns 3, buf[0] = 'a', buf[2] = 'b', buf[1] = 'c'
sol.read(buf, 1) # return 0
```

#### How to Solve

Create an internal buffer and save the characters read by `read4` API. There may be shortage or excess of characters from `read4`.
In case of shortage, repeat reads. In case of excess, append the characters in the internal buffer. Copy necessary number of characters to the given buffer. At the same time, delete the same number of characters from internal buffer from head.

#### Solution
- Python

```python
# API definition
# @param buf, a list of characters
# @return an integer
# def read4(buf):

class Read4:
    def __init__(self):
        self.queue = []

    def read(self, buf, n):
        """
        :type buf: Destination buffer (List[str])
        :type n: Number of characters to read (int)
        :rtype: The number of actual characters read (int)
        """
        if n == 0: return 0
        while len(self.queue) < n:
            tmp = [''] * 4
            count = read4(tmp)
            self.queue += tmp[:count]
            if count < 4:
                break
        length = min(n, len(self.queue))
        buf[:length] = self.queue[:length]
        del self.queue[:length]
        return length
```

#### Complexity
- Time: O(n)
- Space: O(n)