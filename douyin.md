# 实时抖音接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

**除非特殊说明，默认都是从app接口获取数据。**

#### 首页推荐流视频
```
http://whosecard.com:8081/api/douyin/aweme/feed?key=***

视频为主页随机更新，遇到重复视频也是正常现象。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 实时获取用户发布的音乐作品列表
```
http://whosecard.com:8081/api/douyin/aweme/music/list?key=***&user_id=96637069360

每页最多返回10个音乐作品，如果要翻页，则需要传入cursor参数，此参数在前一页的请求中会返回，每次翻页都会更新。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 实时获取单个音乐作品详情
```
http://whosecard.com:8081/api/douyin/aweme/music/detail?key=***&music_id=6564548752472345351

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 实时获取单个音乐作品关联的视频列表
```
http://whosecard.com:8081/api/douyin/aweme/music/aweme/list?key=***&music_id=6564548752472345351

每页最多返回18个音乐作品，如果要翻页，则需要传入cursor参数，此参数在前一页的请求中会返回，每次翻页都会更新。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 实时获取用户发布的视频列表（按时间排序）
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

<!--
#### 实时获取用户发布的视频列表 - 网页版（按时间排序）
```
http://whosecard.com:8081/api/douyin/aweme/post/web?key=***&user_id=96637069360

如果要翻页，则需要传入max_cursor参数，此参数在前一页的请求中会返回，每次翻页都会更新。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}

ps： 本接口的字段比app版本返回的会少一些，但核心字段差不多都有，同时会返回作品播放量。
```
-->

#### 实时获取用户喜欢（点赞）的视频列表（按时间排序）
```
http://whosecard.com:8081/api/douyin/aweme/favorite?key=***&user_id=96637069360

如果要翻页，则需要传入max_cursor参数，此参数在前一页的请求中会返回，每次翻页都会更新。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 实时获取话题/挑战视频列表（按热度排序）
```
http://whosecard.com:8081/api/douyin/aweme/challenge?key=***&ch_id=1611823344632835&is_commerce=1

参数is_commerce不能为空，此值是从话题/挑战详情接口里获取到的，如果is_commerce=1则表示为商业话题，传0则为普通话题
如果要翻页，需要传入cursor参数（这里的参数跟前面的max_cursor不一样，不要搞混了），此参数在前一页的请求中会返回，每次翻页都会更新。
此接口返回的视频个数可能不固定，具体以实际为准。

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取抖音用户详情页
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

#### 获取话题/挑战详情页
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

#### 获取话题/挑战的相关地点
```
http://whosecard.com:8081/api/douyin/aweme/poi/challenge/related?ch_id=***&key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 实时获取单个抖音视频detail信息（不包含播放量）
```
http://whosecard.com:8081/api/douyin/aweme/detail?key=***&aweme_id=6580087189395213581&short_url=https://v.douyin.com/JXwVogj/

aweme_id是视频id，short_url是视频分享的短链接，传其中任意一个都可以

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

当视频不存在时，则返回如下：
{
  "cost": true,
  "error": "作品不存在",
  "ok": false,
  "result": {
    "extra": {
      "fatal_item_ids": [],
      "logid": "20190424113225010016028077357335",
      "now": 1556076745000
    },
    "log_pb": {
      "impr_id": "20190424113225010016028077357335"
    },
    "status_code": 0
  }
}

划重点：请传入有效的aweme_id
```

#### 获取视频评论列表
```
http://whosecard.com:8081/api/douyin/aweme/comment?key=***&aweme_id=***

如果要翻页，需要传入cursor参数（这里的参数跟前面的max_cursor不一样，不要搞混了），此参数在前一页的请求中会返回，每次翻页都会更新。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取视频评论回复列表
```
http://whosecard.com:8081/api/douyin/aweme/comment/reply?key=***&aweme_id=***&comment_id=***

如果要翻页，需要传入cursor参数，此参数在前一页的请求中会返回，每次翻页都会更新。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取抖音用户商品橱窗列表
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


#### 从haohuo获取单个商品详情
```
http://whosecard.com:8081/api/douyin/haohuo/product/item?key=***&url=https%3a%2f%2fhaohuo.snssdk.com%2fviews%2fproduct%2fitem2%3fid%3d3320163565905801015%26origin_type%3d3002002000%26origin_id%3d95899249695_3320163565905801015

