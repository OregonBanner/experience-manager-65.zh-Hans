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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 将HTML5表单另存为草稿 {#saving-an-html-form-as-a-draft}

您可以将HTML5表单另存为草稿，并在以后的阶段继续填写表单。 Forms Portal允许任何用户保存和恢复HTML5表单。 要启用“另存为草稿”功能，请将以下配置添加到配置文件节点：

## 允许“另存为草图”功能的自定义配置文件 {#custom-profile-to-allow-save-as-draft-feature}

开箱即用，AEM Forms会提供另存为草 **稿配置文件** 。 您可以使用“另存为草稿”配置文件渲染表单，以启用HTML5表单的草稿功能。 您可以在 [Forms Manager中为表单指定HTML渲染配置文件](/help/forms/using/introduction-managing-forms.md)。

要为现有自定义配置文件启用另存为草稿 [功能](/help/forms/using/custom-profile.md)，请向自定义配置文件节点添加以下属性：

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
   <td><p>启用另存为绘制功能</p> <p>对于此配置文件。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>允许上传附件</p> <p>用这个档案。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿存储和列表 {#drafts-storage-and-listing}

为表单启用“另存为草稿”功能后；保存表单后，表单将列在草稿和提 [交组件中](/help/forms/using/draft-submission-component.md)。 您可以检索并开始填写从草稿和提交组件保存的表单。

要为“草稿”和“提交”组件启用表单列表，请将以下属性添加到配置文件节点：

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
   <td>使草稿和表单在提交后在<br /> Forms Portal“草稿和提交”组件中列出</td>
  </tr>
 </tbody>
</table>

默认情况下，AEM Forms会在“发布”实例的/content/forms/fp节点中存储与表单的草稿和提交相关的用户数据。 您可以添加自定义存储提供商，以了解详细信息，请参 [阅草稿和提交的自定义存储组件](/help/forms/using/adding-custom-storage-provider-forms.md)。
