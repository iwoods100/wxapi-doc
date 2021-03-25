# youtube实时采集接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 采集指定用户/channel下的视频列表
```
http://whosecard.com:8081/api/youtube/channel/videos?channel=***&key=***

eg:
http://whosecard.com:8081/api/youtube/channel/videos?channel=UCGfr1FclscwCp7aVJw3C1Zw&key=***

返回如下：
{
	"ok": true,
	"result": {***}
}
```
