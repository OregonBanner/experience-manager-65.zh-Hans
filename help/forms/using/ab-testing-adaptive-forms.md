---
title: 创建和管理自适应表单的A/B测试
seo-title: 创建和管理自适应表单的A/B测试
description: AEM Forms与Adobe Target集成，允许运行自适应表单的A/B测试，以增强客户体验和改善转化率。
seo-description: AEM Forms与Adobe Target集成，允许运行自适应表单的A/B测试，以增强客户体验和改善转化率。
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---


# 创建和管理自适应表单的A/B测试{#create-and-manage-a-b-test-for-adaptive-forms}

## 概述 {#overview-br}

如果您的客户提供的体验不吸引人，他们可能会放弃表单。 虽然这令客户感到沮丧，但也可以增加组织的支持量和成本。 识别和提供正确的客户体验是至关重要的，也具有挑战性，可以增加转化率。 Adobe Experience Manager Forms是这个问题的关键。

AEM Forms与Adobe Marketing Cloud解决方案Adobe Target集成，跨多个数字渠道提供个性化、引人入胜的客户体验。 A/B测试是目标的关键功能之一，它允许您快速设置并发A/B测试，向目标用户展示相关内容，并识别驱动更好转化率的体验。

借助AEM Forms，您可以实时设置并运行自适应表单的A/B测试。 它还提供开箱即用、可自定义的报告功能，以可视化表单体验的实时性能，并确定可最大限度提高用户参与度和转化率的体验。

## 在AEM Forms建立和集成目标{#set-up-and-integrate-target-in-aem-forms}

在开始创建和分析自适应表单的A/B测试之前，您需要设置目标服务器并将其集成到AEM Forms。

### 设置目标{#set-up-target}

要将AEM与目标集成，请确保您拥有有效的Adobe Target帐户。 当你向Adobe Target注册时，你会收到一个客户代码。 您需要客户端代码、与目标帐户关联的电子邮件和密码才能将AEM与目标连接。

