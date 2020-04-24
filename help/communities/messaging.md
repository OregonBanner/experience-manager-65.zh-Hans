---
title: 配置消息传递
seo-title: 配置消息传递
description: 社区消息
seo-description: 社区消息
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# 配置消息传递 {#configure-messaging}

## 概述 {#overview}

AEM Communities的消息传递功能允许登录站点访客（成员）相互发送消息，这些消息在登录站点时可访问。

通过在社区站点创建过程中选中一个框，为社区站点启 [用消息传递](/help/communities/sites-console.md)。

此页包含有关默认配置和可能调整的信息。

有关开发人员的其他信息，请参 [阅Messaging Essentials](/help/communities/essentials-messaging.md)。

## Messaging Operations Service {#messaging-operations-service}

配置 [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) (AEM Communities Messaging Operations Service)可标识处理消息相关请求的端点、服务应用于存储消息的文件夹，以及如果消息可能包括文件附件，则允许使用哪些文件类型。

对于使用创建的社区站 `Communities Sites console`点，服务的一个实例已存在，收件箱设置为 `/mail/inbox`。

### 社区消息处理运营服务 {#community-messaging-operations-service}

如下所示，对于使用站点创建向导创建的站点，存在服 [务的配置](/help/communities/sites-console.md)。 通过选择配置旁的铅笔图标，可以查看或编辑配置。

![消息——操作](assets/messaging-operations.png)

### 添加新的配置 {#add-new-configuration}

要添加新配置，请选择服务名称旁的加号“**+**”图标：

* **消息字段白名单**

   指定用户可以编辑和保留的合成消息组件的属性。 如果添加了新的表单元素，则需要添加元素ID（如果需要）才能存储在SRP中。 默认为两个条目：主 *题**和内容*。

* **消息框大小限制**

   每个用户消息框中的最大字节数。 默认为 *1073741824* (1 GB)。

* **消息计数限制**

   每个用户允许的消息总数。 值为-1表示允许不限数量的消息，但须遵守消息框大小限制。 默认为 *10000* (10k)。

* **通知投放失败**

   如果选中此项，则在消息投放未能到达某些收件人时通知发送方。 默认为选 *中*。

* **失败投放发送方ID**

   发送者的名称，其显示在投放失败消息中。 默认值为 *failureNotifier*。

* **失败消息模板路径**

   投放失败的消息模板根的绝对路径。 默认值为 */etc/notification/messaging/default*。

* **重试**

   尝试重新发送未能传送的消息的次数。 Default is *3*.

* **在重试之间等待**

   在发送失败时尝试重新发送消息之间等待的秒数。 默认为 *100* （秒）。

* **计数更新池大小**

   用于计数更新的并发线程数。 Default is *10*.

* **收件箱路径**

   (必&#x200B;*需*)用于文件夹的路径，相对于用户的节点(/home/users/*username*) **`inbox`** 。 路径不能以尾随正斜杠&#39;/&#39;结束。 默认为 */mail/inbox*。

* **已发送项目路径**

   (必&#x200B;*需*)用于文件夹的路径，相对于用户的节点(/home/users/*username*) **`send items`** 。 路径不能以尾随正斜杠&#39;/&#39;结束。 默认为 */mail/sentitems* 。

* **支持附件**

   如果选中此项，则用户可以向其邮件中添加附件。 默认为选 *中*。

* **启用组消息传递**

   如果选择此项，则注册用户可以向一组成员发送批量消息。 取消选择 *默认值*。

* **最大值。 总收件人**

   如果启用了组消息传递，请指定每次可向其发送组消息的最大收件人数。 Default is *100*.

* **批量大小**

   发送到大量收件人时要一起发送的消息数。 Default is *100*.

* **附件总大小**

   如果选中supportAttachments，则此值指定所有附件所允许的最大总大小（以字节为单位）。 默认 *为104857600* (100 MB)。

* **附着式黑色列表**

   文件扩展名的黑名单，前缀为“”**。**&#x200B;被制度拒绝。 如果不已列入黑名单，则允许扩展。 可以使用“**+**”和“**-**”图标添加或删除扩展。

* **允许的附件类型**

   **(需&#x200B;*要操作*** )文件扩展名的白名单，与黑名单相反。 要允许除那些已列入黑名单外的所有文件扩展名，请使用“**-**”图标删除单个空条目。

* **服务选择器**

   (*必需*)调用服务的绝对路径（端点）（虚拟资源）。 所选路径的根必须是OSGi配置的“执行路径 *”配置设置中的一个* , [ 如、 `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)和 `/bin/``/apps/``/services/`。 要为站点的消息功能选择此配置，此端点将作为站点的 **`Service selector`** 值提供 `Message List and Compose Message components` (请参阅 [消息功能](/help/communities/configure-messaging.md))。

   默认值为 */bin/messaging* 。

* **字段白名单**

   使用 **消息字段白名单**。

>[!CAUTION]
>
>每次打开配 `Messaging Operations Service` 置进行编辑时，如果已删 `allowedAttachmentTypes.name` 除，则会重新添加一个空条目以使属性可配置。 单个空条目会有效禁用文件附件。
>
>要允许除那些已列入黑名单之外的所有文件扩展名，请在单击“保存”之前（再次）使用“**-**”图标删除单个空条目 ****。


## Group Messaging {#group-messaging}

要允许注册用户向用户组批量发送直接消息，请确保在以下两个 **Messaging Operation Services配置实例中启用组消** 息传递 **** :

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**消息传递操作服务：社交控制台**

![social-console-op-service](assets/social-console-op-service.png)

**消息传递操作服务：社交消息**

![社交消息服务](assets/social-message-op-service.png)

## 疑难解答 {#troubleshooting}

解决问题的一种方法是启用日 [志中的调试消息。](/help/sites-administering/troubleshooting.md)

另请参 [阅个人服务的记录者和作者](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)。

要监控的包装是 `com.adobe.cq.social.messaging`。
