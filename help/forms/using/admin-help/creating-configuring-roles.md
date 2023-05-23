---
title: 建立和設定角色
seo-title: Creating and configuring roles
description: 瞭解如何將使用者和群組與已成為「使用者管理」資料庫一部分的角色相關聯。 您也可以建立、編輯和刪除角色。
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# 建立和設定角色{#creating-and-configuring-roles}

您可以使用「使用者管理」網頁，將使用者與群組與已經是「使用者管理」資料庫一部分的角色建立關聯。 您也可以建立、編輯和刪除角色。

「使用者管理」有兩種角色：

**可變角色：** 您可以編輯和刪除此類角色，也可以從這些角色型別新增和刪除角色許可權。 您建立的任何角色都視為可變角色。 您可以新增或移除指派給可變角色的使用者和群組。

**不可變角色：** 「使用者管理」中包含的預設角色為不可變角色。 無法編輯或刪除這些角色。 但是，您可以新增或移除指派給不可變角色的使用者和群組。

可變和不可變角色也可以透過AEM Forms API建立。

## 預設角色 {#default-roles}

下列預設角色包含在「使用者管理」資料庫中。

**Administration Console使用者：** 可以存取管理主控台。

**應用程式管理員：** 可以使用所有Workbench功能。 可以使用Administration Console中的「應用程式和服務」頁面來設定服務執行階段特性、端點和安全性。

**AEM表單管理員：** 可以執行所有已安裝服務的所有工作。

**安全管理員：** 控制使用者管理設定，並管理與任何使用者管理員網域相關聯的使用者和群組

**服務使用者：** 可以檢視及叫用任何服務

**超級管理員：** 可存取系統中的所有管理功能，包括服務

**信任管理員：** 可以管理從管理主控台的「信任存放區管理」頁面管理的PKI信任設定值和PKI證明資料

### 其他預設角色 {#additional-default-roles}

根據您安裝的AEM Forms元件，可能包括以下其他預設角色

**檔案上傳應用程式使用者：** 可使用Flex Remoting上傳檔案。

**Forms管理員：** 可以從Administration Console的Forms頁面檢視及修改設定

**AEM Forms Contentspace管理員：** 可以從Administration Console的Content Services (Deprecated)頁面檢視和修改設定

**AEM Forms Contentspace使用者：** 可以登入Contentspace （已棄用）網頁

**Documentum Connector管理員：** 可以從Administration console的Connector for EMC Documentum頁面檢視和修改設定

**AEM Forms FileNet聯結器管理員：** 可以從Administration Console的Connector for IBM FileNet頁面檢視及修改設定

**AEM forms IBM CM聯結器管理員：** 可以從Administration Console的IBM Content Manager聯結器頁面檢視和修改設定

**Rights Management管理員：** 執行相關Rights Management頁面上所有伺服器設定所需的所有工作

**Rights Management一般使用者：** 可存取Rights Management一般使用者網頁

**Rights Management邀請使用者：** 可以邀請使用者

**Rights Management管理受邀和本機使用者：** 可以執行管理相關Rights Management頁面上所有受邀和本機使用者所需的工作

**Rights Management原則集管理員：** 執行相關Rights Management頁面上所有原則集所需的所有工作

**Rights Management超級管理員：** 執行Rights Management頁面所需的所有工作

**AEM Forms工作區管理員：** 可以從「管理主控台」的「工作區」頁面檢視及修改設定

***注意&#x200B;**：AEM Forms版本已棄用Flex Workspace。*

**工作區使用者：** 可登入Workspace一般使用者應用程式

**輸出管理員：** 可以從Administration Console的[輸出]頁面檢視及修改設定

**PDFG管理員：** 可以從Administration Console的PDF產生器頁面檢視及修改設定

**PDFG使用者：** 可以存取PDF產生器的所有非管理功能

**Acrobat Reader DC擴充功能Web應用程式：** 可以使用Acrobat Reader DC擴充功能Web應用程式

