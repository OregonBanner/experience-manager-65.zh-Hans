---
title: 草稿和提交组件
seo-title: Drafts and submissions component
description: 草稿和提交组件列出了处于草稿状态且已提交的表单。 您可以自定义组件的外观和样式。
seo-description: Drafts and submissions component lists forms that are in the draft state and are already submitted. You can customize appearance and style of the component.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# 草稿和提交组件{#drafts-and-submissions-component}

草稿和提交组件列出了处于草稿状态的所有表单以及已提交的表单。 该组件为草稿和提交的表单分别提供了多个部分（选项卡）。 用户只能查看其草稿和提交的表单。

## 配置组件 {#configuring-the-component}

“草稿和提交”组件有两个选项卡：草稿和提交。

要允许提交自适应表单以显示在提交选项卡中，请将 **提交操作** to **[Forms Portal提交操作](../../forms/using/configuring-submit-actions.md). 或者，** 启用Forms Portal提交选项。 每当用户提交表单时，表单都会添加到提交选项卡。

草稿功能现成可用。 用户单击 **保存** 在自适应表单上，表单会添加到“草稿”选项卡。

执行以下步骤以添加和配置“草稿和提交”组件：

1. 拖放 **草稿和提交** 组件（在页面上的组件浏览器中为“文档服务”类别下）。
1. 点按组件，然后点按 ![settings_icon](assets/settings_icon.png) 打开组件的编辑对话框。

   ![草稿和提交组件](assets/drafts-submissions-edit.png)

1. 在编辑对话框中，指定以下详细信息并点按 **完成** 来保存设置。

<table>
 <tbody>
  <tr>
   <th>制表符</th>
   <th>配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>常规</td>
   <td>总结果</td>
   <td>指定要显示的结果的最大数量。 如果结果计数增加总结果限制，则 <strong>更多 </strong>链接会显示在组件底部。 单击 <strong>更多 </strong>显示所有表单。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>样式类型</td>
   <td>指定组件的样式。 您可以指定 <strong>无样式</strong>, <strong>默认样式</strong>或 <strong>自定义样式</strong> ，以列出表单。 对于自定义样式选项，您可以在 <strong>自定义样式路径 </strong>字段<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自定义样式路径</td>
   <td>如果您选择 <strong>自定义样式</strong> 选项 <strong>样式类型</strong> 字段，请使用 <strong>自定义样式路径</strong> 字段以指定自定义CSS文件的路径。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>显示选项</td>
   <td><p>指定要显示的选项卡。 您可以选择显示草稿表单、已提交表单，或同时显示两者。 </p> <p><strong>注意</strong>:<em> 对于 <strong>显示选项</strong>，如果您选择 <strong>两者兼有</strong>, <strong>默认选项卡</strong> 字段，则不会使用此选项。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>默认选项卡</td>
   <td>指定在Forms Portal页面加载时要显示的选项卡。 您可以选择 <strong>草稿Forms选项卡</strong> 和 <strong>已提交的Forms选项卡</strong>.</td>
  </tr>
  <tr>
   <td>草稿Forms选项卡配置</td>
   <td>自定义标题</td>
   <td>指定 <strong>草稿Forms</strong> 选项卡。 默认值为 <strong>草稿Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>指定用于草稿Forms列表的布局。</td>
  </tr>
  <tr>
   <td>已提交的Forms选项卡配置</td>
   <td>自定义标题 </td>
   <td>指定 <strong>已提交Forms </strong>选项卡。 默认值为 <strong>已提交Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>指定用于已提交的Forms的布局<strong> </strong>列表。 </td>
  </tr>
 </tbody>
</table>

## 自定义存储 {#customizing-the-storage}

当您使用Forms Portal提交操作或在自适应表单中启用“在表单门户中存储数据”选项时，表单数据会存储在AEM存储库中。 在生产环境中，建议不要将草稿或提交的表单数据存储在AEM存储库中。 您而是必须将草稿和提交组件与安全存储（如企业数据库）集成，以存储草稿和提交的表单数据。

Forms Portal允许您将数据存储在本地AEM存储库、远程AEM存储库或数据库中。 AEM Forms允许您自定义存储草稿和提交的用户数据的实施。 您可以覆盖默认方法，以指定草稿和提交数据在所选存储中的存储方式。 例如，您可以将数据存储在您组织中当前实施的数据存储中。

Forms Portal提供开箱即用的服务(API)，用于在本地和远程AEM Forms发布实例的crx存储库上存储数据。 您可以替换默认实施，如 [为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md) 文章，以替换默认功能。 有关自定义实施中在安全位置存储内容所需方法的详细信息，请参阅 [自定义草稿和提交数据服务](/help/forms/using/custom-draft-submission-data-services.md) 和 [草稿和提交组件的自定义存储。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms文档提供了 [将草稿和提交组件与数据库集成的示例](integrate-draft-submission-database.md). 您可以使用示例实施来开发您自己的自定义实施。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列出表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)
