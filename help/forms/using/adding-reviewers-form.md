---
title: 将提交审阅人与表单关联
seo-title: Associating submission reviewers with a form
description: 了解如何将提交审阅人与AEM Forms中的表单相关联。 关联的审阅人审阅通过Forms Portal提交的表单。
seo-description: Learn how to associate submission reviewers with a form in AEM Forms. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: Adaptive Forms
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 10%

---

# 将提交审阅人与表单关联 {#associating-submission-reviewers-with-a-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

在创建表单时，您可以指定审阅通过表单门户提交的表单并提供反馈的用户。 贵组织可以收集反馈并对提交的表单进行返工。

AEM Forms允许您将审阅者组与表单关联。 添加到表单审核组的用户，可以查看该表单的提交并提供反馈。

分配给表单的审阅人组只能审阅指定表单的提交。

## 先决条件 {#prerequisite}

### 使用元数据架构编辑器启用自适应表单的提交审核者组属性 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

要将审阅者组与表单关联，请编辑自适应表单的元数据架构。 默认情况下，您无法将审阅者组添加到已提交的表单。

要编辑元数据架构，请执行以下操作：

1. 在创作模式的Experience Manager下，单击 **工具** > **资产** > **元数据架构**.
1. 在架构Forms页面中，导航到 **Forms** > **Forms在AEM中创作。**

   页面的URL为：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 选择 **自适应表单** 并单击 **编辑**.
1. 在“编辑表单”页中，单击 **高级**.
1. 在高级选项卡中，拖放 **单行文本** “构建表单”下可用的组件。
1. 选择添加的文本组件以查看其设置。

   在设置下，输入 `./jcr:content/metadata/form-submission-reviewer-group` 在映射到属性字段中。

   自适应表单的高级属性中的提交审核者组字段使用您在字段标签下指定的名称启用。

## 将提交审阅人与表单关联 {#associating-submission-reviewers-with-a-form-1}

要将提交审阅人与自适应表单关联，请创建一个审阅人组并将用户添加到该组。 在表单高级属性的表单提交审阅人字段下添加创建的审阅人组。
用户组允许您将不同的提交审阅人集与不同的自适应表单相关联。 此功能可防止未经授权的用户进行提交审核。

执行以下步骤之前，请参阅 [先决条件](../../forms/using/adding-reviewers-form.md#prerequisite).

要创建组并向其添加成员，请导航至 **工具** > **操作** > **安全性** > **组**.
有关更多信息，请参阅 [用户管理和服务](/help/sites-administering/security.md).
确保将您创建的组添加为现成用户组的成员： **表单 — 提交 — 审阅者**. 此用户组随AEM Forms一起提供，可确保将用户添加为提交评审员。

要将用户组与自适应表单关联，请执行以下操作：

1. 在创作模式下，导航到 **Forms** > **Forms和文档**.
1. 使用**选择**选项选择自适应表单，然后单击 **查看属性**.
1. 在窗体的“属性”窗口中，单击 **编辑**，然后单击 **高级**.
1. 在提交审核者组字段中输入组，然后单击 **完成**.

   此时将显示提交审核者组字段，其中包含您在自适应表单的已编辑元数据架构中指定的名称。

>[!NOTE]
>
>复制用户和表单，以确保AEM Forms远程实施中的用户和表单的可用性。
>
>确保所有用户都作为查看远程实施中用户组的成员进行复制。
