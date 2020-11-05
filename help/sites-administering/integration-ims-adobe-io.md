---
title: 使用AdobeI/O与Adobe Target集成
seo-title: 使用AdobeI/O与Adobe Target集成
description: 了解如何使用AdobeI/O将AEM与Adobe Target集成
seo-description: 了解如何使用AdobeI/O将AEM与Adobe Target集成
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: d12ebf77d2af389e0a3aea5c7f311c828ecd7c17
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 1%

---


# 使用AdobeI/O与Adobe Target集成{#integration-with-adobe-target-using-adobe-i-o}

通过Target Standard API将AEM与Adobe Target集成需要配置AdobeIMS(Identity Management系统)和AdobeI/O。

>[!NOTE]
>
>AEM 6.5中新增了对Adobe Target标准API的支持。目标标准API使用IMS身份验证。
>
>仍支持在AEM中使用Adobe Target经典API实现向后兼容。 目标 [经典API使用用户凭据身份验证](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。
>
>API选择由用于AEM/目标集成的身份验证方法驱动。

## 前提条件 {#prerequisites}

在开始此过程之前：

* [Adobe支持](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) ，必须为以下项目配置您的帐户：

   * Adobe控制台
   * AdobeI/O
   * Adobe Target
   * AdobeIMS(Identity Management系统)

* 贵组织的系统管理员应使用该Admin Console将贵组织中所需的开发人员添加到相关产品用户档案。

   * 这为特定开发人员提供了在AdobeI/O内启用集成的权限。
   * 有关更多详细信息，请 [参阅管理开发人员](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)。


## 配置IMS配置——生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一阶段是在AEM中创建IMS配置并生成公钥。

1. 在AEM中，打开 **工具** 菜单。
1. 在“安 **全** ”部分 **，选择AdobeIMS配置**。
1. 选择 **创建** ，以打开 **AdobeIMS技术帐户配置**。
1. 使用云配置下 **的下拉框**，选择 **Adobe Target**。
1. 激活 **创建新证书** ，然后输入新别名。
1. 使用创建 **证书进行确认**。

   ![](assets/integrate-target-io-01.png)

1. 选 **择** “下载”( **或“下载公钥**”)将文件下载到本地驱动器，以便在配置AdobeI/O以与AEM [集成时使用它](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)。

   >[!CAUTION]
   >
   >保持此配置打开，在AEM中完成IMS配 [置时将再次需要此配置](#completing-the-ims-configuration-in-aem)。

   ![](assets/integrate-target-io-02.png)

## 配置AdobeI/O以与AEM集成Adobe Target {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

您需要创建与AEM将使用的AdobeI/O项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

打开AdobeI/O控制台，与AEM将使用的Adobe Target创建I/O项目：

>[!NOTE]
>
>另请参阅 [AdobeI/O教程](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)。

1. 打开项目的AdobeI/O控制台：

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 将显示您拥有的任何项目。 选 **择创建新项目** -位置和使用情况取决于：

   * 如果您还没有任何项目，则“ **创建新项目** ”将居中、底部。
      ![创建新项目——第一个项目](assets/integration-target-io-02.png)
   * 如果您已有项目，则这些项目将列出， **并且“创建新项目** ”将位于右上方。
      ![创建新项目——多个项目](assets/integration-target-io-03.png)


1. 选择 **添加到项目** ，后 **跟API**:

   ![](assets/integration-target-io-10.png)

1. 选择 **Adobe Target**，然后 **选择下一**&#x200B;步：

   >[!NOTE]
   >
   >如果您订阅的是Adobe Target，但未看到其列出，则应检查“预先 [请求”](#prerequisites)。

   ![](assets/integration-target-io-12.png)

1. **上传您的公钥**，完成后，继续执行下 **一步**:

   ![](assets/integration-target-io-13.png)

1. 查看凭据，然后继续 **使用**:

   ![](assets/integration-target-io-15.png)

1. 选择所需的产品用户档案，然后继续使 **用保存配置的API**:

   >[!NOTE]
   >
   >显示的产品用户档案取决于您是否具有：
   >
   >* Adobe Target标准版——仅 **提供默认工** 作区
   >* Adobe Target高级版——列出所有可用工作区，如下所示


   ![](assets/integration-target-io-16.png)

1. 将确认创建。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 为集成分配权限 {#assigning-privileges-to-the-integration}

您现在必须为集成分配所需的权限：

1. 打开Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到 **产品** （顶部工具栏），然 **后选择&#x200B;*Adobe Target-*&lt;您的租户-id** >（从左侧面板）。
1. 选择 **产品用户档案**，然后从显示的列表中选择所需的工作区。 例如，默认工作区。
1. 选择 **集成**，然后选择所需的集成配置。
1. 选择 **Editor** 作为 **产品角色**;而不是 **观察者**。

## 存储为AdobeI/O集成项目的详细信息 {#details-stored-for-the-adobe-io-integration-project}

从AdobeI/O项目控制台中，您可以看到所有集成项目的列表:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

选 **择视图** （特定项目条目的右侧）以显示有关配置的更多详细信息。 这些 Cookie 包括：

* 项目概述
* 分析
* 凭据
   * 服务帐户(JWT)
      * 凭据详细信息
      * 生成JWT
* API
   * 比如Adobe Target

其中一些需要完成AdobeI/O集成，以便在AEM目标进行。

## 在AEM中完成IMS配置 {#completing-the-ims-configuration-in-aem}

返回AEM后，您可以通过从AdobeI/O集成中添加所需值来完成IMS配置，以用于目标:

1. 返回AEM中 [打开的IMS配置](#configuring-an-ims-configuration-generating-a-public-key)。
1. 选择&#x200B;**下一步**。

1. 您可以在此使用 [AdobeI/O的详细信息](#details-stored-for-the-adobe-io-integration-project):

   * **标题**:您的文本。
   * **授权服务器**:从以下“有效负 `"aud"` 荷”部 **分的行复制** /粘贴此项， `"https://ims-na1.adobelogin.com"` 例如，在以下示例中
   * **API密钥**:从Adobe [I](#details-stored-for-the-adobe-io-integration-project) /O集成的概述部分复制此组件以供目标
   * **客户端机密**:在AdobeI/ [O集成](#details-stored-for-the-adobe-io-integration-project) 的“概述”部分生成此组件，并复制
   * **有效负荷**:从AdobeI/ [O集成的](#details-stored-for-the-adobe-io-integration-project) “生成JWT”部分复制此组件以供目标

   ![](assets/integrate-target-io-10.png)

1. 通过创建 **进行确认**。

1. 您的Adobe Target配置将显示在AEM控制台中。

   ![](assets/integrate-target-io-11.png)

## 确认IMS配置 {#confirming-the-ims-configuration}

要确认配置是否按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 选择您的配置。
1. 从工 **具栏中** ，选择检查运行状况，然后 **选择检查**。

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您将看到以下消息：

   ![](assets/integrate-target-io-13.png)

## 配置Adobe TargetCloud Service {#configuring-the-adobe-target-cloud-service}

现在可以为Cloud Service引用此配置以使用Target Standard API:

1. 打开“工 **具** ”菜单。 然后，在“Cloud Services **”部分** ，选择“ **旧Cloud Services”**。
1. 向下滚动到 **Adobe Target** ，然后选择 **立即配置**。

   The **Create Configuration** dialog will open.

1. 输入 **标题** ，并根据需要输入 **名称** （如果留空，则将从标题生成该名称）。

   您还可以选择所需的模板（如果有多个模板可用）。

1. 通过创建 **进行确认**。

   将打 **开编辑组** 件对话框。

1. 在“Adobe Target设置”选 **项卡中输入** 详细信息：

   * **身份验证**:IMS
   * **租户ID**:adobeIMS租户ID
   * **IMS配置**:选择IMS配置的名称
   * **API类型**:休息
   * **A4TAnalytics Cloud配置**:选择用于目标活动目标和指标的Analytics云配置。 如果您在定位内容时使用Adobe Analytics作为报告源，则需要此项。 如果看不到云配置，请参阅配置A4T [Analytics Cloud配置中的注释](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)。
   * **使用准确定位**:默认情况下，此复选框处于选中状态。 如果选中，云服务配置将在加载内容之前等待上下文加载。 请参阅以下注释。
   * **同步来自Adobe Target的区段**:选择此选项可下载在目标中定义的区段，以便在AEM中使用它们。 当“API类型”属性为REST时，必须选择此选项，因为不支持内联段，并且您始终需要使用目标中的段。 (请注意，AEM术语“segment”等效于目标“受众”。)
   * **客户端库**:选择是要AT.js客户端库，还是mbox.js（已弃用）。
   * **使用标签管理系统交付客户端库**:使用DTM（已弃用）、Adobe启动或任何其他标签管理系统。
   * **自定义AT.js**:如果选中“标签管理”框或使用默认的AT.js，则保留为空。 或者上传自定义AT.js。 仅当您选择了AT.js时显示。

   >[!NOTE]
   >
   >[已弃用使用Cloud Service经典API的目标配置](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) (使用“Adobe Recommendations设置”选项卡)。

   例如：

   ![](assets/integrate-target-io-14.png)

1. 单击 **连接以目标** ，以初始化与Adobe Target的连接。

   如果连接成功，则显示“ **连接成功** ”消息。

1. 在消 **息上** ，选择确定，然后 **在对话** 框上选择确定，以确认配置。
1. 您现在可以继 [续添加目标框架](/help/sites-administering/target-configuring.md#adding-a-target-framework) ，以配置将发送到目标的ContextHub或ClientContext参数。 请注意，将AEM Experience Fragments导出到目标时可能不需要这样做。

