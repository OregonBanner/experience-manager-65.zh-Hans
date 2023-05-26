---
title: 连接到Adobe Analytics并创建框架
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: 了解如何将AEM连接到SiteCatalyst和创建框架。
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 6%

---

# 连接到Adobe Analytics并创建框架 {#connecting-to-adobe-analytics-and-creating-frameworks}

要从Adobe Analytics中的AEM页面跟踪Web数据，请创建Adobe Analytics Cloud Services配置和Adobe Analytics框架：

* **Adobe Analytics配置：** 有关您的Adobe Analytics帐户的信息。 通过Adobe Analytics配置，AEM可以连接到Adobe Analytics。 为您使用的每个帐户创建一个Adobe Analytics配置。
* **Adobe Analytics框架：** Adobe Analytics报表包属性和CQ变量之间的一组映射。 使用框架配置网站数据如何填充Adobe Analytics报表。 框架与Adobe Analytics配置关联。 您可以为每个配置创建多个框架。

将网页与框架关联时，该框架将对该页面以及该页面的后代执行跟踪。 然后，可以从Adobe Analytics中检索页面查看并显示在站点控制台中。

## 前提条件 {#prerequisites}

### Adobe Analytics帐户 {#adobe-analytics-account}

要在Adobe Analytics中跟踪AEM数据，您必须拥有有效的Adobe Experience Cloud Adobe Analytics帐户。

Adobe Analytics帐户必须：

* 具有 **管理员** 权限
* 分配给 **Web服务访问** 用户组。

>[!CAUTION]
>
>提供 **管理员** 权限(在Adobe Analytics中)不足以允许用户从AEM连接到Adobe Analytics。 该帐户还必须具有 **Web服务访问** 权限。

![chlimage_1-67](assets/chlimage_1-67.png)

在继续操作之前，请确保您的凭据允许您登录到Adobe Analytics。 通过下列任一方式：

