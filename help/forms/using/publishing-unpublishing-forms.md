---
title: 发布和取消发布表单和文档
seo-title: 发布和取消发布表单和文档
description: 您可以计划发布和取消发布表单。 已发布的表单会在发布实例上复制。
seo-description: 您可以计划发布和取消发布表单。 已发布的表单会在发布实例上复制。
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---

# 发布和取消发布表单和文档{#publishing-and-unpublishing-forms-and-documents}

通过AEM Forms，您可以轻松创建、发布和取消发布表单。 有关AEM Forms的更多信息，请参阅[管理表单简介](../../forms/using/introduction-managing-forms.md)。

AEM Forms服务器提供两个实例：创作和发布。 创作实例用于创建和管理表单资产和资源。 发布实例用于保留可供最终用户使用的资产和相关资源。 您可以在创作模式下导入XDP和PDF forms。 有关更多信息，请参阅[在AEM Forms中获取XDP和PDF文档](../../forms/using/get-xdp-pdf-documents-aem.md)。

## 支持的资产   {#supported-assets-nbsp}

AEM Forms支持以下类型的资产：

* 自适应表单
* 自适应文档
* 自适应表单片段
* 主题
* 表单模板（XFA表单）
* PDF forms
* 文档（平面PDF文档）
* 表单集
* 资源（图像、架构和样式表）

最初，所有资产只能在创作实例中使用。 管理员或表单作者可以发布除资源之外的所有资产。

当您选择并发布表单时，其相关资产和资源也会发布。 但是，从属资产不会发布。 在此上下文中，相关资产和资源是指已发布资产使用或引用的资产。 从属资产是指引用已发布资产的资产。

您的自适应Forms可能会利用一些未自动发布的配置、设置和自定义。 建议您在发布自适应表单之前发布或激活这些资源。

* 可编辑的自适应表单模板
* Cloud ServiceAdobe Sign、Typekit、reCAPTCHA和表单数据模型的配置
* 仅当用户具有管理员权限时，才会激活其他云服务配置。
* 自定义。 这些功能包括但不限于：

   * 自定义布局
   * 自定义外观
   * CSS文件 — 作为自适应表单容器属性对话框中的输入
   * 客户端库类别 — 作为自适应表单容器属性对话框中的输入
   * 任何可能包含在自适应表单模板中的其他客户端库。
   * 设计路径

## 资产状态{#asset-states}

资产可以具有以下状态：

* **未发布：** 从未发布的资产(未发布状态仅适用于Forms资产。通信管理资产没有未发布状态。)
* **已发布**:已发布且可在发布实例中使用的资产
* **已修改**:发布后修改的资产

## 发布资产{#publish-an-asset}

1. 登录到AEM Forms服务器。
1. 使用以下任一方式选择和发布资产。

   1. 将指针移到资产上，然后点按&#x200B;**[!UICONTROL 发布]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png)。
   1. 执行下列操作之一，然后点按发布：

      * 如果您在卡片视图中，请点按&#x200B;**[!UICONTROL 进入选择]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然后点按资产。 此时会选择资产。
      * 如果您在列表视图中，请选中资产的复选框。 此时会选择资产。
      * 点按资产以显示其详细信息。
      * 通过点按查看属性![viewproperties](assets/viewproperties.png)来显示资产的属性。

      >[!NOTE]
      >
      >请勿选择多个资产。 不支持同时发布多个资产。


1. 发布过程启动时，将显示一个确认对话框，其中列出了所有相关的资产和资源。 在包含相关资产的对话框中，点按&#x200B;**[!UICONTROL 发布]**。 此时会发布资产，并显示发布资产成功对话框。

   >[!NOTE]
   >
   >对于自适应表单以及相关资产，也会显示自适应表单页面名称。

   ![与所有相关资产和资源的确认对话框](assets/p4.png)

   与所有相关资产和资源的确认对话框。

   >[!NOTE]
   >
   >对于Forms Manager，如果用户没有发布列出的资产的权限，则“发布”操作将处于禁用状态。 需要额外权限的资产将以红色显示。

   发布资产后，资产的元数据属性将会复制到发布实例，并且资产的状态会更改为已发布。 发布的从属资产的状态也会更改为“已发布”。

   发布资产后，您可以使用Forms门户在网页上显示所有资产。 有关更多信息，请参阅[在门户上发布表单简介](../../forms/using/introduction-publishing-forms.md)。

## 发布所有通信管理资产{#publish-all-the-correspondence-management-assets}

通过AEM Forms，您可以一次在服务器上发布所有通信管理资产。 已发布的资产包括所有通信管理资产和相关依赖关系。

完成以下步骤以在服务器上发布所有通信管理资产：

