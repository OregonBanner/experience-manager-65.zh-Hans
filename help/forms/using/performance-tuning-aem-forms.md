---
title: AEM Forms 服务器性能优化
seo-title: AEM Forms 服务器性能优化
description: 为了使AEM Forms发挥最佳性能，您可以微调缓存设置和JVM参数。 此外，使用Web服务器可以提高AEM Forms部署的性能。
seo-description: 为了使AEM Forms发挥最佳性能，您可以微调缓存设置和JVM参数。 此外，使用Web服务器可以提高AEM Forms部署的性能。
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
role: Administrator
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 1%

---

# AEM Forms 服务器性能优化{#performance-tuning-of-aem-forms-server}

本文讨论了您可以实施的策略和最佳实践，以减少瓶颈并优化AEM Forms部署的性能。

## 缓存设置{#cache-settings}

您可以在AEM Web配置控制台中使用&#x200B;**Mobile Forms配置**&#x200B;组件，配置和控制AEM Forms的缓存策略，具体位置为：

* (AEM Forms on OSGi)`https://'[server]:[port]'/system/console/configMgr`
* (JEE上的AEM Forms)`https://'[server]:[port]'/lc/system/console/configMgr`

缓存的可用选项如下：

* **无**:强制不缓存任何对象。实际上，这会降低性能，并且由于缺少缓存而需要高内存可用性。
* **保守派**:指示仅缓存在渲染表单之前生成的中间工件，例如包含内联片段和图像的模板。
* **咄咄逼人**:强制缓存几乎所有可缓存的内容，包括呈现的HTML内容（除了保守缓存级别的所有工件之外）。这会产生最佳性能，但也会消耗更多内存来存储缓存的伪像。 激进的缓存策略意味着在缓存渲染的内容时，您在渲染表单时将获得持续的时间性能。

AEM Forms的默认缓存设置可能不足以获得最佳性能。 因此，建议使用以下设置：

* **缓存策略**:攻击性
* **缓存大小** （根据表单数量）：根据需要
* **最大对象大小**:根据需要

![移动Forms配置](assets/snap.png)

>[!NOTE]
>
>如果您使用AEM Dispatcher缓存自适应表单，则它也会缓存包含带有预填充数据的表单的自适应表单。 如果此类表单是从AEM Dispatcher缓存提供的，则可能会导致向用户提供预填充或过时的数据。 因此，请使用AEM Dispatcher缓存未使用预填充数据的自适应表单。 此外，调度程序缓存不会自动使缓存的片段失效。 因此，请勿将其用于缓存表单片段。 对于此类表单和片段，请使用[自适应表单缓存](../../forms/using/configure-adaptive-forms-cache.md)。

## JVM参数{#jvm-parameters}

为了获得最佳性能，建议使用以下JVM `init`参数来配置`Java heap`和`PermGen`。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>推荐的设置适用于Windows 2008 R2 8核心和OracleHotSpot 1.7（64位）JDK，并且应根据您的系统配置进行放大或缩小。

## 使用Web服务器{#using-a-web-server}

自适应表单和HTML5表单以HTML5格式呈现。 结果输出可能会很大，具体取决于表单大小和表单中图像等因素。 为优化数据传输，建议使用从中提供请求的Web服务器压缩HTML响应。 此方法可减少响应大小、网络流量以及在服务器和客户端计算机之间传输数据所需的时间。

例如，执行以下步骤以使用JBoss对Apache Web Server 2.0 32位启用压缩：

>[!NOTE]
>
>以下说明不适用于Apache Web Server 2.0 32位以外的任何服务器。 有关特定于任何其他服务器的步骤，请参阅相应的产品文档。

以下步骤演示了使用Apache Web Server启用压缩所需的更改

**获取适用于您的操作系统的Apache Web服务器软件**

* Windows:从Apache HTTP Server项目站点下载Apache Web服务器。
* Solaris 64位：从Sunfreeware for Solaris网站下载Apache Web服务器。
* Linux:Linux系统上预装了Apache Web服务器。

Apache可以使用HTTP协议与CRX通信。 配置用于使用HTTP进行优化。

1. 在`APACHE_HOME/conf/httpd.conf`文件中取消对以下模块配置的注释。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >对于Linux，默认的`APACHE_HOME`为`/etc/httpd/`。

1. 在crx的端口4502上配置代理。
在`APACHE_HOME/conf/httpd.conf`配置文件中添加以下配置。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 启用压缩。 在`APACHE_HOME/conf/httpd.conf`配置文件中添加以下配置。

   **对于HTML5表单**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **对于自适应表单**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   要访问crx服务器，请使用`https://'server':80`，其中`server`是运行Apache服务器的服务器名称。

## 在运行AEM Forms {#using-an-antivirus-on-server-running-aem-forms}的服务器上使用防病毒

在运行防病毒软件的服务器上可能会出现性能缓慢的情况。 防病毒（访问扫描）软件始终扫描系统的所有文件。 这可能会降低服务器速度，并且会影响AEM Forms的性能。

要提高性能，您可以指导防病毒软件从始终开启（访问）扫描中排除以下AEM Forms文件和文件夹：

* AEM安装目录。 如果无法排除完整目录，请排除以下内容：

   * [AEM安装目录]\crx-repository\temp
   * [AEM安装目录]\crx-repository\repository
   * [AEM安装目录]\crx-repository\launchpad

* 应用程序服务器临时目录。 默认位置为：

   * (Jboss)[AEM安装目录]\jboss\standalone\tmp
   * (Weblogic)\Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere)\Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(仅限JEE上的AEM Forms)** 全局文档存储(GDS)目录。默认位置为：

   * (JBoss)[appserver根]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic)[appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere)[appserver根]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(仅限JEE上的AEM Forms)** AEM Forms服务器日志和临时目录。默认位置为：

   * 服务器日志 — [AEM Forms安装目录]\Adobe\AEM forms\[app-server]\server\all\logs
   * Temp目录 — [AEM Forms安装目录]\temp

>[!NOTE]
>
>* 如果您对GDS和临时目录使用其他位置，请在`https://'[server]:[port]'/adminui`处打开AdminUI，导航至&#x200B;**主页>设置>核心系统设置>核心配置**&#x200B;以确认使用的位置。

* 如果AEM Forms服务器在排除建议的目录后执行速度缓慢，则也排除Java可执行文件(java.exe)。


