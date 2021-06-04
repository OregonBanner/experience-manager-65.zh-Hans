---
title: 与AdobeSearch&Promote集成
seo-title: 与AdobeSearch&Promote集成
description: 了解如何与AdobeSearch&Promote集成。
seo-description: 了解如何与AdobeSearch&Promote集成。
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# 与AdobeSearch&amp;Promote集成{#integrating-with-adobe-search-promote}

要从您的网站调用AdobeSearch&amp;Promote服务，请执行以下任务：

1. 指定云的URL。
1. 配置与Search&amp;Promote服务的连接。
1. 将Search&amp;Promote组件添加到Sidekick。
1. 使用组件创作内容。 (请参阅[向网页添加Search&amp;Promote功能](/help/sites-authoring/search-and-promote.md)。)
1. 将横幅添加到您的页面。 横幅图像对Search&amp;Promote数据敏感。
1. 为要使用的Search&amp;Promote服务生成站点映射。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的Search&amp;Promote，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能使用4.x API:
>
>* 3.x配置了[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置了[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## 更改Search&amp;Promote服务URL {#changing-the-search-promote-service-url}

为Search&amp;Promote服务配置的默认URL为`https://searchandpromote.omniture.com/px/`。 要使用其他服务，请使用OSGi控制台指定其他URL。

1. 打开OSGi控制台，然后单击配置选项卡。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 单击Day CQSearch&amp;Promote配置项。
1. 在“远程服务器URI”框中输入URL，然后单击“保存”。

## 配置与Search&amp;Promote{#configuring-the-connection-to-search-promote}的连接

配置一个或多个与Search&amp;Promote的连接，以便网页可以与服务进行交互。 要连接，您需要您的Search&amp;Promote帐户的成员标识和帐号。

1. 从&#x200B;**工具**&#x200B;图标> **部署**&#x200B;中，选择&#x200B;**Cloud Services**。

   这会将您转到“Cloud Services”功能板。 如果在本地计算机上，功能板的url将如下所示：

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. 在Cloud Services页面中，单击AdobeSearch&amp;Promote链接或Search&amp;Promote图标。

1. 如果这是您首次配置AdobeSearch&amp;Promote，请单击&#x200B;**立即配置**&#x200B;以打开创建配置面板。

   如果您想了解有关Search&amp;Promote的更多信息，请点击&#x200B;**了解更多**。

   ![](assets/chlimage_1-59.png)

1. 输入页面作者可识别的&#x200B;**标题**，输入唯一的&#x200B;**名称**，然后单击&#x200B;**创建**。

   将打开&#x200B;**编辑组件**&#x200B;窗口。

   此外，新创建的配置显示在&#x200B;**Cloud Services功能板** AdobeSearch&amp;Promote列表项的&#x200B;**可用配置**&#x200B;下方。

   ![](assets/chlimage_1-60.png)

1. 将以下内容添加到&#x200B;**编辑组件**&#x200B;对话框中的字段。

   * **成员·ID**
   * **帐号**

   >[!NOTE]
   >
   >要自己获取此信息&#x200B;**，您首先需要登录**
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >使用您的有效Seach&amp;Promote凭据（电子邮件/密码）。
   >然后，您需要在浏览器的地址栏中查看url，其外观应当如下所示：
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**其中：**
   >
   >    * **** XXXXXXXX与您的**会员id相对应**
   >    * **** spYYYYYYYYYYYY与您的帐 **号对应**


1. 单击&#x200B;**连接到Search&amp;Promote**。

   出现连接成功消息时，单击&#x200B;**确定**。

   (连接后，按钮文本将变为**重新连接到Search&amp;Promote**。)

1. 单击&#x200B;**确定**。此时将显示您刚刚创建的配置的Search&amp;Promote设置页面。

## 配置数据中心{#configuring-the-data-center}

如果您的Search&amp;Promote帐户位于亚洲或欧洲，则需要更改默认的数据中心，以便它指向正确的数据中心（默认的数据中心适用于北美帐户）。

要配置数据中心，请执行以下操作：

1. 导航到位于`https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`的Web控制台

   ![](assets/chlimage_1-61.png)

1. 根据服务器的位置，将URI更改为以下URI之一：

   * 北美：[https://center.atomz.com/px/](https://center.atomz.com/px/)
   * 欧洲、中东和非洲地区：[https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC:[https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 单击&#x200B;**保存**。

## 将Search&amp;Promote组件添加到Sidekick {#adding-search-promote-components-to-sidekick}

在设计模式下，编辑&#x200B;**par**&#x200B;组件，以允许在Sidekick中使用Search&amp;Promote组件。 （有关更多信息，请参阅[组件](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode)文档。）

有关使用组件的信息，请参阅[将Search&amp;Promote功能添加到网页](/help/sites-authoring/search-and-promote.md)。)

## 指定页面使用{#specifying-the-search-promote-service-that-your-pages-use}的Search&amp;Promote服务

配置网页，以便它们使用特定的Search&amp;Promote服务。 Search&amp;Promote组件会自动使用其主页的服务。

在为页面配置Search&amp;Promote属性时，所有子页面都会继承设置。 如果需要，您可以配置子页面以覆盖继承的设置。

>[!NOTE]
>
>必须已配置服务连接。 (请参阅[配置与Search&amp;Promote的连接](#connection)。)

1. 打开&#x200B;**页面属性**&#x200B;对话框。 例如，在**网站**页面上，右键单击该页面，然后单击&#x200B;**属性**。
1. 单击&#x200B;**Cloud Services**&#x200B;选项卡。
1. 要禁用父页面中云服务配置的继承，请单击继承路径旁边的挂锁图标。

   ![](assets/sandpinheritpadlock.png)

1. 单击&#x200B;**添加服务**，选择&#x200B;**AdobeSearch&amp;Promote**，然后单击&#x200B;**确定**。
1. 选择Search&amp;Promote帐户的连接配置，然后单击&#x200B;**确定**。

## 产品馈送{#product-feed}

Search&amp;Promote集成允许您：

* 使用电子商务API，与底层存储库结构和商务平台无关。
* 利用Search&amp;Promote的索引连接器功能以XML格式提供产品馈送。
* 利用Search&amp;Promote的远程控制功能执行产品馈送的按需或计划请求
* 不同Search&amp;Promote帐户的信息源生成，配置为云服务配置。

有关更多信息，请阅读[产品信息源](/help/sites-administering/product-feed.md)。
