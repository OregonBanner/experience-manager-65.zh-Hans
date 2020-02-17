---
title: 配置分析和报告
seo-title: 配置分析和报告
description: 了解如何配置Adobe Analytics，以发现用户在使用自适应表单、自适应文档和HTML5表单时面临的交互模式和问题。
seo-description: 了解如何配置Adobe Analytics，以发现用户在使用自适应表单、自适应文档和HTML5表单时面临的交互模式和问题。
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 配置分析和报告{#configuring-analytics-and-reports}

AEM Forms与Adobe Analytics集成，使您能够捕获和跟踪已发布表单和文档的性能指标。 分析这些指标的目的是根据使表单或文档更易用所需的更改数据做出明智决策。

>[!NOTE]
>
>AEM Forms中的分析功能可作为AEM Forms加载项包的一部分使用。 有关安装加载项包的信息，请参 [阅安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。
>
>除了加载项包，您还需要AEM实例的Adobe Analytics帐户和管理员权限。 有关该解决方案的信息，请参 [阅Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

## 概述 {#overview}

您可以使用Adobe Analytics发现用户在使用自适应表单、HTML5表单和交互式通信时所面临的交互模式和问题。 开箱即用地，Adobe分析会跟踪和存储有关以下参数的信息：

* **平均填充时间**:填写表单的平均时间。
* **再现**:表单的打开次数。
* **草稿**:表单在草稿状态中保存的次数。
* **提交**:提交表单的次数。
* **中止**:用户在未填写表单的情况下离开的次数。

您可以自定义Adobe Analytics以添加／删除更多参数。 除了上述信息，报告还包含有关HTML5和自适应表单的每个面板的以下信息：

* **时间**:在面板和面板字段上所花费的时间。
* **错误**:面板和面板字段上遇到的错误数。
* **帮助**:用户打开面板帮助和面板字段的次数。

## 创建报告套件 {#creating-report-suite}

分析数据存储在称为报表包的客户特定存储库中。 要创建报表包并使用Adobe Analytics，您必须拥有有效的Adobe Marketing cloud帐户。 在执行以下步骤之前，请确保您拥有有效的Adobe Marketing cloud帐户。

执行以下步骤以创建报表包。

1. 登录网 [址：https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. 在Marketing cloud中，选择“管 **理员** ”>“管 **理控制台** ” **>“报**&#x200B;表包”。
1. 在“ **报表包管理器** ”中 **选择“新建”** > “报表包”。

   ![创建新的报告套件](assets/newreportsuite_new.png)

   创建新的报告套件

1. 确保第一个下拉列表设置为“从模 **板创建”** ，然后选择“商 **务”**。
1. 找到报 **表包ID字段** ，然后添加新的报表包ID。 例如，JJEsquire。 报表包ID显示在报表包ID字段的下方。 它包含一个自动前缀，通常是公司名称。
1. 添加新 **站点标题**。 例如，JJEsquire Getting Started Suite。 此标题在Analytics UI中使用。 在代码中使用报表包ID。
1. 从下拉 **菜单中选择时区** 。 此报表包中的所有数据都将根据定义的时区进行记录。
1. 将“基 **本URL** ”和“默 **认页面** ”字段留空。 这两个值只能从Adobe Marketing cloud界面中用于链接到您的网站。
1. 将“开始 **生效日期** ”设置为今天。 起始日期决定激活报表包的日期。
1. 在“估 **计的每日页面查看次数** ”字段中，键入100。 使用此字段可估计您预计的网站每天的页面查看次数。 这一估计使Adobe能够部署适当数量的硬件来处理您要收集的数据。
1. 从下拉 **菜单中选择基本货币** 。 此报表包中的所有货币数据都将转换并存储为此货币格式。
1. 单击 **创建报告** Suite。 您应当看到页面刷新，并显示一条消息，告知您的报表包已成功创建。
1. 选择新创建的报表包。 导航到“编 **辑设置** ”>“ **常规** ” **>“**&#x200B;常规帐户设置”。

   ![常规帐户设置](assets/geographic_settings.png)

   常规帐户设置

1. 在“常规帐户设置”屏幕中，启用“地 **理位置报告**”，然后单击“ **保存”。**
1. 导航到编 **辑设置** > **流量** > **流量变量**。
1. 在报表包中，配置并启用以下流量变量。

   * **formName**:自适应表单的标识符。
   * **formInstance**:自适应表单实例的标识符。 为此变量启用路径报告。
   * **fieldName**:自适应表单字段的标识符。 为此变量启用路径报告。
   * **panelName**:自适应表单面板的标识符。 为此变量启用路径报告。
   * **formTitle**:表单的标题。
   * **fieldTitle**:表单字段的标题。
   * **panelTitle**:表单面板的标题。
   * **analyticsVersion**:表单分析版本。

1. 导航到编 **辑设置** >转 **化** >成 **功事件**。 定义并启用以下成功事件：

   | 成功事件 | 类型 |
   |---|---|
   | 放弃 | 计数器 |
   | 渲染 | 计数器 |
   | panel访问 | 计数器 |
   | fieldVisit | 计数器 |
   | 保存 | 计数器 |
   | 错误 | 计数器 |
   | 帮助 | 计数器 |
   | 提交 | 计数器 |
   | timeSpent | 数值 |

   >[!NOTE]
   >
   >用于配置AEM Forms分析的事件编号和属性编号必须与 [AEM分析配置中使用的事件编号和属性编号](/help/sites-administering/adobeanalytics.md) 不同。

1. 注销Adobe Marketing cloud帐户。

## 创建云服务配置 {#creating-cloud-service-configuration}

云服务配置是关于您的Adobe Analytics帐户的信息。 此配置使Adobe Experience Manager(AEM)能够连接到Adobe Analytics。 为您使用的每个Analytics帐户创建单独的配置。

1. 以管理员身份登录到您的AEM作者实例。
1. 在左上角，单击“ **Adobe Experience Manager** ”>“工具 **”** >“部署 ![](/help/forms/using/assets/tools.png) ” ********>“云服务”。
1. 找到 **Adobe Analytics图标** 。 单击 **显示配置** ，然后继续单击 **[]** +以添加新配置。

   如果您是首次使用者，请单击“立即 **配置”**。

1. 为新配置添加标题（填写名称字段是可选的）。 例如，我的分析配置。 单击&#x200B;**创建**。

1. 当“编辑”面板在配置页面上打开时，填写以下字段：

   * **公司**:您公司在Adobe Analytics中的特色名称。
   * **用户名**:用于登录Adobe Analytics的名称。
   * **密码**:上述帐户的Adobe Analytics密码。
   * **数据中心**:Adobe Analytics帐户的数据中心。

1. 单击 **“连接到分析”**。 将显示一个对话框，其中显示连接成功的消息。 单击&#x200B;**确定**。

## 创建云服务框架 {#creating-cloud-service-framework}

Adobe Analytics框架是Adobe Analytics变量与AEM变量之间的一组映射。 使用框架配置表单如何将数据填充到Adobe Analytics报告。 框架与Adobe Analytics配置相关联。 您可以为每个配置创建多个框架。

1. 在AEM云服务控制台上，单击“Adobe **Analytics”下的**“显示配置”。
1. 单击 **[Analytics配置旁]** 的+链接。

   ![Adobe Analytics配置](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics配置

1. 键入框 **架的标题****和名称** ，选择 **Adobe Analytics** Framework，然后单 ****&#x200B;击创建CreateCreate。 将打开框架进行编辑。
1. 在侧面窗格的“报表包”部分，单击“添加项目 ****”，然后使用下拉框架选择框架将与之交互的报表包ID（例如，JJEsquire）。
1. 在报表包ID旁，选择要向报表包发送信息的服务器实例。

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. 将表 **单分析组件从** SideKick的 **其他类别拖** 放到框架上。
1. 要将Analytics变量与组件中定义的变量进行映射，请将变量从AEM内容查找器拖到跟踪组件上的字段上。

   ![将AEM变量与Adobe Analytics变量映射](assets/analytics_new.png)

1. 使用Sidekick中的页面选 **项卡激活框架** ，单击 **激活框架**。

## 配置AEM Forms Analytics配置服务 {#configuring-aem-forms-analytics-configuration-service}

1. 在创作实例上，打开AEM Web Console配置管理器(位于 `https://<server>:<port>;/system/console/configMgr`)。
1. 找到并打开AEM Forms分析配置

   ![AEM Forms Analytics配置服务](assets/analytics_configuration.png)

   AEM Forms Analytics配置服务

1. 为以下字段指定相应的值，然后单击“保 **存”**。

   * **SiteCatalyst Framework**:在设置跟踪框架部分中选择您定义的框架／配置。
   * **字段时间跟踪基准**:指定持续时间（以秒为单位），之后必须跟踪字段访问。 默认值为 0。当值大于0（零）时，将向Adobe Analytics服务器发送两个单独的跟踪事件。 第一个事件指示分析服务器停止跟踪退出的字段。 第二个事件在经过指定的持续时间后发送。 第二个事件指示分析服务器开始跟踪已访问字段。 使用两个单独的事件有助于准确测量在字段上花费的时间。 当值为0（零）时，单个跟踪事件将发送到Adobe Analytics服务器。

   * **分析报告同步cron**:指定从Adobe Analytics获取报告的cron表达式。 默认值是0 0 2 ?* *.

   * **** 提取报告超时：指定等待服务器响应分析报告的持续时间（以秒为单位）。 默认时间为120秒。
   >[!NOTE]
   >
   >超时报告提取操作和指定的秒数可能需要多达10秒的时间。

1. 对发布实例重复第1-3步以配置分析。

现在，您可以启用表单分析并生成分析报告。

## 为表单或文档启用分析 {#enabling-analytics-for-a-form-or-document}

1. 登录到AEM门户，网址为 `https://[hostname]:[port]`。
1. 单击 **表单>表单和文档**，选择表单或文档，然后单击启用 **分析**。 分析已启用。

   ![为表单或文档启用分析](assets/enable-analytics-1.png)

   为表单启用分析

   ******答：“启用分析”按**&#x200B;钮B。所选表单

   有关查看表单分析报告的详细信息，请参阅查 [看和了解AEM表单分析报告](../../forms/using/view-understand-aem-forms-analytics-reports.md)

