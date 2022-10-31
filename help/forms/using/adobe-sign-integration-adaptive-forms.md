---
title: 将Adobe Sign与AEM Forms集成
seo-title: Integrate Adobe Sign with AEM Forms
description: 了解如何配置Adobe Sign for AEM Forms
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 24%

---

# 集成 [!DNL Adobe Sign] 与AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 为自适应表单启用电子签名工作流。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在 [!DNL Adobe Sign] 和自适应表单方案中，用户将自适应表单填充到 **申请服务**. 例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服务提供商将审核申请，并使用 [!DNL Adobe Sign] 将申请标记为已批准。要启用类似的电子签名工作流，您可以集成 [!DNL Adobe Sign] 与AEM [!DNL Forms].

使用 [!DNL Adobe Sign] 与AEM [!DNL Forms]，配置 [!DNL Adobe Sign] 在AEM云服务中：

## 前提条件 {#prerequisites}

您需要满足以下条件才能集成 [!DNL Adobe Sign] 与AEM [!DNL Forms]:

* 活动 [Adobe Sign开发人员帐户。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 安 [启用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 服务器。
* [Adobe Sign API 应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API 应用程序的凭据（客户端 ID 和客户端密码）。
* 重新配置时，请删除现有 [!DNL Adobe Sign] 从创作实例和发布实例进行配置。
* 针对创作实例和发布实例，使用[相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 配置 [!DNL Adobe Sign] 与AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

在满足先决条件后，执行以下步骤以配置 [!DNL Adobe Sign] 与AEM [!DNL Forms] 在创作实例上：

1. 在AEM上 [!DNL Forms] 创作实例，导航到 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档以了解更多信息。
1. 在 **[!UICONTROL 创建配置]** 对话框，指定 **[!UICONTROL 标题]** 对于配置，请启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 它会为云服务创建一个配置容器。
1. 导航到 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** ，然后选择在上述步骤中创建的配置容器。

   >[!NOTE]
   >
   >您可以执行步骤1-4来创建新配置容器并创建 [!DNL Adobe Sign] 配置或使用现有 `global` 文件夹 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 如果在新配置容器中创建配置，请确保在 **[!UICONTROL 配置容器]** 字段。

   >[!NOTE]
   确保云服务配置页面的URL以开头 **HTTPS**. 如果没有， [启用SSL](/help/sites-administering/ssl-by-default.md) for AEM [!DNL Forms] 服务器。

1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] 在AEM中配置 [!DNL Forms].
1. 在 **[!UICONTROL 常规]** 选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** ，然后点按 **[!UICONTROL 下一个]**. 您可以选择指定标题并浏览以选择配置的缩略图。

1. 将当前浏览器窗口中的 URL 复制到记事本。需要配置 [!DNL Adobe Sign] 使用AEM应用程序[!DNL Forms].

1. 在 **[!UICONTROL 设置]** 选项卡 **[!UICONTROL OAuth URL]** 字段中包含默认URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果为 Adobe Experience Manager 功能或组件创建另一个 [!DNL Adobe Sign] 配置，请确保所有 [!DNL Adobe Sign] 云配置指向同一分片。

   >[!NOTE]
   保留 **创建Adobe Sign配置** 页面。 不要关闭它。 您可以检索 **客户端Id** 和 **客户端密钥** 在为 [!DNL Adobe Sign] 应用程序，如后续步骤中所述。


1. 配置 [!DNL Adobe Sign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口并登录到 [!DNL Adobe Sign] 开发人员帐户。
   1. 选择为AEM配置的应用程序 [!DNL Forms]，然后点按 **[!UICONTROL 为应用程序配置OAuth]**.
   1. 复制 **[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密钥]** 记事本。
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加在上一步中复制的HTTPS URL。
   1. 为 [!DNL Adobe Sign] 应用程序并单击 **[!UICONTROL 保存]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   有关为 [!DNL Adobe Sign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth 配置](assets/oauthconfig_new.png)

1. 返回到 **[!UICONTROL 创建Adobe Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡 **[!UICONTROL OAuth URL]** 字段中会提及默认URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。

   您可以修改数据库分片的值。重新启动服务器，以便能够将新值用于数据库共享。

   >[!NOTE]
   确保您的创作和发布实例配置指向同一共享。 如果您为组织创建多个Adobe Sign配置，请确保所有配置都使用同一共享。

1. 返回到 **[!UICONTROL 创建Adobe Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡，指定 **客户端ID** （也称为应用程序ID）和 **客户端密钥**. 使用 [Adobe Sign应用程序的客户端ID和客户端密钥](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 为AEM Forms创建。

1. 选择 **[!UICONTROL 还为附件启用Adobe Sign]** 用于将附加到自适应表单的文件附加到相应表单的选项 [!DNL Adobe Sign] 文档已发送以供签名。

1. 点按 **[!UICONTROL 连接到Adobe Sign]**. 在系统提示输入凭据时，提供在创建 [!DNL Adobe Sign] 应用程序时所用帐户的用户名和密码。

1. 点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] 配置。

1. 打开AEM Web Console。 URL为 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **[!UICONTROL Forms通用配置服务].**
1. 在 **[!UICONTROL 允许]** 字段， **选择** 所有用户 — 所有用户（匿名或已登录）都可以预览附件、验证和签名表单，然后单击 **[!UICONTROL 保存].** 创作实例配置为使用 [!DNL Adobe Sign].
1. 发布配置。
1. 使用 [复制](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) 以在相应的发布实例上创建相同的配置。

现在， [!DNL Adobe Sign] 与AEM集成 [!DNL Forms] 并可在自适应表单中使用。 至 [在自适应表单中使用Adobe Sign服务](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，在自适应表单属性中指定上面创建的配置容器。



## 配置 [!DNL Adobe Sign] 调度程序以同步签名状态 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

安 [!DNL Adobe Sign] 只有在所有签名者完成签名过程后，才会提交已启用的自适应表单。 默认情况下， [!DNL Adobe Sign] 计划程序服务计划在每24小时后检查（轮询）签名者响应。 您可以为您的环境更改此默认间隔。执行以下步骤以更改默认间隔：

1. 登录AEM [!DNL Forms] 具有管理员凭据的服务器，然后导航到 **工具** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   您还可以在浏览器窗口中打开以下URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到并打开 **[!UICONTROL Adobe Sign配置服务]** 选项。 指定 [cron表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 在 **[!UICONTROL 状态更新调度程序表达式]** 字段，单击 **[!UICONTROL 保存]**. 例如，要每天00:00 am运行配置服务，请指定 `0 0 0 1/1 * ? *` 在 **[!UICONTROL 状态更新调度程序表达式]** 字段。

同步状态的默认间隔为 [!DNL Adobe Sign] 现在已更改。

## 相关文章 {#related-articles}

* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [将Adobe Sign与AEM Forms结合使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
