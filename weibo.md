# 微博-实时接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 获取用户详情
```
http://whosecard.com:8081/api/weibo/user/profile/v1?key=***&user_id=1642566747

参数解释：
user_id为用户id

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取用户作品列表
```
http://whosecard.com:8081/api/weibo/user/feeds/v1?key=***&user_id=1642566747&since_id=

参数解释：
user_id为用户id
since_id为翻页参数，第一页不用传，下一页的since_id将在本次请求的since_id字段返回

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```


#### 搜索关键词
```
http://whosecard.com:8081/api/weibo/search/v1?key={{key}}&keyword=今天&page=1&search_type=0

参数解释：
keyword为搜索关键词
page为翻页参数，起始值为1，每次翻页加1
search_type为搜索类型，不传则默认为0（综合搜索）
user_id为限制在指定用户的作品里进行搜索，可不传

search_type支持以下类型:
  0: 综合
  1: 用户
  2: 实时
  3: 视频
  4: 图片
  5: 文章
  6: 问答
  7: 热门
  8: 话题

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```
