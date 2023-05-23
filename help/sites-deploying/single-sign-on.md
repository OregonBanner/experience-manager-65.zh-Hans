---
title: 單一登入
seo-title: Single Sign On
description: 瞭解如何為AEM執行個體設定單一登入(SSO)。
seo-description: Learn how to configure Single Sign On (SSO) for an AEM instance.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: Configuring
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# 單一登入 {#single-sign-on}

單一登入(SSO)可讓使用者在提供一次驗證認證（例如使用者名稱和密碼）之後存取多個系統。 獨立的系統（稱為受信任的驗證者）會執行驗證並提供Experience Manager使用者認證。 Experience Manager會檢查並強制使用者的存取許可權（即決定允許使用者存取哪些資源）。

SSO驗證處理常式服務( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)會處理受信任的驗證器提供的驗證結果。 SSO驗證處理常式會依下列順序搜尋ssid （SSO識別碼）作為特殊屬性的值：

1. 請求標頭
1. Cookie
1. 要求引數

找到某個值後，就會完成搜尋並使用此值。

設定下列兩個服務來識別儲存ssid的屬性名稱：

* 登入模組。
* SSO驗證服務。

您必須為兩個服務指定相同的屬性名稱。 屬性包含在 `SimpleCredentials` 提供給 `Repository.login`. 屬性的值不相關且會被忽略，僅僅存在它就很重要且經過驗證。

## 設定SSO {#configuring-sso}

若要為AEM執行個體設定SSO，您需要設定 [SSO驗證處理常式](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler)：

1. 使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

   例如，對於NTLM集：

   * **路徑：** 視需要；例如 `/`
   * **頁首名稱**： `LOGON_USER`
   * **ID格式**： `^<DOMAIN>\\(.+)$`

      位置 `<*DOMAIN*>` 由您自己的網域名稱取代。
   對於CoSign：

   * **路徑：** 視需要；例如 `/`
   * **頁首名稱**： remote_user
   * **ID格式：** 原樣

   對於SiteMinder：

   * **路徑：** 視需要；例如 `/`
   * **頁首名稱：** SM_USER
   * **ID格式**：依現狀



1. 確認單一登入已視需要運作；包括授權。

>[!CAUTION]
>
>如果設定了SSO，請確定使用者無法直接存取AEM。
>
>透過要求使用者通過執行SSO系統代理程式的網頁伺服器，可確保沒有使用者可以直接傳送標頭、Cookie或引數，使使用者受到AEM信任，因為代理程式會篩選從外部傳送的此類資訊。
>
>任何使用者只要不透過網頁伺服器直接存取您的AEM執行個體，都可以傳送標頭、Cookie或引數（如果名稱已知），以任何使用者身分操作。
>
>同時請確定在標頭、Cookie和請求引數名稱中，您僅需設定SSO設定所需的名稱。

>[!NOTE]
>
>單一登入通常搭配使用 [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>如果您也使用 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 若使用Microsoft Internet Information Server (IIS)，則需要在下列專案中進行其他設定：
>
>* `disp_iis.ini`
>* IIS
>
>在 `disp_iis.ini` 設定：
>(請參閱 [安裝Dispatcher搭配Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) 以取得完整詳細資訊)
>
>* `servervariables=1` （將IIS伺服器變數作為請求標頭轉送給遠端執行個體）
>* `replaceauthorization=1` （將任何名為「Authorization」的標頭「Basic」以外的標頭替換為其「Basic」同等標頭）
>
>在IIS中：
>
>* disable **匿名存取**
>
>* 啟用 **整合式Windows驗證**
>


您可以使用以下專案檢視將哪個驗證處理常式套用至內容樹的任何區段： **驗證者** Felix主控台的選項；例如：

`http://localhost:4502/system/console/slingauth`

系統會先查詢最符合路徑的處理常式。 例如，如果您為路徑設定處理常式A `/` 和路徑的處理常式B `/content`，然後請求給 `/content/mypage.html` 會先查詢處理常式B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 示例 {#example}

對於Cookie請求（使用URL） `http://localhost:4502/libs/wcm/content/siteadmin.html`)：

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用以下設定：

* **路径**: `/`

* **頁首名稱**： `TestHeader`

* **Cookie名稱**： `TestCookie`

* **引數名稱**： `TestParameter`

* **ID格式**： `AsIs`

回應會是：

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

如果您要求，這也可以使用：
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

或者，您可以使用以下curl命令來傳送 `TestHeader` 頁首至 `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在瀏覽器中使用請求引數時，您只會看到部分HTML — 沒有CSS。 這是因為來自HTML的所有請求都是在沒有請求引數的情況下進行的。

## 移除AEM登出連結 {#removing-aem-sign-out-links}

使用SSO時，登入和登出會由外部處理，因此AEM自己的登出連結不再適用，應該移除。

您可使用下列步驟移除歡迎畫面上的登出連結。

1. 覆蓋 `/libs/cq/core/components/welcome/welcome.jsp` 至 `/apps/cq/core/components/welcome/welcome.jsp`
1. 從jsp中移除下列零件。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

若要移除使用者右上角個人功能表中可用的登出連結，請遵循下列步驟：

1. 覆蓋 `/libs/cq/ui/widgets/source/widgets/UserInfo.js` 至 `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 從檔案中移除下列零件：

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
