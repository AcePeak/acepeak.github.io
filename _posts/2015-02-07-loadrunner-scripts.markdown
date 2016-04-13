---
layout: blogs_item
title: LoadRunner实战系列之三：脚本
author: AcePeak
categories:
  - 积累
tags:
  - 原创
  - Web
  - 测试
  - LoadRunner
---


> 系列列表：
>
> [LoadRunner实战系列之一：安装]({% post_url 2015-02-05-loadrunner-install %})
>
> [LoadRunner实战系列之二：流程]({% post_url 2015-02-06-loadrunner-operation %})
>
> [LoadRunner实战系列之三：脚本]({% post_url 2015-02-07-loadrunner-scripts %})
>
> [LoadRunner实战系列之四：术语]({% post_url 2015-02-08-loadrunner-glossary %})

##脚本篇

1.HTTP的GET请求

这里以访问百度为例，地址http://www.baidu.com/s?wd=mobile，表示在百度上搜索mobile。具体脚本如下（有注释）


{% highlight c++ %}
Action()  
{  
    int status;  
    lr_start_transaction("send");  

    web_reg_find("Search=Body",//这里说明在Body的范围内查找  
                 "SaveCount=ret_Count",//这里表示把返回值的个数放在变量ret_Count里  
                 "Text=mobile",//这里表示查找的内容是“mobile”  
                 LAST);  

    status=web_url("Baidu_Search",
        "URL= http://www.baidu.com/s?wd=mobile",
        "TargetFrame=Main",
        "Resource=0",
        "RecContentType=text/html",
        "Mode=http",
        LAST );

    lr_output_message("Request Status:%d",status);  
    lr_output_message("查找到的返回值个数:%d",atoi(lr_eval_string("{ret_Count}")));  


    if (atoi(lr_eval_string("{ret_Count}")) > 0){//这里判断检查到的个数  
         lr_output_message("Rec successful.");  
         lr_end_transaction("send", LR_PASS);  
     }  
     else{
         lr_error_message("Rec failed");  
         lr_end_transaction("send", LR_FAIL);  
     }

    return 0;  
}  
{% endhighlight %}


2.HTTP POST请求
这个是在我们项目中用到的，发送POST请求，进行自然语言识别的，脚本如下：

{% highlight c++ %}
Action()  
{  
    int status;  

    lr_start_transaction("send");  

    web_reg_find("Search=Body",//这里说明在Body的范围内查找  
                 "SaveCount=ret_Count",//这里表示把返回值的个数放在变量ret_Count里  
                 "Text=t",//这里表示查找的内容是“t”  
                 LAST);  

    status=web_submit_data("trs",  
                "Action=http://192.168.77.185:9002/recognizeText",//地址  
                "Method=POST",//POST请求  
                "RecContentType=text/html",  
                "Mode=HTML",  
                ITEMDATA,  
                "Name=usercontent","Value=gprs",ENDITEM,//这一行表示传入一个参数usercontent，值为gprs  
                "Name=Accept","Value=text/plain",ENDITEM,  
                LAST);  

     lr_output_message("Request Status:%d",status);  

     if (atoi(lr_eval_string("{ret_Count}")) > 0){//这里判断检查到的个数  
         lr_output_message("Rec successful.");  
         lr_end_transaction("send", LR_PASS);  
     }  
     else{
         lr_error_message("Rec failed");  
         lr_end_transaction("send", LR_FAIL);  
     }

     return 0;  
}  
{% endhighlight %}


3.WebService请求

详细脚本如下：

{% highlight c++ %}
Action()  
{  
    int status;  

    lr_start_transaction("send");  

    status=web_service_call( "StepName=getSupportCity_102",  
        "SOAPMethod=WeatherWebService|WeatherWebServiceSoap|getSupportCity",//这里是我已经引用了webservice的名称及调用方法  
        "ResponseParam=response",  
        "Service=WeatherWebService",  
        "ExpectedResponse=SoapResult",  
        "Snapshot=t1353067092.inf",  
        BEGIN_ARGUMENTS,  
                      "byProvinceName=安徽",//这里是入参，参数名称：byProvinceName，值：安徽。入参和返回值的名称都可以再引用里看见  
        END_ARGUMENTS,  
        BEGIN_RESULT,  
                      "getSupportCityResult=result",//这里是返回值，名称：getSupportCityResult，把它放到变量result中  
        END_RESULT,  
        LAST);  

    lr_output_message("Request Status:%d",status);  
    lr_output_message("Result:%s",lr_eval_string("{result}"));//这里把返回值输出，调试webservice的时候用  


    if(strstr(lr_eval_string("{result}"),"合肥")>0){//这里是判断返回值中是否包含“合肥”  
        lr_end_transaction("send",LR_PASS);  
    }else{  
        lr_end_transaction("send",LR_AUTO);  
    }  

    return 0;  
}  
{% endhighlight %}


4.Socket请求
我这里指的是简单的Socket请求，端连接，发送接收的都是一个字符串。比较复杂的Socket请求，自己录制脚本。如果不知道，自己去查。
详细脚本如下，另外还包含一个data.ws文件，用来声明发送和接收的字节数组及其长度的，并指定要发送的内容（发送的内容一样可以参数化的）

{% highlight c++ %}
#include "lrs.h"  
Action()  
{  
    char *recvbuf;  
    int recvlen=0;  
    int rc;  

    lrs_startup(257);  

    lr_start_transaction("Trans_1");  
    lr_start_transaction("Conn_1");  

    rc=lrs_create_socket("socket0", "TCP", "RemoteHost=192.168.1.101:8888",  LrsLastArg);//创建Socket连接  

    if (rc != 0 ) {
        lr_end_transaction("Conn_1", LR_FAIL);
        lr_end_transaction ("Trans_1", LR_FAIL);
        return 0;
    }  
    lr_end_transaction("Conn_1", LR_PASS);  //判断socket是否链接成功的事务，0表示创建成功  

    lrs_send("socket0", "buf0", LrsLastArg); //发送buf0，buf0为在data.ws中定义的发送变量  

    lrs_receive("socket0", "buf1", LrsLastArg); //接收消息，存放在buf1中，buf1是在data.ws中定义的接收数组，注意数组长度一定要大于等于实际接收长度  

    lrs_get_last_received_buffer("socket0",&recvbuf,&recvlen);//把Socket最后接收的字节数组，长度放在recvlen中，内容放在recvbuf中  

    lr_output_message("Received:%s",lr_eval_string(recvbuf));  

    if(recvlen>3)  
        lr_end_transaction("Trans_1", LR_PASS);  
    else  
        lr_end_transaction ("Trans_1", LR_FAIL);  


    lrs_disable_socket("socket0", DISABLE_SEND_RECV);  

    lrs_close_socket("socket0");  
    return 0;  
}  
{% endhighlight %}


{% highlight c++ %}
//data.ws  
;WSRData 2 1  

send  buf0 32  
    "hehehehe"  

recv  buf1 50  



-1  
{% endhighlight %}
