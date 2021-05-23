# 京东-实时接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 获取单个商品详情
```
http://whosecard.com:8081/api/jd/product/detail/v1?key=***&sku=3195185

sku参数为商品id，来自于商品列表接口中的wareid取值，不能为空

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取店铺商品列表
```
http://whosecard.com:8081/api/jd/shop/products/v1?key=***&shop_id=1000001782&seller_id=1036678467&page=1&sort=0

shop_id为店铺相关id，不能为空
page为翻页参数，从1开始，每次翻页需要加1
sort为排序参数，支持以下排序（默认为0）：
  0: 默认
  1: 销量
  2: 新品
  3: 低价优先
  4: 高价优先

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取商品评论列表
```
http://whosecard.com:8081/api/jd/product/comments/v1?key=***&sku=3195185&page=1

sku参数来自于商品列表接口中的wareid取值，不能为空
page为翻页参数，从1开始，每次翻页需要加1

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```
