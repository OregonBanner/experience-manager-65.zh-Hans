---
title: 使用Adobe Analytics与Adobe I/O集成
description: 了解如何使用AEM与Adobe Analytics集成Adobe I/O
source-git-commit: c2c7c3f745a5f1edc1a8d2a73922f86f0b952ff7
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 1%

---

# 使用Adobe Analytics与Adobe I/O集成 {#integration-with-adobe-analytics-using-adobe-i-o}

要通过Analytics Standard API将AEM与Adobe Analytics集成，需要配置Adobe IMS(Identity Management系统)和Adobe I/O。

>[!NOTE]
>
>AEM 6.5.12.0中新增了对Adobe Analytics Standard API 2.0的支持。此版本的API支持IMS身份验证。
>
>仍支持在AEM中使用Adobe Analytics Classic API 1.4以实现向后兼容性。 的 [Analytics Classic API使用用户凭据身份验证](/help/sites-administering/adobeanalytics-connect.md).
>
>API选择由用于AEM/Analytics集成的身份验证方法驱动。
>
>详情见 [迁移到2.0 API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## 前提条件 {#prerequisites}

在开始此过程之前：

* [Adobe支持](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) 必须为您的帐户配置：

   * Adobe控制台
   * Adobe I/O
   * Adobe Analytics和
   * Adobe IMS(Identity Management系统)

* 贵组织的系统管理员应使用Admin Console将组织中所需的开发人员添加到相关的产品配置文件中。

   * 这为特定开发人员提供了在Adobe I/O内启用集成的权限。
   * 有关更多详细信息，请参阅 [管理开发人员](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## 配置IMS配置 — 生成公钥 {#configuring-an-ims-configuration-generating-a-public-key}

配置的第一步是在AEM中创建IMS配置并生成公钥。

1. 在AEM中，打开 **工具** 菜单。
1. 在 **安全性** 部分选择 **Adobe IMS配置**.
1. 选择 **创建** 打开 **Adobe IMS技术帐户配置**.
1. 使用下拉菜单 **云配置**，选择 **Adobe Analytics**.
1. 激活 **创建新证书** 并输入新别名。
1. 使用确认 **创建证书**.

   ![](assets/integrate-analytics-io-01.png)

1. 选择 **下载** (或 **下载公钥**)将文件下载到本地驱动器，以便在 [配置Adobe I/O以将Adobe Analytics与AEM集成](#configuring-adobe-i-o-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >保持此配置处于打开状态，在 [在AEM中完成IMS配置](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-analytics-io-02.png)

## 为Adobe Analytics与AEM集成配置Adobe I/O {#configuring-adobe-i-o-for-adobe-analytics-integration-with-aem}

您需要创建与AEM将使用的Adobe Analytics的Adobe I/O项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

打开Adobe I/O控制台，以创建将由AEM使用的包含Adobe Target的I/O项目：

<!--
>[!NOTE]
>
>See also the [Adobe I/O tutorials](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).
-->

1. 打开项目的Adobe I/O控制台：

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 您所有的项目都将显示出来。 选择 **创建新项目**  — 位置和使用情况取决于：

   * 如果您还没有任何项目， **创建新项目** 中间，底部。
      ![新建项目 — 第一个项目](assets/integration-analytics-io-02.png)
   * 如果您已经拥有现有项目，则将列出这些项目，并 **创建新项目** 右上方。
      ![创建新项目 — 多个项目](assets/integration-analytics-io-03.png)


1. 选择 **添加到项目** 后跟 **API**:

   ![开始使用新项目](assets/integration-analytics-io-10.png)

1. 选择 **Adobe Analytics**，则 **下一个**:

   >[!NOTE]
   >
   >如果您订阅了Adobe Analytics，但未在列表中看到它，则应查看 [先决条件](#prerequisites).

   ![添加API](assets/integration-analytics-io-12.png)

1. 选择 **服务帐户(JWT)** 作为身份验证类型，然后继续 **下一个**:

   ![选择身份验证类型](assets/integration-analytics-io-12a.png)

1. **上传您的公钥**，完成后，继续 **下一个**:

   ![上传您的公钥](assets/integration-analytics-io-13.png)

1. 查看凭据，并继续 **下一个**:

   ![查看凭据](assets/integration-analytics-io-15.png)

1. 选择所需的产品配置文件，然后继续 **保存配置的API**:

   >[!NOTE]
   >
   >显示的产品配置文件取决于您是否具有：
   >
   >* Adobe Target Standard — 仅 **默认工作区** 可用
   >* Adobe Target Premium — 列出了所有可用工作区，如下所示


   ![选择所需的产品配置文件](assets/integration-analytics-io-16.png)

1. 将确认配置。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 为集成分配权限 {#assigning-privileges-to-the-integration}

您现在必须为集成分配所需的权限：

1. 打开Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到 **产品** （顶部工具栏），然后选择 **Adobe Analytics - &lt;*your-tenant-id*>** （从左侧面板）。
1. 选择 **产品配置文件**，则会从显示的列表中找到所需的工作区。 例如，默认工作区。
1. 选择 **API凭据**，则是所需的集成配置。
1. 选择 **编辑器** 作为 **产品角色**;而不是 **观察者**.

## 存储的Adobe I/O集成项目详细信息 {#details-stored-for-the-adobe-io-integration-project}

从Adobe I/O项目控制台中，您可以看到所有集成项目的列表：

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

选择特定项目条目以显示有关配置的更多详细信息。 这些功能包括：

* 项目概述
* 分析
* 凭据
   * 服务帐户(JWT)
      * 凭据详细信息
      * 生成JWT
* API
   * 例如，Adobe Analytics

其中某些内容需要完成AEM中Adobe Analytics的Adobe I/O集成。

## 在AEM中完成IMS配置 {#completing-the-ims-configuration-in-aem}

返回AEM后，您可以通过从TargetAdobe I/O集成添加所需值来完成IMS配置：

1. 返回到 [在AEM中打开IMS配置](#configuring-an-ims-configuration-generating-a-public-key).
1. 选择&#x200B;**下一步**。

1. 在此，您可以使用 [中项目配置的详细信息Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **标题**:你的短信。
   * **授权服务器**:从 `aud` 行 **负载** ，例如 `https://ims-na1.adobelogin.com` 在以下示例中
   * **API密钥**:从 **凭据** 部分 [项目概述](#details-stored-for-the-adobe-io-integration-project)
   * **客户端密钥**:在 [服务帐户(JWT)部分的“客户端密钥”选项卡](#details-stored-for-the-adobe-io-integration-project)，和复制
   * **负载**:从 [生成服务帐户(JWT)部分的JWT选项卡](#details-stored-for-the-adobe-io-integration-project)

   ![AEM IMS配置详细信息](assets/integrate-analytics-io-10.png)

1. 使用确认 **创建**.

1. 您的Adobe Target配置将显示在AEM控制台中。

   ![IMS 配置](assets/integrate-analytics-io-11.png)

## 确认IMS配置 {#confirming-the-ims-configuration}

要确认配置可按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 选择您的配置。
1. 选择 **检查运行状况** ，然后 **检查**.

   ![IMS配置 — 检查运行状况](assets/integrate-analytics-io-12.png)

1. 如果成功，您将看到一条确认消息。

   <!--
   ![](assets/integrate-target-io-13.png)
   -->

## 配置Adobe Analytics Cloud服务 {#configuring-the-adobe-analytics-cloud-service}

现在，可以为Cloud Service引用配置以使用Analytics Standard API:

1. 打开 **工具** 菜单。 然后，在 **Cloud Services** 选择 **旧版Cloud Services**.
1. 向下滚动到 **Adobe Analytics** 选择 **立即配置**.

   的 **创建配置** 对话框。

1. 输入 **标题** 如果你愿意， **名称** （如果留空，则从标题生成）。

   您还可以选择所需的模板（如果有多个模板可用）。

1. 使用确认 **创建**.

   的 **编辑组件** 对话框。

1. 在 **Analytics设置** 选项卡：

   * **身份验证**:IMS

   * **IMS配置**:选择IMS配置的名称

1. 单击 **连接到Analytics** 初始化与Adobe Target的连接。

   如果连接成功，则显示消息 **连接成功** 中。

1. 选择 **确定** 消息中。

1. 根据需要完成其他参数，然后是 **确定** ，以确认配置。

1. 您现在可以继续 [添加Analytics框架](/help/sites-administering/adobeanalytics-connect.md) 以配置将发送到Adobe Analytics的参数。
