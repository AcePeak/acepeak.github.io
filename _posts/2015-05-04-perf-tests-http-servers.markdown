---
layout: blogs_item
title: 几个HTTP服务器的横向测试比较
author: AcePeak
categories: [Internet]
tags: 
- Web
- 原生
---


===
测试环境
===

192.168.8.161		测试发起服务器
192.168.8.91		被测试Linux服务器
192.168.8.8		被测试Windows服务器

其中被测试机器的配置一样

===
测试类型
===

192.168.8.8:9000		Windows+IIS+Asp.net

使用asp.net技术，写了一个Handler.ashx，内容如下：


{% highlight C#  %}
<%@ WebHandler Language="C#" Class="Handler" %>

using System;
using System.Web;

public class Handler : IHttpHandler {
    
    public void ProcessRequest (HttpContext context) {
        context.Response.ContentType = "text/plain";
        context.Response.Write("Hello World");
    }
 
    public bool IsReusable {
        get {
            return false;
        }
    }
}
{% endhighlight %}


192.168.8.91:1337	Linux+Nodejs

{% highlight javascript  %}
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World\n');
}).listen(9702, '127.0.0.1');
console.log('Server running at http://127.0.0.1:9702/');
{% endhighlight %}

192.168.8.91:1338	Linux+Nodejs+Express+Cluster

{% highlight javascript  %}
var cluster = require('cluster');
var numCPUs = require('os').cpus().length;
if (cluster.isMaster) {
  for (var i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
} else {
    var express = require('express');
    var app = express();
    app.get('/', function(req, res){
                res.writeHead(200, {'Content-Type': 'text/plain'});
                res.end('Hello World\n');
    });
    app.listen(1338);
    console.log('listen on 1338');
}
{% endhighlight %}

192.168.8.91:1339	Linux+Nodejs+Cluster

{% highlight javascript  %}
var cluster = require('cluster');
var numCPUs = require('os').cpus().length;
if (cluster.isMaster) {
  for (var i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
} else {
    var http = require('http');
	http.createServer(function (req, res) {
		res.writeHead(200, {'Content-Type': 'text/plain'});
		res.end('Hello World\n');
	}).listen(1339, '192.168.8.161');
	console.log('Server running at http://127.0.0.1:1339/');
}
{% endhighlight %}

192.168.8.91:1340	Linux+Proxygen



===
测试结果
===

> 测试方法1：ab -r -c [10000|1000|100] -n 100000 http://xxx

16core+8G

|| 类型 || RPS(c=10000) || RPS(c=1000) || RPS(c=100) ||
|| Windows+IIS+Asp.net || 6770.54 || 9996.72 || 10381.01 ||
|| CentOS+Nodejs || X || 6036.13 || 6641.44 ||
|| CentOS+Nodejs+Express+Cluster || 4354.29 || 12757.53 || 11832.70 ||
|| CentOS+Nodejs+Cluster || 5214.44 || 12170.55 || 12501.20 ||
|| CentOS+DE || 2330.63 || 14022.68 || 13397.61 ||
|| CentOS+Nodejs+Dsp || 4945.00 || 6772.59 || 7157.34 ||


4core+4G

|| 类型 || RPS(c=10000) || RPS(c=1000) || RPS(c=100) ||
|| Ubuntu+Nodejs+Express+Cluster || 4157.49 || 6920.84 || 8935.38 ||
|| Ubuntu+Proxygen || 3272.74 || 9051.58 || 7332.77 ||
|| Ubuntu+Nodejs+Dsp(POST) || 3436.93 || 6231.99 || 6676.61 ||
