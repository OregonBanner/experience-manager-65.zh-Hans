---
title: 对邮件服务的 OAuth2 支持
description: 'Oauth2对邮件服务的支持  '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# 对邮件服务的 OAuth2 支持 {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service 提供对其集成的邮件服务的 OAuth2 支持，以便各组织能够遵守安全电子邮件要求。

您可以为多个电子邮件提供商配置 OAuth。以下分步说明针对在 Microsoft Office 365 Outlook 中配置 AEM 邮件服务以通过 OAuth2 进行身份验证。可通过类似方式配置其他供应商。

## Microsoft Outlook {#microsoft-outlook}

1. 转至 [https://portal.azure.com/](https://portal.azure.com/) 并登录。
1. 在搜索栏中搜索 **Azure Active Directory**，并单击搜索结果。或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击&#x200B;**应用程序注册** - **新注册**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. 根据您的要求填写信息，然后单击&#x200B;**注册**
1. 转至新创建的应用程序，并选择 **API 权限**
1. 转至&#x200B;**添加权限** - **图表权限** - **委派权限**
1. 为应用程序选择以下权限，然后单击&#x200B;**添加权限**：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 转至&#x200B;**身份验证** - **添加平台** - **Web**，然后在&#x200B;**重定向 URL** 部分中，添加以下 URL - 一个带正斜杠，一个不带正斜杠：
   * `http://localhost/`
   * `http://localhost`
1. 在添加每个 URL 后按&#x200B;**配置**，然后根据您的要求配置设置
1. 接下来，转到 **证书和密钥**，单击 **新客户端密钥** 并按照屏幕上的步骤创建密钥。 请务必记下此密码供以后使用
1. 按 **概述** ，并复制 **应用程序（客户端）ID** 供以后使用。

要重新查看，您需要以下信息才能在AEM端为Mail服务配置OAuth2:

* 格式为：的身份验证URL `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* 格式为的令牌URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* 表单中的刷新URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* 客户端 ID
* 客户端密码

### 生成刷新令牌 {#generating-the-refresh-token}

接下来，您需要生成刷新令牌，如后续步骤中所示。

可执行以下步骤来做到这一点：

1. 在将 `clientID` ，且值特定于您的帐户：

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. 允许许可（无论何时需要）。
1. URL 将重定向到一个新位置，并采用以下格式：`http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 复制上述示例中的 `<code>` 的值
1. 使用以下 cURL 命令获取 refreshToken。将clientID、clientSecret替换为您帐户的值和 `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. 记下 refreshToken 和 accessToken。

### 验证令牌 {#validating-the-tokens}

继续在 AEM 端配置 OAuth 之前，确保使用以下过程验证 accessToken 和 refreshToken：

1. 使用上一个过程中生成的 refreshToken 生成 accessToken。您可以通过以下curl和替换 `<client_id>`,`<client_secret>` 以及 `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. 使用accessToken发送邮件，以查看邮件是否正常工作。

>[!NOTE]
>
> 您可以从[此位置](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)获取 Postman API 收藏集。

### 使用Auth2.0支持配置电子邮件服务 {#configureemailservice}

现在，您必须通过在管理员UI中登录来在最新的JEE服务器上配置电子邮件服务：

1. 转到 **主页** - **服务** - **应用程序和服务** - **服务管理** - **电子邮件服务**
1. **配置电子邮件服务** 窗口，配置 **SMPT** 和 **IMP** 用于基本身份验证的服务器。
1. 要启用Outlook邮件身份验证服务，请选择 **oAuth 2.0身份验证设置** 复选框。
1. 复制 **客户端ID** 和 **客户端密钥** 从Azure门户。
1. 复制生成的值 **刷新令牌**.
1. 单击 **保存** 以保存详细信息。
1. 登录Workbench并搜索 **电子邮件1.0** 从 **活动选取器**.
1. Email 1.0下提供了以下三个选项：
   * **随文档发送**:发送包含单个附件的电子邮件。
   * **随附件映射一起发送**:发送包含多个附件的电子邮件。
   * **接收**:从POP3或IMAP接收电子邮件。
1. 通过选择 **随文档发送**
1. 提供 **至** 和 **从** 地址。
1. 调用应用程序，然后使用oAuth2.0身份验证发送电子邮件。

>[!NOTE]
>
> 如果要将Auth 2.0身份验证设置更改为Workbench中特定进程的基本身份验证，可取消选中 **oAuth2.0身份验证** 复选框下方 **使用全局设置** 在 **连接设置** 选项卡。

### 疑难解答 {#troubleshooting}

如果邮件服务无法正常运行，请重新生成 `refreshToken` 如上所述。 部署新值需要几分钟。


