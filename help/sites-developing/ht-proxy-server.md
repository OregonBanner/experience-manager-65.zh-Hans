---
title: 如何使用Proxy伺服器工具
seo-title: How to use the Proxy Server Tool
description: Proxy伺服器會作為中繼伺服器，在使用者端和伺服器之間轉送請求
seo-description: The proxy server acts as an intermediate server that relays requests between a client and a server
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
exl-id: 7222a0c3-cdb9-4c73-9d53-26f00792e439
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# 如何使用Proxy伺服器工具{#how-to-use-the-proxy-server-tool}

Proxy伺服器會作為中繼伺服器，在使用者端和伺服器之間轉送請求。 Proxy伺服器會追蹤所有使用者端 — 伺服器互動，並輸出整個TCP通訊的記錄。 這可讓您監控確切的狀況，而不需要存取主要伺服器。

您可以在AEM安裝中找到代理伺服器，網址為：

`crx-quickstart/opt/helpers/proxy-2.1.jar`

您可以使用Proxy伺服器來監視所有使用者端 — 伺服器互動，無論基礎通訊協定為何。 例如，您可以監視下列通訊協定：

* 網頁的HTTP
* 用於安全網頁的HTTPS
* 電子郵件訊息的SMTP
* 用於使用者管理的LDAP

例如，您可以在透過TCP/IP網路通訊的任意兩個應用程式(例如網頁瀏覽器和AEM)之間定位Proxy伺服器。 這可讓您監控當您請求CQ頁面時的確切情形。

## 啟動Proxy伺服器工具 {#starting-the-proxy-server-tool}

在命令列上啟動伺服器：

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**参数**

`<host>`

這是您要連線的CRX執行個體的主機位址。 如果執行個體位於您的本機電腦上，則這將會是 `localhost`.

`<remoteport>`

這是目標CRX執行個體的主機連線埠。 例如，新安裝的AEM安裝的預設值為 **`4502`** 而新安裝的AEM編寫執行個體的預設值為 `4502`.

`<localport>`

這是您本機電腦上要連線的連線埠，以透過Proxy存取CRX執行個體。

**选项**

`-q` （安靜模式）

不要將輸出寫入主控台視窗。 如果您不想減慢連線的速度，或是將輸出記錄到檔案中（請參閱 — logfile選項），請使用此選項。

`-b`（二進位模式）

如果您要在流量中尋找特定的位元組組合，請啟用二進位模式。 然後，輸出將包含十六進位和字元輸出。

`-t` （時間戳記記錄專案）

新增時間戳記至每個記錄輸出。 時間戳記以秒為單位，因此可能不適合檢查單一請求。 如果您使用Proxy伺服器的時間較長，可使用它來找出特定時間發生的事件。

`-logfile <filename>`（寫入記錄檔）

將使用者端 — 伺服器交談寫入記錄檔。 此引數也會在安靜模式下運作。

**`-i <numIndentions>`**（新增縮排）

每個使用中的連線都會縮排，以提高可讀性。 預設值為16個層級。 此功能的推出背景為 `proxy.jar version 1.16`.

### 記錄格式 {#log-format}

proxy-2.1.jar產生的記錄專案都具有下列格式：

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例如，對網頁的要求可能如下所示：

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C表示此專案來自使用者端（這是對網頁的請求）
* 0是連線號碼（連線計數器從0開始）
* 顯#00000位元組資料流中的位移。 這是第一個專案，所以位移為0。
* `[GET <?>]` 是請求的內容，例如其中一個HTTP標頭(url)。

當連線關閉時，會記錄下列資訊：

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這會顯示使用者端( `C`)和伺服器( `S`)和平均速度進行。

**記錄輸出範例**

例如，考慮請求時產生以下程式碼的頁面：

### 示例 {#example}

例如，請考量位於存放庫中的非常簡單的html檔案

`/content/test.html`

與位於下列位置的影像檔案並排

`/content/test.jpg`

的內容 `test.html` 為：

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

假設AEM執行個體執行於 `localhost:4502` 我們啟動Proxy的方式如下：

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

CQ/CRX例項現在可以透過Proxy進行存取，網址為 `localhost:4444` 而且所有透過此連線埠的通訊都會記錄到 `test.log`.

如果我們現在觀看Proxy的輸出，就會看到瀏覽器與AEM執行個體之間的互動。

啟動時，Proxy輸出以下內容：

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

然後，我們開啟瀏覽器並存取測試頁面：

`http://localhost:4444/content/test.html`

而且我們看到瀏覽器讓了 `GET` 頁面的請求：

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

AEM執行個體會以檔案內容回應 `test.html`：

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

### Proxy伺服器的使用 {#uses-of-the-proxy-server}

下列案例說明可以使用Proxy伺服器的幾個用途：

**檢查Cookie及其值**

以下記錄專案範例顯示自代理啟動後，使用者端在第六個開啟的連線上傳送的所有Cookie及其值：

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**檢查標題及其值**

下列記錄專案範例顯示伺服器能夠建立保持連線且內容長度標頭已正確設定：

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**檢查保持連線是否有效**

Keep-alive是HTTP的一項功能，可讓使用者端重複使用伺服器的TCP連線，以提出多個要求（頁面代碼、圖片、樣式表等）。 若不保持連線，使用者端必須為每個要求建立新的連線。

若要檢查保持連線是否有效：

* 啟動Proxy伺服器
* 請求頁面。
* 如果keep-alive正常運作，連線計數器絕不能超過5到10個連線。
* 如果keep-alive無法運作，連線計數器會快速增加。

**尋找遺失的請求**

如果您在複雜的伺服器設定中遺失要求（例如使用防火牆和Dispatcher），您可以使用Proxy伺服器來找出遺失要求的位置。 若使用防火牆：

* 在防火牆之前啟動Proxy
* 在防火牆之後啟動另一個Proxy
* 使用這些來檢視請求進度。

**擱置中的請求**

如果您不時遇到擱置中的請求：

* 啟動Proxy。
* 等待或將存取記錄檔寫入檔案，每個專案都有時間戳記。
* 當請求開始掛起時，您可以看到開啟了多少連線以及哪個請求造成了問題。
