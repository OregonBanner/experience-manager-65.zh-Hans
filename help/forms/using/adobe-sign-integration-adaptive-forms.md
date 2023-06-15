---
title: 将Adobe Sign与AEM Forms集成
seo-title: Integrate Adobe Sign with AEM Forms
description: 了解如何为AEM Forms配置Adobe Sign
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 66674f0e2621d8786ab4d662cddad373122d8b51
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 18%

---

# 集成 [!DNL Adobe Sign] 使用AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 支持自适应表单的电子签名工作流。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在典型的 [!DNL Adobe Acrobat Sign] 和自适应表单方案中，用户需填写自适应表单来申请服务。例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服务提供商将审核申请，并使用 [!DNL Adobe Acrobat Sign] 将申请标记为已批准。AEM Forms支持Adobe Acrobat Sign和Adobe Acrobat Sign Solutions政府版。 根据您的许可证和要求，您可以将AEM Forms与以下任一解决方案集成或连接：

* [将AEM Forms与Adobe Acrobat Sign连接](#adobe-sign)
* [将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接](#adobe-acrobat-sign-for-government)

## 将AEM Forms与Adobe Acrobat Sign连接 {#adobe-sign}

连接 **[!DNL AEM Forms]** 替换为 **[!DNL Adobe Acrobat Sign]**，设置先决条件部分中列出的软件和帐户，并将Adobe Sign连接到您的所有AEM Forms创作和发布实例：

## 前提条件 {#prerequisites}

您需要以下项才能集成 [!DNL Adobe Sign] 使用AEM [!DNL Forms]：

* 活动 [Adobe Sign开发人员帐户。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* An [已启用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 服务器。
* [Adobe Sign API 应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API 应用程序的凭据（客户端 ID 和客户端密码）。
* 重新配置时，删除现有 [!DNL Adobe Sign] 来自创作实例和发布实例的配置。
* 针对创作实例和发布实例，使用[相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 配置 [!DNL Adobe Sign] 使用AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

满足前提条件后，执行以下步骤以配置 [!DNL Adobe Sign] 使用AEM [!DNL Forms] 在创作实例上：

1. 在AEM上 [!DNL Forms] 创作实例，导航到 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
1. 在 **[!UICONTROL 创建配置]** 对话框，请指定 **[!UICONTROL 标题]** 对于配置，启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 它会创建一个配置容器。
1. 导航到 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 并选择您在上一步中创建的配置容器。

   >[!NOTE]
   >
   >您可以执行步骤1-4以创建新的配置容器并创建 [!DNL Adobe Sign] 在容器中配置或使用现有 `global` 文件夹位置 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 如果您在新配置容器中创建配置，请确保在 **[!UICONTROL 配置容器]** 创建自适应表单时显示的字段。

   >[!NOTE]
   >
   确保“Cloud Services配置”页的URL开头为 **HTTPS**. 如果没有， [启用SSL](/help/sites-administering/ssl-by-default.md) 对于AEM [!DNL Forms] 服务器。

1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] AEM中的配置 [!DNL Forms].
1. 在 **[!UICONTROL 常规]** 的选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** 有关配置，请点按 **[!UICONTROL 下一个]**. 您可以选择指定标题并浏览以选择配置的缩略图。

1. 将当前浏览器窗口中的 URL 复制到记事本。需要配置 [!DNL Adobe Sign] 使用AEM的应用程序[!DNL Forms].

1. 在 **[!UICONTROL 设置]** 选项卡， **[!UICONTROL OAuth URL]** 字段包含默认URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果为 Adobe Experience Manager 功能或组件创建另一个 [!DNL Adobe Sign] 配置，请确保所有 [!DNL Adobe Sign] 云配置指向同一分片。

   >[!NOTE]
   >
   保留 **创建Adobe Sign配置** 页面打开。 不要关闭它。 您可以检索 **客户端ID** 和 **客户端密码** 在为配置OAuth设置后 [!DNL Adobe Sign] 应用程序（如即将执行的步骤中所述）。


1. 配置 [!DNL Adobe Sign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口并登录到 [!DNL Adobe Sign] 开发人员帐户。
   1. 选择为AEM配置的应用程序 [!DNL Forms]，然后点按 **[!UICONTROL 为应用程序配置OAuth]**.
   1. 复制 **[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]** 记事本。
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加在上一步中复制的HTTPS URL。
   1. 为启用以下OAuth设置 [!DNL Adobe Sign] 应用程序并单击 **[!UICONTROL 保存]**.

   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   有关为 [!DNL Adobe Sign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth 配置](assets/oauthconfig_new.png)

1. 返回至 **[!UICONTROL 创建Adobe Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡， **[!UICONTROL OAuth URL]** 字段提及默认URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。

   您可以修改数据库分片的值。重新启动服务器以便能够使用数据库分片的新值。

   >[!NOTE]
   >
   确保您的创作实例和发布实例配置指向同一分片。 如果为组织创建多个Adobe Sign配置，请确保所有配置都使用相同分片。

1. 返回至 **[!UICONTROL 创建Adobe Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡，指定 **客户端ID** （也称为应用程序ID）和 **客户端密码**. 使用 [Adobe Sign应用程序的客户端ID和客户端密码](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 已为AEM Forms创建。

1. 选择 **[!UICONTROL 另为附件启用Adobe Sign]** 用于将附加到自适应表单的文件追加到相应表单的选项 [!DNL Adobe Sign] 文档已发送供签名。

1. 点按 **[!UICONTROL 连接到Adobe Sign]**. 在系统提示输入凭据时，提供在创建 [!DNL Adobe Sign] 应用程序时所用帐户的用户名和密码。

1. 点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] 配置。

1. 打开AEM Web控制台。 URL是 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **[!UICONTROL Forms通用配置服务].**
1. 在 **[!UICONTROL 允许]** 字段， **选择** 所有用户 — 所有用户（匿名或登录）都可以预览附件、验证和签署表单，然后单击 **[!UICONTROL 保存].** 创作实例配置为使用 [!DNL Adobe Sign].
1. 发布配置。
1. 使用 [复制](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=zh-Hans) 以在相应的发布实例上创建相同的配置。

现在， [!DNL Adobe Sign] 与AEM集成 [!DNL Forms] 并准备用于自适应表单。 至 [在自适应表单中使用Adobe Sign服务](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，指定在自适应表单属性中创建的配置容器。

## 将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接 {#adobe-acrobat-sign-for-government}

[!BADGE 测试版文档]{type=Caution tooltip="黄色状态"}
<span class="preview"> 本部分包含测试版文档，这些信息可能会发生更改。</span>

将AEM Forms与面向政府的Adobe Acrobat Sign Solutions连接是一个多步骤的过程。 它涉及：

* 为您的AEM实例创建重定向URL
* 与适用于政府团队的Adobe Sign解决方案共享重定向URL和范围
* 从Adobe Sign团队接收凭据
* 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

![](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 开始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

在开始将AEM Forms与Adobe Acrobat Sign解决方案连接之前，

* 确保您的 [Adobe Acrobat Sign Solutions政府版](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 已配置帐户。
* 您的AEM [!DNL Forms] 服务器是 [已启用SSL](/help/sites-administering/ssl-by-default.md) .
* 您的AEM [!DNL Forms] 服务器正在使用 [相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) （创作实例和发布实例）。

### 将AEM Forms连接到适用于政府的Adobe Acrobat Sign Solutions {#connect-adobe-acrobat-sign-for-government}

#### 为您的AEM实例创建重定向URL

1. 在您的AEM Forms实例上，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，请指定 **[!UICONTROL 标题]** 对于配置，启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 它会创建一个配置容器。 确保容器/文件夹名称不包含任何空格。

1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 并打开您在上一步中创建的配置容器。 创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。
1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Acrobat Sign] AEM Forms配置。
1. 将当前浏览器窗口的URL从URL复制到记事本。 此URL称为 `re-direct URL`. 在下一部分中，您共享 `re-direct URL` 和 `Scopes` 包含Adobe Sign团队和请求凭据（客户端ID和客户端密钥）。

>
>
>
* 使用 [顶级](https://en.wikipedia.org/wiki/Top-level_domain) 域为 `re-direct URL`. 例如，`https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* 请勿将本地URL用作 `re-direct URL`. 例如：`https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/SignConfig`。
> 


#### 与Adobe Sign团队共享重定向URL和作用域并接收凭据

Adobe Acrobat Sign政府解决方案团队要求 `re-direct URL` 以及要为您的Adobe Acrobat Sign应用程序启用的特定范围（如下所列），以生成凭据（客户端ID和客户端密钥），从而允许您将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接。

共享 `scopes` （如下所列）和 `re-direct URL` 与您的Adobe Acrobat Sign政府解决方案代表([Adobe Professional Services团队成员](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password))。

**_范围_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

该代表会生成凭据并与您共享。 在下一部分中，您将使用凭据（客户端ID和客户端密钥）将AEM Forms与用于政府管理的Adobe Acrobat Sign Solutions连接。

#### 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

1. 打开 `re-direct URL` 在浏览器中。 您已创建并记下 `re-direct URL` 在 [在您的AEM实例上创建重定向URL](#create-redirect-url) 部分。

1. 在 **[!UICONTROL 常规]** 的选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** ，然后点按 **[!UICONTROL 下一个]**. 您可以选择指定 **[!UICONTROL 标题]** 并浏览以选择 **[!UICONTROL 缩略图]** 用于配置。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 设置]** 的选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，用于 **[!UICONTROL 选择解决方案]** 选项，选择 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions政府版](/help/forms/using/assets/adobe-sign-for-govt.png)

1. 在 **[!UICONTROL 电子邮件]** 字段，为政府帐户指定与您的Adobe Acrobat Sign Solutions关联的电子邮件地址。

1. 此 **[!UICONTROL OAuth URL]** 字段指定Adobe Sign数据库分片。 字段包含默认URL。 请勿更改URL。

1. 使用Adobe Acrobat Sign为政府解决方案代表共享的凭据([Adobe Professional Services团队成员])在上一部分中作为[**[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]**]。

1. 选择 **[!UICONTROL 为附件启用Adobe Acrobat Sign]** 用于将附加到自适应表单的文件追加到相应表单的选项 [!DNL Adobe Acrobat Sign] 文档已发送供签名。

1. 点按 **[!UICONTROL 连接到Adobe Sign]**. 在系统提示输入凭据时，提供在创建 [!DNL Adobe Acrobat Sign] 应用程序时所用帐户的用户名和密码。当要求确认访问时 `your developer account`，单击 **[!UICONTROL 允许访问]**. 如果凭据正确，并且您允许 [!DNL AEM Forms] 访问您的 [!DNL Adobe Acrobat Sign] 开发人员帐户，系统会显示一条与以下内容类似的成功消息。

   ![Adobe Acrobat Sign云配置成功](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. 点按 **[!UICONTROL 创建]** 以创建配置。
1. 打开AEM Web控制台。 URL是 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **[!UICONTROL Forms通用配置服务].**
1. 在 **[!UICONTROL 允许]** 字段， **选择** 所有用户 — 所有用户（匿名或登录）都可以预览附件、验证和签署表单，然后单击 **[!UICONTROL 保存].** 创作实例配置为使用 [!DNL Adobe Sign].

1. 发布配置。
1. 使用 [复制](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=zh-Hans) 以在相应的发布实例上创建相同的配置。

现在，您可以 [在自适应表单中添加字段Adobe Acrobat Sign](working-with-adobe-sign.md) 或 [AEM Workflow](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). 确保将用于Cloud Service配置的配置容器添加到启用的所有自适应Forms [!DNL Adobe Acrobat Sign]. 您可以在自适应表单的属性中指定配置容器。


## 配置 [!DNL Adobe Sign] 同步签名状态的计划程序 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

An [!DNL Adobe Sign] 仅在所有签名者完成签名过程后提交启用的自适应表单。 默认情况下， [!DNL Adobe Sign] 计划程序服务计划每24小时检查（轮询）一次签名者响应。 您可以为您的环境更改此默认间隔。执行以下步骤以更改默认间隔：

1. 登录到AEM [!DNL Forms] 使用管理员凭据访问服务器并导航到 **工具** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   您还可以在浏览器窗口中打开以下URL：
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到并打开 **[!UICONTROL Adobe Sign配置服务]** 选项。 指定 [cron表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 在 **[!UICONTROL 状态更新计划程序表达式]** 字段并单击 **[!UICONTROL 保存]**. 例如，要在每天凌晨00:00运行配置服务，请指定 `0 0 0 1/1 * ? *` 在 **[!UICONTROL 状态更新计划程序表达式]** 字段。

同步状态的默认间隔 [!DNL Adobe Sign] 现已更改。

## 相关文章 {#related-articles}

* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [将Adobe Sign与AEM Forms结合使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
