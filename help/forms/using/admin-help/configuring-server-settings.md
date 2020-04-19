---
title: 配置服务器设置
seo-title: 配置服务器设置
description: “服务器设置”页提供对电子邮件、任务通知和管理员通知设置的访问。
seo-description: “服务器设置”页提供对电子邮件、任务通知和管理员通知设置的访问。
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 配置服务器设置 {#configuring-server-settings}

通过“服务器设置”页，可以访问表单工作流的各种设置：

* **启用发送电子邮件** ，以及用于这些电子邮件的电子邮件服务器设置的电子邮件设置。 (See [Configuring email settings](configuring-server-settings.md#configuring-email-settings).)
* **任务通知设置** ，用于启用、禁用或修改通过电子邮件通知发送给最终用户和用户组的与其任务相关的消息。 (请参 [阅配置用户和用户组的通知](configuring-server-settings.md#configuring-notifications-for-users-and-groups)。)
* **管理员通知设置** ，用于启用、禁用或修改在管理任务的电子邮件通知中发送的消息。 (请参阅 [配置管理员通知](configuring-server-settings.md#configuring-notifications-for-administrators)。)

## 配置电子邮件设置 {#configuring-email-settings}

您可以为表单服务器指定电子邮件帐户，通过该帐户向AEM表单用户和管理员发送电子邮件。 这些电子邮件用于通知和提醒用户必须完成的任务，通知用户已到达截止日期的任务，并通知管理员出现任何进程错误。

要在AEM表单和用户之间启用电子邮件发送，请在“电子邮件设置”页面上配置传出电子邮件设置。 传出电子邮件必须使用SMTP服务器。

要使AEM表单能够接收和处理用户传入的电子邮件，请为完整任务服务创建电子邮件端点。 (请参 [阅为完整任务服务创建电子邮件端点](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service))。

如果您的流程是在设计和实施时不需要发送电子邮件，则不必在“电子邮件设置”页面上配置任何选项。

### 配置发送电子邮件设置 {#configure-outgoing-email-settings}

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“电子邮件设置”。
1. 选择“启用传出消息”。
1. 在“SMTP服务器”框中，键入电子邮件服务器名或IP地址。 来自表单工作流的所有通知电子邮件都从此电子邮件服务器发送。
1. 在“用户名”和“口令”框中，键入SMTP服务器需要身份验证时要使用的登录名和口令。 如果允许匿名登录，则将其留空。
1. 在“电子邮件地址”框中，键入要用作表单工作流发送的电子邮件的返回地址的电子邮件地址。

   >[!NOTE]
   >
   >如果您使用的是Microsoft Exchange Server，且电子邮件地址为无效的电子邮件地址，则Microsoft Exchange服务器无法向分发列表发送电子邮件。 要解决此问题，请为Microsoft Exchange服务器上 **的每个分发列表单独选择“启用外部通信** ”选项。

1. 单击保存。

>[!NOTE]
>
>如果输入的信息不正确，则可单击“取消”返回之前显示的页面。

### 配置电子邮件模板以使用AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM表单版本中已弃用Flex Workspace。

默认情况下，AEM表单发送的电子邮件包含指向（JEE上的AEM表单已弃用）Flex Workspace的链接。 您可以配置AEM表单以发送包含指向AEM Forms Workspace的链接的电子邮件。 要进一步了解AEM Forms Workspace的优势（JEE上的AEM表单已弃用），请参阅此 [文章](/help/forms/using/features-html-workspace-available-flex.md) 。

1. 在管理控制台中，单击“主页”>“服务”>“表单工作流”>“服务器设置”>“任务通知”。
1. 打开任务分配模板。
1. 在任务通知中将模板设置为： `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```as3
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## 为用户和用户组配置通知 {#configuring-notifications-for-users-and-groups}

在“任务通知”页面上，您可以配置表单工作流将用来生成发送给用户和组的电子邮件通知的模板。 您可以使用表单工作流变量自定义通知并设置通知的格式。

为用户和用户组配置以下类型的通知：

* 提醒
* 任务分配
* 截止日期

要为组生成电子邮件通知，请在“用户管理”中指定组的电子邮件地址。 <!--Fix broken link See Setting up and organizing users -->当表单工作流向组发送电子邮件通知时，组中具有指定电子邮件地址的每个成员都会收到电子邮件通知。 当组成员收到电子邮件通知并要申请任务时，该成员必须单击电子邮件通知中的索赔链接，该链接将在Workspace中打开任务详细信息页面。 从那里，会员可以主张或主张并打开工作项。

>[!NOTE]
>
>AEM表单发行版中已弃用Flex工作空间。

### 为用户或用户组配置提醒 {#configure-reminders-for-users-or-groups}

在完成任务的截止期限即将到来时，您可以向已分配的用户或用户组发送提醒通知。 用于确定提醒通知的确切发送时间的规则由流程开发者确定。

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“任务通知”。
1. 在“通知类型”下，单击“提醒”（对于用户）或“组——提醒”（对于组）。
1. 选择“启用提醒”或“启用组——提醒”。
1. （仅限用户通知）要在提醒电子邮件中包含表单及其数据的附件，请选择“包括表单数据”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“消息格式”列表中，选择电子邮件的发送格式（HTML或文本）。 默认格式为HTML。
1. 在“电子邮件编码”列表中，选择用于电子邮件的编码格式。 默认值为UTF-8，大多数日本以外的用户都将使用它。 日本用户可以选择ISO2022-JP。
1. 单击保存。

### 为用户或用户组配置任务分配通知 {#configure-task-assignment-notifications-for-users-or-groups}

当用户或用户组分配了任务时，您可以向其发送任务分配通知。

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“任务通知”。
1. 在“通知类型”下，单击“用户任务分配”或“用户组任务分配”。
1. 选择“为用户启用任务分配”或“为用户启用组——为用户组启用任务分配”。
1. （仅限用户通知）要在任务分配电子邮件中包含表单的附件及其数据，请选择“包括表单数据”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“消息格式”列表中，选择电子邮件的发送格式（HTML或文本）。 默认格式为HTML。
1. 在“电子邮件编码”列表中，选择用于电子邮件的编码格式。 默认值为UTF-8，大多数日本以外的用户都将使用它。 日本用户可以选择ISO2022-JP。
1. 单击保存。

### 为用户或用户组配置截止通知 {#configure-deadline-notifications-for-users-or-groups}

您可以在分配的任务的截止期限过后向用户和用户组发送截止通知。 截止期限通知通常是信息性的，因为用户无法再对分配的任务执行操作。

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“任务通知”。
1. 在“通知类型”下，单击“截止日期”（对于用户）或“组——截止日期”（对于组）。
1. 选择“启用截止日期”或“启用组——截止日期”。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“消息格式”列表中，选择电子邮件的发送格式（HTML或文本）。 默认格式为HTML。
1. 在“电子邮件编码”列表中，选择用于电子邮件的编码格式。 默认值为UTF-8，大多数日本以外的用户都将使用它。 日本用户可以选择ISO2022-JP。
1. 单击保存。

### 隐藏所有电子邮件的“请勿删除”标记 {#hide-the-do-not-delete-tag-for-all-emails}

您可以将电子邮件配置为隐藏到以人为中心的流程发送的所有电子邮件中的“请勿删除”跟踪标签。 有关详细信 [息，请参阅如何用CSS隐藏“DO-NOT-DELETE”标签](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## 为管理员配置通知 {#configuring-notifications-for-administrators}

您可以配置表单工作流将用来生成发送给管理员的电子邮件通知的模板。

可为管理员配置以下类型的通知：

* 停止分支
* 停止运行

### 配置已停止的分支通知 {#configure-stalled-branch-notifications}

如果分支停止运行（故意停止运行或由于错误而停止运行），您可以向管理员或其他用户发送电子邮件通知，然后由他们调查问题。

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“管理员通知”。
1. 在“通知类型”下，单击“停止的分支”。
1. 选择“启用已停止的分支”。
1. 在“电子邮件地址”框中，键入分支停止时要通知的用户的地址。 使用user@domain.com格式，并用逗号分隔每个地址。 通常，此电子邮件地址适用于管理员。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 在“消息格式”列表中，选择电子邮件的发送格式（HTML或文本）。 默认格式为HTML。
1. 在“电子邮件编码”列表中，选择用于电子邮件的编码格式。 默认为UTF-8，大多数日本以外的用户都使用它。 日本用户可以选择ISO2022-JP。
1. 单击保存。

### 配置停止的操作通知 {#configure-stalled-operation-notifications}

如果某个操作停止（故意停止或由于错误而停止），您可以向管理员或其他可以调查问题的用户发送电子邮件通知。

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“管理员通知”。
1. 在“通知类型”下，单击“停止的操作”。
1. 选择“启用已停止的操作”。
1. 在“电子邮件地址”框中，键入操作停止时要通知的用户的地址。 使用user@domain.com格式，并用逗号分隔每个地址。 通常，此电子邮件地址适用于管理员。
1. 在“主题”框中，键入电子邮件主题行的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请参 [阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)
1. 在“通知模板”框中，键入电子邮件正文的文本。 此字段预填充了默认文本。 有关自定义此字段的详细信息，请 [参阅自定义通知内容](configuring-server-settings.md#customizing-the-content-of-notifications)。
1. 单击保存。

## 自定义通知内容 {#customizing-the-content-of-notifications}

“任务通知”和“管理员通知”页提供了多种功能，使您能够自定义通知消息：

* 富文本编辑器
* 变量选取器
* URL生成

### Rich text editor {#rich-text-editor}

“通知模板”区域是富文本编辑器，它允许您为电子邮件通知消息生成HTML。 它提供了字体和段落格式选项，这些选项位于“通知模板”框下方。 选项包括字体类型、大小、样式和颜色，以及段落对齐方式和项目符号。

### URL生成 {#url-generation}

仅对于任务通知，表单工作流包含两个预定义的URL配置，您可以将它们从Url生成列表拖入通知模板框中，然后进行自定义：

* OpenTask可用于提醒和任务分配通知类型。 此URL在Workspace中提供指向任务的链接，使用户能够从电子邮件通知中快速访问任务。 将OpenTask URL拖动到“通知模板”框时，URL采用以下格式：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask可用于“组——提醒和组-任务分配”通知类型。 此URL提供指向Workspace中的任务详细信息页面的链接，用户可在该页面中声明或声明并打开工作项。 将ClaimTask URL拖动到“通知模板”框时，URL的格式如下：

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM表单发行版中已弃用Flex工作空间。

如果您的解决方案部署在群集环境中，请用群 `@@notification-host@@` 集地址替换。

`<`*PORT *`>`是应用程序服务器的HTTP监听器的端口号。 支持的应用程序服务器的默认HTTP监听器端口如下：

**JBoss:** 八〇八〇年

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 九零八零年

要使这些URL正常工作，请 `<`*将PORT *`>`替换为适合您的环境的端口号。

>[!NOTE]
>
>如果您使用Forms以外的自定义Web应用程序向用户提供对任务的访问权，则必须改用适合您的自定义应用程序的URL格式。

### 变量选取器 {#variable-picker}

变量选取器列表提供了一些有用的变量，您可以将这些变量拖放到“主题”或“通知模板”框中。 当您将变量放在“主题”或“通知模板”框中时，它会更改为实际的表单工作流变量名称，其两侧有两个@符号，例如 `@@taskid@@`。

对于用户和用户组的提醒、任务分配和截止日期，您可以在“主题”和“通知模板”框中使用以下变量：

**description** “描述”属性的内容，如Workbench中流程的用户步骤(开始点、分配任务操作或分配多个任务操作)中所定义。

**说明** “任务说明”属性的内容，如Workbench中流程的用户步骤中所定义。

**notification-host** AEM forms应用程序服务器的主机名。

**process-name** 进程的名称。

**operation-name** 步骤的名称。

**taskid** 当前任务的唯一标识符。

**actions** 生成有效路由的编号列表（例如，批准、拒绝）,收件人可以单击这些路由。

此外，对于组提醒、组任务分配和组截止日期，您还可以使用：

**group-name** 为工作项分配的组的名称。

>[!NOTE]
>
>如果变量没有值，则不返回任何内容。

对于已停止的分支，您可以在“主题”和“通知模板”框中使用以下变量：

**branch-id** 分支标识符。

**process-id** 进程实例标识符。

**notification-host** AEM forms应用程序服务器的主机名。

对于已停止的操作，您可以在“主题”和“通知模板”框中使用以下变量：

**action-id操作标识符** 。

**branch-id** 分支标识符。

**process-id** 进程实例标识符。

**notification-host** AEM forms应用程序服务器的主机名。

### 在“主题”框中使用变量 {#using-a-variable-in-the-subject-box}

如果在“主题”框中键入以下文本以发送任务分配通知：

`Please complete task @@taskid@@`

如果用户被分配了第376号任务，则用户会收到一封包含下列主题的电子邮件：

`Please complete task 376`

### 在“通知模板”框中使用变量 {#using-variables-in-the-notification-template-box}

如果在“已停止的分支通知”的“通知模板”框中键入以下文本：

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

如果分支编号为4868，并且服务器名称为，则管理员会收到一封电子邮件，其中包含以下内容 `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## 配置业务活动监控连接 {#configuring-business-activity-monitoring-connections}

业务活动监控是一个可选模块，它提供一组操作仪表板，可实时查看您的操作和关键绩效指标。

在“BAM配置设置”页面上，您可以设置与运行BAM的服务器的连接，以便跟踪进程相关事件并将其传输到该服务器。

1. 在管理控制台中，单击“服务”>“表单工作流”>“服务器设置”>“BAM配置设置”。
1. 在“BAM主机”框中，键入运行BAM的服务器的名称。 默认为localhost。
1. 在“BAM端口”框中，键入用于连接到运行BAM的服务器的端口。 JBoss的默认BAM端口为8080,WebLogic为7001,WebSphere为9080。
1. 在“服务器主机”框中，键入主机表单服务器的名称或IP地址。 默认值是localhost。
1. 在“服务器端口”框中，键入表单服务器使用的端口号。
1. 在“用户名”和“密码”框中，键入相应的用户ID和密码以访问BAM服务器。 默认用户名为CognosNowAdmin，默认密码为manager。
1. 单击保存。

