---
title: 在OSGi上安裝及設定以Forms為中心的工作流程
seo-title: Installing and Configuring Forms-centric workflow on OSGi
description: 安裝並設定AEM Forms互動式通訊，以建立商務對應、檔案、對帳單、權益通知、行銷郵件、帳單和歡迎套件。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 6%

---

# 在OSGi上安裝及設定以Forms為中心的工作流程{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 简介 {#introduction}

企業會從多個表單、後端系統和其他資料來源收集及處理資料。 資料處理涉及複查與核准程式、重複工作與資料封存。 例如，檢閱表單並將其轉換為PDF檔案。 手動完成時，重複式作業會花費許多時間與資源。

您可以使用 [OSGi上以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md) 以快速建立最適化表單式工作流程。 這些工作流程可協助您自動執行複查與核准工作流程、業務流程工作流程及其他重複性的工作。 這些工作流程還有助於處理檔案(建立、彙編、分發和封存PDF檔案、新增數位簽名以限制對檔案的存取、解碼條碼表單等)，以及將Adobe Sign簽名工作流程用於表單和檔案。

設定後，這些工作流程可以手動觸發，以完成定義的流程，或在使用者提交表單或互動式通訊時以程式設計方式執行。 此功能包含在AEM Forms附加元件套件中。

AEM Forms是功能強大的企業級平台。 OSGi上以Forms為中心的工作流程只是AEM Forms功能之一。 如需完整的功能清單，請參閱 [AEM Forms簡介](introduction-aem-forms.md).

>[!NOTE]
>
>透過OSGi上的Forms工作流程，您可以快速在OSGi棧疊上建置和部署各種任務的工作流程，而不需要在JEE棧疊上安裝完整的流程管理功能。 參閱 [比較](capabilities-osgi-jee-workflows.md) OSGi上的Forms中心AEM工作流程和JEE上的流程管理，以瞭解功能的差異和相似性。
>
>比較後，如果您選擇在JEE棧疊上安裝「程式管理」功能，請參閱 [在JEE上安裝或升級AEM Forms](/help/forms/home.md) 以取得關於安裝和設定JEE棧疊及「程式管理」功能的詳細資訊。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您只需要至少一個AEM作者或處理執行個體（生產作者），就能在OSGi功能上執行Forms為中心的工作流程。 處理執行個體是 [強化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 執行個體。 請勿對生產作者執行任何實際製作，例如建立工作流程或調適型表單。

下列拓撲可代表如何在OSGi功能上執行AEM Forms互動式通訊、通訊管理、AEM Forms資料擷取和以Forms為中心的工作流程。 如需拓撲的詳細資訊，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

OSGi上的AEM Forms Forms中心工作流程會在AEM Forms的作者執行個體上執行AEM收件匣和AEM工作流程模型建立UI。

## 系统要求 {#system-requirements}

>[!NOTE]
>
>跳至 [後續步驟](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 部分(如果您已在OSGi上安裝AEM Forms)，請參閱 [安裝及設定資料擷取功能](../../forms/using/installing-configuring-aem-forms-osgi.md) 文章。

開始在OSGi上安裝及設定以Forms為中心的工作流程之前，請確保：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且正在執行。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 您至少需要一個AEM例項（製作或處理），才能在OSGi上執行Forms為中心的工作流程：

   * **作者**：AEM執行個體，用來建立、上傳和編輯內容以及管理網站。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **處理中：** 處理執行個體是 [強化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 執行個體。 您可以設定Author例項，並在執行安裝後加以強化。

   * **發佈**：透過網際網路或內部網路，向公眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的暫存空間，適用於Microsoft Windows安裝。
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

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含有關OSGi和其他功能的Forms中心工作流程。 執行以下步驟來安裝附加元件套件：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 點選適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 打开[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 選取套件並按一下 **[!UICONTROL 安裝]**.

   您也可以透過下列連結下載套件： [AEM Forms發行版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log檔案且記錄穩定。
1. 對所有Author和Publish執行個體重複步驟1至7。

## 安裝後設定 {#post-installation-configurations}

AEM Forms有一些必要和選用的設定。 強制設定包括設定BouncyCastle程式庫和序列化代理程式。 選擇性設定包括設定Dispatcher和Adobe Target。

### 強制安裝後設定 {#mandatory-post-installation-configurations}

#### 設定RSA和BouncyCastle資料庫  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish執行個體上執行下列步驟，以啟動委派程式庫：

1. 停止基礎AEM執行個體。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果您使用 [AEM安裝目錄]\crx-quickstart\bin\start.bat以啟動AEM，然後編輯位於的sling.properties [AEM_root]\crx-quickstart\。

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

#### 配置 Dispatcher {#configure-dispatcher}

Dispatcher是適用於AEM的快取和負載平衡工具。 AEM Dispatcher也有助於保護AEM伺服器不受攻擊。 您可以搭配使用Dispatcher與企業級Web伺服器，以提高AEM執行個體安全性。 如果您使用 [Dispatcher](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，然後針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需篩選器的詳細資訊，請參閱 [Dispatcher檔案](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix Configuration Manager。 設定管理員的預設URL為https://&#39;server&#39;：[連線埠號碼]/system/console/configMgr。 在 **設定** 功能表，選取 **Apache Sling查閱者篩選器** 選項。 在允許主機欄位中，輸入Dispatcher的主機名稱，以允許其作為反向連結，然後按一下 **儲存**. 專案的格式為 `https://'[server]:[port]'`.

#### 設定快取 {#configure-cache}

快取是一種可縮短資料存取時間、減少延遲及改善輸入/輸出(I/O)速度的機制。 調適型表單快取只會儲存調適型表單的HTML內容和JSON結構，不會儲存任何預先填入的資料。 這有助於減少轉譯最適化表單所需的時間。

* 在使用最適化表單快取時，請使用 [AEM傳送器](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html) 快取最適化表單的使用者端資料庫（CSS和JavaScript）。
* 開發自訂元件時，請停用用於開發的伺服器上的最適化表單快取。

執行以下步驟來設定最適化表單快取：

1. 前往AEM Web主控台組態管理員，位於 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 以編輯其組態值。 在編輯設定值對話方塊中，指定AEM Forms伺服器執行個體可快取的表單或檔案數目上限。 **最適化Forms數量** 欄位。 默认值为 100。单击“**保存**”。

   >[!NOTE]
   >
   >若要停用快取，請將「最適化Forms數目」欄位中的值設為 **0**. 當您停用或變更快取設定時，快取會重設，所有表單和檔案都會從快取中移除。

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可啟用最適化表單的電子簽章工作流程。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在OSGi上的典型Adobe Sign和Forms工作流程中，使用者會填寫最適化表單以 **申請服務**. 例如，信用卡申请表和公民权益表。當使用者填寫、提交和簽署申請表單時，核准/拒絕工作流程就會開始。 服務提供者會稽核AEM收件匣中的應用程式，並使用Adobe Sign以電子方式簽署應用程式。 若要啟用類似的電子簽章工作流程，您可以將Adobe Sign與AEM Forms整合。

若要搭配AEM Forms使用Adobe Sign， [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## 后续步骤 {#next-steps}

您已將環境設定為在OSGi功能上使用以Forms為中心的工作流程。 現在，使用功能的步驟如下：

* [在OSGi上使用以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [字母和互動式通訊的後處理](../../forms/using/submit-letter-topostprocess.md)
