---
title: 草稿和提交组件
seo-title: 草稿和提交组件
description: 草稿和提交组件列表处于草稿状态且已提交的表单。 您可以自定义组件的外观和样式。
seo-description: 草稿和提交组件列表处于草稿状态且已提交的表单。 您可以自定义组件的外观和样式。
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# 草稿和提交组件{#drafts-and-submissions-component}

草稿和提交组件将列表处于草稿状态的所有表单以及已提交的表单。 该组件具有用于草稿和提交表单的单独部分（选项卡）。 用户只能视图其草稿和提交的表单。

## 配置组件{#configuring-the-component}

“草稿和提交”组件包含两个选项卡：草稿和提交。

要使自适应表单的提交显示在提交选项卡中，请将&#x200B;**提交操作**&#x200B;设置为&#x200B;**[Forms门户提交操作](../../forms/using/configuring-submit-actions.md)。 或者，**&#x200B;启用“Forms门户提交”选项。 每当用户提交表单时，表单即添加到提交选项卡。

草稿功能现已启用。 当用户单击自适应表单上的&#x200B;**保存**&#x200B;时，表单将添加到草稿选项卡。

执行以下步骤以添加和配置草稿和提交组件：

1. 将组件浏览器中“文档服务”类别下的&#x200B;**草稿和提交**&#x200B;组件拖放到您的页面。
1. 点按组件，然后点按![settings_icon](assets/settings_icon.png)以打开组件的编辑对话框。

   ![草稿和提交组件](assets/drafts-submissions-edit.png)

1. 在编辑对话框中，指定以下详细信息，然后点按&#x200B;**完成**&#x200B;以保存设置。

<table>
 <tbody>
  <tr>
   <th>选项卡·</th>
   <th>配置</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>常规</td>
   <td>总结果</td>
   <td>指定要显示的结果的最大数量。 如果结果计数增加“总结果”限制，则组件底部将显示<strong>更多</strong>链接。 单击<strong>更多</strong>将显示所有表单。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>样式类型</td>
   <td>指定组件的样式。 可以指定<strong>没有样式</strong>、<strong>默认样式</strong>或<strong>自定义样式</strong>来列出表单。 对于“自定义样式选项”，可在<strong>“自定义样式路径</strong>”字段<strong>中指定自定义CSS文件的路径。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>自定义样式路径</td>
   <td>如果在<strong>样式类型</strong>字段中选择<strong>自定义样式</strong>选项，请使用<strong>自定义样式路径</strong>字段指定自定义CSS文件的路径。 </td>
  </tr>
  <tr>
   <td> </td>
   <td>显示选项</td>
   <td><p>指定要显示的选项卡。 您可以选择显示草稿表单、已提交表单或同时显示两者。 </p> <p><strong>注意</strong><em> ：对 <strong>于“显</strong>示”选项 <strong>，如果选择“两者”以外的选</strong>项， <strong>则不</strong> 会使用“默认tabfield”选项。</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>默认选项卡</td>
   <td>指定加载表单门户页面时显示的选项卡。 您可以选择<strong>Forms制表符草稿</strong>和<strong>已提交的Forms制表符</strong>。</td>
  </tr>
  <tr>
   <td>草稿Forms选项卡配置</td>
   <td>自定义标题</td>
   <td>指定<strong>Forms草案</strong>选项卡的标题。 默认值为<strong>Forms草案。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>指定用于“Forms草案”列表的布局。</td>
  </tr>
  <tr>
   <td>已提交的Forms选项卡配置</td>
   <td>自定义标题 </td>
   <td>指定<strong>已提交的Forms</strong>选项卡的标题。 默认值为<strong>已提交的Forms。</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>布局模板</td>
   <td>指定用于已提交Forms<strong> </strong>列表的布局。 </td>
  </tr>
 </tbody>
</table>

## 自定义存储{#customizing-the-storage}

当您使用Forms门户提交操作或启用自适应表单中的“在表单门户中存储数据”选项时，表单数据将存储在AEM存储库中。 在生产环境中，建议不要将草稿或提交的表单数据存储在AEM存储库中。 您必须将草稿和提交组件与安全存储（如企业数据库）集成，以存储草稿和提交的表单数据。

Forms门户允许您在本地AEM存储库、远程AEM存储库或数据库中存储数据。 AEM Forms允许您自定义为草稿和提交文件存储用户数据的实施。 您可以覆盖默认方法，以指定在您选择的存储存储草稿和提交数据的方式。 例如，可以将数据存储在组织中当前实施的数据存储中。

Forms门户提供开箱即用服务(API)，以在本地和远程AEM Forms发布实例的crx-repository上存储数据。 您可以用自定义实现替换默认功能，如[配置草稿和提交的存储服务](/help/forms/using/configuring-draft-submission-storage.md)文章中所述。 有关在安全位置存储内容的自定义实现所需方法的详细信息，请参见[自定义草稿和提交数据服务](/help/forms/using/custom-draft-submission-data-services.md)和[草稿和提交组件的自定义存储。](/help/forms/using/adding-custom-storage-provider-forms.md)

AEM Forms文档提供了将草稿和提交组件与数据库[集成的示例。 ](integrate-draft-submission-database.md)您可以使用示例实现来开发您自己的自定义实现。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列表表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和已提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)
