---
title: 安裝及設定互動式通訊
seo-title: Install and configure Interactive Communications
description: 安裝並設定AEM Forms互動式通訊，以建立商務對應、檔案、對帳單、權益通知、行銷郵件、帳單和歡迎套件。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 7%

---

# 安裝及設定互動式通訊{#install-and-configure-interactive-communications}

## 简介 {#introduction}

AEM Form可集中建立、組裝、管理及傳送安全且互動式的檔案，例如商業信函、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。 此功能稱為互動式通訊。 此功能包含在AEM Forms附加元件套件中。 附加元件套件部署在AEM的Author或Publish執行個體上。

您可以使用互動式通訊功能，以多種格式產生通訊。 例如，網頁和PDF。 您可以將互動式通訊與AEM Workflow整合，以便透過客戶選擇的管道處理及傳送已組裝的通訊給客戶。 例如，透過電子郵件傳送通訊給一般使用者。

如果您要從舊版升級，而且已投資通訊管理，您可以安裝 [相容性套件](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) 以繼續使用通訊管理。 如需互動式通訊與通訊管理之間差異的相關資訊，請參閱 [互動式通訊概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms是功能強大的企業級平台。 互動式通訊只是AEM Forms的其中一項功能。 如需完整的功能清單，請參閱 [AEM Forms簡介](../../forms/using/introduction-aem-forms.md).

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您至少只需要一個AEM製作和處理執行個體，即可執行互動式通訊功能。 下列拓撲可代表如何在OSGi功能上執行AEM Forms互動式通訊、通訊管理、AEM Forms資料擷取和以Forms為中心的工作流程。 如需拓撲的詳細資訊，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

AEM Forms互動式通訊會在AEM Forms的製作執行個體上執行管理、製作和代理程式使用者介面。 Publish執行個體會託管互動式通訊的最終版本，以供一般使用者使用。

## 系统要求 {#system-requirements}

開始安裝及設定AEM Forms的互動式通訊與通訊管理功能之前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且正在執行。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 您需要至少一個AEM執行個體（製作或處理）來執行AEM Forms互動式通訊和通訊管理功能：

   * **作者**：AEM執行個體，用來建立、上傳和編輯內容以及管理網站。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **處理中：** 處理執行個體是 [強化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 執行個體。 您可以設定Author例項，並在執行安裝後加以強化。

   * **發佈**：透過網際網路或內部網路，向公眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的暫存空間，適用於Microsoft® Windows安裝。
   * UNIX安裝需要6 GB的暫存空間。

* UNIX系統的額外需求：如果您使用的是UNIX作業系統，請從個別作業系統的安裝媒體安裝下列套件。

<table>
 <tbody>
  <tr>
   <td>外傳</td>
   <td>libxcb</td>
   <td>自由文字</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms互動式通訊、通訊管理和其他功能。 執行以下步驟來安裝附加元件套件：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

   您也可以透過下列連結下載套件： [AEM Forms發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans) 文章。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log檔案且記錄穩定。
1. 對所有Author和Publish執行個體重複步驟1至7。

## 安裝後設定 {#post-installation-configurations}

AEM Forms有一些必要和選用的設定。 強制設定包括設定BouncyCastle程式庫和序列化代理程式。 選擇性設定包括設定Dispatcher和Adobe Target。

### 強制安裝後設定 {#mandatory-post-installation-configurations}

#### 設定RSA和BouncyCastle資料庫  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish執行個體上執行下列步驟，以啟動委派程式庫：

1. 停止基礎AEM執行個體。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果您使用 [AEM安裝目錄]\crx-quickstart\bin\start.bat以啟動AEM，然後編輯sling.properties，網址為 [AEM_root]\crx-quickstart\。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 儲存並關閉檔案，然後啟動AEM執行個體。
1. 在所有Author和Publish執行個體上重複步驟1至4。

#### 設定序列化代理程式 {#configure-the-serialization-agent}

對所有Author和Publish執行個體執行下列步驟，將套件新增至允許清單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr.
1. 搜尋並開啟 **還原序列化防火牆設定**.
1. 新增 **sun.util.calendar** 封裝到 **允許清單** 欄位。 单击“保存”。
1. 在所有Author和Publish執行個體上重複步驟1至3。

### 選用的安裝後設定 {#optional-post-installation-configurations}

#### 安裝相容性套件 {#install-compatibility-package}

在AEM 6.5 Forms中，互動式通訊是建立客戶通訊的預設和建議方法。 如果您已從舊版升級或移轉，並計畫繼續使用信件（通訊管理），請安裝 [AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en).

AEMFD相容性套件可讓您在AEM 6.5 Forms上使用AEM 6.4 Forms、AEM 6.3 Forms和AEM 6.2 Forms的下列資產：

* 檔案片段
* 书信
* 資料字典
* 最適化表單已棄用的範本和頁面

#### 配置 Dispatcher {#configure-dispatcher}

Dispatcher 是 Adobe Experience Manager 与企业级 Web 服务器结合使用的缓存和负载平衡工具。如果您使用 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans)，然後針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需篩選器的詳細資訊，請參閱 [Dispatcher檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans).

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix Configuration Manager。 設定管理員的預設URL為https://&#39;server&#39;：[連線埠號碼]/system/console/configMgr。 在 **設定** 功能表，選取 **Apache Sling查閱者篩選器** 選項。 在允許主機欄位中，輸入Dispatcher的主機名稱，以允許其作為反向連結，然後按一下 **儲存**. 專案的格式為https://&#39;[伺服器]：[連線埠]&#39;.

#### 整合Adobe Target {#integrate-adobe-target}

如果互動式通訊提供的體驗不吸引人，您的客戶可能會捨棄互動式通訊。 雖然讓客戶感到沮喪，但也提高了貴組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉換率，這既重要又具有挑戰性。 AEM forms保有此問題的關鍵。

AEM forms與Adobe Target (一種Adobe Experience Cloud解決方案)整合，跨多個數位頻道提供個人化且吸引人的客戶體驗。 若要使用Adobe Target來個人化互動式通訊， [將Adobe Target與AEM Forms整合](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### 設定表單資料模型的SSL通訊  {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要為表單資料模型啟用SSL通訊，請在啟動任何AEM Forms執行個體之前，為所有執行個體的Java™信任存放區新增憑證。 您可以執行以下命令來新增憑證：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 后续步骤 {#next-steps}

您已將環境設定為使用互動式通訊和通訊管理功能。 現在，使用功能的步驟如下：

* [通訊管理概觀](/help/forms/using/interactive-communications-overview.md)

* [建立互動式通訊](../../forms/using/create-interactive-communication.md)

* [建立通訊管理信件](../../forms/using/create-letter.md)
