---
title: 安裝及設定資料擷取功能
seo-title: Install and configure data capture capabilities
description: 安裝並設定最適化表單、PDF forms和HTML5 Forms。 設定最適化表單的Adobe Analytics和Adobe Target ，以分析表單的使用情況，並根據使用者的設定檔鎖定使用者。
seo-description: Install and configure adaptive forms, PDF Forms, and HTML5 Forms. Configure Adobe Analytics and Adobe Target for adaptive forms to analyze usage of forms and target users based on their profile.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Admin
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 9%

---

# 安裝及設定資料擷取功能{#install-and-configure-data-capture-capabilities}

## 简介 {#introduction}

AEM Forms提供一組表單，用於從一般使用者取得資料：最適化表單、HTML5 Forms和PDF forms。 它還提供工具，用於列出網頁上的所有可用表單、分析表單的使用情況，以及根據使用者的個人資料鎖定使用者。 這些功能包含在AEM Forms附加元件套件中。 附加元件套件部署在AEM的Author或Publish執行個體上。

**調適型表單：** 這些表單會根據裝置的熒幕大小變更外觀、吸引人且互動性質。 最適化Forms也可以整合Adobe Analytics、Adobe Sign和Adobe Target。 它讓您能夠根據使用者的人口統計和其他功能，為其提供個人化的表單和以流程為導向的體驗。 您也可以將最適化表單與Adobe Sign整合。

**PDF forms** 適用於畫素完美列印，以及PDF檔案中的數位資訊擷取。 在數位頭像中，您可以使用Adobe Acrobat或Acrobat Reader來填寫這些表單。 您可以在網站上託管這些表單，或使用表單入口網站在AEM網站上列出這些表單。 您也可以將這些表單以電子郵件的形式傳送給其他人，作為附件。 這些表單最適合案頭環境。

**HTML5 FORMS** 是瀏覽器易用的PDF forms版本。 HTML5 Forms適用於不支援PDF外掛程式的環境。 HTML5 Forms可在不支援XFAPDF的行動裝置和案頭瀏覽器上，轉譯XFA型表單。 這些表格最適合平板電腦和桌上型電腦環境。

AEM Forms是功能強大的企業級平台，而資料擷取(調適型表單、PDF forms和HTML5 Forms)只是AEM Forms功能之一。 如需完整的功能清單，請參閱 [AEM Forms簡介](/help/forms/using/introduction-aem-forms.md).

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您只需要至少一個AEM作者和AEM發佈執行個體，即可執行AEM Forms資料擷取功能。 建議使用下列拓撲來執行AEM Forms AEM Forms資料擷取功能。 如需拓撲的詳細資訊，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

## 系统要求 {#system-requirements}

開始安裝及設定AEM Forms的資料擷取功能之前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且正在執行。 若是Windows使用者，請在提升許可權的模式下安裝AEM執行個體。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 您至少需要兩個 [AEM例項（一個作者和一個發佈）](/help/sites-deploying/deploy.md) 若要執行AEM Forms資料擷取功能：

   * **作者**：AEM執行個體，用來建立、上傳和編輯內容以及管理網站。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **發佈**：透過網際網路或內部網路，向公眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的暫存空間，適用於Microsoft Windows安裝。
   * UNIX安裝需要6 GB的暫存空間。

* 已設定作者和發佈執行個體的復寫和反向復寫。 如需詳細資訊，請參閱 [復寫](/help/sites-deploying/replication.md).
* 對於基於UNIX的系統：

   * 從安裝媒體安裝下列32位元套件：

<table>
 <tbody>
  <tr>
   <td>外傳</td>
   <td>fontconfig</td>
   <td>自由文字</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>利比庫</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 如果伺服器上已安裝OpenSSL，請將其升級至最新版本。
>* 分別建立指向最新版libcurl、libcrypto和libssl程式庫的libcurl.so、libcrypto.so和libssl.so symlink。
>


* 從安裝媒體安裝下列64位元套件：

   * 利比庫

* 安裝 [Microsoft Visual Studio 2019 32位元可轉散發套件](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).


## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms資料擷取和其他功能。 執行以下步驟來安裝附加元件套件：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

   您也可以透過下列連結下載套件： [AEM Forms發行版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。
1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 檔案和記錄穩定。
1. 對所有Author和Publish執行個體重複步驟1至7。

### （僅限Windows）自動安裝Visual Studio可轉散發套件 {#automatic-installation-visual-studio-redistributables}

如果您以提升許可權模式安裝AEM執行個體，則在安裝AEM Forms附加元件套件期間，會自動安裝32位元Visual Studio可轉散發套件。

若要評估是否已自動安裝Visual Studio可轉散發套件，請開啟 `error.log` 檔案位於 `/crx-repository/logs/` 目錄。 記錄檔包含下列訊息：

`Redist <service name> already installed on system, will not attempt re-installation`

如果無法安裝可轉散發套件，記錄會包含下列訊息：

`Current user does not have elevated privileges, aborting installation of redist <service name>`

若要解決此問題，請重新啟動AEM伺服器，以提升許可權模式安裝AEM，然後安裝AEM Forms附加元件套件。

如果許可權檢查失敗，記錄會包含以下訊息：

`Privilege escalation check failed with error: <error message>`

## 安裝後設定 {#post-installation-configurations}

AEM Forms有一些必要和選用的設定。 強制設定包括設定BouncyCastle程式庫和序列化代理程式。 選擇性設定包括設定Dispatcher、Forms入口網站、Adobe Sign、Adobe Analytics和Adobe Target。

### 強制安裝後設定 {#mandatory-post-installation-configurations}

#### 設定RSA和BouncyCastle資料庫  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish執行個體上執行下列步驟，以啟動委派程式庫：

1. 停止基礎AEM執行個體。
1. 開啟 `[AEM installation directory]\crx-quickstart\conf\sling.properties` 檔案進行編輯。

   如果您使用 `[AEM installation directory]\crx-quickstart\bin\start.bat` 若要啟動AEM，然後編輯位於以下位置的sling.properties `[AEM_root]\crx-quickstart\`.

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 儲存並關閉檔案，然後啟動AEM執行個體。
1. 在所有Author和Publish執行個體上重複步驟1-4。

#### 設定序列化代理程式 {#configure-the-serialization-agent}

對所有Author和Publish執行個體執行下列步驟，將套件新增至允許清單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為 `https://'[server]:[port]'/system/console/configMgr`.
1. 搜尋 **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** 並開啟設定。
1. 新增 **sun.util.calendar** 封裝到 **允許清單** 欄位。 单击“**保存**”。
1. 在所有Author和Publish執行個體上重複步驟1-3。

### 選用的安裝後設定 {#optional-post-installation-configurations}

#### 配置 Dispatcher {#configure-dispatcher}

Dispatcher 是 Adobe Experience Manager 的缓存和/或负载平衡工具，可与企业级 Web 服务器结合使用。如果您使用 [Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，然後針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需篩選器的詳細資訊，請參閱 [Dispatcher檔案](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix Configuration Manager。 設定管理員的預設URL為 `https://[server]:[port_number]/system/console/configMgr`. 在 **設定** 功能表，選取 **Apache Sling查閱者篩選器** 選項。 在允許主機欄位中，輸入Dispatcher的主機名稱，以允許其作為反向連結，然後按一下 **儲存**. 專案的格式為 `https://[server]:[port]`.

#### 設定快取 {#configure-cache}

快取是一種可縮短資料存取時間、減少延遲及改善輸入/輸出(I/O)速度的機制。 調適型表單快取只會儲存調適型表單的HTML內容和JSON結構，不會儲存任何預先填入的資料。 這有助於減少轉譯最適化表單所需的時間。

* 在使用最適化表單快取時，請使用 [AEM傳送器](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) 快取最適化表單的使用者端資料庫（CSS和JavaScript）。
* 開發自訂元件時，請停用用於開發的伺服器上的最適化表單快取。

執行以下步驟來設定最適化表單快取：

1. 前往AEM Web主控台設定管理員，網址為https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr.
1. 按一下 **最適化表單和互動式通訊Web頻道設定** 以編輯其組態值。 在編輯設定值對話方塊中，指定AEM Forms伺服器執行個體可快取的表單或檔案數目上限。 **最適化Forms數量** 欄位。 默认值为 100。单击“**保存**”。

   >[!NOTE]
   >
   >若要停用快取，請將「最適化Forms數目」欄位中的值設為 **0**. 當您停用或變更快取設定時，快取會重設，所有表單和檔案都會從快取中移除。

#### 設定表單資料模型的SSL通訊 {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要為表單資料模型啟用SSL通訊，請在啟動任何AEM Forms執行個體之前，為所有執行個體的Java信任存放區新增憑證。 您可以執行以下命令來新增憑證： 」

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可啟用最適化表單的電子簽章工作流程。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在一般Adobe Sign和調適型表單案例中，使用者需填寫調適型表單以 **申請服務**. 例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服務提供者會檢閱應用程式，並使用Adobe Sign將應用程式標示為已核准。 若要啟用類似的電子簽章工作流程，您可以將Adobe Sign與AEM Forms整合。

若要搭配AEM Forms使用Adobe Sign， [將Adobe Sign與AEM Forms整合](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### 設定Adobe Analytics {#configure-adobe-analytics}

AEM Forms與Adobe Analytics整合，可讓您擷取及追蹤已發佈表單和檔案的績效量度。 分析这些指标的目的在于，根据有关使表单或文档更有用所需的更改的数据做出明智的决策。

若要搭配AEM Forms使用Adobe Analytics，請參閱 [設定分析和報表](/help/forms/using/configure-analytics-forms-documents.md).

#### 整合Adobe Target {#integrate-adobe-target}

如果表單提供的體驗不吸引人，您的客戶可能會捨棄表單。 雖然讓客戶感到沮喪，但也可以提高貴組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉換率既關鍵又具有挑戰性。 AEM forms保有此問題的關鍵。

AEM forms與Adobe Target (一種Adobe Marketing Cloud解決方案)整合，跨多個數位頻道提供個人化且吸引人的客戶體驗。 若要使用Adobe Target來測試A/B調適型表單， [將Adobe Target與AEM Forms整合](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## 后续步骤 {#next-steps}

您已將環境設定為使用AEM Forms資料擷取功能。 現在，使用功能的後續步驟為：

* [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md)
* [建立您的第一個PDF表單](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 Forms簡介](/help/forms/using/introduction.md)
