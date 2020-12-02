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
source-git-commit: f0038c1f88ea0047cbaae4fe49456a665aa67f10
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---


# 将Adobe Sign与AEM Forms整合{#integrate-adobe-sign-with-aem-forms}

Adobe Sign为自适应表单启用电子签名工作流。 电子签名可改善处理法律、销售、工资、人力资源管理等文档的工作流。

在典型的Adobe Sign和自适应表单场景中，用户填写自适应表单以申请服务&#x200B;**。**&#x200B;例如，信用卡申请和公民福利表。 当用户填写、提交和签署应用程序表单时，该表单将发送给服务提供商以执行进一步操作。 服务提供商审阅应用程序，并使用Adobe Sign标记已批准的应用程序。 要启用类似的电子签名工作流，您可以将Adobe Sign与AEM Forms集成。

要将Adobe Sign与AEM Forms结合使用，请在AEM云服务中配置Adobe Sign:

## 前提条件 {#prerequisites}

您需要以下条件将Adobe Sign与AEM Forms集成：

* 活动[Adobe Sign开发者帐户。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* 启用[SSL的](/help/sites-administering/ssl-by-default.md)AEM Forms服务器。
* [Adobe SignAPI应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* Adobe SignAPI应用程序的凭据（客户端ID和客户端机密）。
* 重新配置时，从创作实例和发布实例中删除现有的Adobe Sign配置。
* 对创作和发布实例使用[相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 将Adobe Sign配置为AEM Forms{#configure-adobe-sign-with-aem-forms}

在入门项目准备就绪后，请执行以下步骤以在创作实例上将Adobe Sign与AEM Forms一起配置：

1. 在AEM Forms创作实例上，导航到&#x200B;**工具** ![锤子](assets/hammer.png) > **常规** > **配置浏览器**。
1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;页面上，点按&#x200B;**[!UICONTROL 创建]**。
   * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定配置&#x200B;**[!UICONTROL 标题]**，启用&#x200B;**[!UICONTROL 云配置]**，然后点按&#x200B;**[!UICONTROL 创建]**。 它为云服务创建配置容器。
1. 导航到&#x200B;**工具**![锤子](assets/hammer.png) > **Cloud Services** > **Adobe Sign**，然后选择您在上述步骤中创建的配置容器。

   >[!NOTE]
   >
   >您可以执行步骤1-4在容器中创建新配置容器并创建Adobe Sign配置，或使用&#x200B;**工具**![锤子](assets/hammer.png)>**Cloud Services**>**Adobe Sign**&#x200B;中现有的`global`文件夹。 如果在新的配置容器中创建配置，请确保在创建自适应表单时在&#x200B;**[!UICONTROL 配置容器]**&#x200B;字段中指定容器名称。

   >[!NOTE]
   确保云服务配置页面的URL开始有&#x200B;**HTTPS**。 否则，[为AEM Forms服务器启用SSL](/help/sites-administering/ssl-by-default.md)。

1. 在配置页面上，点按&#x200B;**[!UICONTROL 创建]**&#x200B;以在AEM Forms创建Adobe Sign配置。
1. 在&#x200B;**[!UICONTROL 创建Adobe Sign配置]**&#x200B;页面的&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，为配置指定&#x200B;**名称**，然后点按&#x200B;**下一个**。 您可以选择指定标题并浏览以选择配置的缩略图。

1. 将当前浏览器窗口中的URL复制到记事本。 需要配置Adobe Sign应用程序与AEM Forms。

1. 为Adobe Sign应用程序配置OAuth设置：

   1. 打开浏览器窗口并登录Adobe Sign开发人员帐户。
   1. 选择为AEM Forms配置的应用程序，然后点按“为应用程序配置OAuth”。
   1. 在&#x200B;**重定向URL**&#x200B;框中，添加在上一步中复制的HTTPS URL，然后单击&#x200B;**保存**。
   1. 为Adobe Sign应用程序启用以下OAuth设置，然后单击&#x200B;**保存**。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   有关为Adobe Sign应用程序配置OAuth设置并获取密钥的分步信息，请参阅[为应用程序配置oAuth设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth配置](assets/oauthconfig_new.png)

1. 返回&#x200B;**创建Adobe Sign配置**&#x200B;页。 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，**[!UICONTROL OAuth URL]**&#x200B;字段提到以下默认URL:

   https://secure.na1.echosign.com/public/oauth

   其中：

   **na1** 指默认数据库共享。

   您可以修改数据库共享的值。 重新启动服务器，以便能够使用数据库共享的新值。

1. 指定&#x200B;**客户端ID**(也称为应用程序 ID)和&#x200B;**客户端机密**。 选择&#x200B;**为附件启用Adobe Sign选项**，将附加到自适应表单的文件追加到发送以供签名的相应Adobe Sign文档。

   点按&#x200B;**[!UICONTROL 连接到Adobe Sign]**。 当提示输入凭据时，请提供创建Adobe Sign应用程序时使用的帐户的用户名和密码。

   点按&#x200B;**[!UICONTROL 创建]**&#x200B;以创建Adobe Sign配置。

1. 打开AEM Web Console。 URL为`https://'[server]:[port]'/system/console/configMgr`
1. 打开&#x200B;**Forms公用配置服务。**
1. 在&#x200B;**允许**&#x200B;字段中，**选择**&#x200B;所有用户——所有用户（匿名或登录）都可以预览附件、验证和签署表单，然后单击&#x200B;**保存。** 作者实例配置为使用Adobe Sign。
1. 发布配置。
1. 使用[replication](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html)在相应的发布实例上创建相同的配置。

现在，Adobe Sign已与AEM Forms集成，并准备以自适应形式使用。 要[以自适应表单](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)使用Adobe Sign服务，请指定以上在自适应表单属性中创建的配置容器。



## 配置Adobe Sign调度程序以同步签名状态{#configure-adobe-sign-scheduler-to-sync-the-signing-status}

只有在所有签名者完成签名过程后，才会提交启用Adobe Sign的自适应表单。 默认情况下，Adobe Sign调度程序服务计划每24小时检查（投票）签署方响应。 您可以更改环境的默认时间间隔。 请执行以下步骤来更改默认时间间隔：

1. 使用管理员凭据登录到AEM Forms服务器，然后导航到&#x200B;**工具** > **操作** > **Web控制台**。

   您还可以在浏览器窗口中打开以下URL:
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到并打开&#x200B;**Adobe Sign配置服务**&#x200B;选项。 在&#x200B;**状态更新表达式表达式**&#x200B;字段中指定[cron调度程序](https://en.wikipedia.org/wiki/Cron#CRON_expression)，然后单击&#x200B;**保存**。 例如，要在每天00:00 am运行配置服务，请在&#x200B;**状态更新调度程序表达式**&#x200B;字段中指定`0 0 0 1/1 * ? *`。

Adobe Sign同步状态的默认时间间隔现已更改。

## 相关文章{#related-articles}

* [以自适应形式使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [将Adobe Sign与AEM Forms结合使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [将Adobe Sign与AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)

