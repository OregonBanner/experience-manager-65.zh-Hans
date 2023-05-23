---
title: 在OSGi環境中強化及保護AEM表單
seo-title: Hardening and Securing AEM forms on OSGi environment
description: 瞭解在OSGi伺服器上保護AEM Forms安全的建議和最佳實務。
seo-description: Learn recommendations and best practices for securing AEM Forms on OSGi server.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---

# 在OSGi環境中強化及保護AEM表單 {#hardening-and-securing-aem-forms-on-osgi-environment}

瞭解在OSGi伺服器上保護AEM Forms安全的建議和最佳實務。

保護伺服器環境對於組織而言至關重要。 本文介紹保護執行AEM Forms之伺服器的建議與最佳實務。 這不是適用於您作業系統的完整主機強化檔案。 相反，本文會說明您應實作的各種安全性強化設定，以增強已部署應用程式的安全性。 不過，為了確保應用程式伺服器的安全，除了本文提供的建議外，您也應實作安全性監控、偵測和回應程式。 本檔案也包含保護PII （個人識別資訊）安全的最佳實務和准則。

本文內容適用於負責規劃AEM Forms應用程式或基礎架構開發及部署的顧問、安全專家、系統架構師和IT專業人員。 這些角色包括下列常見角色：

* IT與營運工程師必須在自己或客戶組織中部署安全的Web應用程式與伺服器。
* 負責規劃組織中客戶架構工作的架構師和規劃師。
* IT安全性專家，專注於提供組織內各平台的安全性。
* 需要客戶和合作夥伴詳細資源的Adobe和合作夥伴顧問。

下圖顯示典型AEM Forms部署中使用的元件和通訊協定，包括適當的防火牆拓撲：

![典型架構](assets/typical-architecture.png)

AEM Forms可高度自訂，可在許多不同的環境中運作。 部分建議可能不適用於您的組織。

## 安全傳輸層 {#secure-transport-layer}

傳輸層安全性弱點是對任何面對網際網路或面對內部網路的應用程式伺服器的首要威脅之一。 本節說明針對這些弱點強化網路上主機的程式。 它處理網路細分、傳輸控制通訊協定/網際網路通訊協定(TCP/IP)棧疊強化，以及使用防火牆保護主機等問題。

### 限制開放端點  {#limit-open-endpoints}

組織可以有外部防火牆，以限制一般使用者與AEM Forms發佈伺服器陣列之間的存取權。 組織也可以有內部防火牆，以限制發佈伺服器陣列和組織元素內的其他專案（例如製作執行個體、處理執行個體、資料庫）之間的存取權。 允許防火牆為一般使用者和組織元素內部啟用對有限數量的AEM Forms URL的存取：

#### 設定外部防火牆  {#configure-external-firewall}

您可以設定外部防火牆，允許特定AEM Forms URL存取網際網路。 填寫或提交最適化表單、HTML5、通訊管理信函或登入AEM Forms伺服器時，需要存取這些URL：

<table> 
 <tbody>
  <tr>
   <td>组件</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>自适应表单</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr：content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5表單</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通訊管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms Portal </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> AEM Forms 应用程序</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### 設定內部防火牆  {#configure-internal-firewall}

您可以將內部防火牆設定為允許某些AEM Forms元件（例如製作執行個體、處理執行個體、資料庫）與發佈伺服器陣列和拓撲圖中所提及的其他內部元件通訊：

