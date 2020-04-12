---
title: 355.设计推特 (Design Twitter)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [355\. 设计推特](https://leetcode-cn.com/problems/design-twitter/)

Difficulty: **中等**


设计一个简化版的推特(Twitter)，可以让用户实现发送推文，关注/取消关注其他用户，能够看见关注人（包括自己）的最近十条推文。你的设计需要支持以下的几个功能：

1.  **postTweet(userId, tweetId)**: 创建一条新的推文
2.  **getNewsFeed(userId)**: 检索最近的十条推文。每个推文都必须是由此用户关注的人或者是用户自己发出的。推文必须按照时间顺序由最近的开始排序。
3.  **follow(followerId, followeeId)**: 关注一个用户
4.  **unfollow(followerId, followeeId)**: 取消关注一个用户

**示例:**

```
Twitter twitter = new Twitter();

// 用户1发送了一条新推文 (用户id = 1, 推文id = 5).
twitter.postTweet(1, 5);

// 用户1的获取推文应当返回一个列表，其中包含一个id为5的推文.
twitter.getNewsFeed(1);

// 用户1关注了用户2.
twitter.follow(1, 2);

// 用户2发送了一个新推文 (推文id = 6).
twitter.postTweet(2, 6);

// 用户1的获取推文应当返回一个列表，其中包含两个推文，id分别为 -> [6, 5].
// 推文id6应当在推文id5之前，因为它是在5之后发送的.
twitter.getNewsFeed(1);

// 用户1取消关注了用户2.
twitter.unfollow(1, 2);

// 用户1的获取推文应当返回一个列表，其中包含一个id为5的推文.
// 因为用户1已经不再关注用户2.
twitter.getNewsFeed(1);
```


#### Solution

Language: **Java**

```java
​class Twitter {
    class Tweet{
        int id;
        int time=0;
        Tweet next;
        public Tweet(int id, int time){
            this.id=id;
            this.time=time;
            next=null;
        }
    }
    /** Initialize your data structure here. */
    HashMap<Integer, Tweet> map;
    HashMap<Integer, HashSet<Integer>> followees;
    int timeStamp;
    public Twitter() {
        map=new HashMap<Integer, Tweet>();
        followees=new HashMap<Integer, HashSet<Integer>>();
        timeStamp=0;
    }

    /** Compose a new tweet. */
    public void postTweet(int userId, int tweetId) {
        Tweet temp=new Tweet(tweetId, timeStamp++);
        Tweet head=map.get(userId);
        temp.next=head;
        head=temp;
        map.put(userId, head);
    }

    /** Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent. */
    public List<Integer> getNewsFeed(int userId) {
        List<Integer> res=new ArrayList<Integer>();
        List<Tweet> tweets=new ArrayList<Tweet>();
        if(map.containsKey(userId)) tweets.add(map.get(userId));
        HashSet<Integer> followeeIds=followees.get(userId);
        if(followeeIds!=null){
            for(Integer followeeId: followeeIds){
                if(map.containsKey(followeeId))
                    tweets.add(map.get(followeeId));
            }
        }
        for(int i=0; i<10; i++){
            int max_index=-1;
            int max=Integer.MIN_VALUE;
            for(int j=0; j<tweets.size(); j++){
                Tweet temp=tweets.get(j);
                if(temp==null) continue;
                if(temp.time>max){
                    max=temp.time;
                    max_index=j;
                }
            }
            if(max_index>=0){
                res.add(tweets.get(max_index).id);
                tweets.set(max_index, tweets.get(max_index).next);
            }
        }
        return res;
    }

    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    public void follow(int followerId, int followeeId) {
        if(followerId==followeeId) return;
        HashSet<Integer> followeeIds=followees.get(followerId);
        if(followeeIds==null){
            followeeIds=new HashSet<Integer>();
            followees.put(followerId, followeeIds);
        }
        followeeIds.add(followeeId);
    }

    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    public void unfollow(int followerId, int followeeId) {
        HashSet<Integer> followeeIds=followees.get(followerId);
        if(followeeIds==null) return;
        followeeIds.remove(followeeId);
    }
}

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * List<Integer> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/design-twitter/submissions/)***
