---
title: 配置电子邮件通知
seo-title: Configuring Email Notification
description: 了解如何在AEM中配置电子邮件通知。
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: 93dfac20bbb761abd580a004741ade20dc4ee2fe
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 12%

---


# 配置电子邮件通知{#configuring-email-notification}

AEM会向符合以下条件的用户发送电子邮件通知：

* 已订阅页面事件，例如修改或复制。 此 [通知收件箱](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications) 部分介绍了如何订阅此类事件。

* 已订阅论坛事件。
* 必须在工作流中执行步骤。 此 [参与者步骤](/help/sites-developing/workflows-step-ref.md#participant-step) 部分介绍了如何在工作流中触发电子邮件通知。

先决条件：

* 用户需要在其个人资料中定义有效的电子邮件地址。
* 此 **Day CQ邮件服务** 需要正确配置。

当用户收到通知时，他将会收到其用户档案中定义的语言版本的电子邮件。 每种语言都有其自己的可自定义模板。 可以为新语言添加新电子邮件模板。

>[!NOTE]
>
>使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 了解更多详细信息和建议的做法。

## 配置邮件服务 {#configuring-the-mail-service}

为了让AEM能够发送电子邮件， **Day CQ邮件服务** 需要正确配置。 您可以在Web控制台中查看配置。 使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 了解更多详细信息和建议的做法。

以下约束适用：

* 此 **SMTP服务器端口** 必须为25或更高。

* 此 **SMTP服务器主机名** 不得为空。
* 此 **“寄件者”地址** 不得为空。

为了帮助您调试的问题 **Day CQ邮件服务**，您可以查看服务的日志：

`com.day.cq.mailer.DefaultMailService`

该配置在Web控制台中如下所示：

![Day CQ Mail Service OSGi配置窗口](assets/chlimage_1-276.png)

## 配置电子邮件通知渠道 {#configuring-the-email-notification-channel}

当您订阅页面或论坛事件通知时，发件人电子邮件地址设置为 `no-reply@acme.com` 默认。 您可以通过配置 **通知电子邮件渠道** Web控制台中的服务。

要配置发件人电子邮件地址，请添加 `sling:OsgiConfig` 节点到存储库。 请按下列步骤使用CRXDE Lite直接添加节点：

1. 在CRXDE Lite中，添加名为的文件夹 `config` 位于应用程序文件夹下方。
1. 在配置文件夹中，添加一个名为的节点：

   `com.day.cq.wcm.notification.email.impl.EmailChannel` 类型 `sling:OsgiConfig`

1. 添加 `String` 属性到名为的节点 `email.from`. 对于值，指定要使用的电子邮件地址。

1. 单击 **全部保存**.

请按下列步骤在内容包源文件夹中定义节点：

1. 在您的 `jcr_root/apps/*app_name*/config folder`，创建一个名为的文件 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

1. 添加以下XML以表示节点：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 替换 `email.from` 属性( `name@server.com`)。

1. 保存文件。

## 配置工作流电子邮件通知服务 {#configuring-the-workflow-email-notification-service}

当您收到工作流电子邮件通知时，发件人电子邮件地址和主机URL前缀都会设置为默认值。 您可以通过配置 **Day CQ工作流电子邮件通知服务** 在Web控制台中。 如果这样做，建议将更改保留在存储库中。

在Web控制台中，默认配置如下所示：

![Day CQ工作流电子邮件通知服务配置窗口](assets/chlimage_1-277.png)

### 页面通知的电子邮件模板 {#email-templates-for-page-notification}

页面通知的电子邮件模板位于下方：

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

默认英语模板( `en.txt`)的定义如下：

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

#### 自定义页面通知的电子邮件模板 {#customizing-email-templates-for-page-notification}

要自定义页面通知的英语电子邮件模板，请执行以下操作：

1. 在CRXDE中，打开文件：

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. 根据需要修改文件。
1. 保存更改。

模板需要具有以下格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

位置 &lt;text_x> 可以是静态文本和动态字符串变量的组合。 以下变量可在电子邮件模板中用于页面通知：

* `${time}`，即事件日期和时间。

* `${userFullName}`，触发事件的用户的全名。

* `${userId}`，触发事件的用户的ID。
* `${modifications}`，采用以下格式描述页面事件的类型和页面路径：

  &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

  例如：

  PageModified => /content/geometrixx/en/products

### 工作流通知的电子邮件模板 {#email-templates-for-workflow-notification}

工作流通知的电子邮件模板（英语）位于：

`/libs/settings/workflow/notification/email/default/en.txt`

其定义如下：

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

#### 自定义工作流通知的电子邮件模板 {#customizing-email-templates-for-workflow-notification}

自定义工作流事件通知的英语电子邮件模板：

1. 在CRXDE中，打开文件：

   `/libs/settings/workflow/notification/email/default/en.txt`

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
>位置 `<text_x>` 可以是静态文本和动态字符串变量的组合。 每行 `<text_x>` 项必须以反斜杠( `\`)，但最后一个实例除外，当反斜杠的缺失指示结束时， `<text_x>` 字符串变量。
>
>有关模板格式的更多信息，请参阅 [Properties.load()的javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) 方法。

方法 `${payload.path.open}` 显示工作项的有效负荷的路径。 例如，对于Sites中的页面，则 `payload.path.open` 将类似于 `/bin/wcmcommand?cmd=open&path=…`.；这没有服务器名称，因此模板会在它前面加上 `${host.prefix}`.

以下变量可在电子邮件模板中使用：

* `${event.EventType}`，事件的类型
* `${event.TimeStamp}`，事件的日期和时间
* `${event.User}`，触发事件的用户
* `${initiator.home}`，启动器节点路径

* `${initiator.name}`，启动器名称

* `${initiator.email}`，发起人的电子邮件地址
* `${item.id}`，工作项的id
* `${item.node.id}`，与此工作项关联的工作流模型中的节点的id
* `${item.node.title}`，工作项的标题
* `${participant.email}`，参与者的电子邮件地址
* `${participant.name}`，参与者的姓名
* `${participant.familyName}`，参与者的姓氏
* `${participant.id}`，参与者的id
* `${participant.language}`，参与者语言
* `${instance.id}`，工作流id
* `${instance.state}`，工作流状态
* `${model.title}`，工作流模型的标题
* `${model.id}`，工作流模型的id

* `${model.version}`，工作流模型的版本
* `${payload.data}`，有效负载

* `${payload.type}`，有效负载类型
* `${payload.path}`，有效负载的路径
* `${host.prefix}`，主机前缀，例如： `http://localhost:4502`

### 添加新语言的电子邮件模板 {#adding-an-email-template-for-a-new-language}

要为新语言添加模板，请执行以下操作：

1. 在CRXDE中，添加文件 `<language-code>.txt` 下：

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` ：用于页面通知
   * `/libs/settings/workflow/notification/email/default` ：用于工作流通知

1. 使文件适应语言。
1. 保存更改。

>[!NOTE]
>
>此 `<language-code>` 用作电子邮件模板的文件名需要是AEM可识别的双字母小写语言代码。 对于语言代码，AEM依赖于ISO-639-1。

## 配置AEM Assets电子邮件通知 {#assetsconfig}

在共享或取消共享AEM Assets中的收藏集时，用户可以从AEM接收电子邮件通知。 要配置电子邮件通知，请执行以下步骤。

1. 配置电子邮件服务，如中所述 [配置邮件服务](/help/sites-administering/notification.md#configuring-the-mail-service).
1. 以管理员身份登录 AEM。单击 **工具** >  **操作** >  **Web控制台** 打开Web控制台配置。
1. 编辑 **Day CQ DAM资源收集Servlet**. 选择 **发送电子邮件**. 单击“**保存**”。

## 设置OAuth {#setting-up-oauth}

AEM为其集成的邮件程序服务提供OAuth2支持，以允许组织遵守安全电子邮件要求。

您可以为多个电子邮件提供商配置OAuth，如下所述。

>[!NOTE]
>
>此过程是Publish实例的示例。 如果您希望在“作者”实例上启用电子邮件通知，则需要在“作者”上执行相同的步骤。

### Gmail {#gmail}

1. 创建项目于 `https://console.developers.google.com/projectcreate`
1. 选择您的项目，然后转到 **API和服务** - **仪表板 — 凭据**
1. 根据您的要求配置OAuth同意屏幕
1. 在随后的“更新屏幕”中，添加以下两个范围：
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 添加范围后，请返回 **凭据** ，然后转到 **创建凭据** - **OAuth客户端ID** - **桌面应用程序**
1. 此时将打开一个包含客户端ID和客户端密钥的新窗口。
1. 保存这些凭据。

**AEM端配置**

>[!NOTE]
>
>Adobe托管服务客户可以与其客户服务工程师合作，对生产环境进行这些更改。

首先，配置邮件服务：

1. 打开AEM Web Console，方法是转到 `http://serveraddress:serverport/system/console/configMgr`
1. 查找，然后单击 **Day CQ邮件服务**
1. 添加以下设置：
   * SMTP 服务器主机名: `smtp.gmail.com`
   * SMTP服务器端口： `25` 或 `587`，具体取决于要求
   * 勾选选选框 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * Check **OAuth流** 并单击 **保存**.

接下来，按照以下过程配置您的SMTP OAuth提供程序：

1. 打开AEM Web Console，方法是转到 `http://serveraddress:serverport/system/console/configMgr`
1. 查找，然后单击 **CQ邮件程序SMTP OAuth2提供程序**
1. 按如下方式填写所需信息：
   * 授权URL： `https://accounts.google.com/o/oauth2/auth`
   * 令牌URL： `https://accounts.google.com/o/oauth2/token`
   * 范围： `https://www.googleapis.com/auth/gmail.send` 和 `https://mail.google.com/`. 您可以通过按 **+** 按钮以打开每个已配置作用域的右侧。
   * 客户端ID和客户端密钥：使用如上段所述检索到的值配置这些字段。
   * 刷新令牌 URL: `https://accounts.google.com/o/oauth2/token`
   * 刷新令牌过期：从不
1. 单击“**保存**”。

<!-- clarify refresh token expiry, currently not present in the UI -->

配置完毕后，设置应如下所示：

![CQ邮件程序SMTP Oauth2提供程序配置窗口](assets/oauth-smtpprov2.png)

现在，激活OAuth组件。 您可以执行以下操作来实现此目标：

1. 访问以下URL以转到组件控制台： `http://serveraddress:serverport/system/console/components`
1. 查找以下组件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按组件左侧的播放图标

   ![显示OAuthCodeGenerateServlet和OAuthCodeAccessTokenGenerator的组件列表](assets/oauth-components-play.png)

最后，通过以下方式确认配置：

1. 转到发布实例的地址，并以管理员身份登录。
1. 在浏览器中打开新选项卡，然后转到 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 这会将您重定向到SMTP提供商的页面，在本例中为Gmail。
1. 登录并同意授予所需权限
1. 同意后，令牌将存储在存储库中。 您可以在以下位置访问它： `accessToken` 通过在发布实例上直接访问此URL： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 对每个发布实例重复以上步骤

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. 转至 [https://portal.azure.com/](https://portal.azure.com/) 并登录。
1. 在搜索栏中搜索 **Azure Active Directory**，并单击搜索结果。或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击&#x200B;**应用程序注册** - **新注册**

   ![配置Microsoft Outlook时的“新建注册”按钮](assets/oauth-outlook1.png)

1. 根据您的要求填写信息，然后单击&#x200B;**注册**
1. 转至新创建的应用程序，并选择 **API 权限**
1. 转至&#x200B;**添加权限** - **图表权限** - **委派权限**
1. 为应用程序选择以下权限，然后单击&#x200B;**添加权限**：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 转到 **身份验证** - **添加平台** - **Web**、和中的 **重定向Url** 部分，添加以下URL以重定向OAuth代码，然后按 **配置**：
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 对每个发布实例重复以上步骤
1. 根据您的要求配置设置
1. 接下来，转至&#x200B;**证书和密码**，单击&#x200B;**新建客户端密码**，然后执行屏幕上显示的步骤来创建密码。请务必记下此密码供以后使用
1. 按左窗格中的&#x200B;**概述**，复制&#x200B;**应用程序（客户端）ID** 和&#x200B;**目录（租户）ID** 的值供以后使用

回顾一下，您需要以下信息为AEM端的邮件程序服务配置OAuth2：

* 将使用租户 ID 构建的身份验证 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 将使用租户 ID 构建的令牌 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 将使用租户 ID 构建的刷新 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 客户端 ID
* 客户端密码

**AEM端配置**

接下来，将您的OAuth2设置与AEM集成：

1. 通过浏览到转到本地实例的Web控制台 `http://serveraddress:serverport/system/console/configMgr`
1. 查找并单击 **Day CQ邮件服务**
1. 添加以下设置：
   * SMTP 服务器主机名: `smtp.office365.com`
   * SMTP用户：您的用户名（电子邮件格式）
   * “发件人”地址：邮件程序发送消息的“发件人：”字段中使用的电子邮件地址
   * SMTP服务器端口： `25` 或 `587` 根据要求
   * 勾选选选框 **SMPT使用StarTLS** 和 **SMTP需要StarTLS**
   * Check **OAuth流** 并单击 **保存**.
1. 查找，然后单击 **CQ邮件程序SMTP OAuth2提供程序**
1. 按如下方式填写所需信息：
   * 通过按照中的说明构造授权URL、令牌URL和刷新令牌URL，以填写它们 [此过程的结束](#microsoft-outlook)
   * 客户端ID和客户端密钥：使用如上所述检索的值配置这些字段。
   * 将以下范围添加到配置：
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode重定向Url： `http://localhost:4503/services/mailer/oauth2/token`
   * 刷新令牌URL：此值应与上面的令牌URL的值相同
1. 单击“**保存**”。

配置完毕后，设置应如下所示：

![已完成的CQ邮件程序SMTP OAuth2配置](assets/oauth-outlook-smptconfig.png)

现在，激活OAuth组件。 您可以执行以下操作来实现此目标：

1. 访问以下URL以转到组件控制台： `http://serveraddress:serverport/system/console/components`
1. 查找以下组件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按组件左侧的播放图标

![包含OAuthCodeGenerateServlet和OAuthCodeAccessTokenGenerator的组件列表的片段](assets/oauth-components-play.png)

最后，通过以下方式确认配置：

1. 转到发布实例的地址，并以管理员身份登录。
1. 在浏览器中打开新选项卡，然后转到 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. 这会将您重定向到SMTP提供商的页面，在本例中为Outlook。
1. 登录并同意授予所需权限
1. 同意后，令牌将存储在存储库中。 您可以在以下位置访问它： `accessToken` 通过在发布实例上直接访问此URL： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
