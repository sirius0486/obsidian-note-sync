> curl 是一个无比有用的网站开发工具， 作用是发出网络请求，然后得到和提取数据，显示在“标准输出” ， 支持多种协议


## 用法指南


### 查看网页源码

```bash
curl domain_url

# example
curl www.sina.com

## response
　　<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
　　<html><head>
　　<title>301 Moved Permanently</title>
　　</head><body>
　　<h1>Moved Permanently</h1>
　　<p>The document has moved <a href="http://www.sina.com.cn/">here</a>.</p>
　　</body></html>

# 保存该网页  加上 -o 参数
curl -o [文件名] www.sina.com

```

### 自动跳转

```bash
使用 -L 参数， curl就会跳转到新的网址， 因为有些网址是自动跳转的

# exmample
curl -L www.sina.com
```


### 显示头信息

```bash
使用 -i 参数， 可以显示 http response的头信息，同时查看网页源码
使用 -I 参数则只显示http response的头信息

# example
curl -i www.sina.com

curl -I www.sina.com

HTTP/1.1 200 OK
Server: Tengine
Content-Type: text/html
Content-Length: 24000
Connection: keep-alive
Date: Thu, 04 May 2023 09:37:00 GMT
Etag: W/"607e950b-c2c"V=5965C31
Expires: Thu, 04 May 2023 09:37:27 GMT
Cache-Control: max-age=120
Vary: Accept-Encoding
Via: http/1.1 ctc.yongfeng.union.222 (ApacheTrafficServer/6.2.1 [cRs f ]), cache25.l2ot7-1[0,0,200-0,H], cache34.l2ot7-1[1,0], cache9.au2[0,0,200-0,H], cache4.au2[2,0]
X-Via-CDN: f=aliyun,s=cache4.au2,c=203.13.23.10;f=sinaedge,s=cnc.beixian.union.199.nb.sinaedge.com,c=47.254.113.45;f=Edge,s=ctc.yongfeng.union.222,c=172.16.157.199
X-Via-Edge: 16831930203202d71fe2fc79d10ac6f57cf72
X-Powered-By: shci_v1.13
X-Via-SSL: ssl.62.sinag1.shx.lb.sinanode.com
Edge-Copy-Time: 1683192845793
Ali-Swift-Global-Savetime: 1683193020
Age: 60
X-Cache: HIT TCP_MEM_HIT dirn:11:307325662
X-Swift-SaveTime: Thu, 04 May 2023 09:37:51 GMT
X-Swift-CacheTime: 69
Timing-Allow-Origin: *
EagleId: 2ff62a9816831930809321638

```

### 显示通信过程

```bash

```


## 参考链接
- [curl用法指南](http://www.ruanyifeng.com/blog/2019/09/curl-reference.html)
- [curl网站开发指南](http://www.ruanyifeng.com/blog/2011/09/curl.html)