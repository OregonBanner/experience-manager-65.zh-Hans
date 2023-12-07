---
title: 配置服务器设置
description: “服务器设置”页提供对电子邮件、任务通知和管理员通知设置的访问权限。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2631'
ht-degree: 0%

---

# 配置服务器设置 {#configuring-server-settings}

“服务器设置”页面提供对表单工作流的各种设置的访问权限：

* **电子邮件设置** 启用外发电子邮件以及这些邮件使用的电子邮件服务器设置。 (请参阅 [配置电子邮件设置](configuring-server-settings.md#configuring-email-settings).)
* **任务通知设置** 启用、禁用或修改在电子邮件通知中发送给最终用户和组的有关其任务的消息。 (请参阅 [为用户和组配置通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **管理员通知设置** 启用、禁用或修改在管理任务的电子邮件通知中发送的消息。 (请参阅 [为管理员配置通知](configuring-server-settings.md#configuring-notifications-for-administrators).)

## 配置电子邮件设置 {#configuring-email-settings}

您可以为Forms服务器指定一个电子邮件帐户，通过该帐户向AEM Forms用户和管理员发送电子邮件。 这些电子邮件用于通知和提醒用户必须完成的任务，通知用户已到达截止日期的任务，并在发生任何进程错误时通知管理员。

要在AEM表单和用户之间启用电子邮件发送，请在“电子邮件设置”页面上配置传出电子邮件设置。 传出电子邮件必须使用SMTP服务器。

要启用AEM表单以接收和处理来自用户的传入电子邮件，请为Complete Task服务创建电子邮件端点。 (请参阅 [为完成任务服务创建电子邮件端点](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service))。

如果您的流程是在不需要电子邮件的情况下设计和实施的，则您无需在“电子邮件设置”页面上配置任何选项。

### 配置传出电子邮件设置 {#configure-outgoing-email-settings}

1. 在管理控制台中，单击服务>表单工作流>服务器设置>电子邮件设置。
1. 选择启用传出消息。
1. 在“SMTP服务器”框中，键入电子邮件服务器名称或IP地址。 来自表单工作流的所有通知电子邮件消息都从此电子邮件服务器发送。
1. 在“用户名”和“密码”框中，键入当SMTP服务器要求验证时使用的登录名和密码。 如果允许匿名登录，则将其留空。
1. 在“电子邮件地址”框中，键入要用作表单工作流所发送电子邮件的返回地址的电子邮件地址。

   >[!NOTE]
   >
   >如果您使用的是Microsoft Exchange Server ，且电子邮件地址为无效的电子邮件地址，则Microsoft Exchange Server无法向通讯组列表发送电子邮件。 要解决此问题，请选择 **启用外部通信** 为Microsoft Exchange Server上的每个通讯组列表分别设置选项。

1. 单击“保存”。

>[!NOTE]
>
>如果输入的信息不正确，可以单击“取消”返回之前显示的页面。

### 配置电子邮件模板以使用AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

默认情况下，由AEM表单发送的电子邮件包含指向(JEE上的AEM表单已弃用) Flex Workspace的链接。 您可以将AEM表单配置为发送包含指向AEM Forms Workspace的链接的电子邮件。 要详细了解AEM Forms工作区与(JEE上的AEM表单已弃用)Flex工作区相比所具有的优势，请参阅 [此](/help/forms/using/features-html-workspace-available-flex.md) 文章。

1. 在管理控制台中，单击主页>服务>表单工作流>服务器设置>任务通知。
1. 打开任务分配模板。
1. 将任务通知中的模板设置为以下内容： `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 为用户和组配置通知 {#configuring-notifications-for-users-and-groups}

在“任务通知”页面上，您可以配置模板，表单工作流将使用该模板生成发送给用户和组的电子邮件通知。 您可以使用表单工作流变量自定义通知和设置通知格式。

您可以为用户和组配置以下类型的通知：

* 提醒
* 任务分配
* 截止日期

要为组生成电子邮件通知，请在用户管理中指定组的电子邮件地址。 <!--Fix broken link See Setting up and organizing users -->当表单工作流向组发送电子邮件通知时，组中每个具有指定电子邮件地址的成员都会收到电子邮件通知。 当组的成员收到电子邮件通知并想要声明任务时，该成员必须单击电子邮件通知中的声明链接，这会在Workspace中打开任务详细信息页面。 从那里，成员可以声明或声明并打开工作项。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

### 为用户或组配置提醒 {#configure-reminders-for-users-or-groups}

临近完成任务的截止日期时，您可以向分配的用户或组发送提醒通知。 用于确切地确定何时发送提醒通知的规则由过程开发人员确定。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>任务通知。
1. 在“通知类型”下，单击“提醒”（适用于用户）或“组 — 提醒”（适用于组）。
1. 选择“启用提醒”或“启用组 — 提醒”。
1. （仅限用户通知）要在提醒电子邮件中包含表单的附件及其数据，请选择“包括表单数据”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在通知模板框中，键入电子邮件正文的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在“邮件格式”列表中，选择发送电子邮件的格式，即HTML或文本。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认值为UTF-8，日本以外的大多数用户都将使用该格式。 日本用户可以选择ISO2022-JP。
1. 单击“保存”。

### 为用户或组配置任务分配通知 {#configure-task-assignment-notifications-for-users-or-groups}

您可以在用户或组被分配任务时向他们发送任务分配通知。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>任务通知。
1. 在“通知类型”下，单击用户的任务分配，或单击组的任务分配。
1. 选择“为用户启用任务分配”或“为组启用组 — 任务分配”。
1. （仅限用户通知）要在任务分配电子邮件中包含表单的附件及其数据，请选择“包括表单数据”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在通知模板框中，键入电子邮件正文的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在“邮件格式”列表中，选择发送电子邮件的格式，即HTML或文本。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认值为UTF-8，日本以外的大多数用户都将使用该格式。 日本用户可以选择ISO2022-JP。
1. 单击“保存”。

### 为用户或组配置截止日期通知 {#configure-deadline-notifications-for-users-or-groups}

当对已分配任务采取行动的截止日期已过时，您可以向用户和组发送截止日期通知。 截止日期通知通常是信息性的，因为用户无法再根据分配的任务执行操作。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>任务通知。
1. 在通知类型下，单击截止日期（对于用户）或组 — 截止日期（对于组）。
1. 选择启用截止日期或启用组 — 截止日期。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在通知模板框中，键入电子邮件正文的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在“邮件格式”列表中，选择发送电子邮件的格式，即HTML或文本。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认值为UTF-8，日本以外的大多数用户都将使用该格式。 日本用户可以选择ISO2022-JP。
1. 单击“保存”。

### 隐藏所有电子邮件的“不DELETE”标记 {#hide-the-do-not-delete-tag-for-all-emails}

您可以将电子邮件配置为在以人为中心的流程发送的所有电子邮件中隐藏“不DELETE”跟踪标记。

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 为管理员配置通知 {#configuring-notifications-for-administrators}

您可以配置表单工作流将用于生成发送给管理员的电子邮件通知的模板。

您可以为管理员配置以下类型的通知：

* 停止的分支
* 停止的操作

### 配置停止的分支通知 {#configure-stalled-branch-notifications}

如果分支停止（由于故意或错误而停止继续操作），您可以向管理员或其他用户发送电子邮件通知，管理员或其他用户随后可以调查该问题。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>管理员通知。
1. 在“通知类型”下，单击“停止的分支”。
1. 选择启用停止的分支。
1. 在“电子邮件地址”框中，键入分支停止时要通知的用户地址。 使用格式user@domain.com ，并用逗号分隔每个地址。 通常情况下，此电子邮件地址适用于管理员。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在通知模板框中，键入电子邮件正文的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 在“邮件格式”列表中，选择发送电子邮件的格式，即HTML或文本。 默认格式为HTML。
1. 在电子邮件编码列表中，选择要用于电子邮件的编码格式。 默认值为UTF-8，日本以外的多数用户都使用该格式。 日本用户可以选择ISO2022-JP。
1. 单击“保存”。

### 配置停止的操作通知 {#configure-stalled-operation-notifications}

如果某个操作停止（有意或由于错误而停止执行），您可以向管理员或其他用户发送电子邮件通知，以便他们调查问题。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置>管理员通知。
1. 在通知类型下，单击停止的操作。
1. 选择启用停止的操作。
1. 在“电子邮件地址”框中，键入要在操作停止时通知的用户地址。 使用格式user@domain.com ，并用逗号分隔每个地址。 通常情况下，此电子邮件地址适用于管理员。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在通知模板框中，键入电子邮件正文的文本。 此字段已预填充默认文本。 有关自定义此字段的详细信息，请参阅 [自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications).
1. 单击“保存”。

## 自定义通知内容 {#customizing-the-content-of-notifications}

“任务通知”和“管理员通知”页提供了若干功能，使您可以自定义通知消息：

* 富文本编辑器
* 变量选取器
* URL生成

### 富文本编辑器 {#rich-text-editor}

Notification Template区域是一个富文本编辑器，可用于生成电子邮件通知消息的HTML。 它提供字体和段落格式选项，这些选项位于通知模板框的下方。 这些选项包括字体类型、大小、样式和颜色，以及段落对齐方式和项目符号。

### URL生成 {#url-generation}

仅对于任务通知，Forms工作流包含两个预定义的URL配置，您可以将这两个配置从“URL生成”列表拖到“通知模板”框中，然后对其进行自定义：

* OpenTask可用于“提醒”和“任务分配”通知类型。 此URL提供指向工作区中任务的链接，允许用户从电子邮件通知中快速访问任务。 将OpenTask URL拖到“通知模板”框时，该URL的格式如下：

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用于“组 — 提醒”和“组 — 任务分配”通知类型。 此URL提供了一个指向工作区中任务详细信息页面的链接，用户可以在其中声明或声明并打开工作项。 将ClaimTask URL拖到“通知模板”框时，该URL的格式如下：

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

如果您的解决方案部署在群集环境中，请替换 `@@notification-host@@` 使用群集地址。

`<`*端口* `>` 是应用程序服务器的HTTP侦听器的端口号。 支持的应用程序服务器的默认HTTP侦听器端口如下所示：

**JBoss：** 8080

**oracleWebLogic Server：** 7001

**IBM WebSphere：** 9080

要使这些URL正常运行，请将 `<`*端口* `>` ，端口号适合您的环境。

>[!NOTE]
>
>如果您使用Forms以外的自定义Web应用程序为用户提供任务访问权限，则必须使用适用于您的自定义应用程序的URL格式。

### 变量选取器 {#variable-picker}

变量选取器列表提供了一些有用的变量，您可以将这些变量拖放到“主题”或“通知模板”框中。 将变量拖放到“主题”或“通知模板”框中时，它会更改为实际表单工作流变量名称，其两侧各有两个@符号，例如， `@@taskid@@`.

对于提醒、任务分配以及用户和组的截止日期，您可以在“主题”和“通知模板”框中使用以下变量：

**描述** 说明属性的内容，如在Workbench中流程的用户步骤（起点、分配任务操作或分配多个任务操作）中所定义。

**说明** 任务指令属性的内容，如Workbench中流程的用户步骤中所定义。

**通知主机** AEM Forms应用程序服务器的主机名。

**process-name** 进程的名称。

**operation-name** 步骤的名称。

**任务** 当前任务的唯一标识符。

**操作** 生成收件人可以单击的有效路由的编号列表（例如，批准、拒绝）。

此外，对于组提醒、组任务分配和组截止日期，您还可以使用：

**group-name** 分配了工作项的组的名称。

>[!NOTE]
>
>如果变量没有值，则不会返回任何内容。

对于停止的分支，您可以在“主题”和“通知模板”框中使用以下变量：

**branch-id** 分支标识符。

**process-id** 进程实例标识符。

**通知主机** AEM Forms应用程序服务器的主机名。

对于停止的操作，您可以在“主题”和“通知模板”框中使用以下变量：

**action-id** 操作标识符。

**branch-id** 分支标识符。

**process-id** 进程实例标识符。

**通知主机** AEM Forms应用程序服务器的主机名。

### 在主题框中使用变量 {#using-a-variable-in-the-subject-box}

如果在“任务分配”通知的“主题”框中键入以下文本：

`Please complete task @@taskid@@`

如果用户被分配任务376，则用户接收带有以下主题的电子邮件：

`Please complete task 376`

### 在通知模板框中使用变量 {#using-variables-in-the-notification-template-box}

如果您在“通知模板”框中为Stalled Branch通知键入以下文本：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支编号为4868且服务器名称为，则管理员会收到一封包含以下内容的电子邮件 `ServerXYZ`：

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 配置业务活动监控连接 {#configuring-business-activity-monitoring-connections}

业务活动监控是一个可选模块，它提供了一组操作仪表板，可实时查看您的操作和关键绩效指标。

在“BAM配置设置”页中，可以设置与运行BAM的服务器的连接，以便可以跟踪与进程相关的事件并将其传输到该服务器。

1. 在管理控制台中，单击服务> Forms工作流>服务器设置> BAM配置设置。
1. 在“BAM主机”框中，键入运行BAM的服务器的名称。 缺省值为localhost。
1. 在“BAM端口”框中，键入用于连接到运行BAM的服务器的端口。 JBoss的默认BAM端口为8080，WebLogic为7001，WebSphere为9080。
1. 在服务器主机框中，键入主机Forms服务器的名称或IP地址。 默认值为localhost。
1. 在“服务器端口”框中，键入Forms服务器使用的端口号。
1. 在“User Name（用户名）”和“Password（密码）”框中，键入相应的用户ID和密码以访问BAM服务器。 默认的用户名为CognosNowAdmin ，默认密码为manager。
1. 单击“保存”。