url参数需要urlencode编码，此参数来自于【获取抖音用户商品橱窗列表】接口的商品链接url字段。
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

#### 抖音搜索
```
http://whosecard.com:8081/api/douyin/aweme/search?keyword=***&search_source=***&key=***

keyword为搜索关键词，如：北京坊
search_source为搜索类型，目前支持以下取值：
  video_search: 搜索视频
  poi: 搜索地点
  user: 搜索用户，此时keyword建议填用户的short_id(抖音号)
  challenge: 搜索话题/挑战
  shopping: 搜索商品

如果对搜索结果如需翻页，可传入cursor参数（上一页会返回下一页的cursor值）
如果是搜索视频，额外支持以下参数：
  sort_type: 对结果排序，取值为 0（综合排序），1（最多点赞），2（最新发布）
  publish_time: 限制发布时间，取值为 0（不限），1（一天内），7（一周内），182（半年内）

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 根据poi_id获取地点详情页数据
```
http://whosecard.com:8081/api/douyin/aweme/poi/detail?poi_id=***&key=***

poi_id为地点的id，如：B0FFJ93NTT
获取地点的详情页数据，包括评分，坐标信息等等

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```


#### 根据poi_id获取地点发布的视频列表
```
http://whosecard.com:8081/api/douyin/aweme/poi/aweme?poi_id=***&cursor=**&key=***

poi_id为地点的id，如：B0FFJ93NTT
cursor在翻页时会用到，初始默认为0，如果前一页请求返回的has_more=1，取cursor返回值可获取下一页数据

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取用户粉丝列表
```
http://whosecard.com:8081/api/douyin/aweme/user/follower/list?key=***&user_id=***

如果要翻页，需要传入max_time参数，此参数可从前一页的返回值min_time获取（⚠️这里是min_time，不是max_time），每次翻页都会更新。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 获取用户关注列表
```
http://whosecard.com:8081/api/douyin/aweme/user/following/list?key=***&user_id=***

如果要翻页，需要传入max_time参数，此参数可从前一页的返回值min_time获取（⚠️这里是min_time，不是max_time），每次翻页都会更新。
返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 品牌热DOU榜 - 品牌分类列表
```
http://whosecard.com:8081/api/douyin/aweme/hotsearch/brand/category?key=***

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 品牌热DOU榜 - 指定品牌分类下的历史榜单
```
http://whosecard.com:8081/api/douyin/aweme/hotsearch/brand/weekly/list?key=***&category_id=**

category_id为品牌分类id，从【品牌热DOU榜 - 品牌分类列表】接口获取

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 品牌热DOU榜 - 指定品牌分类下的指定某一期榜单信息
```
http://whosecard.com:8081/api/douyin/aweme/hotsearch/brand/billboard?key=***&category_id=**&start_date=**

category_id为品牌分类id，从【品牌热DOU榜 - 品牌分类列表】接口获取
start_date为指定某一期榜单，如果为空字符串则取最近一期，可选值从【品牌热DOU榜 - 指定品牌分类下的历史榜单】接口获取

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 品牌热DOU榜 - 获取单个品牌的详情数据
```
http://whosecard.com:8081/api/douyin/aweme/hotsearch/brand/detail?key=***&category_id=**&brand_id=**

category_id为品牌分类id，从【品牌热DOU榜 - 品牌分类列表】接口获取
brand_id为品牌id，从【品牌热DOU榜 - 指定品牌分类下的指定某一期榜单信息】接口获取

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 抖音直播间基础信息 - 包括当前观看人数等
```
http://whosecard.com:8081/api/douyin/webcast/room/info?key=***&room_id=**

room_id是直播间id，对于正在直播的用户，可以从用户详情接口里获得room_id

返回如下：
{
  "ok": true,
  "result": {
    ... # 返回值与抖音接口一样，字段比较多，按字面意思理解即可
  }
}
```
