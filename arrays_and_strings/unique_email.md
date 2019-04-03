# Unique Email Addresses

#### Description

Given a list of emails, find how many unique email addresses are there.

Definition
- Every email consists of a local name and a domain name, separated by the @ sign.
- The local name may contain '.'s or '+'s besides lowercase letters.
- The local names are the same with and without '.'; for example, "alice.z" and "alicez" are the same.
- Every character after '+' will be ignored; for example, "m.y+name" and "my" are the same.

#### Example
Input:

```
["test.email+alex@leetcode.com",
"test.e.mail+bob.cathy@leetcode.com",
"testemail+david@lee.tcode.com"]
```

Output: `2`

Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" are unique emails.

#### How to Solve

Separate local and domain name by '@', then separate local name by '+'. Since multiple '+' signs may be contained in the local name, take the first one as local name. Finally, replace '.' by ''. Adding modified local name with @domain to set, the number of uniq emails will be found.  

#### Solution
- Python

```python
class UniqueEmail:
    def numUniqueEmails(self, emails: 'List[str]') -> int:
        seen = set()
        for email in emails:
            local, domain = email.split("@")
            name = local.split('+')[0]
            name = name.replace('.', '')
            seen.add('@'.join([name, domain]))
        return len(seen)
```

- Ruby

```ruby
require 'set'

# @param {String[]} emails
# @return {Integer}
def num_nique_emails(emails)
  seen = Set.new
  emails.each do |email|
    local, domain = email.split('@')
    local = local.split("+")[0]
    local = local.tr(".","")
    seen.add("#{local}@#{domain}")
  end
  seen.size
end
```

#### Complexity
- Time: O(n)
- Space: O(n)