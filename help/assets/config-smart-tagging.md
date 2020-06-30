---
title: 使用智能内容服务配置资产标记。
description: 了解如何使用智能内容服务在Adobe Experience Manager中配置智能标记和增强的智能标记。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f3d699f35c7b1ef832a0857fa2fa41aed1fe5a4e
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 15%

---


# 使用智能内容服务配置资产标记 {#configure-asset-tagging-using-the-smart-content-service}

您可以使 [!DNL Adobe Experience Manager] 用Adobe开发人员控制台与智能内容服务集成。 使用此配置从中访问智能内容服 [!DNL Experience Manager]务。

文章详细列出了配置智能内容服务所需的以下主要任务。 在后端，服务器在将 [!DNL Experience Manager] 您的请求转发到智能内容服务之前，使用Adobe开发人员控制台网关验证您的服务凭据。

* 在中创建智能内容服 [!DNL Experience Manager] 务配置以生成公钥。 获取用于OAuth集成的公共证书。
* 在Adobe开发人员控制台中创建集成并上传生成的公钥。
* 使用Adobe [!DNL Experience Manager] 开发人员控制台中的API密钥和其他凭据配置您的实例。
* （可选）在资产上传时启用自动标记。

## 前提条件 {#prerequisites}

在使用智能内容服务之前，请确保在Adobe开发人员控制台上创建集成：

* 具有组织管理员权限的Adobe ID帐户。
* 您的组织已启用智能内容服务。

## 获取公共证书 {#obtain-public-certificate}

公共证书允许您在Adobe开发人员控制台上验证用户档案。

1. 在用户 [!DNL Experience Manager] 界面中，访问 **[!UICONTROL 工具>Cloud Service]**>旧 **[!UICONTROL 版Cloud Service]**。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. 在创 **[!UICONTROL 建配置]** 对话框中，指定智能标记配置的标题和名称。 单击&#x200B;**[!UICONTROL 创建]**。
1. 在AEM **[!UICONTROL 智能内容服务]** 对话框中，使用以下值：

   **[!UICONTROL 服务 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**: `https://ims-na1.adobelogin.com`

   现在将其他字段留空（稍后提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智能内容服务对话框，用于提供内容服务URL](assets/aem_scs.png)

1. 单击 **[!UICONTROL “下载用于OAuth集成的公共证书]**”，然后下载公共证书文件 `AEM-SmartTags.crt`。

   ![为智能标记服务创建的设置的表示形式](assets/smart-tags-download-public-cert.png)

### 证书过期时重新配置 {#certrenew}

证书过期后，它不再受信任。 无法续订过期的证书。 要添加新证书，请执行以下步骤。

1. Log in your [!DNL Experience Manager] deployment as an administrator. 单击“ **[!UICONTROL 工具]** ”>“安 **[!UICONTROL 全]** ” **[!UICONTROL >“]**&#x200B;用户”。

1. 找到并单 **[!UICONTROL 击dam-update-service用户]** 。 单击“密 **[!UICONTROL 钥库]** ”选项卡。
1. 删除已过期 **[!UICONTROL 证书的]** 现有相似性搜索密钥库。 Click **[!UICONTROL Save &amp; Close]**.

   ![删除密钥库中现有的相似性搜索条目以添加新的安全证书](assets/smarttags_delete_similaritysearch_keystore.png)

   *图： 删除密钥库`similaritysearch`中的现有条目以添加新的安全证书。*

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL 旧版云服务]**。单击 **[!UICONTROL 资产智能标记]** >显 **[!UICONTROL 示配置]** >可 **[!UICONTROL 用配置]**。 单击所需的配置。

