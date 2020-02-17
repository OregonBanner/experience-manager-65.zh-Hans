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
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 配置电子邮件 {#configuring-email}

AEM Communities使用电子邮件

* [社区通知](notifications.md)
* [社区订阅](subscriptions.md)

默认情况下，电子邮件功能不起作用，因为它需要SMTP服务器和SMTP用户的规范。

>[!CAUTION]
>
>通知和订阅的电子邮件必须仅在主发布者 [上配置](deploy-communities.md#primary-publisher)。

## 默认邮件服务配置 {#default-mail-service-configuration}

通知和订阅均需要默认的邮件服务。

* 在主发行商上
* 以管理员权限登录
* 访问 [Web控制台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到 `Day CQ Mail Service`
* 选择编辑图标

这基于配置电子邮件通 [知的文档](../../help/sites-administering/notification.md)，但有一点不同，该字段不 `"From" address` 是必 *需的* ，应留空。

例如（仅为说明目的而填写值）:

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL SMTP服务器主机名]**:(必 *需)要使用的* SMTP服务器。

* **[!UICONTROL SMTP服务器端]** 口 *（必需）* SMTP服务器端口必须为25或更高。

* **[!UICONTROL SMTP用户]**:( *必需)* SMTP用户。

* **[!UICONTROL SMTP密码]**:(必 *需)* SMTP用户的口令。

* **[!UICONTROL “发件人”地址]**:留空
* **[!UICONTROL SMTP使用SSL]**:如果选中此项，将发送安全电子邮件。 确保端口设置为465或SMTP服务器需要。
* **[!UICONTROL 调试电子邮件]**:如果选中此项，则启用SMTP服务器交互的日志记录。

## AEM Communities电子邮件配置 {#aem-communities-email-configuration}

配置默 [认邮件服务后](#default-mail-service-configuration) ，发行版中包含的 `AEM Communities Email Reply Configuration` OSGi配置的两个现有实例即可正常工作。

允许通过电子邮件回复时，只需进一步配置订阅实例。

1. ` [email](#configuration-for-notifications)` 实例

   不支持回复电子邮件且不应更改的通知

1. ` [subscriptions-email](#configuration-for-subscriptions)` 实例

   需要配置以完全启用通过回复电子邮件创建帖子

要访问Communities电子邮件配置实例，请执行以下操作：

* 在主发行商上
* 以管理员权限登录
* 访问 [Web控制台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 定位 `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### 通知配置 {#configuration-for-notifications}

OSGi配置和 `AEM Communities Email Reply Configuration` 名称电子邮件的实例是即时功能。 此功能不包括电子邮件回复。

不应更改此配置。

* 找到 `AEM Communities Email Reply Configuration`
* 选择编辑图标
* 验证 **名称**`email`

* 验证 **通过回复电子邮件创建帖子**`unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### 订阅配置 {#configuration-for-subscriptions}

对于社区订阅，可以启用或禁用会员回复电子邮件以发布内容的功能。

* 找到 `AEM Communities Email Reply Configuration`
* 选择编辑图标
* 验证 **名称**`subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL 名称]** : *（必需）*`subscriptions-email`。 请勿编辑。

* **[!UICONTROL 通过回复电子邮件创建帖子]**:如果选中此项，订阅电子邮件的收件人可以通过发送回复来发布内容。 选中默认值。
* **[!UICONTROL 将跟踪ID添加到标题]**:默认值为 `Reply-To`。

* **[!UICONTROL 主题的最大长度]**:如果跟踪器ID添加到主题行，则这是主题的最大长度（不包括跟踪器ID），之后将裁切该主题。 请注意，这应尽可能小，以避免被跟踪的ID信息丢失。 默认值为200。
* **[!UICONTROL 电子邮件“发件人”地址]**:(必 *需)* ，通知电子邮件的发送地址。 可能为默认 **邮件服务指定** 的同 [一SMTP用户](#configuredefaultmailservice)。 Default is `no-reply@example.com`.

* **[!UICONTROL 答复分隔符]**:如果将跟踪器ID添加到回复标题，则将使用此分隔符。 默认为 `+` （加号）。

* **[!UICONTROL 主题中的跟踪器ID前缀]**:如果将跟踪器ID添加到主题行，则将使用此前缀。 Default is `post#`.

* **[!UICONTROL 消息正文中的跟踪器ID前缀]**:如果向消息正文添加了跟踪器ID，则将使用此前缀。 Default is `Please do not remove this:`.

* **[!UICONTROL 以HTML形式发送电子邮件]**:如果选中此项，则电子邮件的“内容类型”将设置为 `"text/html;charset=utf-8"`。 选中默认值。

* **[!UICONTROL 默认用户名]**:此名称将不用于姓名用户。 Default is `no-reply@example.com`.

* **[!UICONTROL 模板根路径]**:电子邮件是使用存储在此根路径中的模板构建的。 Default is `/etc/community/templates/subscriptions-email`.

## 配置轮询导入程序 {#configure-polling-importer}

要将电子邮件导入存储库，必须配置轮询导入程序并在存储库中手动配置其属性。

### 添加新轮询导入程序 {#add-new-polling-importer}

* 在主发行商上
* 以管理员权限登录
* 浏览至轮询导入程序控制台例如， [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)
* 选择添 **[!UICONTROL 加]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL 类型]**: *（必需）* ，下拉选择 `POP3 (over SSL).`

* **[!UICONTROL URL]**:(必 *需)* “出站邮件服务器”。 For example, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL 导入到Path]**&amp;ast;:(必 *需)* ，通过浏 `/content/usergenerated/mailFolder/postEmails`览到文件夹并选择“ `postEmails`确定”来设 **置**

* **[!UICONTROL 更新间隔（以秒为单位）]**:(可 *选)* ，为默认邮件服务配置的邮件服务器可能要求更新时间间隔值。 例如，Gmail可能需要间隔时间 `300`。

* **[!UICONTROL 登录]**: *（可选）*

* **[!UICONTROL 密码]**: *（可选）*

* 选择确 **[!UICONTROL 定]**

### 调整新轮询导入程序的协议 {#adjust-protocol-for-new-polling-importer}

保存新的轮询配置后，有必要进一步修改订阅电子邮件导入程序的属性，以便将协议从更改 `POP3` 为 `emailreply`

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 在主发行商上
* 以管理员权限登录
* 浏览 [至https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importers/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* 选择新创建的配置
* 修改以下属性

   * **feedType**:替换 `pop3s` 为 **`emailreply`**
   * **source**:将源协议替换 `pop3s://` 为 **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

红色三角形表示修改的属性。 请务必保存更改：

* 选择 **[!UICONTROL 全部保存]**

