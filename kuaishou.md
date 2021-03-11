# 快手接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 根据用户分享链接获取用户id信息
```
http://whosecard.com:8081/api/kuaishou/userIdInfo?shareUrl=***&key=***

参数shareUrl为快手app个人页的分享链接，需要urlencode，比如：
https://f.kuaishou.com/snK21
编码后为
https%3a%2f%2ff.kuaishou.com%2fsnK21

返回如下：
{
  "ok": true,
  "result": {
    "userEid": "YYQXsgxka",
    "userId": 1858201250
  }
}
```

#### 根据用户任意作品分享链接里的photoId获取用户id信息
```
http://whosecard.com:8081/api/kuaishou/userIdInfoFromPhoto?photoId=***&key=***

参数photoId为快手个人页的任意作品id，即分享链接的最后一部分，比如：
https://kphshanghai.m.chenzhongtech.com/fw/photo/3xn3da4txhinyv4 里的 3xn3da4txhinyv4 即为photoId

返回如下：
{
  "ok": true,
  "result": {
    "userEid": "xq935932775",
    "userId": 344153274
  }
}
```

#### 获取用户个人信息（app版）
```
http://whosecard.com:8081/api/kuaishou/profile?userId=***&key=***

userId为用户唯一数字id，如: 119808726
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}

ps：所有统计性数字上万后会使用缩写，比如：3.1w
```

#### 获取单个视频的信息（app版）
```
http://whosecard.com:8081/api/kuaishou/photo/profile/v2?shareUrl=***&photoId=***&key=***

shareUrl是视频的分享短链接，如：https://v.kuaishou.com/16tm5I
photoId是视频的唯一数字id，如：5223894118313887282

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

<!--
#### 获取单个视频的信息（web版）
```
http://whosecard.com:8081/api/kuaishou/photo/profile/web/v1?shareUrl=***&photoId=***&key=***

shareUrl是视频的分享短链接，如：https://v.kuaishou.com/16tm5I
photoId是视频id，如：3xa7rzmrfa4epwq

⚠️shareUrl和photoId两者只需要传一个就行，但是最好传shareUrl，因为photoId有过期时间，同时有极少数视频的photoId参数无法获取正确结果。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回字段按字面意思理解即可
  }
}
```
-->

#### 获取小店商品列表
```
http://whosecard.com:8081/api/kuaishou/grocery/product?userId=358250606&page=1&key=***

userId为快手用户id。
page指定页数，从1开始。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取用户视频流Feed（app版）
```
http://whosecard.com:8081/api/kuaishou/user/feeds?userId=119808726&pcursor=***&key=***

userId为快手用户唯一数字id。
pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取tag的Feed流（app版）
```
http://whosecard.com:8081/api/kuaishou/tag/feeds?tag=手机摄影&feedType=***&pcursor=***&key=***

tag为指定话题参数。
feedType为请求feed类型，一共两种：热门与最近，分别取值为: hot|recent。
pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 获取tag详情页（app版）
```
http://whosecard.com:8081/api/kuaishou/tag/info?tag=手机摄影&key=***

tag为指定话题参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### location poi接口（app版）
```
http://whosecard.com:8081/api/kuaishou/location/poi?poiId=***&subPath=***&pcursor=***&key=***

poiId为位置id，如：68088943
subPath可取值为: detail与feed，分别代表详情页与feed页。
当subPath=feed时，pcursor用于翻页，第一页不用填，返回结果的pcursor值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```

#### 搜索接口（app版）
```
http://whosecard.com:8081/api/kuaishou/search?search_type=new&keyword=***&pcursor=***&ussid=***&key=***

search_type为搜索类型，可取值： new(综合), user(用户), imGroup(群聊), tag(标签), feed(作品)
keyword为要搜索的关键词
pcursor与ussid用于翻页，第一页不用填，返回结果的pcursor和ussid值为下一页的请求参数。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样
  }
}
```