>[!NOTE]
>
>出於安全原因，具有特定管理員許可權型別的使用者無法存取Workspace一般使用者網頁。 因為這些頁面可能存在於防火牆之外，允許管理層級工作可能會帶來安全性風險。 只有具有AEM Forms Workspace管理員或AEM Forms Workspace使用者許可權的使用者才能存取Workspace一般使用者網頁。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

## 建立角色 {#create-a-role}

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「新增角色」。
1. 在「角色名稱」方塊中，輸入角色名稱，並選擇性地輸入角色描述，然後按下一步。

   >[!NOTE]
   >
   >使用MySQL時，您無法建立名稱相同但擴充字元使用方式不同的兩個角色。 例如，當名為abcde的角色已存在時，嘗試建立名為abcde的角色會導致錯誤。

1. 按一下尋找許可權，選取要新增至角色的許可權。
1. 按一下「確定」，然後按一下「下一步」。
1. 將此角色指派給使用者和群組：

   * 按一下「尋找使用者/群組」。
   * 在「尋找」方塊中，輸入搜尋條件。
   * 選取「名稱」、「電子郵件」或「使用者ID」，然後選取「使用者」、「群組」或「使用者與群組」。
   * 選取領域，選取要顯示的結果數目，然後按一下「尋找」。
   * 選取要指派此角色的使用者和群組核取方塊，然後按一下「確定」。

1. 若要檢視使用者和群組詳細資訊，請選取實體。
1. 按一下「確定」，然後按一下「完成」。

## 編輯角色 {#edit-a-role}

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「角色名稱」。

   依預設，「角色管理」頁面會顯示「使用者管理」資料庫中的所有角色。 如果角色清單很大，請使用頁面頂端的「尋找」區域來搜尋特定的角色名稱。

1. 按一下要編輯的角色、編輯一般設定，然後按一下儲存。
1. 若要編輯角色許可權，請按一下「許可權」索引標籤並執行下列工作：

   * 若要新增許可權，請按一下[尋找許可權]，選取要新增的許可權核取方塊，按一下[確定]，然後按一下[儲存]。
   * 若要從角色中刪除許可權，請選取許可權的核取方塊，按一下「刪除」，然後按一下「儲存」。

1. 若要管理角色指派給誰，請按一下「角色使用者」索引標籤，然後執行下列工作：

   * 若要將角色指派給新的使用者和群組，請按一下「尋找使用者/群組」，然後完成搜尋資訊。 選取要指派此角色之每個使用者和群組的核取方塊，按一下「確定」，然後按一下「儲存」。
   * 若要移除角色，請選取使用者或群組的核取方塊，按一下「取消指派」，然後按一下「儲存」。

## 刪除角色 {#delete-a-role}

您可以刪除任何您建立的角色，但不會刪除產品中包含的預設AEM表單角色。

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「角色名稱」。

   依預設，「角色管理」頁面會顯示「使用者管理」資料庫中的所有角色。 如果角色清單很大，請使用頁面頂端的「尋找」區域來搜尋特定的角色名稱。

1. 選取要刪除的角色的核取方塊，按一下刪除，然後按一下確定。

## 指派角色給使用者和群組 {#assign-a-role-to-users-and-groups}

1. 在管理控制檯中，按一下「設定>使用者管理>使用者和群組」。
1. 指定資訊以縮小搜尋範圍，然後按一下「尋找」。 搜尋結果會列在頁面底部。 您可以按一下任何欄標題來排序清單。
1. 選取使用者與群組旁的核取方塊，以與角色建立關聯，然後按一下「指派角色」。
1. 選取要指派給使用者或群組的角色，然後按一下確定。

您也可以使用「角色管理」頁面來指派角色。

## 決定指派給角色的使用者 {#determine-who-is-assigned-to-a-role}

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「角色名稱」。

   依預設，「角色管理」頁面會顯示「使用者管理」資料庫中的所有角色。 如果角色清單很大，請使用頁面頂端的「尋找」區域來搜尋特定的角色名稱。

