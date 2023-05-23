---
title: 設定IBM FileNet的聯結器
seo-title: Configuring Connector for IBM FileNet
description: 瞭解如何設定IBM FileNet的聯結器，以啟用AEM Forms與IBM FileNet之間的通訊。
seo-description: Learn how to configure the Connector for IBM FileNet to enable communication between AEM forms and IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# 設定IBM FileNet的聯結器 {#configuring-connector-for-ibm-filenet}

IBM FileNet聯結器可啟用AEM Forms與IBM FileNet之間的通訊。 如需其他背景資訊，請參閱以下的「Connectors for ECM」： [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>在舊版中，資產可以儲存在ECM存放庫中。 在此版本中，資產會儲存在AEM Forms原生存放庫中，且存放庫Provider Services已過時。 資產從ECM存放庫移轉至AEM表單存放庫是在您執行升級至AEM表單時完成的。 如需詳細資訊，請參閱應用程式伺服器的AEM表單升級指南。

## 設定與內容引擎的連線 {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine提供軟體服務，用於管理FileNet內容存放庫中的企業內容和客戶定義的商業物件。

1. 在Administration Console中，按一下「服務」>「IBM FileNet聯結器」。
1. 在「內容引擎URL」方塊中，輸入完整的連線URL。 例如：

   如果您使用FileNet Content Engine 4.x搭配CEWS傳輸，請輸入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果您使用FileNet Content Engine 4.x搭配EJB傳輸（只有WebLogic支援），請輸入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在「認證保護配置」清單中，選取下列其中一個保護等級：

   * **清除：** 以無保護模式透過網路傳送認證
   * **對稱：** 透過網路傳送加密的認證

1. 在「加密檔案位置」方塊中，輸入加密檔案的路徑：

   * 如果您選取「清除」作為認證保護配置，則會忽略此關鍵字及其值。
   * 如果您選取Symmetric作為認證保護配置，則您輸入的路徑會指向forms伺服器上包含要使用的密碼編譯金鑰的加密檔案的位置。

1. 在「預設物件存放區」方塊中，輸入AEM Forms預設會連線的物件存放區聯結器。
1. 在「使用者名稱」方塊中，輸入具有您在上一步中指定的預設物件存放區存取許可權的使用者的使用者名稱。
1. 在「密碼」方塊中，輸入使用者的密碼，然後按一下「儲存」。

## 設定程式引擎設定 {#configure-the-process-engine-settings}

IBM FileNet的聯結器包含IBM FileNet服務的Process Engine Connector，用於與IBM FileNet Process Engine互動。 您可以設定此服務的設定。

1. 在Administration Console中，按一下「服務」>「IBM FileNet聯結器」。
1. 若要啟用對IBM FileNet服務使用Process Engine Connector，請選取「使用Process Engine Connector服務」。
1. 在「處理路由器/連線點」方塊中，輸入主機名稱或IP位址和連線埠號碼，後接處理路由器名稱。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在「使用者名稱」方塊中，輸入用來連線至程式引擎的使用者名稱。
1. 在「密碼」方塊中，輸入用來連線至程式引擎的密碼，然後按一下「儲存」。

## 驗證服務設定 {#validation-of-service-settings}

如果您在設定「內容引擎」連線或「處理引擎」設定時輸入不正確的使用者名稱或密碼，將會根據服務目前是否執行而得到下列結果：

* 如果IBM FileNet的「儲存庫提供者」服務和IBM FileNet的「內容儲存庫聯結器」服務都已停止，當您儲存服務組態資訊時，不會出現任何錯誤。 不過，下次啟動服務時，將會擲回例外狀況，且服務不會啟動。
* 如果IBM FileNet的「儲存庫提供者」服務或IBM FileNet的「內容儲存庫聯結器」服務已啟動，當您儲存服務組態資訊時，服務會嘗試立即驗證認證資訊。 在這種情況下，會發生錯誤且未儲存設定資訊。

## 變更存放庫服務提供者 {#change-the-repository-service-provider}

您可以設定要搭配FileNet使用的存放庫服務提供者。 存放庫服務呼叫會委派給您設定的提供者。

以下选项可供选择：

**目前的存放庫提供者名稱：** 目前存放庫服務提供者的名稱

**IBM FileNet存放庫提供者：** 讓FileNet儲存區域提供者成為儲存區域的提供者。 此選項已過時。

**存放庫提供者：** 讓原生存放庫提供者成為存放庫的提供者

>[!NOTE]
>
>若要選取所列專案以外的存放庫服務提供者，請在「應用程式和服務」中設定RepositoryService。 <!-- Fix broken link(See Managing Services) -->

1. 在Administration Console中，按一下「服務」>「IBM FileNet聯結器」。
1. 在「存放庫服務提供者資訊」區域中，選取替代的存放庫服務提供者，然後按一下儲存。
