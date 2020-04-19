---
title: 导入和导出全局设置
seo-title: 导入和导出全局设置
description: 您可以导入和导出Workspace的搜索模板定义和全局设置。
seo-description: 您可以导入和导出Workspace的搜索模板定义和全局设置。
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 导入和导出全局设置 {#importing-and-exporting-global-settings}

您可以导入和导出Workspace的搜索模板定义和全局设置。

>[!NOTE]
>
>AEM表单发行版中已弃用Flex工作空间。

例如，您可以从开发环境移动到生产环境，方法是从一个环境导出搜索模板定义和全局设置，然后将它们导入到另一个。

导出全局设置文件后，可以在XML或文本编辑器中修改设置。 但是，您唯一想要编辑的设置是JChannelConnectionProperties、formViewOnly和specialRoutes设置。 有关详细信息，请参阅工 [作区全局设置](importing-exporting-global-settings.md#workspace-global-settings)。


>[!NOTE]
>
>如果更改全局设置文件中的事件属性，则必须重新启动服务器。

## 导入搜索模板定义 {#import-a-search-template-definition}

1. 在管理控制台中，单击“服务”>“工作区”>“全局管理”。
1. 在“导入搜索模板定义”框下，单击“选择文件”，然后选择搜索模板。 您只能导入最初从Workspace实例导出的搜索模板定义。
1. 单击导入。

## 导出搜索模板定义 {#export-a-search-template-definition}

1. 在“全局管理”页面的“导出搜索模板”定义下，单击“全部列表”。
1. 在搜索模板的列表中，选择要导出的模板。

   >[!NOTE]
   >
   >您可以选择多个模板，但只会导出最后选定的模板。

1. 单击“导出”，然后在计算机上保存文件。

## 导入全局设置 {#import-global-settings}

1. 在“全局管理”页面的“导入全局设置”下，单击“选择文件”，然后选择全局设置文件。 全局设置文件必须采用XML格式。
1. 单击导入。

## 导出全局设置 {#export-global-settings}

1. 在“全局管理”页面的“导出全局设置”下，单击“导出”。
1. 将文件保存在计算机上。

## 工作区全局设置 {#workspace-global-settings}

可以修改全局设置文件；但是，您唯一想要编辑的设置是JChannelConnectionProperties、formViewOnly和specialRoutes设置。

>[!NOTE]
>
>AEM表单发行版中已弃用Flex工作空间。

工作区全局设置文件包括以下设置：

### specialRoutes设置 {#specialroutes-settings}

specialRoutes *设置指定* Workspace中特殊路由的属性，即批准和拒绝。 在某些情况下，这些路由的按钮会显示在Workspace的任务卡上，用户无需打开表单即可选择它们。 您可以修改全局设置文件中的specialRoutes设置，以添加用于批准和拒绝的自定义名称或创建其他路由。

**client_specialRoutes_routes_approve_style:** 位于工作区主题中的样式名称，用于标识批准按钮图标。 样式必须包括启用图标和禁用图标的值。 要为自定义按钮定义样式，必须使用以下模板：工` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` 作区CSS文件嵌入在workspace-theme.swf文件中，该文件位于adobe-workspace-client.ear > adobe-workspace-client.war文件中。 要更改工作区的外观，必须重新编译workspace-theme.swf文件。

**client_specialRoutes_routes_deny_names:** Workbench用户可用来解释为“deny”的字符串的各种不同。 字符串区分大小写。 例如，默认值为deny。 如果工作台用户在流程中使用“拒绝”一词，则无法识别该词。 必须向此设置添加“拒绝”一词，以便自定义路由按钮并将样式应用于该按钮。

**client_specialRoutes_routes_deny_style:** 位于Workspace主题文件中的样式名称，用于标识拒绝按钮图标。 样式必须包括启用图标和禁用图标的值。 要为自定义按钮定义样式，必须使用以下模板：`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }`**client_specialRoutes_routes_approve_names:** Workbench用户可用来解释为“approve”的字符串的各种不同。 字符串区分大小写。 例如，默认值为approve。 如果工作台用户在流程中使用“批准”一词，则不会识别该词。 必须向此设置添加“批准”字样，以便自定义路由按钮并将样式应用于该按钮。

**client_specialRoutes_names:** 用于从资源文件中查找自定义字符串值的键。 此设置中的每个条目都需要包含名称和样式的值。

### JGroup设置 {#jgroup-settings}

这些设置仅在从Adobe LiveCycle ES 2.5或更早版本升级后才显示。

**server_remoteevents_ClientTimeout毫秒：** JGroup等待事件消息的最长时间。 不应更改此设置。

**server_remoteevents_ServerTimeout毫秒：** 服务器上接收JGroup消息的超时。 此选项设置从服务器向客户端发送消息的延迟。

**server_remoteevents_JChannelConnectionProperties:** 用于在服务器(RemoteEvent服务在其上处理服务事件)与Workspace的所有实例之间通信的JGroup的连接属性。

您可能需要更改多播IP地址(mcast_addr)、多播IP端口(mcast_port)和多播包(ip_ttl)的TTL值。 默认情况下，多播IP地址和端口值是随机生成的，并且通常不需要更改这些值。 但是，如果您的公司对多播IP地址的特定多播范围有任何网络策略，则可能需要更改这些值。

>[!NOTE]
>
>TTL必须大于群集中服务器之间的网络交换机数量；但是，如果设置的值过高，则会导致多播数据包进入子网，在子网中将丢弃这些数据包。

不应更改此设置中的其余属性。

**server_remoteevents_JGroupName:** 用于远程事件通信的JGroup的名称。 该值是随机生成的，以避免群集中的冲突。 不应更改此值。

有关JGroup和Workspace的其他信息，请参 [阅JGroup和AEM表单工作区——说明](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html)。

### formView设置 {#formview-settings}

**client_formView_openFormInFullScreen:** 要以全屏模式在Workspace中显示所有表单，请将此选项设置为true。 默认情况下，此选项设置为false，并且表单不以全屏模式显示。 请注意，用户服务包含一个选项，用于以全屏模式打开与文档关联的任务。 这使您能够按每个进程控制显示。

**client_routes_formViewOnly:** 设置为“True”时，路由不会显示在Workspace的卡视图或列表视图中。 默认值为False，表示路由以卡视图和列表视图显示。

### 其他设置 {#other-settings}

**client_mimeTypes_openOutsideBrowser:** 将在Workspace浏览器实例外打开的文档的MIME类型。 如果贵组织的进程需要其他MIME类型，请在此处指定它。 默认值为：

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** 缓存自定义任务用户界面。

**server_debugLevel:** 请勿更改此设置。

**client_pollingInterval:** 设置在（JEE上的AEM表单已弃用）Flex Workspace上使用的轮询间隔（以秒为单位），以检测新的和修改的任务。 默认值是3秒。 这对AEM Forms Workspace不起作用。

**client_systemContext_name:** 在AEM Forms Workspace中，为任务的附件指定要在“添加者”字段（在“附件”选项卡中）中显示的自定义名称（例如“公民”）。

要定义自定义名称，请执行以下操作：

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>对于Demo应用程序，默认显示名称为 **Citizen**。 对于您创建的自定义应用程序，默认显示名称为 **System Context Account**。***client_idleTimeout:** 当用户在特定时间段内保持不活动状态时，AEM Forms Workspace会话将过期。 要启用该功能，请向Global Settings &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>添加一个条目。 您可以指定值0以禁用空闲超时。 以秒为单位指定时间量。
