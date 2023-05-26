---
title: 在AEM中创建Adobe Campaign Forms
description: AEM允许您创建和使用与您网站上的Adobe Campaign交互的表单。 可以将特定字段插入表单并映射到Adobe Campaign数据库。
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# 在AEM中创建Adobe Campaign Forms{#creating-adobe-campaign-forms-in-aem}

AEM允许您创建和使用与您网站上的Adobe Campaign交互的表单。 可以将特定字段插入表单并映射到Adobe Campaign数据库。

您可以管理新的联系人订阅、退订和用户配置文件数据，同时将其数据集成到您的Adobe Campaign数据库中。

要在AEM中使用Adobe Campaign表单，您需要按照本文档中描述的以下步骤操作：

1. 使模板可用。
1. 创建表单。
1. 编辑表单内容。

默认情况下，提供了三种特定于Adobe Campaign的表单类型：

* 保存配置文件
* 订购服务
* 取消订阅服务

这些表单定义一个URL参数，该参数接受Adobe Campaign配置文件的加密主密钥。 根据此URL参数，表单会更新关联Adobe Campaign配置文件的数据。

尽管单独创建这些表单，但在典型用例中，您会在新闻稿内容中生成指向表单页面的个性化链接，以便收件人可以打开该链接并对其配置文件数据进行调整（无论是取消订阅、订阅还是更新其配置文件）。

表单会根据用户自动更新。 参见 [编辑表单内容](#editing-form-content) 了解更多信息。

## 使模板可用 {#making-a-template-available}

在能够创建特定于Adobe Campaign的表单之前，必须在AEM应用程序中提供各种模板。

要执行此操作，请参阅 [模板文档](/help/sites-developing/page-templates-static.md#templateavailability).

首先，检查创作实例和发布实例之间的连接，确保Adobe Campaign正常运行。 参见 [与Adobe Campaign Standard集成](/help/sites-administering/campaignstandard.md) 或 [与Adobe Campaign 6.1集成](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>确保 **acMapping** 页面上的属性 **jcr：content** 节点设置为 **mapRecipient** 或 **个人资料** 分别使用Adobe Campaign 6.1.x或Adobe Campaign Standard时

### 创建表单 {#creating-a-form}

1. 在siteadmin中启动。
1. 滚动浏览树结构以转到您要在所选网站中创建表单的位置。
1. 选择 **新** > **新建页面……**.
1. 选择 **Adobe Campaign配置文件(AC 6.1)** 或 **Adobe Campaign配置文件(ACS)** 模板并输入页面属性。

   >[!NOTE]
   >
   >如果模板不可用，请参阅 [使模板可用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) 部分。

1. 单击 **创建** 以创建表单。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   然后，您可以 [编辑和配置表单内容](#editing-form-content).

## 编辑表单内容 {#editing-form-content}

专门用于Adobe Campaign的Forms具有特定的组件。 这些组件允许您选择将表单的每个字段链接到Adobe Campaign数据库中的字段。

>[!NOTE]
>
>如果所需的模板不可用，请参阅 [使模板可用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

此部分仅详细介绍指向Adobe Campaign的特定链接。 有关如何在Adobe Experience Manager中使用表单的更一般概述的更多信息，请参阅 [Editmode组件](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. 导航到要编辑的表单。
1. 在工具箱中，选择 **页面** > **页面属性……** 然后转到 **Cloud Services** 选项卡。
1. 通过单击添加Adobe Campaign服务 **添加服务**，然后在服务的下拉列表中选择与您的Adobe Campaign实例对应的配置。 在设置实例之间的连接时执行此配置。 有关更多信息，请参阅 [将AEM连接到Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >如有必要，单击挂锁图标可解锁配置，以便能够添加Adobe Campaign服务。

1. 使用访问表单的常规参数 **编辑** 在表单开头找到的按钮。 此 **表单** 选项卡允许您选择在验证表单后用户将被重定向到的感谢页面。

   此 **高级** 表单允许您选择表单类型。 此 **帖子选项** 字段允许您在三种类型的Adobe Campaign表单之间进行选择：

   * **Adobe Campaign：保存配置文件**：用于在Adobe Campaign中创建或更新收件人（默认值）。
   * **Adobe Campaign：订阅服务**：用于在Adobe Campaign中管理收件人的订阅。
   * **Adobe Campaign：取消订阅服务**：用于在Adobe Campaign中取消收件人的订阅。

   此 **操作配置** 字段可让您指定是否希望在Adobe Campaign数据库中创建收件人配置文件（如果该配置文件不存在）。 要执行此操作，请查看 **创建用户（如果不存在）** 选项。

1. 通过将所选组件从工具箱中拖放到表单中，来添加这些组件。 有关可用的Adobe Campaign特定组件的更多信息，请参阅 [Adobe表单组件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 通过双击添加的字段来配置它们。 此 **Adobe Campaign** 选项卡，用于将字段链接到Adobe Campaign收件人表中的字段。 您还可以指定字段是否为协调键值的一部分，该协调键值允许识别Adobe Campaign数据库中已存在的收件人。

   >[!CAUTION]
   >
   >此 **元素名称** 每个表单字段必须不同。 根据需要进行更改。
   >
   >每个表单必须包含 **加密的主密钥** 组件，以便在Adobe Campaign数据库中正确管理收件人。

1. 通过选择激活页面 **页面** > **激活页面** 在工具箱里。 页面已在您的网站上激活。 您可以通过转到AEM发布实例来查看它。 验证表单后，Adobe Campaign数据库中的数据即会更新。

## 测试表单 {#testing-a-form}

在创建表单并编辑表单内容后，您可能需要手动测试表单是否按预期工作。

>[!NOTE]
>
>您必须拥有 **加密的主键** 每个表单上的组件。 在组件中，选择Adobe Campaign ，以便仅显示这些组件。
>
>虽然在此过程中您手动输入用户档案编号，但实际上，用户会在新闻稿中获取指向此页面的链接（无论是取消订阅、订阅还是更新用户档案）。 根据用户，页面会自动更新。
>
>要创建该链接，您需要使用变量 **主要资源标识符**(Adobe Campaign Standard)或 **加密标识符** (Adobe Campaign 6.1)(例如，在 **文本和个性化（营销活动）** 组件)，用于链接到Adobe Campaign中的epk。

为此，您需要手动获取Adobe Campaign配置文件的EPK，然后将其附加到URL：

1. 要获取Adobe Campaign配置文件的加密主密钥(EPK)，请执行以下操作：

   * 在Adobe Campaign Standard中 — 导航到 **用户档案和受众** > **配置文件**，其中列出了现有用户档案。 确保表显示 **主资源标识符** 列中的字段（这可以通过单击/点按进行配置） **配置列表**)。 复制所需配置文件的主资源标识符。
   * 在Adobe Campaign 6.11中，转到 **配置文件和目标** >  **收件人**，其中列出了现有用户档案。 确保表显示 **加密标识符** 列中的字段(这可以通过右键单击条目并选择 **配置列表……**)。 复制所需配置文件的加密标识符。

1. 在AEM中，打开发布实例上的表单页面，并将步骤1中的EPK作为URL参数附加：在创作表单时，请使用之前在EPK组件中定义的相同名称(例如： `?epk=...`)
1. 该表单现在可用于修改与链接的Adobe Campaign配置文件关联的数据和订阅。 修改某些字段并提交表单后，您可以在Adobe Campaign中验证适当的数据是否已更新。

验证表单后，Adobe Campaign数据库中的数据即会更新。
