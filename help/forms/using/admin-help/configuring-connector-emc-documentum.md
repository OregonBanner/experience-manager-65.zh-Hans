---
title: 為EMC Documentum設定聯結器
seo-title: Configuring Connector for EMC Documentum
description: 瞭解如何設定EMC Documentum聯結器，以啟用AEM Forms與EMC Documentum之間的通訊。
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 為EMC Documentum設定聯結器 {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum可實現AEM Forms與EMC Documentum之間的通訊。 如需其他背景資訊，請參閱以下的「Connectors for ECM」： [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

設定EMC Documentum的聯結器需要設定伺服器連線和存放庫憑證。

>[!NOTE]
>
>在舊版中，資產可以儲存在ECM存放庫中。 在目前版本中，資產會儲存在AEM Forms原生存放庫中，且存放庫Provider Services已過時。 資產從ECM存放庫移轉至AEM表單存放庫是在您執行升級至AEM表單時完成的。 如需詳細資訊，請參閱應用程式伺服器的AEM表單升級指南。

## 設定伺服器連線 {#configuring-the-server-connection}

本主題說明您可以在「組態設定」頁面上執行的EMC Documentum聯結器工作。

>[!NOTE]
>
>如果您同時設定所有設定，則只需按一下「儲存」一次。

### 設定伺服器 {#configure-the-server}

您必須設定連線代理人伺服器資訊。 此資訊對於連線到Documentum內容存放庫和啟動EMC Documentum聯結器是必要的。

1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「組態設定」。
1. 在「Documentum組態資訊」區域中，輸入連線代理人的主機名稱或IP位址以及連線埠號碼。 連線埠號碼必須是正整數（例如1489）。
1. 单击“保存”。

### 設定主體認證 {#configure-principal-credentials}

在設定主體認證時，您提供的存放庫名稱取決於登入期間是否提供明確的存放庫名稱。

如果您輸入不正確的使用者名稱或密碼，將會根據服務目前是否執行而得到下列結果：

* 如果EMC Documentum Repository Provider服務和EMC Documentum Content Repository Connector服務都停止，當您儲存服務組態資訊時，不會出現任何錯誤。 不過，下次啟動服務時，將會擲回例外狀況，且服務不會啟動。
* 如果EMC Documentum Repository Provider服務或EMC Documentum Content Repository Connector服務已啟動，當您儲存服務組態資訊時，服務會嘗試立即驗證認證資訊。 在這種情況下，會發生錯誤且未儲存設定資訊。

1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「組態設定」。
1. 在「Documentum主體證明資料」區域中，輸入具有超級管理員許可權的使用者的使用者名稱和密碼。
1. 如果在登入期間未提供明確的存放庫名稱，請輸入與證明資料關聯的存放庫名稱。
1. 单击“保存”。

### 變更存放庫服務提供者 {#change-the-repository-service-provider}

您可以設定要搭配Documentum使用的儲存庫服務提供者。 存放庫服務呼叫會委派給您設定的提供者。 以下选项可供选择：

**目前的存放庫服務提供者名稱：** 目前存放庫服務提供者的名稱

**ECM Documentum儲存庫提供者：** 讓Documentum儲存庫提供者成為儲存庫的提供者。 此選項已過時

**存放庫提供者：** 讓原生存放庫提供者成為存放庫的提供者

>[!NOTE]
>
>若要選取所列專案以外的存放庫服務提供者，請在「應用程式和服務>服務管理」中設定RepositoryService。 <!-- Fix broken link (See Managing Services) -->.

1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「組態設定」。
1. 在「存放庫服務提供者資訊」區域中，選取替代的存放庫服務提供者。
1. 单击“保存”。

## 設定存放庫認證 {#configuring-repository-credentials}

Documentum認證資訊用於AEM表單系統內容。 存放庫認證是特定於Documentum中的特定存放庫。 您可以為任何數量的存放庫提供證明資料，但您只能為每個存放庫指定一組證明資料。

### 新增存放庫認證 {#add-a-repository-credential}

1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「存放庫憑證設定」。
1. 按一下「新增」。 便會顯示「Documentum系統證明資訊」頁面。
1. 輸入存放庫的名稱。
1. 輸入使用者名稱和密碼。
1. 单击“保存”。

如果EMC Documentum的Content Repository Connector服務和/或EMC Documentum的Repository Service正在執行，則在將認證資訊儲存在資料庫中之前，會針對指定的儲存庫進行驗證。 如果認證無效或存在，則會顯示錯誤訊息。

### 移除存放庫認證 {#remove-a-repository-credential}

1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「組態設定」。
1. 選取要從中移除認證的存放庫旁的核取方塊，然後按一下移除。 所選儲存區域的證明資料會從資料庫中移除。

### 變更存放庫認證的使用者名稱和密碼 {#change-the-user-name-and-password-for-a-repository-credential}

1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「組態設定」。
1. 按一下要編輯其證明資料的儲存庫名稱。
1. 變更存放庫的使用者名稱或密碼，或同時變更兩者。 （存放庫名稱是唯讀的。）
1. 单击“保存”。

如果EMC Documentum的Content Repository Connector服務和/或EMC Documentum的Repository Service正在執行，則在將認證資訊儲存在資料庫中之前，會針對指定的儲存庫進行驗證。 如果認證無效或存在，則會顯示錯誤訊息。

## 啟用共用工作區工作佇列的請求 {#enable-the-request-for-sharing-of-workspace-task-queues}

需要一些手動步驟，以確保Workspace中的「請求工作佇列共用」功能可與Connector for EMC Documentum正常運作。

1. 部署AEM Forms並安裝Workbench後，登入Workbench並開啟「資源」檢視。 您將決定QueueSharing.swf檔案在此檢視中的位置。
1. 將QueueSharing.swf檔案從「資源檢視」拖曳至Windows案頭或同等位置（視您的作業系統而定）。
1. 在管理控制檯中，按一下「服務」>「EMC Documentum聯結器」>「組態設定」。
1. 在「儲存庫服務提供者資訊」下，將已設定的儲存庫提供者變更為「EMC Documentum儲存庫提供者」。
1. 啟動Workbench，並將QueueSharing.swf檔案從您最初複製到的位置（例如Windows案頭或其他位置）複製到EMC Documentum存放庫內的現有目錄中。
1. 在「維護作業處理」檢視表中，開啟「佇列共用」處理。
1. 在「變數」檢視中，開啟「theForm」變數的屬性，並變更URI以符合您在步驟5中放置QueueSharing.swf檔案的路徑。
1. 儲存程式。
1. 根據貴組織的原則將流程移轉至生產環境。
