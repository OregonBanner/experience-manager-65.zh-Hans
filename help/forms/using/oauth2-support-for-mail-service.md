---
title: 为Microsoft® Office 365邮件服务器协议配置基于OAuth2的身份验证
description: 为Microsoft® Office 365邮件服务器协议配置基于OAuth2的身份验证
source-git-commit: 35595ffca9d2f6fd80bfe93bade247f5b4600469
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 3%

---

# 与Microsoft® Office 365邮件服务器协议集成 {#oauth2-support-for-the-microsoft-mail-server-protocols}

为了让组织遵守安全的电子邮件要求，AEM Forms提供了OAuth 2.0支持与Microsoft® Office 365邮件服务器协议集成。 您可以使用Azure Active Directory(Azure AD)OAuth 2.0身份验证服务，与各种协议（如IMAP、POP或SMTP）连接并访问Office 365用户的电子邮件数据。 以下是配置Microsoft® Office 365邮件服务器协议以通过OAuth 2.0服务进行身份验证的分步说明：

1. 登录 [https://portal.azure.com/](https://portal.azure.com/) 和搜索 **Azure Active Directory** ，然后单击结果。
或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击 **添加** > **应用程序注册** > **新注册**

   ![应用程序注册](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根据您的要求填写信息，然后单击 **注册**.
   ![支持的帐户](/help/forms/using/assets/azure_suuportedaccountype.png)
在上述情况下， 
**任何组织目录（任何Azure AD目录 — 多租户）中的帐户和个人Microsoft®帐户（例如，Skype、Xbox）** 选项。

   >[!NOTE]
   >
   > * 对于 **任何组织目录（任何Azure AD目录 — 多租户）中的帐户** 应用程序时，建议使用工作帐户，而不是个人电子邮件帐户。
   > * **个人Microsoft®帐户** 和 **单租户** 不支持应用程序。
   > * 建议使用 **多租户和个人Microsoft®帐户** 应用程序。


1. 接下来，转到 **证书和密钥**，单击 **新客户端密钥** 并按照屏幕上的步骤创建密钥。 请务必注意此密钥值，供以后使用。

   ![密钥](/help/forms/using/assets/azure_secretkey.png)

1. 要添加权限，请转到新创建的应用程序，然后选择 **API权限** > **添加权限** > **Microsoft®图** > **授权权限**
1. 选中应用程序以下权限对应的复选框，然后单击 **添加权限**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API权限](/help/forms/using/assets/azure_apipermission.png)

1. 选择 **身份验证** > **添加平台** > **Web**&#x200B;和 **重定向Url** 部分，将以下任何URI（通用资源标识符）添加为：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在这种情况下， `https://login.microsoftonline.com/common/oauth2/nativeclient` 用作重定向URI。

1. 单击 **配置** 添加每个URL后，并根据您的要求配置设置。
   ![重定向 URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 必须选择 **访问令牌** 和 **ID令牌** 复选框。

1. 单击 **概述** ，并复制 **应用程序（客户端）ID**, **目录（租户）ID**&#x200B;和 **客户端密钥** 供以后使用。

   ![概述](/help/forms/using/assets/azure_overview.png)

## 生成授权代码 {#generating-the-authorization-code}

接下来，您需要生成授权代码，如以下步骤中所述：

1. 在将 `clientID` 和 `<client_id>` 和 `redirect_uri` 使用您的应用程序的重定向URI:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

1. 当您键入上述URL时，系统会将您重定向到登录屏幕：
   ![登录屏幕](/help/forms/using/assets/azure_loginscreen.png)

1. 输入电子邮件，单击 **下一个** 和应用程序权限屏幕出现：

   ![允许权限](/help/forms/using/assets/azure_permission.png)

1. 在您允许权限后，您将被重定向到新URL，如下所示： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 复制 `<code>` 来自 `0.ASY...` to `&session_state` 中。

## 生成刷新令牌 {#generating-the-refresh-token}

接下来，您需要生成刷新令牌，如以下步骤中所述：

1. 打开命令提示符，然后使用以下cURL命令获取refreshToken。

1. 替换 `clientID`, `client_secret` 和 `redirect_uri` ，以及 `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

1. 记下刷新令牌。

## 使用OAuth 2.0支持配置电子邮件服务 {#configureemailservice}

现在，您必须通过在管理员UI中登录来在最新的JEE服务器上配置电子邮件服务：

1. 转到 **主页** > **服务** > **应用程序和服务** > **服务管理** > **电子邮件服务**, **配置电子邮件服务** 窗口，已配置基本身份验证。

   >[!NOTE]
   >
   > 要启用oAuth 2.0身份验证服务，必须选择 **SMTP服务器是否需要身份验证（SMTP身份验证）** 复选框。

1. 已设置 **oAuth 2.0身份验证设置** as `True`.
1. 复制 **客户端ID** 和 **客户端密钥** 从Azure门户。
1. 复制生成的值 **刷新令牌**.
1. 登录到 **Workbench** 和搜索 **电子邮件1.0** 从 **活动选取器**.
1. Email 1.0下提供了以下三个选项：
   * **随文档发送**:发送包含单个附件的电子邮件。
   * **随附件映射一起发送**:发送包含多个附件的电子邮件。
   * **接收**:从IMAP接收电子邮件。

   >[!NOTE]
   >
   >* 传输安全协议的有效值为：“blank”、“SSL”或“TLS”。 您必须将 **SMTP传输安全** 和 **接收传输安全性** to **TLS** 用于启用oAuth身份验证服务。
   >* **POP3协议** 不支持OAuth。


   ![连接设置](/help/forms/using/assets/oauth_connectionsettings.png)

1. 通过选择 **随文档发送**.
1. 提供 **至** 和 **从** 地址。
1. 调用应用程序，然后使用0Auth 2.0身份验证发送电子邮件。

   >[!NOTE]
   >
   >如果要将Auth 2.0身份验证设置更改为Workbench中特定进程的基本身份验证，则可以将 **OAuth 2.0身份验证** 值为“False”时 **使用全局设置** 在 **连接设置** 选项卡。

## 启用oAuth任务通知 {#enable_oauth_task}

1. 转到 **主页** > **服务** > **表单工作流** > **服务器设置** > **电子邮件设置**
1. 要启用oAuth任务通知，请选择 **启用oAuth** 复选框。
1. 复制 **客户端ID** 和 **客户端密钥** 从Azure门户。
1. 复制生成的值 **刷新令牌**.
1. 单击 **保存** 以保存详细信息。

   ![任务通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 要了解与任务通知相关的更多信息， [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 配置电子邮件端点 {#configure_email_endpoint}

1. 转到 **主页** > **服务** > **应用程序和服务** > **端点管理**
1. 要配置电子邮件端点，请设置 **oAuth 2.0身份验证设置** as `True`.
1. 复制 **客户端ID** 和 **客户端密钥** 从Azure门户。
1. 复制生成的值 **刷新令牌**.
1. 单击 **保存** 以保存详细信息。

   ![连接设置](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 要了解有关配置电子邮件端点的更多信息，请单击 [配置电子邮件端点](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## 疑难解答 {#troubleshooting}

* 如果电子邮件服务无法正常工作。 尝试重新生成 `Refresh Token` 如上所述。 部署新值需要几分钟。

* 使用Workbench在电子邮件端点中配置电子邮件服务器详细信息时出错。请尝试通过管理员UI而不是Workbench配置端点。

