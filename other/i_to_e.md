# Integer to English Words

#### Description

Given a non-negative integer, convert it to english words representation. The input is less than 2^31 - 1.

#### Example 1
Input: `123`

Output: `"One Hundred Twenty Three"`

#### Example 2
Input: `12345`

Output: `"Twelve Thousand Three Hundred Forty Five"`

#### Example 3
Input: `1234567`

Output: `"One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"`

#### Example 4
Input: `1234567891`

Output: `"One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"`

#### How to Solve

The recursive call is used to solve this problem. After handling a chunk of digitis, which are 3 in higher orders, a decreased number is passed to the next process. The tricky part is handling zero especially it appears in the middle since it should not add an extra space in the result.

#### Solution
- Python

```python
class IntegerToEnglish:
    def numberToWords(self, num):
        """
        :type num: int
        :rtype: str
        """
        under19 = [
            'One', 'Two', 'Three', 'Four',
            'Five', 'Six', 'Seven', 'Eight', 'Nine', 
            'Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen',
            'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen'
            ]
        tens = [
            'Twenty', 'Thirty', 'Forty',
            'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety'
            ]
        orders = [
             'Thousand', 'Million', 'Billion'
            ]
        def toEnglish(num):
            if num < 20: return under19[num-1:num]
            if num < 100: return [tens[num // 10 - 2]] + toEnglish(num % 10)
            if num < 1000: return [under19[num // 100 - 1]] + ['Hundred'] + toEnglish(num % 100)
            for i, order in enumerate(orders, 1):
                if num < 1000**(i+1): return toEnglish(num // 1000**i) + [order] + toEnglish(num % 1000**i)
        
        return ' '.join(toEnglish(num)) or 'Zero'
```

- Ruby

```ruby
# @param {Integer} num
# @return {String}
def number_to_words(num)
  result = to_english(num).join(' ')
  result.empty? ? 'Zero' : result
end
UNDER19 = [
    'One', 'Two', 'Three', 'Four',
    'Five', 'Six', 'Seven', 'Eight', 'Nine',
    'Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen',
    'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen'
]
TENS = [
    'Twenty', 'Thirty', 'Forty',
    'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety'
]
ORDERS = [
    'Thousand', 'Million', 'Billion'
]
def to_english(num)
  case
  when num == 0
    return []
  when num < 20
    return [UNDER19[num - 1]]
  when num < 100
    return [TENS[num / 10 - 2]] + to_english(num % 10)
  when num < 1000
    return [UNDER19[num / 100 - 1]] + ['Hundred'] + to_english(num % 100)
  else
    ORDERS.each.with_index(1) do |order, i|
      if num < 1000**(i+1)
        return to_english(num / 1000**i) + [order] +  to_english(num % 1000
      end
    end
  end
end
```

#### Complexity
- Time: `O(1)`
- Space: `O(1)`