1. 在「角色詳細資訊」頁面上，按一下「角色使用者」標籤。 隨即顯示與該角色直接相關聯的使用者和群組清單。

## 變更角色許可權 {#change-role-permissions}

您可以變更您建立的任何角色的許可權。 您無法變更產品中所包含預設AEM表單角色的許可權。

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「角色名稱」。

   依預設，「角色管理」頁面會顯示「使用者管理」資料庫中的所有角色。 如果角色清單很大，請使用頁面頂端的「尋找」區域來搜尋特定的角色名稱。

1. 選取要檢視許可權的角色，然後按一下「許可權」索引標籤。
1. 若要變更這些許可權，請按一下[尋找許可權]，選取要新增至角色之許可權的核取方塊，按一下[確定]，然後按一下[儲存]。
1. 若要刪除許可權，請選取許可權，按一下刪除，然後按一下儲存。

### AEM forms許可權 {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM：** 新增、移除和修改服務的端點

**Admin Console登入：** 檢視管理主控台

**憑證修改：** 修改信任存放區中任何憑證的信任設定

**憑證讀取：** 讀取信任存放區中的任何憑證

**憑證寫入：** 新增憑證至信任存放區

**元件新增：** 在系統中安裝新元件

**元件刪除：** 刪除系統中的任何元件

**元件讀取：** 讀取系統中的任何元件

**Contentspace管理員：** Contentspace （已棄用）管理員的許可權

**Contentspace主控台登入：** Contentspace （已棄用）主控台登入的許可權

**核心設定控制：** 在管理控制檯中管理「核心系統設定」頁面上的設定

**CREATE_VERSION_PERM：** 建立服務的新版本

**認證修改：** 修改信任存放區中的任何簽署認證

**已讀取的認證：** 讀取信任存放區中的任何簽署認證

**認證寫入：** 新增簽署認證至信任存放區

**CRL修改：** 修改信任存放區中的任何CRL （憑證撤銷清單）

**CRL讀取：** 讀取信任存放區中的任何CRL

**CRL寫入：** 將CRL新增至信任存放區

**委派：** 在資源上設定ACL

**DELETE_版本_PERM：** 刪除服務的版本

**檔案上傳：** 在AEM表單中上傳檔案

**網域控制：** 建立、刪除或修改任何使用者管理網域的設定，包括其驗證和目錄提供者

**事件型別編輯：** 編輯事件型別

**身分模擬控制：** 在使用者管理員中模擬身分

**INVOKE_PERM：** 叫用服務上的所有作業

**LCDS資料模型控制：** 讀取和部署資料服務中的資料模型

**License Manager更新：** 更新授權資訊

**MODIFY_CONFIG_PERM：** 修改服務的設定

**詞語** 修改服務的版本

**PDFGAdminPermission：** PDFG管理員

**PDFGUserPermission：** PDFG使用者

**PERM_DCTM_ADMIN：** Documentum Connector管理員

**PERM_FILENET_ADMIN：** FileNet聯結器管理員

**PERM_FORMS_ADMIN：** Forms管理員

**PERM_IBMCM_ADMIN：** IBM CM Connector管理員

**PERM_OUTPUT_ADMIN：** 輸出管理員

**PERM_EXTENSIONS_WEB_APPLICATIONREADER：** 使用Acrobat Reader DC擴充功能Web應用程式

**PERM_SP_ADMIN：** 管理SharePoint聯結器設定

**PERM_WORKSPACE_ADMIN：** 管理工作區設定

**PERM_WORKSPACE_USER：** 登入Workspace使用者應用程式

**主體控制：** 管理任何網域的使用者和群組，以及管理任何網域中所有使用者和群組的角色指派

**處理記錄讀取/刪除：** 列出和擷取工作流程稽核例項

**PROCESS_OWNER_PERM：** 檢視趨勢資料，並對從處理序建立的服務執行管理動作

**讀取：** 讀取資源的內容

**讀取_PERM：** 讀取或檢視服務

