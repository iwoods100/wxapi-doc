#实时获取公众号历史发文页面

url请求需带上参数key，每个用户有唯一的key。

所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.

```
http://whosecard.com:8081/api/wx/profile?biz=***&key=***

eg:
http://whosecard.com:8081/api/wx/profile?biz=MjM5ODIyMTE0MA==&key=***

返回如下：
{
	"ok": true,
	"html": "历史列表页html文本"
 }

 默认最多返回最近十次发文（⚠️不是十篇也不是十天，是十次）

 如果需要翻页，需要带上offset参数，如offset=10，则返回从第11次开始的10次文章，此参数与微信接口的offset参数含义一致。

⚠️注意，如果是公众号自身的问题导致失败，依旧会扣费，并在error字段返回失败原因，同时会返回cost字段为true，如下：
{'ok': false, 'error': '此帐号已申请公众号帐号迁移流程，被冻结/回收，小主页暂无法访问。', 'cost': true}
{'ok': false, 'error': '此帐号已自主注销，内容无法查看。', 'cost': true}
{'ok': false, 'error': '经大量用户投诉，此帐号存在违规行为，已限制跳转到小主页。', 'cost': true}
# 之后可能会扩展更多公众号异常场景，建议使用cost字段判断是否需要重试

如果收到cost=true的失败返回结果，就不用再重试请求了。
如果是接口本身导致的失败则不会扣费，建议请求失败时设置最大重试次数。
```