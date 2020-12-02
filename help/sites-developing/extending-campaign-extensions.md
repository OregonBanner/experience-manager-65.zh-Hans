---
title: 创建自定义扩展
seo-title: 创建自定义扩展
description: 您可以从AEM或从AEM到Adobe Campaign调用自定义代码
seo-description: 您可以从AEM或从AEM到Adobe Campaign调用自定义代码
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---


# 创建自定义扩展{#creating-custom-extensions}

通常，在实施项目时，AEM和Adobe Campaign中都有自定义代码。 通过使用现有API，您可以从AEM或从AEM到Adobe Campaign调用自定义代码。 本文档介绍如何执行此操作。

## 前提条件 {#prerequisites}

您需要安装以下组件：

* Adobe Experience Manager
* Adobe Campaign6.1

有关详细信息，请参阅[将AEM与Adobe Campaign6.1](/help/sites-administering/campaignonpremise.md)集成。

## 示例1:AEM到Adobe Campaign{#example-aem-to-adobe-campaign}

AEM与活动之间的标准集成基于JSON和JSSP（JavaScript服务器页）。 这些JSSP文件可在活动控制台中找到，所有开始均具有&#x200B;**amc**(Adobe Marketing Cloud)。

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[有关此示例，请参阅Geometrixx](/help/sites-developing/we-retail.md)，它可从包共享中获取。

在此示例中，我们将新建一个自定义JSSP文件，并从AEM端调用该文件以检索结果。 例如，这可用于从Adobe Campaign检索数据或将数据保存到Adobe Campaign。

1. 在Adobe Campaign中，要创建新的JSSP文件，请单击&#x200B;**新建**&#x200B;图标。

   ![](do-not-localize/chlimage_1-4a.png)

1. 输入此JSSP文件的名称。 在此示例中，我们使用&#x200B;**cus:custom.jssp**(这意味着它将位于&#x200B;**cus**&#x200B;命名空间中)。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 将以下代码放入jssp-file中：

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 保存您的工作。 其余工作在AEM。
1. 在AEM端创建一个简单的servlet以调用此JSSP。 在本例中，我们假定：

   * 您在AEM和活动之间有连接
   * 活动云服务配置在&#x200B;**/content/geometrixx-outdoors**&#x200B;上

   此示例中最重要的对象是&#x200B;**GenericCampaignConnector**，它允许您在Adobe Campaign端调用（获取和发布）jssp文件。

   下面是一小段代码：

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 正如您在本例中所看到的，您需要将凭据传递到调用中。 您可以通过getCredentials()方法获取此信息，在该方法中，您可以在已配置活动云服务的页面中传递该信息。

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

完整代码如下：

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

## 示例2:Adobe Campaign到AEM {#example-adobe-campaign-to-aem}

AEM优惠开箱即用的API，用于检索siteadmin explorer视图中任意位置可用的对象。

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[有关此示例，请参阅Geometrixx](/help/sites-developing/we-retail.md)，它可从包共享中获取。

对于资源管理器中的每个节点，都有一个与其链接的API。 例如，节点：

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

API是：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

URL **.1.json**&#x200B;的结尾可替换为&#x200B;**.2.json**、**.3.json**，具体取决于您想获取的子级别数。要获取所有子级，可以使用关键字&#x200B;**infinity**:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

现在，要使用API，我们必须知道，默认情况下，AEM使用基本身份验证。

名为&#x200B;**amcIntegration.js**&#x200B;的JS库在6.1.1（内部版本8624及更高版本）中可用，可在多个其他版本中实现该逻辑。

### AEM API调用{#aem-api-call}

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

