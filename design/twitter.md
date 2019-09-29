# Design Twitter

#### Description

Design a simplified version of Twitter which supports methods below:

- `postTweet(userId, tweetId)`

    Compose a new tweet.

- `getNewsFeed(userId)`

    Retrieve 10 most recent tweet ids in the user's news feed.
    Each item in the news feed should be own tweet and following user's tweet. The tweets should be ordered from the most to least recent.

- `follow(followerId, followeeId)`

    Follower follows a followee.

- `unfollow(followerId, followeeId)`

    Follower unfollows a followee.

#### Example

```python
twitter = Twitter()

# User 1 posts a new tweet (id = 5).
twitter.postTweet(1, 5)

# User 1's news feed should return a list with 1 tweet id -> [5].
twitter.getNewsFeed(1)

# User 1 follows user 2.
twitter.follow(1, 2)

# User 2 posts a new tweet (id = 6).
twitter.postTweet(2, 6)

# User 1's news feed should return a list with 2 tweet ids -> [6, 5].
# Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.getNewsFeed(1)

# User 1 unfollows user 2.
twitter.unfollow(1, 2)

# User 1's news feed should return a list with 1 tweet id -> [5],
# since user 1 is no longer following user 2.
twitter.getNewsFeed(1)
```

#### How to Solve

The most complicated method is the `getNewsFeed`. Alongside with own tweets, it needs to get following users tweets as well. However, following or not is dynamic. It happens that a userA starts following a userB but unfollows later. In such a case, the userB's tweets appear on the userA's newsfeed while following only.

Considering that, the solution keeps a following list for each user. Also, it saves tweets of the user in the table where key is a user id and value is a list of tweets. When the newsfeed is requested, the requested user id's tweets and following users' tweets are combined and sorted. So that sorting can be done in the newest to older, each post is saved with the timestamp.

How to maintain the timestamp is worth considering. One is to save the timestamp as a instance variable and count up when the `postTweet` method gets called. The problem is a concurrency. Without properly locking/unlocking the variable, the timestamp count up is easily messed up. To avoid such situation, this solution simply calls `time.time()` method to get a time in millisecond. However, this is still not free from a trouble. It depends on the ability of the system running on. Sometime, exactly the same timestamp is given to multiple tweets. In an actual situation, this doesn't bother users, so the solution here chose this style.

#### Solution

- Python

```python
from collections import defaultdict
import time

class Twitter:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.users = defaultdict(set) # userId -> followeeIds
        self.posts = defaultdict(list) # userId -> posts, posts = (timestamp, postId)

    def postTweet(self, userId: int, tweetId: int) -> None:
        """
        Compose a new tweet.
        """
        ts = time.time()
        self.posts[userId].append((ts, tweetId))

    def getNewsFeed(self, userId: int) -> 'List[int]':
        """
        Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent.
        """
        news = [v for v in self.posts[userId]]
        for id in self.users[userId]:
            news += self.posts[id]
        return [id for _, id in sorted(news, reverse=True)[:10]]

    def follow(self, followerId: int, followeeId: int) -> None:
        """
        Follower follows a followee. If the operation is invalid, it should be a no-op.
        """
        if followerId == followeeId: return
        self.users[followerId].add(followeeId)

    def unfollow(self, followerId: int, followeeId: int) -> None:
        """
        Follower unfollows a followee. If the operation is invalid, it should be a no-op.
        """
        self.users[followerId].discard(followeeId)
```

#### Complexity
- Time: `postTweet`, `follow`, `unfollow`: `O(1)`, `getNewsFeed`: `O(nlog(n))` -- n is a number of tweets
- Space: `O(m)` -- m is a number of users
