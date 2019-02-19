#实时抖音接口

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.


####1. 实时获取up主发布的视频列表（按时间排序）
```
http://whosecard.com:8081/api/douyin/aweme/post?key=***&user_id=96637069360

如果要翻页，则需要传入max_cursor参数，此参数在前一页的请求中会返回，每次翻页都会更新。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

####2. 实时获取挑战视频列表（按热度排序）
```
http://whosecard.com:8081/api/douyin/aweme/challenge?key=***&ch_id=1611823344632835

如果要翻页，需要传入cursor参数（这里的参数跟前面的max_cursor不一样，不要搞混了），此参数在前一页的请求中会返回，每次翻页都会更新。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

####3. 获取抖音UP主详情页
```
http://whosecard.com:8081/api/douyin/aweme/user/detail?user_id=102020882079&key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

####4. 获取挑战详情页
```
http://whosecard.com:8081/api/douyin/aweme/challenge/detail?ch_id=1612674164817944&key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

####5. 实时获取单个抖音视频detail信息（不包含播放量）
```
http://whosecard.com:8081/api/douyin/aweme/detail?key=***&aweme_id=6580087189395213581

返回如下：
{
  "ok": true,
  "result": {
    "statistics": {
        "forward_count": 0,
        "digg_count": 1,  # 有效点赞数
        "play_count": 0,  # 此字段目前不返回真实数据
        "comment_count": 0,  # 有效评论数
        "aweme_id": "6572756298830449927",
        "share_count": 0
      },
    ... # 其它字段按字面意思理解
  }
}

result包含了抖音返回的所有字段数据，除了statistics字段外还会返回其它字段，按照字面意思理解即可。

划重点：请传入有效的aweme_id
```

####6. 获取抖音UP主商品橱窗列表
```
http://whosecard.com:8081/api/douyin/aweme/promotion?user_id=95899249695&cursor=0&key=***

每次返回10个商品信息，如果要翻页，则需要传入cursor参数，第一次请求时cursor为0，之后每次翻页传的cursor都要加10。
比如当cursor=0时，返回第1-10条商品信息。
比如当cursor=10时，返回第11-20条商品信息。
以此类推，每次请求结果可以根据返回的has_more参数判断是否需要翻页。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```


####7. 从haohuo获取单个商品详情
```
http://whosecard.com:8081/api/douyin/haohuo/product/item?key=***&url=https%3a%2f%2fhaohuo.snssdk.com%2fviews%2fproduct%2fitem2%3fid%3d3320163565905801015%26origin_type%3d3002002000%26origin_id%3d95899249695_3320163565905801015

url参数需要urlencode编码，此参数来自于【获取抖音UP主商品橱窗列表】接口的商品链接url字段。
如：https://haohuo.snssdk.com/views/product/item2?id=3320163565905801015&origin_type=3002002000&origin_id=95899249695_3320163565905801015

⚠️ url必须是https://haohuo.snssdk.com开头，否则此接口请求无效（如果是其它链接，如淘宝商品链接，则不要请求此接口）。

对于haohuo商品的详情数据，返回如下：
{
  "ok": true,
  "result": {
    "ajaxstaticitem": {***},  # 商品的静态信息
    "ajaxitem": {***}  # 商品的动态信息
  }
}

ps：返回的ajaxstaticitem与ajaxitem内容实际上是来自两个接口的，共同组成完整的商品详情信息。
```