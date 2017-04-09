---
layout: post
title: COOKIE和SESSION
categories: frontend
catalog: true
original: true
tags: Cookie Session
---

HTTP协议是无状态的，服务器接受客户端的请求时并不知道这个请求是哪个用户的，用户的状态是什么样的。
服务器端为了把请求和用户的状态关联在一起。让请求变的有状态。于是有了session和cookie机制。

### cookie
cookie是保存在浏览器端的小型文本文件，内容为一系列键值对。Cookie的是http协议的一部分。
具体规范定义在[RFC2109: HTTP State Management Mechanism](https://www.ietf.org/rfc/rfc2109.txt)中。

#### Cookie工作原理  
1.浏览器发送HTTP请求给服务器  
2.服务器端生成Cookie值，在HTTP响应头中加入该值。Set-Cookie: cookie值  
3.浏览器收到HTTP响应，解析Cookie值，保存在浏览器端。不同域名的Cookie保存的路径不同。  
4.浏览器下次发送请求时，会自动把Cookie值加入HTTP请求的头字段中。Cookie: cookie值  
5.服务接受请求后，解析Cookie。就能知道这个用户的状态。  

![Cookie工作原理](/static/images/frontend/cookie.png)

#### Cookie存储：内存存储和硬盘存储
内存Cookie由浏览器维护，保存在内存中，浏览器关闭后就消失了。
硬盘Cookie保存在硬盘里，有一个过期时间，除非用户手工清理或到了过期时间，硬盘Cookie不会被删除。

#### Cookie的问题
1. Cookie大小4KB左右。
2. Cookie是保存在浏览器端的，而且是明文传递。容易篡改，因此在Cookie中不能保存敏感数据。

具体限制请参照[RFC2109 6.3 Implementation Limits](https://www.ietf.org/rfc/rfc2109.txt)

### session
为了改善cookie存在的缺陷。有了session。和cookie不同。session保存在服务器端。这样用户的敏感数据可以保存在服务器端。

#### Session工作原理  
1.浏览器发送HTTP请求给服务器  
2.服务器保存当前用户状态信息保存在文件或者数据库中，生成一个唯一ID，加入HTTP响应中，sessionId: 唯一ID  
3.浏览器收到HTTP响应，把该值保存在Cookie中。  
4.浏览器下次发送请求时，附带Cookie值给服务器。Cookie:sessionId=xxxxxxxx  
5.服务器接受请求后，从Cookie中解析sessionID，判断用户状态。  

#### Session的问题
开销大，每个用户都会生成一个独立的Session对象。一般Session都是保存在db中，每次收到请求时，需要验证Session的有效性，并更新最新状态。
