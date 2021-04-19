# 大众点评-实时接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 获取店铺列表
```
http://whosecard.com:8081/api/dianping/shop/list?key=***&lng=121.528064&lat=31.308544&categoryid=*&start=0&sort_type=0

参数解释：
lng与lat分别为指定的经纬度，不能为空
start为翻页参数，注意是从0开始，下一页的start将在本次请求的nextStartIndex字段返回
categoryid为店铺类型，目前支持这些类型，不能为空：
  10: 美食
  133: 酒吧
  135: ktv
  140: 洗浴/汗蒸
  141: 按摩/足疗
  158: 美容spa
  2754: 密室
  26085: 鲜花
sort_type为排序类型：默认为0
  0: 智能排序
  1: 距离优先
  2: 人气优先
  3: 好评优先
  4: 口味优先
  5: 环境优先
  6: 服务优先
  8: 低价优先
  9: 高价优先

注意：
  不同categoryid返回的结果格式是不一定相同的，以实际返回结果为准。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取单个店铺详情
```
http://whosecard.com:8081/api/dianping/shop/detail?key=***&shopid=*

参数解释：
shopid为店铺id，可以是数字id或字母id

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取店铺评价列表
```
http://whosecard.com:8081/api/dianping/shop/review?key=***&shopid=*&start=0

参数解释：
shopid为店铺id，可以是数字id或字母id
start为翻页参数，注意是从0开始，下一页的start将在本次请求的nextStartIndex字段返回

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```
