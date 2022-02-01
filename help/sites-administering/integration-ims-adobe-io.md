---
title: 使用Adobe Target与Adobe I/O集成
seo-title: Integration with Adobe Target using Adobe I/O
description: 了解如何使用AEM与Adobe Target集成Adobe I/O
seo-description: Learn about integrating AEM with Adobe Target using Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: 9fbf338b18e73fbd272af061381baf34b694239a
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 1%

---

# 使用Adobe Target与Adobe I/O集成{#integration-with-adobe-target-using-adobe-i-o}

要通过Target Standard API将AEM与Adobe Target集成，需要配置Adobe IMS(Identity Management系统)和Adobe I/O。

>[!NOTE]
>
>AEM 6.5中新增了对Adobe Target Standard API的支持。Target Standard API使用IMS身份验证。
>
>为了向后兼容，仍支持在AEM中使用Adobe Target Classic API。 的 [Target Classic API使用用户凭据身份验证](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>API选择由用于AEM/Target集成的身份验证方法驱动。
>另请参阅 [租户ID和客户端代码](#tenant-client) 中。

## 前提条件 {#prerequisites}

在开始此过程之前：

* [Adobe支持](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) 必须为您的帐户配置：

   * Adobe控制台
   * Adobe I/O
   * Adobe Target和
   * Adobe IMS(Identity Management系统)

* 贵组织的系统管理员应使用Admin Console将组织中所需的开发人员添加到相关的产品配置文件中。

   * 这为特定开发人员提供了在Adobe I/O内启用集成的权限。
   * 有关更多详细信息，请参阅 [管理开发人员](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## 配置IMS配置 — 生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一步是在AEM中创建IMS配置并生成公钥。

1. 在AEM中，打开 **工具** 菜单。
1. 在 **安全性** 部分选择 **Adobe IMS配置**.
1. 选择 **创建** 打开 **Adobe IMS技术帐户配置**.
1. 使用下拉菜单 **云配置**，选择 **Adobe Target**.
1. 激活 **创建新证书** 并输入新别名。
1. 使用确认 **创建证书**.

   ![](assets/integrate-target-io-01.png)

1. 选择 **下载** (或 **下载公钥**)将文件下载到本地驱动器，以便在 [配置Adobe I/O以将Adobe Target与AEM集成](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >保持此配置处于打开状态，在 [在AEM中完成IMS配置](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## 为Adobe Target与AEM集成配置Adobe I/O {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

您需要创建与AEM将使用的Adobe Target的Adobe I/O项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

打开Adobe I/O控制台，以创建将由AEM使用的包含Adobe Target的I/O项目：

>[!NOTE]
>
>另请参阅 [Adobe I/O教程](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. 打开项目的Adobe I/O控制台：

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 您所有的项目都将显示出来。 选择 **创建新项目**  — 位置和使用情况取决于：

   * 如果您还没有任何项目， **创建新项目** 中间，底部。
      ![新建项目 — 第一个项目](assets/integration-target-io-02.png)
   * 如果您已经拥有现有项目，则将列出这些项目，并 **创建新项目** 右上方。
      ![创建新项目 — 多个项目](assets/integration-target-io-03.png)


1. 选择 **添加到项目** 后跟 **API**:

   ![](assets/integration-target-io-10.png)

1. 选择 **Adobe Target**，则 **下一个**:

   >[!NOTE]
   >
   >如果您订阅了Adobe Target，但未在列表中看到它，则应查看 [先决条件](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **上传您的公钥**，完成后，继续 **下一个**:

   ![](assets/integration-target-io-13.png)

1. 查看凭据，并继续 **下一个**:

   ![](assets/integration-target-io-15.png)

1. 选择所需的产品配置文件，然后继续 **保存配置的API**:

   >[!NOTE]
   >
   >显示的产品配置文件取决于您是否具有：
   >
   >* Adobe Target Standard — 仅 **默认工作区** 可用
   >* Adobe Target Premium — 列出了所有可用工作区，如下所示


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

1. 导航到 **产品** （顶部工具栏），然后选择 **Adobe Target - &lt;*your-tenant-id*>** （从左侧面板）。
1. 选择 **产品配置文件**，则会从显示的列表中找到所需的工作区。 例如，默认工作区。
1. 选择 **集成**，则是所需的集成配置。
1. 选择 **编辑器** 作为 **产品角色**;而不是 **观察者**.

## 存储的Adobe I/O集成项目详细信息 {#details-stored-for-the-adobe-io-integration-project}

从Adobe I/O项目控制台中，您可以看到所有集成项目的列表：

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

选择 **查看** （位于特定项目条目的右侧）以显示有关配置的更多详细信息。 这些功能包括：

* 项目概述
* 分析
* 凭据
   * 服务帐户(JWT)
      * 凭据详细信息
      * 生成JWT
* API
   * 例如，Adobe Target

其中一些操作需要完成AEM中Target的Adobe I/O集成。

## 在AEM中完成IMS配置 {#completing-the-ims-configuration-in-aem}

返回AEM后，您可以通过从TargetAdobe I/O集成添加所需值来完成IMS配置：

1. 返回到 [在AEM中打开IMS配置](#configuring-an-ims-configuration-generating-a-public-key).
1. 选择&#x200B;**下一步**。

1. 在此，您可以使用 [来自Adobe I/O的详细信息](#details-stored-for-the-adobe-io-integration-project):

   * **标题**:你的短信。
   * **授权服务器**:从 `aud` 行 **负载** ，例如 `https://ims-na1.adobelogin.com` 在以下示例中
   * **API密钥**:从 [概述](#details-stored-for-the-adobe-io-integration-project) TargetAdobe I/O集成部分
   * **客户端密钥**:在 [概述](#details-stored-for-the-adobe-io-integration-project) Adobe I/O集成部分，并复制
   * **负载**:从 [生成JWT](#details-stored-for-the-adobe-io-integration-project) TargetAdobe I/O集成部分

   ![](assets/integrate-target-io-10.png)

1. 使用确认 **创建**.

1. 您的Adobe Target配置将显示在AEM控制台中。

   ![](assets/integrate-target-io-11.png)

## 确认IMS配置 {#confirming-the-ims-configuration}

要确认配置可按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 选择您的配置。
1. 选择 **检查运行状况** ，然后 **检查**.

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您将看到以下消息：

   ![](assets/integrate-target-io-13.png)

## 配置Adobe TargetCloud Service {#configuring-the-adobe-target-cloud-service}

现在，可以为Cloud Service引用配置以使用Target Standard API:

1. 打开 **工具** 菜单。 然后，在 **Cloud Services** 选择 **旧版Cloud Services**.
1. 向下滚动到 **Adobe Target** 选择 **立即配置**.

   的 **创建配置** 对话框。

1. 输入 **标题** 如果你愿意， **名称** （如果留空，则从标题生成）。

   您还可以选择所需的模板（如果有多个模板可用）。

1. 使用确认 **创建**.

   的 **编辑组件** 对话框。

1. 在 **Adobe Target设置** 选项卡：

   * **身份验证**:IMS

   * **租户ID**:Adobe IMS租户ID。 另请参阅 [租户ID和客户端代码](#tenant-client) 中。

      >[!NOTE]
      >
      >对于IMS，需要从Target本身中获取此值。 您可以登录Target并从URL中提取租户ID。
      >
      >例如，如果URL为：
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >那你就用 `yourtenantid`.

   * **客户端代码**:请参阅 [租户ID和客户端代码](#tenant-client) 中。

   * **IMS配置**:选择IMS配置的名称

   * **API类型**:REST

   * **A4T Analytics Cloud配置**:选择用于定位活动目标和量度的Analytics云配置。 如果您在定位内容时使用Adobe Analytics作为报表源，则需要使用此功能。 如果您看不到云配置，请参阅 [配置A4T Analytics Cloud配置](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **使用准确定位**:默认情况下，此复选框处于选中状态。 如果选中此选项，云服务配置将等待上下文加载后再加载内容。 请参阅以下注释。

   * **同步来自Adobe Target的区段**:选择此选项可下载在Target中定义的区段，以在AEM中使用它们。 当API类型属性为REST时，您必须选择此选项，因为不支持内联区段，您始终需要使用Target中的区段。 (请注意，“区段”的AEM术语等同于Target“受众”。)

   * **客户端库**:选择您是希望使用AT.js客户端库，还是mbox.js（已弃用）。

   * **使用标签管理系统来交付客户端库**:使用DTM（已弃用）、LaunchAdobe或任何其他标签管理系统。

   * **自定义AT.js**:如果您选中标签管理框或使用默认AT.js，则保留为空。 或者，上传您的自定义AT.js。 仅当您选择了AT.js时，才会显示。
   >[!NOTE]
   >
   >[配置Cloud Service以使用Target Classic API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 已弃用(使用Adobe Recommendations设置选项卡)。

1. 单击 **连接到Target** 初始化与Adobe Target的连接。

   如果连接成功，则显示消息 **连接成功** 中。

1. 选择 **确定** 在留言上，然后 **确定** ，以确认配置。

1. 您现在可以继续 [添加Target框架](/help/sites-administering/target-configuring.md#adding-a-target-framework) 配置将发送到Target的ContextHub或ClientContext参数。 请注意，将AEM体验片段导出到Target时可能不需要执行此操作。

### 租户ID和客户端代码 {#tenant-client}

使用 [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md)，则“客户端代码”字段已添加到Target配置窗口中。

在配置租户ID和客户端代码字段时，请注意以下事项：

1. 对于大多数客户，租户ID和客户端代码是相同的。 这表示两个字段包含相同的信息且相同。 请确保在这两个字段中输入租户ID。
2. 出于旧版目的，您还可以在租户ID和客户端代码字段中输入不同的值。

在这两种情况下，请注意：

* 默认情况下，客户端代码（如果先添加）也会自动复制到租户ID字段中。
* 您可以选择更改默认的租户ID集。
* 因此，对Target的后端调用将基于租户ID，而对Target的客户端调用将基于客户端代码。

如前所述，第一个案例是AEM 6.5中最常见的案例。无论哪种情况，请确保 **both** 字段包含正确的信息，具体取决于您的要求。

>[!NOTE]
>
> 如果要更改现有Target配置：
>
> 1. 重新输入租户ID。
> 2. 重新连接到Target。
> 3. 保存配置。