1. 要下载公共证书，请单击“ **[!UICONTROL 下载用于OAuth集成的公共证书”]**。
1. 访 [问https://console.adobe.io](https://console.adobe.io) ，然后导航到“集成”页面上的现有智能 **[!UICONTROL 内容]** 服务。 上传新证书。 有关详细信息，请参阅创建Adobe开 [发人员控制台集成中的说明](#create-adobe-i-o-integration)。

## 创建Adobe Developer Console集成 {#create-adobe-i-o-integration}

要使用智能内容服务API，请在Adobe开发人员控制台中创建集成，以生成API密钥、技术帐户ID、组织ID和客户端机密。

1. 在浏 [览器](https://console.adobe.io/) 中访问https://console.adobe.io。 选择相应的帐户并验证关联的组织角色是系统管理员。
1. 创建具有任何所需名称的项目。 单击 **[!UICONTROL 添加API]**。
1. 在“添 **[!UICONTROL 加API”页]** ，选择 **[!UICONTROL Experience Cloud]** ，然 **[!UICONTROL 后选择智能内容]**。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择 **[!UICONTROL 上传您的公钥]**。 提供从下载的证书文件 [!DNL Experience Manager]。 将显 [!UICONTROL 示一条消息，成功上传] 公钥。 单击&#x200B;**[!UICONTROL 下一步]**。
1. [!UICONTROL 创建新的服务帐户(JWT)凭据页] ，将显示刚刚配置的服务帐户的公钥。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在“选 **[!UICONTROL 择产品用户档案]** ”页面上，选 **[!UICONTROL 择智能内容服务]**。 单击 **[!UICONTROL 保存配置的API]**。 页面会显示有关配置的更多信息。 在中进一步配置智能标记时，请保持此页面处于打开状态，以复制这些值并在Experience Manager中添加 [!DNL Experience Manager]这些。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)

## 配置智能内容服务 {#configure-smart-content-service}

要配置集成，请使用Adobe开发人员控制台集成中的技术帐户ID、组织ID、客户端机密、授权服务器和API密钥字段的值。 创建智能标记云配置允许验证来自实例的API [!DNL Experience Manager] 请求。

1. 在中 [!DNL Experience Manager]，导航到 **[!UICONTROL 工具>Cloud Service>旧Cloud Service]** ，以打开 [!UICONTROL Cloud Service控] 制台。
1. 在资产 **[!UICONTROL 智能标记下]**，打开以上创建的配置。 在服务设置页面上，单击 **[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。
1. 对于字段 **[!UICONTROL API 密钥]**、**[!UICONTROL 技术帐户 ID]**、**[!UICONTROL 组织 ID]** 和&#x200B;**[!UICONTROL 客户端密钥]**，请使用上面生成的值。

## 验证配置 {#validate-the-configuration}

完成配置后，可使用JMX MBean验证配置。 要验证，请按照以下步骤操作。

1. 访问您 [!DNL Experience Manager] 的服务器 `https://[aem_server]:[port]`。

1. 转到“ **[!UICONTROL 工具”>“操作”>“Web控制台]** ”以打开OSGi控制台。 单击 **[!UICONTROL “主> JMX]**”。
1. 单 **[!UICONTROL 击com.day.cq.dam.similaritysearch.internal.impl]**。 它打开“相似 **[!UICONTROL 性搜索”杂项任务]**。
1. 单 **[!UICONTROL 击validateConfigs()]**。 在验证 **[!UICONTROL 配置对话框中]** ，单击调 **[!UICONTROL 用]**。

   验证结果显示在同一对话框中。

## 在DAM更新资产工作流中启用智能标记（可选） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在中， [!DNL Experience Manager]转到“工 **[!UICONTROL 具”>“工作流”>“模型”]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。
1. 单击工 **[!UICONTROL 具栏]** 中的编辑。
1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在DAM更新资产工作流中的流程缩略图步骤之后添加 [!UICONTROL 智能标记资产步] 骤](assets/smart-tag-in-dam-update-asset-workflow.png)

   *图： 在DAM更新资产工作流中的流程缩略图步骤之[!UICONTROL 后添加智能标记资产]步骤。*

1. 在编辑模式下打开该步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序高级]**&#x200B;选项。

   ![配置DAM更新资产工作流并添加智能标记步骤](assets/smart-tag-step-properties-workflow1.png)

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望完成工作流，请选择&#x200B;**[!UICONTROL 忽略错误]**，即使自动标记步骤失败也是如此。

   ![配置DAM更新资产工作流以添加智能标记步骤和提前选择处理程序](assets/smart-tag-step-properties-workflow2.png)

   要在上传资产时标记资产，而不管是否在文件夹中启用智能标记，请选 **[!UICONTROL 择忽略智能标记标志]**。

   ![配置DAM更新资产工作流以添加智能标记步骤并选择忽略智能标记标记](assets/smart-tag-step-properties-workflow3.png)

1. 单击 **[!UICONTROL 确定]** ，以关闭流程步骤，然后保存工作流。

>[!MORELIKETHIS]
>
>* [管理智能标记](managing-smart-tags.md)
>* [智能标记概述和培训方法](enhanced-smart-tags.md)
>* [培训智能内容服务的准则和规则](smart-tags-training-guidelines.md)
>* [有关如何配置智能标记的视频教程](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

