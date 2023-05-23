---
title: 收藏集、代碼片段和代碼片段範本的多重租用
description: 瞭解多租使用者功能如何讓您根據客戶組織來隔離CRX存放庫中的內容，以防止未經授權的存取。
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 收藏集、代碼片段和代碼片段範本的多重租用 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

多租使用者功能可讓您根據組織首碼和組織ID在CRX中分隔內容，以防止其他組織的使用者未經授權存取內容。

[!DNL Adobe Experience Manager Assets] 會以不同路徑儲存每個組織的資料。 每個組織特定的路徑都由組織首碼和組織ID識別，這些組織首碼和組織ID包含在傳統位置，而不同型別的資產會儲存在CRX中。

例如，如果您建立的資料夾名為 `Demo`， [!DNL Experience Manager] 資產傳統上會將資料夾儲存在 `../content/dam/Demo`. 啟用多租戶後，您現在可以將資料儲存在 `../content/dam/<organization prefix>/<organization id>Demo`

例如，如果 [!DNL Adobe Marketing Cloud] 使用者 [!DNL Assets] （隨選）指派給 `aodpremium` 組織，您可以使用多租使用者功能來設定 `../content/dam/<mac>/<aodpremium>Demo` 分隔其內容的路徑。 在此範例中， `mac` 是組織首碼，且 `aodpremium` 是組織ID。

根據使用者的組織和ID，此合格路徑會顯示在 [!DNL Assets] 介面和各種精靈，包括用來強制隔離的「移動」和「程式碼片段」建立精靈。

多租使用者功能可讓您分隔下列資產和元件型別：

* 收藏集
* 公開集合
* 目錄（包括「新增/選取頁面」精靈）
* 模板
* 程式碼片段範本
* Lightbox
