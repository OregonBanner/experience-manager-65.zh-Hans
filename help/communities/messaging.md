---
title: 配置消息传送
description: 了解AEM Communities中的消息传送功能，该功能为登录网站访客（成员）提供相互发送消息的功能。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# 配置消息传送 {#configure-messaging}

## 概述 {#overview}

AEM Communities的消息传送功能允许登录的网站访客（成员）向彼此发送登录网站时可访问的消息。

通过在社区站点启用消息传送期间选中相应复选框， [社区站点创建](/help/communities/sites-console.md).

本页包含有关默认配置和可能调整的信息。

有关开发人员的更多信息，请参阅 [消息传送要点](/help/communities/essentials-messaging.md).

## 消息传送操作服务 {#messaging-operations-service}

配置 [AEM Communities消息传送操作服务](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) 标识处理消息相关请求的端点、服务应用于存储消息的文件夹，以及如果消息可能包含文件附件，则允许的文件类型。

对于使用创建的社区站点 `Communities Sites console`，则该服务的实例已存在，且收件箱设置为 `/mail/inbox`.

### 社区消息传送运营服务 {#community-messaging-operations-service}

如下所示，使用创建的站点存在服务的配置 [站点创建向导](/help/communities/sites-console.md). 通过选择配置旁边的铅笔图标，可以查看或编辑配置。

![消息传送 — 操作](assets/messaging-operations.png)

### 添加新的配置 {#add-new-configuration}

要添加配置，请选择加号&#39;**+**&#39;服务名称旁边的图标：

* **列入允许列表消息字段**

  指定用户可以编辑并保留的撰写消息组件的属性。 如果添加了新表单元素，则必须添加元素ID（如果需要）以存储在SRP中。 默认值为两个条目： *主题* 和 *内容*.

* **消息框大小限制**

  每个用户的消息框中的最大字节数。 默认为 *1073741824* (1 GB)。

* **消息计数限制**

  每个用户允许的消息总数。 值为–1表示允许消息数量不受限制，但受消息框大小限制。 默认为 *10000* (10k)。

* **通知投放失败**

  如果选中此选项，则在邮件发送给某些收件人失败时通知发件人。 默认为 *已选中*.

* **失败投放发件人ID**

  投放失败消息中显示的发件人名称。 默认为 *failureNotifier*.

* **失败消息模板路径**

  投放失败消息模板根目录的绝对路径。 默认为 */etc/notification/messaging/default*.

* **重试次数**

  尝试重新发送无法传递的消息的次数。 默认为 *3*.

* **重试之间等待**

  发送失败时尝试重新发送消息之间等待的秒数。 默认为 *100* （秒）。

* **更新池大小计数**

  用于计数更新的并发线程数。 默认为 *10*.

* **收件箱路径**

  (*必填*)相对于用户节点的路径(/home/users/*用户名*)，以用于 `inbox` 文件夹。 路径不能以尾随正斜杠“/”结尾。 默认为 */mail/inbox*.

* **已发送项目路径**

  (*必填*)相对于用户节点的路径(/home/users/*用户名*)，以用于 `sent items` 文件夹。 路径不能以尾随正斜杠“/”结尾。 默认为 */mail/sentitems* .

* **支持附件**

  如果选中，用户将能够向其邮件添加附件。 默认为 *已选中*.

* **启用组消息传递**

  如果选定此选项，则注册的用户可以向一组成员发送批量消息。 默认为 *已取消选择*.

* **最大数量 收件人总数**

  如果启用了组消息，请指定一次可向其发送组消息的最大收件人数。 默认为 *100*.

* **批量大小**

  发送给大量收件人时要批处理在一起进行发送的消息数。 默认为 *100*.

* **附件总大小**

  如果选中supportAttachments ，此值指定所有附件允许的最大总大小（字节）。 默认为 *104857600* (100 MB)。

* **列入阻止列表附件类型**

  文件扩展名阻止列表，以“**.**&#39;，系统拒绝该选项。 如果未列入阻止列表，则允许扩展。 可以使用“**+**&#39;和&#39;**-**&#39;图标。

* **允许的附件类型**

  **(*需要操作*)** 文件扩展名的允许列表 列入阻止列表，与相反。 要允许除列入阻止列表文件以外的所有文件扩展名，请使用&#39;**-**&#39;图标以删除单个空条目。

* **服务选择器**

  (*必填*)用于调用服务的绝对路径（端点）（虚拟资源）。 所选路径的根必须包含在 *执行路径* OSGi配置的配置设置 [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)，例如 `/bin/`， `/apps/`、和 `/services/`. 要为站点的消息传送功能选择此配置，提供此端点作为 **`Service selector`** 的值 `Message List and Compose Message components` (请参阅 [消息功能](/help/communities/configure-messaging.md))。

  默认为 */bin/messaging* .

* **字段允许列表**

  使用 **列入允许列表消息字段**.

>[!CAUTION]
>
>每次 `Messaging Operations Service` 如果符合以下条件，将打开配置进行编辑 `allowedAttachmentTypes.name` ，则会读取一个空条目，以便对属性进行配置。 单个空条目会有效地禁用文件附件。
>
>要允许除列入阻止列表文件以外的所有文件扩展名，请使用&#39;**-**&#39;图标，以在（再次）单击之前删除单个空条目 **保存**.

## 组消息 {#group-messaging}

要允许注册用户将私信批量发送到用户组，请确保 **启用组消息传递** 在以下两个实例中 **消息传送操作服务** 配置：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**消息传送操作服务：社交控制台**

![social-console-op-service](assets/social-console-op-service.png)

**消息传送操作服务：社交消息**

![social-message-op-service](assets/social-message-op-service.png)

## 疑难解答 {#troubleshooting}

解决问题的一种方法是启用 [调试日志中的消息。](/help/sites-administering/troubleshooting.md)

另请参阅 [适用于单个服务的记录器和写入程序](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

要监视的包为 `com.adobe.cq.social.messaging`.
