---
title: 将Adobe Sign与AEM Forms集成
seo-title: 将Adobe Sign与AEM Forms集成
description: 了解如何为AEM Forms配置Adobe Sign
seo-description: 了解如何为AEM Forms配置Adobe Sign
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---


# 将Adobe Sign与AEM Forms集成{#integrate-adobe-sign-with-aem-forms}

Adobe Sign支持自适应表单的电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等文档的工作流。

在典型的Adobe Sign和自适应表单场景中，用户填写自适应表单 **以申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署应用程序表单时，该表单将发送给服务提供商以执行进一步操作。 服务提供商审阅应用程序，并使用Adobe Sign标记已批准的应用程序。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms一起使用，请配置Adobe Sign登录AEM cloud services:

## 前提条件 {#prerequisites}

您需要满足以下条件才能将Adobe Sign与AEM Forms集成：

* 有效的 [Adobe Sign开发人员帐户。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 启用 [SSL的AEM Forms](/help/sites-administering/ssl-by-default.md) 服务器。
* Adobe [Sign API应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* Adobe Sign API应用程序的凭据（客户端ID和客户端机密）。

## 使用AEM Forms配置Adobe Sign {#configure-adobe-sign-with-aem-forms}

入门项目准备就绪后，请执行以下步骤以配置Adobe Sign，并在创作实例上使用AEM Forms:

1. 在AEM Forms作者实例上，导航 **到工具**![锤](assets/hammer.png) >常 **规** >配 **置浏览器**。
1. 在“配置 **[!UICONTROL 浏览器]** ”页面上，点 **[!UICONTROL 按创建]**。
1. 在创 **[!UICONTROL 建配置]** ，指定配置的标 **[!UICONTROL 题]** ，启用云 **[!UICONTROL 配置]**，然后点 **[!UICONTROL 按创]**&#x200B;建。 它为云服务创建配置容器。
1. 导航到工 **具锤** 子 ![>](assets/hammer.png) Cloud Service **>****> Adobe Sign** ，然后选择您在上述步骤中创建的配置容器。

   >[!NOTE]
   >
   >确保云服务配置页面的URL与HTTPS开始 **在一起**。 否则，为 [AEM Forms服](/help/sites-administering/ssl-by-default.md) 务器启用SSL。

1. 在配置页面上，点按 **[!UICONTROL 创建]** ，以在AEM Forms中创建Adobe Sign配置。
1. 在“创 **[!UICONTROL 建Adobe]** Sign配置”页 **[!UICONTROL 面的“常规]** ”选项卡中 **，指定配置的** 名称 **，然后点**&#x200B;按下一个。 您可以选择指定标题并浏览以选择配置的缩略图。

   在当前浏览器窗口中复制URL。 需要使用AEM Forms配置Adobe Sign应用程序。

1. 为Adobe Sign应用程序配置OAuth设置：

   1. 打开浏览器窗口并登录到Adobe Sign开发人员帐户。
   1. 选择为AEM Forms配置的应用程序，然后点按为应用程序配置OAuth。
   1. 在“重 **定向URL** ”框中，添加上一步中复制的HTTPS URL，然后单击“ **保存”**。
   1. 为Adobe Sign应用程序启用以下OAuth设置，然后单击“保 **存”**。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   有关为Adobe Sign应用程序配置OAuth设置并获取密钥的分步信息，请参阅应用程 [序开发人员文档的配置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobeio/adobeio-documentation/master/sign/gstarted/configure_oauth.md) oAuth设置。

   ![OAuth配置](assets/oauthconfig_new.png)

1. 返回“创建 **Adobe Sign配置”页** 。 在“设 **[!UICONTROL 置]** ”选项卡中， **[!UICONTROL OAuth URL]** (OAuth URL)字段提及以下默认URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1指** 默认数据库共享。

   您可以修改数据库共享的值。 重新启动服务器，以便能够为数据库共享使用新值。

1. 指定 **客户端** ID(也称为应用程序 ID **)和客户**&#x200B;端机密。 选择“ **为附件启用Adobe Sign** ”选项，将附加到自适应表单的文件追加到发送以供签名的相应Adobe Sign文档。

   Tap **[!UICONTROL Connect to Adobe Sign]**. 当提示输入凭据时，请提供创建Adobe Sign应用程序时使用的帐户的用户名和密码。

   点按 **[!UICONTROL 创建]** ，以创建Adobe Sign配置。

1. 打开AEM Web Console。 URL为 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **Forms常用配置服务。**
1. 在“允 **许** ”字段中，选 **择“所有用户** -所有用户”（匿名或登录），可以预览附件、验证和签署表单，然后单击“保 **存”。** 创作实例配置为使用Adobe Sign。
1. 在Publish [实例](/help/sites-deploying/deploy.md) 中，登录并打开以下URL:

   `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`

1. 重复第1步到第12步，以配置带有AEM Forms的Adobe Sign。 使用相同的配置标题（如第3步中指定）和相同的名称（如第6步中指定）来复制在创作实例上配置的设置。

   现在，Adobe Sign已与AEM Forms集成，可在自适应表单中使用。 要在 [自适应表单中使用Adobe Sign服务](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，请指定在自适应表单属性中创建的上述配置容器。

## 配置Adobe Sign调度程序以同步签名状态 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

仅当所有签名者完成签名过程后，才会提交启用Adobe Sign的自适应表单。 默认情况下，Adobe Sign调度程序服务计划每24小时检查（投票）签署方响应。 您可以更改环境的默认时间间隔。 请执行以下步骤来更改默认时间间隔：

1. 使用管理员凭据登录到AEM Forms服务器，并导航到 **工具** > **操作** > **Web控制台**。

   您还可以在浏览器窗口中打开以下URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到并打开 **Adobe Sign Configuration Service选项** 。 在“状态 [更新表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) ”表达式 **字段中指定一个cron调度程序，然后单** 击“保 **存”**。 例如，要在每天00:00 am运行配置服务，请在“状态更 `0 0 0 1/1 * ? *` 新调度程序 **”表达式字段中指定** 。

Adobe Sign同步状态的默认时间间隔现已更改。

## 相关文章 {#related-articles}

* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [将Adobe Sign与AEM Forms一起使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)

