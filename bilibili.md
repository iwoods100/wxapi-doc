# Bilibili接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### web版接口合集

```
http://whosecard.com:8081/api/bilibili/web?key=***&api=***&其它参数=***

本接口根据不同的api参数，调用不同的数据接口，统一返回格式如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}

以下是各数据接口定义：

获取用户基础信息：
api=user_base
mid=用户id，如 507537547

获取用户标签：
api=user_tags
mid=用户id，如 507537547

获取用户粉丝数，关注数：
api=user_stat
mid=用户id，如 507537547

获取用户总播放数、阅读数、点赞数
api=user_upstat
mid=用户id，如 507537547

获取用户充电数据
api=user_charging
mid=用户id，如 507537547

获取用户发布作品分类统计
api=user_navnum
mid=用户id，如 507537547

获取用户关注列表：
api=user_followings
mid=用户id，如 507537547
page：翻页数，默认为1

获取用户粉丝列表：
api=user_followers
mid=用户id，如 507537547
page：翻页数，默认为1


获取视频列表：
api=user_submit_videos
mid=用户id，如 507537547
page：翻页数，默认为1

获取单条视频的统计数据：
api=single_stat
aid=单条视频id，如 91256107

获取单条视频的tag列表：
api=detail_tag
aid=单条视频id，如 91256107

获取视频下的评论：
api=comments
aid=单条视频id，如 91256107

获取动态历史列表：
api=user_space_history
mid=用户id，如 2505015
offset_dynamic_id： 上一页请求的最后一条动态id，用来翻页，初始为0
```
