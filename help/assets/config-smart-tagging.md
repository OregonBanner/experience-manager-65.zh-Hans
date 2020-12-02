---
title: 使用智能内容服务配置资产标记
description: 了解如何使用智能内容服务在 [!DNL Adobe Experience Manager]中配置智能标记和增强的智能标记。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 27%

---


# 为智能标记{#configure-asset-tagging-using-the-smart-content-service}准备[!DNL Assets]

在使用智能内容服务开始标记资产之前，请将[!DNL Experience ManageR Assets]与Adobe开发者控制台集成，以利用[!DNL Adobe Sensei]的智能服务。 配置后，使用一些图像和标签培训服务。

在使用智能内容服务之前，请确保：

* [使用 Adobe 开发人员控制台进行集成](#integrate-adobe-io).
* [培训智能内容服务](#training-the-smart-content-service)。

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* 安装最新的[Experience Manager服务包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)。

## 使用 Adobe 开发人员控制台进行集成 {#integrate-adobe-io}

当您与Adobe开发者控制台集成时，[!DNL Experience Manager]服务器会先使用Adobe开发者控制台网关验证您的服务凭据，然后再将请求转发到智能内容服务。 要进行集成，您需要具有Adobe ID帐户，该帐户具有组织的管理员权限，并为您的组织购买和启用智能内容服务许可证。

要配置智能内容服务，请按照以下顶级步骤操作：

1. [在中创建智](#obtain-public-certificate) 能内容服 [!DNL Experience Manager] 务配置以生成公钥。为 OAuth 集成[获取公共证书](#obtain-public-certificate)。

1. [在 Adobe 开发人员控制台中创建集成](#create-adobe-i-o-integration)，并上传生成的公共密钥。

1. [使用Adobe开](#configure-smart-content-service) 发人员控制台中的API密钥和其他凭据配置您的部署。

1. [测试配置](#validate-the-configuration)。

1. （可选）[在资产上传时启用自动标记](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

### 创建智能内容服务配置以获取公共证书{#obtain-public-certificate}

公共证书允许您在 Adobe 开发人员控制台上验证配置文件。

1. 在[!DNL Experience Manager]用户界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 旧Cloud Services]**。

1. 在Cloud Services页面中，单击&#x200B;**[!UICONTROL 资产智能标记]**&#x200B;下的&#x200B;**[!UICONTROL 立即配置]**。

1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定智能标记配置的标题和名称。 单击&#x200B;**[!UICONTROL 创建]**。

1. 在&#x200B;**[!UICONTROL AEM智能内容服务]**&#x200B;对话框中，使用以下值：

   **[!UICONTROL 服务 URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**: `https://ims-na1.adobelogin.com`

   现在将其他字段留空（稍后提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智能内容服务对话框，用于提供内容服务URL](assets/aem_scs.png)


   *图：用于提供内容服务URL的智能内容服务对话框*

   >[!NOTE]
   >
   >作为[!UICONTROL 服务URL]提供的URL无法通过浏览器访问，并生成404错误。 配置工作正常，与[!UICONTROL 服务URL]参数的值相同。 有关总体服务状态和维护计划，请参阅[https://status.adobe.com](https://status.adobe.com)。

1. 单击&#x200B;**[!UICONTROL 下载OAuth集成的公共证书]**，然后下载公共证书文件`AEM-SmartTags.crt`。

   ![为智能标记服务创建的设置的表示形式](assets/smart-tags-download-public-cert.png)


   *图：智能标记服务的设置*

#### 证书过期{#certrenew}时重新配置

证书过期后，它不再受信任。 无法续订已过期的证书。要添加新证书，请执行以下步骤。

1. 以管理员身份登录 [!DNL Experience Manager] 部署。单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。

1. 找到并单击 **[!UICONTROL dam-update-service]** 用户。单击&#x200B;**[!UICONTROL 密钥库]**&#x200B;选项卡。

1. 删除包含已过期证书的现有 **[!UICONTROL similaritysearch]** KeyStore。单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![删除密钥库中现有的相似性搜索条目以添加新的安全证书](assets/smarttags_delete_similaritysearch_keystore.png)


   *图：删除 Keystore 中的现有 `similaritysearch` 条目以添加新的安全证书。*

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL 旧版云服务]**。单击 **[!UICONTROL 资产智能标记]** >显 **[!UICONTROL 示配置]** >可 **[!UICONTROL 用配置]**。 单击所需的配置。

1. 要下载公共证书，请单击&#x200B;**[!UICONTROL 下载OAuth集成的公共证书]**。

1. 访问[https://console.adobe.io](https://console.adobe.io)并导航到&#x200B;**[!UICONTROL 集成]**&#x200B;页面上的现有智能内容服务。 上传新证书。 有关详细信息，请参阅[创建Adobe开发者控制台集成](#create-adobe-i-o-integration)中的说明。

### 创建Adobe开发者控制台集成{#create-adobe-i-o-integration}

要使用智能内容服务API，请在Adobe开发者控制台中创建集成，以获取[!UICONTROL API密钥](在Adobe开发者控制台集成的[!UICONTROL 客户端ID]字段中生成)、[!UICONTROL 技术帐户ID]、[!UICONTROL 组织[!UICONTROL &lt;a10/>资产智能标记服务设置]中云配置的ID]和[!UICONTROL 客户端机密]。[!DNL Experience Manager]

1. 在浏览器中访问 [https://console.adobe.io](https://console.adobe.io/)。选择相应的帐户并验证关联的组织角色是否为系统管理员。

1. 创建具有任何所需名称的项目。单击&#x200B;**[!UICONTROL 添加 API]**。

1. 在&#x200B;**[!UICONTROL 添加 API]** 页面中，依次选择 **[!UICONTROL Experience Cloud]** 和&#x200B;**[!UICONTROL 智能内容]**。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**[!UICONTROL 上传您的公共密钥]**。提供从 [!DNL Experience Manager] 下载的证书文件。此时将显示“[!UICONTROL 公共密钥上传成功]”消息。单击&#x200B;**[!UICONTROL 下一步]**。

   “[!UICONTROL 创建新的服务帐户 (JWT) 凭证]”页面将显示刚刚配置的服务帐户的公共密钥。

1. 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 选择产品配置文件]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 智能内容服务]**。单击&#x200B;**[!UICONTROL 保存配置的 API]**。

   页面会显示有关配置的更多信息。使此页保持打开状态，以复制这些值并在[!DNL Experience Manager]云配置的[!UICONTROL 资产智能标记服务设置]中添加这些值，以配置智能标记。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)


   *图：Adobe开发人员控制台中集成的详细信息*

### 配置智能内容服务{#configure-smart-content-service}

要配置集成，请使用Adobe开发者控制台集成中的[!UICONTROL 技术帐户ID]、[!UICONTROL 组织ID]、[!UICONTROL 客户端机密]和[!UICONTROL 客户端ID]字段的值。 创建智能标记云配置允许验证来自[!DNL Experience Manager]部署的API请求。

1. 在[!DNL Experience Manager]中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 旧Cloud Services]**&#x200B;以打开[!UICONTROL Cloud Services]控制台。

1. 在&#x200B;**[!UICONTROL 资产智能标记]**&#x200B;下，打开以上创建的配置。 在服务设置页面上，单击&#x200B;**[!UICONTROL 编辑]**。

1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。

1. 对于字段[!UICONTROL Api密钥]、[!UICONTROL 技术帐户ID]、[!UICONTROL 组织ID]和[!UICONTROL 客户机密码]，复制并使用在[Adobe开发者控制台集成](#create-adobe-i-o-integration)中生成的以下值。

   | [!UICONTROL 资产智能标记服务设置] | [!DNL Adobe Developer Console] 集成字段 |
   |--- |--- |
   | [!UICONTROL API 键] | [!UICONTROL 客户端ID] |
   | [!UICONTROL 技术帐户 ID] | [!UICONTROL 技术帐户ID] |
   | [!UICONTROL 组织 ID] | [!UICONTROL 组织 ID] |
   | [!UICONTROL 客户端密钥] | [!UICONTROL 客户端机密] |

### 验证配置 {#validate-the-configuration}

完成配置后，可以使用JMX MBean验证配置。 要验证，请按照以下步骤操作。

1. 访问`https://[aem_server]:[port]`的[!DNL Experience Manager]服务器。

1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**&#x200B;以打开OSGi控制台。 单击&#x200B;**[!UICONTROL Main] > [!UICONTROL  JMX]**。

1. 单击 `com.day.cq.dam.similaritysearch.internal.impl`. 它打开&#x200B;**[!UICONTROL SimilaritySearch其他任务]**。

1. 单击 `validateConfigs()`. 在&#x200B;**[!UICONTROL 验证配置]**&#x200B;对话框中，单击&#x200B;**[!UICONTROL 调用]**。

验证结果将显示在同一对话框中。

### 在[!UICONTROL DAM更新资产]工作流中启用智能标记（可选）{#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在[!DNL Experience Manager]中，转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。

1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。

1. 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤](assets/smart-tag-in-dam-update-asset-workflow.png)

   *图：在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤。*

1. 在编辑模式下打开该步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序前进]**&#x200B;选项。

   ![配置DAM更新资产工作流并添加智能标记步骤](assets/smart-tag-step-properties-workflow1.png)


   *图：配置DAM更新资产工作流并添加智能标记步骤*

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望完成工作流，请选择&#x200B;**[!UICONTROL 忽略错误]**，即使自动标记步骤失败也是如此。

   ![配置DAM更新资产工作流以添加智能标记步骤和提前选择处理程序](assets/smart-tag-step-properties-workflow2.png)


   *图：配置DAM更新资产工作流以添加智能标记步骤和提前选择处理程序*

   要在上传资产时标记资产，而不考虑是否对文件夹启用了智能标记，请选择&#x200B;**[!UICONTROL 忽略智能标记标志]**。

   ![配置DAM更新资产工作流以添加智能标记步骤并选择忽略智能标记标记](assets/smart-tag-step-properties-workflow3.png)


   *图：配置DAM更新资产工作流以添加智能标记步骤并选择忽略智能标记标记*

1. 单击&#x200B;**[!UICONTROL 确定]**，以关闭流程步骤，然后保存工作流。

## 培训智能内容服务{#training-the-smart-content-service}

要使智能内容服务识别您的业务分类，请在已包含与您的业务相关标签的资产集上运行它。 为了有效地标记您的品牌图像，智能内容服务要求培训图像符合某些准则。 培训后，服务可以对类似的资产集应用相同的分类。

您可以对服务进行多次培训，以提高应用相关标签的能力。 在每个培训周期后，运行一个标记工作流并检查您的资产是否已正确标记。

您可以定期或根据需要培训智能内容服务。

>[!NOTE]
>
>培训工作流仅在文件夹上运行。

### 培训指南{#guidelines-for-training}

为获得最佳效果，培训集中的图像应符合以下准则：

**数量和大小：**&#x200B;每个标记至少 30 张图像。长边至少 500 像素。

**一致性**:标记的图像应在视觉上相似。

例如，将所有这些图像标记为`my-party`（对于培训）不是个好主意，因为它们在视觉上并不相似。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/coherence.png)

**覆盖**:培训中的图像应该有足够的多样性。我们的想法是提供几个但相当多样化的例子，让Experience Manager学会专注于正确的事情。 如果要对视觉上不相似的图像应用同一标签，请至少包含每种类型的五个示例。

例如，对于标签&#x200B;*模型向下姿势*，包含更多与下面突出显示的图像相似的培训图像，以便服务在标记期间更准确地识别类似图像。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/coverage_1.png)

**干扰／阻碍**:该服务更好地训练那些分散注意力的图像（突出的背景、不相关的伴奏，如有主题的物体／人）。

例如，对于标签&#x200B;*休闲鞋*，第二幅图像不是很好的培训候选者。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 `raincoat` 和 `model-side-view` 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智能内容服务能否训练您的标记并将它们应用于其他图像取决于您用于培训的图像质量。 为获得最佳效果，Adobe建议您使用视觉上相似的图像来为每个标签培训服务。

### 定期培训{#periodic-training}

您可以启用智能内容服务，以定期培训文件夹中的资产和相关标记。 打开资产文件夹的[!UICONTROL 属性]页面，在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡下选择&#x200B;**[!UICONTROL 启用智能标记]**，然后保存更改。

![enable_smart_tags](assets/enable_smart_tags.png)

为文件夹选择此选项后，[!DNL Experience Manager]将自动运行培训工作流，以针对文件夹资产及其标记对智能内容服务进行培训。 默认情况下，培训工作流程每周在星期六的凌晨12:30运行。

### 按需培训{#on-demand-training}

您可以根据需要从工作流控制台培训智能内容服务。

1. 在[!DNL Experience Manager]接口中，转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面中，选择&#x200B;**[!UICONTROL 智能标记培训]**&#x200B;工作流，然后单击工具栏中的&#x200B;**[!UICONTROL 开始工作流]**。
1. 在&#x200B;**[!UICONTROL 运行工作流]**&#x200B;对话框中，浏览至包含用于培训服务的标记资源的有效负荷文件夹。
1. 指定工作流的标题并添加评论。 然后，单击&#x200B;**[!UICONTROL 运行]**。 资产和标记将提交用于培训。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>在对文件夹中的资产进行培训后，仅在后续培训周期中处理修改后的资产。

### 视图培训报告{#viewing-training-reports}

要检查智能内容服务是否在资产培训集中的标记上接受过培训，请从“报告”控制台查看培训工作流报告。

1. 在[!DNL Experience Manager]接口中，转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报告]**。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 创建]**。
1. 选择&#x200B;**[!UICONTROL 智能标记培训]**&#x200B;报告，然后单击工具栏中的&#x200B;**[!UICONTROL 下一步]**。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然后，单击工具栏中的&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。要视图报告，请单击工具栏中的&#x200B;**[!UICONTROL 视图]**。
1. 查看报告的详细信息。

   报表显示您培训的标记的培训状态。**[!UICONTROL 培训状态]**&#x200B;列中的绿色表示已为标记培训“智能内容服务”。黄色表示服务未针对特定标记进行完整培训。在这种情况下，使用特定标记添加更多图像并运行培训工作流以在标签上完整地培训服务。

   如果此报告中未显示标记，请再次运行这些标记的培训工作流程。

1. 要下载报告，请从列表中选择它，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。 报告以Microsoft Excel电子表格的形式下载。

## 限制 {#limitations}

* 增强的智能标签基于图像及其标签的学习模型。 这些模型并不总是能够完美地识别标记。 智能内容服务的当前版本具有以下限制：

   * 无法识别图像中的细微差异。 比如，修身与普通衬衫。
   * 无法根据图像的微小图案／部分识别标记。 例如，T恤上的徽标。
   * 在支持[!DNL Experience Manager]的语言环境中支持标记。 有关语言列表，请参阅[智能内容服务发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

* 要使用智能标记（常规或增强）搜索资产，请使用[!DNL Assets]全文搜索（全文搜索）。 智能标记没有单独的搜索谓词。

>[!MORELIKETHIS]
>
>* [智能标记概述和培训方法](enhanced-smart-tags.md)
>* [有关智能标签的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

