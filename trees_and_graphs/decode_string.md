# Decode String

#### Description

Given an encoded string, return its decoded string. The encoding rule is below:

- Encoding Rule
    - basic pattern is `k[encoded_string]` where `k` is a positive integer and `encoded_string` consists of alphabetical letters
    - the `encoded_string` repeats exactly `k` times
    - the given string is always valid: no white space, square brackets are well-formed

#### Example 1

Input: `"3[a]2[bc]"`

Output: `"aaabcbc"`

#### Example 2

Input: `"3[a2[c]]"`

Output: `"accaccacc"`

#### Example 3

Input: `"2[abc]3[cd]ef"`

Output: `"abcabccdcdcdef"`

#### How to Solve

Since the encoded string pattern may be nested, using a stack or recursion would be good approaches. The solution here used the stack.
While going over the given string, if the character is not a closing bracket, stack up the character. If the character is the closing bracket, process the characters in the stack.
The characters are saved in a reverse order, so add the character on the head while popping from the stack unless it sees the opening bracket. Before the opening bracket, the digits are saved. The digits are saved in a reverse order, so added the digit on the head while popping digits from the stack. When no more digit is on the top of the stack, create a substring so far and save to the stack.
When all characters are processed or saved, the stack has the processed substrings including additional characters on the tail. Joining those will give the answer.

#### Solution
- Python

```python
class DecodeString:
    def decodeString(self, s: str) -> str:
        stack = []
        for c in s:
            if c != ']':
                stack.append(c)
            else:
                sub = ''
                while stack and stack[-1] != '[':
                    sub = stack.pop() + sub
                stack.pop()
                d = ''
                while stack and stack[-1].isdigit():
                    d = stack.pop() + d
                stack.append(sub * int(d))
        return ''.join(stack)
```

#### Complexity
- Time: `O(n)` -- n is a length of the given string
- Space: `O(n)`
