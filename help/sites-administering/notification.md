---
title: 設定電子郵件通知
seo-title: Configuring Email Notification
description: 瞭解如何在AEM中設定電子郵件通知。
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: 144fbe2d0efe20d848e9556f8d652a403d1835b2
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 12%

---

# 設定電子郵件通知{#configuring-email-notification}

AEM傳送電子郵件通知給使用者：

* 已訂閱頁面事件，例如修改或復寫。 此 [通知收件匣](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 一節說明如何訂閱這類事件。

* 已訂閱論壇事件。
* 必須在工作流程中執行步驟。 此 [參與者步驟](/help/sites-developing/workflows-step-ref.md#participant-step) 一節說明如何在工作流程中觸發電子郵件通知。

先決條件：

* 使用者需要在其設定檔中定義有效的電子郵件地址。
* 此 **Day CQ郵件服務** 需要正確設定。

當使用者收到通知時，他將會收到在其設定檔中定義的語言電子郵件。 每種語言都有各自的範本可供自訂。 可以為新語言新增新的電子郵件範本。

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

## 設定郵件服務 {#configuring-the-mail-service}

為了讓AEM能夠傳送電子郵件， **Day CQ郵件服務** 需要正確設定。 您可以在Web主控台中檢視設定。 使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

下列限制適用：

* 此 **SMTP伺服器連線埠** 「 」必須為25或更高。

* 此 **smtp伺服器主機名稱** 不得為空白。
* 此 **「寄件者」地址** 不得為空白。

為協助您對問題進行偵錯 **Day CQ郵件服務**，您可以檢視服務的記錄：

`com.day.cq.mailer.DefaultMailService`

在Web主控台中，設定如下所示：

![chlimage_1-276](assets/chlimage_1-276.png)

## 設定電子郵件通知通道 {#configuring-the-email-notification-channel}

當您訂閱頁面或論壇事件通知時，寄件者電子郵件地址會設為 `no-reply@acme.com` 根據預設。 您可以透過設定 **通知電子郵件頻道** Web控制檯中的服務。

若要設定寄件者電子郵件地址，請新增 `sling:OsgiConfig` 節點至存放庫。 使用以下程式，透過CRXDE Lite直接新增節點：

1. 在CRXDE Lite中，新增名為的資料夾 `config` 位於應用程式資料夾下方。
1. 在設定資料夾中，新增名為的節點：

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 型別 `sling:OsgiConfig`

1. 新增 `String` 屬性至名為的節點 `email.from`. 對於值，指定您要使用的電子郵件地址。

1. 按一下 **全部儲存**.

使用以下程式來定義內容套件來源資料夾中的節點：

1. 在您的 `jcr_root/apps/*app_name*/config folder`，建立名為的檔案 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 新增下列XML來代表節點：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 取代 `email.from` 屬性( `name@server.com`)填入您的電子郵件地址。

1. 保存文件。

## 設定工作流程電子郵件通知服務 {#configuring-the-workflow-email-notification-service}

當您收到工作流程電子郵件通知時，寄件者電子郵件地址和主機URL首碼都會設為預設值。 您可以透過設定 **Day CQ工作流程電子郵件通知服務** 在Web主控台中。 若您這麼做，建議您將變更保留在存放庫中。

在Web主控台中，預設設定如下所示：

![chlimage_1-277](assets/chlimage_1-277.png)

### 頁面通知的電子郵件範本 {#email-templates-for-page-notification}

頁面通知的電子郵件範本位於下方：

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

預設英文範本( `en.txt`)的定義如下：

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自訂頁面通知的電子郵件範本 {#customizing-email-templates-for-page-notification}

若要自訂頁面通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 視需要修改檔案。
1. 保存更改。

範本的格式必須如下：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

位置 &lt;text_x> 可以是靜態文字和動態字串變數的組合。 下列變數可用於頁面通知的電子郵件範本中：

* `${time}`，即事件日期和時間。

* `${userFullName}`，觸發事件的使用者全名。

* `${userId}`，觸發事件的使用者的ID。
* `${modifications}`，說明頁面事件的型別和格式的頁面路徑：

   &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

   例如：

   PageModified => /content/geometrixx/en/products

### 工作流程通知的電子郵件範本 {#email-templates-for-workflow-notification}

工作流程通知的電子郵件範本（英文）位於：

`/libs/settings/workflow/notification/email/default/en.txt`

其定義如下：

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自訂工作流程通知的電子郵件範本 {#customizing-email-templates-for-workflow-notification}

若要自訂工作流程事件通知的英文電子郵件範本：

1. 在CRXDE中，開啟檔案：

   `/libs/settings/workflow/notification/email/default/en.txt`

1. 視需要修改檔案。
1. 保存更改。

範本的格式必須如下：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>位置 `<text_x>` 可以是靜態文字和動態字串變數的組合。 每行 `<text_x>` 專案必須以反斜線( `\`)，但最後一個例項除外，因為缺少反斜線代表 `<text_x>` 字串變數。
>
>有關範本格式的更多資訊，請參閱 [Properties.load()的javadocs](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 方法。

方法 `${payload.path.open}` 顯示工作專案裝載的路徑。 例如，若為Sites中的頁面，則 `payload.path.open` 會類似於 `/bin/wcmcommand?cmd=open&path=…`.；這沒有伺服器名稱，因此範本會在前面加上 `${host.prefix}`.

下列變數可用於電子郵件範本中：

* `${event.EventType}`，事件型別
* `${event.TimeStamp}`，事件的日期和時間
* `${event.User}`，觸發事件的使用者
* `${initiator.home}`，啟動器節點路徑

* `${initiator.name}`，啟動器名稱

* `${initiator.email}`，發起人的電子郵件地址
* `${item.id}`，工作專案的id
* `${item.node.id}`，此工作專案相關之工作流程模型中的節點id
* `${item.node.title}`，工作專案的標題
* `${participant.email}`，參與者的電子郵件地址
* `${participant.name}`，參與者名稱
* `${participant.familyName}`，參與者的姓氏
* `${participant.id}`，參與者的id
* `${participant.language}`，參與者語言
* `${instance.id}`，工作流程id
* `${instance.state}`，工作流程狀態
* `${model.title}`，工作流程模型的標題
* `${model.id}`，工作流程模型的id

* `${model.version}`，工作流程模型的版本
* `${payload.data}`，裝載

* `${payload.type}`，裝載型別
* `${payload.path}`，裝載的路徑
* `${host.prefix}`，主機首碼，例如： http://localhost:4502

### 新增新語言的電子郵件範本 {#adding-an-email-template-for-a-new-language}

若要新增新語言的範本：

1. 在CRXDE中，新增檔案 `<language-code>.txt` 下：

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` ：用於頁面通知
   * `/libs/settings/workflow/notification/email/default` ：用於工作流程通知

1. 將檔案調整成語言。
1. 保存更改。

>[!NOTE]
>
>此 `<language-code>` 用作電子郵件範本的檔案名稱時，必須使用AEM可辨識的雙字母小寫語言代碼。 對於語言代碼，AEM依賴ISO-639-1。

## 設定AEM Assets電子郵件通知 {#assetsconfig}

共用或取消共用AEM Assets中的集合時，使用者可以收到來自AEM的電子郵件通知。 若要設定電子郵件通知，請遵循下列步驟。

1. 設定電子郵件服務，如上所述 [設定郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service).
1. 以管理员身份登录 AEM。按一下 **工具** >  **作業** >  **網頁主控台** 以開啟Web主控台組態。
1. 編輯 **Day CQ DAM資源收集Servlet**. 選取 **傳送電子郵件**. 单击“**保存**”。

## 設定OAuth {#setting-up-oauth}

AEM為其整合的郵件程式服務提供OAuth2支援，以允許組織遵守安全電子郵件要求。

您可以為多個電子郵件提供者設定OAuth，如下所述。

>[!NOTE]
>
>此程式是發佈執行個體的範例。 如果您想在作者執行個體上啟用電子郵件通知，您需要對作者執行相同的步驟。

### Gmail {#gmail}

1. 建立您的專案於 `https://console.developers.google.com/projectcreate`
1. 選取您的專案，然後前往 **API和服務** - **儀表板 — 認證**
1. 根據您的要求設定OAuth同意畫面
1. 在隨後的「更新畫面」中，新增這兩個範圍：
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 新增範圍後，請返回 **認證** 在左側功能表中，然後前往 **建立認證** - **OAuth使用者端ID** - **案頭應用程式**
1. 將會開啟一個包含使用者端ID和使用者端密碼的新視窗。
1. 儲存這些認證。

**AEM Side設定**

>[!NOTE]
>
>Adobe Managed Service客戶可與客戶服務工程師合作，對生產環境進行這些變更。

首先，設定郵件服務：

1. 開啟AEM Web Console，方法是前往 `http://serveraddress:serverport/system/console/configMgr`
1. 尋找，然後按一下 **Day CQ郵件服務**
1. 新增下列設定：
   * SMTP 服务器主机名: `smtp.gmail.com`
   * SMTP伺服器連線埠： `25` 或 `587`，視需求而定
   * 勾選勾選方塊 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * Check **OAuth流程** 並按一下 **儲存**.

接下來，請依照下列程式設定您的SMTP OAuth提供者：

1. 開啟AEM Web Console，方法是前往 `http://serveraddress:serverport/system/console/configMgr`
1. 尋找，然後按一下 **CQ郵件程式SMTP OAuth2提供者**
1. 請依照以下說明填寫必要資訊：
   * 授權URL： `https://accounts.google.com/o/oauth2/auth`
   * 權杖URL： `https://accounts.google.com/o/oauth2/token`
   * 範圍： `https://www.googleapis.com/auth/gmail.send` 和 `https://mail.google.com/`. 您可以按下 **+** 按鈕來設定每個已設定範圍的右側。
   * 使用者端ID和使用者端密碼：依照上段所述，以您擷取的值來設定這些欄位。
   * 刷新令牌 URL: `https://accounts.google.com/o/oauth2/token`
   * 重新整理Token到期日：永不
1. 单击“**保存**”。

<!-- clarify refresh token expiry, currrently not present in the UI -->

設定完成後，設定應如下所示：

![oauth smtp提供者](assets/oauth-smtpprov2.png)

現在啟動OAuth元件。 您可以执行以下操作来实现此目标：

1. 請造訪此URL前往「元件主控台」： `http://serveraddress:serverport/system/console/components`
1. 尋找下列元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「播放」圖示

   ![元件](assets/oauth-components-play.png)

最後，透過以下方式確認設定：

1. 前往發佈執行個體的位址，並以管理員身分登入。
1. 在瀏覽器中開啟新標籤，然後前往 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 這會將您重新導向至SMTP提供者的頁面，在此案例中為Gmail。
1. 登入並同意授予必要許可權
1. 在同意後，權杖將會儲存在存放庫中。 您可以在下列位置存取它： `accessToken` 直接存取發佈執行個體上的此URL： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 對每個發佈執行個體重複上述步驟

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. 转至 [https://portal.azure.com/](https://portal.azure.com/) 并登录。
1. 在搜索栏中搜索 **Azure Active Directory**，并单击搜索结果。或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击&#x200B;**应用程序注册** - **新注册**

   ![](assets/oauth-outlook1.png)

1. 根据您的要求填写信息，然后单击&#x200B;**注册**
1. 转至新创建的应用程序，并选择 **API 权限**
1. 转至&#x200B;**添加权限** - **图表权限** - **委派权限**
1. 为应用程序选择以下权限，然后单击&#x200B;**添加权限**：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 前往 **驗證** - **新增平台** - **Web**，以及 **重新導向Url** 區段，新增下列URL以重新導向OAuth程式碼，然後按下 **設定**：
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 對每個發佈執行個體重複上述步驟
1. 根據您的需求進行設定
1. 接下来，转至&#x200B;**证书和密码**，单击&#x200B;**新建客户端密码**，然后执行屏幕上显示的步骤来创建密码。请务必记下此密码供以后使用
1. 按左窗格中的&#x200B;**概述**，复制&#x200B;**应用程序（客户端）ID** 和&#x200B;**目录（租户）ID** 的值供以后使用

回顧一下，您需要以下資訊為AEM端的郵件程式服務設定OAuth2：

* 将使用租户 ID 构建的身份验证 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 将使用租户 ID 构建的令牌 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 将使用租户 ID 构建的刷新 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 客户端 ID
* 客户端密码

**AEM Side設定**

接下來，將您的OAuth2設定與AEM整合：

1. 瀏覽至您本機執行個體的Web主控台 `http://serveraddress:serverport/system/console/configMgr`
1. 尋找並按一下 **Day CQ郵件服務**
1. 新增下列設定：
   * SMTP 服务器主机名: `smtp.office365.com`
   * SMTP使用者：您的電子郵件格式使用者名稱
   * 「寄件者」地址：郵件程式所傳送訊息的「寄件者：」欄位中使用的電子郵件地址
   * SMTP伺服器連線埠： `25` 或 `587` 視需求而定
   * 勾選勾選方塊 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * Check **OAuth流程** 並按一下 **儲存**.
1. 尋找，然後按一下 **CQ郵件程式SMTP OAuth2提供者**
1. 請依照以下說明填寫必要資訊：
   * 填寫「授權URL」、「權杖URL」和「重新整理權杖URL」，方法為依照下列說明建構它們： [此程式的結尾](#microsoft-outlook)
   * 使用者端ID和使用者端密碼：使用上述擷取的值來設定這些欄位。
   * 将以下范围添加到配置：
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode重新導向Url： `http://localhost:4503/services/mailer/oauth2/token`
   * 重新整理記號URL：這應該與上述記號URL的值相同
1. 单击“**保存**”。

設定完成後，設定應如下所示：

![](assets/oauth-outlook-smptconfig.png)

現在啟動OAuth元件。 您可以执行以下操作来实现此目标：

1. 請造訪此URL前往「元件主控台」： `http://serveraddress:serverport/system/console/components`
1. 尋找下列元件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按元件左側的「播放」圖示

![components2](assets/oauth-components-play.png)

最後，透過以下方式確認設定：

1. 前往發佈執行個體的位址，並以管理員身分登入。
1. 在瀏覽器中開啟新標籤，然後前往 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 這會將您重新導向至SMTP提供者的頁面，在此例中是Outlook。
1. 登入並同意授予必要許可權
1. 在同意後，權杖將會儲存在存放庫中。 您可以在下列位置存取它： `accessToken` 直接存取發佈執行個體上的此URL： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
