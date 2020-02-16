---
title: 使用Adobe I/O与Adobe Target集成
seo-title: 使用Adobe I/O与Adobe Target集成
description: 了解如何使用Adobe I/O将AEM与Adobe Target集成
seo-description: 了解如何使用Adobe I/O将AEM与Adobe Target集成
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: f476091236018c826ae303b4b0fc32c691318f79

---


# 使用Adobe I/O与Adobe Target集成{#integration-with-adobe-target-using-adobe-i-o}

通过Target Standard API将AEM与Adobe Target集成需要配置Adobe IMS(Identity Management System)和Adobe I/O。

>[!NOTE]
>
>AEM 6.5中新增了对Adobe Target Standard API的支持。Target Standard API使用IMS身份验证。
>
>仍支持在AEM中使用Adobe Target Classic API，以实现向后兼容性。 Target [Classic API使用用户凭据身份验证](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。
>
>API选择由用于AEM/Target集成的身份验证方法驱动。

## 前提条件 {#prerequisites}

在开始此过程之 [前](https://helpx.adobe.com/contact/enterprise-support.ec.html) ,Adobe支持部门必须为以下项目配置帐户：

* Adobe Console
* Adobe I/O
* Adobe Target和
* Adobe IMS（身份管理系统）

## 配置IMS配置——生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一阶段是在AEM中创建IMS配置并生成公钥。

1. 在AEM中，打开“工 **具** ”菜单。
1. 在“安 **全** ”部分 **，选择Adobe IMS配置**。
1. 选择 **创建** ，以打开 **Adobe IMS技术帐户配置**。
1. 使用云配置下 **的下拉列表**，选择 **Adobe Target**。
1. 激活 **创建新证书** ，然后输入新别名。
1. 使用创建 **证书进行确认**。

   ![](assets/integrate-target-io-01.png)

1. 选择 **下载** (或 **下载公钥**)以将文件下载到本地驱动器，以便在配置Adobe I/O以与AEM集成时可以使用它 [](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)。

   >[!CAUTION]
   >
   >保持此配置打开状态，在AEM中完成IMS配 [置时将再次需要此配置](#completing-the-ims-configuration-in-aem)。

   ![](assets/integrate-target-io-02.png)

## 配置Adobe I/O以与AEM集成Adobe Target {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

您需要创建AEM将使用的Adobe I/O与Adobe target的集成，然后分配所需的权限。

### 创建集成 {#creating-the-integration}

打开Adobe I/O控制台，以创建AEM将使用的与Adobe Target的I/O集成：

>[!NOTE]
>
>另请参 [阅Adobe I/O教程](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)。

1. 打开Adobe I/O控制台进行集成：

   * [https://console.adobe.io/integrations](https://console.adobe.io/integrations)

1. 选择 **新集成**:

   >[!NOTE]
   >
   >如果您已有集成，则将列出这些集成，并且“ **新集成** ”按钮将位于右上方。

   ![](assets/integrate-target-io-03.png)

1. 选择 **访问API** ，然后 **选择继续**:

   ![](assets/integrate-target-io-04.png)

1. 选择 **Adobe Target**，然后选择 **继续**:

   ![](assets/integrate-target-io-05.png)

1. 为集成配置添加所需的详细信息：

   * **名称**

      输入名称。

   * **描述**

      说明是可选的。

   * **公钥证书**

      上传公钥文件；在“配置IMS [配置——生成公钥”下生成](#configuring-an-ims-configuration-generating-a-public-key)。

      加载后，证书将列在“证书” **下**。

   * **产品配置**

      产品配置与Target中的工作区等同，AEM可用于内容导出和选件创建。 默认情况下，将选择“目标默认工作区”。 选择任何其他应作为导出目标在AEM中显示的配置文件／工作区。
   例如：

   ![](assets/integrate-target-io-06.png)

1. 通过创建集 **成进行确认**。
1. 创建过程将得到确认，您现在可以继 **续查看集成详细信息**;在AEM中完 [成IMS配置时需要这些](#completing-the-ims-configuration-in-aem)。

   ![](assets/integrate-target-io-07.png)

### 为集成分配权限 {#assigning-privileges-to-the-integration}

您现在必须为集成分配所需的权限：

1. 打开Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到 **产品** （顶部工具栏），然后选择 **Adobe Target - &lt;*your-tenant-id*>** （从左侧面板）。
1. 选择 **产品配置**，然后从显示的列表中选择所需的工作区。 例如，默认工作区。
1. 选择 **集成**，然后选择所需的集成配置。
1. 选择 **编辑器** ，作为 **产品角色**;而不是 **观察者**。

## 为Adobe I/O集成存储的详细信息 {#details-stored-for-the-adobe-i-o-integration}

从Adobe I/O集成控制台中，您可以看到所有集成的列表：

* [https://console.adobe.io/integrations](https://console.adobe.io/integrations)

选 **择** “查看”（特定集成条目右侧）以显示有关配置的更多详细信息。 这些 Cookie 包括：

* 概述
* 分析
* 服务
* 事件
* JWT（JSON web令牌）

其中一些操作需要在AEM中完成Target的Adobe I/O集成。

1. **概述**:

   ![](assets/integrate-target-io-08.png)

1. **JWT**:

   ![](assets/integrate-target-io-09.png)

## 在AEM中完成IMS配置 {#completing-the-ims-configuration-in-aem}

返回AEM后，您可以通过从Adobe I/O集成为Target添加所需的值来完成IMS配置：

1. 返回在AEM [中打开的IMS配置](#configuring-an-ims-configuration-generating-a-public-key)。
1. 选择&#x200B;**下一步**。

1. 您可以在此使用 [Adobe I/O的详细信息](#details-stored-for-the-adobe-i-o-integration):

   * **标题**:您的文本。
   * **授权服务器**:从以下“有效负荷 `"aud"` ”部分的行复 **制／粘贴** ，例如，在下面的 `"https://ims-na1.adobelogin.com"` 示例中
   * **API密钥**:从Adobe I/O集 [成](#details-stored-for-the-adobe-i-o-integration) （针对Target）的“概述”部分复制此内容
   * **客户端机密**:在Adobe I/O集 [成的](#details-stored-for-the-adobe-i-o-integration) Target的“概述”部分中生成此组件，并复制
   * **有效负荷**:从Adobe I/O集 [成的](#details-stored-for-the-adobe-i-o-integration) Target的JWT部分复制此组件
   ![](assets/integrate-target-io-10.png)

1. 使用创建进 **行确认**。

1. AEM控制台中将显示您的Adobe target配置。

   ![](assets/integrate-target-io-11.png)

## 确认IMS配置 {#confirming-the-ims-configuration}

要确认配置是否按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`
   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 选择您的配置。
1. 从工 **具栏中选择** “检查运行状况”，然后选择 **检查**。

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您将看到以下消息：

   ![](assets/integrate-target-io-13.png)

## 配置Adobe Target云服务 {#configuring-the-adobe-target-cloud-service}

现在，可以为云服务引用该配置以使用Target Standard API:

1. 打开“工 **具** ”菜单。 然后，在“云服 **务”部分** ，选择 **“旧版云服务”**。
1. 向下滚动到 **Adobe Target** ，然后选择 **立即配置**。

   The **Create Configuration** dialog will open.

1. 输入 **标题** ，并根据需要输入名称 **** （如果留空，此名称将从标题生成）。

   您还可以选择所需的模板（如果有多个模板可用）。

1. 使用创建进 **行确认**。

   此时 **将打开编辑组件** 。

1. 在“ **Adobe Target设置”选项卡中输入详细信息** :

   * **客户端代码**:adobe IMS租户ID

      >[!CAUTION]
      >
      >必须在标有“客户端代码”的字段中输入Adobe IMS租户ID。

   * **身份验证**:IMS
   * **IMS配置**:选择IMS配置的名称
   * **API类型**:REST
   * **A4T Analytics云配置**:选择用于目标活动目标和指标的Analytics云配置。 如果您在定位内容时使用Adobe Analytics作为报告源，则需要此功能。 如果看不到云配置，请参阅配置A4T [Analytics云配置中的注意事项](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)。
   * **使用准确定位**:默认情况下，此复选框处于选中状态。 如果选择此项，云服务配置将在加载内容之前等待上下文加载。 请参阅以下注意事项。
   * **从Adobe Target同步区段**:选择此选项可下载在Target中定义的区段，以便在AEM中使用它们。 当“API类型”属性为REST时，必须选择此选项，因为不支持内联区段，并且您始终需要使用Target中的区段。 （请注意，“segment”的AEM术语与Target的“audience”等效。）
   * **客户端库**:选择是要AT.js客户端库还是mbox.js（已弃用）。
   * **使用标签管理系统交付客户端库**:使用DTM（已弃用）、Adobe Launch或任何其他标签管理系统。
   * **自定义AT.js**:如果选中“标签管理”框或要使用默认的AT.js，请将其留空。 或者上传自定义AT.js。 仅当您选择了AT.js时显示。
   >[!NOTE]
   >
   >[已弃用配置云服务以使用Target Classic API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) （使用Adobe Recommendations设置选项卡）。

   例如：

   ![](assets/integrate-target-io-14.png)

1. 单 **击“连接到Target** ”以初始化与Adobe Target的连接。

   如果连接成功，则显示“连接 **成功** ”消息。

1. 在消 **息上选择** OK（确定），然后在对 **话框上选择** OK（确定）以确认配置。
1. 您现在可以继 [续添加Target Framework](/help/sites-administering/target-configuring.md#adding-a-target-framework) ，以配置将发送到Target的ContextHub或ClientContext参数。 请注意，将AEM Experience Fragments导出到Target时可能不需要执行此操作。

