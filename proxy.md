# 代理请求接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 使用代理转发国内请求
```
通过此接口请求目标网站，我们将随机分配国内代理IP代为请求并返回目标网站的结果。
建议正式使用前先充分测试此接口是否能满足你的代理需求。

POST http://whosecard.com:8081/api/proxy/request?key=***

参数key放在url里请求，其它参数放在json请求体里（即请求时Content-Type=application/json）
json请求体参数如下：
  method: 传GET或POST，不能为空
  url: 请求链接，不能为空
  params: 查询字符串参数，字典类型，默认为空
  json: post时传的json请求体，字典类型，默认为空
  data: post时传的form表单，字典类型，默认为空
  cookies: 字典类型，默认为空
  headers: 字典类型，默认为空
  timeout: 整数，默认为5
  allow_redirects: 是否重定向请求，bool类型[true|false]，默认为true
  verify: 是否验证SSL证书，bool类型[true|false]，默认为true

示例json参数:
{
    "url": "https://www.baidu.com",
    "method":"GET",
    "params": {"test":"a"},
    "cookies": {"a":"b"},
    "headers": {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"},
    "timeout": 3,
    "verify": false
}

返回的headers里有PROXY_OK和PROXY_ERROR两个字段，含义如下：
PROXY_OK：为true表示代理服务器是否转发成功，将正常扣费，否则不扣费
PROXY_ERROR：当代理服务器遇到错误时，将错误解释放在此字段

只要请求时未发生异常，都认为正常请求（返回的状态码不一定是200）
```

#### 使用代理转发海外请求
```
通过此接口请求目标网站，我们将随机分配海外代理IP代为请求并返回目标网站的结果。
建议正式使用前先充分测试此接口是否能满足你的代理需求。

POST http://whosecard.com:8081/api/proxy/request/abroad?key=***

请求参数及使用方式与【使用代理转发国内请求】接口完全一样。
```
