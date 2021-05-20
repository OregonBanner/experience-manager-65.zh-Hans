---
title: 将HTML5表单另存为草稿
seo-title: 将HTML5表单另存为草稿
description: 将HTML5表单另存为草稿，然后在稍后阶段继续填写表单。
seo-description: 将HTML5表单另存为草稿，然后在稍后阶段继续填写表单。
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: 移动设备表单
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---

# 将HTML5表单另存为草稿{#saving-an-html-form-as-a-draft}

您可以将HTML5表单另存为草稿，然后在以后的阶段继续填写表单。 Forms Portal允许任何用户保存和恢复HTML5表单。 要启用另存为草稿功能，请将以下配置添加到配置文件节点：

## 允许“另存为草稿”功能{#custom-profile-to-allow-save-as-draft-feature}的自定义配置文件

AEM Forms现成提供一个&#x200B;**另存为草稿**&#x200B;配置文件。 您可以渲染具有另存为草稿配置文件的表单，以启用HTML5表单的草稿功能。 您可以在[Forms Manager](/help/forms/using/introduction-managing-forms.md)中为表单指定HTML呈现配置文件。

要为现有[自定义配置文件](/help/forms/using/custom-profile.md)启用另存为草稿功能，请将以下属性添加到自定义配置文件节点：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>启用另存为草稿功能</p> <p>，以查看此用户档案。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>允许上传附件</p> <p>使用此用户档案。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿存储和列表{#drafts-storage-and-listing}

为表单启用另存为草稿功能后；保存表单后，它会列在[草稿和提交组件](/help/forms/using/draft-submission-component.md)中。 您可以从草稿和提交组件中检索并开始填写已保存的表单。

要为草稿和提交组件启用表单列表，请将以下属性添加到配置文件节点：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>字符串</td>
   <td>true</td>
   <td>使草稿和表单在提交后列在<br />Forms Portal的“草稿和提交”组件中</td>
  </tr>
 </tbody>
</table>

默认情况下，AEM Forms会将与表单的草稿和提交相关联的用户数据存储在Publish实例的/content/forms/fp节点中。 您可以添加自定义存储提供程序，有关详细信息，请参阅[草稿和提交组件的自定义存储](/help/forms/using/adding-custom-storage-provider-forms.md)。