<table> 
 <tbody>
  <tr>
   <td>主机<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>發佈陣列（發佈節點）</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>處理伺服器</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow附加元件伺服器(JEE伺服器上的AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 設定存放庫許可權和存取控制清單(ACL) {#setup-repository-permissions-and-access-control-lists-acls}

依預設，發佈節點上可用的資產可供所有人存取。 已針對所有資產啟用唯讀存取。 必須啟用匿名存取。 如果您打算限制表單檢視，並只向已驗證的使用者提交存取權，則使用通用群組來允許僅已驗證的使用者對發佈節點上可用的資產具有唯讀存取權。 下列位置/目錄包含需要強化的forms資產（已驗證身分的使用者僅能唯讀存取）：

* /content/&amp;ast；
* /etc.clientlibs/fd/&amp;ast；
* /libs/fd/&amp;ast；

## 安全地處理表單資料  {#securely-handle-forms-data}

AEM Forms會將資料儲存至預先定義的位置和暫時資料夾。 您應該保護資料安全，以防止未經授權的使用。

### 設定定期清除暫存資料夾 {#setup-periodic-cleanup-of-temporary-folder}

當您設定檔案附件的表單、驗證或預覽元件時，對應的資料會儲存在位於/tmp/fd/的發佈節點上。 資料會定期清除。 您可以修改預設的資料清除工作，使其更具侵略性。 若要修改排定清除資料的工作，請開啟AEM Web主控台、開啟AEM Forms臨時儲存清除工作，並修改Cron運算式。

在上述案例中，只會為已驗證身分的使用者儲存資料。 此外，資料受到存取控制清單(ACL)的保護。 因此，修改資料永久刪除是保護資訊的額外步驟。

### 表單入口網站提交動作儲存的安全資料 {#secure-data-saved-by-forms-portal-submit-action}

依預設，最適化表單的Forms Portal提交動作會將資料儲存在發佈節點的本機存放庫中。 資料會儲存在/content/forms/fp。 **不建議將資料儲存在發佈執行個體上。**

您可以將儲存服務設定為透過網路傳送至處理叢集，而不需將任何內容儲存在發佈節點的本機。 處理叢集位在私人防火牆後面的安全區域中，資料仍保持安全。

使用AEM DS設定服務的處理伺服器認證，將資料從發佈節點發佈到處理伺服器。 建議使用對處理伺服器的存放庫具有讀寫存取許可權的受限制非管理使用者的認證。 如需詳細資訊，請參閱 [設定草稿和提交的儲存服務](/help/forms/using/configuring-draft-submission-storage.md).

### 由表單資料模型(FDM)處理的安全資料 {#secure-data-handled-by-form-data-model-fdm}

使用具有最低必要許可權的使用者帳戶來設定表單資料模型(FDM)的資料來源。 使用管理帳戶可向未獲授權的使用者提供對中繼資料和結構描述實體的開放存取。\
資料整合也提供授權FDM服務請求的方法。 您可以插入預先和後續執行授權機制來驗證請求。 服務請求是在預先填寫表單、提交表單和透過規則叫用服務時產生的。

**預先處理授權：** 您可以在執行請求之前，使用預先處理授權來驗證請求的真實性。 您可以使用輸入、服務和請求詳細資料來允許或停止執行請求。 如果執行停止，您可以傳回資料整合例外狀況OPERATION_ACCESS_DENIED。 您也可以在傳送使用者端請求以供執行之前修改該請求。 例如，變更輸入並新增其他資訊。

**處理後授權：** 您可以使用後處理授權來驗證和控制結果，然後再將結果傳回給請求者。 您也可以篩選、刪減和插入其他資料至結果。

### 限制使用者存取 {#limit-user-access}

創作、發佈和處理執行個體需要一組不同的使用者角色。 請勿使用管理員認證執行任何執行個體。

**在發佈執行個體上：**

* 只有表單 — 使用者群組的使用者可以預覽、建立草稿和提交表單。
* 只有cm-user-agent群組的使用者可以預覽通訊管理信件。
* 停用所有非必要的匿名存取。

**在作者執行個體上：**

* 預先定義了一組不同的群組，每個角色都有特定的許可權。 將使用者指派至群組。

   * 表單 — 使用者群組的使用者：

      * 可以建立、填寫、發佈及提交表單。
      * 無法建立XDP型最適化表單。
      * 無權為最適化表單編寫指令碼。
      * 無法匯入XDP或任何包含XDP的封裝
   * 表單的使用者超級使用者群組可建立、填寫、發佈及提交所有型別的表單、編寫最適化表單的指令碼，以及匯入包含XDP的套件。
   * 範本作者和範本超級使用者的使用者可以預覽和建立範本。
   * fdm作者的使用者可以建立和修改表單資料模型。
   * cm-user-agent群組的使用者可以建立、預覽和發佈通訊管理信件。
   * 工作流程編輯器群組的使用者可以建立收件匣應用程式和工作流程模型。


**處理作者時：**

* 對於遠端儲存和提交使用案例，請建立具有crx-repository的內容/表單/fp路徑讀取、建立和修改許可權的使用者。
* 將使用者新增至工作流程 — 使用者群組，讓使用者能夠使用AEM收件匣應用程式。

## AEM Forms環境的安全內部網路元素 {#secure-intranet-elements-of-an-aem-forms-environment}

一般而言，處理叢集和Forms Workflow附加元件(JEE上的AEM Forms)會在防火牆後面執行。 因此，這些被認為是安全的。 您仍然可以執行一些步驟來強化這些環境：

### 安全處理叢集 {#secure-processing-cluster}

處理叢集會在作者模式下執行，但不會將其用於開發活動。 不允許在處理叢集的內容作者和表單使用者群組中包含一般使用者。

### 使用AEM最佳實務來保護AEM Forms環境的安全 {#use-aem-best-practices-to-secure-an-aem-forms-environment}

本檔案提供AEM Forms環境的特定指示。 您應確保基礎AEM安裝部署時安全無虞。 如需詳細指示，請參閱 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md) 說明檔案。
