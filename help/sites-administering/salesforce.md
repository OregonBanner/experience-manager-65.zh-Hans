---
title: 与 Salesforce 集成
seo-title: 与 Salesforce 集成
description: 了解如何将AEM与Salesforce集成。
seo-description: 了解如何将AEM与Salesforce集成。
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 与 Salesforce 集成 {#integrating-with-salesforce}

将Salesforce与AEM集成可提供潜在客户管理功能，并利用Salesforce提供的现有开箱即用功能。 您可以配置AEM以将潜在客户发布到Salesforce，并创建直接从Salesforce访问数据的组件。

AEM与Salesforce之间的双向、可扩展集成支持：

* 组织充分利用和更新数据以增强客户体验。
* 从营销到销售活动的参与度。
* 组织自动从Salesforce数据存储中传输和接收数据。

本文档将介绍以下内容：

* 如何配置Salesforce云服务（将AEM配置为与Salesforce集成）。
* 如何在Client context中使用Salesforce潜在客户／联系人信息并实现个性化。
* 如何使用Salesforce工作流模型将AEM用户作为潜在客户发布到salesforce。
* 如何创建显示Salesforce中数据的组件。

## 配置AEM以与Salesforce集成 {#configuring-aem-to-integrate-with-salesforce}

要配置AEM以与Salesforce集成，您需要首先在Salesforce中配置远程访问应用程序。 然后，您将salesforce云服务配置为指向此远程访问应用程序。

>[!NOTE]
>
>您可以在Salesforce中创建免费的开发人员帐户。

要将AEM配置为与Salesforce集成，请执行以下操作：

>[!CAUTION]
>
>在继续执行该过程之 [前，您需要安装Salesforce Force API](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/com.adobe.cq.mcm.salesforce.content#) Integration包。 有关如何使用包的更多详细信息，请参阅 [如何使用包页](/help/sites-administering/package-manager.md#package-share) 。

1. 在AEM中，导航到 **云服务**。 在第三方服务中，单击“ **立即在****Salesforce中配置”**。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 创建新配置，例如，开 **发人员**。

   >[!NOTE]
   >
   >新配置将重定向到新页面： **http://localhost:4502/etc/cloudservices/salesforce/developer.html**。 这与在Salesforce中创建远程访问应用程序时在回调URL中指定的值完全相同。 这些值必须匹配。

1. 登录您的salesforce帐户(或者，如果您没有帐户，请在https://developer.force.com中创建 [一个](https://developer.force.com))。
1. 在Salesforce中，导航至 **Salesforce** > **** Connected Apps **(在旧版本的Salesforce中，该工作流是DeployDeploy（部署）> Remote Access（远程访问）********** Salesforce（远程访问）。)
1. 单击 **新建** ，以将AEM与Salesforce连接。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 输入“已 **连接的应用程序名**”、“ **API名称**”和“联 **系电子邮件”**。 选中“ **启用OAuth设置** ”复选框，然后输入回 **调URL** ，并添加OAuth范围（例如，完全访问）。 回调URL的外观与以下内容类似： `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   更改服务器名／端口号和页面名称以匹配您的配置。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 单击 **保存** ，以保存salesforce配置。 Salesforce可创建 **消费者密钥****和消费者机密**，您需要它们进行AEM配置。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >您可能需要等待几分钟（最长15分钟），才能激活Salesforce中的远程访问应用程序。

1. 在AEM中，导航到 **Cloud Services** ，然后导航到您之前创建的salesforce配置(例如，开 **发人员**)。 单击 **编辑** ，然后从salesforce.com输入客户密钥和客户机密。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 登录 Url | 这是Salesforce授权端点。 它的值已预填充，在大多数情况下都适用。 |
   |---|---|
   | 客户密钥 | 输入从salesforce.com的“远程访问应用程序注册”页面获取的值 |
   | 客户机密 | 输入从salesforce.com的“远程访问应用程序注册”页面获取的值 |

1. 单击 **“连接到Salesforce** ”以连接。 Salesforce请求您允许您的配置连接到Salesforce。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   在AEM中，将打开一个确认对话框，告知您已成功连接。

1. 导航到网站的根页面，然后单击“页 **面属性”**。 然后选 **择云服务** ，添加 **Salesforce** ，并选择正确的配置(例如， **开发人员**)。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   现在，您可以使用工作流模型将潜在客户发布到Salesforce并创建从Salesforce访问数据的组件。

## 将AEM用户导出为Salesforce潜在客户 {#exporting-aem-users-as-salesforce-leads}

如果要将AEM用户导出为销售人员潜在客户，您需要配置工作流以将潜在客户发布到销售人员。

要将AEM用户作为Salesforce潜在客户导出，请执行以下操作：

1. 通过右键单击工作流 `http://localhost:4502/workflow` Salesforce.com导出并单击开始，导 **航到位于的Salesforce工** 作流 ****。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 选择要创建为潜在客户的AEM用户作为此工作流的 **有效负荷** （主页->用户）。 请务必选择用户的配置文件节点，因为该节点包含像 **gevindName**、 **familyName**&#x200B;等信息，这些信息映射到Salesforce潜在客户的FirstName **和****** LastNameSaidSalestNameAdjips。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >在启动此工作流之前，AEM中的潜在客户节点在发布到Salesforce之前必须具有某些必填字段。 这些是 **给定的Name**、 **familyName**、 **** company和 **email**。 要查看AEM用户与Salesforce潜在客户之间映射的完整列表，请参阅AEM用 [户与Salesforce潜在客户之间的映射配置。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 单击&#x200B;**确定**。用户信息将导出到salesforce.com。 您可以在salesforce.com上验证它。

   >[!NOTE]
   >
   >错误日志将显示是否导入了潜在客户。 有关详细信息，请查看错误日志。

### 配置Salesforce.com导出工作流 {#configuring-the-salesforce-com-export-workflow}

您可能需要配置Salesforce.com导出工作流，以将其与正确的Salesforce.com配置匹配或进行其他更改。

要配置Salesforce.com导出工作流，请执行以下操作：

1. 导航至 `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 打开Salesforce.com导出步骤，选择“参 **数** ”选项卡，然后选择正确的配置并单击“确 **定”**。 此外，如果希望工作流重新创建在Salesforce中删除的潜在客户，请选中此复选框。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 单击 **保存** ，以保存更改。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM用户与Salesforce潜在客户之间的映射配置 {#mapping-configuration-between-aem-user-and-salesforce-lead}

要查看或编辑AEM用户与Salesforce潜在客户之间的当前映射配置，请打开配置管理器：并搜 `https://<hostname>:<port>/system/console/configMgr` 索“ **Salesforce潜在客户映射配置”**。

1. 通过单击“Web控制台”或 **直接转到** “配置管理器”，打开配置管理器 `https://<hostname>:<port>/system/console/configMgr.`
1. 搜索 **Salesforce潜在客户映射配置**。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 根据需要更改映射。 默认映射遵循模式 **aemUserAttribute=sfLeadAttribute**。 单击 **保存** ，以保存更改。

## 配置Salesforce客户端上下文存储 {#configuring-salesforce-client-context-store}

与AEM中已有的信息相比，salesforce客户端上下文存储显示有关当前登录用户的其他信息。 它根据用户与Salesforce的连接从Salesforce中提取此附加信息。

为此，您需要配置以下各项：

1. 通过Salesforce connect组件将AEM用户与Salesforce ID关联。
1. 将“Salesforce配置文件数据”添加到Client Context页中，以配置要查看的属性。
1. （可选）构建使用Salesforce Client Context Store中数据的区段。

### 将AEM用户与Salesforce ID关联 {#linking-an-aem-user-with-a-salesforce-id}

您需要将AEM用户映射为Salesforce ID，才能在Client Context中加载它。 在现实场景中，您将基于已知用户数据与验证进行链接。 出于演示目的，在此过程中，您使用 **Salesforce connect组件** 。

1. 导航到AEM中的网站，登录并从Sidekick中拖放 **Salesforce Connect** 组件。

   >[!NOTE]
   >
   >如果 **Salesforce Connect组件不可用** ，请转到“设计”视图，选择该组件，以在“编辑”视图中使其 **可用****** 。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   将组件拖动到页面时，会显示指向 **Salesforce=Off的链接**。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >此组件仅用于演示目的。 对于真实场景，还会有另一个过程将用户与潜在客户关联／匹配。

1. 在页面上拖动组件后，打开它进行配置。 选择配置、联系人类型以及Salesforce潜在客户或联系人，然后单击“确 **定”**。

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM将用户与Salesforce联系人或潜在客户链接。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### 将Salesforce数据添加到Client Context {#adding-salesforce-data-to-client-context}

您可以从Client Context中的Salesforce加载用户数据以用于个性化：

1. 打开要扩展的Client Context，例如， `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 将Salesforce配置 **文件数据组件拖到** Client Context中。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 双击组件以将其打开。 选择 **添加项目** ，然后从下拉列表中选择一个属性。 添加所需数量的属性，然后选择“确 **定”**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 现在，您会看到Salesforce中特定于Salesforce的属性，这些属性显示在客户端上下文中。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### 使用Salesforce Client Context Store中的数据构建区段 {#building-a-segment-using-data-from-salesforce-client-context-store}

您可以构建使用Salesforce Client Context Store中数据的区段。 要执行此操作：

1. 在AEM中导航到细分，方法是转 **到工具** >细 **分** ，或转到 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation)。
1. 创建或更新区段以包含来自Salesforce的数据。 有关详细信息，请参阅 [分段](/help/sites-administering/campaign-segmentation.md)。

## 搜索潜在客户 {#searching-leads}

AEM附带一个示例搜索组件，该组件可根据给定条件在Salesforce中搜索潜在客户。 此组件向您展示如何使用Salesforce REST API搜索salesforce对象。 您需要将页面与Salesforce配置关联，以跟踪对salesforce.com的调用。

>[!NOTE]
>
>这是一个示例组件，它显示了如何使用Salesforce REST API查询Salesforce对象。 以它为例，根据您的需求创建更复杂的组件。

要使用此组件，请执行以下操作：

1. 导览至要使用此配置的页面。 打开页面属性，然后选择 **云服务。** 单击 **添加服务** ，选择 **Salesforce** 和相应的配置，然后单击 **确定**。

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. 将Salesforce搜索组件拖动到页面（前提是它已启用）。 要启用它，请转到“设计”模式，并将其添加到相应区域)。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 打开搜索组件并指定搜索参数，然后单击 **确定。**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM显示在搜索组件中指定的与指定条件匹配的潜在客户。

   ![chlimage_1-87](assets/chlimage_1-87.png)

