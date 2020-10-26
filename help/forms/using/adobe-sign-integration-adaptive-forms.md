---
title: 将Adobe Sign与AEM Forms整合
seo-title: 将Adobe Sign与AEM Forms整合
description: 了解如何为AEM Forms配置Adobe Sign
seo-description: 了解如何为AEM Forms配置Adobe Sign
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# 将Adobe Sign与AEM Forms整合{#integrate-adobe-sign-with-aem-forms}

Adobe Sign为自适应表单启用电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等文档的工作流。

在典型的Adobe Sign和自适应表单场景中，用户填写自适应表单 **以申请服务**。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署应用程序表单时，该表单将发送给服务提供商以执行进一步操作。 服务提供商审阅应用程序，并使用Adobe Sign标记已批准的应用程序。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms结合使用，请在AEM云服务中配置Adobe Sign:

## 前提条件 {#prerequisites}

您需要以下条件将Adobe Sign与AEM Forms集成：

* 一个有效的 [Adobe Sign开发者帐户。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 启 [用SSL的](/help/sites-administering/ssl-by-default.md) AEM Forms服务器。
* 一个 [Adobe SignAPI应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* Adobe SignAPI应用程序的凭据（客户端ID和客户端机密）。
* 重新配置时，从创作实例和发布实例中删除现有的Adobe Sign配置。
* 对创 [作实例和发布实例](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) ，使用相同的加密密钥。

## 配置Adobe Sign与AEM Forms {#configure-adobe-sign-with-aem-forms}

在入门项目准备就绪后，请执行以下步骤以在创作实例上将Adobe Sign与AEM Forms一起配置：

1. 在AEM Forms的创作实例中，导 **航到**![Tools](assets/hammer.png) **hammer** > **General**> Configuration Browser 。
1. 在“配置 **[!UICONTROL 浏览器]** ”页面上，点 **[!UICONTROL 按创建]**。
   * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
1. 在创 **[!UICONTROL 建配置]** ，指定配置的标 **[!UICONTROL 题]** ，启用云 **[!UICONTROL 配置]**，然后点 **[!UICONTROL 按创]**&#x200B;建。 它为云服务创建配置容器。
1. 导航到 **工具** 锤 ![>](assets/hammer.png) Cloud Services **>** Adobe Sign **，然后选** 择您在上述步骤中创建的配置容器。

   >[!NOTE]
   >
   >确保云服务配置页面的URL与HTTPS开始 **在一起**。 否则，为 [AEM Forms服](/help/sites-administering/ssl-by-default.md) 务器启用SSL。

1. 在配置页面上，点按创 **[!UICONTROL 建]** ，在AEM Forms创建Adobe Sign配置。
1. 在“创 **[!UICONTROL 建Adobe Sign]** 配置”页 **[!UICONTROL 面的“常规]** ”选项卡中，指 **定配置的名** 称 **，然后点**&#x200B;按下一。 您可以选择指定标题并浏览以选择配置的缩略图。

1. 将当前浏览器窗口中的URL复制到记事本。 需要配置Adobe Sign应用程序与AEM Forms。

1. 为Adobe Sign应用程序配置OAuth设置：

   1. 打开浏览器窗口并登录Adobe Sign开发人员帐户。
   1. 选择为AEM Forms配置的应用程序，然后点按“为应用程序配置OAuth”。
   1. 在“重 **定向URL** ”框中，添加上一步中复制的HTTPS URL，然后单击“ **保存”**。
   1. 为Adobe Sign应用程序启用以下OAuth设置，然后单击“保 **存”**。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   有关为Adobe Sign应用程序配置OAuth设置并获取密钥的分步信息，请参阅为应用程 [序开发人员文档配置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) oAuth设置。

   ![OAuth配置](assets/oauthconfig_new.png)

1. 返回“创建 **Adobe Sign配置** ”页。 在“设 **[!UICONTROL 置]** ”选项卡中， **[!UICONTROL OAuth URL]** (OAuth URL)字段提及以下默认URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1指** 默认数据库共享。

   您可以修改数据库共享的值。 重新启动服务器，以便能够使用数据库共享的新值。

1. 指定 **客户端** ID(也称为应用程序 ID **)和客户**&#x200B;端机密。 选择“ **启用Adobe Sign附件** ”选项，将附加到自适应表单的文件追加到发送以供签名的相应Adobe Sign文档。

   Tap **[!UICONTROL Connect to Adobe Sign]**. 当提示输入凭据时，请提供创建Adobe Sign应用程序时使用的帐户的用户名和密码。

   点按 **[!UICONTROL 创建]** ，以创建Adobe Sign配置。

1. 打开AEM Web Console。 URL为 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **Forms通用配置服务。**
1. 在“允 **许** ”字段中，选 **择“所有用户** -所有用户”（匿名或登录），可以预览附件、验证和签署表单，然后单击“保 **存”。** 作者实例配置为使用Adobe Sign。
1. 发布配置。
1. 使用复 [制](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) ，在相应的发布实例上创建相同的配置。

现在，Adobe Sign已与AEM Forms集成，并准备以自适应形式使用。 要在 [自适应表单中使用Adobe Sign服务](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，请在自适应表单属性中指定上面创建的配置容器。



## 配置Adobe Sign调度程序以同步签名状态 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

只有在所有签名者完成签名过程后，才会提交启用Adobe Sign的自适应表单。 默认情况下，Adobe Sign调度程序服务计划每24小时检查（投票）签署方响应。 您可以更改环境的默认时间间隔。 请执行以下步骤来更改默认时间间隔：

1. 使用管理员凭据登录到AEM Forms服务器，并导航到 **工具** > **操作** > **Web控制台**。

   您还可以在浏览器窗口中打开以下URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到并打开“ **Adobe Sign配置服务** ”选项。 在“状态 [更新表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) ”表达式 **字段中指定一个cron调度程序，然后单** 击“保 **存”**。 例如，要在每天00:00 am运行配置服务，请在“状态更 `0 0 0 1/1 * ? *` 新调度程序 **”表达式字段中指定** 。

Adobe Sign同步状态的默认时间间隔现已更改。

## 相关文章 {#related-articles}

* [以自适应形式使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [将Adobe Sign与AEM Forms结合使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [将Adobe Sign与AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)

