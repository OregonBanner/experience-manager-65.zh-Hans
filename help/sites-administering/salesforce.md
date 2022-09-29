---
title: 与 Salesforce 集成
seo-title: Integrating with Salesforce
description: 了解如何将AEM与Salesforce集成。
seo-description: Learn about integrating AEM with Salesforce.
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
source-git-commit: c7958efbc4557ab3e50732da59faabf4e36c3844
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 1%

---


# 与 Salesforce 集成 {#integrating-with-salesforce}

将Salesforce与AEM集成可提供潜在客户管理功能，并利用Salesforce提供的现有开箱即用功能。 您可以配置AEM以将潜在客户发布到Salesforce，并创建可直接从Salesforce访问数据的组件。

AEM与Salesforce之间的双向可扩展集成支持：

* 组织可充分利用和更新数据以增强客户体验。
* 从营销到销售活动的参与度。
* 组织自动从Salesforce数据存储中传输和接收数据。

本文档将介绍以下内容：

* 如何配置SalesforceCloud Services(配置AEM以与Salesforce集成)。
* 如何在Client Context和Personalization中使用Salesforce潜在客户/联系信息。
* 如何使用Salesforce工作流模型将AEM用户作为潜在客户发布到salesforce。
* 如何创建显示Salesforce数据的组件。

## 配置AEM以与Salesforce集成 {#configuring-aem-to-integrate-with-salesforce}

要配置AEM以与Salesforce集成，您需要先在Salesforce中配置远程访问应用程序。 然后，您将salesforce云服务配置为指向此远程访问应用程序。

>[!NOTE]
>
>您可以在Salesforce中创建免费的开发人员帐户。

要配置AEM以与Salesforce集成，请执行以下操作：

