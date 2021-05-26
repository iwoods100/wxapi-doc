# 淘宝/天猫-实时接口

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
http://whosecard.com:8081/api/taobao/product/detail/v1?key=***&item_id=624015039172

item_id为商品id，不能为空

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
http://whosecard.com:8081/api/taobao/shop/products/v1?key=***&shop_id=100004927&seller_id=1036678467&page=1&sort=0

shop_id与seller_id为店铺相关id，不能为空
page为翻页参数，从1开始，每次翻页需要加1
sort为排序参数，支持以下排序（默认为0）：
  0: 综合
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
http://whosecard.com:8081/api/taobao/product/comments/v1?key=***&item_id=624015039172&page=1

item_id为商品id，不能为空
page为翻页参数，从1开始，每次翻页需要加1

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
根据关键词返回商品列表

http://whosecard.com:8081/api/taobao/search/v1?key=***&keyword=手机&page=1&search_tab=0&sort=0

shop_id与seller_id为店铺相关id，不能为空
page为翻页参数，从1开始，每次翻页需要加1
search_tab为搜索类型：0（搜全部），1（搜天猫）。默认为0
sort为排序参数，支持以下排序（默认为0）：
  0: 综合
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
