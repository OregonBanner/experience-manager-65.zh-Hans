---
title: 连接到AdobeAnalytics并创建框架
seo-title: 连接到AdobeAnalytics并创建框架
description: 了解如何将AEM连接到SiteCatalyst和创建框架。
seo-description: 了解如何将AEM连接到SiteCatalyst和创建框架。
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 8%

---


# 连接到AdobeAnalytics并创建框架 {#connecting-to-adobe-analytics-and-creating-frameworks}

要跟踪AdobeAnalyticsAEM页面中的Web数据，请创建AdobeAnalyticsCloud Service配置和AdobeAnalytics框架：

* **AdobeAnalytics配置：** 有关您的AdobeAnalytics帐户的信息。 AdobeAnalytics配置使AEM能够连接到AdobeAnalytics。 为您使用的每个帐户创建AdobeAnalytics配置。
* **AdobeAnalytics框架：** AdobeAnalytics报告套件属性与CQ变量之间的映射集。 使用框架配置网站数据如何填充AdobeAnalytics报告。 框架与AdobeAnalytics配置相关。 您可以为每个配置创建多个框架。

将网页与框架关联后，框架将对该页面及该页面的后代执行跟踪。 页面视图随后可从Adobe Analytics检索并显示在站点控制台中。

## 前提条件 {#prerequisites}

### Adobe Analytics Account {#adobe-analytics-account}

要跟踪AdobeAnalytics的AEMAdobe Marketing Cloud，您必须拥有有效的AdobeAnalytics帐户。

AdobeAnalytics帐户需要：

* 具有管 **理员** 权限
* 被分配给 **Web服务访问** 用户组。

>[!CAUTION]
>
>提 **供管理员** (在AdobeAnalytics内)权限不足以允许用户从AEM连接到AdobeAnalytics。 帐户还必须具有 **Web服务访问权** 限。

![chlimage_1-67](assets/chlimage_1-67.png)

在继续操作之前，请确保凭据允许您登录AdobeAnalytics。 通过以下任一方式：

