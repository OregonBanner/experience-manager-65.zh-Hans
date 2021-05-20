---
title: 创建和管理自适应表单的A/B测试
seo-title: 创建和管理自适应表单的A/B测试
description: AEM Forms与Adobe Target集成，后者允许运行自适应表单的A/B测试，以增强客户体验并提高转化率。
seo-description: AEM Forms与Adobe Target集成，后者允许运行自适应表单的A/B测试，以增强客户体验并提高转化率。
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 创建和管理自适应表单的A/B测试{#create-and-manage-a-b-test-for-adaptive-forms}

## 概述 {#overview-br}

如果您的客户交付的体验没有吸引人，则他们可能会放弃表单。 虽然这令客户感到沮丧，但也会提高贵组织的支持量和成本。 确定并提供正确的客户体验以提高转化率，这一点既重要，也极具挑战性。 Adobe Experience Manager Forms是这个问题的关键。

AEM Forms与Adobe Marketing Cloud解决方案Adobe Target集成，以跨多个数字渠道提供个性化且引人入胜的客户体验。 Target的一个关键功能是A/B测试，该功能允许您快速设置并发A/B测试，向目标用户显示相关内容，并识别可提高转化率的体验。

借助AEM Forms，您可以实时对自适应表单设置和运行A/B测试。 它还提供了开箱即用、可自定义的报告功能，以可视化表单体验的实时性能，并确定可最大化用户参与和转化的体验。

## 在AEM Forms中设置和集成Target {#set-up-and-integrate-target-in-aem-forms}

在开始创建和分析自适应表单的A/B测试之前，您需要设置Target服务器并将其集成到AEM Forms中。

### 设置目标{#set-up-target}

要将AEM与Target集成，请确保您拥有有效的Adobe Target帐户。 在Adobe Target注册后，您会收到一个客户端代码。 您需要客户端代码、与Target帐户关联的电子邮件以及将AEM与Target连接的密码。

客户端代码可标识Adobe Target客户帐户，并在调用Adobe Target服务器时在URL中用作子域。 在继续操作之前，请确保您的凭据允许您登录[https://testandtarget.omniture.com/](https://testandtarget.omniture.com/)。

### 在AEM Forms中集成Target {#integrate-target-in-aem-forms}

执行以下步骤，将正在运行的Target服务器与AEM Forms集成：

1. 在AEM服务器上，转到https://*hostname*>:*port*>/libs/cq/core/content/tools/cloudservices.html。

1. 在&#x200B;**Adobe Target**&#x200B;部分中，单击&#x200B;**显示配置**，然后单击&#x200B;**+**图标以添加新配置。
如果您是首次配置目标，请单击**立即配置。**

1. 在创建配置对话框中，为配置指定&#x200B;**标题**&#x200B;和可选的&#x200B;**名称**。

1. 单击&#x200B;**创建**。此时将打开编辑组件对话框。
1. 指定您的Target帐户详细信息，如客户端代码、电子邮件和密码。
1. 从“API类型”下拉列表中选择&#x200B;**Rest**。

1. 单击&#x200B;**连接到Adobe Target**&#x200B;以初始化与Target的连接。 如果连接成功，则会显示“连接成功”消息。 在消息上单击&#x200B;**OK**，然后在对话框上单击&#x200B;**OK**。 Target帐户已配置。

1. 按照[Add a framework](/help/sites-administering/target.md)中所述创建Target框架。

1. 转到https://*hostname*>:*port*>/system/console/configMgr。

1. 单击&#x200B;**AEM Forms Target配置**。
1. 选择&#x200B;**目标框架**。
1. 在&#x200B;**目标URL**&#x200B;字段中，指定将运行A/B测试的所有URL。 例如， https://*hostname*>:&lt;*端口*>/(适用于OSGi上的AEM Forms服务器)或https://&lt;*主机名*>:*端口*>/lc/(适用于JEE上的AEM Forms服务器)。
假定您要为发布实例配置Target URL，并且客户可以使用主机名或IP地址访问该URL，则您需要同时配置为Target URL — 使用主机名和IP地址。 如果您仅配置其中一个URL，则不会为来自其他URL的客户运行A/B测试。 单击**+**&#x200B;以指定多个URL。

1. 单击&#x200B;**保存**。

您的Target服务器已与AEM Forms集成。 现在，如果您拥有使用Adobe Target的完整许可证，则可以启用A/B测试。

如果您拥有使用Adobe Target的完整许可证，请在将Target与AEM Forms集成后，使用以下参数启动服务器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM实例在JBoss上运行，从`jboss\bin\standalone.conf.bat`文件的整套服务中启动，请在以下条目中添加 — Dabtesting.enabled=true参数：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss服务器之外，您还可以在任何应用程序服务器的服务器启动脚本中添加 — Dabtesting.enabled=true jvm参数。 现在，您可以创建并运行自适应表单的A/B测试。

>[!NOTE]
>
>如果您稍后更新配置的Target URL，请确保更新任何正在运行的A/B测试，以便它们指向当前URL。 有关更新A/B测试的信息，请参阅[更新A/B测试](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)。


## 在AEM {#create-audiences-within-aem}中创建受众

AEM允许您创建受众，并将其用于A/B测试。 您在AEM中创建的受众在AEM Forms中可用。 执行以下步骤以在AEM中创建受众：

1. 在创作实例中，点按&#x200B;**Adobe Experience Manager** > **个性化** > **受众**。

1. 在“受众”页面中，点按&#x200B;**创建受众>创建目标受众**。
1. 在Adobe Target配置对话框中，选择Target配置，然后单击&#x200B;**确定**。
1. 在创建新受众页面中，创建规则。 规则允许您对受众进行分类。 例如，您要根据操作系统对受众进行分类。 受众A来自Windows，受众B来自Linux。

   1. 要根据Windows对受众进行分类，请在规则#1中，选择&#x200B;**OS**&#x200B;属性类型。 从“时间”下拉菜单中，选择&#x200B;**Windows。**

   1. 要根据Linux对受众进行分类，请在规则#2中，选择&#x200B;**OS**&#x200B;属性类型。 从&#x200B;**When**&#x200B;下拉列表中，选择&#x200B;**Linux**，然后单击&#x200B;**Next**。

1. 指定已创建受众的名称，然后单击&#x200B;**保存**。

在为表单配置A/B测试时，您可以选择受众，如下所示。

## 创建A/B测试{#create-a-b-test}

执行以下步骤为自适应表单创建A/B测试。

1. 转到&#x200B;**Forms &amp; Documents**(https://*hostname*>):*port*>/aem/forms.html/content/dam/formsanddocuments。

1. 导航到包含自适应表单的文件夹。
1. 单击工具栏中的&#x200B;**选择**&#x200B;工具，然后选择自适应表单。
1. 单击工具栏中的&#x200B;**更多**，然后选择&#x200B;**配置A/B测试**。 此时会打开配置A/B测试页面。

[ ](assets/ab-test-configure-1.png)

1. 为A/B测试指定&#x200B;**活动名称**。

1. 从“受众”下拉列表中，选择您要向其提供表单不同体验的受众。 例如，使用Chrome的&#x200B;**访客**。 受众列表由配置的Target服务器填充。

1. 在体验A和B的&#x200B;**体验分发**&#x200B;字段中，以百分比形式指定分发，以确定体验在总受众中的分发。 例如，如果您为体验A和B分别指定40、60，则体验A将提供给40%的受众，其余60%的受众将看到体验B。
1. 单击&#x200B;**配置**。 将显示一个对话框，确认创建A/B测试。
1. 单击&#x200B;**编辑体验B**&#x200B;以在编辑模式下打开自适应表单。 修改表单以创建与默认体验A不同的体验。体验B中允许的可能变体包括：

   * CSS或样式
   * 不同面板或同一面板中的字段顺序
   * 面板布局
   * 面板标题
   * 字段的描述、标签和帮助文本
   * 不影响或中断提交流程的脚本
   * 验证（客户端和服务器端）
   * 体验B的主题。（您可以为体验B选择替代主题）

1. 转到Forms和文档UI，选择自适应表单，单击&#x200B;**更多**，然后选择&#x200B;**启动A/B测试**。

您的A/B测试现在正在运行，并且将根据指定的分发随机向指定的受众提供体验。

## 更新A/B测试{#update-a-b-test}

您可以更新运行的A/B测试的受众和体验分布。 为此，请执行以下操作：

1. 在Forms和文档UI中，导航到包含运行A/B测试的自适应表单的文件夹。
1. 选择自适应表单。
1. 单击&#x200B;**更多**，然后选择&#x200B;**编辑A/B测试**。 此时会打开更新A/B测试页面。

1. 根据需要更新受众和体验分发。
1. 单击&#x200B;**Update**。

## 查看并分析A/B测试报告{#view-and-analyze-a-b-test-report}

在允许A/B测试在所需的时间段内运行后，您可以生成报表并检查哪个体验改善了转化。 您可以将性能较好的体验声明为入选者，或选择运行另一个A/B测试。 为此，请执行以下步骤：

1. 选择自适应表单，单击&#x200B;**更多**，然后单击&#x200B;**A/B测试报表**。 随即会显示报表。

[ ](assets/ab-test-report-3.png)

1. 分析报表，并查看您是否有足够的数据点来声明哪个体验的入选效果最好。 您可以选择继续同一A/B测试更长时间，或声明入选者并结束A/B测试。
1. 要声明入选者并结束A/B测试，请单击报表仪表板上的&#x200B;**结束A/B测试**按钮。 出现一个对话框，提示您将两个体验之一声明为入选者。 选择一个入选者并确认结束A/B测试。
或者，您也可以先通过单击相应体验的**声明入选者**&#x200B;按钮来声明入选者。 它会提示您确认入选者。 单击&#x200B;**Yes**&#x200B;以结束A/B测试。

如果您选择体验A作为入选者，则A/B测试将结束，并且今后，只会向所有受众提供体验A。
