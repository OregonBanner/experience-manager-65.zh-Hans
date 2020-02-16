---
title: 发布和取消发布表单和文档
seo-title: 发布和取消发布表单和文档
description: 您可以计划表单的发布和取消发布。 已发布的表单将复制在发布实例上。
seo-description: 您可以计划表单的发布和取消发布。 已发布的表单将复制在发布实例上。
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# 发布和取消发布表单和文档{#publishing-and-unpublishing-forms-and-documents}

通过AEM Forms，您可以轻松创建、发布和取消发布表单。 有关AEM Forms的详细信息，请参 [阅管理表单的简介](../../forms/using/introduction-managing-forms.md)。

AEM Forms服务器提供两个实例：创作和发布。 创作实例用于创建和管理表单资产和资源。 发布实例用于保留可供最终用户使用的资产和相关资源。 您可以在“创作”模式下导入XDP和PDF表单。 有关详细信息，请 [参阅在AEM Forms中获取XDP和PDF文档](../../forms/using/get-xdp-pdf-documents-aem.md)。

## 支持的资源 {#supported-assets-nbsp}

AEM Forms支持以下类型的资产：

* 自适应表单
* 自适应文档
* 自适应表单片段
* 主题
* 表单模板（XFA表单）
* PDF表单
* 文档（平面PDF文档）
* 表单集
* 资源（图像、架构和样式表）

最初，所有资产仅在作者实例中可用。 管理员或表单作者可以发布除资源以外的所有资产。

当您选择并发布表单时，也会发布其相关的资产和资源。 但是，从属资产不会发布。 在此上下文中，相关资产和资源是已发布资产使用或引用的资产。 从属资产是指引用已发布资产的资产。

您的自适应表单可能会利用一些未自动发布的配置、设置和自定义。 建议在发布自适应表单之前发布或激活这些资源。

* 可编辑的自适应表单模板
* Adobe Sign、Typekit、reCAPTCHA和表单数据模型的云服务配置
* 其他云服务配置仅在用户具有管理员权限时激活。
* 自定义。 这些包括但不限于：

   * 自定义布局
   * 自定义外观
   * CSS文件——在“自适应表单”容器属性对话框中作为输入
   * 客户端库类别——在自适应表单容器属性对话框中作为输入
   * 任何其他客户端库都可能包含在自适应表单模板中。
   * 设计路径

## 资产状态 {#asset-states}

资产可以具有以下状态：

* **** 未发布：从未发布的资产(未发布的状态仅适用于表单资产。 通信管理资产没有“未发布”状态。)
* **已发布**:已发布且在发布实例上可用的资产
* **修改时间**:在发布后修改的资产

## 发布资产 {#publish-an-asset}

