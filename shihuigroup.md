# 十荟团-实时接口

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
http://whosecard.com:8081/api/shihuigroup/listNearLeaders?key=***&lng=121.528064&lat=31.308544

lng与lat分别为指定的经纬度

此接口在app和微信小程序里返回的数据不完全相同，默认走app，如果要走小程序请求，请传参数source=wxmini

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 根据partnerId获取grouponId
```
http://whosecard.com:8081/api/shihuigroup/getGrouponId?partner_id=168968&key=***

partner_id是从【根据地理坐标获取附近自提点列表】接口获取到的相关id
返回如下：
{
  "ok": true,
  "result": {
    "grouponId": "150305",
    "partnerId": "168968"
  }
}
```

#### 获取指定团长店铺下的商品种类列表
```
http://whosecard.com:8081/api/shihuigroup/listCategory?key=***&groupon_id=93763&partner_id=351382

groupon_id与partner_id是从【根据地理坐标获取附近自提点列表】接口获取到的相关id

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 列出店铺下指定分类的商品列表
```
http://whosecard.com:8081/api/shihuigroup/listGoods?key=***&groupon_id=93763&partner_id=351382&category_id=473&category_type=1&page=1

groupon_id与partner_id是从【根据地理坐标获取附近自提点列表】接口获取到的相关id
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
