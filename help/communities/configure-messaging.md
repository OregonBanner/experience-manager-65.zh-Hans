---
title: 消息功能
seo-title: 消息功能
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
source-git-commit: 56c2e6b55964ea5f3e180b17bd2a244882aa62ea
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---


# 消息功能 {#messaging-feature}

除了在论坛和评论中发生的公开可见的交互外，AEM Communities的消息传递功能还使社区成员能够更加私下地进行交互。

创建社区站点时可 [以包含](/help/communities/overview.md#communitiessites) 此功能。

消息功能可以：

**A** —— 向一个或多个社区成员发送消息

**B** —— 批量向社区 [成员组发送直接消息](/help/communities/messaging.md#group-messaging)

**C** —— 发送包含附件的邮件

**D** —— 转发消息

**E** —— 回复邮件

**F** —— 删除消息

**G** —— 恢复已删除的消息

![消息](assets/messaging-section.png)![区还原消息](assets/restore-message.png)

要启用和修改消息功能，请参阅：

* [为管理员配置](/help/communities/messaging.md) “消息传递”
* [面向开发人员的](/help/communities/essentials-messaging.md) Messaging Essentials

>[!NOTE]
>
>在作者编辑模式 `Compose Message, Message, or Message List` 下，不支 `Communities`持将组件（在组件组中）添加到页面。


## 配置消息传递组件 {#configure-messaging-components}

为社区站点启用消息传递后，无需进一步配置即可设置该消息。 如果需要更改默认配置，则会提供该信息。

### 配置消息列表（消息框） {#configure-message-list-message-box}

要修改消息传递功能的收件箱 **、已发送**&#x200B;项目和废纸篓页面 **的邮件列表的配置**，请以作者编辑模式打 **开该网**[](/help/communities/sites-console.md#authoring-site-content)站的作者编辑模式。

1. 在模 `Preview` 式中，选择 **消息链** 接以打开主消息页面。 然后，选择“收 **件箱**”、“ **已发送项目** ”或“废 **纸篓** ”来为该邮件列表配置组件。

1. 在模 `Edit` 式中，选择页面上的组件。
1. 要访问配置对话框，请通过选择图标取消继 `link` 承。
取消继承后，可以选择配置图标以打开配置对话框。

1. 配置完成后，必须通过选择图标来恢复继 `broken link` 承。

![configure-message-列表](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**

   (*必需*)将此值设置为AEM Communities消息 **`serviceSelector.name`** 操作服 [务的属性值](/help/communities/messaging.md#messaging-operations-service)。

* **合成页面**

   (必&#x200B;*需*)成员单击按钮时要打开的 **`Reply`** 页面。 目标页面应包含合 **成消息** 。

* **答复/视图作为资源**

   如果选中此项，则回复URL和视图URL将引用资源，否则数据将作为查询参数传递到URL中。

* **用户档案显示表单**

   用于显示发件人用户档案的用户档案表单。

* **垃圾桶文件夹**

   如果选中，则此消息列表组件仅显示标记为已删除（垃圾桶）的消息。

* **文件夹路径**

   (*必需*)引用“AEM Communities **Operations Messaging Service”中为** inbox.path.name和 **sentitems.path.name设**[](/help/communities/messaging.md#messaging-operations-service)置的值。 为配置时， `Inbox`请使用inbox.path.name的值 **添加一个条目**。 为配置时， `Outbox`请使用sentitems.path.name的 **值添加一个条目**。 配置时， `Trash`添加两个同时具有这两个值的条目。

#### 显示选项卡 {#display-tab}

![display-tab-message-列表](assets/display-tab-message-list.png)

* **标记阅读按钮**

   如果选中，则显示 `Read`一个按钮，允许消息标记为已读。

* **标记未读按钮**

   如果选中，则显 `Mark Unread` 示一个按钮，允许消息标记为已读。

* **删除按钮**

   如果选中，则显 `Delete` 示一个按钮，允许消息标记为已读。 如果同时选中，将重复 **`Message Options`** 删除功能。

* **消息选项**

   如果选中，则显 **`Reply`**&#x200B;示、 **`Reply All`**&#x200B;和 **`Forward`** 按钮，允 **`Delete`** 许重新发送或删除消息。 如果同时选中，将重复 **`Delete Button`** 删除功能。

* **每个页面的消息数**

   指定的数量是分页方案中每页显示的最大消息数。 如果未指定任何数字（留空），则显示所有消息，且不显示分页。

* **时间戳模式**

   提供一种或多种语言的时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

* **显示用户**

   选择 **`Sender`** 还是 **`Recipients`** 确定是显示发送者还是收件人。

### 配置起草消息 {#configure-compose-message}

要修改合成消息页面的配置，请在作者编辑模 [式下打开站点](/help/communities/sites-console.md#authoring-site-content)。

* 在模 `Preview` 式中，选择 **消息链** 接以打开主消息页面。 然后选择“新建消息”按钮以打开 `Compose Message` 页面。

* 在模 `Edit` 式中，在包含消息正文的页面上选择主组件。
* 要访问配置对话框，请通过选择图标取消继 `link` 承。
取消继承后，可以选择配置图标以打开配置对话框。

* 配置完成后，必须通过选择图标来恢复继 `broken link` 承。

![config-compose](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![基本制表](assets/basic-tab-compose.png)

* **重定向URL**

   输入发送邮件后显示的页面URL。 For example, `../messaging.html`.

* **取消 URL**

   输入发送方取消消息时显示的页面URL。 For example, `../messaging.html`.

* **邮件主题的最大长度**

   “主题”字段中允许的最大字符数。 例如，500。 默认值为无限制。

* **消息正文的最大长度**

   “内容”字段中允许的最大字符数。 例如，10000。 默认值为无限制。

* **服务选择器**

   (*必需*)将此值设置为AEM Communities消息 **`serviceSelector.name`** 操作服 [务的属性值](/help/communities/messaging.md#messaging-operations-service)。

#### 显示选项卡 {#display-tab-1}

![显示——选项卡——合成](assets/display-tab-compose.png)

* **显示主题字段**

   如果选中，则显示 `Subject` 该字段并启用向邮件添加主题。 未选中默认值。

* **主题标签**

   输入要在字段旁边显示的 `Subject` 文本。 Default is `Subject`.

* **显示附加文件字段**

   如果选中，则显示 `Attachment` 该字段并启用向邮件添加文件附件。 未选中默认值。

* **附加文件标签**

   输入要在字段旁边显示的 `Attachment` 文本。 Default is **`Attach File`**.

* **显示内容字段**

   如果选中，则显示 `Content` 字段并启用添加消息正文。 未选中默认值。

* **内容标签**

   输入要在字段旁边显示的 `Content` 文本。 Default is **`Body`**.

* **使用富文本编辑器**

   如果选中，则表示自定义内容文本框与其自己的富文本编辑器一起使用。 未选中默认值。

* **时间戳模式**

   提供一种或多种语言的时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

