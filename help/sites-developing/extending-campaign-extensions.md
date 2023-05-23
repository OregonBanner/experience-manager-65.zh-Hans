---
title: 建立自訂擴充功能
seo-title: Creating Custom Extensions
description: 您可以在Adobe Campaign中從AEM或從AEM呼叫Adobe Campaign的自訂程式碼
seo-description: You can call your custom code in Adobe Campaign from AEM or from AEM to Adobe Campaign
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
exl-id: 0702858e-5e46-451f-9ac3-40a4fec68ca0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# 建立自訂擴充功能{#creating-custom-extensions}

一般而言，實作專案時，您在AEM和Adobe Campaign中都有自訂程式碼。 使用現有API，您可以在Adobe Campaign中從AEM或從AEM到Adobe Campaign呼叫自訂程式碼。 本檔案將說明如何執行此操作。

## 前提条件 {#prerequisites}

您必須安裝下列專案：

* Adobe Experience Manager
* Adobe Campaign 6.1

另請參閱 [將AEM與Adobe Campaign 6.1整合](/help/sites-administering/campaignonpremise.md) 以取得詳細資訊。

## 範例1：從AEM到Adobe Campaign {#example-aem-to-adobe-campaign}

AEM和Campaign之間的標準整合是以JSON和JSSP （JavaScript伺服器頁面）為基礎。 這些JSSP檔案可在Campaign主控台中找到，而且全都開頭為 **amc** (Adobe Marketing Cloud)。

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[如需此範例，請參閱Geometrixx](/help/sites-developing/we-retail.md)，可在「封裝共用」中取得。

在此範例中，我們會建立新的自訂JSSP檔案，並從AEM端呼叫該檔案來擷取結果。 舉例來說，這可用來從Adobe Campaign擷取資料，或將資料儲存至Adobe Campaign。

1. 在Adobe Campaign中，若要建立新的JSSP檔案，請按一下 **新增** 圖示。

   ![](do-not-localize/chlimage_1-4a.png)

1. 輸入此JSSP檔案的名稱。 在此範例中，我們使用 **cus：custom.jssp** (這表示它將位於 **cus** 名稱空間)。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 將下列程式碼放入jssp-file中：

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 儲存您的工作。 其餘的工作在AEM中。
1. 在AEM端建立簡單的servlet以呼叫此JSSP。 在此範例中，我們假設如下：

   * 您已在AEM和Campaign之間使用連線
   * campaign cloudservice設定於 **/content/geometrixx-outdoors**

   此範例中最重要的物件是 **GenericCampaignConnector**，可讓您在Adobe Campaign端呼叫（取得和發佈） jssp檔案。

   以下是一個小型程式碼片段：

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 如本範例所示，您必須將認證傳入呼叫。 您可以透過getCredentials()方法取得此資訊，您可在其中傳入已設定Campaign雲端服務的頁面。

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

完整的程式碼如下：

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## 範例2：從Adobe Campaign到AEM {#example-adobe-campaign-to-aem}

AEM提供立即可用的API，可擷取siteadmin explorer檢視中任何位置的物件。

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[如需此範例，請參閱Geometrixx](/help/sites-developing/we-retail.md)，可在「封裝共用」中取得。

對於總管中的每個節點，都有一個API連結至該節點。 例如，節點：

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

API是：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

URL結尾 **.1.json** 可以取代為 **.2.json**， **.3.json**，根據您想要取得的子層級數量以取得所有子層級關鍵字 **無限** 可使用：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

現在若要使用API，我們必須知道AEM預設會使用基本驗證。

名為的JS程式庫 **amcIntegration.js** 6.1.1 （版本編號8624及更新版本）中提供，可在其他數個版本中實作該邏輯。

### AEM API呼叫 {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```
