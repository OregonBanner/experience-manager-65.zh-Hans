---
title: 配置分析和报表
seo-title: 配置分析和报表
description: 了解如何配置Adobe Analytics，以发现用户在使用自适应表单、自适应文档和HTML5表单时遇到的交互模式和问题。
seo-description: 了解如何配置Adobe Analytics，以发现用户在使用自适应表单、自适应文档和HTML5表单时遇到的交互模式和问题。
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---

# 配置Analytics和报表{#configuring-analytics-and-reports}

AEM Forms与Adobe Analytics集成，允许您捕获和跟踪已发布的表单和文档的性能量度。 分析这些量度的目的是，根据使表单或文档更易用所需更改的数据做出明智决策。

>[!NOTE]
>
>AEM Forms中的分析功能作为AEM Forms附加组件包的一部分提供。 有关安装附加组件包的信息，请参阅[安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。
>
>除了附加组件包之外，您还需要拥有AEM实例的Adobe Analytics帐户和管理员权限。 有关解决方案的信息，请参阅[Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

## 概述 {#overview}

您可以使用Adobe Analytics来发现用户在使用自适应表单、HTML5表单和交互式通信时遇到的交互模式和问题。 Adobe分析会开箱即用地跟踪和存储有关以下参数的信息：

* **平均填充时间**:填写表单的平均逗留时间。
* **演绎版**:打开表单的次数。
* **草稿**:表单在草稿状态下保存的次数。
* **提交**:提交表单的次数。
* **中止**:用户在未完成表单时离开的次数。

您可以自定义Adobe Analytics以添加/删除更多参数。 除了上述信息外，该报表还包含有关HTML5和自适应表单每个面板的以下信息：

* **时间**:在面板和面板字段上逗留的时间。
* **错误**:在面板和面板的字段中遇到的错误数。
* **帮助**:用户打开面板帮助和面板字段的次数。

## 创建报表包{#creating-report-suite}

Analytics数据存储在称为报表包的特定于客户的存储库中。 要创建报表包并使用Adobe Analytics，您必须拥有有效的Adobe Marketing Cloud帐户。 在执行以下步骤之前，请确保您拥有有效的Adobe Marketing Cloud帐户。

执行以下步骤以创建报表包。

1. 登录到[https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. 在Marketing Cloud中，选择&#x200B;**管理员** > **Admin Console** > **报表包**。
1. 在报表包管理器中选择&#x200B;**新建** > **报表包**。

   ![新建报表包](assets/newreportsuite_new.png)

   新建报表包

1. 确保第一个下拉列表设置为&#x200B;**从模板创建**，然后选择&#x200B;**商务**。
1. 找到&#x200B;**报表包ID**&#x200B;字段并添加新的报表包ID。 例如，JJEsquire。 报表包ID显示在报表包ID字段的下方。 它包含自动前缀，该前缀通常为公司名称。
1. 添加新的&#x200B;**站点标题**。 例如，JJEsquire快速入门套件。 此标题在Analytics UI中使用。 在代码中使用报表包ID。
1. 从下拉菜单中选择&#x200B;**时区**。 进入此报表包的所有数据都会根据定义的时区进行记录。
1. 将&#x200B;**基本URL**&#x200B;和&#x200B;**默认页面**&#x200B;字段留空。 这两个值仅用于从Adobe Marketing Cloud界面链接到您的网站。
1. 将&#x200B;**Go Live Date**&#x200B;保留设置为今天。 起始日期确定激活报表包的日期。
1. 在&#x200B;**估计每日页面查看次数**&#x200B;字段中，键入100。 使用此字段可估计您预计网站每天的页面查看次数。 此估计值允许Adobe放置适当数量的硬件来处理您要收集的数据。
1. 从下拉菜单中选择&#x200B;**基本货币**。 此报表包中的所有货币数据都将以此货币格式转换和存储。
1. 单击&#x200B;**创建报表**&#x200B;包。 您应会看到页面刷新，并显示一条消息，指出您的报表包已成功创建。
1. 选择新创建的报表包。 导航到&#x200B;**编辑设置** > **常规** > **一般帐户设置**。

   ![一般帐户设置](assets/geographic_settings.png)

   一般帐户设置

1. 在“一般帐户设置”屏幕中，启用&#x200B;**Geography Reporting**，然后单击&#x200B;**Save.**
1. 导航到&#x200B;**编辑设置** > **流量** > **流量变量**。
1. 在报表包中，配置并启用以下流量变量。

   * **formName**:自适应表单的标识符。
   * **formInstance**:自适应表单实例的标识符。启用此变量的路径报表。
   * **fieldName**:自适应表单字段的标识符。启用此变量的路径报表。
   * **panelName**:自适应表单面板的标识符。启用此变量的路径报表。
   * **formTitle**:表单的标题。
   * **fieldTitle**:表单字段的标题。
   * **panelTitle**:表单面板的标题。
   * **analytics版本**:表单分析的版本。

1. 导航到&#x200B;**编辑设置** > **转化** > **成功事件**。 定义并启用以下成功事件：

   | 成功事件 | 类型 |
   |---|---|
   | 放弃 | 计数器 |
   | render | 计数器 |
   | panelVisit | 计数器 |
   | fieldVisit | 计数器 |
   | 保存 | 计数器 |
   | 错误 | 计数器 |
   | 帮助 | 计数器 |
   | 提交 | 计数器 |
   | timeSpent | 数值 |

   >[!NOTE]
   >
   >用于配置AEM Forms Analytics的事件编号和prop编号必须与[AEM Analytics](/help/sites-administering/adobeanalytics.md)配置中使用的事件编号和prop编号不同。

1. 从Adobe Marketing Cloud帐户注销。

## 创建Cloud Service配置{#creating-cloud-service-configuration}

Cloud Service配置是有关您的Adobe Analytics帐户的信息。 配置允许Adobe Experience Manager(AEM)连接到Adobe Analytics。 为您使用的每个Analytics帐户创建单独的配置。

1. 以管理员身份登录AEM创作实例。
1. 单击左上角的&#x200B;**Adobe Experience Manager** > **工具** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **旧版Cloud Services**。
1. 找到&#x200B;**Adobe Analytics**&#x200B;图标。 单击&#x200B;**显示配置**，然后继续单击&#x200B;**[+]**&#x200B;以添加新配置。

   如果您是首次用户，请单击&#x200B;**立即配置**。

1. 向新配置中添加标题（可选填写“名称”字段）。 例如，我的分析配置。 单击&#x200B;**创建**。

1. 在配置页面上打开编辑面板时，填写以下字段：

   * **公司**:您公司在Adobe Analytics上的名称。
   * **用户名**:用于登录到Adobe Analytics的名称。
   * **密码**:上述帐户的Adobe Analytics密码。
   * **数据中心**:您的Adobe Analytics帐户的数据中心。

1. 单击&#x200B;**连接到Analytics**。 出现一个对话框，其中显示连接成功的消息。 单击&#x200B;**确定**。

## 创建Cloud Service框架{#creating-cloud-service-framework}

Adobe Analytics框架是Adobe Analytics变量和AEM变量之间的一组映射。 使用框架配置表单如何向Adobe Analytics报表填充数据。 框架与Adobe Analytics配置关联。 您可以为每个配置创建多个框架。

1. 在AEM云服务控制台上，单击Adobe Analytics下的&#x200B;**显示配置**。
1. 单击Analytics配置旁边的&#x200B;**[+]**&#x200B;链接。

   ![Adobe Analytics配置](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics配置

1. 键入框架的&#x200B;**标题**&#x200B;和&#x200B;**名称**，选择&#x200B;**Adobe Analytics**&#x200B;框架，然后单击&#x200B;**创建**。 随即会打开框架进行编辑。
1. 在侧面板的“报表包”部分中，单击&#x200B;**添加项目**，然后使用下拉列表选择框架将与之交互的报表包ID（例如，JJEsquire）。
1. 在报表包ID旁边，选择要向报表包发送信息的服务器实例。

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. 将&#x200B;**表单分析组件**&#x200B;从&#x200B;**其他**&#x200B;类别从SideKick拖动到框架上。
1. 要将Analytics变量与组件中定义的变量进行映射，请将AEM内容查找器中的变量拖动到跟踪组件上的字段。

   ![将AEM变量与Adobe Analytics变量映射](assets/analytics_new.png)

1. 使用Sidekick中的&#x200B;**页面选项卡**&#x200B;激活框架，单击&#x200B;**激活框架**。

## 配置AEM Forms Analytics配置服务{#configuring-aem-forms-analytics-configuration-service}

1. 在创作实例上，打开位于`https://<server>:<port>;/system/console/configMgr`的AEM Web控制台配置管理器。
1. 找到并打开AEM Forms Analytics配置

   ![AEM Forms Analytics配置服务](assets/analytics_configuration.png)

   AEM Forms Analytics配置服务

1. 为以下字段指定相应的值，然后单击&#x200B;**保存**。

   * **SiteCatalyst框架**:选择您在设置跟踪框架部分中定义的框架/配置。
   * **字段时间跟踪基线**:指定必须跟踪字段访问的持续时间（以秒为单位）。默认值为 0。当值大于0（零）时，将向Adobe Analytics服务器发送两个单独的跟踪事件。 第一个事件会指示Analytics服务器停止跟踪退出字段。 第二个事件在指定的持续时间过后发送。 第二个事件会指示Analytics服务器开始跟踪已访问的字段。 使用两个单独的事件有助于准确测量字段逗留的时间。 当值为0（零）时，会将单个跟踪事件发送到Adobe Analytics服务器。

   * **Analytics报表同步轮**:指定用于从Adobe Analytics获取报表的cron表达式。默认值为0 0 2 ?* *.

   * **获取报表超时：** 指定等待服务器响应Analytics报表的持续时间（以秒为单位）。默认时间为120秒。
   >[!NOTE]
   >
   >报表获取操作超时，以及指定的秒数，可能最多需要10秒。

1. 对发布实例重复步骤1-3以配置分析。

现在，您可以为表单启用分析并生成分析报表。

## 为表单或文档{#enabling-analytics-for-a-form-or-document}启用分析

1. 登录到AEM Portal，地址为`https://[hostname]:'port'`。
1. 单击&#x200B;**Forms > Forms和文档**，选择表单或文档，然后单击&#x200B;**启用Analytics**。 分析已启用。

   ![为表单或文档启用分析](assets/enable-analytics-1.png)

   为表单启用分析

   **A.启** 用Analytics按钮 **B.选** 定表单

   有关查看表单分析报表的详细信息，请参阅[查看和了解AEM Forms分析报表](../../forms/using/view-understand-aem-forms-analytics-reports.md)