* [Adobe Experience Cloud登录](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [AdobeAnalytics登录](https://sc.omniture.com/login/)

### 将AEM配置为使用AdobeAnalytics数据中心 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

AdobeAnalytics [数据中心](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) ，收集、处理和存储与您的AdobeAnalytics报告套件相关的数据。 您必须配置AEM以使用承载AdobeAnalytics报表包的数据中心。 下表列表了可用数据中心及其URL。

| 数据中心 | URL |
|---|---|
| 圣何塞 | https://api.omniture.com/admin/1.4/rest/ |
| 达拉斯 | https://api2.omniture.com/admin/1.4/rest/ |
| 伦敦 | https://api3.omniture.com/admin/1.4/rest/ |
| 新加坡 | https://api4.omniture.com/admin/1.4/rest/ |
| 俄勒冈州 | https://api5.omniture.com/admin/1.4/rest/ |

默认情况下，AEM使用San Jose(https://api.omniture.com/admin/1.4/rest/)数据中心。

使用Web [控制台配置OSGi bundle](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)**Adobe AEMAnalyticsHTTP客户端**。 为承载 **AEM页面** （其收集数据）报表包的数据中心添加数据中心URL。

![aa-07](assets/aa-07.png)

1. 在Web浏览器中打开Web控制台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 输入您的凭据以访问控制台。

   >[!NOTE]
   >
   >请联系您的站点管理员，了解您是否有权访问此控制台。

1. 选择名为Adobe AEM **AnalyticsHTTP Client的配置项**。
1. 要添加数据中心的URL，请按“数据中心URL” **列表旁的** +按钮，并在框中键入URL。

1. 要从列表中删除URL，请单击URL旁的——按钮。
1. 单击保存。

## Configuring the Connection to Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，因此无法再使用 AEM 中包含的 Activity Map 版本。
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/zh-Hans/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Configuring for the Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，因此无法再使用 AEM 中包含的 Activity Map 版本。
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/zh-Hans/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## 创建AdobeAnalytics框架 {#creating-a-adobe-analytics-framework}

对于您正在使用的报表包ID(RSID)，您可以控制哪些服务器实例（作者、发布或两者）将数据贡献到报表包：

* **全部**: 来自作者和发布实例的信息将填充报表包。
* **作者**: 只有来自作者实例的信息才会填充报表包。
* **发布**: 只有发布实例中的信息才会填充报表包。

>[!NOTE]
>
>选择服务器实例的类型不会限制对Adobe Analytics的调用，它只控制哪些调用包括RSID。
>
>例如，框架配置为使用diweretail报 *表包* ，而author是选定的服务器实例。 当页面与框架一起发布时，仍会向Adobe Analytics发出调用，但这些调用不包含RSID。 只有来自作者实例的调用包含RSID。

1. 使用 **导航**，选 **择工具**, **Cloud Service**，然后选 **择旧版** Cloud Service。
1. 滚动到Adobe **Analytics** ，然后选择 **“显示配置”**。
1. 单击您 **的AdobeAnalytics** 配置旁边的[+]链接。

1. 在“创 **建框架** ”对话框中：

   * 指定 **标题**。
   * （可选）您可以 **为存储**&#x200B;库中存储框架详细信息的节点指定名称。
   * 选择 **AdobeAnalytics框架**

   然后单击 **创建**。

   此时将打开框架进行编辑。

1. 在侧 **面板** （主面板右侧）的“报表包”部分，单击“添 **加项目”**。 然后使用下拉框选择框架将与之交互的 `geometrixxauth`报表包ID（例如）。

   >[!NOTE]
   >
   >选择报表包ID时，左侧的内容查找器中会填充AdobeAnalytics变量（SiteCatalyst变量）。

1. 然后使用 **运行模式** （在报表包ID旁边）下拉框选择要向报表包发送信息的服务器实例。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 要使框架可用于站点的发布实例，请在Sidekick的“页面 **”选项卡** ，单击“激 **活框架”。**

### 为Adobe Adobe配置服务器设置Analytics {#configuring-server-settings-for-adobe-analytics}

框架系统允许您更改每个AdobeAnalytics框架中的服务器设置。

>[!CAUTION]
>
>这些设置决定了数据的发送位置和发送方式，因此您必须 *不要篡改这些设置* ，让AdobeAnalytics代表设置它。

开始。 按“Servers（服务器）”旁边的向下 **箭头**:

![server_001](assets/server_001.png)

* **跟踪服务器**

   * 包含用于发送AdobeAnalytics呼叫的URL

      * cname —— 默认为AdobeAnalytics帐户的 *公司名*
      * d1 —— 与数据中心对应，信息将被发送到（可以是d1、d2或d3）
      * sc.omtrdc.net —— 域名

* **安全跟踪服务器**

   * 具有与跟踪服务器相同的区段
   * 它用于从安全页面发送数据(https://)

* **访客命名空间**

   * 命名空间确定跟踪URL的第一部分。
   * 例如，将命名空间更 **改为** CNAME将导致对Adobe Deport的调用 **看起来像CNAME.d1.omtrdc.net** ，而不是默认。

## 将页面与AdobeAnalytics框架关联 {#associating-a-page-with-a-adobe-analytics-framework}

当页面与AdobeAnalytics框架关联时，页面加载时会向AdobeAnalytics发送数据。 页面所填充的变量是从框架中的AdobeAnalytics变量映射和检索的。 例如，从Adobe Design检索页面视图。

页面的后代继承与框架的关联。 例如，将站点的根页面与框架关联时，站点的所有页面都与框架关联。

1. 从“站 **点** ”控制台中，选择要设置跟踪的页面。
1. 直接从 **[控制台或](/help/sites-authoring/editing-page-properties.md)**页面编辑器打开页面属性。
1. 打开**Cloud Service**选项卡。

1. 使用 **添加配置** 下拉框，从 **可用选项** 中选择AdobeAnalytics。 如果放置了继承，则需要在选择器可用之前禁用它。

1. Adobe Analytics的下拉选 **择器将** 附加到可用选项中。 使用它选择所需的框架配置。

1. Select **Save &amp; Close**.
1. **[发布页](/help/sites-authoring/publishing-pages.md)**，以激活页面和所有连接的配置／文件。
1. 最后一步是访问发布实例中的页面，并使用搜索组件搜索关键字(如 **茄子** )。
1. 然后，您可以使用适当的工具检查向AdobeAnalytics发出的呼叫； 例如， [Adobe Experience Cloud调试器](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)。
1. 使用提供的示例，调用应包含eVar7中输入的值(即事件语)，而列表语应包含事件3。

### 页面查看次数 {#page-views}

当页面与AdobeAnalytics框架关联时，页面视图的数量可显示在站点控制台的列表视图中。

有关更 [多详细信息，请参](/help/sites-authoring/page-analytics-using.md) 阅查看页面Analytics数据。

### 配置导入间隔 {#configuring-the-import-interval}

配置Adobe AEM Managed轮询配 **置服务的相应实例** :

* **轮询间隔**:
服务从Adobe Analytics检索页面视图数据的时间间隔（以秒为单位）。
默认时间间隔为43200000毫秒（12小时）。

* **启用**:
启用或禁用服务。 默认情况下，服务处于启用状态。

要配置此OSGi服务，您可以使 [用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) , [或在存储库中使用](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) osgiConfig节点(服务PID `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`为)。

## 编辑AdobeAnalytics配置和／或框架 {#editing-adobe-analytics-configurations-and-or-frameworks}

与创建AdobeAnalytics配置或框架时一样，导航到（传统） **Cloud Service屏** 。 选 **择显示**&#x200B;配置，然后单击指向要更新的特定配置的链接。

编辑AdobeAnalytics配置时，您还需要在配置页 **面本身** 上按“编辑”按钮，才能打开“编 **辑组件** ”对话框。

## 删除AdobeAnalytics框架 {#deleting-adobe-analytics-frameworks}

要删除AdobeAnalytics框架，请先 [打开进行编辑](#editing-adobe-analytics-configurations-and-or-frameworks)。

然后， **从Sidekick的** “页 **面”选** 项卡中选择“删除框架”。

