---
title: 在表单中创建和管理资产的审阅
seo-title: 在表单中创建和管理资产的审阅
description: '审阅是一种机制，允许一个或多个审阅者对表单中提供的资产进行注释。 '
seo-description: '审阅是一种机制，允许一个或多个审阅者对表单中提供的资产进行注释。 '
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---


# 在表单中创建和管理资产的审阅{#creating-and-managing-reviews-for-assets-in-forms}

## 审核 {#review}

审阅是一种机制，允许一个或多个审阅者对表单中提供的资产进行注释。

## 设置审阅{#setting-up-a-review}

1. 导览至“Forms”选项卡，然后选择一个表单。
1. 如果资产没有进行审阅，则“操作”栏中会显示开始审阅![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)图标。 单击开始查看![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)图标。
1. 输入以下信息：

   * 审阅名称：必填，可包含字母数字字符、连字符或下划线。
   * 查看说明：（可选）用于审阅的目的/内容的描述。
   * 审阅截止日期：（可选）审核结束的日期。 超过截止日期后，任务将显示为“逾期”。
   * 审阅人：至少1个是强制性的。 使用组合框可添加审阅者。 键入名称会列表所有匹配的名称；选择一个名称，然后单击“添加”。

1. 填写所有剩余的详细信息，然后单击“开始”。

### 设置{#actions-that-occur-when-a-review-is-set-up}审阅时发生的操作

本节介绍创建或设置审阅时发生的情况。

1. 将创建新的审阅任务并将其分配给审阅的发起者。
1. 为所有审阅者分配了审阅任务。 任务将显示在其“通知”部分。 审阅者可以单击通知，或转到收件箱以视图任务。 审阅者可以单击以打开审阅任务,视图表单，并开始添加注释。

   ![审阅者通知警报](assets/noti.png)

   审阅者通知警报

1. 资产的发起人和审阅人可以使用评论框。 其他人可以视图注释，但不能写注释。

## 管理审阅{#managing-a-review}

>[!NOTE]
>
>只能修改正在进行的审阅。 无法修改已完成的审阅。

1. 导览至“Forms”选项卡，然后选择一个表单。

1. 如果资产正在进行审阅，而您是审阅的发起人，则“操作”栏中将显示“管理审阅” ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)图标。 只有审阅发起人才能管理（更新/结束）审阅。

   单击“管理审阅![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)”图标。

   对于发起方以外的用户，“管理审阅”图标处于禁用状态。

1. 您会看到一个显示信息的屏幕：

   * **审阅名称**:无法编辑。

   * **查看说明**:可供编辑。

   * **审阅截止日期**:可供编辑。您可以将截止日期修改为超过当前日期和时间的任何日期和时间。

   * **审阅人**:可供编辑。可以添加或删除审阅者。 如果任务逾期，则只能在将截止日期延长到超过当前日期之后添加审阅者。

1. 编辑必要的字段，然后单击“更新”。

   ![在任务 Manager中查看更新状态](assets/tskmgr.png)

   在任务 Manager中查看更新状态

1. 要结束审阅，请单击“结束”。

### 修改审阅时发生的操作{#actions-that-occur-when-a-review-is-modified}

本节介绍审阅结束/修改时发生的情况：

1. 如果修改了“审阅”描述，则会更新审阅者和发起者的相应任务。
1. 如果修改了审阅截止日期，则审阅者的相应任务将更新为新日期。

1. 如果删除了审阅者：

   ![删除审阅者](assets/removeduser.png)

   删除审阅者

   1. 如果未完成，则终止分配的任务。
   1. 审阅人无法再对资产进行注释。

1. 如果添加了审阅者：

   ![添加审阅者](assets/addedreviewer.png)

   添加审阅者

   1. 将创建审阅任务并将其分配给新添加的审阅者。
   1. 新添加的审阅人可以为资产添加注释。

1. 审阅结束时：

   1. **审阅人**:对于每个审阅者，与审阅相关的未完成任务被终止。任务在审阅者的“通知”部分中不再显示为“待定”。
   1. **启动器**:分配给审阅发起者的任务标记为完成。任务将从审阅发起者的“通知”部分删除。
   1. **全部**:该审阅显示在“上一个审阅”(Previous Reviews)部分。不能添加其他评论。