* [Adobe Experience Cloud登录](https://experience.adobe.com/#/@login/home)

* [Adobe Analytics登录](https://sc.omniture.com/login/)

### 配置AEM以使用您的Adobe Analytics数据中心 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [数据中心](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) 收集、处理和存储与您的Adobe Analytics报表包关联的数据。 配置AEM以使用托管Adobe Analytics报表包的数据中心。 您的合同中提到了数据中心。 有关此类信息，请联系您组织中的管理员。

如有必要，请使用下列内容以路由到正确的数据中心： `https://api.omniture.com/`.

如果您的组织需要从特定数据中心收集或检索数据，请使用以下内容：

| 数据中心 | URL |
|---|---|
| 伦敦 | `https://api3.omniture.com/` |
| 新加坡 | `https://api4.omniture.com/` |
| 俄勒冈州 | `https://api5.omniture.com/` |

使用 [用于配置OSGi包的Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **AdobeAEM Analytics HTTP客户端**. 添加 **数据中心URL** 适用于托管报表包的数据中心，您的AEM页面会为报表包收集数据。

![aa-07](assets/aa-07.png)

1. 在Web浏览器中打开Web控制台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 要访问该控制台，请输入您的凭据。

   >[!NOTE]
   >
   >要了解您是否有权访问此控制台，请联系您的站点管理员。

1. 选择名为的配置项 **AdobeAEM Analytics HTTP客户端**.
1. 要添加数据中心的URL，请按“+”按钮 **数据中心URL** 列表，然后在框中键入URL。

1. 要从列表中删除URL，请单击URL旁边的 — 按钮。
1. 单击“保存”。

## 配置与Adobe Analytics的连接 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>此 [Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 现在应使用。

## 为Activity Map配置 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>此 [Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 现在应使用。

## 创建Adobe Analytics框架 {#creating-a-adobe-analytics-framework}

对于您正在使用的报表包ID (RSID)，您可以控制哪些服务器实例（创作、发布或两者）向报表包贡献数据：

* **全部**：来自创作实例和发布实例的信息会填充报表包。
* **作者**：只有来自创作实例的信息会填充报表包。
* **Publish**：只有发布实例中的信息会填充报表包。

>[!NOTE]
>
>选择服务器实例的类型不会限制对Adobe Analytics的调用，它只是控制哪些调用包含RSID。
>
>例如，框架配置为使用 *diiweretail* 报表包和作者是选定的服务器实例。 当页面与框架一起发布时，仍会调用Adobe Analytics，但这些调用不包含RSID。 只有来自创作实例的调用包含RSID。

1. 使用 **导航**，选择 **工具**， **Cloud Services**，则 **旧版Cloud Services**.
1. 滚动到 **Adobe Analytics** 并选择 **显示配置**.
1. 单击 **[+]** Adobe Analytics配置旁边的链接。

1. 在 **创建框架** 对话框：

   * 指定&#x200B;**标题**。
   * （可选）您可以指定 **名称**，适用于在存储库中存储框架详细信息的节点。
   * 选择 **Adobe Analytics框架**

   然后单击 **创建**.

   此时将打开框架进行编辑。

1. 在 **报表包** 侧面板的部分（主面板的右侧），单击 **添加项目**. 然后，使用下拉菜单选择报表包ID(例如， `geometrixxauth`)进行交互。

   >[!NOTE]
   >
   >当您选择报表包ID时，左侧的SiteCatalyst查找器中会填充Adobe Analytics变量（内容变量）。

1. 要选择要向报表包发送信息的服务器实例，请使用 **运行模式** 下拉列表（位于报表包ID旁边）。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 要使框架在网站的发布实例上可用，请在 **页面** 选项卡，单击 **激活框架。**

### 配置Adobe Analytics的服务器设置 {#configuring-server-settings-for-adobe-analytics}

通过框架系统，您可以更改每个Adobe Analytics框架中的服务器设置。

>[!CAUTION]
>
>这些设置决定发送数据的位置和方式，因此您必须执行以下操作 *请勿篡改这些设置* 让您的Adobe Analytics代表来设置它。

首先打开面板。 按旁边向下箭头 **服务器**：

![server_001](assets/server_001.png)

* **跟踪服务器**

   * 包含用于发送Adobe Analytics调用的URL

      * `cname`  — 默认为Adobe Analytics帐户的 *公司名称*
      * `d1`  — 对应于将信息发送到的数据中心(通过 `d1`， `d2`，或 `d3`)
      * `sc.omtrdc.net`  — 域名

* **安全跟踪服务器**

   * 具有与跟踪服务器相同的区段
   * 用于从安全页面发送数据(`https://`)

* **访客命名空间**

   * 命名空间可确定跟踪URL的第一部分。
   * 例如，将命名空间更改为 **CNAME** 导致对Adobe Analytics的调用显示为 **CNAME.d1.omtrdc.net** 而不是默认内容。

## 将页面与Adobe Analytics框架关联 {#associating-a-page-with-a-adobe-analytics-framework}

当页面与Adobe Analytics框架关联时，页面会在加载时向Adobe Analytics发送数据。 页面填充的变量将从框架中的Adobe Analytics变量中进行映射和检索。 例如，从Adobe Analytics中检索页面查看次数。

页面的后代将继承与框架的关联。 例如，将站点的根页面与框架关联时，站点的所有页面都将与框架关联。

1. 从 **站点** 控制台中，选择要使用跟踪设置的页面。
1. 打开 **[页面属性](/help/sites-authoring/editing-page-properties.md)**，可以直接从控制台访问，也可以从页面编辑器访问。
1. 打开**Cloud Services**选项卡。

1. 使用 **添加配置** 下拉菜单选择 **Adobe Analytics** 从可用选项开始。 如果存在继承，请在选择器可用之前禁用继承。

1. 的下拉选择器 **Adobe Analytics** 会附加到可用的选项中。 选择所需的框架配置。

1. 选择 **保存并关闭**.
1. 要激活页面和任何连接的配置/文件，请 **[Publish](/help/sites-authoring/publishing-pages.md)** 页面。
1. 最后一步是访问发布实例上的页面，然后使用搜索关键词（例如，茄子） **搜索** 组件。
1. 然后，您可以使用适当的工具检查对Adobe Analytics进行的调用；例如， [Adobe Experience Cloud调试器](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. 根据提供的示例，调用应包含在eVar7中输入的值（即，eggplant），事件列表应包含event3。

### 页面视图 {#page-views}

当页面与Adobe Analytics框架关联时，站点控制台的列表视图中可以显示页面查看次数。

参见 [查看页面分析数据](/help/sites-authoring/page-analytics-using.md) 了解更多详细信息。

### 配置导入间隔 {#configuring-the-import-interval}

配置适当的实例 **AdobeAEM托管轮询配置** 服务：

* **轮询间隔**：服务从Adobe Analytics检索页面查看数据的时间间隔，以秒为单位。
默认时间间隔为43200000毫秒（12小时）。

* **启用**：启用或禁用服务。 默认情况下，该服务处于启用状态。

要配置此OSGi服务，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存储库中的osgiConfig节点](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (服务PID为 `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`)。

## 编辑Adobe Analytics配置和/或框架 {#editing-adobe-analytics-configurations-and-or-frameworks}

与创建Adobe Analytics配置或框架时一样，导航到（旧版） **Cloud Services** 屏幕。 选择 **显示配置**，然后单击要更新的特定配置的链接。

编辑Adobe Analytics配置时，按 **编辑** 在配置页面上打开 **编辑组件** 对话框。

## 删除Adobe Analytics框架 {#deleting-adobe-analytics-frameworks}

要删除Adobe Analytics框架，请首先 [打开以进行编辑](#editing-adobe-analytics-configurations-and-or-frameworks).

然后选择 **删除框架** 从 **页面** 帮他搭便车。
