---
title: 在表单中创建和管理资产审核
seo-title: Creating and managing reviews for assets in forms
description: 审核是一种机制，它允许一个或多个审核者对表单中可用的资源进行评论。
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# 在表单中创建和管理资产审核{#creating-and-managing-reviews-for-assets-in-forms}

## 审核 {#review}

审核是一种机制，它允许一个或多个审核者对表单中可用的资源进行评论。

## 设置审阅 {#setting-up-a-review}

1. 导航到Forms选项卡并选择表单。
1. 如果资产没有正在进行的审核，则开始审核 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 图标。 单击“开始复查” ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 图标。
1. 输入以下信息：

   * 审核名称：必填项，可包含字母数字字符、连字符或下划线。
   * 审核描述：可选，用于审核的目的/内容的描述。
   * 审核截止日期：可选，审核结束的日期。 超过截止日期时，该任务显示为“过期”。
   * 审阅者：必须至少有一个。 使用组合框添加审阅人。 键入名称可列出所有匹配的名称；选择名称并单击“添加”。

1. 填写其余所有详细信息，然后单击“开始”。

### 设置审核时发生的操作 {#actions-that-occur-when-a-review-is-set-up}

本节介绍创建或设置审阅时会发生什么情况。

1. 将创建一个新的审阅任务并将其分配给审阅发起人。
1. 将为所有审阅人分配一个审阅任务。 任务将显示在其通知部分中。 查看者可以单击通知，或转到“收件箱”查看任务。 审阅人可单击以打开审阅任务、查看表单并开始添加注释。

   ![查看者通知警报](assets/noti.png)

   查看者通知警报

1. 该注释框可供资产的发起人和审阅人使用。 其他人可以查看注释，但不能编写注释。

## 管理审阅 {#managing-a-review}

>[!NOTE]
>
>只能修改正在进行的审阅。 无法修改已完成的审核。

1. 导航到Forms选项卡并选择表单。

1. 如果资产正在进行审阅，并且您是审阅的发起人，则管理审阅 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 图标显示在操作栏中。 只有审阅发起人才能管理（更新/结束）审阅。

   单击管理复查 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)图标。

   对于启动器以外的用户，“管理审阅”图标处于禁用状态。

1. 您将获得一个显示信息的屏幕：

   * **审核名称**：无法编辑。

   * **查看描述**：可用于编辑。

   * **审核截止日期**：可用于编辑。 可以将截止日期修改为当前日期和时间之后的任何日期和时间。

   * **审阅者**：可用于编辑。 您可以添加或删除审阅人。 如果任务过期，则只有在截止日期延长到当前日期之后才能添加审阅人。

1. 编辑必要的字段，然后单击“更新”。

   ![在任务管理器中查看更新的状态](assets/tskmgr.png)

   在任务管理器中查看更新的状态

1. 要结束审阅，请单击“结束”。

### 修改审阅时发生的操作 {#actions-that-occur-when-a-review-is-modified}

此部分介绍审阅结束/修改时执行的操作：

1. 如果修改了Review描述，将更新审阅者和发起者的相应任务。
1. 如果修改了审阅截止日期，审阅人的相应任务将使用新日期更新。

1. 如果移除审阅者：

   ![删除审阅人](assets/removeduser.png)

   删除审阅人

   1. 如果不完整，则终止分配的任务。
   1. 查看者无法再对资源进行评论。

1. 如果添加了审阅人：

   ![添加审阅者](assets/addedreviewer.png)

   添加审阅者

   1. 创建审阅任务并将其分配给新添加的审阅人。
   1. 新添加的审阅者可以为资源添加注释。

1. 当审核结束时：

   1. **审阅者**：对于每个审阅人，与审阅相关的未完成任务将终止。 任务在查看者的“通知”部分中不再显示为“待处理”。
   1. **发起者**：分配给审阅发起人的任务被标记为“完成”。 任务将从审阅发起人的Notification部分删除。
   1. **全部**：该审阅显示在以前的审阅部分中。 无法添加其他注释。
