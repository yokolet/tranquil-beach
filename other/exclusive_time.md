# Exclusive Time of Functions

#### Description

Given the running logs of n functions that are executed in a nonpreemptive single threaded CPU, find the exclusive time of these functions. The output should be sorted by function id.

- Definition

    Exclusive time of a function is defined as the time spent within this function. The time spent by calling other functions should not be considered as this function's exclusive time.

    Each function has a unique id, start from 0 to n-1. A function may be called recursively or by another function.

    Each log is a string in the format, `function_id:start_or_end:timestamp`. For example, `"0:start:0"` means function 0 starts from the very beginning of time 0. `"0:end:0"` means function 0 ends to the very end of time 0.

Input logs will be sorted by timestamp, NOT log id.
`1 <= n <= 100`

#### Example
Input:

```
n = 2
logs = 
["0:start:0",
 "1:start:2",
 "1:end:5",
 "0:end:6"]
 ```

Output:`[3, 4]`

Explanation: 

```
       +- 0 -+- 1 -+- 2 -+- 3 -+- 4 -+- 5 -+- 6 -+
fn 0 : |===========------------------------=====>|  3 units
fn 1 :             |======================>|        4 units
```

#### How to Solve

Use a stack to save a previous function id. When another function comes in, add up units so far to the previous function id in the result array. Push the current function id to the stack and update the unit. When the event is the "end.", the function id itself should be on the top of the stack. Add up units so far to the result array for the last function id, then pop the function id. The unit calculations on start or end are slightly different. In any case, each function gets at least 1 unit. In light of this, the unit on the end event gets 1 more.

A tricky part of this problem is: no function may be on the running state. In such a case, `stack[-1]` fails. To pevent this, the solution adds the first function id in the stack and start the iteration from the first one.

#### Solution
- Python

```python
class ExclusiveTime:
    def exclusiveTime(self, n: int, logs: 'List[str]') -> 'List[int]':
        result = [0 for _ in range(n)]
        f_id, event, t = logs[0].split(":")
        prev_t = int(t)
        stack = [int(f_id)]
        for log in logs:
            f_id, event, t = log.split(":")
            cur_t = int(t)
            if event == "start":
                result[stack[-1]] += cur_t - prev_t
                stack.append(int(f_id))
                prev_t = cur_t
            else:
                result[stack[-1]] += cur_t - prev_t + 1
                stack.pop()
                prev_t = cur_t + 1
        return result
```

- Ruby

```ruby
# @param {Integer} n
# @param {String[]} logs
# @return {Integer[]}
def exclusive_time(n, logs)
  result = Array.new(n, 0)
  f, event, t = logs[0].split(":")
  stack = [f.to_i]
  units = t.to_i
  logs.each do |log|
    f, event, t = log.split(":")
    t_ = t.to_i
    if event == "start"
      result[stack[-1]] += (t_ - units)
      stack.push(f.to_i)
      units = t_
    else
      result[stack[-1]] += (t_ - units + 1)
      stack.pop
      units = t_ + 1
    end
  end
  result
end
```

#### Complexity
- Time: `O(n)`
- Space: `O(n)`