---
title: 適用於AEM Forms的AEM Forms修補程式安裝指示
description: OSGi和JEE環境的AEM Forms service pack安裝指示
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 01bf12ec46966ab2c78e2e825840230ea1bd3395
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 9%

---

# AEM 6.5 Forms Service Pack安裝指示 {#aem-form-patch-installation-instructions}

## 发行版信息

| 产品 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 版本 | 6.5.16.0 |
| 类型 | Service Pack發行 |
| 日期 | 2023年3月2日 |
| 下载 URL | [最新AEM Forms版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>檢視最新的 [AEM Service Pack發行說明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html) 以取得已修正問題的完整清單。

## Experience Manager Forms 6.5包含的內容

Adobe Experience Manager (AEM) Forms service pack包含新功能和升級功能，例如客戶要求的重要增強功能、效能、穩定性和安全性改善。 AEM Forms會定期發行Service Pack，以提供最新功能和改善專案。 根據您的棧疊，選擇下列其中一個路徑，以下載並在您的環境中安裝Service Pack：

* [在JEE環境的AEM表單上下載並安裝Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi環境的AEM表單上下載並安裝Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe會每隔6個Service Pack發行完整安裝程式。 JEE上的AEM 6.5 Forms Service Pack 12 (6.5.12.0)是最後一個完整安裝程式。 完整版安裝程式支援新平台，而一般Service Pack安裝程式則包含新功能、錯誤修正和一般改善。 如果您正在執行全新安裝或計畫針對JEE環境的AEM 6.5 Forms使用最新軟體，Adobe建議使用2022年3月3日發行的JEE版AEM 6.5.12.0 Forms完整安裝程式，而非2019年4月8日發行的AEM 6.5 Forms安裝程式。 使用完整安裝程式後，請安裝最新的Service Pack。

## 在JEE環境的AEM表單上下載並安裝Service Pack {#download-and-install-for-jee-service-pack}

![JEE安裝](/help/forms/using/assets/jeeinstallation.png)

+++1. 備份您的現有環境：

1. 備份您的 [CRX儲存庫、資料庫結構描述和GDS （全域檔案儲存）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. 備份&lt;*AEM_forms_root*>/deploy資料夾。

>[!NOTE]
>
> 在執行AEM Service Pack安裝程式之前，請確定您擁有AEM安裝目錄的寫入存取許可權。

+++

+++2.下載必要的軟體：

* [JEE Service Pack上的AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM 服务包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [片段Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. 在JEE Service Pack上安裝AEM Forms：

1. 停止应用程序服务器。
1. 擷取 **JEE Service Pack安裝程式封存上的AEM Forms** 至您的硬碟：

   * **Windows**
導覽至安裝媒體上的適當目錄，或硬碟上您複製安裝程式的資料夾，然後按兩下 
`aemforms65_cfp_install.exe` 檔案。

      * （Windows 32位元） `Windows\Disk1\InstData\VM`
      * （Windows 64位元） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
導覽至適當的目錄，並從殼層和型別 
`./aem65_cfp_install.bin`。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   这会启动安装向导，引导您完成安装。

1. 在“Introduction”面板上，单击 **[!UICONTROL Next]**。
1. 於 **選擇安裝資料夾** 畫面，確認顯示的預設位置對於您的現有安裝而言是正確的，或按一下 **[!UICONTROL 瀏覽]** 以選取安裝AEM表單的替代資料夾，然後按一下 **[!UICONTROL 下一個]**.
1. 閱讀Service Pack摘要資訊，然後按一下 **[!UICONTROL 下一個]**.
1. 阅读“Pre-Installation Summary”信息，然后单击 **[!UICONTROL Install]**。
1. 安装完成后，单击 **[!UICONTROL Next]** 以将快速修补程序更新应用到已安装的文件。
1. **[僅適用於Windows]：** 執行下列步驟之一：

   * 取消選取 **啟動Configuration Manager** 選項，然後再按一下 **[!UICONTROL 完成]**. 執行 **設定管理員** 藉由使用 **ConfigurationManager.bat** 檔案位於 `[aem-forms root]\configurationManager\bin`.

   * 或取消選取 **啟動Configuration Manager** 選項，然後再按一下 **[!UICONTROL 完成]**. 執行前 **設定管理員** 使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，導覽至 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目錄和取代 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 檔案。

      >[!NOTE]
      >
      >* 更新或取代 **ConfigurationManager.bat** 檔案可協助您避免手動更新.lax檔案。


1. **[僅適用於Unix]：** 此 **啟動Configuration Manager** 預設會選取核取方塊。 按一下 **[!UICONTROL 完成]** 立即執行組態管理員或執行 **設定管理員** 稍後，取消選取 **啟動Configuration Manager** 選項，然後再按一下 **[!UICONTROL 完成]**. 您可以開始 **設定管理員** 稍後在中使用適當的指令碼 `[AEM_forms_root]/configurationManager/bin` 目錄。

1. 根據您的應用程式伺服器，選擇下列其中一份檔案，然後依照 *設定和部署AEM表單* 區段。

   * [安裝和部署AEM forms for JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安裝和部署AEM forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [安裝和部署AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [安裝和部署AEM forms for JBoss®叢集](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [安裝和部署AEM Forms for WebSphere®叢集](https://helpx.adobe.com/content/dam/help/cn/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [安裝和部署適用於WebLogic叢集的AEM Forms](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> 在JEE Service Pack上安裝AEM Forms後，您需要從移除Forms附加元件套件 `crx-repository\install` 資料夾，然後再重新啟動appserver。 從下載最新的Forms附加元件套件 [軟體發佈入口網站](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. 安裝servlet片段

>[!NOTE]
>
> * 如果是，您正在從 **AEM Service Pack 6.5.15.0**，則不需要安裝 **servlet片段**. 如果您要升級所使用的版本早於 **AEM Service Pack 6.5.15.0**，您必須安裝 **servlet片段**.
> * 您必須安裝 **servlet片段** 適用於所有應用程式伺服器，但不包括在 **JBoss® EAP 7.4.0**.



若要下載並安裝servlet片段：

1. 如果您尚未下載片段，請從下載 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. 啟動應用程式伺服器，等待記錄檔穩定並檢查套件組合狀態。

1. 開啟Web控制檯組合。 預設URL為 `http://[Server]:[Port]/system/console/bundles`.

1. 按一下「安裝/更新」。 選擇下載的片段， `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. 按一下 **安裝** 或 **更新**. 等待應用程式伺服器穩定下來

1. 停止應用程式伺服器。

+++

+++5. 安装 AEM Service Pack

1. 如果執行個體處於更新模式（執行個體是從舊版更新時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。
1. 安裝之前，請先拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。
1. 下載Service Pack，從 [Software Distribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).
1. 選取套件，然後選取 **[!UICONTROL 安裝]**.

**自动安装**

您可以使用兩種方法自動安裝 [!DNL ExperienceManager] service pack。<!--       UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。
套件會自動安裝。

* 使用 [套件管理器的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 使用  `cmd=install&recursive=true` 以便安裝巢狀套件。

   >[!NOTE]
   Experience ManagerService Pack不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

   **驗證安裝**

   若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

   1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (spversion)` 在 [!UICONTROL 已安裝產品].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. 所有OSGi套件組合都可以 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。
   1. OSGi套件 `org.apache.jackrabbit.oak-core` 為1.22.14版或更新版本(使用WebConsole： `/system/console/     bundles`)。

+++

+++6. 安裝AEM Experience Manager Forms附加元件套件

1. 確定您已安裝 [!DNL Experience Manager] service pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 依照中的說明安裝Forms附加元件套件 [安裝AEM Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 如果您在Experience Manager6.5 Forms中使用字母，請安裝 [最新的AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 在OSGi環境的AEM表單上下載並安裝Service Pack {#download-and-install-for-osgi-service-pack}

![OSGi安裝步驟](/help/forms/using/assets/osgiinstallation.png)


+++1. 備份您的現有環境：

1. 備份您的 [CRX儲存庫和資料庫結構](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
如果您安裝關聯式資料庫的AEM Forms Service Pack，則必須備份DB_schema。

+++

+++2.下載必要的軟體：

* [AEM 服务包](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. 安装 AEM Service Pack

1. 如果執行個體處於更新模式（執行個體是從舊版更新時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。
1. 安裝之前，請先拍攝快照或進行全新備份 [!DNL Experience Manager] 執行個體。
1. 下載Service Pack，從 [Software Distribution](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟封裝管理員，然後選取 **[!UICONTROL 上傳套裝]** 以上傳套件。 若要瞭解更多，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).
1. 選取套件，然後選取 **[!UICONTROL 安裝]**.

**自动安装**

您可以使用兩種方法自動安裝 [!DNL Experience Manager] service pack。<!--  UPDATE FOR EACH NEW RELEASE -->

* 將套件置於 `../crx-quickstart/install` 資料夾（當伺服器線上上可用時）。 套件會自動安裝。
* 使用 [套件管理器的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 使用 `cmd=install&recursive=true` 以便安裝巢狀套件。

   >[!NOTE]
   Experience ManagerService Pack不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

   **驗證安裝**

   若要瞭解經過認證可搭配此版本使用的平台，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

   1. 產品資訊頁(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (spversion)` 在 [!UICONTROL 已安裝產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. 所有OSGi套件組合都可以 **[!UICONTROL 作用中]** 或 **[!UICONTROL 片段]** 在OSGi主控台中(使用Web主控台： `/system/console/bundles`)。

      1. OSGi套件 `org.apache.jackrabbit.oak-core` 是1.22.14版或更新版本(使用Web主控台： `/system/console/bundles`)。

+++

+++4. 安裝AEM Experience Manager Forms附加元件套件

1. 確定您已安裝 [!DNL Experience Manager] service pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 依照中的說明安裝Forms附加元件套件 [安裝AEM Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. 如果您在Experience Manager6.5 Forms中使用字母，請安裝 [最新的AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 疑难解答

* 若 **套件管理員UI上的對話方塊** 會在安裝Service Pack期間退出，請等待錯誤記錄穩定下來後再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常會發生在Safari瀏覽器中，但也可能間歇性地發生在任何瀏覽器上。

* 安裝完成後，請檢查監視記錄(error.log)是否有任何活動。 等候幾分鐘，直到記錄中沒有活動。 重新啟動AEM執行個體。

* 萬一您收到 **服務無法使用的錯誤** 安裝AEM Forms 6.5.15.0 Service Pack後， [安裝servlet片段和套裝](/help/forms/using/aem-service-pack-installation-solution.md) 以修正錯誤。
