---
layout: blogs_item
title: 几个HTTP服务器的横向测试比较
author: AcePeak
categories:
  - 积累
tags:
  - Web
  - 测试
  - 原创
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

192.168.8.91:1340	Ubuntu+Proxygen

{% highlight C++  %}
DEFINE_int32(http_port, 11000, "Port to listen on with HTTP protocol");
DEFINE_int32(spdy_port, 11001, "Port to listen on with SPDY protocol");
DEFINE_string(ip, "localhost", "IP/Hostname to bind to");
DEFINE_int32(threads, 0, "Number of threads to listen on. Numbers <= 0 "
             "will use the number of cores on this machine.");

class EchoHandlerFactory : public RequestHandlerFactory {
 public:
  void onServerStart() noexcept override {
    stats_.reset(new EchoStats);
  }

  void onServerStop() noexcept override {
    stats_.reset();
  }

  RequestHandler* onRequest(RequestHandler*, HTTPMessage*) noexcept override {
    return new EchoHandler(stats_.get());
  }

 private:
  folly::ThreadLocalPtr<EchoStats> stats_;
};

int main(int argc, char* argv[]) {
  std::vector<HTTPServer::IPConfig> IPs = {
    {SocketAddress(FLAGS_ip, FLAGS_http_port, true), Protocol::HTTP},
    {SocketAddress(FLAGS_ip, FLAGS_spdy_port, true), Protocol::SPDY},
  };

  if (FLAGS_threads <= 0) {
    FLAGS_threads = sysconf(_SC_NPROCESSORS_ONLN);
    CHECK(FLAGS_threads > 0);
  }

  HTTPServerOptions options;
  options.threads = static_cast<size_t>(FLAGS_threads);
  options.idleTimeout = std::chrono::milliseconds(60000);
  options.shutdownOn = {SIGINT, SIGTERM};
  options.handlerFactories = RequestHandlerChain()
      .addThen<EchoHandlerFactory>()
      .build();

  HTTPServer server(std::move(options));
  server.bind(IPs);

  // Start HTTPServer mainloop in a separate thread
  std::thread t([&] () {
    server.start();
  });

  t.join();
  return 0;
}
{% endhighlight %}


Ubuntu+apache+mod

{% highlight C++  %}
/* Include the required headers from httpd */
#include "httpd.h"
#include "http_core.h"
#include "http_protocol.h"
#include "http_request.h"

/* Define prototypes of our functions in this module */
static void register_hooks(apr_pool_t *pool);
static int example_handler(request_rec *r);

/* Define our module as an entity and assign a function for registering hooks  */

module AP_MODULE_DECLARE_DATA   example_module =
{
    STANDARD20_MODULE_STUFF,
    NULL,            // Per-directory configuration handler
    NULL,            // Merge handler for per-directory configurations
    NULL,            // Per-server configuration handler
    NULL,            // Merge handler for per-server configurations
    NULL,            // Any directives we may have for httpd
    register_hooks   // Our hook registering function
};


/* register_hooks: Adds a hook to the httpd process */
static void register_hooks(apr_pool_t *pool)
{

    /* Hook the request handler */
    ap_hook_handler(example_handler, NULL, NULL, APR_HOOK_LAST);
}

/* The handler function for our module.
 * This is where all the fun happens!
 */

static int example_handler(request_rec *r)
{
    /* First off, we need to check if this is a call for the "example" handler.
     * If it is, we accept it and do our things, it not, we simply return DECLINED,
     * and Apache will try somewhere else.
     */
    if (!r->handler || strcmp(r->handler, "example-handler")) return (DECLINED);

    // The first thing we will do is write a simple "Hello, world!" back to the client.
    ap_rputs("Hello, world!<br/>", r);
    return OK;
}
{% endhighlight %}

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
|| Ubuntu+Apache+Mod || 3272.74 || 9176.34 || 10618.78 ||
|| Ubuntu+Nodejs+Dsp(POST) || 3436.93 || 6231.99 || 6676.61 ||
