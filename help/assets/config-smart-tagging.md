---
title: 使用智慧內容服務設定資產標籤
description: 瞭解如何在中設定智慧標籤和增強智慧標籤 [!DNL Adobe Experience Manager]，使用智慧內容服務。
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 25%

---

# 準備 [!DNL Assets] 用於智慧標籤 {#configure-asset-tagging-using-the-smart-content-service}

開始使用Smart Content Services標籤資產之前，請先整合 [!DNL Experience Manager Assets] Adobe Developer Console所提供的智慧服務， [!DNL Adobe Sensei]. 設定完成後，請使用一些影像和標籤來訓練服務。

>[!NOTE]
>
>* 新使用者無法再使用智慧內容服務 [!DNL Experience Manager Assets] 內部部署客戶。 已啟用此功能的現有內部部署客戶可以繼續使用智慧內容服務。
>* 智慧內容服務適用於現有 [!DNL Experience Manager Assets] 已啟用此功能的Managed Services客戶。
>* 新增 [!DNL Experience Manager Assets] Managed Services客戶可以依照本文所述的指示，設定智慧內容服務。


在使用智慧內容服務之前，請確定以下事項：

* [使用 Adobe 开发人员控制台进行集成](#integrate-adobe-io).
* [訓練智慧內容服務](#training-the-smart-content-service).

* 安裝最新的 [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## 使用 Adobe 开发人员控制台进行集成 {#integrate-adobe-io}

當您整合Adobe Developer Console時， [!DNL Experience Manager] 伺服器會先透過Adobe Developer主控台閘道驗證服務認證，再將您的請求轉送至智慧內容服務。 若要整合，您需要具有組織管理員許可權的Adobe ID帳戶，以及為貴組織購買並啟用的Smart Content Service授權。

若要設定Smart Content Service，請遵循下列頂層步驟：

1. 若要產生公開金鑰， [建立智慧內容服務](#obtain-public-certificate) 中的設定 [!DNL Experience Manager]. 为 OAuth 集成[获取公共证书](#obtain-public-certificate)。

1. [在 Adobe 开发人员控制台中创建集成](#create-adobe-i-o-integration)，并上传生成的公共密钥。

1. [設定您的部署](#configure-smart-content-service) 從Adobe Developer主控台使用API金鑰和其他認證。

1. [测试配置](#validate-the-configuration)。

1. 或者， [在資產上傳時啟用自動標籤](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### 透過建立智慧內容服務設定來取得公開憑證 {#obtain-public-certificate}

公共证书允许您在 Adobe 开发人员控制台上验证配置文件。

1. 在 [!DNL Experience Manager] 使用者介面，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 舊版Cloud Services]**.

1. 在Cloud Services頁面中，按一下 **[!UICONTROL 立即設定]** 在 **[!UICONTROL 資產智慧標籤]**.

1. 在 **[!UICONTROL 建立設定]** 對話方塊中，指定智慧標籤設定的標題和名稱。 单击&#x200B;**[!UICONTROL 创建]**。

1. 在 **[!UICONTROL AEM智慧內容服務]** 對話方塊中，使用以下值：

   **[!UICONTROL 服务 URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   例如， `https://smartcontent.adobe.io/apac`. 您可以指定 `na`， `emea`，或， `apac` 作為託管Experience Manager作者執行個體的地區。

   >[!NOTE]
   >
   >如果Experience Manager Managed Service是在2022年9月1日之前布建，請使用下列服務URL：
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**: `https://ims-na1.adobelogin.com`

   其他欄位暫時保留空白（稍後提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智慧內容服務對話方塊以提供內容服務URL](assets/aem_scs.png)


   *圖：提供內容服務URL的智慧內容服務對話方塊*

   >[!NOTE]
   >
   >提供的URL為 [!UICONTROL 服務URL] 無法透過瀏覽器存取，並產生404錯誤。 設定使用相同的值正常運作 [!UICONTROL 服務URL] 引數。 如需整體服務狀態和維護排程，請參閱 [https://status.adobe.com](https://status.adobe.com).

1. 按一下 **[!UICONTROL 下載公開憑證以進行OAuth整合]**，並下載公開憑證檔案 `AEM-SmartTags.crt`.

   ![為智慧標籤服務建立的設定表示法](assets/smart-tags-download-public-cert.png)


   *圖：智慧標籤服務的設定。*

#### 憑證過期時重新設定 {#certrenew}

憑證過期後，即不再受信任。 无法续订已过期的证书。若要新增憑證，請按照以下步驟操作。

1. 以管理员身份登录 [!DNL Experience Manager] 部署。单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用户]**。

1. 找到并单击 **[!UICONTROL dam-update-service]** 用户。按一下 **[!UICONTROL 金鑰存放區]** 標籤。

1. 删除包含已过期证书的现有 **[!UICONTROL similaritysearch]** KeyStore。单击&#x200B;**[!UICONTROL 保存并关闭]**。

   ![刪除Keystore中現有的相似性搜尋專案，以新增安全性憑證](assets/smarttags_delete_similaritysearch_keystore.png)


   *圖：刪除現有的 `similaritysearch` Keystore中的專案以新增安全性憑證。*

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 云服务]** > **[!UICONTROL 旧版云服务]**。单击 **[!UICONTROL 资产智能标记]** >显 **[!UICONTROL 示配置]** >可 **[!UICONTROL 用配置]**。 单击所需的配置。

1. 若要下載公開憑證，請按一下 **[!UICONTROL 下載公開憑證以進行OAuth整合]**.

1. 存取 [https://console.adobe.io](https://console.adobe.io) 並導覽至 **[!UICONTROL 整合]** 頁面。 上傳新憑證。 如需詳細資訊，請參閱 [建立Adobe Developer主控台整合](#create-adobe-i-o-integration).

### 建立Adobe Developer主控台整合 {#create-adobe-i-o-integration}

若要使用Smart Content Service API，請在Adobe Developer主控台中建立整合，以取得 [!UICONTROL API金鑰] (產生於 [!UICONTROL 使用者端ID] Adobe Developer欄位)， [!UICONTROL 技術帳戶ID]， [!UICONTROL 組織ID]、和 [!UICONTROL 使用者端密碼] 的 [!UICONTROL 資產智慧標籤服務設定] 中的雲端設定 [!DNL Experience Manager].

1. 在浏览器中访问 [https://console.adobe.io](https://console.adobe.io/)。选择相应的帐户并验证关联的组织角色是否为系统管理员。

1. 创建具有任何所需名称的项目。单击&#x200B;**[!UICONTROL 添加 API]**。

1. 在&#x200B;**[!UICONTROL 添加 API]** 页面中，依次选择 **[!UICONTROL Experience Cloud]** 和&#x200B;**[!UICONTROL 智能内容]**。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**[!UICONTROL 上传您的公共密钥]**。提供从 [!DNL Experience Manager] 下载的证书文件。此时将显示“[!UICONTROL 公共密钥上传成功]”消息。单击&#x200B;**[!UICONTROL 下一步]**。

   [!UICONTROL 建立新的服務帳戶(JWT)認證] 頁面會顯示服務帳戶的公開金鑰。

1. 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 选择产品配置文件]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 智能内容服务]**。单击&#x200B;**[!UICONTROL 保存配置的 API]**。

   页面会显示有关配置的更多信息。保持此頁面開啟，以複製這些值並新增至 [!UICONTROL 資產智慧標籤服務設定] 中的雲端設定 [!DNL Experience Manager] 以設定智慧標籤。

   ![在“概述”选项卡中，您可以查看为集成提供的信息。](assets/integration_details.png)


   *圖：Adobe Developer主控台中的整合詳細資料*

### 設定智慧內容服務 {#configure-smart-content-service}

若要設定整合，請使用 [!UICONTROL 技術帳戶ID]， [!UICONTROL 組織ID]， [!UICONTROL 使用者端密碼]、和 [!UICONTROL 使用者端ID] Adobe Developer主控台整合中的欄位。 建立智慧標籤雲端設定，可驗證來自以下專案的API請求： [!DNL Experience Manager] 部署。

1. 在 [!DNL Experience Manager]，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 舊版Cloud Services]** 以開啟 [!UICONTROL Cloud Services] 主控台。

1. 在 **[!UICONTROL 資產智慧標籤]**，開啟上方建立的設定。 在服務設定頁面上，按一下 **[!UICONTROL 編輯]**.

1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。

1. 針對欄位 [!UICONTROL Api金鑰]， [!UICONTROL 技術帳戶ID]， [!UICONTROL 組織ID]、和 [!UICONTROL 使用者端密碼]，複製並使用中產生的下列值 [Adobe Developer主控台整合](#create-adobe-i-o-integration).

   | [!UICONTROL 资产智能标记服务设置] | [!DNL Adobe Developer Console] 整合欄位 |
   |--- |--- |
   | [!UICONTROL API 键] | [!UICONTROL 使用者端ID] |
   | [!UICONTROL 技术帐户 ID] | [!UICONTROL 技術帳戶ID] |
   | [!UICONTROL 组织 ID] | [!UICONTROL 组织 ID] |
   | [!UICONTROL 客户端密钥] | [!UICONTROL 使用者端密碼] |

### 验证配置 {#validate-the-configuration}

完成設定後，您可以使用JMX MBean來驗證設定。 若要進行驗證，請按照以下步驟操作。

1. 存取您的 [!DNL Experience Manager] 伺服器位置 `https://[aem_server]:[port]`.

1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]** 以開啟OSGi主控台。 按一下 **[!UICONTROL 主要] > [!UICONTROL JMX]**.

1. 单击 `com.day.cq.dam.similaritysearch.internal.impl`. 隨即開啟 **[!UICONTROL 相似性搜尋其他任務]**.

1. 单击 `validateConfigs()`. 在 **[!UICONTROL 驗證設定]** 對話方塊，按一下 **[!UICONTROL 叫用]**.

驗證結果會顯示在同一個對話方塊中。

### 在中啟用智慧標籤 [!UICONTROL DAM更新資產] 工作流程（選擇性） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. 在 [!DNL Experience Manager]，前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面上，选择 **[!UICONTROL DAM 更新资产]**&#x200B;工作流模式。

1. 单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

1. 展开侧面板以显示步骤。拖动 DAM 工作流部分中可用的&#x200B;**[!UICONTROL 智能标记资产]**&#x200B;步骤，并将其放在&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤之后。

   ![在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤](assets/smart-tag-in-dam-update-asset-workflow.png)

   *图：在 DAM 更新资产工作流中的流程缩略图步骤之后添加智能标记资产步骤。*

1. 在编辑模式下打开该步骤。在&#x200B;**[!UICONTROL 高级设置]**&#x200B;下，确保选中&#x200B;**[!UICONTROL 处理程序前进]**&#x200B;选项。

   ![設定DAM更新資產工作流程並新增智慧標籤步驟](assets/smart-tag-step-properties-workflow1.png)


   *圖：設定DAM更新資產工作流程並新增智慧標籤步驟*

1. 在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中，如果希望完成工作流，请选择&#x200B;**[!UICONTROL 忽略错误]**，即使自动标记步骤失败也是如此。

   ![設定DAM更新資產工作流程，以新增智慧標籤步驟並選取處理常式前進](assets/smart-tag-step-properties-workflow2.png)


   *圖：設定DAM更新資產工作流程以新增智慧標籤步驟並選取進階處理常式*

   要在上传资产时标记资产，而不考虑是否对文件夹启用了智能标记，请选择&#x200B;**[!UICONTROL 忽略智能标记标志]**。

   ![設定DAM更新資產工作流程以新增智慧標籤步驟，並選取忽略智慧標籤標幟](assets/smart-tag-step-properties-workflow3.png)


   *圖：設定DAM更新資產工作流程以新增智慧標籤步驟，並選取忽略智慧標籤標幟。*

1. 单击&#x200B;**[!UICONTROL 确定]**，以关闭流程步骤，然后保存工作流。

## 訓練智慧內容服務 {#training-the-smart-content-service}

若要讓智慧內容服務辨識您的企業分類法，請在已包含與您的企業相關之標籤的一組資產上執行它。 為了有效標籤您的品牌影像，智慧內容服務要求培訓影像符合特定准則。 訓練後，此服務可以對類似的一組資產套用相同的分類法。

您可以訓練服務多次，以提高其套用相關標籤的能力。 在每個訓練週期後，執行標籤工作流程，並檢查資產是否已正確標籤。

您可以定期或依需求訓練智慧內容服務。

>[!NOTE]
>
>訓練工作流程僅在資料夾上執行。

### 訓練准則 {#guidelines-for-training}

為達到最佳效果，訓練集中的影像需符合下列准則：

**数量和大小：**&#x200B;每个标记至少 30 张图像。长边至少 500 像素。

**一致性**：用於特定標籤的影像在視覺上類似。

例如，將所有影像標示為 `my-party` （適用於訓練），因為視覺上並不相似。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/coherence.png)

**涵蓋範圍**：在訓練中使用足夠的影像變化。 我們的想法是提供一些相當多元化的範例，讓Experience Manager學會專注於正確的事情。 如果您要在視覺上相異的影像上套用相同的標籤，請至少包含每種型別的五個範例。

例如，對於標籤 *模型向下姿態*，加入更多與下方醒目提示影像類似的培訓影像，以便服務在標籤期間更準確地識別類似影像。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/coverage_1.png)

**干擾/阻礙**：此服務會針對干擾較少的影像（顯著背景、不相關的隨附，例如主要主題的物件/人員）提供更好的訓練。

例如，對於標籤 *休閒鞋*，第二個影像不是良好的訓練候選項。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 `raincoat` 和 `model-side-view` 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![說明性影像，以示範訓練准則](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>智慧型內容服務是否能在您的標籤上訓練並套用至其他影像，取決於您用於訓練的影像品質。 為達到最佳效果，Adobe建議您使用視覺上相似的影像，來訓練每個標籤的服務。

### 定期訓練 {#periodic-training}

您可以讓智慧內容服務定期訓練資料夾中的資產和關聯標籤。 開啟 [!UICONTROL 屬性] 頁面，選取 **[!UICONTROL 啟用智慧標籤]** 在 **[!UICONTROL 詳細資料]** 標籤，並儲存變更。

![enable_smart_tags](assets/enable_smart_tags.png)

為資料夾選取此選項後， [!DNL Experience Manager] 自動執行培訓工作流程，以針對資料夾資產及其標籤培訓智慧內容服務。 根據預設，培訓工作流程每週於星期六凌晨12:30執行。

### 隨選培訓 {#on-demand-training}

您可以視需要從「工作流程」主控台訓練「智慧內容服務」。

1. 在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 從 **[!UICONTROL 工作流程模型]** 頁面，選取 **[!UICONTROL 智慧標籤培訓]** 工作流程，然後按一下 **[!UICONTROL 開始工作流程]** （從工具列）。
1. 在 **[!UICONTROL 執行工作流程]** 對話方塊中，瀏覽至包含標籤資產的裝載資料夾，以培訓服務。
1. 指定工作流程的標題並新增註解。 然後，按一下 **[!UICONTROL 執行]**. 資產和標籤會提交以進行訓練。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>在處理資料夾中的資產以進行訓練後，後續訓練週期中只會處理修改的資產。

### 檢視訓練報告 {#viewing-training-reports}

若要檢查智慧型內容服務是否已針對您資產培訓集中的標籤進行培訓，請從「報表」控制檯檢閱培訓工作流程報表。

1. 在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.
1. 在 **[!UICONTROL 資產報表]** 頁面，按一下 **[!UICONTROL 建立]**.
1. 選取 **[!UICONTROL 智慧標籤培訓]** 報表，然後按一下 **[!UICONTROL 下一個]** （從工具列）。
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。然後，按一下 **[!UICONTROL 建立]** （從工具列）。
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。若要檢視報表，請按一下 **[!UICONTROL 檢視]** （從工具列）。
1. 檢閱報告的詳細資訊。

   报表显示您培训的标记的培训状态。**[!UICONTROL 培训状态]**&#x200B;列中的绿色表示已为标记培训“智能内容服务”。黄色表示服务未针对特定标记进行完整培训。在这种情况下，使用特定标记添加更多图像并运行培训工作流以在标签上完整地培训服务。

   如果您在此報告中看不到您的標籤，請再次執行這些標籤的培訓工作流程。

1. 若要下載報表，請從清單中選取報表，然後按一下 **[!UICONTROL 下載]** （從工具列）。 報表會下載為Microsoft Excel試算表。

## 限制 {#limitations}

* 增強型智慧標籤是以學習的影像模型及其標籤為基礎。 這些模型並不總是能夠完美地識別標籤。 目前版本的Smart Content Service有下列限制：

   * 無法辨認影像中的細微差異。 例如，超薄襯衣與一般適合的襯衫。
   * 無法根據影像的微小模式/部分識別標籤。 例如，T恤上的標誌。
   * 在以下地區設定中支援標籤： [!DNL Experience Manager] 支援。

* 若要搜尋具有智慧標籤（一般或增強功能）的資產，請使用 [!DNL Assets] Omnisearch （全文檢索搜尋）。 智慧標籤沒有獨立的搜尋述詞。

>[!MORELIKETHIS]
>
>* [智慧標籤的概觀及訓練方式](enhanced-smart-tags.md)
>* [有關智慧標籤的教學影片](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

