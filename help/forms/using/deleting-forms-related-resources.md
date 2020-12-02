---
title: 删除表单和相关资源
seo-title: 删除表单和相关资源
description: 如何删除AEM Forms的表单或资产，以及对引用和引用资产及XFA表单的影响。
seo-description: 如何删除AEM Forms的表单或资产，以及对引用和引用资产及XFA表单的影响。
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# 删除表单和相关资源{#deleting-forms-and-related-resources}

您可以删除表单和资产，以从存储库中删除这些资产。 删除操作适用于所有资产类型和文件夹。

如果您从作者实例中删除资产，该资产也会从发布实例中删除。 AEM Forms服务器由作者实例和发布实例组成。 创作实例用于创建和管理表单资产和资源。 发布实例包含可供最终用户使用的已发布表单资产和相关资源。

## 如何删除表单{#how-to-delete-a-form}

1. 通过访问`https://[hostname]:'port'/aem/forms.html.`登录AEM Forms用户界面
1. 导航到要删除的表单并选择它。 单击工具栏中的删除![aem6forms_delete2](assets/aem6forms_delete2.png)并确认删除操作。

   >[!NOTE]
   >
   >一次只能删除一个表单。 单独删除多个表单或删除父级文件夹。

1. 在删除资产之前，AEM Forms会检查引用并请求明确确认。 如果要删除资产而不考虑关系状态，请单击强制删除。

   >[!NOTE]
   >
   >删除由其他资产引用的资产可能会导致功能问题。

   >[!NOTE]
   >
   >如果选定的资产是文件夹，并且其层次结构中包含此类资产，则单独删除其他资产，或删除整个文件夹。

## 删除引用的XFA表单{#impact-of-deleting-a-referenced-xfa-form}的影响

在AEM Forms,XFA表单模板可以由自适应表单或其他XFA表单模板引用。 此外，模板可以引用资源或其他XFA模板。

不建议删除由自适应表单引用的XFA表单，因为它可能会损坏自适应表单。 当自适应表单引用XFA表单时，其字段将绑定。 删除XFA后，自适应表单无法将其字段与XFA字段同步，并会显示此类字段的错误消息。 要进一步了解引用的XFA删除和脏AF的影响，请参阅[更新引用的XFA表单](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)。

要删除此类XFA表单，请更新自适应表单并删除与XFA字段绑定。
