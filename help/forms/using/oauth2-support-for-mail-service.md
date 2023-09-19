---
title: 为Microsoft&reg； Office 365邮件服务器协议配置基于OAuth2的身份验证
description: 为Microsoft&reg； Office 365邮件服务器协议配置基于OAuth2的身份验证
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: 99808cb38c5d376ccb7fb550c5212138890cec11
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 7%

---

# 与Microsoft® Office 365邮件服务器协议集成 {#oauth2-support-for-the-microsoft-mail-server-protocols}

为了让组织遵守安全电子邮件要求，AEM Forms提供了OAuth 2.0支持与Microsoft® Office 365邮件服务器协议集成。 您可以使用Azure Active Directory (Azure AD) OAuth 2.0身份验证服务连接各种协议（如IMAP、POP或SMTP），并访问Office 365用户的电子邮件数据。 以下是配置Microsoft® Office 365邮件服务器协议以通过OAuth 2.0服务进行身份验证的分步说明：

1. 登录 [https://portal.azure.com/](https://portal.azure.com/) 和搜索 **Azure活动目录** 在搜索栏中单击结果。
或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击 **添加** > **应用程序注册** > **新建注册**

   ![应用程序注册](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根据您的要求填写信息，然后单击&#x200B;**注册。**
   ![支持的帐户](/help/forms/using/assets/azure_suuportedaccountype.png)
在上述案例中， **任何组织目录（任何Azure AD目录 — 多租户）中的帐户和个人Microsoft®帐户（例如，Skype、Xbox）** 已选中选项。

   >[!NOTE]
   >
   > * 对象 **任何组织目录（任何Azure AD目录 — 多租户）中的帐户** ，Adobe建议您使用工作帐户，而不是个人电子邮件帐户。
   > * **仅限个人Microsoft®帐户** 应用程序不受支持。
   * Adobe建议您使用 **多租户和个人Microsoft®帐户** 应用程序。

1. 接下来，转至&#x200B;**证书和密码**，单击&#x200B;**新建客户端密码**，然后执行屏幕上显示的步骤来创建密码。请务必记下此secret值供以后使用。

   ![密钥](/help/forms/using/assets/azure_secretkey.png)

1. 要添加权限，请转到新创建的应用程序，然后选择 **API权限** > **添加权限** > **Microsoft® Graph** > **委派权限**
1. 选中应用程序的以下权限对应的复选框，然后单击 **添加权限**：

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API权限](/help/forms/using/assets/azure_apipermission.png)

1. 选择 **身份验证** > **添加平台** > **Web**、和 **重定向Url** 部分，添加以下任意URI（通用资源标识符）作为：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在本例中， `https://login.microsoftonline.com/common/oauth2/nativeclient` 用作重定向URI。

1. 单击 **配置** 添加每个URL并根据您的要求配置设置后。
   ![重定向 URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   必须选择 **访问令牌** 和 **ID令牌** 复选框。

1. 单击 **概述** 并将值复制到 **应用程序（客户端）ID**， **目录（租户）ID**、和 **客户端密码** 供以后使用。

   ![概述](/help/forms/using/assets/azure_overview.png)

## 生成授权码 {#generating-the-authorization-code}

接下来，必须生成授权码，如以下步骤所述：

1. 替换后在浏览器中打开以下URL `clientID` 使用 `<client_id>` 和 `redirect_uri` 使用应用程序的重定向URI：

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   如果存在单个租户应用程序，请替换 `common` 与您的 `[tenantid]` 在以下URL中生成授权码： `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 键入上述URL后，您将被重定向到登录屏幕：
   ![登录屏幕](/help/forms/using/assets/azure_loginscreen.png)

1. 输入电子邮件，然后单击 **下一个** 此时会显示“应用程序权限”屏幕：

   ![允许权限](/help/forms/using/assets/azure_permission.png)

1. 一旦您允许权限，您就会被重定向到一个新的URL，如下所示： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 复制的值 `<code>` 从上述URL从 `0.ASY...` 到 `&session_state` 在上面URL中。

## 生成刷新令牌 {#generating-the-refresh-token}

接下来，必须生成刷新令牌，如以下步骤所述：

1. 打开命令提示符并使用以下cURL命令获取refreshToken。

1. 替换 `clientID`， `client_secret`、和 `redirect_uri` 应用程序的值以及 `<code>`：

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   在单个租户应用程序中，要生成刷新令牌，请使用以下cURL命令并替换 `common` 使用 `[tenantid]` 范围：
   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 记下刷新令牌。

## 使用OAuth 2.0支持配置电子邮件服务 {#configureemailservice}

现在，通过登录到管理员UI在最新的JEE服务器上配置电子邮件服务：

1. 转到 **主页** > **服务** > **应用程序和服务** > **服务管理** > **电子邮件服务**， **配置电子邮件服务** 此时将显示一个窗口，该窗口已针对基本身份验证进行了配置。

   >[!NOTE]
   >
   要启用oAuth 2.0身份验证服务，必须选择 **SMTP服务器是否需要身份验证（SMTP身份验证）** 复选框。

1. 设置 **oAuth 2.0身份验证设置** 作为 `True`.
1. 复制以下项目的值： **客户端ID** 和 **客户端密码** 从Azure门户。
1. 复制生成的的值 **刷新令牌**.
1. 登录 **Workbench** 和搜索 **电子邮件1.0** 从 **活动选取器**.
1. 电子邮件1.0下提供了三个选项：
   * **随文档发送**：发送带有单个附件的电子邮件。
   * **随附件映射一起发送**：发送具有多个附件的电子邮件。
   * **接收**：从IMAP接收电子邮件。

   >[!NOTE]
   >
   * 传输安全协议具有以下有效值：“blank”、“SSL”或“TLS”。 设置值 **SMTP传输安全性** 和 **接收传输安全** 到 **TLS** 用于启用oAuth身份验证服务。
   * **POP3协议** 在使用电子邮件端点时，不支持OAuth。

   ![连接设置](/help/forms/using/assets/oauth_connectionsettings.png)

1. 通过选择测试应用程序 **随文档发送**.
1. 提供 **至** 和 **从** 地址。
1. 调用应用程序，并使用0Auth 2.0身份验证发送电子邮件。

   >[!NOTE]
   >
   如果要将Auth 2.0身份验证设置更改为工作台中特定进程的基本身份验证，则可以设置 **OAuth 2.0身份验证** 值为“False”，位于 **使用全局设置** 在 **连接设置** 选项卡。

## 启用oAuth任务通知 {#enable_oauth_task}

1. 转到 **主页** > **服务** > **表单工作流** > **服务器设置** > **电子邮件设置**
1. 要启用oAuth任务通知，请选择 **启用oAuth** 复选框。
1. 复制以下项目的值： **客户端ID** 和 **客户端密码** 从Azure门户。
1. 复制生成的的值 **刷新令牌**.
1. 单击 **保存** 以保存详细信息。

   ![任务通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   要了解与任务通知相关的更多信息， [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 配置电子邮件端点 {#configure_email_endpoint}

1. 转到 **主页** > **服务** > **应用程序和服务** > **端点管理**
1. 要配置电子邮件端点，请设置 **oAuth 2.0身份验证设置** 作为 `True`.
1. 复制以下项目的值： **客户端ID** 和 **客户端密码** 从Azure门户。
1. 复制生成的的值 **刷新令牌**.
1. 单击 **保存** 以保存详细信息。

   ![连接设置](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   要了解有关配置电子邮件端点的更多信息，请单击 [配置电子邮件端点](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## 疑难解答 {#troubleshooting}

* 如果电子邮件服务无法正常工作，请尝试重新生成 `Refresh Token` 如上所述。 部署新值需要花费几分钟的时间。

* 使用Workbench在电子邮件端点中配置电子邮件服务器详细信息时出错。 尝试通过Admin UI（而不是Workbench）配置端点。