1. 登录到AEM Forms服务器。
1. 点按全局导航栏中的&#x200B;**Adobe Experience Manager**。
1. 点按![工具](assets/tools.png)，然后点按&#x200B;**Forms**。
1. 点按&#x200B;**发布通信管理资产**。

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   此时会显示发布所有通信管理资产页面，并显示有关上次尝试发布通信管理资产流程的信息。

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 点按&#x200B;**发布**，然后在确认消息中，点按&#x200B;**确定**。

   完成批处理后，您可以查看上次运行的详细信息。 这包括管理员登录以及批处理是否成功运行或失败等信息。

   >[!NOTE]
   >
   >启动后，发布进程便无法取消。 此外，在发布操作进行中，请勿创建、删除、修改或发布任何资产，或启动导出所有通信管理资产操作。

## 自动发布和取消发布Forms和文档{#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms允许您为Forms和文档计划资产发布和取消发布。 您可以在元数据编辑器中指定计划。 有关管理表单元数据的更多信息，请参阅[管理表单元数据。](../../forms/using/manage-form-metadata.md)

请按照以下步骤来计划发布和取消发布Forms和文档资产的日期和时间：

1. 选择资产，然后点按&#x200B;**[!UICONTROL 查看属性]**。 此时将打开元数据属性页面。
1. 在“元数据属性”页面中，点按&#x200B;**[!UICONTROL 高级]**，然后点按&#x200B;**[!UICONTROL 编辑]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
1. 在&#x200B;**[!UICONTROL Publish On Time]**&#x200B;和&#x200B;**[!UICONTROL Publish Off Time]**&#x200B;字段中，选择日期和时间。\
   点按&#x200B;**[!UICONTROL Done]** ![aem6forms_check](assets/aem6forms_check.png)。

## 取消发布资产{#unpublish-an-asset}

1. 选择已发布的资产，然后点按&#x200B;**[!UICONTROL 取消发布]** ![取消发布](assets/unpublish.png)。
1. 使用以下任一方法选择和取消发布资产。

   1. 将指针移到资产上，然后点按&#x200B;**[!UICONTROL 取消发布]** ![取消发布](assets/unpublish.png)。
   1. 执行以下操作之一，然后点按取消发布：

      * 如果您在卡片视图中，请点按&#x200B;**[!UICONTROL 进入选择]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然后点按资产。 此时会选择资产。

      * 如果您在列表视图中，将鼠标悬停在资产上，然后点按![selectassetcheckmark](assets/selectassetcheckmark.png) 。 此时会选择资产。

      * 点按资产以显示其详细信息。
      * 通过点按查看属性![viewproperties](assets/viewproperties.png)来显示资产的属性。

1. “取消发布”进程启动时，会显示确认对话框。 点按&#x200B;**[!UICONTROL 取消发布]**。

   >[!NOTE]
   >
   >只有选定的资产未发布，且其子资产和引用的资产（如果有）未发布。

## 将资产或信件还原到之前发布的版本{#revert-an-asset-or-letter-to-the-previously-published-version}

每当您在编辑资产或信件后发布该资产或信件时，都会创建资产或信件的某个版本。 您可以将资产或信件还原到之前发布的版本。 如果资产或文档的当前版本出现问题，您可能需要这样做。

>[!NOTE]
>
>如果从系统中删除了该已发布信件中使用的任何从属资产，请勿将信件还原到上次发布状态。

1. 选择资产，然后点按&#x200B;**[!UICONTROL 还原到之前发布的版本]** ![还原到之前发布的版本](assets/reverttopreviouslypublishedversion.png)。
1. 在恢复资产之前，会显示一个确认对话框。 点按&#x200B;**[!UICONTROL 还原]**。

   资产或信件将被回滚到其先前发布的版本。

## 删除资产{#delete-an-asset}

>[!NOTE]
>
>删除资产会将其从发布实例中删除。 删除资产也会删除其版本历史记录（基本版本除外）。

1. 选择资产，然后点按&#x200B;**[!UICONTROL Delete]** ![delete](assets/delete.png)。

   >[!NOTE]
   >
   >当您通过点按资产来显示资产详细信息，或者通过点按查看属性![视图属性](assets/viewproperties.png)来显示资产属性时，删除选项也会可用。

1. 在删除资产之前，会显示一个确认对话框。 点按&#x200B;**[!UICONTROL 删除]**。

   >[!NOTE]
   >
   >只会删除选定的资产，而不会删除从属资产和。 要检查资产的引用，请点按![引用](assets/references.png)，然后选择资产。
   >
   >
   >如果您尝试删除的资产是另一个资产的子资产，则不会删除该资产。 要删除此类资产，请从其他资产中删除对该资产的引用，然后重试。

## 受保护的自适应表单{#protected-adaptive-forms}

您可以为希望选定用户访问的表单启用身份验证。 为表单启用身份验证后，用户在访问之前会看到登录屏幕。 只有具有授权凭据的用户才能访问表单。

要为表单启用身份验证，请执行以下操作：

1. 在浏览器中，在发布实例中打开configMgr。\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. 在Adobe Experience Manager Web Console配置中，单击&#x200B;**Apache Sling身份验证服务**&#x200B;以对其进行配置。
1. 在显示的Apache Sling身份验证服务对话框中，使用&#x200B;**+**&#x200B;按钮添加路径。\
   添加路径时，将为该路径中的表单启用身份验证服务。
