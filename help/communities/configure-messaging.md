---
title: 消息传送功能
seo-title: Messaging Feature
description: 配置消息传送组件
seo-description: Configuring Messaging components
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
source-wordcount: '927'
ht-degree: 3%

---

# 消息传送功能 {#messaging-feature}

除了在论坛和评论中发生的公开可见的交互之外，AEM Communities的报文传送功能还使社区成员能够更加私下地进行交互。

当 [社区网站](/help/communities/overview.md#communitiessites) 创建时。

消息传送功能提供以下功能：

**A**  — 向一个或多个社区成员发送消息

**B**  — 发送私信 [批量到社区成员组](/help/communities/messaging.md#group-messaging)

**C**  — 发送带有附件的邮件

**D**  — 转发消息

**E**  — 回复邮件

**F**  — 删除消息

**G**  — 恢复已删除的消息

![消息传送区](assets/messaging-section.png)

![还原消息](assets/restore-message.png)

要启用和修改消息传送功能，请参阅：

* [配置消息传送](/help/communities/messaging.md) 对于管理员
* [消息传送要点](/help/communities/essentials-messaging.md) 适用于开发人员

>[!NOTE]
>
>不支持添加 `Compose Message, Message, or Message List` 组件(可在 `Communities`组件组)到“创作编辑”模式下的页面。

## 配置消息传送组件 {#configure-messaging-components}

为社区站点启用消息传送后，无需进一步配置即可进行设置。 如果需要更改默认配置，则会提供该信息。

### 配置消息列表（消息框） {#configure-message-list-message-box}

修改 **收件箱**, **已发送项目**&#x200B;和 **垃圾** 消息传送功能的页面，在 [创作编辑模式](/help/communities/sites-console.md#authoring-site-content).

1. 在 `Preview` 模式，选择 **消息** 链接以打开主消息传送页面。 然后，选择 **收件箱**, **已发送项目** 或 **垃圾** 为该消息列表配置组件。

1. 在 `Edit` 模式下，在页面上选择组件。
1. 要访问配置对话框，请通过选择 `link` 图标。
取消继承后，可以选择配置图标以打开配置对话框。

1. 配置完成后，需要通过选择 `broken link` 图标。

![configure-message-list](assets/configure-message-list.png)

#### “基本”选项卡 {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**

   (*必需*)将其设置为属性的值 **`serviceSelector.name`** 从 [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

* **撰写页面**

   (*必需*)成员单击 **`Reply`** 按钮。 目标页面应包含 **撰写消息** 表单。

* **回复/查看为资源**

   如果选中此项，则回复URL和查看URL将引用资源，否则数据将作为查询参数在URL中传递。

* **配置文件显示表单**

   用于显示发件人配置文件的配置文件表单。

* **垃圾桶文件夹**

   如果选中，此消息列表组件仅显示标记为已删除（垃圾桶）的消息。

* **文件夹路径**

   (*必需*)引用为 **inbox.path.name** 和 **sentitems.path.name** 在 [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service). 为 `Inbox`，使用的值添加一个条目 **inbox.path.name**. 为 `Outbox`，使用的值添加一个条目 **sentitems.path.name**. 配置 `Trash`，则添加两个具有这两个值的条目。

#### “显示”选项卡 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **“标记读取”按钮**

   如果选中，则显示 `Read`按钮，将消息标记为已读。

* **“标记未读”按钮**

   如果选中，则显示 `Mark Unread` 按钮，将消息标记为已读。

* **“删除”按钮**

   如果选中，则显示 `Delete` 按钮，将消息标记为已读。 将在 **`Message Options`** 中。

* **消息选项**

   如果选中，则显示 **`Reply`**, **`Reply All`**, **`Forward`** 和 **`Delete`** 允许重新发送或删除消息的按钮。 将在 **`Delete Button`** 中。

* **每个页面的消息数**

   指定的编号是分页方案中每页显示的消息的最大数量。 如果未指定数字（留空），则会显示所有消息，并且不进行分页。

* **时间戳模式**

   为一种或多种语言提供时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

* **显示用户**

   选择 **`Sender`** 或 **`Recipients`** 以确定是显示发件人还是收件人。

### 配置撰写消息 {#configure-compose-message}

要修改撰写消息页面的配置，请在 [创作编辑模式](/help/communities/sites-console.md#authoring-site-content).

* 在 `Preview` 模式，选择 **消息** 链接以打开主消息传送页面。 然后，选择New Message按钮以打开 `Compose Message` 页面。

* 在 `Edit` 模式下，在包含消息正文的页面上选择主组件。
* 要访问配置对话框，请通过选择 `link` 图标。
取消继承后，可以选择配置图标以打开配置对话框。

* 配置完成后，需要通过选择 `broken link` 图标。

![config-compose-message](assets/config-compose-message.png)

#### “基本”选项卡 {#basic-tab-1}

![基本 — 制表](assets/basic-tab-compose.png)

* **重定向URL**

   输入发送消息后显示的页面URL。 例如：`../messaging.html`。

* **取消 URL**

   输入发件人取消消息时显示的页面URL。 例如：`../messaging.html`。

* **消息主体的最大长度**

   “主题”字段中允许的最大字符数。 例如，500。 默认为无限制。

* **消息正文的最大长度**

   “内容”字段中允许的最大字符数。 例如，10000。 默认为无限制。

* **服务选择器**

   (*必需*)将其设置为属性的值 **`serviceSelector.name`** 从 [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

#### “显示”选项卡 {#display-tab-1}

![显示 — 选项卡 — 合成](assets/display-tab-compose.png)

* **显示主题字段**

   如果选中，则显示 `Subject` 字段，并启用向消息添加主题。 未选中默认值。

* **主题标签**

   输入要在 `Subject` 字段。 默认为 `Subject`.

* **显示附加文件字段**

   如果选中，则显示 `Attachment` 字段，并启用向消息添加文件附件的功能。 未选中默认值。

* **附加文件标签**

   输入要在 `Attachment` 字段。 默认为 **`Attach File`**.

* **显示内容字段**

   如果选中，则显示 `Content` 字段，并启用添加消息正文。 未选中默认值。

* **内容标签**

   输入要在 `Content` 字段。 默认为 **`Body`**.

* **使用富文本编辑器**

   如果选中，则表示使用具有其自身富文本编辑器的自定义内容文本框。 未选中默认值。

* **时间戳模式**

   为一种或多种语言提供时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。
