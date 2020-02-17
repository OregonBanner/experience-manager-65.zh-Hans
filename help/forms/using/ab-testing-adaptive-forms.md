---
title: 创建和管理自适应表单的A/B测试
seo-title: 创建和管理自适应表单的A/B测试
description: AEM Forms与Adobe Target集成，它允许对自适应表单运行A/B测试，以增强客户体验并提高转化率。
seo-description: AEM Forms与Adobe Target集成，它允许对自适应表单运行A/B测试，以增强客户体验并提高转化率。
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# 创建和管理自适应表单的A/B测试{#create-and-manage-a-b-test-for-adaptive-forms}

## 概述 {#overview-br}

如果表单提供的体验不具有吸引力，您的客户可能会放弃表单。 虽然这令客户感到沮丧，但也可以增加组织的支持量和成本。 识别和提供能够提高转化率的正确客户体验至关重要，也具有挑战性。 Adobe Experience Manager Forms是解决此问题的关键。

AEM Forms与Adobe target（一种Adobe Marketing cloud解决方案）集成，跨多个数字渠道提供个性化、引人入胜的客户体验。 Target的关键功能之一是A/B测试，它允许您快速设置并发A/B测试，向目标用户展示相关内容，并识别可提高转化率的体验。

借助AEM Forms，您可以实时在自适应表单上设置和运行A/B测试。 它还提供开箱即用、可自定义的报告功能，以可视化表单体验的实时性能并识别最大化用户参与度和转化率的报表功能。

## 在AEM Forms中设置和集成Target {#set-up-and-integrate-target-in-aem-forms}

在开始创建和分析自适应表单的A/B测试之前，您需要设置Target服务器并将其集成到AEM Forms中。

### 设置目标 {#set-up-target}

要将AEM与Target集成，请确保您拥有有效的Adobe Target帐户。 当您向Adobe Target注册时，您会收到一个客户端代码。 您需要客户端代码、与Target帐户关联的电子邮件和密码才能将AEM与Target连接。

客户端代码标识Adobe Target客户帐户，并在调用Adobe Target服务器时用作URL中的子域。 在继续操作之前，请确保凭据允许您登录https://testandtarget.omniture.com/ [](https://testandtarget.omniture.com/)。

### 在AEM Forms中集成Target {#integrate-target-in-aem-forms}

执行以下步骤将正在运行的Target服务器与AEM Forms集成：

1. 在AEM服务器上，转到https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html。

1. 在 **Adobe Target部分** ，单击“显 **示配置** ”，然后 **** 单击+图标以添加新配置。
如果您是第一次配置目标，请单击“立即 **配置”。**

1. 在“创建配置”对话框中，指定 **标题** ，或指定 **配置的名称** 。

1. 单击&#x200B;**创建**。此时将打开编辑组件对话框。
1. 指定Target帐户详细信息，如客户端代码、电子邮件和密码。
1. 从“ **API类型** ”(API Type)下拉列表中选择“其余”(Rest)。

1. 单 **击“连接到Adobe Target** ”以初始化与Target的连接。 如果连接成功，则显示“连接成功”消息。 单 **击消息** “确定”，然后 **单击** “确定”。 Target帐户已配置。

1. 创建Target框架，如添加框 [架中所述](/help/sites-administering/target.md)。

1. 转到https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr。

1. 单击 **AEM Forms Target配置**。
1. 选择一 **个Target Framework**。
1. 在“ **目标URL** ”字段中，指定A/B测试将运行的所有URL。 例如，https://&lt;*hostname*>:&lt;port *>/（对于OSGi上的AEM Forms服务器）或https://&lt;* hostname *>:&lt;***portLc>/（对于JEE上的AEM Forms服务器）。
请考虑您要为发布实例配置目标URL，并且您的客户可以使用主机名或IP地址访问该URL，您需要将二者配置为目标URL —— 使用主机名和IP地址。 如果仅配置其中一个URL，则对于来自另一个URL的客户，将不会运行A/B测试。 单击 **+** 可指定多个URL。

1. 单击&#x200B;**保存**。

您的Target服务器已与AEM Forms集成。 如果您拥有使用Adobe target的完整许可证，您现在可以启用A/B测试。

如果您有使用Adobe Target的完整许可证，请在将Target与AEM Forms集成之后，使用以下参数启动服务器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM实例在JBoss上运行，从整套服务开始，在文件中，添加 `jboss\bin\standalone.conf.bat` -Dabtesting.enabled=true参数：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss服务器之外，您还可以在任何应用程序服务器的服务器启动脚本中添加-Dabtesting.enabled=true jvm参数。 现在，您可以创建并运行自适应表单的A/B测试。

