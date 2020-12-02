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
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---


# 与AdobeSearch&amp;Promote集成{#integrating-with-adobe-search-promote}

要从您的网站调用AdobeSearch&amp;Promote服务，请执行以下任务:

1. 指定云的URL。
1. 配置与Search&amp;Promote服务的连接。
1. 将Search&amp;Promote组件添加到Sidekick。
1. 使用组件创作内容。 (请参阅[向网页添加Search&amp;Promote功能](/help/sites-authoring/search-and-promote.md)。)
1. 向页面添加横幅。 横幅图像对Search&amp;Promote数据敏感。
1. 为要使用的Search&amp;Promote服务生成站点地图。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的Search&amp;Promote，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些则使用4.x API:
>
>* 3.x配置有[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置有[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## 更改Search&amp;Promote服务URL {#changing-the-search-promote-service-url}

为Search&amp;Promote服务配置的默认URL为`https://searchandpromote.omniture.com/px/`。 要使用其他服务，请使用OSGi控制台指定其他URL。

1. 打开OSGi控制台，然后单击“Configuration（配置）”选项卡。 ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. 单击“Day CQSearch&amp;Promote配置”项。
1. 在“远程服务器URI”框中输入URL，然后单击“保存”。

## 配置与Search&amp;Promote{#configuring-the-connection-to-search-promote}的连接

配置一个或多个与Search&amp;Promote的连接，以便网页能够与服务交互。 要进行连接，您需要您的Search&amp;Promote帐户的成员标识和帐户号。

1. 从&#x200B;**工具**&#x200B;图标> **部署**&#x200B;中，选择&#x200B;**Cloud Services**。

   这会带你去Cloud Services仪表板。 如果在本地计算机上，仪表板的url将类似于：

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. 在Cloud Services页面中，单击AdobeSearch&amp;Promote链接或Search&amp;Promote图标。

1. 如果这是您首次配置AdobeSearch&amp;Promote，请单击&#x200B;**立即配置**&#x200B;以打开创建配置面板。

   如果想了解有关Search&amp;Promote的更多信息，请单击&#x200B;**了解更多**。

   ![](assets/chlimage_1-59.png)

1. 输入页面作者可识别的&#x200B;**标题**，输入唯一的&#x200B;**名称**，然后单击&#x200B;**创建**。

   将打开&#x200B;**编辑组件**&#x200B;窗口。

   此外，新创建的配置显示在&#x200B;**Cloud Services仪表板** AdobeSearch&amp;Promote项&lt;a2/>可用配置&#x200B;**下。**

   ![](assets/chlimage_1-60.png)

1. 在&#x200B;**编辑组件**&#x200B;对话框的字段中添加以下内容。

   * **成员·ID**
   * **帐号**

   >[!NOTE]
   >
   >要自行获取此信息&#x200B;**，您首先需要登录**
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >使用有效的Seach&amp;Promote凭据（电子邮件／密码）。
   >然后，您需要查看浏览者地址栏中的url，其应类似于：
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**其中：**
   >
   >    * **** XXXXXXXXXX与您**成员id**对应
   >    * **spYYYYYYYYY** YYYY与您的帐 **户编号对应**


1. 单击&#x200B;**连接到Search&amp;Promote**。

   显示连接成功消息时，单击&#x200B;**确定**。

   (连接后，按钮文本变为**重新连接到Search&amp;Promote**。)

1. 单击&#x200B;**确定**。此时将显示您刚刚创建的配置的Search&amp;Promote设置页。

## 配置数据中心{#configuring-the-data-center}

如果您的Search&amp;Promote帐户位于亚洲或欧洲，您需要更改默认数据中心，以便它指向正确的数据中心（默认数据中心针对北美客户）。

要配置数据中心，请执行以下操作：

1. 导航到位于`https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`的Web控制台

   ![](assets/chlimage_1-61.png)

1. 根据服务器的位置，将URI更改为以下值之一：

   * 北美：[https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA:[https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * 亚太：[https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 单击&#x200B;**保存**。

## 将Search&amp;Promote组件添加到Sidekick {#adding-search-promote-components-to-sidekick}

在“设计”模式中，编辑&#x200B;**par**&#x200B;组件，以允许Sidekick中的Search&amp;Promote组件。 （有关详细信息，请参阅[组件](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode)文档。）

有关使用这些组件的信息，请参阅[向网页添加Search&amp;Promote功能](/help/sites-authoring/search-and-promote.md)。)

## 指定页面使用的Search&amp;Promote服务{#specifying-the-search-promote-service-that-your-pages-use}

配置网页，使其使用特定的Search&amp;Promote服务。 Search&amp;Promote组件自动使用其主机页的服务。

为页面配置Search&amp;Promote属性时，所有子页面都会继承设置。 如果需要，您可以配置子页面以覆盖继承的设置。

>[!NOTE]
>
>必须已配置服务连接。 (请参阅[配置与Search&amp;Promote的连接](#connection)。)

1. 打开&#x200B;**页面属性**&#x200B;对话框。 例如，在**网站**页面上，右键单击该页面，然后单击&#x200B;**属性**。
1. 单击&#x200B;**Cloud Services**&#x200B;选项卡。
1. 要从父页面禁用云服务配置的继承，请单击继承路径旁的挂锁图标。

   ![](assets/sandpinheritpadlock.png)

1. 单击&#x200B;**添加服务**，选择&#x200B;**AdobeSearch&amp;Promote**，然后单击&#x200B;**确定**。
1. 选择Search&amp;Promote帐户的连接配置，然后单击&#x200B;**确定**。

## 产品源{#product-feed}

Search&amp;Promote集成允许您：

* 使用独立于基础存储库结构和商务平台的eCommerce API。
* 利用Search&amp;Promote的索引连接器功能以XML格式提供产品源。
* 利用Search&amp;Promote的远程控制功能执行产品源的按需或计划请求
* 不同Search&amp;Promote帐户的源生成，配置为云服务配置。

有关详细信息，请阅读[产品信息源](/help/sites-administering/product-feed.md)。
