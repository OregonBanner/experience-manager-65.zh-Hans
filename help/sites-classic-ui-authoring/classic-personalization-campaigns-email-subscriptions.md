---
title: 管理订阅
seo-title: Managing Subscriptions
description: 借助在AEM网页上使用的表单组件，可以要求用户订阅电子邮件服务提供商的邮件列表。 要准备带有注册表单的AEM页面以订阅电子邮件服务邮件列表，必须将相应的服务配置应用于潜在订阅者将访问的AEM页面。
seo-description: Users can be asked to subscribe to Email Service Provider's mailing lists with the help of the Form component used on an AEM web page. To prepare an AEM page with a sign-up form for subscription to your e-mail service mailing lists, you must apply the corresponding service configuration to the AEM page that the potential subscriber will visit.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 0%

---

# 管理订阅{#managing-subscriptions}

>[!NOTE]
>
>Adobe不打算进一步增强此功能（管理潜在客户和列表）。
>建议利用 [Adobe Campaign及其AEM集成](/help/sites-administering/campaign.md).

可要求用户订阅 **电子邮件服务提供者的** 邮件列表在 **表单** 在AEM网页上使用的组件。 要准备带有注册表单的AEM页面以订阅电子邮件服务邮件列表，必须将相应的服务配置应用于潜在订阅者将访问的AEM页面。

## 将电子邮件服务配置应用到页面 {#applying-email-service-configuration-to-a-page}

要配置AEM页面，请执行以下操作：

1. 导航至 **网站** 选项卡。
1. 选择需要为服务配置的页面。 右键单击页面并选择 **属性**.

1. 选择 **Cloud Service** 则 **添加服务**. 从可用配置列表中选择配置。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 单击&#x200B;**确定**。

## 在AEM页面上创建用于订阅/取消订阅列表的注册表单 {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

要创建注册表单并将其配置为订阅电子邮件服务提供商的邮件列表，请执行以下操作：

1. 打开用户将访问的AEM页面。
1. 将电子邮件服务提供商的配置应用到页面。

1. 添加 **表单** 通过将组件从sidekick拖动到页面中。 如果组件不可用，请切换到设计模式并启用 **表单** 组。
1. 单击 **编辑** 在 **表单的开头** 栏并导航到 **高级** 选项卡。
1. 在 **表单** 下拉菜单，选择 **电子邮件服务：创建订阅者** 并将其添加到列表。
1. 在对话框底部，打开 **操作配置** 下拉列表，允许您选择一个或多个订阅列表。
1. 在 **选择列表**，选择要用户订阅的列表。 您可以使用加号按钮(**添加项目**)。

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >您的对话框可能会因电子邮件服务提供商的不同而有所不同。

1. 在 **表单** 选项卡，选择用户提交表单后要前往的感谢页面（如果留空，表单会在提交时重新显示）。 单击&#x200B;**确定**。An **电子邮件ID** 组件显示在表单中，通过它，可创建表单，用户可在其中提交电子邮件地址以订阅或取消订阅邮件列表。
1. 添加 **提交** 按钮组件 **表单** 在sidekick中的部分。

   表单已准备就绪。 发布上述步骤中配置的页面以及 **谢谢** 页面到发布实例。 任何访问页面的潜在订阅者都可以填写表单并订阅配置中提供的列表。

   >[!NOTE]
   >
   >要正确设置表单订阅功能， [需要在发布实例上导出和导入来自作者的加密密钥](#exporting-keys-from-author-and-importing-on-publish).

## 从作者导出键并在发布时导入 {#exporting-keys-from-author-and-importing-on-publish}

要使电子邮件服务通过发布实例上的注册表单进行订阅和取消订阅，您需要执行以下步骤：

1. 在创作实例上，导航到包管理器。
1. 创建新资源包。 将筛选器设置为 `/etc/key`.
1. 生成并下载包。
1. 导航到发布实例上的包管理器，并上传此包。
1. 导航到发布osgi控制台，然后重新启动名为的捆绑包 **AdobeGranite加密支持**.

## 从列表中取消订阅用户 {#unsubscribing-users-from-lists}

要从列表中取消订阅用户，请执行以下操作：

1. 打开具有注册表单的AEM页面的页面属性以取消订阅潜在客户。
1. 将服务配置应用到页面。
1. 在页面上创建一个注册表单。
1. 配置组件时，选择操作 **电子邮件服务**： **从列表中取消订阅用户。**
1. 从下拉菜单中，选择取消订阅时从中删除用户的相应列表。

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. 将键从创作导出到发布。

## 为电子邮件服务配置自动回复方电子邮件 {#configuring-auto-responder-emails-for-email-service}

要为订阅者配置自动回复电子邮件，请执行以下操作：

1. 打开具有注册表单的AEM页面的页面属性，为潜在客户配置自动响应。
1. 将ExactTarget配置应用到页面。

1. 添加 **表单** 通过将组件从sidekick拖动到页面中。 如果该组件不可用，请切换到设计模式并启用 **表单** 组。
1. 单击 **编辑** 在 **表单的开头** 栏并导航到 **高级** 选项卡。
1. 在 **表单** 下拉菜单，选择 **电子邮件服务：发送自动回复者电子邮件。**
1. **选择电子邮件** （这是作为自动回复电子邮件发送的邮件）。

1. **选择分类** （此分类用于发送电子邮件）。
1. 选择 **谢谢** 页面（用户提交表单后会被定向到的页面）。

   在 **表单** 选项卡，选择用户提交表单后要前往的感谢页面。 （如果留空，表单会在提交时重新显示。） 单击&#x200B;**确定**。

1. 将键从创作导出到发布。
1. 添加 **提交** 按钮组件 **表单** 在sidekick中的部分。

   注册表单已准备就绪。 发布上述步骤中配置的页面以及 **谢谢** 页面到发布实例。 任何访问页面的潜在订阅者都可以填写表单，并且在提交表单时，访客将收到一封使用填写表单的电子邮件ID的自动回复电子邮件。

   >[!NOTE]
   >
   >要使注册表单订阅正常工作， [需要在发布实例上导出和导入来自作者的加密密钥](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
