---
title: 推送通知
seo-title: 推送通知
description: 可查看本页以了解如何在AEM mobile应用程序中使用推送通知。
seo-description: 可查看本页以了解如何在AEM mobile应用程序中使用推送通知。
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 推送通知{#push-notifications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

能否立即向AEM mobile应用程序用户发送重要通知对移动应用程序及其营销活动的价值至关重要。 在此，我们将介绍允许应用程序接收推送通知所需执行的步骤，以及如何配置推送并将推送从AEM mobile发送到电话上安装的应用程序。 此外，本节还介绍如何配置推送通 [知的“深层链接](#deeplinking) ”功能。

>[!NOTE]
>
>*推送通知不保证交付；它们更像是公告。 尽最大努力确保每个人都能收到它们，但它们不是保证的交付机制。 此外，推送推送的时间可能从不到1秒到长达半小时不等。*

将推送通知与AEM结合使用需要一些不同的技术。 首先，必须使用推送通知服务提供商来管理通知和设备（AEM尚未这样做）。 两个提供者在AEM中现成配置：Amazon [Simple Notification Service](https://aws.amazon.com/sns/) （或SNS）和 [Pushwoosh](https://www.pushwoosh.com/)。 其次，针对给定移动操作系统的推送技术必须通过相应的服务— 适用于iOS设备的Apple推送通知服务（或APNS）;和Google Cloud Messaging（或GCM），用于Android设备。 尽管AEM不直接与这些平台特定服务通信，但AEM必须提供一些相关配置信息以及通知，这些服务才能执行推送。

安装和配置（如下所述）后，其工作方式如下：

1. 在AEM中创建推送通知，并将其发送给服务提供商（Amazon SNS或Pushwoosh）。
1. 服务提供商接收并将其发送到核心提供商（APNS或GCM）。
1. 核心提供者将通知推送到为该推送注册的所有设备。 对于每个设备，它使用蜂窝数据网络或WiFi（以设备上当前可用者为准）。
1. 如果注册的应用程序未运行，则通知将显示在设备上。 点击通知的用户将启动应用程序并在应用程序内显示通知。 如果应用程序已在运行，则只显示应用程序内通知。

此版本的AEM支持iOS和Android移动设备。

## 概述和过程 {#overview-and-procedure}

要在AEM mobile应用程序中使用推送通知，必须执行以下高级步骤。

通常，AEM开发人员将：

1. 注册Apple和Google消息服务
1. 使用推送消息服务注册并配置它
1. 向应用程序添加推送支持
1. 准备电话以进行测试

而AEM管理员将：

1. 在AEM应用程序上配置推送
1. 构建和部署应用程序
1. 发送推送通知
1. 配置深层链 *接（可选）*

### 第1步：注册Apple和Google消息服务 {#step-register-with-apple-and-google-messaging-services}

#### 使用Apple推送通知服务(APNS) {#using-the-apple-push-notification-service-apns}

转到此处的Apple [页面](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) ，熟悉Apple推送通知服务。

要使用APNS，您需要 **Apple提供的证书文件** （.cer文件）、推送私钥（.p12文件）和 **私钥密码****** 。 有关如何执行此操作的说明，请在此 [处找到](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html)。

#### 使用Google Cloud Messaging(GCM)服务 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google正在用一项名为Firebase Cloud Messaging(FCM)的类似服务取代GCM。 有关FCM的详细信息，请单 [击此处](https://developers.google.com/cloud-messaging/faq)。

转到此处的Google页 [面](https://developer.android.com/google/gcm/index.html) ，熟悉适用于Android的Google Cloud Messaging。

您需要按照以下步骤 [创建](https://developer.android.com/google/gcm/gs.html)**Google API项目**, **启用GCM服务**, ****&#x200B;并获取API密钥Accept。 您需要 **API密钥** ，才能将推送通知发送到Android设备。 另外，请记 **录项目编号**，该编号有时也称为 **GCM发送者Id**。

以下步骤显示了创建GCM API密钥的不同方法：

1. 登录google并转到 [Google的“开发人员”页面](https://developers.google.com/mobile/add?platform=android&cntapi=gcm)。
1. 从列表中选择您的应用程序（或创建新应用程序）。
1. 在“Android包名称”下，输入您的应用程序ID，即 `com.adobe.cq.mobile.weretail.outdoorsapp`. （如果这不起作用，请使用“test.test”重试。）
1. 单击 **继续以选择和配置服务**
1. 选择“云消息传递”，然后单击“ **启用Google云消息传递”**。
1. 随后将显示新的服务器API密钥和（新的或现有的）发送者ID。

>[!NOTE]
>
>记录服务器API密钥。 该值是在您的推送提供者的站点上输入的。

### 第2步：注册和配置推送消息服务 {#step-register-and-configure-a-push-messaging-service}

AEM配置为将三种服务之一用于推送通知：

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*Amazon SNS* 和 ** Pushwoosh配置允许您从AEM屏幕中发送推送的内容。

*Adobe Mobile Services* 配置允许您使用Adobe Analytics帐户在Adobe Mobile services中配置和发送推送通知（但需要使用此配置集构建应用程序以启用AMS推送通知）。

#### 使用Amazon SNS消息传递服务 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*有关Amazon SNS的信息以及用于创建新AWS帐户的链接，请访[问](https://aws.amazon.com/sns/)。 你可以免费获得一年的帐户。*

如果您不想使用Amazon SNS，可以跳过这些步骤。

请按照以下步骤为推送通知设置Amazon SNS:

1. **向Amazon SNS注册**

   1. 记录您的帐户ID。 格式应为12位数，不带空格或短划线，即《123456789012》。
   1. 确保您位于“美国东部”或“欧盟”地区，因为后续步骤（创建身份池）需要其中一个步骤。
   1. 注册后，登录管理控制台并选择 [SNS](https://console.aws.amazon.com/sns/) （推送通知服务）。 如果显示“开始”，请单击它。

1. **创建访问密钥和ID**

   1. 单击屏幕右上角的登录名，然后从菜单中选择“安全凭据”。
   1. 单击“访问密钥”，然后在下面的空格中，单击“创建 **新访问密钥”**。
   1. 单击 **显示访问密钥**，然后复制并保存显示的访问密钥ID和机密访问密钥。 如果选择下载键的选项，您将获得包含这些相同值的csv文件。
   1. 可在此页上管理其他安全相关证书和其他证书。
   >[!NOTE]
   >
   >访问密钥可用于多个应用程序。

   对于使用“AWS沙箱”帐户的组织，这些步骤非常相似，并在此列出：

   1. 单击屏幕右上角的登录名，然后从菜单中选择“我的安全凭据”。
   1. 单击操作左侧列表中的“用户”，然后选择您的用户名。
   1. 单击“安全凭据”选项卡。
   1. 从此处，您会看到您的密钥并创建新密钥。 保存密钥供以后使用。


1. **创建主题**

   1. 单击 **创建主题** ，然后选择主题名称。 记录所有字段，如“主题ARN”、“主题所有者”、“区域”、“显示名称”。
   1. 单击“ **其他主题操作** ”>“ **编辑主题策略”**。 在“ **允许这些用户订阅此主题”下**，选择“所 **有人”。**
   1. 单击 **更新策略**。
   >[!NOTE]
   >
   >您可以针对开发、测试、演示等不同场景创建多个主题。 其余的SNS配置可以保持不变。 使用不同的主题构建应用程序；发送到该主题的推送通知将仅由使用该主题构建的应用程序接收。

1. **创建平台应用程序**

   1. 单击“应用程序”，然后单击“创建平台应用程序”。 选择一个名称并选择一个平台(APNS for iOS, GCM for Android)。 根据平台的不同，其他字段需要填写：

      1. 对于APNS，必须输入P12文件、密码、证书和私钥。 应已在上述步骤使用Apple *推送通知服务(APNS)中获取这些通知* 。
      1. 对于GCM，必须输入API密钥。 这应该已在上述使用Google Cloud Messaging(GCM) *服务步骤中获得* 。
   1. 对要支持的每个平台重复上述步骤一次。 要同时推送到iOS和Android，必须创建两个平台应用程序。


1. **创建标识池**

   1. 使用 [Cognito](https://console.aws.amazon.com/cognito) 创建标识池，该池将存储未经身份验证的用户的基本数据。 请注意，目前只有“美国东部”和“欧盟”地区受Amazon Cognito支持。
   1. 为其命名，并选中“启用对未验证身份的访问”框。
   1. 在下一页(“您的&#x200B;*Cognito身份需要访问您的资源*”)，单击“允许”。
   1. 在页面的右上角，单击链接“编辑标&#x200B;*识池”*。 此时将显示标识池ID。 保存此文本以供以后使用。
   1. 在同一页面上，选择“未验证角色”旁边的下拉框，确保其已选中Cognito_&lt;池名称>UnauthRole角色。 保存更改。

1. **配置访问权限**

   1. 登录 [Identity and Access Management](https://console.aws.amazon.com/iam/home) (IAM)
   1. 选择角色
   1. 单击在上一步中创建的角色，称为Cognito_&lt;yourIdentityPoolName>Unauth_Role。 记录显示的“角色ARN”。
   1. 打开“内联策略”（如果尚未打开）。 您应当看到一个名称类似oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123的策略。
   1. 单击“编辑策略”。 将策略文档的内容替换为以下JSON片段：
   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> “版本”:《2012-10-17》,</p> <p> "语句": [</p> <p> {</p> <p> "操作": [</p> <p> "mobileanalytics:PutEvents",</p> <p> “cognito sync:*”,</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS：订阅"</p> <p> ],</p> <p> “效果”:“允许”,</p> <p> "资源": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. 单击“应 **用策略”**


#### 使用Pushwoosh消息传递服务 {#using-the-pushwoosh-messaging-service}

如果您不想使用Pushwoosh，可以跳过此步骤。

要使用Pushwoosh，请执行以下操作：

1. **使用Pushwoosh注册**

   1. 转到pushwoosh.com并创建新帐户。

1. **创建API访问令牌**

   1. 在Pushwoosh站点上，转到“API访问”菜单项以生成API访问令牌。 您需要安全地记录此信息。

1. **创建新应用程序**

   1. 要获得Android支持，您需要提供GCM API密钥。
   1. 配置应用程序时，选择Cordova作为框架。
   1. 要获得iOS支持，您需要提供证书文件(.cer)、推送证书(.p12)和私钥密码；这些应该是从苹果的APNS网站上获得的。 对于“框架”，选择“Cordova”。
   1. Pushwoosh将为该应用程序生成一个App Id，格式为“XXXXX-XXXXX”，其中每个X都是一个十六进制值（0到F）。

>[!NOTE]
>
>*如果在AEM中配置了另一个应用程序，且该应用程序具有相同的App Id（和其他相关值）:API访问令牌和GCM ID)，通过AEM上的第二个应用程序发送的任何推送通知都将转到具有该App id的任何其他应用程序。*

### 第3步：向应用程序添加推送支持 {#step-add-push-support-to-the-app}

#### 添加ContentSync配置 {#add-contentsync-configuration}

创建两个名为notificationsConfig的内容节点（一个在app-config中，一个在app-config-dev中）:

* /content/`<your app>`/shell/jcr:content/pge-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/pge-app/app-config/notificationsConfig

对于这些属性（.content.xml文件）:&lt;jcr:root xmlns:jcr=&quot; [https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot;jcr:primaryType=&quot;nt:unstructured&quot;excludeProperties=&quot;[appAPIAccessToken]&quot;path=&quot;。./../..&quot;
targetRootDirectory=&quot;www&quot;type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>内容同步处理函数会查找这些节点，如果它们不在该节点处，它不会写出pge-notifications-config.json文件。

#### 添加客户端库 {#add-client-libraries}

必须按照以下步骤将推送通知客户端库添加到应用程序：

在CRXDE Lite中：

1. 导航到 */etc/designs/phonegap/&lt;app name>/clientlibsall。*
1. 双击属性窗格中的嵌入部分。
1. 在出现的对话框中，单击+按钮添加新的客户端库。
1. 在新文本字段中，添加“cq.mobile.push”，然后单击“确定”。
1. 再添加一个名为cq.mobile.push.amazon的应用程序，然后单击“确定”。
1. 保存更改。

>[!NOTE]
>
>如果出于应用程序上的空间注意事项而删除或不使用推送通知，并且要避免出现控制台错误消息，请从应用程序中删除这些clientlib。

### 第4步：准备电话以进行测试 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*对于推送通知，您需要在实际设备上进行测试，因为模拟器无法接收推送通知。*

#### IOS {#ios}

对于iOS，您需要使用Mac OS计算机，并且您需要加入 [iOS开发人员计划](https://developer.apple.com/programs/ios/)。 某些公司拥有公司许可证，所有开发人员都可以使用这些许可证。

对于XCode 8.1，在使用推送通知之前，您必须转到项目的“功能”选项卡，然后切换“推送通知”切换为“打开”。

#### Android {#android}

要使用CLI在Android手机上安装应用程序，请执行以下操作：第 **6步——构建和部署应用程序**)，您首先必须将电话置于“开发人员模式”。 有关 [执行此操作的详细信息，请参阅启用设备上开发人员选项](https://developer.android.com/tools/device.html#developer-device-options) 。

### 第5步：在AEM应用程序上配置推送 {#step-configure-push-on-aem-apps}

在构建并部署到已配置的移动设备之前，您必须为您决定使用的消息服务配置通知设置。

1. 为推送通知创建适当的授权组。
1. 以相应用户身份登录AEM，单击“应用程序”选项卡。
1. 单击应用程序。
1. 查找“管理云服务”拼贴并单击铅笔以修改您的云配置。
1. 选择Amazon SNS Connection、Pushwoosh Connection或Adobe Mobile services作为通知配置。
1. 输入提供者属性，然后单击提交以保存它们，然后单击完成。 除了AMS外，在此阶段不进行远程验证。
1. 您现在应该可以看到您刚刚在“管理云服务”拼贴中输入的配置。

### 第6步：构建和部署应用程序 {#step-build-and-deploy-the-app}

**** 注意：另请参阅此处有关构建PhoneGap [应用程序](/help/mobile/building-app-mobile-phonegap.md) 的说明。

使用PhoneGap构建和部署应用程序有两种方法。

**** 注意：对于推送通知测试，模拟器无法满足要求，因为推送通知在推送提供者（Apple或Google）和设备之间使用不同的协议。 当前的Mac/PC硬件和模拟器不支持此功能。

1. *PhoneGap Build是PhoneGap提供的一项服务* ，它将在您的服务器上为您构建应用程序，并允许您直接将其下载到设备。 请参阅 [PhoneGap build文档](https://build.phonegap.com/) ，了解如何设置和使用PhoneGap Build。

1. *PhoneGap命令行界面* (CLI)允许您在命令行中使用丰富的PhoneGap命令集来构建、调试和部署应用程序。 请参阅 [PhoneGap开发人员文档](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) ，了解如何设置和使用PhoneGap CLI。

### 第7步：发送推送通知 {#step-send-a-push-notification}

要创建新通知并发送，请按照以下步骤操作。

1. 创建新通知

   * 在AEM mobile应用程序的功能板中，查找推送通知拼贴。
   * 在右上角的菜单中，选择“创建”。 请注意，此按钮在云配置首次设置之前不可用。
   * 在创建通知向导中，输入标题和消息，然后单击“创建”按钮。 您的通知现在可以立即发送或稍后发送。 可以编辑消息和／或标题，并更改和保存标题。

1. 发送通知

   * 在“应用程序”功能板中，找到“推送通知”拼贴。
   * 选择通知，或单击右下角的详细信息按钮(...)以显示通知列表。 此列表还指示通知是否已准备好发送、是否已发送，或是否在发送过程中出错。
   * 选中一个通知（仅）的复选框，然后单击列表上方的“发送通知”按钮。 您将有一次机会在出现的对话框中“取消”或“发送”通知。

1. 处理结果

   * 如果推送通知服务（Amazon SNS或Pushwoosh）收到发送请求，确认其有效，并将其成功发送到本机提供者（APNS和GCM），则“发送”对话框将关闭，不显示任何消息。 在通知列表中，该通知的状态将列为“已发送”。
   * 如果推送发送失败，对话框将显示一条消息，指明问题。 在通知列表中，该通知的状态将列为“错误”，但如果问题得到纠正，则可以再次发送通知。 发生错误时，服务器错误日志中应显示其他错误信息。
   * 请注意，iOS和Android推送通知之间存在一些平台差异。 其中包括：

      * 使用CLI构建应用程序将在应用程序部署到Android上后启动。 在iOS上，必须手动启动它。 由于推送注册步骤在启动时执行，因此Android应用程序可以立即接收推送通知（因为它将启动并注册），而iOS应用程序则不会。
      * 在Android上，“确定”按钮文本为全部大写（以及在应用程序内通知上添加的任何其他按钮中），而在iOS中则不是。

对于AMS推送通知，必须从AMS服务器编写和发送通知。 AMS提供的推送通知功能超出了AEM通知与AWS和Pushwoosh提供的功能。

>[!NOTE]
>
>*推送通知不保证交付；它们更像是公告。 尽最大努力确保每个人都听到这一消息，但它们不是保证的交付机制。 此外，推送推送的时间可能从不到1秒到长达半小时不等。*

### 配置带推送通知的深层链接 {#configuring-deep-linking-with-push-notifications}

什么是深层链接？ 在推送通知的上下文中，这是一种允许将应用程序打开或定向到应用程序内指定位置的方法（如果打开）。

它是如何工作的？ 推送通知的作者可以选择添加按钮标签(即“给我看看！”)通知，并通过可视路径浏览器选择要在通知中链接的页面。 发送后，推送将正常进行，但应用程序内消息中的“确定”按钮将替换为“取消”按钮，并指定新按钮（“显示我！”）的双曲余切值。 单击新按钮将使应用程序转到应用程序中的指定页面。 单击“取消”将只关闭消息。

如果应用程序未打开，则阴影将显示为正常。 对底纹中的通知执行操作将打开应用程序，然后根据推送通知中配置的内容向用户显示深层链接按钮。

创建通知，为可选深层链接添加按钮文本和链接路径：

>[!CAUTION]
>
>.要访问功能板中的推送通知拼贴，请执行以下步骤。

1. 单击“管理云服务”拼贴右上角 **的编辑** 。

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 选择“ **Pushwoosh连接”**。 单击&#x200B;**下一步**。

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. 输入属性的详细信息，然后单击“提 **交”**。

   ![chlimage_1-110](assets/chlimage_1-110.png)

   提交配置后，功能板中 **会显示推送通知** 拼贴。

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 创建通知向导 {#create-notification-wizard}

在功能 **板中显示推送通知** “拼贴”后，使用创建通知向导添加内容：

1. 单击“推送通知”拼贴右上角的添加符 **号** ，以打开创建 **通知向导**。

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. 单击链接路径中的浏览图标，向用户显示应用程序的内容结构。

   选择路径后，单击复选图标。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >“链接按钮文本”限制为20个字符。
   >
   >如果最终用户没有最新版本的应用程序并且链接的路径不可用，则确认深层链接的操作将使用户进入应用程序的主页。

1. 在创建通 **知向导中输入** “文本详细信 **息”，然后单击“** 创建 ****”。

   ![chlimage_1-114](assets/chlimage_1-114.png)

   通过单击您从“推送通知”拼贴创建的推送通知，打开 **详细信息** 。

   您可以编辑属性、发送通知或删除通知。

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**附加信息**:
>
>在6.4版本发布后，将不支持Pushwoosh和Amazon SNS，并将作为包共享的加载项提供。

### 后续步骤 {#the-next-steps}

了解有关应用程序推送通知的详细信息后，请参阅 [AEM Mobile内容个性化](/help/mobile/phonegap-aem-mobile-content-personalization.md)。

