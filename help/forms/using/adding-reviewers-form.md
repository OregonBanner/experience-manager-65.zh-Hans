---
title: 将提交审阅人与表单关联
seo-title: 将提交审阅人与表单关联
description: 了解如何在AEM Forms中将提交审阅人与表单关联。 相关审阅人会审核通过表单门户提交的表单。
seo-description: 了解如何在AEM Forms中将提交审阅人与表单关联。 相关审阅人会审核通过表单门户提交的表单。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: 自适应表单
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# 将提交审阅人与表单{#associating-submission-reviewers-with-a-form}关联

在创建表单时，您可以指定通过表单门户查看表单提交情况并提供反馈的用户。 贵组织可以收集对已提交表单的反馈和返工。

AEM Forms允许您将审阅人组与表单关联。 添加到表单审核组的用户可以查看此表单提交情况并提供反馈。

分配给表单的审阅者组只能审核指定表单的提交。

## 先决条件 {#prerequisite}

### 使用元数据架构编辑器{#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}启用自适应表单的提交审阅者组属性

要将审阅人组与表单关联，请编辑自适应表单的元数据架构。 默认情况下，您无法将审核者组添加到已提交的表单中。

要编辑元数据架构，请执行以下操作：

1. 在创作模式下，在Experience Manager下，单击&#x200B;**工具** > **资产** > **元数据架构**。
1. 在架构Forms页面中，导航到&#x200B;**Forms** > **在AEM中创作的Forms。**

   页面的URL是：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 选择&#x200B;**自适应表单**&#x200B;并单击&#x200B;**编辑**。
1. 在“编辑表单”页面中，单击&#x200B;**Advanced**。
1. 在高级选项卡中，拖放“构建表单”下可用的&#x200B;**单行文本**&#x200B;组件。
1. 选择添加的文本组件可查看其设置。

   在设置下，在映射到属性字段中输入`./jcr:content/metadata/form-submission-reviewer-group`。

   自适应表单的高级属性中的提交审核者组字段将启用，并使用您在字段标签下指定的名称。

## 将提交审阅人与表单{#associating-submission-reviewers-with-a-form-1}关联

要将提交审阅人与自适应表单关联，请创建审阅人组并将用户添加到该组。 在表单高级属性的表单提交审核者字段下添加已创建的审核者组。
用户组允许您将不同的提交审阅人集与不同的自适应表单相关联。 此功能可防止未经授权的用户进行提交审核。

在执行以下步骤之前，请参阅[先决条件](../../forms/using/adding-reviewers-form.md#prerequisite)。

要创建组并向其添加成员，请导航到&#x200B;**工具** > **操作** > **安全** > **组**。
有关更多信息，请参阅[用户管理和服务](/help/sites-administering/security.md)。
确保将创建的组添加为现成用户组的成员：**forms-submission-reviewers**。 此用户组随AEM Forms一起提供，它可确保将用户添加为提交审阅人。

要将用户组与自适应表单关联，请执行以下操作：

1. 在创作模式下，导航至&#x200B;**Forms** > **Forms和文档**。
1. 使用**选择**选项选择自适应表单，然后单击&#x200B;**查看属性**。
1. 在表单的“属性”窗口中，单击&#x200B;**编辑**，然后单击&#x200B;**高级**。
1. 在提交审核者组字段中输入组，然后单击&#x200B;**Done**。

   将显示提交审核者组字段，其中包含您在自适应表单的编辑元数据架构中指定的名称。

>[!NOTE]
>
>复制用户和表单，以确保在AEM Forms的远程实施中提供用户和表单。
>
>确保将所有用户复制为远程实施中审核用户组成员。
