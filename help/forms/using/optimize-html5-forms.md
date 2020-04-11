---
title: 优化HTML5表单
seo-title: 优化HTML5表单
description: 您可以优化HTML5表单的输出大小。
seo-description: 您可以优化HTML5表单的输出大小。
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 优化HTML5表单 {#optimizing-html-forms}

HTML5表单以HTML5格式呈现表单。 根据表单大小和表单中的图像等因素，生成的输出可能很大。 要优化数据传输，建议的方法是使用从中提供请求的Web服务器压缩HTML响应。 此方法可减小响应大小、网络流量以及在服务器和客户端计算机之间流化数据所需的时间。

本文介绍使用JBoss为Apache Web Server 2.0 32位启用压缩所需的步骤。

*注意：以下说明不适用于除Apache Web Server 2.0 32位之外的服务器。*

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

   将以下配置添加到APACHE_HOME/conf/httpd.conf *配置文* 件中。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >使用代理时，需要进行以下配置更改：
   >
   >* 访问：https://&lt;server>:&lt;port>/system/console/configMgr **
   * 编辑Apache Sling推荐人过滤器的配置
   * 在“允许主机”中，为代理服务器添加条目


1. 启用压缩。

   将以下配置添加到APACHE_HOME/conf/httpd.conf *配置文* 件中。

   ```java
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
