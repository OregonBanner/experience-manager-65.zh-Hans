---
title: 使用链接共享资产
description: 以URL的形式共享资产、文件夹和收藏集。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f6da1c69ea3b3c3f07e8ac10fd8e1e9c7208158
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 7%

---


# 通过链接共享资产 {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] 允许您以URL的形式与组织成员和外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to [!DNL Assets].

>[!PREREQUISITES]
>
>* 您需要对要作为链接共享的文件夹或资产具有“编辑ACL”权限。
>* 要向用户发送电子邮件，请在Day CQ邮件服务中配置SMTP服 [务器详细信息](#configmailservice)。


## 共享资产 {#sharelink}

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在位置具有读取权 `/var/dam/share` 限的用户能够视图与他们共享的链接。

1. In the [!DNL Assets] user interface, select the asset to share as a link.
1. 在工具栏中，单击共享 **[!UICONTROL 链接共享]**![资产图标](assets/do-not-localize/assets_share.png)。

   单击“共享”后将创建的 [!UICONTROL 链接] 会提前显示在“ [!UICONTROL 共享链接] ”字段。 链接的默认过期时间为一天。

   ![与链接共享对话框](assets/Link-sharing-dialog-box.png)

   *图：将资产共享为链接的对话框。*

   >[!NOTE]
   >
   >如果要将创作部署中的链 [!DNL Experience Manager] 接共享到外部实体，请确保仅对请求显示以下URL（用于链接共享） `GET` 。 出于安全原因阻止其他URL。
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. 在界 [!DNL Experience Manager] 面中，访问 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. 对于 `local` 和属 `author` 性，请分别提供本地实例和作者实例的URL。 如果 `local` 运行 `author` 单个作者实例，则这两个属性的值 [!DNL Experience Manager] 相同。 对于发布实例，请提供发布实例 [!DNL Experience Manager] 的URL。

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您可以添加一个或多个用户。

   ![直接从“链接共享”对话框共享指向资产的链接](assets/Asset-Sharing-LinkShareDialog.png)

   *图：直接从“链接共享”对话框共享 [!UICONTROL 指向资产的] 链接。*

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words [!UICONTROL External User] are prefixed with the email ID of the user.

1. 在“主 **[!UICONTROL 题]** ”字段中，输入主题行。

1. 在“消 **[!UICONTROL 息]** ”字段中，输入可选消息。

1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link to stop working. 默认情况下，过期日期设置为您共享链接后一周的时间。

   ![设置共享链接的到期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始资产和演绎版，请选 **[!UICONTROL 择允许下载原始文件]**。 默认情况下，用户只能下载您共享为链接的资产的演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已通过电子邮件将链接共享给用户。

1. 要视图共享的资产，请单击发送给用户的电子邮件中的链接。 共享的资源显示在 **[!UICONTROL Adobe Marketing Cloud]** 页面。

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. 要生成资产的预览，请单击共享的资产。 To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 支持只生成受支持文件类 [型的资产预览](/help/assets/assets-formats.md)。 如果共享了其他MIME类型，则只能下载资产，而不能进行预览。

1. 要下载共享的资产，请单 **[!UICONTROL 击工]** 具栏中的选择 **[!UICONTROL ，单击资产，然后单击工具]** 栏中的下载。

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. 要视图您已作为链接共享的资产，请转到用 [!DNL Assets] 户界面，然后单击 [!DNL Experience Manager] 徽标。 选择 **[!UICONTROL 导航]**。 In the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.

1. 要取消共享资产，请选择该资产，然后单 **[!UICONTROL 击工]** 具栏中的取消共享。 随后将显示确认消息。 资产的条目会从列表中删除。

## 配置Day CQ邮件服务 {#configmailservice}

1. 在主页 [!DNL Experience Manager] 中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 在服务列表中，找到 **[!UICONTROL Day CQ Mail Service]**。
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器密码

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小 {#maxdatasize}

当您使用链接共享功能从共享的链接下载资产时，会 [!DNL Experience Manager] 从存储库中压缩资产层次结构，然后以ZIP文件格式返回资产。 但是，在ZIP文件中压缩的数据量没有限制的情况下，大量数据会受到压缩，这会导致JVM中内存不足错误。 要保护系统免受由于这种情况而可能发生的拒绝服务攻击，请使用配置管理器中Day CQ DAM Adhoc Asset Share Proxy Servlet的 **[!UICONTROL Max Content Size（未压缩）]**[!UICONTROL 参数配置] 最大大小。 如果资产的未压缩大小超出配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. 从Web控制台中，找到 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet配置]** 。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## Best practices and troubleshooting {#bestpractices}

* 名称中包含空白的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享的资产，请咨询您 [!DNL Experience Manager] 的管理员，了解 [下载限制](#maxdatasize) 。
* 如果您无法发送包含共享资产链接的电子邮件，或者如果其他用户无法收到您的电子邮件，请咨询您 [!DNL Experience Manager] 的管理员，了解 [是否已配置](#configmailservice) 电子邮件服务。
* 如果您无法使用链接共享功能共享资产，请确保您具有相应的权限。 请参阅 [共享资产](#sharelink)。
* 如果共享资产被移动到其他位置，其链接将停止工作。 重新创建链接并与用户重新共享。
