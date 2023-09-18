---
title: 创建和管理自适应表单的A/B测试
description: AEM Forms与Adobe Target集成，允许为自适应表单运行A/B测试，以增强客户体验并提高转化率。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 2%

---

# 创建和管理自适应表单的A/B测试{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE 已终止]{type=negative tooltip="此功能现已终止使用"}

<div class="preview"> 自适应表单的A/B测试功能已终止使用，不再受支持。 </div>

## 概述 {#overview-br}

如果您的表单提供的体验不吸引人，则客户可能会放弃表单。 虽然这会让客户感到沮丧，但也会增加贵组织的支持量和成本。 确定并提供提高转化率的正确客户体验是关键而富有挑战性的。 Adobe Experience Manager Forms掌握着这个问题的关键。

AEM Forms与Adobe Experience Cloud解决方案Adobe Target集成，跨多个数字渠道提供个性化且引人入胜的客户体验。 Target的一项重要功能是A/B测试，它允许您快速设置并发A/B测试，向目标用户展示相关内容，并确定可提高转化率的体验。

借助Adobe Experience Manager (AEM) Forms，您可以实时对自适应表单设置和运行A/B测试。 它还提供开箱即用和可自定义的报告功能，以可视化表单体验的实时性能，并确定可最大程度提高用户参与度和转化率的表单体验。

## 在AEM Forms中设置并集成Target {#set-up-and-integrate-target-in-aem-forms}

在开始为自适应表单创建和分析A/B测试之前，必须设置Target服务器并将其集成到AEM Forms中。

### 设置Target {#set-up-target}

要将AEM与Target集成，请确保您拥有有效的Adobe Target帐户。 当您注册Adobe Target时，您会收到一个客户端代码。 您需要客户端代码、与Target帐户关联的电子邮件和密码才能将AEM与Target连接。

