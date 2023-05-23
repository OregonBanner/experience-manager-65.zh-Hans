---
title: 正在設定AEM DS設定
seo-title: Configuring AEM DS settings
description: 提交表單前，您必須指定處理伺服器URL。
seo-description: You need to specify the processing server URL before you submit a form.
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Admin
exl-id: c43cab7b-3421-4e1b-a834-b2dd6eb23c1d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 正在設定AEM DS設定{#configuring-aem-ds-settings}

本文會說明如何設定 **AEM DS設定服務**. 此設定可用於多個情境，例如：

* 在通訊管理中

   * 設定AEM Forms工作流程
   * 使用表單入口網站從遠端儲存草稿/提交內容時

* 在最適化表單中，適用於從發佈執行個體提交最適化表單的情況

以下是設定 **[!UICONTROL AEM DS設定]**：

1. 使用URL在發佈執行個體上開啟Configuration Manager：\
   *https://localhost:port/system/console/configMgr*.

   ![AEM Web主控台設定](assets/web_configuration_console_new.png)

1. 在 **[!UICONTROL Adobe Experience Manager Web主控台設定]** 視窗，找到並按一下 **[!UICONTROL AEM DS設定]** 選項。

   ![DS設定](assets/ds_settings_new.png)

1. 此 **[!UICONTROL AEM DS設定服務]** 視窗會顯示AEM DS元件的常見組態設定。

   ![DS設定服務](assets/ds_settings_service_new.png)

1. 在個別欄位中新增下列資訊：

   **[!UICONTROL 處理伺服器URL]**：處理伺服器是需要觸發Forms或AEM工作流程的伺服器。 這可以與AEM編寫執行個體的URL或其他伺服器URL (即https://localhost:port/)相同。

   **[!UICONTROL 處理伺服器使用者名稱]**：工作流程使用者的使用者名稱 [根據所使用的伺服器URL]

   **[!UICONTROL 處理伺服器密碼]**：工作流程使用者密碼

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 使用Forms或AEM工作流程時，從發佈伺服器提交任何內容之前，必須先設定DS設定服務。 否則，表單提交將會失敗。

