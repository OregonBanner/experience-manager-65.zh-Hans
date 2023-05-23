---
title: 設定Forms的位置
seo-title: Configuring locations for Forms
description: 瞭解如何設定Forms的位置。
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# 設定Forms的位置 {#configuring-locations-for-forms}

您可以指定屬性的URL、URI和檔案位置，例如Web根目錄、要擷取的表單位置、PDFForm轉換中使用的種子PDF檔案以及快取位置。

1. 在Administration Console中，按一下「服務> Forms」。
1. 在「位置」下，指定適當的選項。 選項如下所述。
1. 单击“保存”。

## 位置設定 {#locations-settings}

**基本URL：** 影像和指令碼等表單資源所在的基本URL。 HTML轉換需要此值，其中包含外部從屬關係（如影像或指令碼）的HREF參照。 其中一個指令碼是xfasubset.js，這是HTML表單執行XFA智慧所必需的。 此值必須是內容根URI的HTTP對等值。

>[!NOTE]
>
>基本URL僅支援HTTP或存放庫通訊協定。 不支援file:///之類的通訊協定。 如果您需要存取資源（例如自訂CSS或數位簽名URI），請使用適當的API引數值來指定絕對位置。

當相依性路徑為絕對時，會忽略基本URL值。 否則，相依性路徑會與基礎URL結合。

預設值為空字串。

以下範例指向相同的內容（使用內容根URI和基本URL）：

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**FS Web根URI：** Forms網頁應用程式的URL。 如果Forms Web應用程式和使用者端應用程式部署在相同應用程式伺服器上，您可以將此方塊留空；將會使用Forms API Web根URL。

如果Forms Web應用程式和使用者端應用程式未部署至相同的應用程式伺服器，請在此方塊中提供Forms Web應用程式的URL，如下列範例所示：

`https://<host name>:<port>/FormServer`

位置 `host name`和 `port` 是裝載Forms Web應用程式的伺服器的伺服器名稱和連線埠號碼。

預設值為空字串。

**網頁根目錄URI：** 應用程式的網頁根目錄。 此值會與sTargetURL引數（當sTargetURL以相對形式提供時）結合(透過AEM Forms SDK指定)，以建構絕對URL來存取應用程式專屬的網頁內容。

預設值為空字串。

**內容根URI：** 從中擷取表單的URI或絕對位置。 此值會與sFormQuery引數（透過API指定）結合，以建構擷取之表單的絕對路徑。 此值可參考可使用HTTP存取的目錄或Web位置。

預設值為空字串。

**XCI設定URI：** 找到用於演算的XCI檔案的相對或絕對位置。 若為相對值，則假設XCI檔案位於可部署的AEM Forms EAR檔案中。

默认值为 `com/adobe/formServer/PA/pa.xci`。

**字型對應URI：** 字型對應檔案的相對或絕對位置。 若為相對值，則假設此檔案位於可部署的AEM Forms EAR檔案中。

字型對應檔案可用來建立表單中HTML轉換的自訂字型對應，因此可讓您指定當使用者端電腦上無法使用字型時，要取代的字型。

默认值为 `com/adobe/formServer/client-font-map.properties`。

下列專案是字型對應檔案中專案的範例：

`Arial=Arial,Helvetica,sans-serif`

**種子PDF檔案：** 用於PDFForm轉換以最佳化傳送的初始PDF檔案。 種子PDF檔案會指定自訂的PDF檔案（僅包含XFA資料流、影像和字型資源），並附加表單設計和資料。 表單會由Acrobat 7或更新版本轉譯，並套用至PDForm轉換。

預設值為空字串。

**快取位置：** 指定Forms磁碟快取的位置。 當您變更此設定時，會重設目前位置的所有現有快取資訊，並在新位置建立新的快取。 選取下列其中一個選項：

**預設位置：** 這是預設選取範圍。 選取此選項時，會在從屬於您正在使用的應用程式伺服器的位置建立快取：

* **JBoss：** [JBoss首頁]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic：** [WebLogic首頁]\user_projects\domains\[aem-forms網域名稱]\adobe\[forms伺服器名稱]\FormServer\Cache
* **WebSphere：** [IBM首頁]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**LC暫存目錄：** 快取是在AEM forms暫存目錄的子目錄中建立的，該子目錄在「設定」>「核心系統設定」>「設定」>「暫存目錄的位置」下的管理控制檯中指定。 子目錄名為adobeform_[伺服器名稱].

>[!NOTE]
>
>如果您使用暫時清除公用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，可能會在短時間內顯著影響效能。 為避免此問題，在清除AEM表單臨時目錄時，請勿刪除這些目錄。
