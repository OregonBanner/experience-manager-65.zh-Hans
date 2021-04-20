---
title: 将HTML5表单另存为草稿
seo-title: 将HTML5表单另存为草稿
description: 将HTML5表单另存为草稿，然后在以后的阶段继续填写表单。
seo-description: 将HTML5表单另存为草稿，然后在以后的阶段继续填写表单。
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---


# 将HTML5表单另存为草稿{#saving-an-html-form-as-a-draft}

您可以将HTML5表单保存为草稿，并在以后的阶段继续填写表单。 Forms Portal允许任何用户保存和恢复HTML5表单。 要启用“另存为草稿”功能，请向用户档案节点添加以下配置：

## 允许“另存为草稿”功能的自定义用户档案{#custom-profile-to-allow-save-as-draft-feature}

开箱即用，AEM Forms提供&#x200B;**另存为草稿**&#x200B;用户档案。 您可以使用“另存为草稿”用户档案渲染表单，以启用HTML5表单的草稿功能。 可以在[Forms Manager](/help/forms/using/introduction-managing-forms.md)中为表单指定HTML渲染用户档案。

要为现有的[自定义用户档案](/help/forms/using/custom-profile.md)启用“另存为草稿”功能，请向自定义用户档案节点添加以下属性：

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
   <td><p>启用另存为拔模特征</p> <p>对此用户档案。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>允许上传附件</p> <p>这用户档案。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿存储和列表{#drafts-storage-and-listing}

为表单启用“另存为草稿”功能后；保存表单后，它将列在[草稿和提交组件](/help/forms/using/draft-submission-component.md)中。 您可以检索并开始填写从草稿和提交组件保存的表单。

要为“草稿”和“提交”组件启用表单列表，请向“用户档案”节点添加以下属性：

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
   <td>允许提交后草稿和表单列在<br /> Forms Portal草稿和提交组件中</td>
  </tr>
 </tbody>
</table>

默认情况下，AEM Forms将与表单的草稿和提交关联的用户数据存储在Publish实例的/content/forms/fp节点中。 您可以添加自定义存储提供程序，有关详细信息，请参阅[草稿和提交组件的自定义存储](/help/forms/using/adding-custom-storage-provider-forms.md)。
