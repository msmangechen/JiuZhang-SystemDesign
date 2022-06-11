# Chapter 23 Comment system

Q: 刚才API那里get all comments符合restful要求吗？我觉得comments写成\~/api/comments/吗

A: 带上id表示具体的某条评论



Q: 一不小心发出去了没发完，刚才API那里get all comments符合restful要求吗？我觉得comments应该写成\~/api/comments/，然后comment是\~/api/comment/

A: 单数还是复数可以看这个https://www.jianshu.com/p/68168eccadf2



Q: 所以fetch某条具体的评论应该是\~/api//comments/吗？感觉这里放ctxid有点多余

A: /api/tweets/1/comments/?page\_size=10\&page=1

表示 id 为 1 的 tweet 下的第一页评论

/api/tweets/1/comments/1

表示 id 为 1 的 tweet 下的 id 为1 的评论

也可以

/api/comments/?page\_size=10\&page=1\&model=tweets\&model\_id=1

表示 id 为 1 的 tweet 下的第一页评论

/api/comments/1?model=tweets\&model\_id=1

表示 id 为 1 的 tweet 下的 id 为1 的评论

