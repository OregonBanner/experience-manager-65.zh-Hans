---
title: 配置消息传送
seo-title: 配置消息传送
description: 社区消息传送
seo-description: 社区消息传送
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---

# 配置消息传送 {#configure-messaging}

## 概述 {#overview}

AEM Communities的消息传送功能允许已登录的网站访客（成员）相互发送消息，这些消息在登录到网站后即可访问。

在[社区站点创建](/help/communities/sites-console.md)期间选中框，可为社区站点启用消息传送。

此页面包含有关默认配置和可能调整的信息。

有关开发人员的其他信息，请参阅[Messaging Essentials](/help/communities/essentials-messaging.md)。

## 报文传送操作服务 {#messaging-operations-service}

配置[AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)标识处理与消息相关请求的端点、服务应用于存储消息的文件夹，以及如果消息可能包含文件附件，则允许使用哪些文件类型。

对于使用`Communities Sites console`创建的社区站点，服务的实例已存在，收件箱设置为`/mail/inbox`。

### Community Messaging Operations Service {#community-messaging-operations-service}

如下所示，对于使用[站点创建向导](/help/communities/sites-console.md)创建的站点，该服务的配置存在。 通过选择配置旁边的铅笔图标，可以查看或编辑配置。

![报文传送操作](assets/messaging-operations.png)

### 添加新的配置 {#add-new-configuration}

要添加新配置，请选择服务名称旁边的加号“**+**”图标：

* **消息字段允许列表**

   指定用户可以编辑和保留的撰写消息组件的属性。 如果添加了新表单元素，则需要添加元素ID（如果需要）才能将其存储在SRP中。 默认为两个条目：*subject*&#x200B;和&#x200B;*content*。

* **消息框大小限制**

   每个用户消息框中的最大字节数。 默认值为&#x200B;*1073741824*(1 GB)。

* **消息计数限制**

   每个用户允许的消息总数。 值为–1表示允许无限数量的消息，但须符合消息框大小限制。 默认值为&#x200B;*10000*(10k)。

* **通知投放失败**

   如果选中此选项，则在向某些收件人发送消息失败时通知发件人。 默认值为&#x200B;*checked*。

* **投放发件人ID失败**

   发送失败消息中显示的发送者名称。 默认值为&#x200B;*failureNotifier*。

* **失败消息模板路径**

   投放失败消息模板根的绝对路径。 默认值为&#x200B;*/etc/notification/messaging/default*。

* **重试次数**

   尝试重新发送消息失败的次数。 默认值为&#x200B;*3*。

* **在重试之间等待**

   尝试在发送失败时重新发送消息之间等待的秒数。 默认值为&#x200B;*100*（秒）。

* **计数更新池大小**

   用于计数更新的并发线程数。 默认值为&#x200B;*10*。

* **收件箱路径**

   （*必需*）相对于用户节点(/home/users/*username*)的用于`inbox`文件夹的路径。 路径不得以尾随正斜杠“/”结尾。 默认值为&#x200B;*/mail/inbox*。

* **已发送项目路径**

   （*必需*）相对于用户节点(/home/users/*username*)的用于`sent items`文件夹的路径。 路径不得以尾随正斜杠“/”结尾。 默认值为&#x200B;*/mail/sentitems* 。

* **支持附件**

   如果选中，则用户能够在其邮件中添加附件。 默认值为&#x200B;*checked*。

* **启用组消息传送**

   如果选中，则注册用户可以向一组成员发送批量消息。 默认值为&#x200B;*deselected*。

* **最大值否。总收件人**

   如果启用了组消息传送，请指定一次可发送到组消息的收件人最大数。 默认值为&#x200B;*100*。

* **批量大小**

   发送到大量收件人时要批量发送的消息数。 默认值为&#x200B;*100*。

* **附件总大小**

   如果选中了supportAttachments，则此值指定所有附件允许的最大总大小（以字节为单位）。 默认值为&#x200B;*104857600*(100 MB)。

* **附件类型阻止列表**

   文件扩展名阻止列表的，前缀为“**”。**&#39;，系统将拒绝该请求。如果未列入阻止列表，则允许使用扩展。 可以使用“**+**”和“**-**”图标添加或删除扩展。

* **允许的附件类型**

   **(*需要操作*)** 文件扩展名允许列表的，与的对阻止列表面。要允许所有文件扩展名(列入阻止列表的扩展名除外)，请使用“**-**”图标删除单个空条目。

* **服务选择器**

   （*必需*）用于调用服务的绝对路径（端点）（虚拟资源）。 所选路径的根必须包含在OSGi配置[ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)的&#x200B;*执行路径*&#x200B;配置设置中，例如`/bin/`、`/apps/`和`/services/`。 要为站点的消息传送功能选择此配置，此端点将作为`Message List and Compose Message components`的&#x200B;**`Service selector`**&#x200B;值提供（请参阅[消息功能](/help/communities/configure-messaging.md)）。

   默认值为&#x200B;*/bin/messaging* 。

* **字段允许列表**

   使用&#x200B;**消息字段允许列表**。

>[!CAUTION]
>
>每次打开`Messaging Operations Service`配置进行编辑时，如果删除了`allowedAttachmentTypes.name`，则会重新添加一个空条目，以便对属性进行配置。 单个空条目会有效地禁用文件附件。
>
>要允许所有文件扩展名(列入阻止列表的扩展名除外)，请使用“**-**”图标（再次）在单击&#x200B;**Save**&#x200B;之前删除单个空条目。

## 群组消息传送 {#group-messaging}

要允许注册用户批量向用户组发送私信，请确保在以下两个&#x200B;**Messaging Operation Services**&#x200B;配置实例中启用组消息传送&#x200B;**:**

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**报文传送操作服务：社交控制台**

![social-console-op-service](assets/social-console-op-service.png)

**报文传送操作服务：社交消息**

![社交消息业务](assets/social-message-op-service.png)

## 疑难解答 {#troubleshooting}

解决问题的一种方法是在日志中启用[调试消息。](/help/sites-administering/troubleshooting.md)

另请参阅[个人服务的记录器和写入器](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要监视的包为`com.adobe.cq.social.messaging`。
