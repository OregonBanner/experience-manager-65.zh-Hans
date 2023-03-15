---
title: 使用停止的操作和分支
seo-title: Working with stalled operations and branches
description: “停止的操作”页和“停止的分支”页显示了停止的进程。
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 使用停止的操作和分支 {#working-with-stalled-operations-and-branches}

“停止的操作”页和“停止的分支”页显示了停止的进程。 如果在操作执行期间或之后发生错误，或者由于进程中有意停顿操作，进程可能会停顿：

* 操作可能会由于不可预见的错误而停止。 但是，进程中的“停止分支”操作会故意阻止进程进一步运行，并要求管理员进行干预。
* 在规则评估期间，分支可能会在操作之间停顿。

当进程停止时，不会运行其他操作，直到问题得到修复并且操作或分支重新启动。

对于每个停顿的项目，列表会显示以下信息：

**操作名称或分支名称：** 操作或分支的名称。

**状态：** 对于停滞的项目，始终处于停滞状态。

**错误：** 问题的简短描述。

**进程ID：** 形成工作流在进程实例化（即，当用户或自动步骤启动进程时）时分配的正整数。 您可以使用此标识符来跟踪流程实例的整个生命周期。

**进程名称 — 版本：** 在Workbench中分配的流程的名称。

**停止日期：** 操作或分支停止的日期和时间。

您可以在“停止的操作”或“停止的分支”页面上执行以下任务：

* 选择一个错误以查看有关该错误的详细信息。 选择错误后，将显示“错误详细信息”页面。
* 终止或重试停止的操作或重试停止的分支。

## 终止或重试停止的操作或分支 {#terminating-or-retrying-stalled-operations-or-branches}

在“停止的操作”页面上，可以终止显示的进程实例。

终止进程实例后，进程实例将停止运行，并且不会执行进一步的操作。 通常，只有在进程因错误而被阻止或不可用，并且无法修复和重新启动时，才终止该进程。

在“停止的操作”页面或“停止的分支”页面上，您可以重试该操作或分支。

当您重试某个操作时，会向Forms工作流发送一个重新启动该操作的请求。 如果导致进程停止的错误已修复，并且重试请求成功，则进程将从停止点重新开始运行，其状态将更改为RUNNING。 如果无法重新启动该操作，则该操作将保持停止状态，您可能需要终止它。

### 终止停止的操作 {#terminate-a-stalled-operation}

1. 在管理控制台中，单击服务>表单工作流>停止的操作错误。
1. 在“停止的操作”页面上，选择要终止的项目，然后单击“终止”。

### 重试停止的操作或分支 {#retry-a-stalled-operation-or-branch}

1. 在管理控制台中，单击服务>表单工作流，然后单击停止的操作错误或停止的分支错误。
1. 在“停止的操作”或“停止的分支”页面上，选择要重试的项目，然后单击“重试”。

## 查看有关停止的操作或分支的错误详细信息 {#viewing-error-details-about-stalled-operations-or-branches}

如果从“停止的操作”或“停止的分支”页上的停止项目列表中选择错误，则会显示“错误详细信息”页，该页显示有助于解决该问题的错误详细信息。

页面底部的框包含错误信息。

您还可以从“错误详细信息”页面终止或重试停止的操作，并重试停止的分支。

## 当提升用户不存在时，进程不会停止 {#process-does-not-stall-when-escalation-user-does-not-exist}

当AEM Forms User服务中的“分配任务”操作配置为在特定时间段后将该任务提升给另一个用户，并且提升用户在“分配任务”操作执行之后但在提升发生之前被删除时，会发生错误。

发生此情况时，进程和任务的状态在配置的升级时间不会更改，升级不会发生，但进程不会停止。 服务器日志中显示以下消息：

“为提升指定的主体无效，对于taskID： *数字*，指定队列： *数字*.”

如果在生成任务之前（在分配任务操作执行之前）删除提升用户，则进程会停止或引发InvalidPrincipal异常事件。

为防止出现此问题，当您删除某个用户时，请搜索属于该用户的任务并相应地处理这些任务。 (请参阅 [使用任务](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