客户端代码标识Adobe Target客户帐户，并在调用Adobe Target服务器时用作URL中的子域。 在继续操作之前，请确保凭据允许您登录[https://testandtarget.omniture.com/](https://testandtarget.omniture.com/)。

### 在AEM Forms整合目标{#integrate-target-in-aem-forms}

执行以下步骤将正在运行的目标服务器与AEM Forms集成：

1. 在AEM服务器上，转到https://&lt;*hostname*:*port*/libs/cq/core/content/tools/cloudservices.html。

1. 在&#x200B;**Adobe Target**&#x200B;部分，单击&#x200B;**显示配置**，然后单击&#x200B;**+**图标以添加新配置。
如果您是第一次配置目标，请单击**立即配置。**

1. 在“创建配置”对话框中，为配置指定&#x200B;**标题**&#x200B;和（可选）**名称**。

1. 单击&#x200B;**创建**。此时将打开编辑组件对话框。
1. 指定您的目标帐户详细信息，如客户代码、电子邮件和密码。
1. 从“API类型”下拉列表中选择&#x200B;**Rest**。

1. 单击&#x200B;**连接到Adobe Target**&#x200B;以使用目标初始化连接。 如果连接成功，则显示“Connection successful（连接成功）”消息。 单击消息上的&#x200B;**OK**，然后单击对话框上的&#x200B;**OK**。 目标帐户已配置。

1. 创建目标框架，如[添加框架](/help/sites-administering/target.md)中所述。

1. 转至https://&lt;*hostname*:*port*/system/console/configMgr。

1. 单击&#x200B;**AEM Forms目标配置**。
1. 选择&#x200B;**目标框架**。
1. 在&#x200B;**目标URL**&#x200B;字段中，指定A/B测试将运行的所有URL。 例如，https://&lt;*hostname*:*port*/(对于OSGi上的AEM Forms服务器)或https://&lt;*hostname*:*port*/lc/(对于JEE上的AEM Forms服务器)。
请考虑您要为发布实例配置目标URL，并且客户可以使用主机名或IP地址访问它，您需要同时配置目标URL —— 使用主机名和IP地址。 如果只配置其中一个URL，则对于来自另一个URL的客户，将不会运行A/B测试。 单击**+**&#x200B;以指定多个URL。

1. 单击&#x200B;**保存**。

您的目标服务器已与AEM Forms集成。 如果您拥有使用Adobe Target的完整许可证，您现在可以启用A/B测试。

如果您拥有使用Adobe Target的完整许可证，在您将目标与AEM Forms集成后，请使用以下参数开始服务器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM实例在JBoss上运行，在`jboss\bin\standalone.conf.bat`文件中以从整套服务开始的服务形式启动，请在以下条目中添加-Dabtesting.enabled=true参数：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss服务器之外，您还可以在任何应用程序服务器的服务器启动脚本中添加-Dabtesting.enabled=true jvm参数。 现在，您可以创建并运行自适应表单的A/B测试。

>[!NOTE]
>
>如果稍后更新配置的目标URL，请确保更新任何正在运行的A/B测试，以便它们指向当前URL。 有关更新A/B测试的信息，请参见[更新A/B测试](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)。


## 在AEM {#create-audiences-within-aem}中创建受众

AEM允许您创建受众，并将其用于A/B测试。 您在AEM中创建的受众在AEM Forms提供。 执行以下步骤在AEM中创建受众:

1. 在创作实例中，点按&#x200B;**Adobe Experience Manager** > **个性化** > **受众**。

1. 在受众页面中，点按&#x200B;**创建受众>创建目标受众**。
1. 在“Adobe Target配置”对话框中，选择目标配置，然后单击&#x200B;**确定**。
1. 在创建新受众页中，创建规则。 规则允许您对受众分类。 例如，您希望根据操作系统对受众进行分类。 您的受众A来自Windows,受众B来自Linux。

   1. 要根据Windows对受众进行分类，请在规则#1中选择&#x200B;**OS**&#x200B;属性类型。 从“When（时间）”下拉框中，选择&#x200B;**Windows。**

   1. 要根据Linux对受众进行分类，请在规则#2中选择&#x200B;**OS**&#x200B;属性类型。 从&#x200B;**When**&#x200B;下拉框中，选择&#x200B;**Linux**，然后单击&#x200B;**Next**。

1. 为创建的受众指定名称，然后单击&#x200B;**保存**。

在为表单配置A/B测试时，可以选择受众，如下所示。

## 创建A/B测试{#create-a-b-test}

执行以下步骤以创建自适应表单的A/B测试。

1. 转到位于https://&lt;*hostname*&#x200B;的&#x200B;**Forms和文档**:&lt;*端口*/aem/forms.html/content/dam/formsanddocuments。

1. 导航到包含自适应表单的文件夹。
1. 单击工具栏中的&#x200B;**选择**&#x200B;工具，然后选择自适应表单。
1. 单击工具栏中的&#x200B;**更多**&#x200B;并选择&#x200B;**配置A/B测试**。 此时将打开“配置A/B测试”页。

[ ![自适应表单的A/B测试配置页](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. 为A/B测试指定&#x200B;**活动名称**。

1. 从“受众”下拉列表中，选择您要向其提供表单不同体验的受众。 例如，**使用Chrome的访客**。 受众列表从配置的目标服务器填充。

1. 在体验A和B的&#x200B;**体验分发**&#x200B;字段中，以百分比形式指定分发，以确定体验在总受众中的分发。 例如，如果您为体验A和B分别指定40、60，则体验A将提供给40%的受众，其余60%将看到体验B。
1. 单击&#x200B;**配置**。 将出现一个对话框，确认A/B测试的创建。
1. 单击&#x200B;**编辑体验B**&#x200B;以在编辑模式下打开自适应表单。 修改表单以创建不同于默认体验A的其他体验。体验B中允许的可能变量包括：

   * CSS或样式
   * 不同面板或同一面板中字段的顺序
   * 面板布局
   * 面板标题
   * 字段的描述、标签和帮助文本
   * 不影响或中断提交流的脚本
   * 验证（客户端和服务器端）
   * 体验B的主题。（您可以为体验B选择一个替代主题）

1. 转到Forms和文档UI，选择自适应表单，单击&#x200B;**更多**，然后选择&#x200B;**开始A/B测试**。

您的A/B测试现在正在运行，将根据指定的分布随机提供指定的受众。

## 更新A/B测试{#update-a-b-test}

您可以更新正在运行的A/B测试的受众和体验分布。 为此，请执行以下操作：

1. 在Forms语和文档语UI中，导航到包含运行A/B测试的自适应表单的文件夹。
1. 选择自适应表单。
1. 单击&#x200B;**更多**，然后选择&#x200B;**编辑A/B测试**。 此时将打开“更新A/B测试”页。

1. 根据需要更新受众和体验分发。
1. 单击&#x200B;**更新**。

## 视图和分析A/B测试报告{#view-and-analyze-a-b-test-report}

在您允许A/B测试在所需时间段内运行后，您可以生成报告并检查哪些体验已带来更好的转化。 您可以将表现更好的体验声明为入选方，或选择运行其他A/B测试。 为此，请执行以下步骤：

1. 选择自适应表单，单击&#x200B;**更多**，然后单击&#x200B;**A/B测试报告**。 将显示报告。

[ ![A/B测试报告](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. 分析报告并查看您是否有足够的数据点，将表现最好的体验之一宣布为赢家。 您可以选择继续使用同一A/B测试更多时间，或者声明一个入选方并结束A/B测试。
1. 要声明入选方并结束A/B测试，请单击报告仪表板上的&#x200B;**结束A/B测试**按钮。 对话框会提示您声明其中一个体验为入选方。 选择入选方并确认结束A/B测试。
或者，您也可以先单击相应体验的**声明入选方**&#x200B;按钮来声明入选方。 它会提示您确认入选方。 单击&#x200B;**是**&#x200B;结束A/B测试。

如果您选择了体验A作为赢家，A/B测试将结束，并且今后，只有体验A才会提供给所有受众。
