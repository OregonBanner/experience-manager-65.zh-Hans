---
title: 配置电子邮件
seo-title: 配置电子邮件
description: 社区的电子邮件配置
seo-description: 社区的电子邮件配置
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
role: Administrator
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 4%

---

# 配置电子邮件{#configuring-email}

AEM Communities使用电子邮件：

* [社区通知](notifications.md)
* [Communities 订阅](subscriptions.md)

默认情况下，电子邮件功能无法正常使用，因为它需要指定SMTP服务器和SMTP用户。

>[!CAUTION]
>
>通知和订阅的电子邮件必须仅在[主发布者](deploy-communities.md#primary-publisher)上配置。

## 默认邮件服务配置{#default-mail-service-configuration}

通知和订阅均需要默认邮件服务。

* 使用管理员权限登录到主发布者，并访问[Web控制台](../../help/sites-deploying/configuring-osgi.md):

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`Day CQ Mail Service`。
* 选择编辑图标。

这基于[配置电子邮件通知](../../help/sites-administering/notification.md)的文档，但有一个不同之处，字段`"From" address`是&#x200B;*不是*&#x200B;必需的，应当留空。

例如（仅用于说明目的的值填充）：

![email-config](assets/email-config.png)

* **[!UICONTROL SMTP服务器主机名]**

   *（必需）* 要使用的SMTP服务器。

* **[!UICONTROL SMTP服务器端口]**

   *（必需）* SMTP服务器端口必须为25或更高。

* **[!UICONTROL SMTP用户]**

   *（必需）* SMTP用户。

* **[!UICONTROL SMTP密码]**

   *（必需）* SMTP用户的密码。

* **[!UICONTROL “发件人”地址]**

   留空
* **[!UICONTROL SMTP使用SSL]**

   如果选中，将发送安全电子邮件。 确保将端口设置为465或SMTP服务器所需的端口。
* **[!UICONTROL 调试电子邮件]**

   如果选中此项，则启用SMTP服务器交互的日志记录。

## AEM Communities电子邮件配置{#aem-communities-email-configuration}

配置[默认邮件服务](#default-mail-service-configuration)后，此版本中包含的`AEM Communities Email Reply Configuration` OSGi配置的两个现有实例即可正常运行。

在允许通过电子邮件回复时，只需进一步配置订阅的实例。

1. [](#configuration-for-notifications) 电子邮件实例：

   不支持回复电子邮件且不应更改的通知。

1. [订阅 — 电子邮](#configuration-for-subscriptions) 件实例：

   需要配置才能完全启用通过回复电子邮件创建帖子的功能。

要访问社区电子邮件配置实例，请执行以下操作：

* 使用管理员权限登录到主发布者，并访问[Web控制台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Email Reply Configuration`。

![email-reply-config](assets/email-reply-config.png)

### 通知配置{#configuration-for-notifications}

带有“名称”电子邮件的`AEM Communities Email Reply Configuration` OSGi配置的实例即为简化功能。 此功能不包括电子邮件回复。

不应更改此配置。

* 找到`AEM Communities Email Reply Configuration`。
* 选择编辑图标。
* 验证&#x200B;**名称**&#x200B;是`email`。

* 验证&#x200B;**通过回复创建帖子电子邮件**&#x200B;是否为`unchecked`。

![configure-email-reply](assets/configure-email-reply.png)

### 订阅配置{#configuration-for-subscriptions}

对于社区订阅，可以启用或禁用成员通过回复电子邮件来发布内容的功能。

* 找到`AEM Communities Email Reply Configuration`。
* 选择编辑图标。
* 验证&#x200B;**名称**&#x200B;是`subscriptions-email`。

   ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名称]**

   *（必需）* `subscriptions-email`。请勿编辑。

* **[!UICONTROL 通过回复电子邮件创建帖子]**

   如果选中，订阅电子邮件的收件人可以通过发送回复来发布内容。 默认选中。
* **[!UICONTROL 将跟踪的ID添加到标题]**

   默认值为`Reply-To`。

* **[!UICONTROL 最大主题长度]**

   如果将跟踪器ID添加到主题行，则这是主题的最大长度（不包括跟踪的ID），在此之后将会对其进行裁剪。 请注意，这应尽可能小，以避免跟踪的ID信息丢失。 默认值为200。

* **[!UICONTROL “回复”电子邮件地址]**

   用作“回复”电子邮件地址的地址。 默认值为`no-reply@example.com`。

* **[!UICONTROL 回复分隔符]**

   如果将跟踪器ID添加到回复标头，则将使用此分隔符。 默认值为`+`（加号）。

* **[!UICONTROL 主题中的跟踪器ID前缀]**

   如果将跟踪器ID添加到主题行，则将使用此前缀。 默认值为`post#`。

* **[!UICONTROL 消息正文中的跟踪器ID前缀]**

   如果将跟踪器ID添加到消息正文，则将使用此前缀。 默认值为`Please do not remove this:`。

* **[!UICONTROL 以HTML形式发送电子邮件]**:如果选中此项，则电子邮件的“内容类型”将设置为 `"text/html;charset=utf-8"`。默认选中。

* **[!UICONTROL 默认用户名]**

   此名称将不用于任何姓名用户。 默认值为`no-reply@example.com`。

* **[!UICONTROL 模板根路径]**

   电子邮件是使用该根路径中存储的模板生成的. 默认值为`/etc/community/templates/subscriptions-email`。

## 配置轮询导入程序{#configure-polling-importer}

要将电子邮件引入存储库，必须配置轮询导入器并在存储库中手动配置其属性。

### 添加新的轮询导入程序{#add-new-polling-importer}

* 使用管理员权限登录到主发布者，然后浏览到轮询导入器控制台：

   例如， [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 选择&#x200B;**[!UICONTROL Add]**

   ![轮询导入程序](assets/polling-importer.png)

* **[!UICONTROL 类型]**

   *（必需）* 下拉以选择 `POP3 (over SSL)`。

* **[!UICONTROL URL]**

   *（必需）* 出站邮件服务器。例如，`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`。

* **[!UICONTROL 导入到路径]**(&amp;A);

   *（必需）* 浏览到文 `/content/usergenerated/mailFolder/postEmails`
件夹并选择“确 `postEmails`定”以设 **置为**。

* **[!UICONTROL 以秒为单位的更新时间间隔]**

   *（可选）* 为默认邮件服务配置的邮件服务器可能需要更新时间间隔值。例如，Gmail可能要求间隔为`300`。

* **[!UICONTROL 登录]**

   *(可选)*

* **[!UICONTROL 密码]**

   *(可选)*

* 选择&#x200B;**[!UICONTROL 确定]**。

### 调整新轮询导入程序{#adjust-protocol-for-new-polling-importer}的协议

保存新的轮询配置后，需要进一步修改订阅电子邮件导入器的属性，以便将协议从`POP3`更改为`emailreply`。

使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 使用管理员权限登录到主发布者，然后浏览到[https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)。
* 选择新创建的配置并修改以下属性：

   * **feedType**:替换 `pop3s` 为  **`emailreply`**
   * **来源**:将源协议替换 `pop3s://` 为  **`emailreply://`**

![轮询协议](assets/polling-protocol.png)

红色三角形表示已修改的属性。 确保保存更改：

* 选择&#x200B;**[!UICONTROL 全部保存]**。
