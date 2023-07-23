---
title: 在表单中创建和管理审阅
seo-title: Creating and managing reviews in forms
description: 审阅是一种允许一个或多个审阅人对表单进行评论的机制。
seo-description: A Review is a mechanism that allows one or more reviewers to comment on a form.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 3%

---

# 创建和管理表单审核{#creating-and-managing-reviews-to-forms}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html) |
| AEM 6.5 | 本文 |

## 审核 {#review}

审阅是一种允许一个或多个审阅人对表单进行评论的机制。

## 设置审阅 {#setting-up-a-review}

1. 导航到表单浏览器，然后选择要审阅的表单。
1. 如果表单没有正在进行的审阅， **开始审阅** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 图标。 单击 **开始审阅** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 图标。
1. 输入以下信息：

   * **标题**：必填项，可包含字母数字字符、连字符和下划线。
   * **描述**：可选，用于描述审阅目的/内容。
   * **截止日期**：可选，查看结束的日期。 超过截止日期时，该任务显示为“过期”。
   * **审阅者姓名**：必须至少有一个。 使用组合框添加审阅人，键入包含所有匹配名称的名称列表；选择一个名称并单击 **添加**. 在的下一部分 **审阅者** 选项卡显示所有审阅人的名称。

1. 单击 **开始** 以开始审阅。

   >[!NOTE]
   >
   >* 管理员可以访问与表单用户关联的任何组。
   >* 服务用户组不可选择进行审阅。

### 设置审核时发生的操作 {#actions-that-occur-when-a-review-is-set-up}

本节介绍创建或设置审阅时会发生什么情况。

1. 将创建一个新的审阅任务并将其分配给选定的审阅人。
1. 将为所有审阅人分配一个审阅任务。 任务将显示在其通知部分中。 查看者可以单击通知，或转到“收件箱”查看任务。 审阅人可单击以打开审阅任务、查看表单并开始添加注释。

   ![查看者通知警报](assets/review-notification-img.png)

   查看者通知警报

1. 注释框可供表单的审阅人使用。 其他人可以阅读这些评论，但不能添加自己的评论。

## 管理审阅 {#managing-a-review}

>[!NOTE]
>
>* 只能修改正在进行的审阅。
>* 无法修改已完成的审核。

1. 导航到表单选项卡并选择表单。

1. 如果表单正在进行审阅，并且您是审阅的发起人，则 **管理审核** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 图标显示在操作栏中。 只有审阅发起人才能管理（更新/结束）审阅。

   单击 **管理审核** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)图标。

   对于启动器以外的用户，“管理审阅”图标处于禁用状态。

1. 现在，您会看到一个显示信息的屏幕：

   * **审核名称**：无法编辑。

   * **查看描述**：可用于编辑。

   * **审核截止日期**：可用于编辑。 可以将截止日期修改为当前日期和时间之后的任何日期和时间。

   * **审阅者**：可用于编辑。 您可以添加或删除审阅人。 如果任务过期，则只有在截止日期延长到当前日期之后才能添加审阅人。

1. 要结束审阅，请单击 **结束**.

### 修改审阅时发生的操作 {#actions-that-occur-when-a-review-is-modified}

此部分介绍以下内容的情况： **审核更新/结束**：

1. 如果修改了审阅说明，审阅人和发起人的相应任务将更新。
1. 如果修改了审阅截止日期，审阅人的相应任务将使用新日期更新。

1. 如果移除审阅者：

   ![删除审阅人](assets/removeduser.png)

   删除审阅人

   1. 如果不完整，则终止分配的任务。
   1. 审核者无法再对表单进行评论。

1. 如果添加了审阅人：

   ![添加审阅者](assets/addedreviewer.png)

   添加审阅者

   1. 创建审阅任务并将其分配给新添加的审阅人。
   1. 新添加的审核者可以添加有关表单的注释。

1. 当审核结束时：

   1. **审阅者**：对于每个审阅人，与审阅相关的未完成任务将终止。 任务在查看者的“通知”部分中不再显示为“待处理”。
   1. **发起者**：分配给审阅发起人的任务被标记为“完成”。 任务将从审阅发起人的Notification部分删除。
   1. **全部**：该审阅显示在以前的审阅部分中。 无法添加其他注释。

   ![审查完成](assets/review-complete-imgg.png)