1. 登录到AEM Forms服务器。
1. 使用以下任一方式选择和发布资产。

   1. 将指针移到资产上，然后点 **[!UICONTROL 按]**![Publish](assets/aem6forms_globe.pngasset.png)aem6forms_globe。
   1. 执行下列操作之一，然后点按发布：

      * 如果您在卡片视图中，请点按 **[!UICONTROL 进入选择]**![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然后点按资产。 此时会选择资产。
      * 如果您在列表视图中，请选中资产的复选框。 此时会选择资产。
      * 点按资产以显示其详细信息。
      * 通过点按查看属性视图属性来显示资产的 ![属性](assets/viewproperties.png)。
      >[!NOTE]
      >
      >请勿选择多个资产。 不支持同时发布多个资产。


1. 当发布过程开始时，将显示确认对话框，其中列出了所有相关的资产和资源。 在包含相关资产的对话框中，点按发 **[!UICONTROL 布]**。 此时会发布资产，并显示发布资产成功对话框。

   >[!NOTE]
   >
   >对于自适应表单以及相关资产，还会显示自适应表单页面名称。

   ![与所有相关资产和资源的确认对话框](assets/p4.png)

   与所有相关资产和资源对应的确认对话框。

   >[!NOTE]
   >
   >对于Forms Manager，如果用户没有发布列出的资产的权限，则“发布”操作将被禁用。 需要额外权限的资产将以红色显示。

   发布资产后，资产的元数据属性将复制到发布实例，资产的状态将更改为已发布。 已发布的从属资产的状态也会更改为“已发布”。

   发布资产后，您可以使用Forms Portal在网页上显示所有资产。 有关详细信息，请参 [阅在门户上发布表单的介绍](../../forms/using/introduction-publishing-forms.md)。

## Publish all the Correspondence Management Assets {#publish-all-the-correspondence-management-assets}

通过AEM Forms，您只需一次即可在服务器上发布所有Correponsement Management资产。 已发布的资产包括所有Correponse Management资产和相关依赖关系。

完成以下步骤以在服务器上发布所有通信管理资产：

1. 登录到AEM Forms服务器。
1. 在全 **局导航栏中点按Adobe Experience Manager** 。
1. 点按 ![工具](assets/tools.png)，然后点按 **表单**。
1. Tap **Publish Correspondence Management Assets**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   此时会显示“发布所有对应管理资产”页面，并显示有关上次尝试发布对应管理资产流程的信息。

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 点 **按发布** ，然后在确认消息中点按 **确定**。

   批处理完成后，您可以查看上次运行的详细信息。 这包括管理员登录以及批处理是否成功运行等信息。

   >[!NOTE]
   >
   >发布进程在启动后便无法取消。 此外，在发布操作进行中，请勿创建、删除、修改或发布任何资产，或启动导出所有对应管理资产操作。

## 自动发布和取消发布表单和文档 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

通过AEM Forms，您可以为表单和文档计划资产发布和取消发布。 您可以在元数据编辑器中指定计划。 有关管理表单元数据的详细信息，请参阅管 [理表单元数据。](../../forms/using/manage-form-metadata.md)

按照以下步骤计划发布和取消发布表单和文档资产的日期和时间：

1. 选择资产，然后点按查 **[!UICONTROL 看属性]**。 此时将打开元数据属性页面。
1. 在“元数据属性”页中，点 **[!UICONTROL 按高级]**，然后点按编辑 **[!UICONTROL illustratorcc_]** penciltool_cur_edit_2_17 ![](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
1. 在“按 **[!UICONTROL 时发布]** ”和“ **[!UICONTROL 按时发布]** ”字段中，选择日期和时间。\
   点按 **[!UICONTROL 完成]**![aem6forms_check](assets/aem6forms_check.png)。

## 取消发布资产 {#unpublish-an-asset}

1. 选择已发布的资产，然后点按取消 **[!UICONTROL 发布]**![取消发布](assets/unpublish.png)。
1. 使用以下任一方法选择和取消发布资产。

   1. 将指针移到资产上，然后点按取消 **[!UICONTROL 发布]**![取消发布](assets/unpublish.png)。
   1. 执行下列操作之一，然后点按取消发布：

      * 如果您在卡片视图中，请点按 **[!UICONTROL 进入选择]**![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然后点按资产。 此时会选择资产。

      * 如果您在列表视图中，请将指针悬停在资产上，然后点按选 ![择资产对勾标记](assets/selectassetcheckmark.png) 。 此时会选择资产。

      * 点按资产以显示其详细信息。
      * 通过点按查看属性视图属性来显示资产的 ![属性](assets/viewproperties.png)。

1. 当“取消发布”进程启动时，将显示确认对话框。 点按 **[!UICONTROL 取消发布]**。

   >[!NOTE]
   >
   >只有选定的资产尚未取消发布，且其子资产和引用的资产（如果有）未取消发布。

## 将资产或信件还原到之前发布的版本 {#revert-an-asset-or-letter-to-the-previously-published-version}

每次您在编辑资产或书信后发布它时，都会创建某个版本的资产或书信。 您可以将资产或信函还原到先前发布的版本。 如果资产或文档的当前版本出现问题，您可能需要这样做。

>[!NOTE]
>
>如果已发布信函中使用的任何从属资产已从系统中删除，请勿将信件还原到上次发布状态。

1. 选择资产，然后点按还 **[!UICONTROL 原到先前发布的版本]** , ![还原到先前发布的版本](assets/reverttopreviouslypublishedversion.png)。
1. 在恢复资产之前，会显示确认对话框。 点按 **[!UICONTROL 还原]**。

   资产或书信将回滚至其先前发布的版本。

## 删除资产 {#delete-an-asset}

>[!NOTE]
>
>删除资产会将其从发布实例中删除。 删除资产也会删除其版本历史记录，但基本版本除外。

1. 选择资产，然后点按删 **[!UICONTROL 除]**![删除](assets/delete.png)。

   >[!NOTE]
   >
   >当您通过点按资产来显示资产详细信息或通过点按查看属性视图属性来显示资产的属性时，删除选项也 ![可用](assets/viewproperties.png)。

1. 删除资产前，将显示确认对话框。 点按 **[!UICONTROL 删除]**。

   >[!NOTE]
   >
   >只有选定的资产才会被删除，从属资产才会被删除。 要检查资产的引用，请点按引 ![用](assets/references.png) ，然后选择资产。
   >
   >
   >如果您尝试删除的资产是另一个资产的子资产，则不会删除该资产。 要删除此类资产，请从其他资产中删除对此资产的引用，然后重试。

## 受保护的自适应表单 {#protected-adaptive-forms}

您可以为希望选定用户访问的表单启用身份验证。 当您为表单启用身份验证时，用户在访问表单之前会看到一个登录屏幕。 只有具有已授权凭据的用户才能访问表单。

要为表单启用身份验证，请执行以下操作：

1. 在您的浏览器中，打开发布实例中的configMgr。\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. 在Adobe Experience Manager web控制台配置中，单击 **Apache Sling Authentication Service** （Apache Sling身份验证服务）对其进行配置。
1. 在出现的“Apache Sling Authentication Service”对话框中，使用 **+按钮** 添加路径。\
   添加路径时，该路径中的表单将启用身份验证服务。
