# 汽车业务接口

#### 接口说明
* 账号注册请联系qq:1628121385，添加好友时请注明:wxapi
* url请求需带上参数key，每个用户有唯一的key。
* 所有接口均返回json格式，其中参数ok[true|false]表示是否请求成功.
* retCode为返回码，详情参考[返回码说明](https://github.com/iwoods100/wxapi-doc/blob/master/retcode.md)
* 当返回ok=false时，可以参考返回的error字段（如果存在的话）
* 一般来说，接口只要返回cost=true，就表示请求有效，会进行收费，此时请不要再重试了，这种情况一般是请求资源已经失效。

#### 根据vin code获取标准设备信息
```
http://whosecard.com:8081/api/car/vin?vin=LFVBA24B323018323&key=***

参数vin请替换为自己想要查询的vin code。

对于haohuo商品的详情数据，返回如下：
{
  "ok": true,
  "cost": true,
  "result": {***},
  "retCode": 0
}
```
