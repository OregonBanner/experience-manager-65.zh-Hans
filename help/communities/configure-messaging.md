---
title: 消息传送功能
description: 了解如何配置AEM Communities的消息传送功能，以允许社区成员更私密地相互交互。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 3%

---

# 消息传送功能 {#messaging-feature}

除了在论坛和评论中发生的公开可见的交互之外，AEM Communities的消息传送功能还允许社区成员更私密地相互交互。

此功能可在 [社区站点](/help/communities/overview.md#communitiessites) 创建。

利用消息传送功能，可执行以下操作：

**A**  — 向一个或多个社区成员发送消息

**B**  — 发送私信 [批量到社区成员组](/help/communities/messaging.md#group-messaging)

**C**  — 发送带有附件的邮件

**D**  — 转发消息

**E**  — 回复消息

**F**  — 删除消息

**G**  — 恢复已删除的消息

![messaging-section](assets/messaging-section.png)

![恢复消息](assets/restore-message.png)

要启用和修改消息传送功能，请参阅：

* [配置消息传送](/help/communities/messaging.md) 适用于管理员
* [消息传送要点](/help/communities/essentials-messaging.md) 面向开发人员

>[!NOTE]
>
>不支持添加 `Compose Message, Message, or Message List` 组件(可在 `Communities`（组件组）的页面中显示的页面名称。

## 配置消息组件 {#configure-messaging-components}

为社区站点启用消息传送后，将进行设置，无需进一步配置。 如果需要更改默认配置，则会提供此信息。

### 配置消息列表（消息框） {#configure-message-list-message-box}

要修改以下项的消息列表的配置： **收件箱**， **已发送项目**、和 **垃圾桶** 在消息传送功能页面上，打开网站，网址为 [作者编辑模式](/help/communities/sites-console.md#authoring-site-content).

1. 在 `Preview` 模式，选择 **消息** 打开主消息传递页面的链接。 然后选择以下任一选项 **收件箱**， **已发送项目** 或 **垃圾桶** 为该消息列表配置组件。

1. 在 `Edit` 模式，在页面上选择组件。
1. 要访问配置对话框，请选择 `link` 图标。
取消继承后，可以选择配置图标以打开配置对话框。

1. 配置完成后，必须选择 `broken link` 图标。

![configure-message-list](assets/configure-message-list.png)

#### “基本”选项卡 {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**

  (*必填*)将此参数设置为属性的值 **`serviceSelector.name`** 从 [AEM Communities消息传送操作服务](/help/communities/messaging.md#messaging-operations-service).

* **撰写页面**

  (*必填*)成员单击 **`Reply`** 按钮。 目标页面应包含 **撰写消息** 表单。

* **回复/查看资源**

  如果选中，回复URL和查看URL将引用资源，否则数据将作为URL中的查询参数传递。

* **配置文件显示表单**

  用于显示发件人配置文件的配置文件表单。

* **将文件夹置入垃圾桶**

  如果选中，此消息列表组件仅显示标记为已删除（垃圾桶）的消息。

* **文件夹路径**

  (*必填*)引用为设置的值 **收件箱路径名称** 和 **sentitems.path.name** 在 [AEM Communities消息传送操作服务](/help/communities/messaging.md#messaging-operations-service). 为配置时 `Inbox`，添加一个条目，使用值 **收件箱路径名称**. 为配置时 `Outbox`，添加一个条目，使用值 **sentitems.path.name**. 配置时 `Trash`，添加两个同时包含两个值的条目。

#### “显示”选项卡 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **标记读取按钮**

  如果选中，将显示 `Read`按钮以将消息标记为已读。

* **标记未读按钮**

  如果选中，将显示 `Mark Unread` 按钮以将消息标记为已读。

* **删除按钮**

  如果选中，将显示 `Delete` 按钮以将消息标记为已读。 在以下情况下复制删除功能 **`Message Options`** 也会被选中。

* **消息选项**

  如果选中，将显示 **`Reply`**， **`Reply All`**， **`Forward`**、和 **`Delete`** 按钮允许重新发送或删除消息。 在以下情况下复制删除功能 **`Delete Button`** 也会被选中。

* **每个页面的消息数**

  指定的数字是分页方案中每页显示的最大消息数。 如果未指定数字（留空），则会显示所有消息并且没有分页。

* **时间戳模式**

  为一种或多种语言提供时间戳模式。 对于en、de、fr、it、es、ja、zh_CN、ko_KR，默认值为。

* **显示用户**

  选择 **`Sender`** 或 **`Recipients`** 以便您确定是显示发件人还是收件人。

### 配置撰写消息 {#configure-compose-message}

要修改撰写消息页面的配置，请在中打开该站点 [作者编辑模式](/help/communities/sites-console.md#authoring-site-content).

* 在 `Preview` 模式，选择 **消息** 打开主消息传递页面的链接。 然后，选择新建消息按钮，以便您可以打开 `Compose Message` 页面。

* 在 `Edit` 模式，在包含消息正文的页面上选择主组件。
* 要访问配置对话框，请选择 `link` 图标。
取消继承后，可以选择配置图标以打开配置对话框。

* 配置完成后，必须选择 `broken link` 图标。

![config — 撰写消息](assets/config-compose-message.png)

#### “基本”选项卡 {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **重定向URL**

  输入发送消息后显示的页面URL。 例如：`../messaging.html`。

* **取消 URL**

  输入发送者取消邮件时显示的页面URL。 例如：`../messaging.html`。

* **消息主题的最大长度**

  主题字段中允许的最大字符数。 例如，500。 默认值为无限制。

* **消息正文的最大长度**

  内容字段中允许的最大字符数。 例如，10000。 默认值为无限制。

* **服务选择器**

  (*必填*)将此参数设置为属性的值 **`serviceSelector.name`** 从 [AEM Communities消息传送操作服务](/help/communities/messaging.md#messaging-operations-service).

#### “显示”选项卡 {#display-tab-1}

![显示 — 选项卡 — 合成](assets/display-tab-compose.png)

* **显示主题字段**

  如果选中，则显示 `Subject` 字段并启用向消息添加主题。 默认未选中。

* **主题标签**

  输入要显示在旁边的文本 `Subject` 字段。 默认为 `Subject`.

* **显示附加文件字段**

  如果选中，则显示 `Attachment` 字段并启用向邮件添加文件附件。 默认未选中。

* **附加文件标签**

  输入要显示在旁边的文本 `Attachment` 字段。 默认为 **`Attach File`**.

* **显示内容字段**

  如果选中，则显示 `Content` 字段并启用添加消息正文。 默认未选中。

* **内容标签**

  输入要显示在旁边的文本 `Content` 字段。 默认为 **`Body`**.

* **使用富文本编辑器**

  如果选中，则表示使用具有自己的富文本编辑器的自定义内容文本框。 默认未选中。

* **时间戳模式**

  为一种或多种语言提供时间戳模式。 对于en、de、fr、it、es、ja、zh_CN、ko_KR，默认值为。
