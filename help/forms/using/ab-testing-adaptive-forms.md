---
title: 创建和管理自适应表单的A/B测试
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms与Adobe Target集成，允许为自适应表单运行A/B测试，以增强客户体验并提高转化率。
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 45ca98ffb68e1e31e2f45f352e86f5aa1b6f0f00
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 2%

---

# 创建和管理自适应表单的A/B测试{#create-and-manage-a-b-test-for-adaptive-forms}

## 概述 {#overview-br}

如果表单提供的体验不吸引人，您的客户可能会放弃表单。 虽然这令客户感到沮丧，但也可能会增加贵组织的支持数量和成本。 确定并提供提高转化率的正确客户体验既关键又具有挑战性。 Adobe Experience Manager Forms掌握着这个问题的关键。

AEM Forms与Adobe Marketing Cloud解决方案Adobe Target集成，跨多个数字渠道提供个性化且富有吸引力的客户体验。 Target的一项重要功能是A/B测试，它允许您快速设置并发A/B测试，向目标用户展示相关内容，以及确定提高转化率的体验。

借助AEM Forms，您可以实时设置自适应表单并运行A/B测试。 它还提供现成且可自定义的报告功能，以可视化表单体验的实时性能，并找出能提高用户参与度和转化率的体验。

## 在AEM Forms中设置并集成Target {#set-up-and-integrate-target-in-aem-forms}

在开始为自适应表单创建和分析A/B测试之前，您需要设置Target服务器并将其集成到AEM Forms中。

### 设置Target {#set-up-target}

要将AEM与Target集成，请确保您拥有有效的Adobe Target帐户。 当您注册Adobe Target时，您将收到一个客户端代码。 您需要客户端代码、与Target帐户关联的电子邮件和密码才能将AEM与Target连接。

