---
title: 管理视频资源
description: 在中上传、预览、注释和发布视频资产 [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 8%

---

# 管理视频资源 {#manage-video-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | 本文 |

视频格式是组织数字资产的重要组成部分。 [!DNL Adobe Experience Manager] 提供成熟的产品和功能，用于在创建视频资产后管理其整个生命周期。

了解如何在中管理和编辑视频资产 [!DNL Adobe Experience Manager Assets]. 视频编码和转码，例如FFmpeg转码，可以使用 [!DNL Dynamic Media] 集成。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资源生成预览。 如果资产的格式不是MP4，请安装FFmpeg包以生成预览。 FFmpeg创建OGG和MP4类型的视频演绎版。 您可以在中预览演绎版 [!DNL Assets] 用户界面。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击 **[!UICONTROL 创建]** 从工具栏中选择 **[!UICONTROL 文件]**. 或者，在用户界面上拖动文件。 参见 [上传资产](manage-assets.md#uploading-assets) 了解详细信息。
1. 要在卡片视图中预览视频，请单击 **[!UICONTROL 播放]** ![播放选项](assets/do-not-localize/play.png) 选项。 您只能在卡片视图中暂停或播放视频。 此 [!UICONTROL 播放] 和 [!UICONTROL 暂停] 选项在列表视图中不可用。

1. 要在资源详细信息页面中预览视频，请单击 **[!UICONTROL 编辑]** 在卡片上。 视频在浏览器的本机视频播放器中播放。 您可以播放、暂停、控制音量以及将视频缩放到全屏。

   ![视频播放控制](assets/video-playback-controls.png)

## 用于上传大于2 GB的资产的配置 {#configuration-to-upload-assets-that-are-larger-than-gb}

默认情况下， [!DNL Assets] 不允许您上传任何因文件大小限制而大于2 GB的资产。 但是，您可以通过进入CRXDE Lite并在下创建节点来覆盖此限制 `/apps` 目录。 节点必须具有相同的节点名称、目录结构和顺序的可比较节点属性。

除此之外 [!DNL Assets] 配置，更改以下配置以上传大型资产：

* 增加令牌过期时间。 参见 [!UICONTROL AdobeGranite CSRF Servlet] 在Web控制台中的 `https://[aem_server]:[port]/system/console/configMgr`. 有关更多信息，请参阅 [CSRF保护](/help/sites-developing/csrf-protection.md).
* 增加 `receiveTimeout` 在Dispatcher配置中。 有关更多信息，请参阅 [Experience ManagerDispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>此 [!DNL Experience Manager] 传统用户界面没有2 GB文件大小限制。 此外，不完全支持大型视频的端到端工作流。

要配置更高的文件大小限制，请在 `/apps` 目录。

1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite中，导航到 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 要查看目录窗口，请单击 `>>`.
1. 在工具栏中，单击 **[!UICONTROL 覆盖节点]**. 或者，从上下文菜单中选择&#x200B;**[!UICONTROL 覆盖节点]**。
1. 在 **[!UICONTROL 覆盖节点]** 对话框，单击 **[!UICONTROL 确定]**.

   ![覆盖节点](assets/overlay-node-path.png)

1. 刷新浏览器。 覆盖节点 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 已选中。
1. 在 **[!UICONTROL 属性]** 选项卡，以字节为单位输入相应的值，以将大小限制增加到所需的大小。 例如，要将大小限制增加到30 GB，请输入 `32212254720` 值。

1. 在工具栏中，单击 **[!UICONTROL 全部保存]**.
1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在 [!DNL Adobe Experience Manager] [!UICONTROL Web控制台包] 在表的“名称”列下，找到并单击 **[!UICONTROL AdobeGranite工作流外部进程作业处理程序]**.
1. 在 [!UICONTROL AdobeGranite工作流外部进程作业处理程序] 页面，为两者设置秒数 **[!UICONTROL 默认超时]** 和 **[!UICONTROL 最大超时]** 字段至 `18000` （5小时）。 单击“**[!UICONTROL 保存]**”。
1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在“工作流模型”页面上，选择 **[!UICONTROL Dynamic Media编码视频]**，然后单击 **[!UICONTROL 编辑]**.
1. 在工作流页面上，双击 **[!UICONTROL Dynamic Media视频服务进程]** 组件。
1. 在[!UICONTROL 步骤属性]对话框的&#x200B;**[!UICONTROL 常用]**&#x200B;选项卡下，展开&#x200B;**高级设置**。
1. 在 **[!UICONTROL 超时]** 字段，指定值 `18000`，然后单击 **[!UICONTROL 确定]** 以返回 **[!UICONTROL Dynamic Media编码视频]** 工作流页面。
1. 在页面顶部附近，在 [!UICONTROL Dynamic Media编码视频] 页面标题，单击 **[!UICONTROL 保存]**.

## 发布视频资产 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中，也可以直接嵌入这些资产。 有关详细信息，请参阅 [发布Dynamic Media资源](/help/assets/publishing-dynamicmedia-assets.md).

## 将视频发布到YouTube {#publishing-videos-to-youtube}

您可以将内部部署Experience Manager视频资产直接发布到之前创建的YouTube渠道。

要将视频资源发布到YouTube，您需要使用标记设置Experience Manager Assets。 将这些标记与YouTube渠道关联。 如果视频资产的标记与YouTube渠道的标记匹配，则视频将发布到YouTube。 只要使用关联的标记，发布到YouTube的过程就会伴随着视频的正常发布。

YouTube自行编码。 因此，上传到Experience Manager的原始视频文件将发布到YouTube，而不是Dynamic Media的编码创建的任何视频演绎版。 虽然不需要使用Dynamic Media处理视频，但预计会在播放需要查看器预设时这样做。

当您绕过视频处理配置文件并直接发布到YouTube时，这仅仅意味着您在Experience Manager资源中的视频资源未获得可查看的缩略图。 这也意味着，如果你跑进 `dynamicmedia` 或 `dynamicmedia_scene7` 运行模式，未编码的视频不适用于任何Dynamic Media资源类型。

将视频资产发布到YouTube服务器需要完成以下任务，以确保使用YouTube进行服务器到服务器身份验证的安全性和安全性：

1. [配置Google云设置](#configuring-google-cloud-settings)
1. [创建YouTube渠道](#creating-a-youtube-channel)
1. [添加标记以进行发布](#adding-tags-for-publishing)
1. [启用YouTube发布复制代理](#enabling-the-youtube-publish-replication-agent)
1. [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem)
1. [（可选）自动为您上传的视频设置默认YouTube属性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [将视频发布到您的YouTube渠道](#publishing-videos-to-your-youtube-channel)
1. [（可选）验证YouTube上发布的视频](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [将YouTube URL链接到您的Web应用程序](#linking-youtube-urls-to-your-web-application)

您还可以 [取消发布视频以从YouTube中删除它们](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google云设置 {#configuring-google-cloud-settings}

要发布到YouTube，您需要Google帐户。 如果您拥有GMAIL帐户，则表明您已经拥有Google帐户；如果您没有Google帐户，则可以轻松创建一个帐户。 您需要帐户，因为您需要凭据才能将视频资产发布到YouTube。 如果您已创建帐户，请跳过此任务并直接转到 [创建YouTube渠道](#creating-a-youtube-channel).

与Google Cloud一起使用的帐户和用于YouTube的Google帐户无需相同。

Google会定期更改其用户界面。 因此，将视频发布到YouTube的步骤可能与以下文档略有不同。 当您尝试检查视频是否已上传到YouTube时，此注意事项也适用。

>[!NOTE]
>
>在撰写本文时，以下步骤是准确的。 但是，Google会定期更新其网站，恕不另行通知。 因此，这些步骤可能略有不同。

要配置Google Cloud设置，请执行以下操作：

1. 创建Google帐户。
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   如果您已有Google帐户，请跳至下一步。

1. 转到 [https://cloud.google.com/](https://cloud.google.com/).
1. 在Google cloud页面的右上角附近，单击控制 **[!UICONTROL 台]**。

   如有必要， **[!UICONTROL 登录]** 使用您的Google帐户凭据查看 **[!UICONTROL 控制台]** 选项。

1. 在“功能板”页面的 **[!UICONTROL Google Cloud平台]**，单击项目下拉列表以打开选择项目对话框。
1. 在选择项目对话框中，点按 **[!UICONTROL 新建项目]**.

   ![6_5_google帐户 — 新项目](assets/6_5_googleaccount-newproject.png)

1. 在“新建项目”对话框的“项目名称”字段中，键入新项目的名称。

   您的项目ID基于您的项目名称。 因此，请仔细选择项目名称；项目名称在创建后无法更改。 此外，当您稍后在Experience Manager中设置YouTube时，必须再次输入相同的项目ID；请考虑将其写下来。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 执行以下任一操作：

   * 在项目的功能板上，在入门信息卡中，点按 **[!UICONTROL 探索和启用API]**.
   * 在您项目的功能板上的API信息卡中，点按 **[!UICONTROL 转到API概述]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. 在“API和服务”页面顶部附近，点按 **[!UICONTROL 启用API和服务]**.
1. 在“API库”页面的左侧，下方 **[!UICONTROL 类别]**，点按 **[!UICONTROL YouTube]**. 在页面的右侧，点按 **[!UICONTROL YouTube数据API]**.
1. 在YouTube Data API v3页面上，点按 **[!UICONTROL 启用]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. 要使用API，您需要凭据。 如有必要，请单击 **[!UICONTROL 创建凭据]**.

   ![6_5_googleaccount-apis-creategrecredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. 在 **[!UICONTROL 向项目添加凭据]** 第页，第1步，执行以下操作：

   * 从 **[!UICONTROL 您使用的是哪个API？]** 下拉列表，选择 **[!UICONTROL YouTube数据API v3]**.

   * 从 **[!UICONTROL 您从何处调用API？]** 下拉列表，选择 **[!UICONTROL Web服务器（例如，node.js、Tomcat）]**

   * 从 **[!UICONTROL 您正在访问哪些数据？]** 下拉列表，点按 **[!UICONTROL 用户数据]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. 点按 **[!UICONTROL 我需要什么凭据？]**
1. 在&#x200B;**[!UICONTROL 将凭据添加到项目]**&#x200B;页面中步骤 2 的&#x200B;**[!UICONTROL 创建 OAuth 2.0 客户端 ID]** 标题下，根据需要在“名称”字段中输入唯一名称。或者，您也可以使用 Google 指定的默认名称。
1. 在 **[!UICONTROL 授权的JavaScript源]** 标题，在文本字段中输入以下路径，在路径中替换您自己的域和端口号，然后按键 **[!UICONTROL 输入]** 要将路径添加到列表，请执行以下操作：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   **注释**：上述路径示例仅用于演示目的。

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. 在 **[!UICONTROL 授权的重定向URI]** 标题，在文本字段中输入以下路径，在路径中替换您自己的域和端口号，然后按键 **[!UICONTROL 输入]** 要将路径添加到列表，请执行以下操作：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **注释**：上述路径示例仅用于演示目的。

1. 单击 **[!UICONTROL 创建OAuth客户端ID]**.
1. 在&#x200B;**[!UICONTROL 向项目添加凭据]**&#x200B;页面的步骤 3 中，在&#x200B;**[!UICONTROL 设置 OAuth 2.0 许可屏幕]**&#x200B;标题下，选择您当前使用的 Gmail 电子邮件地址。

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. 在 **[!UICONTROL 向用户显示的产品名称]** 标题，在文本字段中，输入要显示在同意屏幕上的内容。

   当Experience Manager管理员对YouTube进行身份验证时，将会向Experience Manager管理员显示同意屏幕；管理员会联系YouTube以获取权限。

1. 单击&#x200B;**[!UICONTROL “继续”]**。
1. 在将凭据添加到项目页面的步骤4中，在“下载凭据 **[!UICONTROL ”标题下]** ，点按 **[!UICONTROL 下载]**。

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. 保存 `client_id.json` 文件。

   稍后在Adobe Experience Manager中设置YouTube时，您需要此下载的json文件。

1. 单击 **[!UICONTROL 完成]**.

   注销您的Google帐户。 现在创建一个YouTube渠道。

### 创建YouTube渠道 {#creating-a-youtube-channel}

要将视频发布到YouTube，您需要具有一个或多个渠道。 如果您已创建YouTube渠道，则可以跳过此任务并转到 [添加标记以进行发布](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>确保您已在YouTube中设置了一个或多个渠道 *早于* 您可以在“Experience Manager中的YouTube设置”下添加渠道(请参阅 [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem) （如下所示）。 如果您未能设置一个或多个渠道，则不会警告您不存在渠道。 但是，在添加频道时，Google身份验证仍会发生，但无法选择发送视频的频道。

**要创建YouTube渠道，请执行以下操作：**

1. 转到 [https://www.youtube.com](https://www.youtube.com/) 并使用您的Google帐户凭据登录。
1. 在YouTube页面的右上角，单击您的个人资料图片（也可以显示为实色圆圈中的字母），然后单击 **[!UICONTROL YouTube设置]** （圆齿轮图标）。
1. 在概述页面的其他功能标题下，单击 **[!UICONTROL 查看我的所有渠道或创建渠道]**.
1. 在渠道页面上，单击 **[!UICONTROL 创建新渠道]**.
1. 在“品牌帐户”页面的品牌帐户名称字段中，输入业务名称或您选择要将视频资产发布到的其他渠道名称，然后单击 **[!UICONTROL 创建]**.

   请记住您在此处输入的名称，因为在Experience Manager中设置YouTube时必须再次输入该名称。

1. （可选）如有必要，请添加更多渠道。

   现在添加标记以进行发布。

### 添加标记以进行发布 {#adding-tags-for-publishing}

要将视频发布到YouTube，Experience Manager会将标记与一个或多个YouTube渠道关联。 要添加标记以进行发布，请参阅 [管理标记](/help/sites-administering/tags.md).

或者，如果您打算在Experience Manager中使用默认标记，则可以跳过此任务并转到 [启用YouTube发布复制代理](#enabling-the-youtube-publish-replication-agent).

### 启用YouTube发布复制代理 {#enabling-the-youtube-publish-replication-agent}

启用YouTube发布复制代理后，如果要测试与Google Cloud帐户的连接，请点按 **[!UICONTROL 测试连接]**. 浏览器选项卡显示连接结果。 如果您已添加YouTube渠道，则测试中将显示渠道列表。

1. 单击Experience Manager左上角的Experience Manager徽标，然后在左边栏中，单击 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** > **[!UICONTROL 作者代理]**.
1. 在“创作代理”页面上，单击 **[!UICONTROL YouTube发布]**.
1. 在工具栏的“设置”右侧，单击 **[!UICONTROL 编辑]**.
1. 选择 **[!UICONTROL 已启用]** 复选框，以便您可以打开复制代理。
1. 单击&#x200B;**[!UICONTROL 确定]**。

   现在在Experience Manager中设置YouTube。

### 在Experience Manager中设置YouTube {#setting-up-youtube-in-aem}

从Experience Manager6.4开始，引入了一种新的触屏用户界面方法，以在Experience Manager中设置YouTube发布。 根据您正在使用的已安装的Experience Manager实例，执行以下操作之一：

* 要在6.4之前的Experience Manager中配置YouTube，请参阅 [在6.4之前的Experience Manager中设置YouTube](/help/assets/video.md#setting-up-youtube-in-aem-before).
* 要在Experience Manager6.4或更高版本中配置YouTube，请参阅 [在Experience Manager6.4及更高版本中设置YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4及更高版本中设置YouTube {#setting-up-youtube-in-aem-and-later}

1. 确保以管理员身份登录到Dynamic Media实例。
1. 点按左上角的Experience Manager徽标，然后点按左边栏中的徽标 **[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube发布配置]**.
1. 点按 **[!UICONTROL 全局]** （请勿选择它）。

1. 在全局页面的右上角附近，点按 **[!UICONTROL 创建]**.
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   在之前最初配置Google Cloud设置时，您指定了项目ID。
将“创建YouTube配置”页面保持打开状态；稍后您将返回到它。

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用纯文本编辑器，打开您之前在任务中下载并保存的JSON文件 [配置Google云设置](/help/assets/video.md#configuring-google-cloud-settings).
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在页面的右上角附近，点按 **[!UICONTROL 保存]**.

   现在在Experience Manager中设置YouTube渠道。

1. 点按 **[!UICONTROL 添加渠道]**.
1. 在渠道名称字段中，输入您在任务中创建的渠道的名称 **[!UICONTROL 向YouTube添加一个或多个渠道]** 更早。

   如果需要，您可以选择添加描述。

1. 点按 **[!UICONTROL 添加]**.
1. 将显示YouTube/Google身份验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择一个渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页，点按 **[!UICONTROL 接受]** 以允许对此渠道的访问。

1. 点按 **[!UICONTROL 允许]**.

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]**  — 在Cloud Services> YouTube页面上，点按铅笔图标以编辑要使用的标记列表。
1. 点按下拉列表图标（上下颠倒的尖号），以便在Experience Manager中显示可用标记的列表。
1. 点按一个或多个标记，以便添加它们。

   要删除已添加的标记，请选择该标记，然后点按 **[!UICONTROL X]**.

1. 添加完所需的标记后，点按 **[!UICONTROL 保存]**.

   现在，您可以将视频发布到YouTube渠道。

#### 在6.4之前的Experience Manager中设置YouTube {#setting-up-youtube-in-aem-before}

1. 确保以管理员身份登录到Dynamic Media实例。

1. 点按左上角的Experience Manager徽标，然后点按左边栏中的徽标 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在“第三方服务”标题下方的YouTube下，点按 **[!UICONTROL 立即配置]**.
1. 在创建配置对话框中，在相应字段中输入标题（必需）和名称（可选）。
1. 点按 **[!UICONTROL 创建]**.
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您最初指定项目ID时 [已配置Google云设置](/help/assets/video.md#configuring-google-cloud-settings) 更早。
保持YouTube帐户设置对话框处于打开状态；稍后您将返回到该对话框。

1. 使用纯文本编辑器，打开您之前在配置Google Cloud设置任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 点按 **[!UICONTROL 确定]**.

   现在在Experience Manager中设置YouTube渠道。

1. 在&#x200B;**[!UICONTROL 可用渠道]**&#x200B;右侧，点按 **+**（加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如果需要，您可以选择添加描述。

1. 点按 **[!UICONTROL 确定]**.
1. 将显示YouTube/Google身份验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择一个渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页，点按 **[!UICONTROL 接受]** 以允许对此渠道的访问。

1. 点按 **[!UICONTROL 允许]**.

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]**  — 在Cloud Services> YouTube页面上，点按铅笔图标以编辑要使用的标记列表。
1. 点按下拉列表图标（上下颠倒的尖号），以便在Experience Manager中显示可用标记的列表。
1. 点按一个或多个标记，以便添加它们。

   要删除已添加的标记，请选择该标记，然后点按 **X**.

1. 添加完所需的标记后，点按 **[!UICONTROL 确定]**.

   现在，您可以将视频发布到YouTube渠道。

### （可选）自动为您上传的视频设置默认YouTube属性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以选择通过在Experience Manager中创建元数据处理配置文件来在上传视频时自动设置YouTube属性。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然后，您可以通过向处理配置文件添加这些值来构建您的YouTube视频元数据处理配置文件。

要自动为您上传的视频设置默认YouTube属性，请执行以下操作：

1. 点按左上角的Experience Manager徽标，然后单击左边栏中的 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
1. 单击 **[!UICONTROL 默认]**. （请勿在“default”左侧的选择框中添加复选标记。）
1. 在 **[!UICONTROL 默认]** 页面，选中左侧的框 **[!UICONTROL 视频]**，然后点按 **[!UICONTROL 编辑]**.
1. 在元数据架构编辑器页面上，点按 **[!UICONTROL 高级]** 选项卡。
1. 在“YouTube 发布”标题下，单击 **[!UICONTROL YouTube 类别]**。
1. 在页面的右侧，在 **[!UICONTROL 设置]** 选项卡，执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段，选择并复制值。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 下 **[!UICONTROL 选项]**，选择并复制您要使用的默认值（例如“人员和博客”或“科学与技术”）。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在YouTube Publishing标题下，点按 **[!UICONTROL YouTube隐私]**.
1. 在页面的右侧，在 **[!UICONTROL 设置]** 选项卡，执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段，选择并复制值。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 下 **[!UICONTROL 选项]**，选择并复制要使用的默认值。 请注意，“选择”分为两组。 该对中的底部字段是您要复制的默认值，如public、unlisted或private。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在“元数据架构编辑器”页面的右上角附近，单击 **[!UICONTROL 取消]**.
1. 点按Experience Manager左上角的Experience Manager徽标，然后单击左边栏中的 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]**.

1. 在元数据配置文件页面右上角附近，单击 **[!UICONTROL 创建]**.
1. 在“添加元数据配置文件”对话框的&#x200B;**[!UICONTROL 配置文件]**&#x200B;文本字段中，输入名称 `YouTube Video`，然后单击&#x200B;**[!UICONTROL 创建]**。
1. 在元数据配置文件编辑器页面上，单击 **[!UICONTROL 前进]** 选项卡。
1. 通过执行以下操作，将复制的YouTube发布值添加到配置文件中：

   * 在页面的右侧，单击 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动标记为的组件 **[!UICONTROL 章节标题]** 左侧，并将其放入表单区域。
   * （可选）单击 **[!UICONTROL 字段标签]** 以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入 `YouTube Publishing`.
   * 单击 **[!UICONTROL 构建表单]** 选项卡，然后拖动标记为的组件 **[!UICONTROL 多值文本]** 然后将其放在 **[!UICONTROL YouTube发布]** 您创建的标题。

   * 单击 **[!UICONTROL 字段标签]** 这样即会选中该组件。
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 通过执行以下操作，将复制的YouTube隐私值添加到用户档案：

   * 在页面的右侧，单击 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动标记为的组件 **[!UICONTROL 章节标题]** 左侧，并将其放入表单区域。
   * （可选）单击 **[!UICONTROL 字段标签]** 以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入 `YouTube Privacy`.
   * 单击 **[!UICONTROL 构建表单]** 选项卡，然后拖动标记为的组件 **[!UICONTROL 多值文本]** 然后将其放在 **[!UICONTROL YouTube隐私]** 您创建的标题。

   * 单击 **[!UICONTROL 字段标签]** 这样即会选中该组件。
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 保存]**。
1. 将YouTube发布元数据配置文件应用到要上传视频的文件夹。 您必须同时设置元数据配置文件和视频配置文件。

   请参阅 [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles) 和视 [频配置文件](/help/assets/video-profiles.md)。

### 将视频发布到您的YouTube渠道 {#publishing-videos-to-your-youtube-channel}

现在，您可以将之前添加的标记关联到视频资产。 此过程可告知Experience Manager要发布到YouTube渠道的资产。

>[!NOTE]
>
>在Dynamic Media - Scene7模式下运行时，不会立即发布自动发布到YouTube。 在设置Dynamic Media - Scene7模式时，有两种发布选项可供选择： **[!UICONTROL 立即]** 或 **[!UICONTROL 激活时]**.
>
>**[!UICONTROL 立即发布]** 这意味着上传的资产（与IPS同步后）会自动发布到投放系统。 虽然这对Dynamic Media是这样，但对YouTube不是这样。 要发布到YouTube，您必须通过Experience Manager创作进行发布。

>[!NOTE]
>
>要从YouTube发布内容，Experience Manager使用 **[!UICONTROL 发布到YouTube]** 工作流，用于监视进度和查看任何故障信息。
>
>参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>有关更详细的进度信息，您可以在复制下监视YouTube日志。 但是，请注意，此类监视需要管理员访问权限。

**要将视频发布到您的YouTube渠道，请执行以下操作：**

1. 在Experience Manager中，导航到要发布到YouTube渠道的视频资源。
1. 选择视频资产（自适应视频集）。
1. 在工具栏上，单击 **[!UICONTROL 属性]**.
1. 在基本选项卡的元数据标题下，单击 **[!UICONTROL 打开选择对话框]** 标记字段的右侧。
1. 在“选择标记”页面上，导航到要使用的标记，然后选择一个或多个标记。

   请记住，标记必须与YouTube渠道关联。

1. 在页面的右上角，单击 **[!UICONTROL 选择]**.
1. 在视频属性页面的右上角，单击 **[!UICONTROL 保存并关闭]**.
1. 在工具栏上，单击 **[!UICONTROL 快速发布]**.

   另请参阅 [在Experience Manager Sites中使用发布管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   您可以选择在YouTube渠道中验证已发布的视频。

### （可选）验证YouTube上发布的视频 {#optional-verifying-the-published-video-on-youtube}

您可以选择监视YouTube发布（或取消发布）的进度。

参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

发布时间会因多种因素而有很大的差异，这些因素包括主源视频的格式、文件大小和上传流量。 发布过程可能需要几分钟到几小时的时间。 此外，更高分辨率格式的渲染速度要慢得多。 例如，720p和1080p的出现时间比480p长。

8小时后，如果您仍然看到一条状态消息，显示 **[!UICONTROL 已上传（正在处理，请稍候）]**，请尝试从Adobe的网站中移除视频并重新上传。

### 将YouTube URL链接到您的Web应用程序 {#linking-youtube-urls-to-your-web-application}

您可以获取Dynamic Media在发布视频后生成的YouTube URL字符串。 复制YouTube URL时，它会登陆到剪贴板，以便您可以根据需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
>在将视频资源发布到YouTube之前，无法复制YouTube URL。

**要将YouTube URL链接到您的Web应用程序，请执行以下操作：**

1. 导航到 *YouTube已发布* 要复制其URL的视频资源，然后选择它。

   请记住，YouTube URL仅可供复制 *之后* 您拥有 *已发布* 将视频资源载入YouTube。

1. 在工具栏上，单击 **[!UICONTROL 属性]**.
1. 单击 **[!UICONTROL 高级]** 选项卡。
1. 在YouTube发布标题下方的YouTube URL列表中，选择URL文本，然后将其复制到Web浏览器，以预览资源或添加到Web内容页面。

### 取消发布视频，以便从YouTube中删除它们 {#unpublishing-videos-to-remove-them-from-youtube}

在Experience Manager中取消发布视频资源时，该视频将从YouTube中删除。

>[!CAUTION]
>
>如果直接从YouTube中删除视频，则Experience Manager不会察觉，并继续像视频仍发布到YouTube那样行事。 始终通过Experience Manager从YouTube取消发布视频资源。

>[!NOTE]
>
>要从YouTube中删除内容，Experience Manager使用 **[!UICONTROL 从YouTube取消发布]** 工作流，用于监视进度和查看任何故障信息。
>
>参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

**要取消发布视频以将其从YouTube中删除，请执行以下操作：**

1. 导航到要从YouTube渠道取消发布的视频资源。
1. 在资源选择模式下，选择一个或多个已发布的视频资源。
1. 在工具栏上，单击 **[!UICONTROL 管理发布]**. 点按三个圆点图标(...) 工具栏上，因此 **[!UICONTROL 管理发布]** 打开。
1. 在管理发布页面上，点按 **[!UICONTROL 取消发布]**.
1. 在页面的右上角，点按 **[!UICONTROL 下一个]**.
1. 在页面的右上角，点按 **[!UICONTROL 取消发布]**.

## 监控视频编码和YouTube发布进度 {#monitoring-video-encoding-and-youtube-publishing-progress}

在将新视频上传到应用了视频编码的文件夹或将视频发布到YouTube时，您可以监控视频编码/Youtube发布的进展情况。 实际的YouTube发布进度只能通过日志获得。 但是，以下过程中介绍的其他方式会列出其失败或成功。 此外，当YouTube发布工作流或视频编码完成或中断时，您会收到电子邮件通知。

### 监测进度 {#monitoring-progress}

1. 在assets文件夹中查看视频编码进度：

   * 在卡片视图中，视频编码进度按百分比显示在资源上。 如果出现错误，资产上也会显示此信息。

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 在列表视图中，视频编码进度显示在 **[!UICONTROL 处理状态]** 列。 如果出现错误，则同一列中将显示此消息。

   ![chlimage_1-430](assets/chlimage_1-430.png)

   默认情况下，此列不显示。要启用该列，请从视图下拉菜单中选择&#x200B;**[!UICONTROL 查看设置]**，然后添加&#x200B;**[!UICONTROL 处理状态]**&#x200B;列，然后点按或单击&#x200B;**[!UICONTROL 更新]**。

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 在资源详细信息中查看进度。 点按或单击资产时，打开下拉菜单并选择 **[!UICONTROL 时间线]**. 要将其缩小到编码或YouTube发布等工作流活动，请选择 **[!UICONTROL 工作流]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   任何工作流信息（如编码）都会显示在时间轴中。 对于YouTube发布，工作流时间轴还包括YouTube渠道的名称和YouTube视频URL。 此外，发布完成后，您会在工作流时间轴中看到任何失败通知。

   >[!NOTE]
   >
   >由于上的多个工作流配置，最终记录失败/错误可能需要较长时间 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 起始日期 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   >    * Apache Sling作业队列配置
   >    * AdobeGranite工作流外部进程作业处理程序
   >    * Granite工作流超时队列

   >
   >您可以调整 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 属性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   >
   >您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-433](assets/chlimage_1-433.png)

   选择实例并点按 **[!UICONTROL 打开历史记录]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   从“工作流实例”区域，您还可以暂停、终止或重命名工作流。 参见 [管理工作流](/help/sites-administering/workflows-administering.md) 了解更多信息。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   >
   >您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由于上的多个工作流配置，最终记录错误消息可能需要较长时间 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 起始日期 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   >
   >
   >    * Apache Sling作业队列配置
   >    * AdobeGranite工作流外部进程作业处理程序
   >    * Granite工作流超时队列

   >
   >
   >您可以调整 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 属性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   >
   >您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 您会收到有关已中止或失败的工作流作业的电子邮件通知。 这些电子邮件通知可由管理员配置。 参见 [配置电子邮件通知](#configuring-e-mail-notifications).

#### 配置电子邮件通知 {#configuring-e-mail-notifications}

>[!NOTE]
>
>您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

配置通知的方式取决于您是要接收编码作业还是YouTube发布作业的通知：

* 对于编码作业，您可以在以下位置访问所有Experience Manager工作流电子邮件通知的配置页面： **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** 并通过搜索 **[!UICONTROL Day CQ工作流电子邮件通知服务]**. 参见 [在Experience Manager中配置电子邮件通知](/help/sites-administering/notification.md). 您可以选中或清除复选框 **[!UICONTROL 中止时通知]** 或 **[!UICONTROL 完成时通知]** 相应地。

* 对于YouTube发布作业，请执行以下操作：

1. 在Experience Manager中，点按 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在“工作流模型”页面上，选择 **[!UICONTROL 发布到YouTube]**，然后点按 **[!UICONTROL 编辑]** 工具栏上。
1. 在“发布到YouTube”工作流页面的右上角附近，点按 **[!UICONTROL 编辑]**.
1. 将鼠标指针悬停在YouTube上传组件上，然后点按一次以显示内联工具栏。

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 在内联工具栏上，点按配置图标（扳手）。 单击 **[!UICONTROL 参数]** 选项卡。

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. 在YouTube上传流程 — 步骤属性对话框中，点按 **[!UICONTROL 参数]** 选项卡。

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 您可以选中或清除以下复选框：

   * 发布开始
   * 发布失败
   * 发布完成 — 包含有关渠道和URL的信息

   清除复选框表示您不会从YouTube Publish工作流收到指定的电子邮件通知。

   >[!NOTE]
   >
   >这些电子邮件特定于YouTube，是通用工作流电子邮件通知的补充。 因此，您可以收到两套电子邮件通知，即中提供的通用通知 **[!UICONTROL Day CQ工作流电子邮件通知服务]** 以及特定于YouTube的一个插件，具体取决于您的配置设置。

1. 完成后，在对话框的右上角附近，点按 **[!UICONTROL 完成]** 图标（复选标记）。
1. 在发布到YouTube工作流页面的右上角附近，点按 **[!UICONTROL 同步]**.

## 为视频资源作批注 {#annotate-video-assets}

1. 从 [!DNL Assets] 控制台，选择 **[!UICONTROL 编辑]** 以显示“资产详细信息”页面。
1. 要播放视频，请单击 **[!UICONTROL 预览]**.
1. 要对视频添加批注，请单击 **[!UICONTROL 批注]**. 在视频中的特定时间（帧）添加注释。 在注释时，可以在画布上绘制并在绘图中包括注释。 评论将自动保存。 要退出注释向导，请单击 **[!UICONTROL 关闭]**.

   ![在视频帧上绘制和批注](assets/annotate-video.png)

1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。

   ![搜寻视频中的时间以跳过指定的秒数](assets/seek-in-video.png)

1. 要在时间轴中查看注释，请单击注释。 要从时间轴中删除注释，请单击 **[!UICONTROL 删除]**.

   ![在时间轴中查看注释和详细信息](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager Assets中管理数字资源](/help/assets/manage-assets.md)
>* [在Experience Manager Assets中管理收藏集](/help/assets/manage-collections.md)
>* [Dynamic Media视频文档](/help/assets/video.md).

