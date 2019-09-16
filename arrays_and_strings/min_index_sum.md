# Minimum Index Sum of Two Lists

#### Description

Given two lists of strings, find common strings whose index sum is minimum. If multiple strings have the same minimum index sum, return all of them with no order requirement.

The length of both lists will be in the range of [1, 1000].
The length of strings in both lists will be in the range of [1, 30].
No duplicates in both lists.

#### Example 1
Input:

```
list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]
list2 = ["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
```

Output: `["Shogun"]`

#### Example 2
Input:

```
list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]
list2 = ["KFC", "Shogun", "Burger King"]
```

Output: `["Shogun"]`

Explanation: "KFC" -> 3 + 0, "Shogun" -> 0 + 1, "Burger King" -> 2 + 1

#### How to Solve

Create a string to index mapping for the first list.
While going over the second list with index, check:

- if index is bigger than the index sum, it won't be the answer.
- if string is in the mapping, check the index sum.
- when the current index sum is the same, add string to the list.
- when the current index sum is less, replace index sum and list.

#### Solution
- Python

```python
class MinIndexSum:
    def findRestaurant(self, list1: 'List[str]', list2: 'List[str]') -> 'List[str]':
        rank1 = {v: i for i, v in enumerate(list1)}
        common = []
        index_sum = float('inf')
        for i, v in enumerate(list2):
            if i > index_sum: break
            if v in rank1:
                cur = i + rank1[v]
                if index_sum == cur:
                    common.append(v)
                elif index_sum > cur:
                    index_sum = cur
                    common = [v]
        return common
```

- Ruby

```ruby
# @param {String[]} list1
# @param {String[]} list2
# @return {String[]}
def find_restaurant(list1, list2)
  rank = {}
  list1.each_with_index { |v, i| rank[v] = i }
  index_sum = 2000
  common = []
  list2.each_with_index do |v, i|
    break if i > index_sum
    if rank.has_key?(v)
      cur = i + rank[v]
      if index_sum == cur
        common << v
      elsif index_sum > cur
        index_sum = cur
        common = [v]
      end
    end
  end
  common
end
```

#### Complexity
- Time: `O(n)` -- n is a length of first list
- Space: `O(n)`
