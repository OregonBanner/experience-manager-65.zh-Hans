---
title: 配置消息
seo-title: 配置消息
description: 社区消息
seo-description: 社区消息
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---


# 配置消息{#configure-messaging}

## 概述 {#overview}

AEM Communities的消息功能允许登录的站点访客（成员）相互发送消息，当登录到站点时，这些消息可供访问。

在[社区站点创建](/help/communities/sites-console.md)期间选中一个框，为社区站点启用消息。

此页包含有关默认配置和可能调整的信息。

有关开发人员的其他信息，请参阅[Messaging Essentials](/help/communities/essentials-messaging.md)。

## 消息操作服务{#messaging-operations-service}

配置[AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)标识处理与消息相关请求的端点、服务应用于存储消息的文件夹，以及如果消息可能包含文件附件，允许哪些文件类型。

对于使用`Communities Sites console`创建的社区站点，已存在服务实例，收件箱设置为`/mail/inbox`。

### 社区消息操作服务{#community-messaging-operations-service}

如下所示，使用[站点创建向导](/help/communities/sites-console.md)创建的站点存在服务配置。 通过选择配置旁边的铅笔图标，可以查看或编辑配置。

![消息 — 操作](assets/messaging-operations.png)

### 添加新的配置 {#add-new-configuration}

要添加新配置，请选择服务名称旁边的加号“**+**”图标：

* **消息字段允许列表**

   指定用户可以编辑和保留的合成消息组件的属性。 如果添加了新的表单元素，则需要添加元素ID（如果需要）才能存储在SRP中。 默认为两个条目：*主题*&#x200B;和&#x200B;*内容*。

* **消息框大小限制**

   每个用户消息框中的最大字节数。 默认值为&#x200B;*1073741824*(1 GB)。

* **消息计数限制**

   每个用户允许的消息总数。 值为–1表示允许不限数量的消息，但须遵守消息框大小限制。 默认值为&#x200B;*10000*(10k)。

* **通知投放失败**

   如果选中，则在消息投放未能达到某些收件人时通知发送者。 默认值为&#x200B;*checked*。

* **失败投放发件人ID**

   在投放失败消息中显示的发件人名称。 默认值为&#x200B;*failureNotifier*。

* **失败消息模板路径**

   投放失败消息模板根的绝对路径。 默认值为&#x200B;*/etc/notification/messaging/default*。

* **重试**

   尝试重新发送未传递的消息的次数。 默认值为&#x200B;*3*。

* **在重试之间等待**

   在发送失败时尝试重新发送消息之间等待的秒数。 默认值为&#x200B;*100*（秒）。

* **计数更新池大小**

   用于计数更新的并发线程数。 默认值为&#x200B;*10*。

* **收件箱路径**

   （*必需*）用于`inbox`文件夹的路径，相对于用户节点(/home/users/*username*)。 路径不能以尾随正斜杠“/”结束。 默认值为&#x200B;*/mail/inbox*。

* **已发送项目路径**

   （*必需*）用于`sent items`文件夹的路径，相对于用户节点(/home/users/*username*)。 路径不能以尾随正斜杠“/”结束。 默认值为&#x200B;*/mail/sentitems*。

* **支持附件**

   如果选中，则用户可以向邮件中添加附件。 默认值为&#x200B;*checked*。

* **启用组消息传递**

   如果选中，注册用户可以向一组成员发送批量消息。 默认值为&#x200B;*取消选择*。

* **最大值总收件人**

   如果启用了组消息传递，请指定每次可向其发送组消息的最大收件人数。 默认值为&#x200B;*100*。

* **批量大小**

   发送到大量收件人组时要一起发送的消息数。 默认值为&#x200B;*100*。

* **附件总大小**

   如果选中supportAttachments，则此值指定所有附件所允许的最大总大小（以字节为单位）。 默认值为&#x200B;*104857600*(100 MB)。

* **附件类阻止列表型**

   文件阻止列表扩展名的，前缀为“**。**&#x200B;这将被制度拒绝。如果未列入阻止列表，则允许扩展。 可以使用“**+**”和“**-**”图标添加或删除扩展。

* **允许的附件类型**

   **(*需要操作*)** 文件扩允许列表展名的，与阻止列表相反。要允许除已外的所有文件扩展名列入阻止列表，请使用“**-**”图标删除单个空条目。

* **服务选择器**

   （*必需*）调用服务的绝对路径（端点）（虚拟资源）。 所选路径的根必须包含在OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)的&#x200B;*执行路径*&#x200B;配置设置中，如`/bin/`、`/apps/`和`/services/`。 要为站点的消息功能选择此配置，此端点将作为`Message List and Compose Message components`的&#x200B;**`Service selector`**&#x200B;值提供（请参阅[消息功能](/help/communities/configure-messaging.md)）。

   默认值为&#x200B;*/bin/messaging*。

* **字段允许列表**

   使用&#x200B;**消息字段允许列表**。

>[!CAUTION]
>
>每次打开`Messaging Operations Service`配置进行编辑时，如果`allowedAttachmentTypes.name`已被删除，则会重新添加一个空条目以使属性可配置。 单个空条目会有效禁用文件附件。
>
>若要允许除已的扩展名外的所有文件列入阻止列表名，请使用“**-**”图标（再次）删除单个空条目，然后单击&#x200B;**保存**。

## 组消息{#group-messaging}

要允许注册用户向用户组批量发送直接消息，请确保在以下两个&#x200B;**消息操作服务**&#x200B;配置实例中启用组消息&#x200B;**:**

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**消息操作服务：社交控制台**

![social-console-op-service](assets/social-console-op-service.png)

**消息操作服务：社交**

![社交消息服务](assets/social-message-op-service.png)

## 疑难解答 {#troubleshooting}

解决问题的一种方法是启用日志中的[调试消息。](/help/sites-administering/troubleshooting.md)

另请参阅[个人服务的记录器和写入器](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要监视的包为`com.adobe.cq.social.messaging`。
