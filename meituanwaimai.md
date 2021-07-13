# 美团外卖-实时接口

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
http://whosecard.com:8081/api/mtwaimai/poi/list?key=***&lng=121.528064&lat=31.308544&category_type=*&second_category_type=&page=0&sort_type=0

参数解释：
lng与lat分别为指定的经纬度，不能为空
category_type为店铺一级类型，目前支持这些类型： 超市便利(102620)，药店(102530)，鲜花/绿植(102529)
second_category_type为店铺二级分类，目前暂不需要传
page为翻页参数，注意是从0开始，每次翻页+1即可
sort_type为排序类型：默认为0
  0: 综合排序
  1: 销量优先
  2: 速度优先
  3: 评分优先
  4: 起送价最低
  5: 距离优先

注意：不同参数返回的结果格式是不一定相同的，以实际返回结果为准。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取指定店铺下的商品列表
```
http://whosecard.com:8081/api/mtwaimai/poi/products?key=***&wm_poi_id=*&category_type=*

参数解释：
wm_poi_id为店铺id
category_type为店铺一级类型，目前支持这些类型： 美食类(910), 超市便利(102620)，药店(102530)，鲜花/绿植(102529)

注意，不同category_type返回的结果格式是不一定相同，以实际返回结果为准

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取商店广告位里的商品列表
```
http://whosecard.com:8081/api/mtwaimai/poi/productSet?key=***&wm_poi_id=*&product_set_tag=*&page=0

参数解释：
wm_poi_id为店铺id
product_set_tag来自于商店的【获取指定店铺下的商品列表】接口，对应字段为：productsettag
page为翻页参数，注意是从0开始，每次翻页+1即可

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取商超店铺指定品类tag下的商品列表
```
http://whosecard.com:8081/api/mtwaimai/poi/sputag/products?key=***&wm_poi_id=*&spu_tag_id=*&tag_type=*&page=0

参数解释：
wm_poi_id为店铺id
spu_tag_id来自于【获取指定店铺下的商品列表】接口，对应字段为：food_spu_tags下tags字段数组里的tag值进行依次遍历获取，如果tags数组为空，则直接取food_spu_tags下的tag字段
tag_type来自于【获取指定店铺下的商品列表】接口，对应字段为spu_tag_id同级别下的type字段
page为翻页参数，注意是从0开始，每次翻页+1即可，此接口基本不需要翻页

由于商超店铺的商品种类繁多，所以需要对每个种类的商品列表单独获取。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 在店铺内搜索商品列表
```
http://whosecard.com:8081/api/mtwaimai/search/inShop?key=***&wm_poi_id=***&keyword=***&&page=0

参数解释：
wm_poi_id为店铺id
keyword为搜索关键词
page为翻页参数，注意是从0开始，每次翻页+1即可，不传默认为0

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```
