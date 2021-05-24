---
title: 连接到Adobe Analytics和创建框架
seo-title: 连接到Adobe Analytics和创建框架
description: 了解如何将AEM连接到SiteCatalyst并创建框架。
seo-description: 了解如何将AEM连接到SiteCatalyst并创建框架。
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 8%

---

# 连接到Adobe Analytics并创建框架{#connecting-to-adobe-analytics-and-creating-frameworks}

要在Adobe Analytics中跟踪来自AEM页面的Web数据，请创建Adobe Analytics Cloud服务配置和Adobe Analytics框架：

* **Adobe Analytics配置：** 有关您的Adobe Analytics帐户的信息。Adobe Analytics配置允许AEM连接到Adobe Analytics。 为您使用的每个帐户创建Adobe Analytics配置。
* **Adobe Analytics框架：** Adobe Analytics报表包属性与CQ变量之间的一组映射。使用框架配置网站数据填充Adobe Analytics报表的方式。 框架与Adobe Analytics配置关联。 您可以为每个配置创建多个框架。

将网页与框架关联后，框架将执行该页面及该页面子项的跟踪。 然后，可以从Adobe Analytics中检索页面查看次数，并在站点控制台中显示这些查看次数。

## 前提条件 {#prerequisites}

### Adobe Analytics帐户{#adobe-analytics-account}

要在Adobe Analytics中跟踪AEM数据，您必须拥有有效的Adobe Marketing Cloud Adobe Analytics帐户。

Adobe Analytics帐户需要：

* 具有&#x200B;**管理员**&#x200B;权限
* 分配给&#x200B;**Web服务访问**&#x200B;用户组。

>[!CAUTION]
>
>提供&#x200B;**管理员**&#x200B;权限(在Adobe Analytics内)不足以允许用户从AEM连接到Adobe Analytics。 帐户还必须具有&#x200B;**Web服务访问**&#x200B;权限。

![chlimage_1-67](assets/chlimage_1-67.png)

在继续之前，请确保您的凭据允许您登录Adobe Analytics。 通过以下任一方式：

