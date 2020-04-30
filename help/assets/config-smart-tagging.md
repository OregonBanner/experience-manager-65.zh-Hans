---
title: 使用智能内容服务配置资产标记。
description: 了解如何使用智能内容服务在Adobe Experience Manager中配置智能标记和增强的智能标记。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 使用智能内容服务配置资产标记 {#configure-asset-tagging-using-the-smart-content-service}

您可以 [!DNL Adobe Experience Manager] 使用Adobe I/O与智能内容服务集成。使用此配置可从中访问智能内容服务 [!DNL Experience Manager]。

文章详细介绍了配置智能内容服务所需的以下主要任务。 在后端，服务器在将 [!DNL Experience Manager] 您的请求转发到智能内容服务之前，使用Adobe I/O网关验证您的服务凭据。

* 在中创建智能内容服务配 [!DNL Experience Manager] 置以生成公钥。 获取用于OAuth集成的公共证书。
* 在Adobe I/O中创建集成并上传生成的公钥。
* 使用 [!DNL Experience Manager] Adobe I/O的API密钥和其他凭据配置实例。
* （可选）在资产上传时启用自动标记。

## 前提条件 {#prerequisites}

在使用智能内容服务之前，请确保以下各项在Adobe I/O上创建集成：

* 具有组织管理员权限的Adobe ID帐户。
* 您的组织启用了智能内容服务。

## 获取公共证书 {#obtain-public-certificate}

公共证书允许您在Adobe I/O上验证用户档案。

1. 在用户 [!DNL Experience Manager] 界面中，访问 **[!UICONTROL 工具>云服务]**> **[!UICONTROL 旧版云服务]**。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. 在“创 **[!UICONTROL 建配置]** ”对话框中，指定智能标记配置的标题和名称。 单击&#x200B;**[!UICONTROL 创建]**。
1. 在 **[!UICONTROL AEM智能内容服务对话框中]** ，使用以下值：

   **[!UICONTROL 服务 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**: `https://ims-na1.adobelogin.com`

   现在将其他字段留空（稍后提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智能内容服务对话框，用于提供内容服务URL](assets/aem_scs.png)

1. 单击 **[!UICONTROL “下载用于OAuth集成的公共证书]**”，然后下载公共证书文件 `AEM-SmartTags.crt`。

   ![为智能标记服务创建的设置的表示形式](assets/download_link.png)

### 证书过期时重新配置 {#certrenew}

证书到期后，不再受信任。 要添加新证书，请执行以下步骤。 您无法续订过期的证书。

1. Log in your [!DNL Experience Manager] deployment as an administrator. 单击“ **[!UICONTROL 工具]** ”>“安 **[!UICONTROL 全]** ” **[!UICONTROL >“]**&#x200B;用户”。

1. 找到并单 **[!UICONTROL 击dam-update-service用户]** 。 单击“ **[!UICONTROL Keystore]** ”选项卡。
1. 删除现有的 **[!UICONTROL 相似性search]** keystore及过期的证书。 Click **[!UICONTROL Save &amp; Close]**.

   ![删除Keystore中现有的相似性搜索条目以添加新的安全证书](assets/smarttags_delete_similaritysearch_keystore.png)

   删除Keystore中现有的相似性搜索条目以添加新的安全证书

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL 旧版云服务]**。单击 **[!UICONTROL 资产智能标记]** >显 **[!UICONTROL 示配置]** >可 **[!UICONTROL 用配置]**。 单击所需的配置。

