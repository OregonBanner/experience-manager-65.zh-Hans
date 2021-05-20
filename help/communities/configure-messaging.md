---
title: 消息传送功能
seo-title: 消息传送功能
description: 配置消息传送组件
seo-description: 配置消息传送组件
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# 消息传送功能{#messaging-feature}

除了在论坛和评论中发生的公开可见的交互之外，AEM Communities的报文传送功能还使社区成员能够更加私下地进行交互。

创建[社区站点](/help/communities/overview.md#communitiessites)时，可以包含此功能。

消息传送功能提供以下功能：

**A**  — 向一个或多个社区成员发送消息

**B**  — 批量向社区 [成员组发送私信](/help/communities/messaging.md#group-messaging)

**C**  — 发送带有附件的消息

**D**  — 转发消息

**E**  — 回复消息

**F**  — 删除消息

**G**  — 恢复已删除的消息

![消息传送区](assets/messaging-section.png)

![还原消息](assets/restore-message.png)

要启用和修改消息传送功能，请参阅：

* [为管理](/help/communities/messaging.md) 员配置消息
* [对开发人](/help/communities/essentials-messaging.md) 员而言的消息传送要求

>[!NOTE]
>
>不支持在创作编辑模式下将`Compose Message, Message, or Message List`组件（位于`Communities`组件组中）添加到页面。

## 配置消息传送组件{#configure-messaging-components}

为社区站点启用消息传送后，无需进一步配置即可进行设置。 如果需要更改默认配置，则会提供该信息。

### 配置消息列表（消息框）{#configure-message-list-message-box}

要修改&#x200B;**收件箱**、**已发送项目**&#x200B;和&#x200B;**邮件功能的垃圾桶**&#x200B;页面的邮件列表配置，请在[作者编辑模式](/help/communities/sites-console.md#authoring-site-content)中打开该站点。

1. 在`Preview`模式下，选择&#x200B;**消息**&#x200B;链接以打开主消息传送页面。 然后，选择&#x200B;**Inbox**、**已发送项目**&#x200B;或&#x200B;**垃圾桶**&#x200B;以配置该消息列表的组件。

1. 在`Edit`模式下，选择页面上的组件。
1. 要访问配置对话框，请通过选择`link`图标来取消继承。
取消继承后，可以选择配置图标以打开配置对话框。

1. 配置完成后，需要通过选择`broken link`图标来恢复继承。

![configure-message-list](assets/configure-message-list.png)

#### 基本选项卡{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**

   （*必需*）将此值设置为[AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)中属性&#x200B;**`serviceSelector.name`**&#x200B;的值。

* **撰写页面**

   （*必需*）成员单击&#x200B;**`Reply`**&#x200B;按钮时要打开的页面。 目标页面应包含&#x200B;**撰写消息**&#x200B;窗体。

* **回复/查看为资源**

   如果选中此项，则回复URL和查看URL将引用资源，否则数据将作为查询参数在URL中传递。

* **配置文件显示表单**

   用于显示发件人配置文件的配置文件表单。

* **垃圾桶文件夹**

   如果选中，此消息列表组件仅显示标记为已删除（垃圾桶）的消息。

* **文件夹路径**

   （*必需*）引用[AEM Communities消息传送操作服务](/help/communities/messaging.md#messaging-operations-service)中&#x200B;**inbox.path.name**&#x200B;和&#x200B;**sentitems.path.name**&#x200B;的值集。 为`Inbox`配置时，请使用&#x200B;**inbox.path.name**&#x200B;的值添加一个条目。 为`Outbox`配置时，请使用&#x200B;**sentitems.path.name**&#x200B;的值添加一个条目。 为`Trash`配置时，请添加两个具有这两个值的条目。

#### 显示选项卡{#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **“标记读取”按钮**

   如果选中，则显示`Read`按钮，允许将消息标记为已读。

* **“标记未读”按钮**

   如果选中，则显示`Mark Unread`按钮，允许将消息标记为已读。

* **“删除”按钮**

   如果选中，则显示`Delete`按钮，允许将消息标记为已读。 如果同时选中&#x200B;**`Message Options`**，则将复制删除功能。

* **消息选项**

   如果选中此项，则显示&#x200B;**`Reply`**、**`Reply All`**、**`Forward`**&#x200B;和&#x200B;**`Delete`**&#x200B;按钮，允许重新发送或删除消息。 如果同时选中&#x200B;**`Delete Button`**，则将复制删除功能。

* **每个页面的消息数**

   指定的编号是分页方案中每页显示的消息的最大数量。 如果未指定数字（留空），则会显示所有消息，并且不进行分页。

* **时间戳模式**

   为一种或多种语言提供时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

* **显示用户**

   选择&#x200B;**`Sender`**&#x200B;或&#x200B;**`Recipients`**&#x200B;以确定是显示发件人还是收件人。

### 配置撰写消息{#configure-compose-message}

要修改撰写消息页面的配置，请以[作者编辑模式](/help/communities/sites-console.md#authoring-site-content)打开站点。

* 在`Preview`模式下，选择&#x200B;**消息**&#x200B;链接以打开主消息传送页面。 然后，选择“新建消息”按钮以打开`Compose Message`页面。

* 在`Edit`模式下，在包含消息正文的页面上选择主组件。
* 要访问配置对话框，请通过选择`link`图标来取消继承。
取消继承后，可以选择配置图标以打开配置对话框。

* 配置完成后，需要通过选择`broken link`图标来恢复继承。

![config-compose-message](assets/config-compose-message.png)

#### 基本选项卡{#basic-tab-1}

![基本 — 制表](assets/basic-tab-compose.png)

* **重定向URL**

   输入发送消息后显示的页面URL。 例如，`../messaging.html`。

* **取消 URL**

   输入发件人取消消息时显示的页面URL。 例如，`../messaging.html`。

* **消息主体的最大长度**

   “主题”字段中允许的最大字符数。 例如，500。 默认为无限制。

* **消息正文的最大长度**

   “内容”字段中允许的最大字符数。 例如，10000。 默认为无限制。

* **服务选择器**

   （*必需*）将此值设置为[AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)中属性&#x200B;**`serviceSelector.name`**&#x200B;的值。

#### 显示选项卡{#display-tab-1}

![显示 — 选项卡 — 合成](assets/display-tab-compose.png)

* **显示主题字段**

   如果选中，则显示`Subject`字段并启用向消息添加主题。 未选中默认值。

* **主题标签**

   在`Subject`字段旁边输入要显示的文本。 默认值为`Subject`。

* **显示附加文件字段**

   如果选中，则显示`Attachment`字段并启用向消息添加文件附件。 未选中默认值。

* **附加文件标签**

   在`Attachment`字段旁边输入要显示的文本。 默认值为&#x200B;**`Attach File`**。

* **显示内容字段**

   如果选中，则显示`Content`字段并启用添加消息正文。 未选中默认值。

* **内容标签**

   在`Content`字段旁边输入要显示的文本。 默认值为&#x200B;**`Body`**。

* **使用富文本编辑器**

   如果选中，则表示使用具有其自身富文本编辑器的自定义内容文本框。 未选中默认值。

* **时间戳模式**

   为一种或多种语言提供时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。