客户端代码标识Adobe Target客户帐户，并在调用Adobe Target服务器时用作URL中的子域。 在继续操作之前，请登录 [https://experience.adobe.com/](https://experience.adobe.com/) 如果您有访问权限，请查看 [!DNL Adobe Target] 中的选项 [!UICONTROL 快速访问] 部分。

### 在AEM Forms中集成Target {#integrate-target-in-aem-forms}

执行以下步骤，将正在运行的Target服务器与AEM Forms集成：

1. 在AEM服务器上，转到https://&lt;*主机名*>：&lt;*端口*>/libs/cq/core/content/tools/cloudservices.html.

1. 在 **Adobe Target** 部分，单击 **显示配置** 然后 **+** 图标以添加新配置。
如果是首次配置Target，请单击 **立即配置。**

1. 在创建配置对话框中，指定 **标题** 和（可选） **名称** 用于配置。

1. 单击&#x200B;**创建**。将打开“编辑组件”对话框。
1. 指定您的Target帐户详细信息，如客户端代码、电子邮件和密码。
1. 选择 **Rest** 从API类型下拉列表中。

1. 单击&#x200B;**连接到 Adobe Target** 可初始化与 Target 的连接。如果连接成功，则将显示消息连接成功。单击消息上的&#x200B;**确定**，然后单击对话框上的&#x200B;**确定**。已配置Target帐户。

1. 按照中的说明创建Target框架 [添加框架](/help/sites-administering/target.md).

1. 转到https://&lt;*主机名*>：&lt;*端口*>/system/console/configMgr.

1. 单击 **AEM Forms Target配置**.
1. 选择 **目标框架**.
1. 在 **目标URL** 字段，指定将运行A/B测试的所有URL。 例如， https://&lt;*主机名*>：&lt;*端口*>/ (对于OSGi上的AEM Forms服务器)或https://&lt;*主机名*>：&lt;*端口*>/lc/(适用于JEE上的AEM Forms服务器)。
假定您要为发布实例配置Target URL，并且您的客户可以使用主机名或IP地址访问它，则您需要将两者配置为目标URL — 使用主机名和IP地址。 如果您只配置其中一个URL，则不会为来自另一个URL的客户运行A/B测试。 单击 **+** 以指定多个URL。

1. 单击“**保存**”。

您的Target服务器已与AEM Forms集成。 如果您拥有使用Adobe Target的完整许可证，您现在可以启用A/B测试。

如果您拥有使用Adobe Target的完整许可证，则在将Target与AEM Forms集成后，请使用以下参数启动服务器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM实例在JBoss上运行，则在 `jboss\bin\standalone.conf.bat` 文件，请在以下条目中添加 — Dabtesting.enabled=true参数：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss服务器之外，您还可以为任何应用程序服务器在服务器启动脚本中添加 — Dabtesting.enabled=true jvm参数。 现在，您可以为自适应表单创建和运行A/B测试。

>[!NOTE]
>
>如果稍后更新已配置的目标URL，请确保更新任何正在运行的A/B测试，以便它们指向当前URL。 有关更新A/B测试的信息，请参阅 [更新A/B测试](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).

## 在AEM中创建受众 {#create-audiences-within-aem}

AEM允许您创建受众，并将其用于A/B测试。 您在AEM中创建的受众可在AEM Forms中使用。 执行以下步骤可在AEM中创建受众：

1. 在创作实例中，点按 **Adobe Experience Manager** > **个性化** > **受众**.

1. 在“受众”页面中，点按 **创建受众>创建目标受众**.
1. 在Adobe Target配置对话框中，选择Target配置，然后单击 **确定**.
1. 在创建新受众页面中，创建规则。 规则允许您对受众进行分类。 例如，您希望根据操作系统对受众进行分类。 受众A来自Windows，受众B来自Linux。

   1. 要根据Windows对受众进行分类，请在规则#1中，选择 **操作系统** 属性类型。 从时间下拉列表中，选择 **Windows。**

   1. 要基于Linux对受众进行分类，请在规则#2中，选择 **操作系统** 属性类型。 从 **时间** 下拉列表，选择 **Linux**，然后单击 **下一个**.

1. 为创建的受众指定名称，然后单击 **保存**.

在为表单配置A/B测试时，您可以选择受众，如下所示。

## 创建A/B测试 {#create-a-b-test}

执行以下步骤可为自适应表单创建A/B测试。

1. 转到 **Forms和文档** 在https://&lt;*主机名*>：&lt;*端口*>/aem/forms.html/content/dam/formsanddocuments.

1. 导航到包含自适应表单的文件夹。
1. 单击 **选择** 工具栏中的工具并选择自适应表单。
1. 单击 **更多** 在工具栏中，然后选择 **配置A/B测试**. 此时会打开配置A/B测试页面。

[ ](assets/ab-test-configure-1.png)

1. 指定 **活动名称** A/B测试。

1. 从“受众”下拉列表中，选择要向其提供不同表单体验的受众。 例如， **使用Chrome的访客**. 受众列表是从配置的Target服务器中填充的。

1. 在 **Experience Distribution** 体验A和B的字段，以百分比形式指定分布，以确定体验在总受众中的分布。 例如，如果分别为体验A和B指定40、60，则体验A将面向40%的受众提供，其余60%将看到体验B。
1. 单击 **配置**. 此时将显示一个对话框，用于确认创建A/B测试。
1. 单击 **编辑体验B** 以在编辑模式下打开自适应表单。 修改表单以创建与默认体验A不同的体验。体验B中允许的可能变体包括以下中的更改：

   * CSS或样式
   * 不同面板或同一面板中的字段顺序
   * 面板布局
   * 面板标题
   * 字段的描述、标签和帮助文本
   * 不影响或中断提交流的脚本
   * 验证（客户端和服务器端）
   * 体验B的主题。（您可以为体验B选择替代主题）

1. 转到Forms和文档UI，选择自适应表单，然后单击 **更多**，并选择 **启动A/B测试**.

您的A/B测试当前正在运行，系统会根据指定的分布随机向指定的受众提供体验。

## 更新A/B测试 {#update-a-b-test}

您可以更新正在运行的A/B测试的受众和体验分布。 为此，请执行以下操作：

1. 在Forms &amp; Documents UI中，导航到包含运行A/B测试的自适应表单的文件夹。
1. 选择自适应表单。
1. 单击 **更多** 然后选择 **编辑A/B测试**. 此时会打开更新A/B测试页面。

1. 根据需要更新受众和体验分发。
1. 单击&#x200B;**更新**。

## 查看和分析A/B测试报告 {#view-and-analyze-a-b-test-report}

在允许A/B测试在所需的时段运行后，您可以生成报告并检查哪个体验产生了更好的转化。 您可以将表现更好的体验声明为入选者，也可以选择运行其他A/B测试。 为此，请执行以下步骤：

1. 选择自适应表单，单击 **更多**，然后单击 **A/B测试报告**. 此时将显示报告。

[ ](assets/ab-test-report-3.png)

1. 分析报表并查看您是否有足够的数据点将其中一个性能更好的体验声明为入选者。 您可以选择继续使用同一A/B测试更长时间，或者声明入选者并结束A/B测试。
1. 要声明入选者并结束A/B测试，请单击 **结束A/B测试** 按钮进行修改。 此时会出现一个对话框，提示您将两个体验之一声明为入选体验。 选择入选者，并确认结束A/B测试。
或者，您可以首先通过单击 **声明入选者** 按钮来显示相应的体验。 它会提示您确认入选者。 单击 **是** 以结束A/B测试。

如果您选择体验A作为入选者，A/B测试将终止，并且以后，只有体验A会提供给所有受众。