1. 要下载公共证书，请单击“下 **[!UICONTROL 载用于OAuth集成的公共证书”]**。
1. 访 [问https://console.adobe.io](https://console.adobe.io) ，然后导航到“集成”页面上的现有智能 **[!UICONTROL 内容服务]** 。 上传新证书。 有关详细信息，请参阅创建 [Adobe I/O集成中的说明](#create-adobe-i-o-integration)。

## 创建 Adobe I/O 集成 {#create-adobe-i-o-integration}

要使用智能内容服务API，请在Adobe I/O中创建集成，以生成API密钥、技术帐户Id、组织Id和客户端机密。

1. 访问 [https://console.adobe.io](https://console.adobe.io/)。
1. 在“集 **[!UICONTROL 成]** ”页面上，选择相应的帐户并验证关联的组织角色是否为系统管理员。
1. 单击“ **[!UICONTROL 新建集成]**”。
1. 在“创 **[!UICONTROL 建新集成]** ”页面上，选 **[!UICONTROL 择访问API]**。 单击“ **[!UICONTROL 继续]**”。
1. 在 **[!UICONTROL Experience Cloud]** 下，选择&#x200B;**[!UICONTROL 智能内容]**。单击“ **[!UICONTROL 继续]**”。

   ![创建新集成时，从可用的选项中选择Experience Cloud下的智能内容](assets/smart_content.png)

1. 在下一页，选择“新 **[!UICONTROL 建集成”]**。 单击“ **[!UICONTROL 继续]**”。
1. 在“集 **[!UICONTROL 成详细信息]** ”页面上，指定集成网关的名称并添加说明。
1. 在公 **[!UICONTROL 钥证书中]**，上 `AEM-SmartTags.crt` 传您上面下载的文件。
1. 单击&#x200B;**[!UICONTROL 创建集成]**。
1. 要视图集成信息，请单击“继 **[!UICONTROL 续”以查看集成详细信息]**。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)

## 配置智能内容服务 {#configure-smart-content-service}

要配置集成，请使用Adobe I/O集成中的“技术帐户ID”、“组织ID”、“客户端机密”、“授权服务器”和API密钥字段的值。 创建智能标记云配置允许对来自实例的API请求进行 [!DNL Experience Manager] 身份验证。

1. 在中， [!DNL Experience Manager]导航到工 **[!UICONTROL 具>云服务>旧版云服务]** ，以打开云服 [!UICONTROL 务控制台] 。
1. 在资产智 **[!UICONTROL 能标记下]**，打开上面创建的配置。 在服务设置页面上，单击“编 **[!UICONTROL 辑”]**。
1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。
1. 对于字段 **[!UICONTROL API 密钥]**、**[!UICONTROL 技术帐户 ID]**、**[!UICONTROL 组织 ID]** 和&#x200B;**[!UICONTROL 客户端密钥]**，请使用上面生成的值。

## 验证配置 {#validate-the-configuration}

完成配置后，可使用JMX MBean验证配置。 要验证，请按照以下步骤操作。

1. 访问您 [!DNL Experience Manager] 的服务器 `https://[aem_server]:[port]`。

1. 转到“工 **[!UICONTROL 具”>“操作”>“Web控制台]** ”以打开OSGi控制台。 单击“ **[!UICONTROL 主> JMX]**”。
1. 单 **[!UICONTROL 击com.day.cq.dam.similaritysearch.internal.impl]**。 它打开SimilaritySearch **[!UICONTROL 杂项任务。]**
1. 单击 **[!UICONTROL validateConfigs()]**。 在“验证 **[!UICONTROL 配置]** ”对话框中，单 **[!UICONTROL 击调用]**。

   验证结果将显示在同一对话框中。

## 在更新资产工作流程中启用智能标记（可选） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在中， [!DNL Experience Manager]转到“工 **[!UICONTROL 具”>“工作流”>“模型”]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。
1. 单击 **[!UICONTROL 工具栏]** 中的编辑。
1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在 [!UICONTROL DAM更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤] 。](assets/chlimage_1-105.png)

   *图：在[!UICONTROL DAM更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤]。*

1. 在编辑模式下打开该步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序高级]**&#x200B;选项。

   ![chlimage_1-3](assets/chlimage_1-106.png)

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望完成工作流，请选择&#x200B;**[!UICONTROL 忽略错误]**，即使自动标记步骤失败也是如此。

   ![chlimage_1-4](assets/chlimage_1-107.png)

   要在上传资产时标记资产，而不管文件夹是否启用了智能标记，请选择忽 **[!UICONTROL 略智能标记标志]**。

   ![chlimage_1-5](assets/chlimage_1-108.png)

1. 单击 **[!UICONTROL 确定]** ，以关闭进程步骤，然后保存工作流。

>[!MORELIKETHIS]
>
>* [管理智能标记](managing-smart-tags.md)
>* [智能标记的概述和如何培训](enhanced-smart-tags.md)
>* [培训智能内容服务的准则和规则](smart-tags-training-guidelines.md)
>* [有关如何配置智能标记的视频教程](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

