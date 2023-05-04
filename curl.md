> curl 是一个无比有用的网站开发工具， 作用是发出网络请求，然后得到和提取数据，显示在“标准输出” ， 支持多种协议

从名字就可以看出来 curl  -> client URL 工具的意思， 如果你更偏好使用命令行，curl完全可以取代Postman这一类图形工具

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
`-v`参数可以显示一次http通信的整个过程，包括端口连接和http request头信息。

# example

curl -v www.sina.com

如果需要输出到文件查看更详细的通信信息， 那么可以

curl --trace output.txt www.sina.com

curl --trace-ascii output.txt www.sina.com
```


### 发送表单信息

```bash

# GET 把数据附在网址后面即可
curl domain_url/endPoint?data=xxx

# POST 需要用到--data参数
curl -X POST --data "data=xxx" example.com/form.cgi

```


### HTTP动词

```bash
curl默认的HTTP动词是GET，使用`-X`参数可以支持其他动词

curl -X POST www.example.com

curl -X DELETE www.example.com

```


### 文件上传

假定文件上传的表单长这个样子
```html
　　<form method="POST" enctype='multipart/form-data' action="upload.cgi">  
　　　　<input type=file name=upload>  
　　　　<input type=submit name=press value="OK">  
　　</form>
```

则可以用curl这样上传文件
```bash
curl --form upload=@localfilename --form press=OK [URL]
```


### Referer字段

```bash
有时你需要在http request头信息中，提供一个referer字段，表示你是从哪里跳转过来的。

curl --referer http://www.example.com http://www.example.com

```


### HTTP动词

```bash
curl默认的HTTP动词是GET，使用`-X`参数可以支持其他动词

curl -X POST www.example.com

curl -X DELETE www.example.com

```

### User Agent字段

```bash
curl --user-agent "[User Agent]" [URL]

```

### Cookie

```bash
使用`--cookie`参数，可以让curl发送cookie。

curl --cookie "name=xxx" www.example.com

至于具体的cookie的值，可以从http response头信息的`Set-Cookie`字段中得到。

`-c cookie-file`可以保存服务器返回的cookie到文件，`-b cookie-file`可以使用这个文件作为cookie信息，进行后续的请求。

curl -c cookies http://example.com  
curl -b cookies http://example.com

```

### 增加头信息

有时需要在http request之中，自行增加一个头信息。`--header`参数就可以起到这个作用

```bash
# 有时需要在http request之中，自行增加一个头信息。`--header`参数就可以起到这个作用

curl --header "Content-Type:application/json" http://example.com
```

### HTTP认证

```bash
# 有些网域需要HTTP认证，这时curl需要用到`--user`参数

curl --user name:password example.com
```

## 参考链接
- [curl用法指南](http://www.ruanyifeng.com/blog/2019/09/curl-reference.html)
- [curl网站开发指南](http://www.ruanyifeng.com/blog/2011/09/curl.html)