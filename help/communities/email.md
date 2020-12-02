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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 4%

---


# 配置电子邮件{#configuring-email}

AEM Communities使用电子邮件：

* [社区通知](notifications.md)
* [社区订阅](subscriptions.md)

默认情况下，电子邮件功能不起作用，因为它需要SMTP服务器和SMTP用户的规范。

>[!CAUTION]
>
>通知和订阅的电子邮件只能在[主发布者](deploy-communities.md#primary-publisher)上配置。

## 默认邮件服务配置{#default-mail-service-configuration}

通知和订阅均需要默认邮件服务。

* 使用管理员权限登录到主发布者并访问[Web控制台](../../help/sites-deploying/configuring-osgi.md):

   * 例如，[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`Day CQ Mail Service`。
* 选择编辑图标。

这基于[配置电子邮件通知](../../help/sites-administering/notification.md)的文档，但有区别的是，字段`"From" address`是&#x200B;*不是必需的*，应留空。

例如（仅为说明目的而填写值）:

![email-config](assets/email-config.png)

* **[!UICONTROL SMTP服务器主机名]**

   *（必需）* 要使用的SMTP服务器。

* **[!UICONTROL SMTP服务器端口]**

   *（必需）* SMTP服务器端口必须为25或更高。

* **[!UICONTROL SMTP用户]**

   *（必需）* SMTP用户。

* **[!UICONTROL SMTP口令]**

   *（必需）* SMTP用户的口令。

* **[!UICONTROL “发件人”地址]**

   留空
* **[!UICONTROL SMTP使用SSL]**

   如果选中，将发送安全电子邮件。 确保端口设置为465或SMTP服务器需要。
* **[!UICONTROL 调试电子邮件]**

   如果选中，则启用SMTP服务器交互的日志记录。

## AEM Communities电子邮件配置{#aem-communities-email-configuration}

配置[默认邮件服务](#default-mail-service-configuration)后，发行版中包含的`AEM Communities Email Reply Configuration` OSGi配置的两个现有实例将开始工作。

允许通过电子邮件回复时，只需进一步配置订阅的实例。

1. [电](#configuration-for-notifications) 子邮件实例：

   对于不支持回复电子邮件的通知，不应更改。

1. [订阅-](#configuration-for-subscriptions) emailinstance:

   需要配置才能完全启用通过回复电子邮件创建帖子。

要访问Communities电子邮件配置实例：

* 使用管理员权限登录到主发布者并访问[Web控制台](../../help/sites-deploying/configuring-osgi.md)

   * 例如，[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Email Reply Configuration`。

![email-reply-config](assets/email-reply-config.png)

### 通知配置{#configuration-for-notifications}

`AEM Communities Email Reply Configuration` OSGi config和“名称”电子邮件的实例是即时功能。 此功能不包括电子邮件回复。

不应更改此配置。

* 找到`AEM Communities Email Reply Configuration`。
* 选择编辑图标。
* 验证&#x200B;**名称**&#x200B;是否为`email`。

* 验证&#x200B;**从回复电子邮件创建帖子**&#x200B;是否为`unchecked`。

![configure-email-reply](assets/configure-email-reply.png)

### 订阅{#configuration-for-subscriptions}的配置

对于社区订阅，可以启用或禁用成员通过回复电子邮件来发布内容的功能。

* 找到`AEM Communities Email Reply Configuration`。
* 选择编辑图标。
* 验证&#x200B;**名称**&#x200B;是否为`subscriptions-email`。

   ![configure-email-订阅](assets/configure-email-subscriptions.png)

* **[!UICONTROL 名称]**

   *（必需）* `subscriptions-email`。请勿编辑。

* **[!UICONTROL 通过回复电子邮件创建帖子]**

   如果选中，订阅电子邮件的收件人可以通过发送回复来发布内容。 选中默认值。
* **[!UICONTROL 将跟踪ID添加到标题]**

   默认值为`Reply-To`。

* **[!UICONTROL 最大主题长度]**

   如果跟踪器ID添加到主题行，则这是主题的最大长度（不包括跟踪的ID），之后将裁切它。 请注意，这应尽可能小，以避免跟踪的ID信息丢失。 默认值为200。

* **[!UICONTROL “回复”电子邮件地址]**

   用作“回复”电子邮件地址的地址。 默认值为`no-reply@example.com`。

* **[!UICONTROL 答复分隔符]**

   如果将跟踪器ID添加到回复标题，则将使用此分隔符。 默认值为`+`（加号）。

* **[!UICONTROL 主题中的跟踪器ID前缀]**

   如果跟踪器ID添加到主题行，则将使用此前缀。 默认值为`post#`。

* **[!UICONTROL 消息正文中的跟踪器ID前缀]**

   如果跟踪器ID添加到消息正文，则将使用此前缀。 默认值为`Please do not remove this:`。

* **[!UICONTROL 以HTML形式发送电子邮件]**:如果选中，则电子邮件的“内容类型”将设置为 `"text/html;charset=utf-8"`。选中默认值。

* **[!UICONTROL 默认用户名]**

   此名称将不用于姓名用户。 默认值为`no-reply@example.com`。

* **[!UICONTROL 模板根路径]**

   电子邮件是使用该根路径中存储的模板生成的. 默认值为`/etc/community/templates/subscriptions-email`。

## 配置轮询导入程序{#configure-polling-importer}

要将电子邮件导入存储库，必须配置轮询导入程序并手动在存储库中配置其属性。

### 添加新轮询导入程序{#add-new-polling-importer}

* 使用管理员权限登录到主发布者并浏览至轮询导入程序控制台：

   例如，[http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* 选择&#x200B;**[!UICONTROL 添加]**

   ![轮询导入程序](assets/polling-importer.png)

* **[!UICONTROL 类型]**

   *（必需）* 下拉选择 `POP3 (over SSL)`。

* **[!UICONTROL URL]**

   *（必需）* 出站邮件服务器。例如，`pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`。

* **[!UICONTROL 导入到路径]**(&amp;A);

   *（必需）通* 过浏 `/content/usergenerated/mailFolder/postEmails`
览到文件夹并选 `postEmails`择“确 **定”**。

* **[!UICONTROL 以秒为单位的更新时间间隔]**

   *（可选）* 为默认邮件服务配置的邮件服务器可能要求更新时间间隔值。例如，Gmail可能需要`300`的间隔。

* **[!UICONTROL 登录]**

   *(可选)*

* **[!UICONTROL 密码]**

   *(可选)*

* 选择&#x200B;**[!UICONTROL 确定]**。

### 调整新轮询导入程序{#adjust-protocol-for-new-polling-importer}的协议

保存新的轮询配置后，必须进一步修改订阅电子邮件导入程序的属性，以便将协议从`POP3`更改为`emailreply`。

使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 使用管理员权限登录到主发布者，并浏览至[https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)。
* 选择新创建的配置并修改以下属性：

   * **feedType**:替换 `pop3s` 为  **`emailreply`**
   * **源**:将源协议替换 `pop3s://` 为  **`emailreply://`**

![轮询协议](assets/polling-protocol.png)

红色三角形表示修改的属性。 请确保保存更改：

* 选择&#x200B;**[!UICONTROL 全部保存]**。

