---
title: Proxy伺服器工具(proxy.jar)
seo-title: Proxy Server Tool (proxy.jar)
description: 瞭解AEM中的Proxy伺服器工具。
seo-description: Learn about the Proxy Server Tool in AEM.
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
source-wordcount: '1161'
ht-degree: 0%

---

# Proxy伺服器工具(proxy.jar){#proxy-server-tool-proxy-jar}

Proxy伺服器會作為中繼伺服器，在使用者端和伺服器之間轉送請求。 Proxy伺服器會追蹤所有使用者端 — 伺服器互動，並輸出整個TCP通訊的記錄。 這可讓您監控確切的狀況，而不需要存取主要伺服器。

您可以在適當的安裝資料夾中找到Proxy伺服器：

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

您可以使用Proxy伺服器來監視所有使用者端 — 伺服器互動，無論基礎通訊協定為何。 例如，您可以監視下列通訊協定：

* 網頁的HTTP
* 用於安全網頁的HTTPS
* 電子郵件訊息的SMTP
* 用於使用者管理的LDAP

例如，您可以在透過TCP/IP網路通訊的任意兩個應用程式(例如網頁瀏覽器和AEM)之間定位Proxy伺服器。 這可讓您監控要求AEM頁面時的確切作業。

## 啟動Proxy伺服器工具 {#starting-the-proxy-server-tool}

此工具可在AEM安裝的/opt/helpers資料夾中找到。 若要啟動它，請鍵入：

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### 选项 {#options}

* **q （安靜模式）** 不要將請求寫入主控台視窗。 如果您不想減慢連線的速度，或是將輸出記錄到檔案中（請參閱 — logfile選項），請使用此選項。
* **b （二進位模式）** 如果您要在流量中尋找特定的位元組組合，請啟用二進位模式。 然後，輸出將包含十六進位和字元輸出。
* **t （時間戳記記錄專案）** 新增時間戳記至每個記錄輸出。 時間戳記以秒為單位，因此可能不適合檢查單一請求。 如果您使用Proxy伺服器的時間較長，可使用它來找出特定時間發生的事件。
* **logfile &lt;filename> （寫入記錄檔）** 將使用者端 — 伺服器交談寫入記錄檔。 此引數也可在安靜模式下運作。
* **i &lt;numindentions> （新增縮排）** 每個使用中的連線都會縮排，以提高可讀性。 預設值為16個層級。 （proxy.jar 1.16版的新增功能）。

## 使用Proxy伺服器工具 {#uses-of-the-proxy-server-tool}

下列案例說明可以使用Proxy伺服器工具的一些用途：

**檢查Cookie及其值**

以下記錄專案範例顯示自代理啟動後，使用者端在第6個開啟的連線中所傳送的所有Cookie及其值：

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**檢查標題及其值** 下列記錄專案範例顯示伺服器能夠建立保持連線且內容長度標頭已正確設定：

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**檢查保持連線是否有效**

**保持連線** 代表使用者端會重複使用與伺服器的連線，以傳輸多個檔案（頁面代碼、圖片、樣式表等）。 若不保持連線，使用者端必須為每個要求建立新的連線。

若要檢查保持連線是否有效：

1. 啟動Proxy伺服器
1. 請求頁面。

* 如果keep-alive正常運作，連線計數器絕不能超過5到10個連線。
* 如果keep-alive無法運作，連線計數器會快速增加。

**尋找遺失的請求**

如果您在複雜的伺服器設定中遺失要求（例如使用防火牆和Dispatcher），您可以使用Proxy伺服器來找出遺失要求的位置。 若使用防火牆：

1. 在防火牆之前啟動Proxy
1. 在防火牆之後啟動另一個Proxy
1. 使用這些來檢視請求進度。

**擱置中的請求**

如果您不時遇到擱置中的請求：

1. 啟動proxy.jar。
1. 等待或將存取記錄檔寫入檔案 — 每個專案都有時間戳記。
1. 當請求開始掛起時，您可以看到開啟了多少連線以及哪個請求造成了問題。

## 記錄訊息的格式 {#the-format-of-log-messages}

proxy.jar產生的記錄專案都具有下列格式：

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例如，對網頁的要求可能如下所示：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C表示此專案來自使用者端（這是對網頁的請求）
* 0是連線號碼（連線計數器從0開始）
* 顯#00000位元組資料流中的位移。 這是第一個專案，所以位移為0。
* [GET &lt;?>] 是請求的內容，例如其中一個HTTP標頭(url)。

當連線關閉時，會記錄下列資訊：

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這會顯示第6個連線中，使用者端與伺服器之間以平均速度傳遞的位元組數。

## 記錄輸出範例 {#an-example-of-log-output}

我們將檢閱簡單範本，依請求產生下列程式碼：

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

如果AEM在localhost：4303上執行，請依照下列方式啟動Proxy伺服器：

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

您可以存取伺服器(`localhost:4303`)，但如果您透過 `localhost:4444`，Proxy伺服器會記錄通訊。 開啟瀏覽器並存取使用上述範本建立的頁面。 之後，檢視記錄檔。

>[!NOTE]
>
>在proxy.jar 1.14版之前，一個連線的記錄專案不會同步，這表示一個使用者端/伺服器連線的記錄專案不需要以正確的順序進行。 較新版本(>=1.14)的Proxy伺服器沒有此問題。

啟動時，會將下列資訊寫入記錄檔：

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

下列標頭欄位會列在第一個連線(0)的開頭，此連線要求主要HTML頁面：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

使用者端要求保持連線，讓伺服器可以透過相同的連線傳送多個檔案：

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

Proxy伺服器是驗證Cookie是否設定正確的理想工具。 在這裡，我們看到：

* AEM產生的cq3session cookie
* CFC產生的顯示模式切換器Cookie
* 名為JSESSIONID的Cookie；若未使用&lt;%@頁面工作階段=&quot;false&quot; %>明確關閉，則會由JSP自動建立：

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

伺服器將在要求後關閉連線0。 無法保持連線，因為請求有問號。 這表示伺服器無法傳回快取版本，因此無法判斷此時保持連線所需的內容長度。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

在此，伺服器會在連線0上開始傳送HTML代碼：

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

連線0會在提供HTML檔案後立即關閉：

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

現在，輸出會從連線1開始，而連線1會下載HTML程式碼中包含的影像：

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

同樣地，使用者端要求保持連線：

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

對於連線1，伺服器可以提供保持連線，因為影像是靜態的，因此內容長度是已知的。

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

伺服器會傳回連線1上的影像內容長度：

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

現在已建立內容長度，伺服器會在連線1上傳送影像資料：

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

達到保持連線逾時後，連線1也會關閉：

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上述範例相對簡單，因為這兩個連線是按順序發生的：

* 首先，伺服器傳回HTML碼
* 然後瀏覽器要求影像並開啟新連線

實際上，頁面可能會產生許多對影像、樣式表、JavaScript檔案等的平行請求。 這表示記錄檔中有重疊的平行開啟連線專案。 在這種情況下，我們建議使用選項 — i來改善可讀性。