客户端代码标识Adobe Target客户帐户，并在调用Adobe Target服务器时用作URL中的子域。 在继续操作之前，请登录 [https://experience.adobe.com/](https://experience.adobe.com/) 如果您有访问权限，请查看 [!DNL Adobe Target] 中的选项 [!UICONTROL 快速访问] 部分。

### 将正在运行的Target服务器与AEM Forms集成 {#integrate-target-in-aem-forms}

1. 在AEM服务器上，转到https://&lt;*主机名*>：&lt;*端口*>/libs/cq/core/content/tools/cloudservices.html.

1. 在 **Adobe Target** 部分，单击 **显示配置** 然后 **+** 图标以添加配置。
如果是首次配置目标，请单击 **立即配置。**

1. 在创建配置对话框中，指定 **标题** 和（可选） **名称** 用于配置。

1. 单击&#x200B;**创建**。将打开“编辑组件”对话框。
1. 指定您的Target帐户详细信息，如客户端代码、电子邮件和密码。
1. 选择 **Rest** 从API类型下拉列表中。

1. 单击 **连接到Adobe Target** 以便初始化与Target的连接。 如果连接成功，则将显示消息连接成功。单击消息上的&#x200B;**确定**，然后单击对话框上的&#x200B;**确定**。已配置Target帐户。

1. 创建Target框架（如所述） [添加框架](/help/sites-administering/target.md).

1. 转到https://&lt;*主机名*>：&lt;*端口*>/system/console/configMgr.

1. 单击 **AEM Forms Target配置**.
1. 选择 **目标框架**.
1. 在 **目标URL** 字段中，指定运行A/B测试的所有URL。 例如， https://&lt;*主机名*>：&lt;*端口*>/ for AEM Forms Server on OSGi或https://&lt;*主机名*>：&lt;*端口*>/lc/(适用于JEE上的AEM Forms Server)。
假定您要为发布实例配置Target URL，并且您的客户可以使用主机名或IP地址访问它。 在这种情况下，您必须将两者都配置为Target URL — 使用主机名和IP地址。 如果仅配置其中一个URL，则不会为来自其他URL的客户运行A/B测试。 单击 **+** 以指定多个URL。

1. 单击&#x200B;**保存**。

您的Target服务器已与AEM Forms集成。 如果您拥有使用Adobe Target的完整许可证，您现在可以启用A/B测试。

如果您拥有使用Adobe Target的完整许可证，则在将Target与AEM Forms集成后，请使用以下参数启动服务器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM实例在JBoss®上运行，则在 `jboss\bin\standalone.conf.bat` 文件，在以下条目中添加 — Dabtesting.enabled=true参数：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了JBoss®服务器之外，您还可以在任何应用程序服务器的服务器启动脚本中添加 — Dabtesting.enabled=true jvm参数。 现在，您可以为自适应表单创建和运行A/B测试。

>[!NOTE]
>
>如果稍后更新已配置的目标URL，请确保更新任何运行的A/B测试，使其指向当前URL。 有关更新A/B测试的信息，请参阅 [更新A/B测试](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).
>

## 在AEM中创建受众 {#create-audiences-within-aem}

AEM允许您创建受众，并将其用于A/B测试。 您在AEM中创建的受众可在AEM Forms中使用。 要在AEM中创建受众，请执行以下操作：

1. 在创作实例中，点按 **Adobe Experience Manager** > **个性化** > **受众**.

1. 在受众页面中，点按 **创建受众>创建目标受众**.
1. 在Adobe Target配置对话框中，选择Target配置，然后单击 **确定**.
1. 在创建新受众页面中，创建规则。 规则允许您对受众进行分类。 例如，您希望根据操作系统对受众进行分类。 您的受众A来自Windows，受众B来自Linux®。

   1. 要基于Windows对受众进行分类，请在规则#1中，选择 **操作系统** 属性类型。 从时间下拉列表中，选择 **Windows。**

   1. 要基于Linux®对受众进行分类，请在规则#2中，选择 **操作系统** 属性类型。 从 **时间** 下拉列表，选择 **Linux®**，然后单击 **下一个**.

1. 为创建的受众指定名称，然后单击 **保存**.

在为表单配置A/B测试时，您可以选择受众，如下所示。

## 为自适应表单创建A/B测试 {#create-a-b-test}

1. 转到 **Forms和文档** 在https://&lt;*主机名*>：&lt;*端口*>/aem/forms.html/content/dam/formsanddocuments.

1. 导航到包含自适应表单的文件夹。
1. 单击 **选择** 工具并选择自适应表单。
1. 单击 **更多** ，然后选择 **配置A/B测试**. 此时会打开配置A/B测试页面。

[](assets/ab-test-configure-1.png)

1. 指定 **活动名称** 用于A/B测试。

1. 从受众下拉列表中，选择要向其提供表单不同体验的受众。 例如， **使用Chrome的访客**. 受众列表从配置的Target服务器中填充。

1. 在 **体验分发** 体验A和B的字段，以百分比形式指定分布，以确定体验在总受众中的分布。 例如，如果分别为体验A和B指定40、60，则体验A会为40%的受众提供，其余60%会为体验B提供。
1. 单击 **配置**. 将显示一个对话框，确认创建A/B测试。
1. 单击 **编辑体验B** 以便您可以在编辑模式下打开自适应表单。 通过创建不同于默认体验A的体验来修改表单。体验B中允许的可能变体包括以下中的更改：

   * CSS或样式
   * 不同面板或同一面板中的字段顺序
   * 面板布局
   * 面板标题
   * 字段的描述、标签和帮助文本
   * 不影响或中断提交流的脚本
   * 验证（客户端和服务器端）
   * 体验B的主题。（您可以为体验B选择替代主题）

1. 转到Forms和文档UI，选择自适应表单，然后单击 **更多**，并选择 **启动A/B测试**.

您的A/B测试现在正在运行，并根据指定的分配随机向指定受众提供体验。

## 更新A/B测试 {#update-a-b-test}

您可以更新运行A/B测试的受众和体验分布。

要更新A/B测试，请执行以下操作：

1. 在Forms和文档UI中，导航到包含运行A/B测试的自适应表单的文件夹。
1. 选择自适应表单。
1. 单击 **更多** 然后选择 **编辑A/B测试**. 此时将打开更新A/B测试页面。

1. 根据需要更新受众和体验分发。
1. 单击&#x200B;**更新**。

## 查看和分析A/B测试报告 {#view-and-analyze-a-b-test-report}

在允许将A/B测试运行所需的时间段后，您可以生成报告并检查哪个体验产生了更好的转化。 您可以将表现更好的体验声明为入选者，也可以选择运行其他A/B测试。

要查看和分析A/B测试报告，请执行以下操作：

1. 选择自适应表单，单击 **更多**，然后单击 **A/B测试报告**. 此时会显示报表。

[](assets/ab-test-report-3.png)

1. 分析报表，并查看您是否有足够的数据点来将某个表现更好的体验声明为入选者。 您可以选择继续同一A/B测试更长时间，或声明入选者并结束A/B测试。
1. 要声明入选者并结束A/B测试，请单击 **结束A/B测试** 按钮进行查看。 出现一个对话框，提示您声明两个体验之一为入选体验。 选择入选者并确认结束A/B测试。
或者，您可以首先通过单击 **声明入选方** 按钮来提供相应的体验。 它会提示您确认入选者。 单击 **是** 结束A/B测试。

如果您选择体验A作为入选者，则A/B测试将终止，并且以后，只有体验A会提供给受众。