* [Adobe Experience Cloud登录](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe Analytics登录](https://sc.omniture.com/login/)

### 配置AEM以使用Adobe Analytics数据中心{#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [数据中心](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored)收集、处理和存储与Adobe Analytics报表包关联的数据。 您必须配置AEM以使用托管Adobe Analytics报表包的数据中心。 下表列出了可用的数据中心及其URL。

| 数据中心 | URL |
|---|---|
| 圣何塞 | https://api.omniture.com/admin/1.4/rest/ |
| 达拉斯 | https://api2.omniture.com/admin/1.4/rest/ |
| 伦敦 | https://api3.omniture.com/admin/1.4/rest/ |
| 新加坡 | https://api4.omniture.com/admin/1.4/rest/ |
| 俄勒冈州 | https://api5.omniture.com/admin/1.4/rest/ |

AEM默认使用圣何塞(https://api.omniture.com/admin/1.4/rest/)数据中心。

使用[Web控制台配置OSGi包](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **AdobeAEM Analytics HTTP Client**。 添加&#x200B;**数据中心URL** ，用于托管您的AEM页面为其收集数据的报表包的数据中心。

![aa-07](assets/aa-07.png)

1. 在Web浏览器中打开Web控制台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 输入您的凭据以访问控制台。

   >[!NOTE]
   >
   >请联系您的站点管理员，以了解您是否有权访问此控制台。

1. 选择名为&#x200B;**AdobeAEM Analytics HTTP Client**&#x200B;的配置项。
1. 要添加数据中心的URL，请按&#x200B;**数据中心URL**&#x200B;列表旁边的+按钮，然后在框中键入该URL。

1. 要从列表中删除URL，请单击URL旁边的 — 按钮。
1. 单击保存。

## 配置与Adobe Analytics的连接{#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>现在，应使用Adobe Analytics](https://docs.adobe.com/content/help/zh-Hans/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap插件。

## 为Activity Map{#configuring-for-the-activity-map}配置

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>现在，应使用Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap插件。

## 创建Adobe Analytics框架{#creating-a-adobe-analytics-framework}

对于您使用的报表包ID(RSID)，您可以控制哪些服务器实例（创作、发布或两者）向报表包贡献数据：

* **全部**:作者和发布实例中的信息会填充报表包。
* **作者**:只有来自创作实例的信息会填充报表包。
* **发布**:只有来自发布实例的信息才会填充报表包。

>[!NOTE]
>
>选择服务器实例类型不会限制对Adobe Analytics的调用，它只会控制包含RSID的调用。
>
>例如，框架配置为使用&#x200B;*diweretail*&#x200B;报表包，并且作者是选定的服务器实例。 当页面与框架一起发布时，仍会对Adobe Analytics发起调用，但这些调用不包含RSID。 只有来自创作实例的调用包含RSID。

1. 使用&#x200B;**导航**，选择&#x200B;**工具**、**Cloud Services**，然后选择&#x200B;**旧版Cloud Services**。
1. 滚动到&#x200B;**Adobe Analytics**，然后选择&#x200B;**显示配置**。
1. 单击您的Adobe Analytics配置旁边的&#x200B;**[+]**&#x200B;链接。

1. 在&#x200B;**创建框架**&#x200B;对话框中：

   * 指定&#x200B;**标题**。
   * 或者，您可以为存储库中框架详细信息的节点指定&#x200B;**名称**。
   * 选择&#x200B;**Adobe Analytics框架**

   然后单击&#x200B;**创建**。

   随即会打开框架进行编辑。

1. 在侧面板（主面板右侧）的&#x200B;**报表包**&#x200B;部分中，单击&#x200B;**添加项目**。 然后，使用下拉列表选择框架将与之交互的报表包ID（例如`geometrixxauth`）。

   >[!NOTE]
   >
   >当您选择报表包ID时，左侧的内容查找器中会填充Adobe Analytics变量(SiteCatalyst变量)。

1. 然后，使用&#x200B;**运行模式**&#x200B;下拉列表（位于报表包ID旁边）选择要向报表包发送信息的服务器实例。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 要使框架在网站的发布实例上可用，请在Sidekick的&#x200B;**Page**&#x200B;选项卡上，单击&#x200B;**激活框架。**

### 为Adobe Analytics配置服务器设置{#configuring-server-settings-for-adobe-analytics}

框架系统允许您更改每个Adobe Analytics框架中的服务器设置。

>[!CAUTION]
>
>这些设置决定了数据的发送位置和发送方式，因此您必须&#x200B;*不要篡改这些设置*，并让Adobe Analytics代表进行设置。

首先打开面板。 按&#x200B;**Servers**&#x200B;旁边的向下箭头：

![server_001](assets/server_001.png)

* **跟踪服务器**

   * 包含用于发送Adobe Analytics调用的URL

      * cname — 默认为Adobe Analytics帐户的&#x200B;*公司名称*
      * d1 — 与数据中心对应，该信息将被发送到（可以是d1、d2或d3）
      * sc.omtrdc.net — 域名

* **安全跟踪服务器**

   * 与跟踪服务器具有相同的区段
   * 用于从安全页面(https://)发送数据

* **访客命名空间**

   * 命名空间会确定跟踪URL的第一部分。
   * 例如，将命名空间更改为&#x200B;**CNAME**&#x200B;将导致对Adobe Analytics的调用看起来类似于&#x200B;**CNAME.d1.omtrdc.net**，而不是默认的。

## 将页面与Adobe Analytics框架{#associating-a-page-with-a-adobe-analytics-framework}关联

当页面与Adobe Analytics框架关联时，页面在加载时会向Adobe Analytics发送数据。 页面填充的变量会从框架中的Adobe Analytics变量进行映射和检索。 例如，页面查看次数是从Adobe Analytics中检索的。

页面的后代将继承与框架的关联。 例如，将站点的根页面与框架关联时，站点的所有页面都与该框架关联。

1. 从&#x200B;**站点**&#x200B;控制台中，选择要设置跟踪的页面。
1. 直接从控制台或页面编辑器中打开&#x200B;**[页面属性](/help/sites-authoring/editing-page-properties.md)**。
1. 打开**Cloud Services**选项卡。

1. 使用&#x200B;**Add Configuration**&#x200B;下拉列表从可用选项中选择&#x200B;**Adobe Analytics**。 如果放置了继承，则需要在选择器可用之前禁用该继承。

1. **Adobe Analytics**&#x200B;的下拉选择器将附加到可用选项中。 使用此选项可选择所需的框架配置。

1. 选择&#x200B;**保存并关闭**。
1. **[](/help/sites-authoring/publishing-pages.md)** 发布页面以激活页面和任何连接的配置/文件。
1. 最后一步是访问发布实例上的页面，并使用&#x200B;**Search**&#x200B;组件搜索关键词（例如茄子）。
1. 然后，您可以使用适当的工具检查对Adobe Analytics发出的调用；例如， [Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)。
1. 使用提供的示例，调用应包含eVar7中输入的值（即茄子），事件列表应包含event3。

### 页面查看次数 {#page-views}

当页面与Adobe Analytics框架关联时，“站点”控制台的“列表”视图中会显示页面查看次数。

有关更多详细信息，请参阅[查看页面分析数据](/help/sites-authoring/page-analytics-using.md)。

### 配置导入间隔{#configuring-the-import-interval}

配置&#x200B;**AdobeAEM Managed Polling Configuration**&#x200B;服务的相应实例：

* **轮询间隔**:服务从Adobe Analytics中检索页面查看数据的间隔，以秒为单位。默认间隔为43200000毫秒（12小时）。

* **启用**:启用或禁用服务。默认情况下，服务处于启用状态。

要配置此OSGi服务，您可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[osgiConfig节点（服务PID为`com.day.cq.polling.importer.impl.ManagedPollConfigImpl`）。

## 编辑Adobe Analytics配置和/或框架{#editing-adobe-analytics-configurations-and-or-frameworks}

与创建Adobe Analytics配置或框架一样，导航到（旧版）**Cloud Services**&#x200B;屏幕。 选择&#x200B;**显示配置**，然后单击指向要更新的特定配置的链接。

在编辑Adobe Analytics配置时，还需要在配置页面本身上按下&#x200B;**Edit**&#x200B;按钮，以打开&#x200B;**Edit Component**&#x200B;对话框。

## 删除Adobe Analytics框架{#deleting-adobe-analytics-frameworks}

要删除Adobe Analytics框架，请首先[将其打开以进行编辑](#editing-adobe-analytics-configurations-and-or-frameworks)。

然后，从Sidekick的&#x200B;**Page**&#x200B;选项卡中选择&#x200B;**删除框架**。
