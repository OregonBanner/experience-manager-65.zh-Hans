---
title: 您的收件箱
seo-title: 您的收件箱
description: 您可以接收来自 AEM 各个区域的通知，例如，关于工作项或任务的通知，这些通知指示您需要对页面内容执行的操作。
seo-description: 您可以接收来自 AEM 各个区域的通知，例如，关于工作项或任务的通知，这些通知指示您需要对页面内容执行的操作。
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 您的收件箱{#your-inbox}

您可以接收来自 AEM 各个区域的通知，例如，关于工作项或任务的通知，这些通知指示您需要对页面内容执行的操作。

您会在按通知类型分开的两个收件箱中接收这些通知：

* 在一个收件箱中，您会看到因订阅而收到的通知，后续部分对该收件箱进行了说明。
* A specialized inbox for workflow items is described in the [Participating in Workflows](/help/sites-classic-ui-authoring/classic-workflows-participating.md) document.

## 查看通知 {#viewing-your-notifications}

查看通知：

1. 打开通知收件箱：在&#x200B;**网站**&#x200B;控制台中，单击右上角的用户按钮，然后选择&#x200B;**通知收件箱**。

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >您也可以直接在浏览器中访问控制台；例如：
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 将列出您的通知。您可以根据需要执行以下操作：

   * [订阅通知](#subscribing-to-notifications)
   * [处理通知](#processing-your-notifications)
   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## 订阅通知 {#subscribing-to-notifications}

订阅通知：

1. 打开通知收件箱：在“**网站**”控制台中，单击右上角的用户按钮，并选择“**通知收件箱**”。

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >您也可以直接在浏览器中访问控制台；例如：
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 单击左上角的&#x200B;**配置...** 以打开配置对话框。

   ![screen_shot_2012-02-08at11056am](assets/screen_shot_2012-02-08at111056am.png)

1. 选择通知渠道：

   * **收件箱**：通知将显示在您的 AEM 收件箱中。
   * **电子邮件**：通知将通过电子邮件发送到您的用户个人资料中定义的电子邮件地址。
   >[!NOTE]
   >
   >需要配置一些设置，才能通过电子邮件通知。也可以自定义电子邮件模板，或针对新语言添加电子邮件模板。有关在 AEM 中配置电子邮件通知的信息，请参阅[配置电子邮件通知](/help/sites-administering/notification.md#configuringemailnotification)。

1. 选择要通知的页面操作：

   * 激活：在已激活某页面时。
   * 取消激活：在已取消激活某页面时。
   * 删除（整合）：在页面被重复删除时，即在重复执行对某个页面的删除操作时。在删除或移动某页面时，会自动重复删除操作：在执行删除操作的源实例中以及复制代理定义的目标实例中，删除该页面。

   * 修改：在已修改某页面时。
   * 创建：在已创建某页面时。
   * 删除：在已通过页面删除操作删除某页面时。
   * 转出：在已转出某页面时。

1. 定义要通知的页面的路径：

   * 单击&#x200B;**添加**&#x200B;向表添加新行。
   * Click the **Path** table cell and enter the path, e.g. `/content/docs`.

   * 要接收属于子树的所有页面的通知，请将“**是否精确？**&#x200B;设置为&#x200B;**否**。要仅接收路径定义的页面上的操作通知，请将&#x200B;**是否精确？**&#x200B;设置为&#x200B;**是**。

   * 要允许该规则，请将&#x200B;**规则**&#x200B;设置为&#x200B;**允许**。如果设置为&#x200B;**拒绝**，则拒绝该规则，但不删除它，可在以后允许该规则。
   要删除定义，请单击表单元格来选择该行，并单击&#x200B;**删除**。

1. 单击&#x200B;**确定**&#x200B;以保存配置。

## 处理通知 {#processing-your-notifications}

如果已选择通过您的 AEM 收件箱接收通知，则会将通知放入您的收件箱中。您可以[查看通知](#viewing-your-notifications)，然后选择所需的通知以执行下列操作：

* 通过单击&#x200B;**批准**&#x200B;来批准它：将&#x200B;**读取**&#x200B;列中的值设置为 **true**。

* 通过单击“**删除**”删除它。

![chlimage_1-5](assets/chlimage_1-5.jpeg)
