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

### 




## 参考链接
- [curl用法指南](http://www.ruanyifeng.com/blog/2011/09/curl.html)
- [curl网站开发指南](http://www.ruanyifeng.com/blog/2011/09/curl.html)