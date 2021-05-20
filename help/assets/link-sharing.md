---
title: 使用链接共享资产
description: 以URL形式共享资产、文件夹和收藏集。
contentOwner: AG
role: Business Practitioner
feature: 链接共享，资产管理
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: 3ec39279d001297dcc11ebd1110bb452de8ca980
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 7%

---

# 通过链接{#asset-link-sharing}共享资产

[!DNL Adobe Experience Manager Assets] 允许您以URL形式与组织成员及外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。通过链接共享资产是使外部各方无需首先登录[!DNL Assets]即可获得资源的一种便捷方式。

>[!PREREQUISITES]
>
>* 您需要对要作为链接共享的文件夹或资产具有编辑ACL权限。
>* 要向用户发送电子邮件，请在[Day CQ Mail Service](#configmailservice)中配置SMTP服务器详细信息。


## 共享资产 {#share-assets}

要为要与用户共享的资产生成URL，请使用链接共享对话框。 具有管理员权限或在`/var/dam/share`位置具有读取权限的用户能够查看与其共享的链接。

1. 在[!DNL Assets]用户界面中，选择要作为链接共享的资产。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 共享链接]** ![共享资产图标](assets/do-not-localize/assets_share.png)。 单击&#x200B;**[!UICONTROL Share]**&#x200B;后将创建的链接会提前显示在[!UICONTROL Share Link]字段中。 在单击&#x200B;**[!UICONTROL Submit]**&#x200B;之前，尚未创建该链接。

   ![链接共享对话框](assets/Link-sharing-dialog-box.png)

   *图：将资产共享为链接的对话框。*

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您可以添加一个或多个用户。

   ![直接从链接共享对话框共享指向资产的链接](assets/Asset-Sharing-LinkShareDialog.png)

   *图：直接从链接共享对话框共享指向 [!UICONTROL 资产] 的链接。*

   >[!NOTE]
   >
   >如果您输入的用户的电子邮件ID不是您组织的成员，则单词[!UICONTROL External User]将在前面添加用户的电子邮件ID。

1. 在&#x200B;**[!UICONTROL 主题]**&#x200B;框中，为您要共享的资产输入主题。

1. 在&#x200B;**[!UICONTROL 消息]**&#x200B;框中，输入可选消息。

1. 在&#x200B;**[!UICONTROL 过期]**&#x200B;字段中，指定链接停止工作的过期日期和时间。 链接的默认过期时间为一天。

   ![设置共享链接的过期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始资产和演绎版，请选择&#x200B;**[!UICONTROL 允许下载原始文件]**。 默认情况下，用户只能下载您以链接形式共享的资产的演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已通过电子邮件与用户共享该链接。

1. 要查看共享的资产，请单击发送给用户的电子邮件中的链接。 要生成资产预览，请单击共享资产。 要关闭预览，请单击&#x200B;**[!UICONTROL 返回]**。 如果已共享文件夹，请单击&#x200B;**[!UICONTROL 父文件夹]**&#x200B;以返回到父文件夹。

   ![预览共享资产](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 支持仅生成支持文件类型 [的资产预览](/help/assets/assets-formats.md)。如果共享其他MIME类型，则您只能下载资产，无法预览。

1. 要下载共享资产，请单击工具栏中的&#x200B;**[!UICONTROL 选择]**，单击资产，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。

   ![用于下载共享资产的工具栏选项](assets/chlimage_1-547.png)

1. 要查看您以链接形式共享的资产，请转到[!DNL Assets]用户界面，然后单击[!DNL Experience Manager]徽标。 选择&#x200B;**[!UICONTROL 导航]**。 在“导航”窗格中，选择&#x200B;**[!UICONTROL 共享链接]**&#x200B;以显示共享资产列表。

1. 要取消共享资产，请选择该资产，然后单击工具栏中的&#x200B;**[!UICONTROL 取消共享]**。 下面显示确认消息。 资产的条目将从列表中删除。

## 配置Day CQ邮件服务{#configure-day-cq-mail-service}

1. 在[!DNL Experience Manager]主页上，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在服务列表中，找到&#x200B;**[!UICONTROL Day CQ Mail Service]**。
1. 单击服务旁边的&#x200B;**[!UICONTROL 编辑]** ，并为&#x200B;**[!UICONTROL Day CQ Mail Service]**&#x200B;配置以下参数，并针对其名称提供详细信息：

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器密码

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小{#configure-maximum-data-size}

使用链接共享功能从共享的链接下载资产时，[!DNL Experience Manager]会从存储库中压缩资产层次结构，然后以ZIP文件形式返回资产。 但是，在对ZIP文件中可压缩的数据量没有限制的情况下，会对大量数据进行压缩，这会导致JVM中出现内存不足错误。 为了保护系统免受由于这种情况而导致的潜在拒绝服务攻击，请在Configuration Manager中使用&#x200B;**[!UICONTROL Max Content Size(uncompressed)]**&#x200B;参数为&#x200B;**[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**&#x200B;配置最大大小。 如果资产的未压缩大小超过配置的值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在Web控制台中，找到&#x200B;**[!UICONTROL Day CQ DAM临时资产共享代理Servlet]**&#x200B;配置。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## {#best-practices-and-troubleshooting}最佳实践和疑难解答

* 名称中包含空格的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资产，请咨询[!DNL Experience Manager]管理员，了解[下载限制](#configure-maximum-data-size)的具体内容。
* 如果您无法发送包含指向共享资产的链接的电子邮件，或者如果其他用户无法收到您的电子邮件，请咨询[!DNL Experience Manager]管理员，确定是否配置了[电子邮件服务](#configure-day-cq-mail-service)。
* 如果您无法使用链接共享功能共享资产，请确保您拥有相应的权限。 请参阅[共享资产](#share-assets)。
* 如果共享资产被移动到其他位置，则其链接会停止工作。 重新创建链接并与用户重新共享。

* 如果要将链接从[!DNL Experience Manager]创作部署共享到外部实体，请确保仅公开以下用于链接共享的URL（仅适用于`GET`请求）。 出于安全原因阻止其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   在[!DNL Experience Manager]界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 打开&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置，并修改&#x200B;**[!UICONTROL Domains]**&#x200B;字段中的以下属性，其值针对`local`、`author`和`publish`。 对于`local`和`author`属性，请分别提供本地实例和Author实例的URL。 如果运行单个[!DNL Experience Manager]创作实例，则对`local`和`author`属性使用相同的值。 对于Publish实例，请提供[!DNL Experience Manager] Publish实例的URL。
