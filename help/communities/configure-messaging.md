---
title: 消息传递功能
seo-title: 消息传递功能
description: 配置消息传递组件
seo-description: 配置消息传递组件
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 消息传递功能{#messaging-feature}

除了在论坛和评论中发生的公开可见交互外，***AEM Communities的消息传递功能还使社区成员能够更加私下地进行交互。

创建社区站点时可 [以包含](/help/communities/overview.md#communitiessites) 此功能。

消息传递功能可以：

**A** —— 发送消息给一个或多个社区成员&#x200B;**B** —— 将直接消息批量发送给社区成员组 [C](/help/communities/messaging.md#group-messaging)C ************ -发送消息，附件D转发消息**转发消息**回复消息*删除消息*删除消息F-删除消息*

![消息段](assets/messaging-section.png)![恢复消息](assets/restore-message.png)

要启用和修改消息功能，请参阅：

* [为管理员配置消息传递](/help/communities/messaging.md) ,
* [面向开发人员的Messaging Essentials](/help/communities/essentials-messaging.md)

>[!NOTE]
>
>在创作编辑模式下，不 `Compose Message, Message, or Message List` 支持将组件( `Communities`在组件组中)添加到页面。

## 配置消息传递组件 {#configure-messaging-components}

为社区站点启用消息传递后，即可设置该站点，无需进一步配置。 如果需要更改默认配置，则会提供该信息。

### 配置消息列表（消息框） {#configure-message-list-message-box}

要修改收件箱、已发送项目和 ****废纸篓****消息功能的消息列表的配置，请以作者编辑模式打 **开站点**[](/help/communities/sites-console.md#authoring-site-content)。

1. 在模 `Preview`式中，选择**消息**链接以打开主消息页面。 然后，选择 **收件箱**、**已发送项目**或**垃圾桶*，为该消息列表配置组件。

1. 在模 `Edit` 式中，选择页面上的组件。
1. 要访问配置对话框，请通过选择图标取消 `link`继承。
取消继承后，可以选择配置图标以打开配置对话框。

1. 配置完成后，必须通过选择图标来恢复继承 `broken link` 。

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**(*必需*)将其设置为`serviceSelector.name`AEM Communities Messaging Operations service中属性** [**的值](/help/communities/messaging.md#messaging-operations-service)。

* **合成页面**(必&#x200B;*需*)当成员单击**`Reply`**按钮时要打开的页面。 目标页面应包含“合 **成消息** ”表单。

* **作为资源回复／查**&#x200B;看如果选中此项，则回复URL和查看URL将引用资源，否则数据将作为URL中的查询参数传递。

* **个人资料显示表**&#x200B;单用于显示发件人个人资料的个人资料表单。

* **废纸篓文件夹**&#x200B;如果选中此项，则此“消息列表”组件将仅显示标记为已删除（废纸篓）的消息。

* **文件夹路径**(*必需*)引用 **AEM Communities Messaging Operations service中inbox.path.name** 和**sentitems.path.name **设置的值 [](/help/communities/messaging.md#messaging-operations-service)。 为配置时， `Inbox`请使用inbox.path.name的值 **添加一个条目**。 为配置时， `Outbox`请使用 **sentitems.path.name的值添加一个条目**。 在配置时， `Trash`添加两个同时包含这两个值的条目。

#### 显示选项卡 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **标记读取按**&#x200B;钮如果选中，则显 `Read`示一个按钮，允许消息标记为读取。

* **标记为未读按**&#x200B;钮如果选中，则显示一 `Mark Unread` 个按钮，允许将消息标记为已读。

* **删除按**&#x200B;钮如果选中，则显 `Delete`示一个按钮，允许将消息标记为已读。 如果同时选中，将复制 **`Message Options`** 删除功能。

* **消息选**&#x200B;项如果选中 **`Reply`**, **`Reply All`**&#x200B;则显示、*`Forward`***和**`Delete`**按钮，允许重新发送或删除消息。 如果同时选中，将复制 **`Delete Button`** 删除功能。

* **每页消息**&#x200B;指定的数量是分页方案中每页显示的最大消息数。 如果未指定编号（留空），则显示所有消息且不存在分页。

* **时间戳模**&#x200B;式为一种或多种语言提供时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

* **显示用**&#x200B;户选择**`Sender`**或**`Recipients`**，以确定显示发送方还是收件人。

### 配置合成消息 {#configure-compose-message}

要修改合成消息页面的配置，请以作者编辑模式 [打开站点](/help/communities/sites-console.md#authoring-site-content)。

* 在模 `Preview`式中，选择**消息**链接以打开主消息页面。 然后选择“新建消息”按钮以打开 `Compose Message` 页面。

* 在模 `Edit` 式中，在包含消息正文的页面上选择主组件。
* 要访问配置对话框，请通过选择图标取消 `link`继承。
取消继承后，可以选择配置图标以打开配置对话框。

* 配置完成后，必须通过选择图标来恢复继 `broken link`承。

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![基本制表符组合](assets/basic-tab-compose.png)

* **重定向URL**&#x200B;输入发送消息后显示的页面的URL。 For example, `../messaging.html`.

* **取消URL**&#x200B;输入发送方取消消息时显示的页面的URL。 For example, `../messaging.html`.

* **消息主题的最大长度**“主题”字段中允许的最大字符数。 例如，500。 默认值为无限制。

* **消息正文的最大长**&#x200B;度“内容”字段中允许的最大字符数。 例如，10000。 默认值为无限制。

* **服务选择器**(*必需*)将其设置为`serviceSelector.name`AEM Communities Messaging Operations service中属性** [**的值](/help/communities/messaging.md#messaging-operations-service)。

#### 显示选项卡 {#display-tab-1}

![显示——选项卡——合成](assets/display-tab-compose.png)

* **显示主题字**&#x200B;段如果选中，则显示 `Subject` 该字段并启用向消息中添加主题。 未选中默认值。

* **主题标**&#x200B;签输入要显示在字段旁边的 `Subject` 文本。 Default is `Subject`.

* **显示附加文件字**&#x200B;段如果选中，则显示该字 `Attachment` 段并启用向邮件中添加文件附件的功能。 未选中默认值。

* **附加文件标**&#x200B;签输入要显示在字段旁边的 `Attachment` 文本。 Default is **`Attach File`**.

* **显示内容字段**&#x200B;如果选中此项，则显示 `Content` 该字段并启用添加消息正文。 未选中默认值。

* **内容标**&#x200B;签输入要显示在字段旁边的 `Content` 文本。 Default is **`Body`**.

* **使用富文本编辑器**&#x200B;如果选中此项，则表示自定义内容文本框的使用情况与其自己的富文本编辑器相同。 未选中默认值。

* **时间戳模**&#x200B;式为一种或多种语言提供时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

