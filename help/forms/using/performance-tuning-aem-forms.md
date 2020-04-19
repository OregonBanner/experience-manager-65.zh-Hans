---
title: AEM Forms服务器的性能调整
seo-title: AEM Forms服务器的性能调整
description: 为了使AEM Forms达到最佳性能，您可以微调缓存设置和JVM参数。 此外，使用Web服务器可以增强AEM Forms部署的性能。
seo-description: 为了使AEM Forms达到最佳性能，您可以微调缓存设置和JVM参数。 此外，使用Web服务器可以增强AEM Forms部署的性能。
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# AEM Forms服务器的性能调整{#performance-tuning-of-aem-forms-server}

本文讨论您可以实施的战略和最佳实践，以减少瓶颈并优化AEM Forms部署的性能。

## 缓存设置 {#cache-settings}

您可以使用AEM Web配置控制台中的 **Mobile Forms Configurations** （移动表单配置）组件，配置和控制AEM Forms的缓存策略：

* （OSGi上的AEM Forms） `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

缓存的可用选项如下：

* **无**:强制不缓存任何对象。 实际上，这将会降低性能，并由于缺少缓存而要求高内存可用性。
* **保守派**:指示仅缓存在呈现表单之前生成的那些中间伪像，如包含内联片段和图像的模板。
* **咄咄逼人**:强制缓存几乎可缓存的所有内容，包括呈现的HTML内容，以及保守级别的所有对象。 它可产生最佳性能，但也会消耗更多内存来存储缓存的伪像。 激进的缓存策略意味着在缓存渲染的内容时，您在渲染表单时将获得持续的时间性能。

AEM Forms的默认缓存设置可能不足以实现最佳性能。 因此，建议使用以下设置：

* **缓存策略**:咄咄逼人
* **缓存大小** （根据表单数量）:根据需要
* **最大对象大小**:根据需要

![移动表单配置](assets/snap.png)

>[!NOTE]
>
>如果使用AEM Dispatcher缓存自适应表单，它还会缓存自适应表单，该表单包含具有预填充数据的表单。 如果此类表单从AEM Dispatcher缓存中提供，则可能导致向用户提供预填或过时的数据。 因此，请使用AEM Dispatcher缓存不使用预填充数据的自适应表单。 此外，调度程序缓存不会使缓存的片段自动失效。 因此，请勿使用它缓存表单片段。 对于此类表单和片段，请使用自适 [应表单缓存](../../forms/using/configure-adaptive-forms-cache.md)。

## JVM参数 {#jvm-parameters}

为获得最佳性能，建议使用以下JVM `init` 参数来配置 `Java heap` 和 `PermGen`。

```java
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>建议的设置适用于Windows 2008 R2 8 Core和Oracle HotSpot 1.7（64位）JDK，并且应根据系统配置进行放大或缩小。

## 使用Web服务器 {#using-a-web-server}

自适应表单和HTML5表单以HTML5格式呈现。 根据表单大小和表单中的图像等因素，生成的输出可能很大。 为了优化数据传输，建议的方法是使用从中提供请求的Web服务器压缩HTML响应。 此方法可减小响应大小、网络流量以及在服务器和客户端计算机之间流化数据所需的时间。

例如，执行以下步骤以使用JBoss对Apache Web Server 2.0 32位启用压缩：

>[!NOTE]
>
>以下说明不适用于除Apache Web Server 2.0 32位服务器之外的任何服务器。 有关特定于任何其他服务器的步骤，请参阅相应的产品文档。

以下步骤演示了使用Apache Web Server启用压缩所需的更改

**获取适用于您的操作系统的Apache Web服务器软件**

* Windows:从Apache HTTP Server项目站点下载Apache Web服务器。
* Solaris 64位：从Sunfreeware for Solaris网站下载Apache Web服务器。
* Linux:apache Web服务器预装在Linux系统上。

Apache可以使用HTTP协议与CRX通信。 这些配置用于使用HTTP进行优化。

1. 在文件中取消以下模块配置 `APACHE_HOME/conf/httpd.conf` 的注释。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >对于Linux，默认 `APACHE_HOME` 值为 `/etc/httpd/`。

1. 在crx的端口4502上配置代理。
在配置文件中添加 `APACHE_HOME/conf/httpd.conf` 以下配置。

   ```java
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 启用压缩。 在配置文件中添加 `APACHE_HOME/conf/httpd.conf` 以下配置。

   **对于HTML5表单**

   ```java
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

   ```java
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

   要访问crx服务器，请使 `https://'server':80`用，其 `server` 中是运行Apache服务器的服务器的名称。

## 在运行AEM Forms的服务器上使用防病毒程序 {#using-an-antivirus-on-server-running-aem-forms}

在运行防病毒软件的服务器上，您可能会遇到性能降低的问题。 始终打开防病毒（访问扫描）软件可扫描系统的所有文件。 它可能会降低服务器速度并影响AEM Forms的性能。

要提高性能，您可以引导防病毒软件从始终处于（访问）扫描状态中排除以下AEM Forms文件和文件夹：

* AEM安装目录。 如果无法排除完整目录，请排除以下内容：

   * [AEM安装目录]\crx-repository\temp
   * [AEM安装目录]\crx-repository\repository
   * [AEM安装目录]\crx-repository\launchpad

* 应用程序服务器临时目录。 默认位置为：

   * (Jboss) [AEM安装目录]\jboss\standalone\tmp
   * (Weblogic)\Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere)\项目Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **（仅限JEE上的AEM Forms）** “全局文档存储”(GDS)目录。 默认位置为：

   * (JBoss) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **（仅限JEE上的AEM Forms）** AEM Forms服务器日志和临时目录。 默认位置为：

   * 服务器日志- [AEM Forms安装目录]\Adobe\AEM forms\[app-server]\server\all\logs
   * 临时目录- [AEM Forms安装目录]\temp

>[!NOTE]
>
>* 如果您对GDS和临时目录使用其他位置，请在打开AdminUI `https://'[server]:[port]'/adminui`，导航到“ **Home”（主页）> “Settings”（设置）> “Core System Settings”（核心系统设置）> “Core Configurations** ”（核心配置），以确认使用的位置。

* 如果AEM Forms服务器在排除建议的目录后运行缓慢，则也排除Java可执行文件(java.exe)。



