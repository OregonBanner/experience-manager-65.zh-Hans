---
title: 指定輸出的檔案位置
seo-title: Specify file locations for Output
description: 瞭解如何指定輸出的檔案位置。
seo-description: Learn how to specify file locations for Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 1%

---

# 指定輸出的檔案位置 {#specify-file-locations-for-output}

您可以指定Output尋找所需特定檔案型別的位置。

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「位置」下，指定適當的選項。
1. 单击“保存”。

## 位置設定 {#locations-settings}

**內容根URI：** 從中擷取表單的存放庫的URI或絕對位置。 此值會與sForm引數（透過API指定）結合，以建構擷取之表單的絕對路徑。 此值可參考可使用HTTP存取的目錄或Web位置。

預設值為空字串。

**XCI組態檔：** 輸出服務用於呈現的XCI組態檔的相對或絕對位置。 若為相對值，則假設XCI檔案位於AEM Forms可部署EAR檔案中。

默认值为 `com/adobe/formServer/PA/pa_output.xci`。

**快取位置：** 指定輸出磁碟快取的位置。 當您變更此設定時，會重設目前位置的所有現有快取資訊，並在新位置建立新的快取。 選取下列其中一個選項：

**預設位置：** 這是預設選取範圍。 選取此選項時，會在從屬於您正在使用的應用程式伺服器的位置建立快取：

* **JBoss：** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic：** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere：** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**LC暫存目錄：** 快取是在AEM forms暫存目錄的子目錄中建立的，該子目錄在「設定」>「核心系統設定」>「設定」>「暫存目錄的位置」下的管理控制檯中指定。 子目錄已命名 `adobeoutput_[servername]`.

>[!NOTE]
>
>如果您使用暫時清除公用程式，請注意，刪除這些目錄不會影響功能，但在建立新快取之前，可能會在短時間內顯著影響效能。 為避免此問題，在清除AEM表單臨時目錄時，請勿刪除這些目錄。
