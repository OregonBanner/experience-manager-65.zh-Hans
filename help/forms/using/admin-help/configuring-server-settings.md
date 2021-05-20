---
title: 配置服务器设置
seo-title: 配置服务器设置
description: “服务器设置”页提供对电子邮件、任务通知和管理员通知设置的访问权限。
seo-description: “服务器设置”页提供对电子邮件、任务通知和管理员通知设置的访问权限。
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2657'
ht-degree: 0%

---

# 配置服务器设置{#configuring-server-settings}

“服务器设置”页面提供了对表单工作流各种设置的访问权限：

* **电子** 邮件设置，以启用传出电子邮件，以及用于这些邮件的电子邮件服务器设置。（请参阅[配置电子邮件设置](configuring-server-settings.md#configuring-email-settings)。）
* **任务通** 知设置，用于启用、禁用或修改电子邮件通知中发送给最终用户和组的有关其任务的消息。（请参阅[配置用户和组的通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups)。）
* **管理员通** 知设置，用于启用、禁用或修改在管理任务的电子邮件通知中发送的消息。（请参阅[为管理员配置通知](configuring-server-settings.md#configuring-notifications-for-administrators)。）

## 配置电子邮件设置{#configuring-email-settings}

您可以为表单服务器指定一个电子邮件帐户，以通过该帐户向AEM表单用户和管理员发送电子邮件消息。 这些电子邮件用于通知和提醒用户必须完成的任务，通知用户已到期的任务，并通知管理员发生任何进程错误。

要在AEM表单和用户之间发送电子邮件，请在“电子邮件设置”页面上配置传出电子邮件设置。 外发电子邮件必须使用SMTP服务器。

要使AEM Forms能够接收和处理来自用户的传入电子邮件，请为完成任务服务创建电子邮件端点。 （请参阅[为完成任务服务创建电子邮件端点](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)）。

如果您的设计和实施流程无需发送电子邮件，则无需在“电子邮件设置”页面上配置任何选项。

### 配置传出电子邮件设置{#configure-outgoing-email-settings}

1. 在管理控制台中，单击服务>表单工作流>服务器设置>电子邮件设置。
1. 选择“启用传出消息”。
1. 在“SMTP服务器”框中，键入电子邮件服务器名称或IP地址。 来自表单工作流的所有通知电子邮件均从此电子邮件服务器发送。
1. 在“用户名”和“密码”框中，键入SMTP服务器需要身份验证时要使用的登录名和密码。 如果允许匿名登录，则将其留空。
1. 在“电子邮件地址”框中，键入要用作表单工作流发送的电子邮件的回访地址。

   >[!NOTE]
   >
   >如果您使用的是Microsoft Exchange Server，并且电子邮件地址是无效的电子邮件地址，则Microsoft Exchange Server无法向通讯组列表发送电子邮件。 要解决此问题，请为Microsoft Exchange服务器上的每个通讯组列表分别选择&#x200B;**启用外部通信**&#x200B;选项。

1. 单击保存。

>[!NOTE]
>
>如果输入了不正确的信息，可以单击“取消”返回到之前显示的页面。

### 配置电子邮件模板以使用AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

默认情况下，由AEM Forms发出的电子邮件包含指向(JEE上的AEM Forms已弃用)Flex Workspace的链接。 您可以配置AEM表单，以发出包含指向AEM Forms Workspace链接的电子邮件。 要详细了解AEM Forms Workspace的优势(已在JEE上弃用AEM表单)Flex Workspace，请参阅[此](/help/forms/using/features-html-workspace-available-flex.md)文章。

1. 在管理控制台中，单击主页>服务>表单工作流>服务器设置>任务通知。
1. 打开任务分配模板。
1. 在任务通知中将模板设置为：`https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 为{#configuring-notifications-for-users-and-groups}用户和组配置通知

在“任务通知”页面上，您可以配置表单工作流用于生成发送给用户和组的电子邮件通知的模板。 您可以使用表单工作流变量自定义通知并设置其格式。

您可以为用户和组配置以下类型的通知：

* 提醒
* 任务分配
* 截止时间

要为群组生成电子邮件通知，请在用户管理中为群组指定电子邮件地址。 <!--Fix broken link See Setting up and organizing users -->当表单工作流向群组发送电子邮件通知时，群组中具有指定电子邮件地址的每个成员都会收到电子邮件通知。当组成员收到电子邮件通知并想要声明任务时，该成员必须单击电子邮件通知中的声明链接，该链接将打开工作区中的任务详细信息页面。 从那里，成员可以要求或要求并打开工作项。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

### 为{#configure-reminders-for-users-or-groups}用户或组配置提醒

当完成任务的截止时间即将到来时，您可以向分配的用户或组发送提醒通知。 用于确定何时发送提醒通知的规则由流程开发人员确定。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>任务通知。
1. 在“通知类型”下，单击提醒（用于用户）或组 — 提醒（用于组）。
1. 选择启用提醒或启用组 — 提醒。
1. （仅限用户通知）要在提醒电子邮件中包含表单的附件及其数据，请选择包含表单数据。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在消息格式列表中，选择发送电子邮件的格式（HTML或文本）。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认为UTF-8，大多数日本以外的用户都将使用UTF-8。 日本的用户可以选择ISO2022-JP。
1. 单击保存。

### 为用户或组{#configure-task-assignment-notifications-for-users-or-groups}配置任务分配通知

在为用户或组分配任务时，您可以向其发送任务分配通知。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>任务通知。
1. 在“通知类型”下，单击“用户的任务分配”或“组 — 组的任务分配”。
1. 选择为用户启用任务分配或为组启用组 — 任务分配。
1. （仅限用户通知）要在任务分配电子邮件中包含表单的附件及其数据，请选择“包括表单数据”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在消息格式列表中，选择发送电子邮件的格式（HTML或文本）。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认为UTF-8，大多数日本以外的用户都将使用UTF-8。 日本的用户可以选择ISO2022-JP。
1. 单击保存。

### 为{#configure-deadline-notifications-for-users-or-groups}用户或组配置截止通知

在分配的任务完成后，您可以向用户和组发送截止日期通知。 截止日期通知通常是信息性的，因为用户无法再对分配的任务执行操作。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>任务通知。
1. 在“通知类型”下，单击“截止时间（对于用户）”或“组 — 截止时间（对于组）”。
1. 选择“启用截止时间”或“启用组 — 截止时间”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在消息格式列表中，选择发送电子邮件的格式（HTML或文本）。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认为UTF-8，大多数日本以外的用户都将使用UTF-8。 日本的用户可以选择ISO2022-JP。
1. 单击保存。

### 隐藏所有电子邮件的DO NOTDELETE标记{#hide-the-do-not-delete-tag-for-all-emails}

您可以将电子邮件配置为在以人为中心的流程中发送的所有电子邮件中隐藏到DO NOTDELETE跟踪标记。 有关详细信息，请参阅[如何使用CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)隐藏“DO-NOT-DELETE”标记

## 为管理员{#configuring-notifications-for-administrators}配置通知

您可以配置表单工作流用于生成发送给管理员的电子邮件通知的模板。

您可以为管理员配置以下类型的通知：

* 停止分支
* 停止操作

### 配置停止的分支通知{#configure-stalled-branch-notifications}

如果分支停止（故意或由于错误而停止继续），则可以向管理员或其他用户发送电子邮件通知，随后管理员或其他用户可以调查问题。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>管理员通知。
1. 在“通知类型”下，单击“停止的分支”。
1. 选择“启用停止的分支”。
1. 在“电子邮件地址”框中，键入分支停止时要通知的用户地址。 使用user@domain.com格式，并用逗号分隔每个地址。 通常，此电子邮件地址是供管理员使用的。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在消息格式列表中，选择发送电子邮件的格式（HTML或文本）。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认为UTF-8，大多数日本以外的用户都使用UTF-8。 日本的用户可以选择ISO2022-JP。
1. 单击保存。

### 配置停止的操作通知{#configure-stalled-operation-notifications}

如果某个操作停止（故意或由于错误而停止继续），您可以向管理员或其他用户发送电子邮件通知，以便他们能够调查问题。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>管理员通知。
1. 在“通知类型”下，单击“停止操作”。
1. 选择启用停止操作。
1. 在“电子邮件地址”框中，键入操作停止时要通知的用户地址。 使用user@domain.com格式，并用逗号分隔每个地址。 通常，此电子邮件地址是供管理员使用的。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参阅[自定义通知的内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 单击保存。

## 自定义通知的内容{#customizing-the-content-of-notifications}

“任务通知”和“管理员通知”页提供了多种功能，可让您自定义通知消息：

* 富文本编辑器
* 变量选取器
* URL生成

### 富文本编辑器{#rich-text-editor}

“通知模板”区域是一个富文本编辑器，可用于为电子邮件通知消息生成HTML。 它提供字体和段落格式选项，这些选项位于“通知模板”框下方。 选项包括字体类型、大小、样式和颜色，以及段落对齐方式和项目符号。

### URL生成{#url-generation}

仅对于任务通知，Forms工作流包含两个预定义的URL配置，您可以将这两个配置从“URL生成”列表拖到“通知模板”框中，然后进行自定义：

* OpenTask可用于提醒和任务分配通知类型。 此URL提供了指向工作区中任务的链接，允许用户从电子邮件通知中快速访问该任务。 将OpenTask URL拖至“通知模板”框时，该URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用于组 — 提醒和组 — 任务分配通知类型。 此URL提供指向工作区中任务详细信息页面的链接，用户可以在该页面中声明或声明并打开工作项。 将ClaimTask URL拖至“通知模板”框时，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

如果您的解决方案部署在群集环境中，请将`@@notification-host@@`替换为群集地址。

`<`** `>` PORT是应用程序服务器的HTTP侦听器的端口号。支持的应用程序服务器的默认HTTP侦听器端口如下所示：

**JBoss:** 8080

**OracleWebLogic服务器：** 7001

**IBM WebSphere:** 9080

要使这些URL正常运行，请将&#x200B;`<`*PORT* `>`替换为适合您环境的端口号。

>[!NOTE]
>
>如果您使用Forms以外的自定义Web应用程序为用户提供任务的访问权限，则必须改为使用适合您的自定义应用程序的URL格式。

### 变量选取器{#variable-picker}

变量选取器列表提供了一些有用的变量，您可以将这些变量拖放到主题或通知模板框中。 在“主题”或“通知模板”框中放置变量时，该变量会变为实际的表单工作流变量名称，其两侧有两个@符号，例如`@@taskid@@`。

对于用户和组的提醒、任务分配和截止时间，您可以在“主题”和“通知模板”框中使用以下变量：

**** 描述描述属性的内容，在Workbench中流程的用户步骤（起始点、分配任务操作或分配多个任务操作）中定义。

**** 说明在Workbench中流程的用户步骤中定义的“任务说明”属性的内容。

**notification-** host AEM forms应用程序服务器的主机名。

**process-** name进程的名称。

**operation-** name步骤的名称。

**** taskid当前任务的唯一标识符。

**** 操作生成收件人可单击的有效路由（例如批准、拒绝）的编号列表。

此外，对于组提醒、组任务分配和组截止时间，您还可以使用：

**group-** name为工作项分配的组的名称。

>[!NOTE]
>
>如果变量没有值，则不会返回任何内容。

对于已停止的分支，您可以在“主题”和“通知模板”框中使用以下变量：

**branch-id** 分支标识符。

**process-id进** 程实例标识符。

**notification-** host AEM forms应用程序服务器的主机名。

对于停止的操作，您可以在“主题”和“通知模板”框中使用以下变量：

**action-id操** 作标识符。

**branch-id** 分支标识符。

**process-id进** 程实例标识符。

**notification-** host AEM forms应用程序服务器的主机名。

### 在“主题”框{#using-a-variable-in-the-subject-box}中使用变量

如果在任务分配通知的“主题”框中键入以下文本：

`Please complete task @@taskid@@`

如果用户被分配了任务376，则用户收到具有以下主题的电子邮件消息：

`Please complete task 376`

### 在“通知模板”框{#using-variables-in-the-notification-template-box}中使用变量

如果在Stalled Branch Notifications的“通知模板”框中键入以下文本：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支编号为4868，服务器名称为`ServerXYZ`，则管理员会收到一封包含以下内容的电子邮件：

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 配置业务活动监控连接{#configuring-business-activity-monitoring-connections}

业务活动监控是一个可选模块，它提供了一组操作功能板，可实时查看您的操作和关键绩效指标。

在“BAM配置设置”页上，您可以设置与运行BAM的服务器的连接，以便跟踪与进程相关的事件并将其传输到该服务器。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置> BAM配置设置。
1. 在“BAM主机”框中，键入运行BAM的服务器的名称。 默认为localhost。
1. 在“BAM端口”框中，键入用于连接到运行BAM的服务器的端口。 JBoss的默认BAM端口为8080, WebLogic为7001, WebSphere为9080。
1. 在“服务器主机”框中，键入主机表单服务器的名称或IP地址。 默认值为localhost。
1. 在“服务器端口”框中，键入表单服务器使用的端口号。
1. 在“User Name（用户名）”和“Password（密码）”框中，键入相应的用户ID和密码以访问BAM服务器。 默认用户名为CognosNowAdmin ，默认密码为manager。
1. 单击保存。
