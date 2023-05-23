---
title: 在OSGi上升級至AEM 6.5 Forms
description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1直接升級至AEM 6.3 Forms。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 5%

---

# 在OSGi上升級至AEM 6.5 Forms {#upgrade-to-aem-forms-osgi}

您可以從AEM 6.3 Forms或AEM 6.4 Forms直接升級至AEM 6.5 Forms。

直接升級路徑： **AEM 6.0 Forms、AEM 6.1 Forms**、和 **AEM 6.2 Forms** 至AEM 6.5 Forms無法使用。 執行中繼 [升級至AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)， [升級至AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)，或 [升級至AEM 6.4 Forms](/help/forms/using/upgrade.md) 然後從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5 Forms。

若要從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5 Forms，請執行下列動作：

1. 將現有AEM執行個體升級至AEM 6.5。步驟如下：

   1. 安裝AEM 6.3 Forms或AEM 6.4 Forms的最新Service Pack和修補程式。 如需詳細資訊，請參閱 [AEM維護中心](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html).
   1. 準備來源執行個體以進行升級。 如需詳細步驟，請參閱 [升級至AEM 6.5](/help/sites-deploying/upgrade.md).
   1. 下載 [AEM 6.5快速入門](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **（僅適用於Unix/Linux安裝）** 如果您使用UNIX或Linux作為基礎作業系統，請開啟終端機視窗，瀏覽至包含crx-quickstart的資料夾，然後執行下列命令：

      `chmod -R 755 ../crx-quickstart`

   1. 將您的AEM執行個體升級至AEM 6.3。如需逐步指示，請參閱 [升級至AEM 6.5](/help/sites-deploying/upgrade.md).

      繼續後續步驟之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 &lt;crx-repository>/error.log檔案。

      >[!NOTE]
      >
      >伺服器啟動並執行後，一些AEM Forms套件組合會維持安裝狀態。 每個安裝的套件組合數量可能有所不同。 您可以安全地忽略這些套裝的狀態。 套件組合列於https://&#39;[伺服器]：[連線埠]&#39;/system/console/。

1. 安裝AEM Forms附加元件套件。 步驟如下：

   1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
   1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
   1. 在 **[!UICONTROL 篩選器]** 區段：
      1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
      1. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
   1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
   1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
   1. 選取套件並按一下 **[!UICONTROL 安裝]**.

      您也可以使用下列直接連結下載套件： [AEM Forms發行版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。

      >[!NOTE]
      >
      >安裝套件後，系統會提示您重新啟動AEM執行個體。 **請勿立即停止伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 &lt;crx-repository>/error.log檔案且記錄穩定。 另請注意，有些套件可能維持已安裝狀態。 您可以安全地忽略這些套件的狀態。

1. 重新啟動AEM執行個體。

1. 執行安裝後活動。

   * **執行移轉公用程式**

      移轉公用程式可讓適用性表單和舊版通訊管理資產相容於AEM 6.5表單。 您可以從AEM Software Distribution下載公用程式。 如需設定和使用移轉公用程式的逐步資訊，請參閱 [移轉公用程式](../../forms/using/migration-utility.md).

      如果您使用 [整合草稿和提交元件的範例](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) 使用資料庫並從舊版升級，然後在執行升級後執行下列SQL查詢：

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(如果從AEM 6.2 Forms或舊版升級)重新設定Adobe Sign**

      如果您已在舊版AEM Forms中設定Adobe Sign，請從AEM雲端服務重新設定Adobe Sign 。 如需詳細資訊，請參閱 [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **支援jQuery**

      在AEM 6.5 Forms中，jQuery的版本更新至3.2.1，而jQuery UI版本更新至1.12.1。AEM Form使用JQuery於 **noConflict** 模式。 因此，如果您使用任何其他jQuery版本，執行升級時都不會顯示任何問題。 不過，當您升級至AEM 6.5 Forms時：

      * 確保您的自訂元件（如果有）與支援的jQuery版本相容。
      * 從自訂元件中移除不支援的API。 另請參閱 [升級指南](https://jquery.com/upgrade-guide/3.0/) 以取得已移除的API清單。 例如，對load()、.unload()和.error() API的支援已移除。 使用.on()方法取代上述API。 例如，將$(&quot;img&quot;)。load(fn)變更為$(&quot;img&quot;)。on(&quot;load&quot;， fn)。
   * **(如果從AEM 6.2 Forms或舊版升級)重新設定分析和報表**

      在AEM 6.4 Forms中，無法使用曝光的來源和成功事件流量變數。 因此，當您從AEM 6.2 Forms或舊版升級時，AEM Forms會停止傳送資料至Adobe Analytics伺服器，且無法使用最適化表單的Analytics報表。 此外，AEM 6.4 Forms還針對表單分析版本引入了流量變數，並針對在欄位上逗留的時間量引入了成功事件。 因此，請為您的AEM Forms環境重新設定分析和報表。 如需詳細步驟，請參閱 [設定分析和報表](../../forms/using/configure-analytics-forms-documents.md).


1. 確認伺服器升級成功，所有資料也成功移轉，而且伺服器可以正常運作。

   * **驗證套件組合的狀態：** 確定所有套件組合都處於作用中狀態。
   * **驗證復寫和反向復寫：** 發佈、填寫和提交一些已移轉的表單。 同時驗證提交的資料。
   * **驗證對管理員和開發人員使用者介面的存取權：** 從管理員帳戶登入AEM執行個體，並確認您擁有下列URL的存取權：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEM 6.4 Forms中，crx-repository的結構已變更。 如果從6.3 Forms升級至AEM 6.5 Forms，請使用變更的路徑進行自訂，讓您重新建立。 如需已變更路徑的完整清單，請參閱 [AEM中的Forms存放庫重組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