**更新宣告：** 在User Management中更新宣告

**存放庫委派：** 在資源上設定ACL

**存放庫讀取：** 讀取資源的內容

**存放庫周遊：** 在資源清單請求中包含資源或讀取資源的中繼資料

**存放庫寫入：** 寫入存放庫中繼資料和內容

**Rights Management變更原則擁有者：** 變更原則擁有者

**Rights Management一般使用者控制檯登入：** 登入Rights Management一般使用者UI

**Rights Management管理設定：** 管理伺服器設定

**Rights Management管理受邀和本機使用者：** 管理受邀和本機使用者

**Rights Management管理原則集：** 管理任何原則集內的所有原則和檔案

**Rights Management原則集新增協調器：** 新增、移除和變更原則集協調員的許可權

**Rights Management原則集建立原則：** 為原則集建立新原則

**Rights Management原則集刪除原則：** 從原則集移除原則

**Rights Management原則集編輯原則：** 編輯原則集中的原則

**Rights Management原則集管理檔案發行者：** 當您建立原則集時，您會將檔案發行者的角色指派給使用者。 檔案發佈者是使用原則保護檔案的使用者。

**Rights Management原則集移除協調器：** 從原則集中移除原則集協調器

**Rights Management原則集撤銷檔案：** 撤銷原則集中檔案的存取權

**Rights Management原則設定切換器原則：** 切換檔案的原則

**Rights Management原則集取消撤銷檔案：** 取消撤銷檔案

**Rights Management原則集檢視事件：** 檢視原則集內任何原則或檔案的原則和檔案事件

**Rights Management檢視伺服器事件：** 搜尋並檢視所有稽核事件

**角色控制：** 在User Management中建立、刪除及修改角色

**服務啟動：** 啟動任何服務，使其可用於叫用

**服務新增：** 將新服務部署至服務登入。 這包括新增新程式與程式變體

**服務停用：** 停止系統中的任何服務

**服務刪除：** 刪除系統中的任何服務，包括流程和流程變體

**服務叫用：** 在執行階段可叫用服務登入中的任何服務

**服務修改：** 修改系統中任何服務的組態屬性。 這包括鎖定和解鎖IDE中的服務，以及新增或移除服務的端點

**服務讀取：** 讀取系統中的任何服務。 這包括所有流程和流程變體

**SERVICE_AGENT_PERM：** 針對從程式建立的服務，檢視資料並與程式執行個體互動

**SERVICE_MANAGER_PERM：** 對從處理序建立的服務執行負載平衡和其他管理動作

**START_STOP_PERM：** 啟動或停止服務

**監督員_PERM：** 檢視從處理序建立之服務的處理序執行個體資料

**周遊：** 在資源清單請求中包含資源或讀取資源的中繼資料

**寫入：** 寫入存放庫中繼資料和內容

**在Workbench中開啟檔案**

若要在Workbench中檢視「資源」檢視的內容並開啟檔案以供檢視，使用者需要下列許可權：

* 存放庫讀取
* 存放庫周遊
* 服務叫用
* 服務讀取

## 從角色中移除使用者或群組 {#remove-a-user-or-group-from-a-role}

您可以在「角色管理」頁面移除特定角色的使用者和群組。 如果使用者或群組繼承了角色指派，則您無法在使用者或群組層級移除角色。 從繼承樹狀結構中移除使用者或群組，或從父項中移除角色。

1. 在管理控制檯中，按一下「設定>使用者管理>角色管理」，然後按一下「角色名稱」。

   依預設，「角色管理」頁面會顯示「使用者管理」資料庫中的所有角色。 如果角色清單很大，請使用頁面頂端的「尋找」區域來搜尋特定的角色名稱。

1. 在角色清單中，按一下要更新的角色名稱，然後按一下角色使用者索引標籤。 隨即顯示與該角色相關聯的使用者和群組清單。
1. 選取要從角色中移除的使用者和群組核取方塊，然後按一下取消指派。
1. 按一下「儲存」，然後按一下「確定」。
