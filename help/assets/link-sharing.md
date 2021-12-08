---
title: 使用链接共享资产
description: 以URL形式共享资产、文件夹和收藏集。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
source-git-commit: fb9de8a0303edd7e54639f7bb9c8a4f8e9227fa8
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 7%

---

# 将资产共享为链接 {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] 允许您以URL形式与组织成员及外部实体（包括合作伙伴和供应商）共享资产、文件夹和收藏集。 通过链接共享资产是让外部各方无需首先登录即可获取资源的一种便捷方式 [!DNL Assets].

>[!PREREQUISITES]
>
>* 您需要 `Edit ACL` 对要作为链接共享的文件夹或资产拥有的权限。
>* 要向用户发送电子邮件，请在 [Day CQ Mail Service](#configmailservice).


## 共享资产 {#share-assets}

要为要与用户共享的资产生成URL，请使用 [!UICONTROL 链接共享] 对话框。

* 具有管理员权限或具有读取权限的用户位于 `/var/dam/share` 位置可以查看与其共享的链接。
* 具有读取权限的用户位于 `/var/dam/jobs/download` 位置可以从共享链接下载资产。

1. 在 [!DNL Assets] 用户界面中，选择要作为链接共享的资产。

1. 在工具栏中，单击 **[!UICONTROL 共享链接]** ![共享资产图标](assets/do-not-localize/assets_share.png). 将在单击 **[!UICONTROL 共享]** 在 [!UICONTROL 共享链接] 字段。 在选择 **[!UICONTROL 提交]**.

   ![链接共享对话框](assets/share-assets-as-link.png)

   *图：将资产共享为链接的对话框。*

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您可以添加一个或多个用户。

   >[!NOTE]
   >
   >如果您输入的用户的电子邮件ID不是您组织的成员，则会使用 [!UICONTROL 外部用户] 前缀为用户的电子邮件ID。

1. 在&#x200B;**[!UICONTROL 主题]**&#x200B;框中，为您要共享的资产输入主题。

1. 在 **[!UICONTROL 消息]** 框中，输入可选消息。

1. 在 **[!UICONTROL 过期]** 字段中，指定链接停止工作的过期日期和时间。 链接的默认过期时间为一天。

   ![设置共享链接的过期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始资产，请选择 **[!UICONTROL 允许下载原始文件]**. 要允许用户仅下载共享资产的演绎版，请选择 **[!UICONTROL 允许下载文件的演绎版]**.

1. 单击&#x200B;**[!UICONTROL 共享]**。系统会显示一条消息，确认已通过电子邮件与用户共享该链接。

1. 要查看共享的资产，请单击发送给用户的电子邮件中的链接。 要生成资产预览，请单击共享资产。 要关闭预览，请单击 **[!UICONTROL 返回]**. 如果已共享文件夹，请单击 **[!UICONTROL 父文件夹]** 返回到父文件夹。

   ![预览共享资产](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] 支持仅生成资产预览 [支持的文件类型](/help/assets/assets-formats.md). 如果共享其他MIME类型，则您只能下载资产，无法预览。

1. 要下载共享资产，请单击 **[!UICONTROL 选择]** 在工具栏中，单击资产，然后单击 **[!UICONTROL 下载]** 中。

   ![用于下载共享资产的工具栏选项](assets/chlimage_1-547.png)

1. 要查看您以链接形式共享的资产，请转到 [!DNL Assets] 用户界面，然后单击 [!DNL Experience Manager] 徽标。 选择 **[!UICONTROL 导航]**. 在导航窗格中，选择 **[!UICONTROL 共享链接]** 以显示共享资产列表。

1. 要取消共享资产，请选择资产并单击 **[!UICONTROL 取消共享]** 中。 下面显示确认消息。 资产的条目将从列表中删除。

## 配置Day CQ邮件服务 {#configure-day-cq-mail-service}

1. 在 [!DNL Experience Manager] 主页，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在服务列表中，找到 **[!UICONTROL Day CQ Mail Service]**.
1. 单击 **[!UICONTROL 编辑]** ，并为 **[!UICONTROL Day CQ Mail Service]** 其名称上有详细说明：

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器密码

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小 {#configure-maximum-data-size}

当您从使用链接共享功能共享的链接下载资产时， [!DNL Experience Manager] 压缩存储库中的资产层次结构，然后以ZIP文件格式返回资产。 但是，在对ZIP文件中可压缩的数据量没有限制的情况下，会对大量数据进行压缩，这会导致JVM中出现内存不足错误。 要保护系统免受由于这种情况而可能发生的拒绝服务攻击，请使用 **[!UICONTROL 最大内容大小（未压缩）]** 参数 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet]** 在配置管理器中。 如果资产的未压缩大小超过配置的值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 从Web控制台中，找到 **[!UICONTROL Day CQ DAM临时资产共享代理Servlet]** 配置。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## 最佳实践和疑难解答 {#best-practices-and-troubleshooting}

* 名称中包含空格的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享的资产，请与 [!DNL Experience Manager] 管理员 [下载限制](#configure-maximum-data-size) 。
* 如果您无法发送包含指向共享资产的链接的电子邮件，或者如果其他用户无法接收您的电子邮件，请与 [!DNL Experience Manager] 管理员(如果 [电子邮件服务](#configure-day-cq-mail-service) 是否已配置。
* 如果您无法使用链接共享功能共享资产，请确保您拥有相应的权限。 请参阅 [共享资产](#share-assets).
* 如果共享资产被移动到其他位置，则其链接会停止工作。 重新创建链接并与用户重新共享。

* 如果要从 [!DNL Experience Manager] 将部署创作到外部实体，请确保仅显示以下用于链接共享的URL，例如 `GET` 仅请求。 出于安全原因阻止其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   在 [!DNL Experience Manager] 界面，访问 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**. 打开 **[!UICONTROL Day CQ链接外部器]** 配置并修改 **[!UICONTROL 域]** 字段中的值 `local`, `author`和 `publish`. 对于 `local` 和 `author` 属性中，分别提供本地实例和创作实例的URL。 如果您运行 [!DNL Experience Manager] 创作实例，请对 `local` 和 `author` 属性。 对于Publish实例，请提供 [!DNL Experience Manager] 发布实例。
