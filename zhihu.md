# 知乎接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### web版接口合集

```
http://whosecard.com:8081/api/zhihu/web?key=***&api=***&其它参数=***

本接口根据不同的api参数，调用不同的数据接口，统一返回格式如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}

以下是各数据接口定义：

个人主页：
api=user_info
urlToken=用户token，如 zhouyuan

提问页：
api=question
questionId: 提问页id
offset：用于翻页，下一页的offset参数使用上一页翻回结果的paging.next值
sortBy: 回答排序，可取值default/updated，默认去default

评论列表
api=root_comments
itemType=作品类型，支持两种:article与answer
itemId=作品ID
```

<!--
搜索页：
api=search
q=搜索关键词
offset：用于翻页，下一页的offset参数使用上一页翻回结果的paging.next值
-->
