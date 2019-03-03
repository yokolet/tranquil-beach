# Implement Sqrt(x)

#### Description

Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Truncate decimal digits and return the integer part only.

#### Example 1
Input: `4`

Output: `2`

#### Example 2
Input: `8`

Output:`2`

Explanation: The square root of 8 is 2.82842..., which will be 2 when decimal digits are truncated.

#### How to Solve

The solution here uses [Newton-Rapson method](https://en.wikipedia.org/wiki/Newton%27s_method) (NR method).

The NR method is applicable when the fucntion is differentiable (continuous). It starts from the initial guess, x0. The x-intercept (y = 0) of the tangent line at x0 is considered a better approximation of root. Let the x-intercept be x1. The x-intercept of the tangent linet at x1 is better than x0. Repeat this until x-intercept is close enough to the real root.

The equation is derived as below:

1. The tangent line to the curve `Y = f(X)` at `X = Xi` is:

    ```
    Y = f'(Xi)(X - Xi) + f(Xi)
    ```

2. The x-intercept to approximate next root, `Xi+1`:

    ```
    0 = f'(Xi)(Xi+1 - Xi) + f(Xi)
    Xi+1 = Xi - f(Xi) / f'(Xi)
    ```
3. `f(X)` and `f'(X)` are:

    ```
    X = sqrt(a)
    X^2 = a
    X^2 - a = 0 = f(X)
    f(X) = X^2 - a
    f'(X) = 2X
    ```

4. Plugin 3 to 2

    ```
    Xi+1 = Xi - (Xi^2 - a) / 2Xi
    Xi+1 = (Xi + a / Xi) / 2
    ```

Iterate the last equation until approximation, `Xi+1`, becomes close enough, which means `Xi+1 * Xi+1 <= a`.

#### Solution
- Python

```python
class SqrtApprox:
    def mySqrt(self, x: int) -> int:
        i = x
        while i * i > x:
            i = (i + x / i) / 2
        return int(i)
```

- Ruby

```ruby
# @param {Integer} x
# @return {Integer}
def my_sqrt(x)
  i = x
  while i * i > x
    i = (i + x / i) / 2
  end
  i.to_i
end
```

#### Complexity
- Time: O(log(n))
- Space: O(1)