---
title: 跟踪弹回的电子邮件
seo-title: 跟踪弹回的电子邮件
description: 您向多位用户发送新闻稿时，列表中通常会存在一些无效的电子邮件地址。发送到这些地址的新闻稿会弹回。AEM 能够管理这些弹回的邮件，并可在超出配置的弹回计数后停止向这些地址发送新闻稿。
seo-description: 您向多位用户发送新闻稿时，列表中通常会存在一些无效的电子邮件地址。发送到这些地址的新闻稿会弹回。AEM 能够管理这些弹回的邮件，并可在超出配置的弹回计数后停止向这些地址发送新闻稿。
uuid: 749959f2-e6f8-465f-9675-132464c65f11
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: fde9027b-9057-48c3-ae34-3f3258c5b371
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 跟踪弹回的电子邮件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe不计划进一步增强对AEM SMTP服务发送的已打开／弹回电子邮件的跟踪。
>
>建议利用Adobe [Campaign及其AEM集成](/help/sites-administering/campaign.md)。

您向多位用户发送新闻稿时，列表中通常会存在一些无效的电子邮件地址。发送到这些地址的新闻稿会弹回。AEM 能够管理这些弹回的邮件，并可在超出配置的弹回计数后停止向这些地址发送新闻稿。默认情况下，弹回率设置为 3，但您可对其进行配置。

要将 AEM 设置为跟踪弹回的电子邮件，您需要对 AEM 进行设置，使其对接收弹回电子邮件的现有邮箱（通常是您指定的从中发送新闻稿的“发件人”电子邮件地址）进行轮询。AEM 会对此收件箱进行轮询并会导入轮询配置中指定路径下的所有电子邮件。然后，将触发一个工作流以搜索用户内退回的电子邮件地址，并相应地更新用户的bounceCounter属性值。 超出配置的最大退回次数时，将会从 Newsletter 列表中删除该用户。

## 配置 Feed Importer {#configuring-the-feed-importer}

Feed Importer 允许您将外部源的内容多次导入到您的存储库中。使用 Feed Importer 的此配置，AEM 可检查发件人邮箱中的退回电子邮件。

对 Feed Importer 进行配置以跟踪退回电子邮件：

1. 在&#x200B;**工具**&#x200B;中，选择 Feed Importer。

1. 单击&#x200B;**添加**&#x200B;以创建新的配置。

   ![chlimage_1](assets/chlimage_1a.png)

1. 通过选择类型和向轮询 URL 添加信息来添加新的配置，以对主机和端口进行配置。此外，还需要对 URL 查询添加一些邮件和协议特定的参数。将配置设置为每天至少轮询一次。

   
在轮询 URL 中，所有配置都需要下列信息：

   `username`: 用于连接的用户名

   `password`: 用于连接的密码

   此外，您可以根据协议配置某些设置。

   **POP3 配置属性：**

   `pop3.leave.on.server`:定义是否将消息保留在服务器上。 设置为 true 会将邮件保留在服务器上，设置为 false 则不会保留。默认设置为 true。

   **POP3 示例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 使用 pop3 通过 SSL 以用户/密码方式连接到 GMail 端口 993 时，默认将消息保留在服务器上  |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP 配置属性：**

   允许您设置标记以供搜索。

   `imap.flag.SEEN`:将新的/未查看的消息设置为 false，将已读消息设置为 true

   See [https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html](https://java.sun.com/products/javamail/javadocs/javax/mail/Flags.Flag.html) for the full list of flags.

   **IMAP 示例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 使用 IMAP 通过 SSL 以用户/密码方式连接到 GMail 端口 993。默认只获取新消息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 使用 IMAP 通过 SSL 以用户/密码方式连接到 GMail 993 时，只会获取已查看的消息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 使用 IMAP 通过 SSL 以用户/密码方式连接到 GMail 993 时，会获取已读消息或新消息。 |

1. 保存配置。

## 配置 Newsletter 服务组件 {#configuring-the-newsletter-service-component}

配置 Feed Importer 后，您需要配置“发件人”地址和弹回计数器。

配置新闻稿服务：

1. 在OSGi控制台中， `<host>:<port>/system/console/configMgr` 并导航到 **MCM新闻稿**。

1. 配置服务并在结束时保存更改。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可对以下配置进行设置以调整行为：

   | 退回计数器最大值 (max.bounce.count) | 定义在发送 Newsletter 时用户被忽略前的退回次数。将此值设置为 0 可完全禁用退回检查。 |
   |---|---|
   | 活动无缓存 (sent.activity.nocache) | 定义用于 Newsletter 发送活动的缓存设置 |

   保存设置后，Newsletter MCM 服务可执行以下操作：

   * 成功发送新闻稿后向用户隐藏的流中写入活动。
   * 在检测到弹回以及用户弹回计数器发生更改时写入活动。
