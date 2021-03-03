# twitter实时采集接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 用户基础信息
```
http://whosecard.com:8081/api/twitter/user/profile?screen_name=***&key=***

eg:
http://whosecard.com:8081/api/twitter/user/profile?screen_name=amrezy&key=***

screen_name是twitter用户的昵称

返回如下：
{
	"ok": true,
	"result": {***}
 }
```

#### 用户作品列表
```
http://whosecard.com:8081/api/twitter/user/feeds?user_id=***&key=***

eg:
http://whosecard.com:8081/api/twitter/user/feeds?user_id=6622192&key=***

user_id是twitter用户的数字id，可通过【用户基础信息】获取
如果要翻页，请传入cursor参数，cursor参数会在前一页的返回结果里返回，请求第一页时不用传cursor

返回如下：（作品列表在tweets字段里）
{
	"ok": true,
	"result": {***}
 }
```

#### 实时搜索
```
http://whosecard.com:8081/api/twitter/search?keyword=***&cursor=***&search_type=***&key=***

eg:
http://whosecard.com:8081/api/twitter/search?keyword=cat&search_type=image&key=***

keyword要搜索的关键词
search_type为搜索类型，支持以下值：top(热门),live(最新),user(搜用户),image(搜图片),video(搜视频), 默认不传时取值top
如果要翻页，请传入cursor参数，cursor参数会在前一页的返回结果里返回，请求第一页时不用传cursor

返回如下：
{
	"ok": true,
	"result": {***}
 }
```
