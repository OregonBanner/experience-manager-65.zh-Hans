---
title: 如何使用Proxy Server Tool
seo-title: 如何使用Proxy Server Tool
description: 代理服务器充当在客户机和服务器之间中继请求的中间服务器
seo-description: 代理服务器充当在客户机和服务器之间中继请求的中间服务器
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 如何使用Proxy Server Tool{#how-to-use-the-proxy-server-tool}

代理服务器充当在客户机和服务器之间中继请求的中间服务器。 代理服务器跟踪所有客户端与服务器的交互，并输出整个TCP通信的日志。 这样，您就可以准确监控正在进行的操作，而无需访问主服务器。

您可以在AEM安装中找到代理服务器，网址为：

`crx-quickstart/opt/helpers/proxy-2.1.jar`

您可以使用代理服务器监视所有客户端与服务器的交互，而不管基础通信协议如何。 例如，您可以监视以下协议：

* 网页HTTP
* 安全网页的HTTPS
* 电子邮件的SMTP
* 用于用户管理的LDAP

例如，您可以在通过TCP/IP网络进行通信的任何两个应用程序之间放置代理服务器；例如Web浏览器和AEM。 这样，您就可以准确地监视请求CQ页面时发生的情况。

## 启动Proxy Server Tool {#starting-the-proxy-server-tool}

在命令行上启动服务器：

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**参数**

`<host>`

这是要连接到的CRX实例的主机地址。 如果实例位于本地计算机上，则此实例将为 `localhost`。

`<remoteport>`

这是目标CRX实例的主机端口。 例如，新安装的AEM安装的默认值是， **`4502`** 新安装的AEM作者实例的默认值是 `4502`。

`<localport>`

这是您本地计算机上要通过代理连接以访问CRX实例的端口。

**选项**

`-q` （安静模式）

不将输出写入控制台窗口。 如果不想降低连接速度，或者将输出记录到文件（请参阅-logfile选项），请使用此选项。

`-b`（二进制模式）

如果要查找流量中的特定字节组合，请启用二进制模式。 然后，输出将包含十六进制和字符输出。

`-t` （时间戳日志条目）

为每个日志输出添加时间戳。 时间戳以秒为单位，因此可能不适合检查单个请求。 如果您在较长的时间段内使用代理服务器，则使用它查找在特定时间发生的事件。

`-logfile <filename>`（写入日志文件）

将客户端——服务器对话写入日志文件。 此参数也在安静模式下工作。

**`-i <numIndentions>`**（添加缩进）

每个活动连接都进行缩进，以提高可读性。 默认为16级。 此功能是随附的 `proxy.jar version 1.16`。

### 日志格式 {#log-format}

proxy-2.1.jar生成的日志条目均具有以下格式：

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例如，网页请求可能如下所示：

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C表示此条目来自客户端（它是对网页的请求）
* 0是连接号（连接计数器从0开始）
* &#x200B;# 00000字节流中的偏移量。 这是第一个条目，因此偏移量为0。
* `[GET <?>]` 是请求的内容，在示例中，HTTP头(url)之一。

当连接关闭时，将记录以下信息：

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

这显示第6个连接上的客户端( `C`)与服务器( `S`)之间以平均速度传递的字节数。

**日志输出示例**

例如，请考虑在请求时生成以下代码的页面：

### 示例 {#example}

例如，请考虑位于

`/content/test.html`

位于

`/content/test.jpg`

内容 `test.html` 是：

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

假定AEM实例在上运行， `localhost:4502` 我们将启动如下代理：

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

CQ/CRX实例现在可通过位于的代理访问， `localhost:4444` 并且通过此端口的所有通信都将记录到 `test.log`。

如果我们现在观察代理的输出，我们将看到浏览器与AEM实例之间的交互。

启动时，代理输出以下内容：

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

然后，我们打开浏览器并访问测试页：

`http://localhost:4444/content/test.html`

我们看到浏览器对页 `GET` 面发出请求：

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

AEM实例会对文件内容做出响应 `test.html`:

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### 代理服务器的使用 {#uses-of-the-proxy-server}

以下场景说明了可以使用代理服务器的几个用途：

**检查Cookie及其值**

以下日志条目示例显示自代理启动以来在打开的第六个连接上客户端发送的所有cookie及其值：

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**检查标题及其值**

以下日志条目示例显示服务器能够建立保持活动连接，并且内容长度标题设置正确：

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**检查Keep-Alive是否有效**

“保持活动”是HTTP的一个功能，它允许客户端重新使用与服务器的TCP连接来发出多个请求（对于页面代码、图片、样式表等）。 如果不保持活动状态，客户端必须为每个请求建立新连接。

要检查“保持活动”是否有效，请执行以下操作：

* 启动代理服务器。
* 请求页面。
* 如果保持活动，则连接计数器不应超过5到10个连接。
* 如果“保持活动”不工作，则连接计数器会迅速增加。

**查找丢失的请求**

如果在复杂的服务器设置（例如防火墙和调度程序）中丢失请求，则可以使用代理服务器查找丢失请求的位置。 如果是防火墙：

* 在防火墙前启动代理
* 在防火墙后启动另一个代理
* 使用这些组件可了解请求的进度。

**请求挂起**

如果您经常遇到挂起请求：

* 启动代理。
* 等待访问日志或将其写入一个文件中，每个条目都有时间戳。
* 当请求开始挂起时，您可以看到打开的连接数以及导致问题的请求数。

