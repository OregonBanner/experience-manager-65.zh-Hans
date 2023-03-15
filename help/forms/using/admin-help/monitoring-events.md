---
title: 监控事件
seo-title: Monitoring events
description: 启用审核功能后，您可以通过Document Security监控特定类型的事件。 您可以使用Document Security轻松搜索和排序事件列表。
seo-description: When the auditing capability is enabled, document security enables you to monitor certain types of events. You can easily search and sort the events list using the document security.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 监控事件 {#monitoring-events}

启用审核功能后，您可以通过Document Security监控特定类型的事件。 您可以看到的事件取决于您的角色：

**用户：** 可以查看其受策略保护的文档以及他们收到并使用的任何受保护文档的已审核事件。

**策略集协调器：** 可以查看受策略保护且不受策略集保护的文档的审核事件（包括文档和策略事件）。

**管理员：** 可以查看与所有受策略保护的文档和用户相关的已审核事件。 管理员还可以跟踪其他类型的事件，包括用户、文档、策略和系统事件。

>[!NOTE]
>
>对受策略保护文档的副本执行的事件，也会作为原始受保护文档上的事件进行跟踪。

(请参阅 [事件审计选项](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

如果未经授权的用户尝试查看文档或尝试使用错误的用户名或密码登录，则会记录失败事件。

>[!NOTE]
>
>如果编辑策略以删除匿名访问，则可以记录文档的匿名访问失败事件。 当授权收件人尝试访问已编辑策略保护的文档时，仍尝试匿名访问，但将失败。

如果策略允许匿名用户访问，但管理员稍后为Document Security关闭匿名访问，则对受策略保护的文档的匿名访问将失败，并且不会记录该事件。

## 启用事件审核 {#enable-event-auditing}

要执行事件审核，必须满足以下设置要求：

* 系统或管理员必须启用服务器的审核权能。

   (请参阅 [配置事件审核和隐私设置](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* 用于保护文档的策略必须启用审核。 (请参阅 [创建和编辑策略](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## 搜索事件 {#search-for-an-event}

您可以搜索事件列表并查看有关事件的更详细说明。 详细说明包括事件ID、描述、IP地址、组织、用户受影响、事件发生日期和时间、被拒绝的活动和离线事件（当用户尝试使用文档时未连接到document security）等信息。

您可以结合使用事件搜索条件和事件发生日期，在“事件”页面上搜索事件。 您可以搜索的事件取决于您的角色：

**用户：** 可以查看其受策略保护的文档以及他们收到并使用的任何受保护文档的已审核事件。 这些搜索选项可用：

**与我相关的事件：** 用户可以为其创建或收到的任何受策略保护文档查找事件。 例如，如果用户打开、查看或打印了其他人保护的文档，则用户只会看到该文档的这些事件。

**与我的文档相关的事件：** 用户可以找到与其自己的受策略保护文档相关的所有事件。 用户会看到每个处理其文档的用户生成的事件。

**策略集协调器：** 可以查看受策略保护且不受策略集保护的文档的审核事件（包括文档和策略事件）。 提供了以下选项：

**记录我是策略集协调者的事件：** 具有查看事件权限的策略集协调员可以查找与其策略集中的策略所保护的文档相关的事件。

**我担任策略集协调器的策略事件：** 具有查看事件权限的策略集协调员可以从其策略集中查找与策略相关的事件。

**管理员：** 可以查看与所有受策略保护的文档和用户相关的已审核事件。 管理员还可以跟踪其他类型。 此外，管理员还可以根据用户类型进一步细分事件搜索：

**已知用户：** 用户位于源目录中或注册为外部用户。

**匿名用户：** 访问受允许匿名访问的策略保护的文档的未知用户。

**系统用户：** 服务器启动的事件，如目录同步。

1. 在document security页面上，单击Events。
1. 在“查找”列表中，选择要使用的搜索条件。 根据您在“查找”列表中的选择，将显示第二个提供附加搜索条件的列表。 如果适用，请在文本框中键入搜索条件。

   有关特定事件类型的更多详细信息，请参阅 [事件审计选项](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. 在用户列表中，选择执行事件的用户类型：

   * 如果选择“已知用户”，则会显示第二个搜索框，您必须在该框中键入用户的用户名或电子邮件地址。
   * 如果您不知道这些值，请单击通讯簿搜索图标，以按用户名或电子邮件地址搜索用户。

1. 在日期列表中，选择一个日期范围选项。 如果选择“自定义日期”，则会显示框，您可以在其中以yyyy/mm/dd格式键入日期，或者可以使用日期选取器指定日期范围：

   * 单击日历以打开日期选择器。
   * 使用箭头查找年和月。
   * 在日历上单击月中某日。
   * 单击“确定”以关闭日期选取器。

1. 在“显示”列表中，选择每页显示的搜索结果数。
1. 单击“查找”。

   任何失败事件都会在列表中突出显示，并带有拒绝图标。

1. 要查看有关事件的详细信息，请单击列表中该事件的说明。

## 对事件列表进行排序 {#sort-the-event-list}

您可以按列标题对事件列表进行排序，以便更轻松地查找事件。 列标题旁边的三角形图标指示当前使用哪一列进行排序。 上指三角形表示升序，下指三角形表示降序。

1. 单击相应的列标题。
1. 要更改排序顺序，请再次单击列标题。
