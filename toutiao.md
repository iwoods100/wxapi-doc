# 今日头条接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

```
http://whosecard.com:8081/api/toutiao/web?key=***&api=接口类型&其它参数=***

所有头条接口根据不同的api参数，对应调用不同的接口，统一返回格式如下：
{
  "ok": true,
  "result": {
    ... # 返回值与官方接口一样，字段比较多，按字面意思理解即可
  }
}
```

#### 发布列表（api=user_feed）
```
api=user_feed
user_token=用户token，如 MS4wLjABAAAAvazHMceCo3MeM9IJbll231AC8GkJDcrd__iZFw2hi4o
category=指定作品分类，可取值：profile_all(全部)、pc_profile_article(文章)、pc_profile_video(视频)、pc_profile_ugc(微头条)、profile_wenda(问答)，默认为profile_all
max_behot_time=翻页参数，第一页请求的时候可不传，之后翻页时此参数都会在前一页返回

示例url: http://whosecard.com:8081/api/toutiao/web?key=***&api=user_feed&category=profile_all&user_token=MS4wLjABAAAAvazHMceCo3MeM9IJbll231AC8GkJDcrd__iZFw2hi4o
```

#### 关注/粉丝数（api=user_fans_stat）
```
api=user_fans_stat
user_token=用户token，如 MS4wLjABAAAAvazHMceCo3MeM9IJbll231AC8GkJDcrd__iZFw2hi4o

示例url: http://whosecard.com:8081/api/toutiao/web?key=***&api=user_fans_stat&user_token=MS4wLjABAAAAvazHMceCo3MeM9IJbll231AC8GkJDcrd__iZFw2hi4o
```

#### 关键字搜索（api=search）
```
api=search
keyword=关键字，如 vlog
offset=翻页参数，取上一页请求的offset返回值作为下一页offset参数，第一页不需要传
search_type：搜索类型（1是综合，2是视频，4是用户，默认为1）

示例url: http://whosecard.com:8081/api/toutiao/web?key=***&api=search&keyword=vlog&search_type=1
```

#### 评论列表（api=item_comment）
```
api=item_comment
item_id=文章/视频id，如 6680829865307931139
offset：默认为0，每次返回10条，以此加10，如果返回评论列表为空，则无需再次请求

注意：web版只能获取前数十条，以实际返回数量为准

示例url: http://whosecard.com:8081/api/toutiao/web?key=***&api=item_comment&item_id=6680829865307931139
```

#### 指定频道feed流（api=ch_feed）
```
api=ch_feed
category=频道类型，默认为【推荐】渠道
max_behot_time=翻页参数，第一页请求的时候可不传，之后翻页时此参数都会在前一页返回

其中category可取值：
  __all__(推荐)、news_hot(热点)、组图(图片)、news_tech（科技）、news_entertainment（娱乐）、
  news_game（游戏）、news_sports（体育）、news_finance（财经）、数码（digital）、news_military（军事）、
  news_fashion（时尚）、news_travel（旅游）、news_discovery（探索）、育儿（news_baby）、news_regimen（养生）、
  news_essay（美文）、news_history（历史）、news_food（美食）

示例url: http://whosecard.com:8081/api/toutiao/web?key=***&api=ch_feed&category=__all__
```
