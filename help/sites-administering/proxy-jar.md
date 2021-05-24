---
title: 代理服务器工具(proxy.jar)
seo-title: 代理服务器工具(proxy.jar)
description: 了解AEM中的代理服务器工具。
seo-description: 了解AEM中的代理服务器工具。
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# 代理服务器工具(proxy.jar){#proxy-server-tool-proxy-jar}

代理服务器充当在客户机和服务器之间中继请求的中间服务器。 代理服务器会跟踪所有客户端与服务器的交互，并输出整个TCP通信的日志。 这样，您就可以准确监控所发生的情况，而无需访问主服务器。

您可以在相应的安装文件夹中找到代理服务器：

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

您可以使用代理服务器来监视所有客户端与服务器的交互，而不考虑底层通信协议。 例如，您可以监视以下协议：

* 网页的HTTP
* 用于安全网页的HTTPS
* 电子邮件的SMTP
* 用于用户管理的LDAP

例如，可以在通过TCP/IP网络通信的任意两个应用程序之间放置代理服务器；例如，Web浏览器和AEM。 这允许您监视请求AEM页面时发生的确切情况。

## 启动代理服务器工具{#starting-the-proxy-server-tool}

该工具可在AEM安装的/opt/helpers文件夹中找到。 要启动该活动，请键入：

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### 选项 {#options}

* **q（静默模式）** 不将请求写入控制台窗口。如果您不想减慢连接速度，或者如果将输出记录到文件（请参阅 — logfile选项），请使用此选项。
* **b（二进制模式）** 如果要在流量中查找特定的字节组合，请启用二进制模式。然后，输出将包含十六进制和字符输出。
* **t（时间戳日志条目）** 向每个日志输出添加一个时间戳。时间戳以秒为单位，因此可能不适合检查单个请求。 如果您在较长的时间段内使用代理服务器，则可使用它查找在特定时间发生的事件。
* **日志 &lt;filename> 文件（写入日志文件）** 将客户端 — 服务器对话写入日志文件。此参数也可在安静模式下工作。
* **i(添 &lt;numindentions> 加缩进)** 为了更好的可读性，会缩进每个活动连接。默认为16级。 （proxy.jar版本1.16中的新增功能）。

## 代理服务器工具{#uses-of-the-proxy-server-tool}的使用

以下情景说明了可以使用代理服务器工具的一些目的：

**检查Cookie及其值**

以下日志条目示例显示自代理启动以来第6次打开连接时客户端发送的所有Cookie及其值：

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**检查标头及其值** 以下日志条目示例显示服务器能够建立保持活动连接，并且内容长度标头已正确设置：

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**检查“保持活动状态”是否有效**

**保留 —** 保留 — 保留意味着客户端重新使用与服务器的连接来传输多个文件（页面代码、图片、样式表等）。如果没有保持活动状态，客户必须为每个请求建立新连接。

要检查保持活动状态是否有效，请执行以下操作：

1. 启动代理服务器。
1. 请求页面。

* 如果保持活动状态正常工作，则连接计数器不得超过5到10个连接。
* 如果保持活动状态不起作用，则连接计数器会快速增加。

**查找丢失的请求**

如果在复杂的服务器设置（例如使用防火墙和调度程序）中丢失请求，则可以使用代理服务器查找请求丢失的位置。 如果有防火墙：

1. 在防火墙之前启动代理
1. 在防火墙后启动另一个代理
1. 使用这些参数可查看请求获得的响应深度。

**挂起请求**

如果您遇到不时挂起请求的情况：

1. 启动proxy.jar。
1. 等待或写入访问日志到文件中 — 每个条目都有时间戳。
1. 当请求开始挂起时，您可以看到有多少个连接处于打开状态，以及哪个请求会导致问题。

## 日志消息{#the-format-of-log-messages}的格式

proxy.jar生成的日志条目均具有以下格式：

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例如，网页请求可能如下所示：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C表示此条目来自客户端（它是对网页的请求）
* 0是连接号（连接计数器从0开始）
* # 00000字节流中的偏移。 这是第一个条目，因此偏移为0。
* [GET &lt;?>] 是请求的内容，在示例中为一个HTTP头(url)。

当连接关闭时，将记录以下信息：

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

这显示在第6个连接上以平均速度在客户端和服务器之间传递的字节数。

## 日志输出{#an-example-of-log-output}的示例

我们将审核一个简单的模板，该模板可根据要求生成以下代码：

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

如果AEM在localhost:4303上运行，请按如下方式启动代理服务器：

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

您无需代理服务器即可访问服务器(`localhost:4303`)，但如果您通过`localhost:4444`访问服务器，则代理服务器将记录通信。 打开浏览器并访问使用上述模板创建的页面。 之后，查看日志文件。

>[!NOTE]
>
>在proxy.jar版本1.14之前，一个连接的日志条目不会同步，这意味着一个客户端/服务器连接的日志条目不必按正确的顺序进行同步。 代理服务器的较新版本(>=1.14)不存在此问题。

启动时，会将以下信息写入日志：

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

在请求主HTML页的第一个连接(0)的开头处列出以下标头字段：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

客户端请求保持活动连接，以便服务器可以通过同一连接发送多个文件：

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

代理服务器是验证Cookie是否正确设置的好工具。 这里，我们看到：

* 由AEM生成的cq3session cookie
* 由CFC生成的show mode开关cookie
* 名为JSESSIONID的Cookie;如果未使用&lt;%@ page session=&quot;false&quot; %>显式关闭，则JSP会自动创建此会话：

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

服务器将在请求后关闭连接0。 无法保持活动状态，因为请求带有问号。 这意味着服务器无法返回缓存的版本，因此无法确定此时的内容长度，这是保持活动连接所需的内容长度。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

在此，服务器开始在连接0上发送HTML代码：

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

连接0在提供HTML文件后立即关闭：

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

现在，连接1的输出开始，连接1将下载HTML代码中包含的图像：

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

客户端再次请求保持活动连接：

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

对于连接1，服务器可以提供保持活动状态，因为图像是静态的，因此内容长度是已知的。

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

服务器返回连接1上图像的内容长度：

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

现在，内容长度已建立，服务器在连接1上发送图像数据：

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

达到保持活动超时后，连接1也会关闭：

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上例相对简单，因为两个连接按顺序发生：

* 首先，服务器返回HTML代码
* 然后，浏览器请求获取图像并打开新连接

实际上，页面可能会为图像、样式表、JavaScript文件等生成许多并行请求。 这意味着日志具有并行打开连接的重叠条目。 在这种情况下，我们建议使用选项 — i来提高可读性。
