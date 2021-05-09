# 饿了么-实时接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 根据经纬度获取店铺列表
```
http://whosecard.com:8081/api/eleme/shop/list/v1?key=***&lat=31.302649&lng=121.508036&category_type=1&page=1&sort_type=0

参数解释：
lng与lat分别为指定的经纬度，不能为空
category_type为店铺类型，默认为0，取值范围如下：
  0: 商超便利
  1: 买药
  2: 鲜花绿植
  3: 买菜
  4: 水果
page为翻页参数，注意是从1开始，每次翻页+1即可
sort_type为排序类型，默认为0，取值范围如下：
  0: 综合排序
  1: 距离优先
  2: 距离优先

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取店铺基础信息
```
http://whosecard.com:8081/api/eleme/shop/info/v1?key=***&store_id=531831336

参数解释：
store_id为店铺id，从店铺列表接口中获取

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取店铺商品分类
```
http://whosecard.com:8081/api/eleme/shop/category/v1?key=***&store_id=531831336

参数解释：
store_id为店铺id，从店铺列表接口中获取

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取店铺指定分类下的商品列表
```
http://whosecard.com:8081/api/eleme/shop/category/detail/v1?key=***&store_id=531831336&category_ids=1,8&category_type=3

参数解释：
store_id为店铺id，从店铺列表接口中获取
category_ids为分类id，取值于【店铺商品分类接口】里每个分类的cat2Ids字段，多个分类id用半角逗号分割，每次最多传3个id
category_type为分类type，取值于【店铺商品分类接口】里每个分类的type字段

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```
