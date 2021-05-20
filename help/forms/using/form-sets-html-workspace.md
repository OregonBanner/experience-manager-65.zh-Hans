---
title: 在AEM Forms工作区中使用表单集
seo-title: 在AEM Forms工作区中使用表单集
description: 表单集是HTML5表单的集合，分组后以一组表单形式呈现给最终用户。 了解如何在AEM Forms工作区中使用表单集。
seo-description: 表单集是HTML5表单的集合，分组后以一组表单形式呈现给最终用户。 了解如何在AEM Forms工作区中使用表单集。
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# 在AEM Forms工作区中使用表单集{#working-with-formsets-in-aem-forms-workspace}

表单集是HTML5表单的集合，分组后以一组表单形式呈现给最终用户。 当最终用户开始填写表单集时，他们会从一个表单无缝地转换到另一个表单。 然后，只需单击一次即可提交一组表单。 有关表单集以及如何设置表单集的更多信息，请参阅AEM Forms](../../forms/using/formset-in-aem-forms.md)中的[表单集。

AEM Forms工作区支持表单集。 使用表单集，可以将与服务或流程相关的多个表单分组，以自动执行业务流程并呈现给最终用户。 在这种情况下，用户可以将整个集合作为一个进行填充，而且无需存档、提交和跟踪单个表单或进程。

## 将表单集附加到AEM Forms工作区应用程序{#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}中的起始点

1. 在Workbench中创建业务流程工作流。 有关更多信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。
1. 从起点的进程属性中，选择演示和数据中的&#x200B;**使用CRX资产**。

   ![1-3](assets/1-3.png)

1. 单击CRX资产路径旁边的![browse](assets/browse.png)（浏览）。 此时会出现“选择表单资产”对话框。

   ![2-1](assets/2-1.png)

1. 单击&#x200B;**Formset**&#x200B;选项卡，从列表中选择相关的表单集，然后单击&#x200B;**OK**。

1. 在更新其他相关流程属性后部署应用程序。

## 在AEM Forms工作区{#using-formset-in-nbsp-aem-forms-workspace}中使用表单集

将表单集附加到起始点后，可以从AEM Forms工作区中调用起始点，就像调用任何其他起始点一样。

通过AEM Forms工作区对表单集支持的操作包括：

* 另存为草稿
* 锁定
* 放弃
* 提交
* 添加附件
* 添加注释
* 使用“返回”或“下一步”按钮在表单集中的表单之间移动

![3-1](assets/3-1.png)

>[!NOTE]
>
>为了在表单集中从上一个表单和下一个表单移动期间提高性能，在相关表单完全呈现之前，所有工作区按钮(“返回”、“下一个”、“保存”、“提交”和……（更多）)都处于禁用状态。
