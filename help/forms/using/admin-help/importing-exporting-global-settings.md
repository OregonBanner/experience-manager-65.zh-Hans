---
title: 导入和导出全局设置
seo-title: 导入和导出全局设置
description: 您可以导入和导出工作区的搜索模板定义和全局设置。
seo-description: 您可以导入和导出工作区的搜索模板定义和全局设置。
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 导入和导出全局设置{#importing-and-exporting-global-settings}

您可以导入和导出工作区的搜索模板定义和全局设置。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

例如，您可以通过从一个环境导出搜索模板定义和全局设置，并将它们导入另一个环境，从开发环境移动到生产环境。

导出全局设置文件后，可以在XML或文本编辑器中修改设置。 但是，您可能想要编辑的唯一设置是JChannelConnectionProperties、formViewOnly和specialRoutes设置。 有关更多信息，请参阅[工作区全局设置](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果在全局设置文件中更改事件属性，则必须重新启动服务器。

## 导入搜索模板定义{#import-a-search-template-definition}

1. 在管理控制台中，单击服务>工作区>全局管理。
1. 在“导入搜索模板定义”框下，单击“选择文件”，然后选择搜索模板。 您只能导入最初从工作区实例导出的搜索模板定义。
1. 单击导入。

## 导出搜索模板定义{#export-a-search-template-definition}

1. 在“全局管理”(Global Administration)页面的“导出搜索模板定义”(Export search template definition)下，单击“全部列表”(List All)。
1. 在搜索模板列表中，选择要导出的模板。

   >[!NOTE]
   >
   >您可以选择多个模板，但只会导出最后选定的模板。

1. 单击导出，然后在计算机上保存文件。

## 导入全局设置{#import-global-settings}

1. 在“全局管理”页面的“导入全局设置”下，单击选择文件，然后选择全局设置文件。 全局设置文件必须采用XML格式。
1. 单击导入。

## 导出全局设置{#export-global-settings}

1. 在“全局管理”页面的“导出全局设置”下，单击导出。
1. 将文件保存在您的计算机上。

## 工作区全局设置{#workspace-global-settings}

您可以修改全局设置文件；但是，您可能想要编辑的唯一设置是JChannelConnectionProperties、formViewOnly和specialRoutes设置。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

工作区全局设置文件包含以下设置：

### specialRoutes设置{#specialroutes-settings}

*specialRoutes*&#x200B;设置在工作区中指定特殊路由（批准和拒绝）的属性。 在某些情况下，这些路由的按钮会显示在工作区的任务卡上，用户无需打开表单即可选择它们。 您可以修改全局设置文件中的specialRoutes设置，以添加用于批准和拒绝的自定义名称，或创建其他路由。

**client_specialRoutes_approve_style:** 位于工作区主题中的样式名称，用于标识批准按钮图标。样式必须包含已启用图标和已禁用图标的值。 要为自定义按钮定义样式，必须使用以下模板：
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }`工作区CSS文件嵌入在workspace-theme.swf文件中，该文件位于adobe-workspace-client.ear > adobe-workspace-client.war文件中。 要更改工作区的外观，必须重新编译workspace-theme.swf文件。

**client_specialRoutes_routes_deny_names:** Workbench用户可用来解释为“deny”的字符串的各种类型。字符串区分大小写。 例如，默认值为deny。 如果Workbench用户在流程中使用“拒绝”一词，则无法识别该词。 必须在此设置中添加“拒绝”一词，才能自定义路由按钮并对其应用样式。

**client_specialRoutes_routes_deny_style:** 位于工作区主题文件中的样式名称，用于标识拒绝按钮图标。样式必须包含已启用图标和已禁用图标的值。 要为自定义按钮定义样式，必须使用以下模板：
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_approve_names:** Workbench用户可用来解释为“approve”的字符串的各种类型。 字符串区分大小写。 例如，默认值为approve。 如果Workbench用户在流程中使用“批准”一词，则该词将不被识别。 必须在此设置中添加Approve一词，才能自定义路由按钮并对其应用样式。

**client_specialRoutes_names:** 用于从资源文件中查找自定义字符串值的键。此设置中的每个条目都需要包含名称和样式的值。

### JGroup设置{#jgroup-settings}

仅当您从AdobeLiveCycleES 2.5或更早版本升级了时，才会显示这些设置。

**server_remoteevents_ClientTimeoutMillicess:** JGroup等待事件消息的最长时间。不应更改此设置。

**server_remoteevents_ServerTimeoutMillicess:** 在服务器上接收JGroup消息的超时。此选项设置将消息从服务器发送到客户端的延迟。

**server_remoteevents_JChannelConnectionProperties:** JGroup的连接属性，用于在服务器（RemoteEvent服务在其上处理服务事件）和工作区的所有实例之间进行通信。

您可能需要更改多播IP地址(mcast_addr)、多播IP端口(mcast_port)的UDP值，以及多播数据包(ip_ttl)的TTL。 默认情况下，组播IP地址和端口值是随机生成的，通常不需要更改这些值。 但是，如果贵公司有任何有关多播IP地址的特定多播范围的网络策略，则可能需要更改这些值。

>[!NOTE]
>
>TTL必须大于群集中服务器之间的网络交换机数；但是，如果值设置过高，则可能会导致多播数据包进入子网，并丢弃这些数据包。

不应更改此设置中的其余属性。

**server_remoteevents_JGroupName:** 用于远程事件通信的JGroup的名称。此值是随机生成的，以避免群集中的冲突。 不应更改此值。

有关JGroup和工作区的其他信息，请参阅[JGroup和AEM Forms Workspace — 说明](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html)。

### formView设置{#formview-settings}

**client_formView_openFormInFullScreen:** 要在工作区中以全屏模式显示所有表单，请将此选项设置为true。默认情况下，此选项设置为false，并且表单不以全屏模式显示。 请注意，用户服务包含一个选项，用于以全屏模式打开与任务关联的文档。 这样，您就可以按流程控制显示。

**client_routes_formViewOnly:** 当设置为True时，在工作区的卡片视图或列表视图中不会显示路由。默认值为False，表示路由在卡片视图和列表视图中显示。

### 其他设置{#other-settings}

**client_mimeTypes_openOutsideBrowser:** 将在工作区浏览器实例外部打开的文档的MIME类型。如果贵组织的进程需要其他MIME类型，请在此处指定。 默认值为：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** 缓存自定义任务用户界面。

**server_debugLevel:** 请勿更改此设置。

**client_pollingInterval:** 设置在(JEE上的AEM表单已弃用)Flex工作区上使用的轮询间隔（以秒为单位），以检测新任务和修改的任务。默认为3秒。 这不适用于AEM Forms Workspace。

**client_systemContext_name:** 为AEM Forms Workspace中任务的附件指定要在“添加者”字段（在“附件”选项卡中）中显示的自定义名称（例如“公民”）。

要定义自定义名称，请执行以下操作：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>对于演示应用程序，默认显示名称为&#x200B;**Citizen**。 对于您创建的自定义应用程序，默认显示名称为&#x200B;**System Context Account**。
>
>**client_idleTimeout:** 当用户在特定时间段内保持不活动状态时，AEM Forms Workspace会话过期。要启用该功能，请向全局设置&lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>添加一个条目。 您可以指定值0以禁用空闲超时。 以秒为单位指定时间。
