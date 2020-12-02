---
title: 将提交审阅者与表单关联
seo-title: 将提交审阅者与表单关联
description: 了解如何将提交审阅者与AEM Forms的表单关联。 关联的审阅者会审阅通过表单门户提交的表单。
seo-description: 了解如何将提交审阅者与AEM Forms的表单关联。 关联的审阅者会审阅通过表单门户提交的表单。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# 将提交审阅者与表单{#associating-submission-reviewers-with-a-form}关联

创建表单时，您可以指定通过表单门户查看表单提交情况并提供反馈的用户。 您的组织可以收集对已提交表单的反馈和返工。

AEM Forms允许您将审阅者组与表单关联。 添加到表单审阅组的用户可以查看此表单的提交情况并提供反馈。

分配给表单的审阅者组只能审阅指定表单的提交。

## 先决条件 {#prerequisite}

### 使用元数据模式编辑器{#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}为自适应表单启用提交审阅者组属性

要将审阅者组与表单关联，请编辑自适应表单的元数据模式。 默认情况下，不能向提交的表单中添加审阅者组。

要编辑元数据模式:

1. 在创作模式下，在Experience Manager下，单击&#x200B;**工具** > **资产** > **元数据模式**。
1. 在“模式Forms”页中，导航至&#x200B;**Forms** > **在AEM中创作的Forms。**

   页面的URL为：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 选择&#x200B;**自适应表单**&#x200B;并单击&#x200B;**编辑**。
1. 在“编辑表单”页面中，单击&#x200B;**高级**。
1. 在高级选项卡中，拖放构建表单下可用的&#x200B;**单行文本**&#x200B;组件。
1. 选择添加的文本组件以查看其设置。

   在“设置”下，在“映射到属性”字段中输入`./jcr:content/metadata/form-submission-reviewer-group`。

   自适应表单的高级属性中的提交审阅者组字段将启用您在字段标签下指定的名称。

## 将提交审阅者与表单{#associating-submission-reviewers-with-a-form-1}关联

要将提交审阅者与自适应表单关联，请创建审阅者组并向其添加用户。 在表单的高级属性中，在表单提交审阅者字段下添加创建的审阅者组。
用户组允许您将不同的提交审阅者集与不同的自适应表单相关联。 此功能可防止未经授权的用户进行提交审阅。

在执行以下步骤之前，请参阅[入门项目](../../forms/using/adding-reviewers-form.md#prerequisite)。

要创建组并向其添加成员，请导航到&#x200B;**工具** > **操作** > **安全** > **组**。
有关详细信息，请参阅[用户管理和服务](/help/sites-administering/security.md)。
确保将您创建的用户组添加为现成用户组的成员：**forms-submission-reviewers**。 此用户组随AEM Forms提供，它确保将用户添加为提交审阅者。

要将用户组与自适应表单关联，请执行以下操作：

1. 在创作模式中，导航到&#x200B;**Forms** > **Forms和文档**。
1. 使用**选择**选项选择自适应表单，然后单击&#x200B;**视图属性**。
1. 在表单的“属性”窗口中，单击&#x200B;**编辑**，然后单击&#x200B;**高级**。
1. 在提交审阅者组字段中输入该组，然后单击&#x200B;**完成**。

   此时将显示提交审阅者组字段，其名称与您在自适应表单的已编辑元数据模式中指定的名称相同。

>[!NOTE]
>
>复制用户和表单，确保在远程实施AEM Forms时可获得用户和表单。
>
>确保所有用户被复制为在远程实施中查看用户组成员。

