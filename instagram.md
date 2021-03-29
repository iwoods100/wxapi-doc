# instagram实时采集接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 搜索框关键词搜索
```
http://whosecard.com:8081/api/instagram/search/top?keyword=***&key=***

eg:
http://whosecard.com:8081/api/instagram/search/top?keyword=cat&key=***

返回如下：
{
	"ok": true,
	"result": {***}
}
```

#### 获取指定tag的作品列表
```
http://whosecard.com:8081/api/instagram/search/tag?tag=***&cursor=***&key=***

eg:
http://whosecard.com:8081/api/instagram/search/tag?tag=cat&key=***

tag是要搜索的tag名称
如果要翻页，请传入cursor参数，第一页不需要传，之后每一页的cursor会在前一页的返回结果里返回

返回如下：
{
	"ok": true,
	"result": {***}
}

返回字段解释：
  edge_hashtag_to_media字段里是按时间排序的作品列表，可以翻页
  edge_hashtag_to_top_posts字段里是最热门的作品列表，为固定值，不能翻页
```

#### 指定用户的作品列表
```
http://whosecard.com:8081/api/instagram/user/posts?username=***&cursor=***&key=***

eg:
http://whosecard.com:8081/api/instagram/user/posts?username=_iamxnami_&key=***

username是用户的昵称
如果要翻页，请传入cursor参数，第一页不需要传，之后每一页的cursor会在前一页的返回结果里返回

返回如下：
{
	"ok": true,
	"result": {***}
}

请求第一页的时候，会将用户的基础信息一同返回（如关注数、粉丝数、简介等），之后的翻页不会再额外返回用户基础信息。

返回字段解释：
  edge_owner_to_timeline_media字段里是作品列表，可以翻页
```

#### 单个作品详情
```
http://whosecard.com:8081/api/instagram/post/detail?shortcode=***&key=***

eg:
http://whosecard.com:8081/api/instagram/post/detail?shortcode=CLzGrEJnZvO&key=***

shortcode是作品id，可从【指定用户的作品列表】接口中获取。

返回如下：
{
	"ok": true,
	"result": {***}
}
```
