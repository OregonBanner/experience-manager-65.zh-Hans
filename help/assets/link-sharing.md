---
title: 生成共享资产的URL
description: 本文介绍如何在Experience Manager资产中以URL的形式共享资产、文件夹和收藏集。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 10%

---


# 通过链接共享资产 {#asset-link-sharing}

Adobe Experience Manager资产允许您以URL的形式与组织成员和外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 通过链接共享资产是一种方便的方式，使外部方无需先登录资产即可获得资源。

>[!NOTE]
>
>您需要对要作为链接共享的文件夹或资产具有“编辑ACL”权限。

## 共享资产 {#sharelink}

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在位置具有读取权 `/var/dam/share` 限的用户能够视图与他们共享的链接。

>[!NOTE]
>
>在与用户共享链接之前，请确保已配置Day CQ邮件服务。 如果尝试共享链接时未首先配置Day CQ邮 [件服务，则会出错](/help/assets/link-sharing.md#configmailservice)。

1. 在“资产”用户界面中，选择要作为链接共享的资产。
1. 在工具栏中，单 **[!UICONTROL 击共享链]**![接assets_share](assets/assets_share.png)。

   资产链接会在共享链接字段中 **[!UICONTROL 自动创建]** 。 复制此链接并与用户共享。 链接的默认过期时间为一天。

   ![与链接共享对话框](assets/Link-sharing-dialog-box.png)

   *图： 将资产共享为链接的对话框。*

   或者，也可以继续执行此操作过程的第 3-7 步，以添加电子邮件收件人、配置链接的有效时间，以及从对话框中发送电子邮件。

   >[!NOTE]
   >
   >如果要将Experience Manager作者实例中的链接共享到外部实体，请确保仅对请求显示以下URL（用于链接共享） `GET` 。 阻止其他URL以确保Experience Manager作者的安全。
   >
   >* http://[aem_server]:[port]/linkshare.html
   >* http://[aem_server]:[port]/linksharepreview.html
   >* http://[aem_server]:[port]/linkexpired.html


   >[!NOTE]
   >
   >如果共享资产被移动到其他位置，其链接将停止工作。 重新创建链接并与用户重新共享。

1. 在Experience Manager界面中，访 **[!UICONTROL 问工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. 对于 `local` 和属 `author` 性，请分别提供本地实例和作者实例的URL。 如果 `local` 运行 `author` 单个Experience Manager作者实例，则这两个属性的值相同。 对 `publish`于，提供Experience Manager发布实例的URL。

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您还可以与多个用户共享该链接。

   如果用户是您组织的成员，请从键入区域下方的列表显示的建议电子邮件ID中选择用户的电子邮件ID。 对于外部用户，请键入完整的电子邮件ID，然后从列表中选择它。

   要向用户发出电子邮件，请在Day CQ邮件服务中配置SMTP服 [务器详细信息](#configmailservice)。

   ![直接从“链接共享”对话框共享指向资产的链接](assets/Asset-Sharing-LinkShareDialog.png)

   *图： 直接从“链接共享”对话框共享[!UICONTROL 指向资产的]链接。*

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words [!UICONTROL External User] are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** field, enter a subject for the asset you want to share.

1. 在“消 **[!UICONTROL 息]** ”字段中，输入可选消息。

1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. 默认情况下，过期日期设置为您共享链接后一周的时间。

   ![设置共享链接的到期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始图像和演绎版，请选择“允 **[!UICONTROL 许下载原始文件”]**。

   >[!NOTE]
   >
   >默认情况下，用户只能下载您共享为链接的资产的演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已通过电子邮件与用户共享链接。
1. 要视图共享的资产，请单击发送给用户的电子邮件中的链接。 共享的资产会显示在 **[!UICONTROL Adobe Marketing Cloud]** 页面。

   ![chlimage_1-260](assets/chlimage_1-545.png)

   要切换到列表视图，请单击工具栏中的布局选项。

1. 要生成资产的预览，请单击共享的资产。 To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >Experience Manager支持生成以下MIME类型的资产的预览: JPG、PNG、GIF、BMP、INDD、PDF和PPT。 您只能下载其他MIME类型的资产。

1. 要下载共享的资产，请单 **[!UICONTROL 击工]** 具栏中的选择 **[!UICONTROL ，单击资产，然后单击工具]** 栏中的下载。

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. 要视图您作为链接共享的资产，请转到资产UI并单击Experience Manager徽标。 从列表 **[!UICONTROL 中选择]** “导航”以显示“导航”窗格。
1. 从“导航”窗格中，选择&#x200B;**[!UICONTROL 共享链接]**，以显示共享资产列表。
1. 要取消共享资产，请选择该资产，然后单 **[!UICONTROL 击工]** 具栏中的取消共享。 随后将显示确认消息。 资产的条目会从列表中删除。

## 配置Day CQ邮件服务 {#configmailservice}

1. 在Experience Manager主页中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 在服务列表中，找到 **[!UICONTROL Day CQ Mail Service]**。
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * SMTP服务器主机名： 电子邮件服务器主机名
   * SMTP服务器端口： 电子邮件服务器端口
   * SMTP用户： 电子邮件服务器用户名
   * SMTP密码： 电子邮件服务器密码
   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小 {#maxdatasize}

当您使用链接共享功能从共享的链接下载资产时，Experience Manager会从存储库中压缩资产层次结构，然后以ZIP文件格式返回资产。 但是，在ZIP文件中压缩的数据量没有限制的情况下，大量数据会受到压缩，这会导致JVM中内存不足错误。 要保护系统免受由于这种情况而可能发生的拒绝服务攻击，请使用配置管理器中Day CQ DAM Adhoc Asset Share Proxy Servlet的 **[!UICONTROL Max Content Size（未压缩）]**[!UICONTROL 参数配置] 最大大小。 如果资产的未压缩大小超出配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. Click the Experience Manager logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. 从Web控制台中，找到 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet配置]** 。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## Best practices and troubleshooting {#bestpractices}

* 名称中包含空白的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享的资产，请咨询Experience Manager管理员，了解下 [载限制](#maxdatasize) 。
* 如果您无法发送包含共享资产链接的电子邮件，或者如果其他用户无法收到您的电子邮件，请咨询您的Experience Manager管理员(如果 [电子邮件服](#configmailservice) 务已配置或未配置)。
* 如果您无法使用链接共享功能共享资产，请确保您具有相应的权限。 请参阅 [共享资产](#sharelink)。
