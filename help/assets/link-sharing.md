---
title: 使用链接共享资源
description: 将资源、文件夹和收藏集共享为URL。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 6%

---

# 将资产作为链接共享 {#asset-link-sharing}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 允许您将资产、文件夹和收藏集作为URL与您的组织成员和外部实体（包括合作伙伴和供应商）共享。 通过链接共享资产是一种方便的方法，使外部方无需先登录即可使用资源 [!DNL Assets].

>[!PREREQUISITES]
>
>* 您需要 `Edit ACL` 对要作为链接共享的文件夹或资源的权限。
>* 要向用户发送电子邮件，请在中配置SMTP服务器详细信息 [Day CQ邮件服务](#configmailservice).

## 共享资源 {#share-assets}

要为要与用户共享的资源生成URL，请使用 [!UICONTROL 链接共享] 对话框。

* 具有管理员权限或读取权限的用户 `/var/dam/share` 位置可查看与其共享的链接。
* 对具有读取权限的用户 `/var/dam/jobs/download` 位置可以从共享链接下载资产。

1. 在 [!DNL Assets] 用户界面中，选择要作为链接共享的资产。

1. 在工具栏中，单击 **[!UICONTROL 共享链接]** ![共享资产图标](assets/do-not-localize/assets_share.png). 单击后创建的链接 **[!UICONTROL 共享]** 会预先显示在 [!UICONTROL 共享链接] 字段。 只有在您选择之前，才会创建链接 **[!UICONTROL 提交]**.

   ![带有链接共享的对话框](assets/share-assets-as-link.png)

   *图：将资源共享为链接的对话框。*

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您可以添加一个或多个用户。

   >[!NOTE]
   >
   >如果您输入的电子邮件ID不是您组织的成员，则您输入的电子邮件 [!UICONTROL 外部用户] 以为用户的电子邮件ID作为前缀。

1. 在 **[!UICONTROL 主题]** 框中，为要共享的资产输入主题。

1. 在 **[!UICONTROL 消息]** 框中，输入可选消息。

1. 在 **[!UICONTROL 过期]** 字段中，指定链接停止工作的过期日期和时间。 链接的默认过期时间为一天。

   ![设置共享链接的到期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始资源，请选择 **[!UICONTROL 允许下载原始文件]**. 要允许用户仅下载共享资源的演绎版，请选择 **[!UICONTROL 允许下载文件演绎版]**.

1. 单击 **[!UICONTROL 共享]**. 将显示一条消息，确认通过电子邮件将链接与用户共享。

1. 要查看共享资产，请单击发送给用户的电子邮件中的链接。 要生成资源的预览，请单击共享资源。 要关闭预览，请单击 **[!UICONTROL 返回]**. 如果已共享文件夹，请单击 **[!UICONTROL 父文件夹]** 以返回到父文件夹。

   ![共享资源的预览](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 仅支持生成的资产预览 [支持的文件类型](/help/assets/assets-formats.md). 如果共享其他MIME类型，则只能下载资源且无法预览。

1. 要下载共享资源，请单击 **[!UICONTROL 选择]** 在工具栏中，单击资产，然后单击 **[!UICONTROL 下载]** 工具栏中。

   ![用于下载共享资源的工具栏选项](assets/chlimage_1-547.png)

1. 要查看您作为链接共享的资源，请转到 [!DNL Assets] 用户界面并单击 [!DNL Experience Manager] 徽标。 选择 **[!UICONTROL 导航]**. 在导航窗格中，选择 **[!UICONTROL 共享的链接]** 以显示共享资源的列表。

1. 要取消共享资产，请选择该资产并单击 **[!UICONTROL 取消共享]** 工具栏中。 随后将显示确认消息。 资源的条目将从列表中删除。

## 配置Day CQ邮件服务 {#configure-day-cq-mail-service}

1. 在 [!DNL Experience Manager] 主页，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在服务列表中，找到 **[!UICONTROL Day CQ邮件服务]**.
1. 单击 **[!UICONTROL 编辑]** ，并配置以下参数 **[!UICONTROL Day CQ邮件服务]** 他们的名字有详细描述：

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器密码

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小 {#configure-maximum-data-size}

当您从使用链接共享功能共享的链接下载资产时， [!DNL Experience Manager] 从存储库压缩资源层次结构，然后以ZIP文件返回资源。 但是，由于ZIP文件中可以压缩的数据量没有限制，因此会压缩大量数据，这会导致JVM中出现内存不足错误。 要保护系统免受由于此情况而导致的潜在拒绝服务攻击，请使用 **[!UICONTROL 最大内容大小（未压缩）]** 参数 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet]** 在Configuration Manager中。 如果资产的未压缩大小超过配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在Web控制台中，找到 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet]** 配置。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## 最佳实践和疑难解答 {#best-practices-and-troubleshooting}

* 名称中包含空格的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资产，请向您的 [!DNL Experience Manager] 管理员什么 [下载限制](#configure-maximum-data-size) 是。
* 如果您无法发送包含共享资产链接的电子邮件，或者其他用户无法接收您的电子邮件，请咨询 [!DNL Experience Manager] 管理员，如果 [电子邮件服务](#configure-day-cq-mail-service) 是否已配置。
* 如果您无法使用链接共享功能共享资源，请确保您拥有适当的权限。 请参阅 [共享资产](#share-assets).
* 如果将共享资源移动到其他位置，则其链接将停止工作。 重新创建链接并与用户重新共享。

* 如果要共享您网站上的 [!DNL Experience Manager] 要向外部实体进行创作部署，请确保仅公开以下用于链接共享的URL，即 `GET` 仅请求。 出于安全原因，阻止其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  在 [!DNL Experience Manager] 界面，访问 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**. 打开 **[!UICONTROL Day CQ链接外部化器]** 配置，并修改中的以下属性 **[!UICONTROL 域]** 字段及其提及的值 `local`， `author`、和 `publish`. 对于 `local` 和 `author` 属性，分别提供本地实例和创作实例的URL。 如果您运行单个 [!DNL Experience Manager] 创作实例，将相同的值用于 `local` 和 `author` 属性。 对于Publish实例，提供 [!DNL Experience Manager] 发布实例。
