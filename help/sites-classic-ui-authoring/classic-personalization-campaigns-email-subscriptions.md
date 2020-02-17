---
title: 管理订阅
seo-title: 管理订阅
description: 可以借助在 AEM 网页上使用的“表单”组件，要求用户订阅电子邮件服务提供商的邮寄列表。要准备一个包含注册表单的 AEM 页面以订阅您的电子邮件服务邮寄列表，您必须将相应的服务配置应用到潜在订阅者将会访问的 AEM 页面。
seo-description: 可以借助在 AEM 网页上使用的“表单”组件，要求用户订阅电子邮件服务提供商的邮寄列表。要准备一个包含注册表单的 AEM 页面以订阅您的电子邮件服务邮寄列表，您必须将相应的服务配置应用到潜在订阅者将会访问的 AEM 页面。
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理订阅{#managing-subscriptions}

>[!NOTE]
>
>Adobe不计划进一步增强此功能（管理潜在客户和列表）。
>建议利用 [Adobe Campaign及其AEM集成](/help/sites-administering/campaign.md)。

Users can be asked to subscribe to **Email Service Provider&#39;s** mailing lists with the help of the **Form** component used on an AEM web page. 要准备一个包含注册表单的 AEM 页面以订阅您的电子邮件服务邮寄列表，您必须将相应的服务配置应用到潜在订阅者将会访问的 AEM 页面。

## 将电子邮件服务配置应用到页面 {#applying-email-service-configuration-to-a-page}

要配置 AEM 页面，请执行以下操作：

1. 导航到&#x200B;**网页**&#x200B;选项卡。
1. 选择需要为服务配置的页面。Right-click the page and select **Properties**.

1. Select **Cloud Services** then **Add Service**. 从可用配置的列表中选择一种配置。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 单击&#x200B;**确定**。

## 在 AEM 页面上创建用于订阅/取消订阅列表的注册表单 {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

要创建并配置注册表单以订阅电子邮件服务提供商的邮寄列表，请执行以下操作：

1. 打开用户将访问的 AEM 页面。
1. 将电子邮件服务提供商的配置应用到该页面。

1. 从 Sidekick 中拖动&#x200B;**表单**&#x200B;组件，以将该组件添加到页面。如果该组件不可用，请切换到设计模式，然后启用&#x200B;**表单**&#x200B;组。
1. Click **Edit** in the **Start of Form** bar and navigate to the **Advanced** tab.
1. In the **Form** drop-down menu, select **E-mail Service: Create Subscriber** and add to list.
1. At the bottom of the dialog box, open the **Action Configuration** drop-down, which allows you to select one or more subscription lists.
1. 在&#x200B;**选择列表**&#x200B;中，选择您希望用户订阅的列表。您可以使用加号按钮（**添加项目**）添加多个列表。

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >您的对话框可能会根据电子邮件服务提供商的不同而有所差异。

1. 在&#x200B;**表单**&#x200B;选项卡中，选择您希望用户在提交表单后转到的感谢页面（如果保留为空，则提交表单后将再次显示表单）。单击&#x200B;**确定**。表单中会显示&#x200B;**电子邮件 ID** 组件，该组件可让您创建表单，在该表单中，用户可提交其电子邮件地址以订阅或取消订阅邮寄列表。
1. 从 Sidekick 中的&#x200B;**表单**&#x200B;部分添加&#x200B;**提交**&#x200B;按钮组件。

   表单现已准备就绪。接下来可将上述步骤中配置的页面和&#x200B;**感谢**&#x200B;页面一起发布到发布实例。访问此页面的任何潜在订阅者都可以填写该表单并订阅配置中提供的列表。

   >[!NOTE]
   >
   >要让表单订阅正常工作，[需要导出创作加密密钥并将其导入到发布实例](#exporting-keys-from-author-and-importing-on-publish)。

## 导出创作密钥并将其导入到发布实例 {#exporting-keys-from-author-and-importing-on-publish}

要通过发布实例中的注册表单进行电子邮件服务订阅和取消订阅，您需要按照下列步骤操作：

1. 在创作实例中，导航到“包管理器”。
1. 新建包。Set the filter as `/etc/key`.
1. 构建和下载包。
1. 导航到发布实例中的“包管理器”并上传此包。
1. 导航到发布 OSGi 控制台，然后重新启动名为 **Adobe Granite Crypto Support** 的捆绑包。

## 使用户从列表中取消订阅 {#unsubscribing-users-from-lists}

要使用户从列表中取消订阅，请执行以下操作：

1. 打开包含注册表单的 AEM 页面的页面属性，以使潜在客户取消订阅。
1. 将服务配置应用到页面。
1. 在页面上创建注册表单。
1. While configuring the component, select the action **E-mail Service**: **Unsubscribe user from list.**
1. 从下拉菜单中，选择在取消订阅时要从中删除用户的相应列表。

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. 将创作密钥导出到发布实例。

## 为电子邮件服务配置自动回复的电子邮件 {#configuring-auto-responder-emails-for-email-service}

为订阅者配置自动回复的电子邮件：

1. 打开包含注册表单的AEM页面的页面属性，为潜在客户配置自动响应程序。
1. 将 ExactTarget 配置应用到此页面。

1. 从 Sidekick 中拖动&#x200B;**表单**&#x200B;组件，以将该组件添加到页面。如果该组件不可用，请切换到设计模式，然后启用&#x200B;**表单**&#x200B;组。
1. Click **Edit** in the **Start of Form** bar and navigate to the **Advanced** tab.
1. In the **Form** drop-down menu, select **E-mail Service: Send auto responder email.**
1. **选择电子邮件** （这是作为自动回复电子邮件发送的邮件）。

1. **选择分类** （此分类用于发送电子邮件）。
1. Select the **Thank you** page (the page where users are directed to once they submit the form).

   In the **Form** tab, select the thank you page you want users to go to after they submit the form. (If left blank, the form redisplays upon submission.) 单击&#x200B;**确定**。

1. 将创作密钥导出到发布实例。
1. 从 Sidekick 中的&#x200B;**表单**&#x200B;部分添加&#x200B;**提交**&#x200B;按钮组件。

   注册表单现已准备就绪。接下来可将上述步骤中配置的页面和&#x200B;**感谢**&#x200B;页面一起发布到发布实例。访问此页面的任何潜在订阅者都可以填写该表单，并且在提交该表单时，访客应会收到使用表单中所填电子邮件 ID 的自动回复的电子邮件。

   >[!NOTE]
   >
   >要让注册表单订阅正常工作，[需要导出创作加密密钥并将其导入到发布实例](#exporting-keys-from-author-and-importing-on-publish)。

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)

