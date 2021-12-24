# 知乎爬虫系统

### 功能

- [x] 采集问题信息
- [ ] 采集用户信息
- [ ] 采集话题信息
- [ ] 采集回答信息

### 页面分析

- 在不登录的情况下可以访问用户的主页、问题的主页、话题的主页、某个用户对某个问题的答案详情、发现页面、热点问题页面、潜力问题页面；
- 用户ID、问题ID、话题ID不是连续的，因此无法通过预判ID的方式访问这些页面；
- 借助问题的ID调用知乎API可以获取作答用户的ID、相关问题的ID；
- 在问题的主页可以获取话题主页的链接地址；
- 借助用户的ID访问API可以获取全部用户信息；
- 通过用户关注页面可以获取大量用户信息，但用户粉丝页面的信息无法直接获取；
- 借助问题的ID和用户的ID可以获取某个用户对某个问题的答案详情；
- 热点问题页面、潜力问题页面的数据是动态渲染出来的，无法直接获取。

### 设计思路

通过访问发现页面可以获取21个问题的ID，其中包括4个热点问题的ID、4个潜力问题的ID、12个圆桌讨论问题的ID、1个知乎指南的ID。

通过某个问题ID可以获取5个相关问题的ID，因此从理论上讲，通过不断访问问题主页可以获取知乎上全部问题的ID，实际上相关问题的相关问题重合度非常高，无法做到每次获得的ID都是不重复的。