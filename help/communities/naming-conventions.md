---
title: Java套件名稱中的命名慣例
description: Java套件名稱中的連字型大小
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---

# 命名约定 {#naming-conventions}

## Java套件名稱中的連字型大小 {#hyphens-in-java-package-name}

建立Java類別的位置時，請注意，套件名稱必須與存放庫資料夾位置的名稱相符，且路徑中的任何連字型大小都必須正確逸出。

雖然在AEM開發中，建議在存放庫專案的名稱中使用連字型大小，但Java套件名稱中的連字型大小不合法。

底層CRX平台必須能夠區分實際底線 `_ `和連字型大小 `-`. 因此，在JCR中，連字型大小必須替換為其Unicode值(u002d)，並以底線逸出 `_`.

例如，如果存放庫路徑為 **/apps/my-example/component/info/Info.java**，封裝名稱應為 `java package apps.my_002dexample.component.info;`

請注意，底線同樣必須逸出，這樣 `_` 變成 `_005f`.
