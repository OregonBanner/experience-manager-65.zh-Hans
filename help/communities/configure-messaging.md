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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---


# 消息功能{#messaging-feature}

除了在论坛和评论中发生的公开可见的互动外，AEM Communities的消息功能还使社区成员能够更加私下地进行互动。

创建[社区站点](/help/communities/overview.md#communitiessites)时，可以包含此功能。

消息功能可以：

**A** -向一个或多个社区成员发送消息

**B** -批量向社区成 [员组发送直接消息](/help/communities/messaging.md#group-messaging)

**C** -发送包含附件的邮件

**D** -转发消息

**E** -回复邮件

**F** -删除消息

**G** -恢复已删除的消息

![消息部分](assets/messaging-section.png)

![恢复消息](assets/restore-message.png)

要启用和修改消息功能，请参阅：

* [为管理](/help/communities/messaging.md) 员配置消息
* [对开发人](/help/communities/essentials-messaging.md) 员来说消息基本

>[!NOTE]
>
>不支持在作者编辑模式下将`Compose Message, Message, or Message List`组件（位于`Communities`组件组中）添加到页面。

## 配置消息传递组件{#configure-messaging-components}

为社区站点启用消息传递后，无需进一步配置即可设置该消息。 如果需要更改默认配置，则会提供该信息。

### 配置消息列表（消息框）{#configure-message-list-message-box}

要修改消息功能&#x200B;**收件箱**、**已发送项**&#x200B;和&#x200B;**垃圾桶**&#x200B;页面的消息列表配置，请以[作者编辑模式](/help/communities/sites-console.md#authoring-site-content)打开站点。

1. 在`Preview`模式中，选择&#x200B;**消息**&#x200B;链接以打开主消息页面。 然后，选择&#x200B;**收件箱**、**已发送项目**&#x200B;或&#x200B;**垃圾桶**&#x200B;来为该邮件列表配置组件。

1. 在`Edit`模式下，选择页面上的组件。
1. 要访问配置对话框，请通过选择`link`图标来取消继承。
取消继承后，可以选择配置图标以打开配置对话框。

1. 配置完成后，必须通过选择`broken link`图标来恢复继承。

![configure-message-列表](assets/configure-message-list.png)

#### 基本选项卡{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服务选择器**

   (*Required*)将此值设置为[AEM Communities消息操作服务](/help/communities/messaging.md#messaging-operations-service)中属性&#x200B;**`serviceSelector.name`**&#x200B;的值。

* **合成页面**

   （*必需*）当成员单击&#x200B;**`Reply`**&#x200B;按钮时要打开的页面。 目标页应包含&#x200B;**撰写消息**&#x200B;表单。

* **答复/视图作为资源**

   如果选中此项，则回复URL和视图URL将引用资源，否则数据将作为查询参数传递到URL中。

* **用户档案显示表单**

   用于显示发件人用户档案的用户档案表单。

* **垃圾桶文件夹**

   如果选中，则此消息列表组件仅显示标记为已删除（垃圾桶）的消息。

* **文件夹路径**

   (*Required*)引用[AEM Communities消息传递操作服务](/help/communities/messaging.md#messaging-operations-service)中为&#x200B;**inbox.path.name**&#x200B;和&#x200B;**sentitems.path.name**&#x200B;设置的值。 为`Inbox`进行配置时，请使用&#x200B;**inbox.path.name**&#x200B;的值添加一个条目。 为`Outbox`进行配置时，请使用&#x200B;**sentitems.path.name**&#x200B;的值添加一个条目。 配置`Trash`时，添加两个同时具有这两个值的条目。

#### 显示选项卡{#display-tab}

![display-tab-message-列表](assets/display-tab-message-list.png)

* **标记阅读按钮**

   如果选中，则显示`Read`按钮，允许将消息标记为已读。

* **标记未读按钮**

   如果选中，则显示`Mark Unread`按钮，允许将消息标记为已读。

* **删除按钮**

   如果选中，则显示`Delete`按钮，允许将消息标记为已读。 如果还选中&#x200B;**`Message Options`**，将重复删除功能。

* **消息选项**

   如果选中，则显示&#x200B;**`Reply`**、**`Reply All`**、**`Forward`**&#x200B;和&#x200B;**`Delete`**&#x200B;按钮，允许重新发送或删除消息。 如果还选中&#x200B;**`Delete Button`**，将重复删除功能。

* **每个页面的消息数**

   指定的数量是分页方案中每页显示的最大消息数。 如果未指定数字（留空），则显示所有消息，且不显示分页。

* **时间戳模式**

   提供一种或多种语言的时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

* **显示用户**

   选择&#x200B;**`Sender`**&#x200B;或&#x200B;**`Recipients`**&#x200B;以确定是显示发件人还是收件人。

### 配置起草消息{#configure-compose-message}

要修改合成消息页面的配置，请以[作者编辑模式](/help/communities/sites-console.md#authoring-site-content)打开站点。

* 在`Preview`模式中，选择&#x200B;**消息**&#x200B;链接以打开主消息页面。 然后选择“新建消息”按钮以打开`Compose Message`页面。

* 在`Edit`模式中，选择包含邮件正文的页面上的主组件。
* 要访问配置对话框，请通过选择`link`图标来取消继承。
取消继承后，可以选择配置图标以打开配置对话框。

* 配置完成后，必须通过选择`broken link`图标来恢复继承。

![config-compose](assets/config-compose-message.png)

#### 基本选项卡{#basic-tab-1}

![基本制表](assets/basic-tab-compose.png)

* **重定向URL**

   输入发送邮件后显示的页面URL。 例如，`../messaging.html`。

* **取消 URL**

   输入发送方取消消息时显示的页面URL。 例如，`../messaging.html`。

* **邮件主题的最大长度**

   “主题”字段中允许的最大字符数。 例如，500。 默认值为无限制。

* **消息正文的最大长度**

   “内容”字段中允许的最大字符数。 例如，10000。 默认值为无限制。

* **服务选择器**

   (*Required*)将此值设置为[AEM Communities消息操作服务](/help/communities/messaging.md#messaging-operations-service)中属性&#x200B;**`serviceSelector.name`**&#x200B;的值。

#### 显示选项卡{#display-tab-1}

![显示——选项卡——合成](assets/display-tab-compose.png)

* **显示主题字段**

   如果选中，则显示`Subject`字段并启用向邮件添加主题。 未选中默认值。

* **主题标签**

   输入在`Subject`字段旁边显示的文本。 默认值为`Subject`。

* **显示附加文件字段**

   如果选中，则显示`Attachment`字段并启用向邮件添加文件附件。 未选中默认值。

* **附加文件标签**

   输入在`Attachment`字段旁边显示的文本。 默认值为&#x200B;**`Attach File`**。

* **显示内容字段**

   如果选中，则显示`Content`字段并启用添加消息正文。 未选中默认值。

* **内容标签**

   输入在`Content`字段旁边显示的文本。 默认值为&#x200B;**`Body`**。

* **使用富文本编辑器**

   如果选中，则表示自定义内容文本框与其自己的富文本编辑器一起使用。 未选中默认值。

* **时间戳模式**

   提供一种或多种语言的时间戳模式。 默认值为en、de、fr、it、es、ja、zh_CN、ko_KR。

