---
title: 在AEM Forms工作区中使用表单集
seo-title: 在AEM Forms工作区中使用表单集
description: 表单集是一组HTML5表单，分组后作为一组表单呈现给最终用户。 了解如何在AEM Forms工作区中使用表单集。
seo-description: 表单集是一组HTML5表单，分组后作为一组表单呈现给最终用户。 了解如何在AEM Forms工作区中使用表单集。
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 在AEM Forms工作区中使用表单集{#working-with-formsets-in-aem-forms-workspace}

表单集是一组HTML5表单，分组后作为一组表单呈现给最终用户。 当最终用户开始填写表单集时，他们会从一个表单无缝过渡到另一个表单。 然后，只需单击一下即可提交表单集。 有关表单集以及如何设置表单集的详细信息，请参阅AEM [表单中的表单集](../../forms/using/formset-in-aem-forms.md)。

AEM Forms工作区支持表单集。 使用表单集，可以将与服务或流程相关的多个表单分组以自动处理业务流程并呈现给最终用户。 在这种情况下，用户可以将整个集合作为一部分进行填写，而无需对单个表单或进程进行归档、提交和跟踪。

## 将表单集附加到AEM Forms工作区应用程序中的起始点 {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. 在Workbench中创建业务流程工作流。 有关详细信息，请参阅 [工作台帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。
1. 从起点的流程属性中，选择“在演 **示和数据中使用CRX资产** ”。

   ![1-3](assets/1-3.png)

1. 单击 ![CRX资产路径旁的浏览](assets/browse.png) （浏览）。 此时将显示“选择表单资产”对话框。

   ![2-1](assets/2-1.png)

1. 单击“ **表单集** ”选项卡，从列表中选择相关表单集，然后单击“确 **定”**。

1. 在更新其他相关进程属性后部署应用程序。

## 在AEM Forms工作区中使用表单集 {#using-formset-in-nbsp-aem-forms-workspace}

将表单集附加到起点后，可以从AEM Forms工作区中调用起点，就像调用任何其他起点一样。

通过AEM Forms工作区对表单集支持的操作有：

* 另存为草稿
* 锁定
* 放弃
* 提交
* 添加附件
* 添加备注
* 使用“返回”或“下一步”按钮在表单集中的表单之间移动

![3-1](assets/3-1.png)

>[!NOTE]
>
>为了在从表单集中的上一个和下一个表单移动期间提高性能，所有工作区按钮（返回、下一个、保存、提交和……）（更多）)禁用，直到相关表单完全呈现。

