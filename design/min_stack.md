#  Min Stack

#### Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

#### Example

```
MinStack minStack = MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2
```

#### How to Solve

#### Solution
- Python

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.mins = []

    def push(self, x):
        """
        :type x: int
        :rtype: void
        """
        self.stack.append(x)
        if len(self.mins) == 0 or self.mins[-1] >= x:
            self.mins.append(x)

    def pop(self):
        """
        :rtype: void
        """
        tmp = self.stack.pop()
        if self.mins[-1] == tmp:
            self.mins.pop()
        return tmp

    def top(self):
        """
        :rtype: int
        """
        return self.stack[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return self.mins[-1]
```

- Ruby

```ruby
class MinStack

=begin
    initialize your data structure here.
=end
  def initialize()
    @stack = []
    @min_stack = []
  end

=begin
    :type x: Integer
    :rtype: Void
=end
  def push(x)
    @stack.append(x)
    if @min_stack.empty? || @min_stack[-1] >= x
      @min_stack.append(x)
    end
  end

=begin
    :rtype: Void
=end
  def pop()
    v = @stack.pop
    if @min_stack[-1] == v
      @min_stack.pop
    end
    v
  end

=begin
    :rtype: Integer
=end
  def top()
    @stack[-1]
  end

=begin
    :rtype: Integer
=end
  def get_min()
    @min_stack[-1]
  end
end
```

#### Complexity
- Time: O(1) --- for all operations
- Space: O(n)