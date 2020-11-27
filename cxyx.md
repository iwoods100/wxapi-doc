# 橙心优选-实时接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 根据地理坐标获取附近自提点列表
```
http://whosecard.com:8081/api/cxyx/listNearLeaders?key=***&lng=121.528064&lat=31.308544&page=1

lng与lat分别为指定的经纬度
如果要翻页，则需要传入page参数，此参数默认初始值为1

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取指定团长店铺下的商品种类列表
```
http://whosecard.com:8081/api/cxyx/listCategory?key=***&uid=637276942853237785

uid是从【根据地理坐标获取附近自提点列表】接口获取到的团长id

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 根据地理坐标获取附近自提点列表
```
http://whosecard.com:8081/api/cxyx/listGoods?key=***&uid=637276942853237785&category_type=0&category_id=1&page=1

uid是从【根据地理坐标获取附近自提点列表】接口获取到的团长id
category_type与category_id是从【获取指定团长店铺下的商品种类列表】接口得到的字段
如果要翻页，则需要传入page参数，此参数默认初始值为1

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```
