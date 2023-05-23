---
title: JavaScript檔案的縮制
seo-title: Minification of the JavaScript files
description: AEM Forms工作區自訂後，產生縮製程式碼的指示，以最佳化網頁的JS檔案。
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# JavaScript檔案的縮制 {#minification-of-the-javascript-files}

縮制會從原始程式碼中移除多餘的字元，例如空白字元、換行字元和註解。 這會藉由減少程式碼大小來改善效能。 雖然縮制不會影響功能，但會降低程式碼的可讀性。

若要產生語意變更的縮製程式碼，請依照下列步驟操作。

1. 複製 `client-html/src/main/webapp/js` 檔案系統上的src-package。

   >[!NOTE]
   >
   >另請參閱 [自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) 以取得有關套件的詳細資訊。

1. 更新中的路徑 `main.js` 位於client-html/src/main/webapp/js下方，用於新增/更新的模型/檢視。

   例如，新增新的Sharequeue模型（例如mySharequeue）後，會變更：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   收件人

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 萬一中別名變更/增加 `main.js`.

   例如，新增新的Sharequeue模型（例如mySharequeue）後，會變更：

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   收件人

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. 在client-html/src/main/webapp/js/minifier，執行命令：

   ```shell
   mvn clean install
   ```

   它會在client-html/src/main/webapp/js下產生一個資料夾縮制檔案，其中包含縮制的main.js和registry.js。

>[!NOTE]
>
>縮制僅適用於64位元JVM。

>[!NOTE]
>
>若您縮制，升級會受到影響。
