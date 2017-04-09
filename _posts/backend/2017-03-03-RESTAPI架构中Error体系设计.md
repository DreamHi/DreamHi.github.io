---
layout: post
title: RESTAPI架构中Error体系设计
categories: backend
catalog: true
original: true
tags: REST API Error
---
现在RestAPI盛行，我们在设计以提供RestAPI为主的架构中，除了API的URL设计，规范，返回结果格式等以外。
异常/错误体系的设计也很重要。

RestAPI结构设计中的错误分类，常用的有以下几种。
1. 客户端参数或者请求的错误
2. 服务器端的业务逻辑错误
3. 服务器端的db访问错误
4. 第三方服务错误(文件存取，通知等)
5. HTTP规范的错误code

## 错误详细
### 1.客户端参数的有效性判断
当从客户端传过来一个参数是，通过怎样的处理，才能证明它是正确的？
``` js
入力：参数A
处理: 
   1. 参数有值没值
      1.1 没值（空）
      1.2 有值
   2. 有值时类型对不
      2.1 类型不正确
      2.2 类型正确
   3. 类型正确时，值对不
      3.1 值不对 (非法字符，长度，边界以外的值）
      3.2 值对
   4. 值对时
      4.1 值不对 (存在性：比如判断值在db中是否存在，逻辑性：业务逻辑中是否整合.）
      4.2 值对
   5. 参数A，是正确的
```

### 2.服务器端的业务逻辑错误
根据业务不同，情况不同，此处省略

### 3.db访问错误
* 数据新规错误
* 数据更新错误
* 数据删除错误
* 数据检索错误

### 4.第三方服务错误(文件存取，通知等)
根据服务不同，情况不同，此处省略

### 5.HTTP规范的错误code

|Status Code|Constructor Name             |
|-----------|-----------------------------|
|400        |BadRequest                   |
|401        |Unauthorized                 |
|402        |PaymentRequired              |
|403        |Forbidden                    |
|404        |NotFound                     |
|405        |MethodNotAllowed             |
|406        |NotAcceptable                |
|407        |ProxyAuthenticationRequired  |
|408        |RequestTimeout               |
|409        |Conflict                     |
|410        |Gone                         |
|411        |LengthRequired               |
|412        |PreconditionFailed           |
|413        |PayloadTooLarge              |
|414        |URITooLong                   |
|415        |UnsupportedMediaType         |
|416        |RangeNotSatisfiable          |
|417        |ExpectationFailed            |
|418        |ImATeapot                    |
|421        |MisdirectedRequest           |
|422        |UnprocessableEntity          |
|423        |Locked                       |
|424        |FailedDependency             |
|425        |UnorderedCollection          |
|426        |UpgradeRequired              |
|428        |PreconditionRequired         |
|429        |TooManyRequests              |
|431        |RequestHeaderFieldsTooLarge  |
|451        |UnavailableForLegalReasons   |
|500        |InternalServerError          |
|501        |NotImplemented               |
|502        |BadGateway                   |
|503        |ServiceUnavailable           |
|504        |GatewayTimeout               |
|505        |HTTPVersionNotSupported      |
|506        |VariantAlsoNegotiates        |
|507        |InsufficientStorage          |
|508        |LoopDetected                 |
|509        |BandwidthLimitExceeded       |
|510        |NotExtended                  |
|511        |NetworkAuthenticationRequired|


## 我们先看看业界大佬的实例
### github
#### 客户端错误体系
1. 发送一个非法的json.

```javascript
 TTP/1.1 400 Bad Request
 Content-Length: 35
 {"message":"Problems parsing JSON"}
```

2.发送的json中，值得类型不正确。

```javascript
 HTTP/1.1 400 Bad Request
 Content-Length: 40
 {"message":"Body should be a JSON object"}
```


3.发送的json对象中，有非法的字段

```javascript
 HTTP/1.1 422 Unprocessable Entity
 Content-Length: 149
 
 {
  "message": "Validation Failed",
  "errors": [
    {
      "resource": "Issue",
      "field": "title",
      "code": "missing_field"
    }
  ]
 }
```

每个错误对象中，都有资源属性和字段属性，便于客户分析错误原因。

|错误code| 描述|
|---------|------------|
|missing|请求的资源不存在|
|missing_field|请求的字段在该资源中不存在|
|invalid|请求的字段在该资源中不合法|
|already_exists|字段值，在别的资源中存在|