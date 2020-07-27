---
title: 优化HTML5表单
seo-title: 优化HTML5表单
description: 可以优化HTML5表单的输出大小。
seo-description: 可以优化HTML5表单的输出大小。
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 优化HTML5表单 {#optimizing-html-forms}

HTML5表单以HTML5格式呈现表单。 生成的输出可能很大，具体取决于表单大小和表单中的图像等因素。 要优化数据传输，建议的方法是使用提供请求的Web服务器压缩HTML响应。 此方法可减小响应大小、网络流量以及在服务器和客户端计算机之间传输数据所需的时间。

本文介绍使用JBoss为Apache Web Server 2.0 32位启用压缩所需的步骤。

>[!NOTE]
>
>以下说明不适用于Apache Web Server 2.0 32位以外的服务器。

获取适用于您的操作系统的Apache Web服务器软件：

* 对于Windows，从Apache HTTP Server项目站点下载Apache Web服务器。
* 对于Solaris 64位，请从Sunfreeware for Solaris网站下载Apache Web服务器。
* 对于Linux,Apache Web服务器预安装在Linux系统上。

Apache可以使用HTTP或AJP协议与JBoss通信。

1. 在APACHE_HOME/conf/httpd.conf文件中取消以下模块配 *置的注* 释。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >对于Linux，默认的APACHE_HOME目录为/etc/httpd/。

1. 在JBoss的端口8080上配置代理。

   将以下配置添加到APACHE_HOME/conf/httpd.conf *配置* 文件中。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >使用代理时，需要进行以下配置更改：
   >
   >* 访问： *https://&lt;server>:&lt;port>/system/console/configMgr*
   * 编辑Apache Sling推荐人过滤器的配置
   * 在“允许主机”中，添加代理服务器的条目


1. 启用压缩。

   将以下配置添加到APACHE_HOME/conf/httpd.conf *配置* 文件中。

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. 要访问AEM服务器，请使用https://[Apache_server]:80。