>[!NOTE]
>
>如果稍后更新配置的Target URL，请确保更新任何正在运行的A/B测试，以便它们指向当前URL。 有关更新A/B测试的信息，请参 [阅更新A/B测试](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)。


## 在AEM中创建受众 {#create-audiences-within-aem}

AEM允许您创建受众，并将其用于A/B测试。 您在AEM中创建的受众可在AEM Forms中使用。 执行以下步骤以在AEM中创建受众：

1. 在创作实例中，点 **按Adobe Experience Manager** > **Personalization** > **Audiences**。

1. 在“受众”页面中，点按创 **建受众>创建目标受众**。
1. 在“Adobe Target配置”对话框中，选择Target配置，然后单击“确 **定”**。
1. 在“创建新受众”页面中，创建规则。 规则允许您对受众进行分类。 例如，您希望根据操作系统对受众进行分类。 您的受众A来自Windows，受众B来自Linux。

   1. 要根据Windows对受众进行分类，请在规则#1中选择 **OS** 属性类型。 从“时间”下拉菜单中，选择“ **Windows”。**

   1. 要根据Linux对受众进行分类，请在规则#2中选择 **OS** 属性类型。 从“时 **间** ”下拉列表中 **，选择** Linux **，然后单击“下**&#x200B;一步”。

1. 为创建的受众指定名称，然后单击“保 **存”**。

在为表单配置A/B测试时，您可以选择受众，如下所示。

## 创建A/B测试 {#create-a-b-test}

请执行以下步骤以创建自适应表单的A/B测试。

1. 转到https:// **&lt;** hostname *>:&lt;* port **>/aem/forms.html/content/dam/formsanddocuments中的“表单和文档”。

1. 导航到包含自适应表单的文件夹。
1. 单击工 **具栏中的** “选择”工具，然后选择自适应表单。
1. 单击 **工具栏** 中的“更多” **，然后选择“**&#x200B;配置A/B测试”。 此时将打开“配置A/B测试”页。

[ 自适应 ![表单的A/B测试配置页](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. 为A/ **B测试指定活动名称** 。

1. 从“受众”下拉列表中，选择要向其提供表单不同体验的受众。 例如，使用 **Chrome的访客**。 受众列表将从已配置的Target服务器填充。

1. 在体验 **A和** B的“体验分发”字段中，按百分比指定分发，以确定体验在总受众中的分发。 例如，如果您为体验A和体验B分别指定40、60，则体验A将提供给40%的受众，其余60%的受众将看到体验B。
1. 单击 **配置**。 将显示一个对话框，确认A/B测试的创建。
1. 单击 **编辑体验B** ，以在编辑模式下打开自适应表单。 修改表单以创建不同于默认体验A的体验。体验B中允许的可能变体是：

   * CSS或样式
   * 不同面板或同一面板中字段的顺序
   * 面板布局
   * 面板标题
   * 字段的描述、标签和帮助文本
   * 不影响或中断提交流的脚本
   * 验证（客户端和服务器端）
   * 体验B的主题。（您可以为体验B选择替代主题）

1. 转到“表单和文档”UI，选择自适应表单，单击“更 **多**”，然后选择“ **开始A/B测试”**。

您的A/B测试现在正在运行，将根据指定的分布随机提供特定受众。

## Update A/B test {#update-a-b-test}

您可以更新正在运行的A/B测试的受众和体验分布。 为此，请执行以下操作：

1. 在“表单和文档”UI中，导览至包含运行A/B测试的自适应表单的文件夹。
1. 选择自适应表单。
1. 单击 **更多** ，然后选择 **编辑A/B测试**。 此时将打开“更新A/B测试”页。

1. 根据需要更新受众和体验分发。
1. Click **Update**.

## 查看和分析A/B测试报告 {#view-and-analyze-a-b-test-report}

在您允许A/B测试在所需时间段内运行后，您可以生成报告并检查哪种体验提高了转化率。 您可以声明性能更好的体验为入选方，或选择运行其他A/B测试。 为此，请执行以下步骤：

1. 选择自适应表单，单击 **更多**，然后单击 **A/B测试报告**。 将显示报告。

[ ![A/B测试报告](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. 分析报告并查看您是否有足够的数据点，以将表现最好的体验之一声明为赢家。 您可以选择继续同一A/B测试更多时间，或声明入选方并结束A/B测试。
1. 要声明入选方并结束A/B测试，请单击报 **告功能板上的“结束A/B测试** ”按钮。 对话框会提示您声明其中一个体验为入选方。 选择入选方并确认结束A/B测试。
或者，您也可以首先单击相应体验的“声 **明入选方** ”按钮来声明入选方。 它会提示您确认入选方。 单击 **是** ，结束A/B测试。

如果您选择了体验A作为赢家，A/B测试将结束，并且今后，只向所有受众提供体验A。
