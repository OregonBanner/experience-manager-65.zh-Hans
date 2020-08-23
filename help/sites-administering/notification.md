---
title: 配置电子邮件通知
seo-title: 配置电子邮件通知
description: 了解如何在AEM中配置电子邮件通知。
seo-description: 了解如何在AEM中配置电子邮件通知。
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 1%

---


# 配置电子邮件通知{#configuring-email-notification}

AEM向用户发送电子邮件通知：

* 已订阅页面事件，例如修改或复制。 “通 [知收件箱](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) ”部分介绍如何订阅此类事件。

* 已订阅论坛事件。
* 必须在工作流中执行一个步骤。 参加 [者步骤](/help/sites-developing/workflows-step-ref.md#participant-step) (Participant Step)部分介绍如何在工作流中触发电子邮件通知。

先决条件：

* 用户需要在其用户档案中定义有效的电子邮件地址。
* 需 **要正确配置Day** CQ Mail Service。

当用户收到通知时，他会收到一封电子邮件，其语言在用户档案中定义。 每种语言都有其自己的可自定义的模板。 可以为新语言添加新的电子邮件模板。

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## 配置邮件服务 {#configuring-the-mail-service}

要使AEM能够发送电子邮件， **Day CQ邮件服务** 需要正确配置。 您可以在Web控制台中视图配置。 When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

以下约束适用：

* SMTP服 **务器端口** 必须为25或更高。

* SMTP服 **务器主机名** 不能为空。
* “ **发件人”地址** 不得为空。

为了帮助您调试Day CQ邮 **件服务的问题**，您可以观看服务的日志：

`com.day.cq.mailer.DefaultMailService`

配置在Web控制台中如下所示：

![chlimage_1-276](assets/chlimage_1-276.png)

## 配置电子邮件通知渠道 {#configuring-the-email-notification-channel}

当您订阅页面或论坛事件通知时，默认情况下会将发件人电子邮件地址设 `no-reply@acme.com` 置为。 您可以通过在Web控制台中配 **置通知电子邮件渠道** ，来更改此值。

要配置发件人电子邮件地址，请向存储 `sling:OsgiConfig` 库添加节点。 请按照以下过程，直接使用CRXDE Lite添加节点：

1. 在CRXDE Lite中，在应用程序文件夹下 `config` 添加一个名为的文件夹。
1. 在config文件夹中，添加一个名为：

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 类型 `sling:OsgiConfig`

1. 向名 `String` 为的节点添加属性 `email.from`。 对于该值，指定要使用的电子邮件地址。

1. 单击“ **全部保存**”。

请按照以下过程定义内容包源文件夹中的节点：

1. 在您的 `jcr_root/apps/*app_name*/config folder`文件中，创建一个名为 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 添加以下XML以表示节点：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 将属性()的 `email.from` 值替换 `name@server.com`为您的电子邮件地址。

1. 保存文件。

## 配置工作流电子邮件通知服务 {#configuring-the-workflow-email-notification-service}

当您收到工作流电子邮件通知时，发件人电子邮件地址和主机URL前缀均设置为默认值。 您可以通过在Web控制台中配 **置Day CQ Workflow电子邮件通知服** 务来更改这些值。 如果这样做，建议保留存储库中的更改。

默认配置在Web控制台中如下所示：

![chlimage_1-277](assets/chlimage_1-277.png)

### 页面通知的电子邮件模板 {#email-templates-for-page-notification}

页面通知的电子邮件模板位于以下位置：

`/etc/notification/email/default/com.day.cq.wcm.core.page`

默认的英语模 `en.txt`板()定义如下：

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 为页面通知自定义电子邮件模板 {#customizing-email-templates-for-page-notification}

为页面通知自定义英语电子邮件模板：

1. 在CRXDE中，打开文件：

   `/etc/notification/email/default/com.day.cq.wcm.core.page/en.txt`

1. 根据需要修改文件。
1. 保存更改。

模板需要具有以下格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中，&lt;text_x>可以是静态文本和动态字符串变量的混合。 以下变量可在页面通知的电子邮件模板中使用：

* `${time}`、事件日期和时间。

* `${userFullName}`，触发事件的用户的全名。

* `${userId}`，触发事件的用户的ID。
* `${modifications}`，以以下格式描述页面事件类型和页面路径：

   &lt;page事件类型> => &lt;page path>

   例如：

   PageModified => /content/geometrixx/cn/products

### 论坛通知的电子邮件模板 {#email-templates-for-forum-notification}

论坛通知的电子邮件模板位于：

`/etc/notification/email/default/com.day.cq.collab.forum`

默认的英语模 `en.txt`板()定义如下：

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 为论坛通知自定义电子邮件模板 {#customizing-email-templates-for-forum-notification}

要自定义论坛通知的英语电子邮件模板，请执行以下操作：

1. 在CRXDE中，打开文件：

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. 根据需要修改文件。
1. 保存更改。

模板需要具有以下格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中 `<text_x>` 可以是静态文本和动态字符串变量的混合。

以下变量可在论坛通知的电子邮件模板中使用：

* `${time}`、事件日期和时间。

* `${forum.path}`, the path to the forum page.

### 工作流通知的电子邮件模板 {#email-templates-for-workflow-notification}

工作流通知的电子邮件模板（英语）位于：

`/etc/workflow/notification/email/default/en.txt`

定义如下：

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 为工作流通知自定义电子邮件模板 {#customizing-email-templates-for-workflow-notification}

要自定义工作流事件通知的英语电子邮件模板，请执行以下操作：

1. 在CRXDE中，打开文件：

   `/etc/workflow/notification/email/default/en.txt`

1. 根据需要修改文件。
1. 保存更改。

模板需要具有以下格式：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>其中 `<text_x>` 可以是静态文本和动态字符串变量的混合。 项目的每行 `<text_x>` 都需要用反斜杠( `\`)结束，但最后一个实例除外，因为缺少反斜杠表示字符串变量 `<text_x>` 的结尾。
>
>有关模板格式的更多信息，请 [参阅Properties.load()方法的javadocs](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 。

该方法 `${payload.path.open}` 显示工作项的有效负荷路径。 例如，对于站点中的页面， `payload.path.open` 则类似于 `/bin/wcmcommand?cmd=open&path=…`。;这没有服务器名称，因此模板会优先使用它 `${host.prefix}`

可以在电子邮件模板中使用以下变量：

* `${event.EventType}`，类型事件
* `${event.TimeStamp}`、事件日期和时间
* `${event.User}`，触发事件的用户
* `${initiator.home}`，启动器节点路径

* `${initiator.name}`，启动器名称

* `${initiator.email}`，启动器的电子邮件地址
* `${item.id}`，工作项的id
* `${item.node.id}`，与此工作项关联的工作流模型中节点的id
* `${item.node.title}`，工作项的标题
* `${participant.email}`，参加者的电子邮件地址
* `${participant.name}`、参加者姓名
* `${participant.familyName}`，参加者的姓氏
* `${participant.id}`，参加者的id
* `${participant.language}`，参加者语言
* `${instance.id}`, workflow id
* `${instance.state}`, the workflow state
* `${model.title}`，工作流模型的标题
* `${model.id}`，工作流模型的id

* `${model.version}`，工作流模型的版本
* `${payload.data}`、有效负荷

* `${payload.type}`、有效负荷类型
* `${payload.path}`，有效负荷的路径
* `${host.prefix}`，主机前缀，例如：http://localhost:4502

### 为新语言添加电子邮件模板 {#adding-an-email-template-for-a-new-language}

为新语言添加模板：

1. 在CRXDE中，添加以下文 `<language-code>.txt` 件：

   * `/etc/notification/email/default/com.day.cq.wcm.core.page` :适用于页面通知
   * `/etc/notification/email/default/com.day.cq.collab.forum` :论坛通知
   * `/etc/workflow/notification/email/default` :工作流通知

1. 使文件适应语言。
1. 保存更改。

>[!NOTE]
>
>用 `<language-code>` 作电子邮件模板文件名的代码必须是由AEM识别的小写字母语言代码。 对于语言代码，AEM依赖于ISO-639-1。

## 配置AEM Assets电子邮件通知 {#assetsconfig}

当AEM Assets的集合被共享或取消共享时，用户可以收到AEM发送的电子邮件通知。 要配置电子邮件通知，请按照以下步骤操作。

1. 按照配置邮件服务中的上述 [说明配置电子邮件服务](/help/sites-administering/notification.md#configuring-the-mail-service)。
1. 以管理员身份登录AEM。 单击 **工具** >操 **作** > Web **控制台** ，打开Web控制台配置。
1. 编辑 **Day CQ DAM资源集合Servlet**。 选择“ **发送电子邮件**”。 单击&#x200B;**保存**。

