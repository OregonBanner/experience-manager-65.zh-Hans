---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

---

# 安装 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | 本文 |

在中擁有管理員存取許可權的使用者 [!DNL Adobe Experience Manager] 安裝增強型聯結器。 安裝之前，請先檢閱平台支援及其他 [聯結器的先決條件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署和設定 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署與設定沒有認證合作夥伴或 [!DNL Adobe Professional Services]，Adobe不支援。
>
>* Adobe可能會將更新發行至 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 讓此聯結器成為備援；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請導覽至 `digital.hoodoo` 群組可在左側窗格中找到，位置為 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans).
>
>* 另請參閱 [適用於Experience Manager Assets增強型聯結器的Workfront合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 如需有關考試的資訊，請參閱 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


若要安裝聯結器，請遵循下列步驟：

1. 從下載聯結器 [[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [設定防火牆](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. 在Dispatcher上，允許名為的HTTP標頭 `authorization`， `username`、和 `apikey`. 允許 `GET`， `POST`、和 `PUT` 要求 `/bin/workfront-tools`.
1. 請確定以下路徑不存在於 [!DNL Experience Manager] 存放庫：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用安裝套件 [!UICONTROL 封裝管理員]. 若要瞭解如何安裝套件，請參閱 [封裝管理員檔案](/help/sites-administering/package-manager.md).
1. 建立 `wf-workfront-users` 在 [!DNL Experience Manager] 使用者群組並指派許可權 `jcr:all` 至 `/content/dam`.

系統使用者 `workfront-tools` 會自動建立，並自動管理所需的許可權。 所有使用者來自 [!DNL Workfront] 使用聯結器的使用者會自動新增為此群組的一部分。

## 設定之間的連線 [!DNL Experience Manager] 和 [!DNL Workfront] {#configure-connection}

若要建立與Workfront的連線，請遵循下列步驟：

1. 在 [!DNL Experience Manager]，選取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**.

1. 選取 `workfront-tools` 在左側面板中並選取 **[!UICONTROL 建立]** 選項。

1. 在 **[!UICONTROL Workfront連線]** 對話方塊，提供您所需的詳細資料 [!DNL Workfront] 部署，並選取 **[!UICONTROL 連線至Workfront]** 選項。 成功連線後， [!DNL Workfront] 檔案自訂整合會自動建立於 [!DNL Workfront] 環境。

   ![Connect [!DNL Experience Manager] 和 [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 若要驗證連線，請在中存取 [!DNL Workfront] 並驗證API金鑰是否相同，以及連線是否為 **[!UICONTROL 已啟用]**. 若要這麼做，請選取 **[!UICONTROL 設定]** > **[!UICONTROL 檔案]** > **[!UICONTROL 自訂整合]** 在 [!DNL Workfront].

## 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets可讓您更新 [!DNL Workfront for Experience Manager enhanced connector] 從舊版升級為最新版。

若要更新 [!DNL Workfront for Experience Manager enhanced connector] 至最新版本：

1. 從下載最新版本的增強型聯結器 [[!DNL Software Distribution] 連結](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. 使用安裝套件 [!UICONTROL 封裝管理員]. 若要瞭解如何安裝套件，請參閱 [封裝管理員檔案](/help/sites-administering/package-manager.md).
