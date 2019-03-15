# Read N Characters Given Read4

#### Description

Given a file and API, `read4`, implement a method, `read`, to read n characters.

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
File file("abc"), n = 4
Solution sol
sol.read(buf, n) # returns 3, buf contains "abc"
```

#### Example 2

```
File file("abcde"), n = 5
Solution sol
sol.read(buf, n) # returns 5, buf contains "abcde"
```

#### Example 3

```
File file("abcdABCD1234"), n = 12
Solution sol
sol.read(buf, n) # returns 12, buf contains "abcdABCD1234"
```

#### Example 4

```
File file("leetcode"), n = 5
Solution sol
sol.read(buf, n) # returns 5, buf contains "leetc"
```

#### How to Solve

Create a temporary buffer to use `read4` API.
Use 2 pointers, start and end to copy read characters to set given buffer. The API gives the feature to read 4 characters in a single call. So, it needs n // 4 plus one (if n % 4 is greater than 0) times to read n characters.

#### Solution
- Python

```python
# The read4 API
# @param buf, a list of characters
# @return an integer
# def read4(buf):

class OnceByRead4:
    def read(self, buf, n):
        """
        :type buf: Destination buffer (List[str])
        :type n: Number of characters to read (int)
        :rtype: The number of actual characters read (int)
        """
        start, end, tmp = 0, 0, [''] * 4
        q, m = divmod(n, 4)
        for _ in range(q):
            count = read4(tmp)
            end += count
            buf[start:end] = tmp[:count]
            start = end
        if m > 0:
            count = read4(tmp)
            count = min(count, m)
            end += count
            buf[start:end] = tmp[:count]
        return end
```

#### Complexity
- Time: O(n)
- Space: O(1)