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


# 通过链接{#asset-link-sharing}共享资产

[!DNL Adobe Experience Manager Assets] 允许您以URL的形式与组织成员和外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。通过链接共享资产是一种方便的方式，使外部方无需先登录[!DNL Assets]即可获得资源。

>[!PREREQUISITES]
>
>* 您需要对要作为链接共享的文件夹或资产具有“编辑ACL”权限。
>* 要向用户发送电子邮件，请在[Day CQ邮件服务](#configmailservice)中配置SMTP服务器详细信息。


## 共享资产 {#sharelink}

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在`/var/dam/share`位置具有读取权限的用户能够视图与他们共享的链接。

1. 在[!DNL Assets]用户界面中，选择要作为链接共享的资产。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 共享链接]** ![共享资产图标](assets/do-not-localize/assets_share.png)。

   单击[!UICONTROL 共享]后将创建的链接会提前显示在[!UICONTROL 共享链接]字段中。 链接的默认过期时间为一天。

   ![与链接共享对话框](assets/Link-sharing-dialog-box.png)

   *图：将资产共享为链接的对话框。*

   >[!NOTE]
   >
   >如果要将[!DNL Experience Manager]作者部署中的链接共享到外部实体，请确保仅为`GET`请求提供以下URL（用于链接共享）。 出于安全原因阻止其他URL。
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. 在[!DNL Experience Manager]接口中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。

1. 打开&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置，在&#x200B;**[!UICONTROL Domains]**&#x200B;字段中修改以下属性，其值针对`local`、`author`和`publish`。 对于`local`和`author`属性，请分别提供本地实例和作者实例的URL。 如果运行单个[!DNL Experience Manager]作者实例，`local`和`author`属性的值相同。 对于发布实例，请提供[!DNL Experience Manager]发布实例的URL。

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您可以添加一个或多个用户。

   ![直接从“链接共享”对话框共享指向资产的链接](assets/Asset-Sharing-LinkShareDialog.png)

   *图：直接从“链接共享”对话框共享 [!UICONTROL 指向资] 产的链接。*

   >[!NOTE]
   >
   >如果您输入的电子邮件ID不是您组织的成员，则单词[!UICONTROL 外部用户]前面会加上用户的电子邮件ID。

1. 在&#x200B;**[!UICONTROL 主题]**&#x200B;字段中，输入主题行。

1. 在&#x200B;**[!UICONTROL 消息]**&#x200B;字段中，输入可选消息。

1. 在&#x200B;**[!UICONTROL Expiration]**&#x200B;字段中，指定链接停止工作的到期日期和时间。 默认情况下，过期日期设置为您共享链接后一周的时间。

   ![设置共享链接的到期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始资产和演绎版，请选择&#x200B;**[!UICONTROL 允许下载原始文件]**。 默认情况下，用户只能下载您共享为链接的资产的演绎版。

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已通过电子邮件将链接共享给用户。

1. 要视图共享的资产，请单击发送给用户的电子邮件中的链接。 共享资产显示在&#x200B;**[!UICONTROL Adobe Marketing Cloud]**&#x200B;页面中。

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. 要生成资产的预览，请单击共享的资产。 要关闭预览并返回至&#x200B;**[!UICONTROL Marketing Cloud]**&#x200B;页面，请单击工具栏中的&#x200B;**[!UICONTROL 返回]**。 如果已共享文件夹，请单击&#x200B;**[!UICONTROL 父文件夹]**&#x200B;返回父文件夹。

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 支持只生成受支持文件类 [型的资产预览](/help/assets/assets-formats.md)。如果共享了其他MIME类型，则只能下载资产，而不能进行预览。

1. 要下载共享的资产，请单击工具栏中的&#x200B;**[!UICONTROL 选择]**，单击资产，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. 要视图已作为链接共享的资产，请转到[!DNL Assets]用户界面，然后单击[!DNL Experience Manager]徽标。 选择&#x200B;**[!UICONTROL 导航]**。 在导航窗格中，选择&#x200B;**[!UICONTROL 共享链接]**&#x200B;以显示共享资产的列表。

1. 要取消共享资产，请选择该资产，然后单击工具栏中的&#x200B;**[!UICONTROL 取消共享]**。 随后将显示确认消息。 资产的条目会从列表中删除。

## 配置Day CQ邮件服务{#configmailservice}

1. 在[!DNL Experience Manager]主页中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在服务列表中，找到&#x200B;**[!UICONTROL Day CQ Mail Service]**。
1. 单击服务旁边的&#x200B;**[!UICONTROL 编辑]**，为&#x200B;**[!UICONTROL Day CQ邮件服务]**&#x200B;配置以下参数，并根据其名称提及详细信息：

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器密码

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小{#maxdatasize}

当您使用链接共享功能从共享的链接下载资产时，[!DNL Experience Manager]会从存储库中压缩资产层次结构，然后以ZIP文件形式返回资产。 但是，在ZIP文件中压缩的数据量没有限制的情况下，大量数据会受到压缩，这会导致JVM中内存不足错误。 要防止系统因此受到潜在拒绝服务攻击，请使用配置管理器中的[!UICONTROL Day CQ DAM临时资产共享代理Servlet]的&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数配置最大大小。 如果资产的未压缩大小超出配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击[!DNL Experience Manager]徽标，然后转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在Web控制台中，找到&#x200B;**[!UICONTROL Day CQ DAM临时资产共享代理Servlet]**&#x200B;配置。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## 最佳实践和疑难解答{#bestpractices}

* 名称中包含空白的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资产，请咨询您的[!DNL Experience Manager]管理员，了解[下载限制](#maxdatasize)是什么。
* 如果您无法发送包含共享资产链接的电子邮件，或者如果其他用户无法收到您的电子邮件，请咨询您的[!DNL Experience Manager]管理员（如果[电子邮件服务](#configmailservice)已配置或未配置）。
* 如果您无法使用链接共享功能共享资产，请确保您具有相应的权限。 请参阅[共享资产](#sharelink)。
* 如果共享资产被移动到其他位置，其链接将停止工作。 重新创建链接并与用户重新共享。