>[!CAUTION]
>
>您需要安装 [Salesforce Force API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) 集成包，然后再继续执行该过程。 有关如何使用资源包的更多详细信息，请参阅 [如何使用包](/help/sites-administering/package-manager.md#package-share) 页面。

1. 在AEM中，导航到 **Cloud Services**. 在第三方服务中，单击 **立即配置** in **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 创建新配置，例如 **开发人员**.

   >[!NOTE]
   >
   >新配置将重定向到新页面： **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. 这与在Salesforce中创建远程访问应用程序时在回调URL中指定的值完全相同。 这些值必须匹配。

1. 登录到您的salesforce帐户(或者，如果您没有帐户，请在 [https://developer.force.com](https://developer.force.com).)
1. 在Salesforce中，导航到 **创建** > **应用程序** 到 **连接的应用程序** (在salesforce的旧版本中，工作流 **部署** > **远程访问**)。
1. 单击 **新建** 将AEM与Salesforce连接。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 输入 **连接的应用程序名称**, **API名称**&#x200B;和 **联系电子邮件**. 选择 **启用OAuth设置** 复选框并输入 **回调URL** 和添加OAuth范围（例如，完全访问权限）。 回调URL类似于以下形式： `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   更改服务器名称/端口号和页面名称以匹配您的配置。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 单击 **保存** 以保存salesforce配置。 Salesforce创建 **消费方密钥** 和 **消费方密码**，这是您配置AEM所需的。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >您可能需要等待几分钟（最多15分钟），才能激活Salesforce中的远程访问应用程序。

1. 在AEM中，导航到 **Cloud Services** 并导航到您之前创建的salesforce配置(例如， **开发人员**)。 单击 **编辑** 并从salesforce.com输入客户密钥和客户密钥。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 登录 Url | 这是Salesforce授权端点。 其值已预填充，适用于大多数情况。 |
   |---|---|
   | 客户密钥 | 在salesforce.com中，输入从“远程访问应用程序注册”页获得的值 |
   | 客户密钥 | 在salesforce.com中，输入从“远程访问应用程序注册”页获得的值 |

1. 单击 **连接到Salesforce** 连接。 Salesforce请求您允许配置连接到Salesforce。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   在AEM中，将打开确认对话框，告知您已成功连接。

1. 导航到网站的根页面，然后单击 **页面属性**. 然后选择 **Cloud Services** 添加 **Salesforce** 并选择正确的配置(例如， **开发人员**)。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   现在，您可以使用工作流模型将潜在客户发布到Salesforce，并创建从Salesforce访问数据的组件。

## 将AEM用户导出为Salesforce潜在客户 {#exporting-aem-users-as-salesforce-leads}

如果要将AEM用户导出为Salesforce潜在客户，您需要配置工作流以将潜在客户发布到Salesforce。

要将AEM用户导出为Salesforce潜在客户，请执行以下操作：

1. 导航到位于的Salesforce工作流 `http://localhost:4502/workflow` 通过右键单击工作流 **Salesforce.com导出** 单击 **开始**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 选择要创建作为潜在客户的AEM用户 **负载** （主页 — >用户）。 确保选择用户的配置文件节点，因为该节点包含诸如 **givenName**, **familyName**，等等，这些变量会映射到Salesforce潜在客户的 **名字** 和 **LastName** 字段。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >在启动此工作流之前，AEM中的潜在客户节点在发布到Salesforce之前必须具有某些必填字段。 这些是 **givenName**, **familyName**, **公司**&#x200B;和 **电子邮件**. 要查看AEM用户与Salesforce潜在客户之间映射的完整列表，请参阅 [在AEM用户和Slaesforce潜在客户之间映射配置。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 单击&#x200B;**确定**。用户信息将导出到salesforce.com。 您可以在salesforce.com上验证它。

   >[!NOTE]
   >
   >错误日志将显示是否导入了潜在客户。 有关详细信息，请查看错误日志。

### 配置Salesforce.com导出工作流 {#configuring-the-salesforce-com-export-workflow}

您可能需要配置Salesforce.com导出工作流，以将其与正确的Salesforce.com配置匹配，或进行其他更改。

要配置Salesforce.com导出工作流，请执行以下操作：

1. 导航至 `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 打开Salesforce.com导出步骤，选择 **参数** ，然后选择正确的配置并单击 **确定**. 此外，如果希望工作流重新创建已在Salesforce中删除的潜在客户，请选中复选框。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 单击 **保存** 以保存更改。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### 在AEM用户和Salesforce潜在客户之间映射配置 {#mapping-configuration-between-aem-user-and-salesforce-lead}

要查看或编辑AEM用户与Salesforce潜在客户之间的当前映射配置，请打开配置管理器： `https://<hostname>:<port>/system/console/configMgr` 和搜索 **Salesforce潜在客户映射配置**.

1. 通过单击 **Web控制台** 或直接转到 `https://<hostname>:<port>/system/console/configMgr.`
1. 搜索 **Salesforce潜在客户映射配置**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 根据需要更改映射。 默认映射遵循模式 **aemUserAttribute=sfLeadAttribute**. 单击 **保存** 以保存更改。

## 配置Salesforce客户端上下文存储 {#configuring-salesforce-client-context-store}

与AEM中已有可用的内容相比，salesforce客户端上下文存储显示有关当前已登录用户的其他信息。 它根据用户与Salesforce的连接，从Salesforce中提取此附加信息。

为此，您需要配置以下内容：

1. 通过Salesforce连接组件将AEM用户与Salesforce ID关联。
1. 将Salesforce配置文件数据添加到客户端上下文页面，以配置要查看的属性。
1. （可选）生成一个区段，以使用Salesforce客户端上下文存储中的数据。

### 将AEM用户与Salesforce ID关联 {#linking-an-aem-user-with-a-salesforce-id}

您需要使用Salesforce ID映射AEM用户，才能在客户端上下文中加载该用户。 在现实场景中，您将基于已知用户数据与验证进行链接。 出于演示目的，在此过程中，您使用 **Salesforce连接** 组件。

1. 导航到AEM中的网站，登录，然后拖放 **Salesforce连接** 组件。

   >[!NOTE]
   >
   >如果 **Salesforce连接** 组件不可用，请转到 **设计** 查看并选择它以使其在 **编辑** 中。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   将组件拖到页面时，会显示该组件 **链接到Salesforce=Off**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >此组件仅用于演示目的。 对于真实情况，还会有另一个流程来链接/匹配用户和潜在客户。

1. 在页面上拖动组件后，将其打开以对其进行配置。 选择配置、联系人类型和Salesforce潜在客户或联系人，然后单击 **确定**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM将用户与Salesforce联系人或潜在客户链接。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### 将Salesforce数据添加到Client Context {#adding-salesforce-data-to-client-context}

您可以在Client Context中从Salesforce加载用户数据，以用于个性化：

1. 例如，通过在此处导航来打开要扩展的客户端上下文， `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 拖动 **Salesforce配置文件数据** 组件。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 双击组件以将其打开。 选择 **添加项目** ，然后从下拉列表中选择一个资产。 添加所需数量的属性并选择 **确定**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 现在，您会在客户端上下文中看到Salesforce中特定于Salesforce的属性。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### 使用来自Salesforce客户端上下文存储的数据构建区段 {#building-a-segment-using-data-from-salesforce-client-context-store}

您可以构建一个区段，该区段使用Salesforce客户端上下文存储中的数据。 要执行此操作：

1. 在AEM中，通过转到 **工具** > **分段** 或 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. 创建或更新区段以包含来自Salesforce的数据。 有关更多信息，请参阅 [分段](/help/sites-administering/campaign-segmentation.md).

## 搜索潜在客户 {#searching-leads}

AEM附带一个示例搜索组件，该组件会根据给定条件在Salesforce中搜索潜在客户。 此组件向您展示如何使用Salesforce REST API搜索Salesforce对象。 您需要将页面与Salesforce配置链接，以跟踪对salesforce.com的调用。

>[!NOTE]
>
>这是一个示例组件，用于向您展示如何使用Salesforce REST API查询Salesforce对象。 以此为例，根据您的需求创建更复杂的组件。

要使用此组件，请执行以下操作：

1. 导航到要使用此配置的页面。 打开页面属性并选择 **Cloud Services。** 单击 **添加服务** 选择 **Salesforce** ，然后单击 **确定**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. 将Salesforce搜索组件拖到页面（前提是已启用它）。 要启用此功能，请转到设计模式并将其添加到相应区域)。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 打开搜索组件并指定搜索参数并单击 **好。**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM显示在搜索组件中指定的与指定的条件匹配的潜在客户。

   ![chlimage_1-87](assets/chlimage_1-87.png)
