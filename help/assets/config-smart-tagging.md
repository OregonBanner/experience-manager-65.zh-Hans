---
title: 使用智能内容服务配置资产标记。
description: 了解如何使用智能内容服务在中配置智能标记 [!DNL Adobe Experience Manager]，以及增强智能标记功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 43%

---


# 使用智能内容服务配置资产标记 {#configure-asset-tagging-using-the-smart-content-service}

您可以使用 [!DNL Adobe Experience Manager] Adobe开发者控制台与智能内容服务集成。 使用此配置从中访问智能内容服 [!DNL Experience Manager]务。

文章详细列出了配置智能内容服务所需的以下主要任务。 At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. Create a Smart Content Service configuration in [!DNL Experience Manager] to generate a public key. 为 OAuth 集成[获取公共证书](#obtain-public-certificate)。
1. [在 Adobe 开发人员控制台中创建集成](#create-adobe-i-o-integration)，并上传生成的公共密钥。
1. [使用Adobe开发](#configure-smart-content-service) 者控制台中的API密钥和其他凭据配置您的部署。
1. [测试配置](#validate-the-configuration)。
1. （可选） [在资产上传时启用自动标记](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

## 前提条件 {#prerequisites}

在使用智能内容服务之前，请确保在Adobe开发者控制台上创建以下集成：

* 具备拥有组织管理员权限的 Adobe ID 帐户。
* 您的组织已启用智能内容服务。

<!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
-->

除了上述功能之外，要启用增强的智能标记，还要安装最新 [的Experience Manager服务包](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。

## 获取公共证书 {#obtain-public-certificate}

公共证书允许您在 Adobe 开发人员控制台上验证配置文件。

1. 在用户 [!DNL Experience Manager] 界面中，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 旧]**&#x200B;版Cloud Service。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. 在创 **[!UICONTROL 建配置]** 对话框中，指定智能标记配置的标题和名称。 单击&#x200B;**[!UICONTROL 创建]**。
1. 在AEM智 **[!UICONTROL 能内容服务]** 对话框中，使用以下值：

   **[!UICONTROL 服务 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**: `https://ims-na1.adobelogin.com`

   现在将其他字段留空（稍后提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智能内容服务对话框，用于提供内容服务URL](assets/aem_scs.png)

   >[!NOTE]
   >
   >作为服务 [!UICONTROL URL提供的] URL无法通过浏览器访问，并生成404错误。 配置与服务URL参数的值相同， [!UICONTROL 可以正常] 。 有关整体服务状态和维护计划，请参 [阅https://status.adobe.com](https://status.adobe.com)。

1. 单击 **[!UICONTROL “下载用于OAuth集成的公共证书]**”，然后下载公共证书文件 `AEM-SmartTags.crt`。

   ![为智能标记服务创建的设置的表示形式](assets/smart-tags-download-public-cert.png)

### Reconfigure when a certificate expires {#certrenew}

证书过期后，它不再受信任。 无法续订已过期的证书。要添加新证书，请执行以下步骤。

1. 以管理员身份登录 [!DNL Experience Manager] 部署。单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。

1. 找到并单击 **[!UICONTROL dam-update-service]** 用户。单击 **[!UICONTROL KeyStore]** 选项卡。
1. 删除包含已过期证书的现有 **[!UICONTROL similaritysearch]** KeyStore。单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![删除密钥库中现有的相似性搜索条目以添加新的安全证书](assets/smarttags_delete_similaritysearch_keystore.png)

   *图：删除 Keystore 中的现有`similaritysearch`条目以添加新的安全证书。*

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL 旧版云服务]**。单击 **[!UICONTROL 资产智能标记]** >显 **[!UICONTROL 示配置]** >可 **[!UICONTROL 用配置]**。 单击所需的配置。

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.
1. 访 [问https://console.adobe.io](https://console.adobe.io) ，并导航到“集成”页面上的现有智能 **[!UICONTROL 内容]** 服务。 上传新证书。 For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## 创建Adobe开发人员控制台集成 {#create-adobe-i-o-integration}

要使用智能内容服务API，请在Adobe开发人员控制台中创建集成，以生成API密钥、技术帐户ID、组织ID和客户端机密。

1. 在浏览器中访问 [https://console.adobe.io](https://console.adobe.io/)。选择相应的帐户并验证关联的组织角色是否为系统管理员。
1. 创建具有任何所需名称的项目。单击&#x200B;**[!UICONTROL 添加 API]**。
1. 在&#x200B;**[!UICONTROL 添加 API]** 页面中，依次选择 **[!UICONTROL Experience Cloud]** 和&#x200B;**[!UICONTROL 智能内容]**。单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择&#x200B;**[!UICONTROL 上传您的公共密钥]**。提供从 [!DNL Experience Manager] 下载的证书文件。此时将显示“[!UICONTROL 公共密钥上传成功]”消息。单击&#x200B;**[!UICONTROL 下一步]**。
1. “[!UICONTROL 创建新的服务帐户 (JWT) 凭证]”页面将显示刚刚配置的服务帐户的公共密钥。单击&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 选择产品配置文件]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 智能内容服务]**。单击&#x200B;**[!UICONTROL 保存配置的 API]**。页面会显示有关配置的更多信息。在 [!DNL Experience Manager] 中进一步配置智能标记时，请保持此页面处于打开状态，以复制这些值，并将其添加到 Experience Manager 中。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)

## 配置智能内容服务 {#configure-smart-content-service}

要配置集成，请使用Adobe开发人员控制台集成中的技术帐户ID、组织ID、客户端机密、授权服务器和API密钥字段的值。 创建智能标记云配置允许对部署中的API请求进行 [!DNL Experience Manager] 身份验证。

1. 在中， [!DNL Experience Manager]导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL LegacyCloud Service，以]** 便打开控制台  ，从而打开旧式Cloud Service控制台。
1. 在资产 **[!UICONTROL 智能标记下]**，打开以上创建的配置。 在服务设置页面上，单击 **[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。
1. 对于字段 **[!UICONTROL API 密钥]**、**[!UICONTROL 技术帐户 ID]**、**[!UICONTROL 组织 ID]** 和&#x200B;**[!UICONTROL 客户端密钥]**，请使用上面生成的值。

## 验证配置 {#validate-the-configuration}

完成配置后，可使用JMX MBean验证配置。 要验证，请按照以下步骤操作。

1. 访问您 [!DNL Experience Manager] 的服务器 `https://[aem_server]:[port]`。
1. 转到 **[!UICONTROL 工具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Web控制台]** ，打开OSGi控制台。 单击 **[!UICONTROL “主]>[!UICONTROL JMX]**”。
1. 单击 `com.day.cq.dam.similaritysearch.internal.impl`. 它打开“相似 **[!UICONTROL 性搜索”杂项任务]**。
1. 单击 `validateConfigs()`. 在验证 **[!UICONTROL 配置对话框中]** ，单击调 **[!UICONTROL 用]**。 验证结果将显示在同一对话框中。

## 在DAM更新资产工作流 [!UICONTROL 程中启用智能标] 记（可选） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。
1. 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。
1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤](assets/smart-tag-in-dam-update-asset-workflow.png)

   *图：在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤。*

1. 在编辑模式下打开该步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序前进]**&#x200B;选项。

   ![配置DAM更新资产工作流并添加智能标记步骤](assets/smart-tag-step-properties-workflow1.png)

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望完成工作流，请选择&#x200B;**[!UICONTROL 忽略错误]**，即使自动标记步骤失败也是如此。

   要在上传资产时标记资产，而不考虑是否对文件夹启用了智能标记，请选择&#x200B;**[!UICONTROL 忽略智能标记标志]**。

   ![配置DAM更新资产工作流以添加智能标记步骤并选择忽略智能标记标记](assets/smart-tag-step-properties-workflow2.png)

1. 单击&#x200B;**[!UICONTROL 确定]**，以关闭流程步骤，然后保存工作流。

>[!MORELIKETHIS]
>
>* [管理智能标记](managing-smart-tags.md)
>* [智能标记概述和培训方法](enhanced-smart-tags.md)
>* [培训智能内容服务的准则和规则](smart-tags-training-guidelines.md)
>* [有关如何配置智能标记的视频教程](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

