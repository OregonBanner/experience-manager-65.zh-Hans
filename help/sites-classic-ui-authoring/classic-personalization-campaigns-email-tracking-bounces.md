---
title: 跟踪退回的电子邮件
description: 当您向许多用户发送新闻稿时，通常列表中会有一些无效的电子邮件地址。 向这些地址发送新闻稿会退回。 AEM可以管理这些退回，并可在超出配置的退回计数器后停止向这些地址发送新闻稿。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 6cda0a68-0df9-44e7-ae4f-9951411af6dd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 跟踪退回的电子邮件{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe不打算进一步增强对AEM SMTP服务发送的已打开/退回电子邮件的跟踪。
>
>建议是 [使用Adobe Campaign及其AEM集成](/help/sites-administering/campaign.md).

当您向许多用户发送新闻稿时，通常列表中会有一些无效的电子邮件地址。 向这些地址发送新闻稿会退回。 AEM可以管理这些退回，并可在超出配置的退回计数器后停止向这些地址发送新闻稿。 默认情况下，跳出率设置为3，但可配置。

要设置AEM以跟踪退回的电子邮件，请设置AEM以轮询接收退回电子邮件的现有邮箱。 通常，此位置是您指定新闻稿发送位置的“发件人”电子邮件地址。 AEM轮询此收件箱并导入轮询配置中指定的路径下的所有电子邮件。 然后，触发工作流以搜索用户内退回的电子邮件地址，并相应地更新用户的bounceCounter属性值。 超过配置的最大跳出次数后，将从新闻稿列表中删除该用户。

## 配置信息源导入程序 {#configuring-the-feed-importer}

信息源导入器允许您重复地将外部源中的内容导入存储库。 使用信息源导入程序的此配置，AEM会检查发件人的邮箱中是否有退回的电子邮件。

要配置馈送导入程序以跟踪退回的电子邮件，请执行以下操作：

1. 在 **工具**&#x200B;中，选择馈送导入程序。

1. 单击 **添加** 以创建配置。

   ![chlimage_1](assets/chlimage_1a.png)

1. 通过选择类型并向轮询URL添加信息以配置主机和端口，从而添加配置。 此外，还可以向URL查询添加一些特定于邮件和协议的参数。 将配置设置为每天至少轮询一次。

   所有配置都需要有关轮询URL中以下内容的信息：

   `username`：用于连接的用户名

   `password`：用于连接的密码

   此外，根据协议，您可以配置某些设置。

   **POP3配置属性：**

   `pop3.leave.on.server`：定义是否在服务器上保留消息。 设置为true会在服务器上保留消息，否则为false。 默认为true。

   **POP3示例：**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | 使用pop3 over SSL以用户/密码连接到端口995上的GMail，默认情况下在服务器上保留消息 |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **IMAP配置属性：**

   允许您设置要搜索的标志。

   `imap.flag.SEEN`：对于新/未查看的消息，设置为false；对于已读取的消息，设置为true

   请参阅 [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) 以获取完整的标志列表。

   **IMAP示例：**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | 使用IMAP over SSL通过用户/密码连接到端口993上的GMail。 默认情况下仅获取新消息。 |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | 使用IMAP over SSL连接到带有用户/密码的GMail 993，只看到消息。 |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | 使用IMAP over SSL连接到带有用户/密码的GMail 993，已读取消息或新消息。 |

1. 保存配置。

## 配置Newsletter服务组件 {#configuring-the-newsletter-service-component}

配置馈送导入程序后，请配置发件人地址和退回计数器。

要配置新闻稿服务，请执行以下操作：

1. 在OSGi控制台中，位于 `<host>:<port>/system/console/configMgr`，导航到 **MCM新闻稿**.

1. 配置服务并在完成后保存更改。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   可以设置以下配置来调整行为：

   | 退回计数器最大值(max.bounce.count) | 定义在发送新闻稿时忽略用户之前的退回次数。 将此值设置为0将完全禁用退回检查。 |
   |---|---|
   | 活动无缓存(sent.activity.nocache) | 定义用于新闻稿发送活动的缓存设置 |

   保存后，新闻稿MCM服务会执行以下操作：

   * 在成功发送新闻稿时将活动写入用户隐藏的流。
   * 如果检测到跳出并且用户跳出计数器发生更改，则写入活动。
