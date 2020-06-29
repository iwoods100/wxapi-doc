# 实时获取公众号阅读点赞/评论接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

参数中的url为文章链接，长短链接均可，但不能是临时链接。

#### 1. 实时获取公众号文章阅读点赞数据
```
http://whosecard.com:8081/api/msg/ext?url=***&key=***

参数中的url为urlencode后的永久链接
eg:
http://whosecard.com:8081/api/msg/ext?url=https%3a%2f%2fmp.weixin.qq.com%2fs%3f__biz%3dMjM5MzI5NTU3MQ%3d%3d%26mid%3d2651456339%26idx%3d1%26sn%3db28ead72f72decc7993d2db6a4a7f437%26scene%3d0%23wechat_redirect&key=***

返回如下：
{
	"ok": true,
	"clicksCount": 56602,  # 阅读量
	"likeCount": 196,  # 在看数
	"oldLikeCount": 100,  # 点赞数
	"top": 1,  # 当前文章在发布时的位置，从1开始计数
	"advertisementNum": 1,
	"advertisementInfo": [
	   {
	       "hint_txt": "每天介绍新的科技玩具",  # 推荐文本
	       # url为推荐卡片外链
	       "url": "https://mp.weixin.qq.com/mp/ad_biz_info?__biz=MzU4MjAzNjkyMw==&amp;sn=6c0dcba45519d4c528756f9f5151130c&amp;weixinadkey=ebfa1f9258d2febf727ffc036131081771b42edf685d445435b51cbd21776cc2cc882dbcbff116ee6988f889a6653733&amp;ticket=2gz4o657fhrrv&amp;gdt_vid=wx0aspf7bz2og7ig00&amp;weixinadinfo=11034783.wx0aspf7bz2og7ig00.0.1#wechat_redirect",
	       "type": "0",
	       "group_id": "",
	       "aid": "11034783",  # 广告id
	       "image_url": "",
	       "ad_desc": "",
	       "biz_appid": "wx98697a2c3864ea4a",
	       "biz_info": {  # 推荐的公众号信息，如果推荐的不是公众号则没有此字段
	         "user_name": "gh_b5782da976b0",
	         "nick_name": "狂丸",
	         "is_subscribed": 0,
	         "head_img": "http://wx.qlogo.cn/mmhead/Q3auHgzwzM7z1t6Nn99nJnyAQ0nsnnCvoYNd490BhPAcXzaqm87tnw/0",
	         "biz_uin": 3582036923
	       },
	       "pos_type": 0,
	       "watermark_type": 0,
	       "logo": "",
	       "is_cpm": 0,
	       "dest_type": 0
     }
  	],
  	"commentCount": 470,  # 评论总数
  	"onlyFansCanComment": false,
  	"commentEnabled": 1
 }

advertisementNum为该文章的附带广告数量，仅开通广点通的公众号才有。
advertisementInfo为微信接口返回的广告内容，具体含义参照字面含义。

划重点：如果给的链接是无效的，则error会返回check_url error开头的一串字符串：
{"ok": false, "error": "check_url error******"}
例如：
{"ok": false, "error": "check_url error, 此帐号已被屏蔽, 内容无法查看"}

此时不要再提交此链接！
```


#### 2. 实时获取公众号文章评论数据
```
http://whosecard.com:8081/api/msg/comment?url=***&key=***

参数中的url为urlencode后的永久链接
eg:
http://whosecard.com:8081/api/msg/comment?url=https%3a%2f%2fmp.weixin.qq.com%2fs%2fmkcNQ14cYaV2VWGywbHCsg&key=***

返回如下：

{
  'ok': true,
  'electedComment': [
    {
      'id': 5,
      'my_id': 29,
      'nick_name': '幻影',
      'logo_url': 'http://wx.qlogo.cn/mmopen/ajNVdqHZLLDLiadQbicUmG1b0PAugEdM46NOvBrY8LSzl2284msWzdDR99YyHTiaSqfa7s7pZdXg9Brm1wPrK2kAQ/132',
      'content': '厉害',
      'create_time': 1526022499,
      'content_id': '1481712138857742365',
      'like_id': 10001,
      'like_num': 1,
      'like_status': 0,
      'is_from_friend': 0,
      'reply': {
        'reply_list': [

        ]
      },
      'is_from_me': 0,
      'is_top': 0
    }
  ],
  "electedCommentTotalCnt": 4,
  "onlyFansCanComment": 4
}


划重点：如果给的链接是无效的，则error会返回check_url error开头的一串字符串：
{"ok": false, "error": "check_url error******"}
例如：
{"ok": false, "error": "check_url error, 此帐号已被屏蔽, 内容无法查看"}

此时不要再提交此链接！
```
