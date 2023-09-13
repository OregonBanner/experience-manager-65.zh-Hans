---
title: JavaScript文件的缩小
description: 说明如何在AEM Forms工作区自定义后生成缩小的代码，以便为Web优化JS文件。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# JavaScript文件的缩小 {#minification-of-the-javascript-files}

缩小会从源代码中删除多余的字符，如空格、新行和注释。 这通过减小代码大小提高了性能。 虽然缩小不会影响功能，但它会降低代码的可读性。

要生成用于语义更改的缩小代码，请执行以下步骤。

1. 复制 `client-html/src/main/webapp/js` 文件系统上的src-package。

   >[!NOTE]
   >
   >请参阅 [自定义AEM Forms工作区简介](/help/forms/using/introduction-customizing-html-workspace.md) 以了解有关包的更多详细信息。

1. 更新中的路径 `main.js` 位于client-html/src/main/webapp/js下，用于添加/更新模型/视图。

   例如，添加新的Sharequeue模型（如mySharequeue）会更改：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   收件人

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 如果更改/添加别名， `main.js`.

   例如，添加新的Sharequeue模型（如mySharequeue）会更改：

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

1. 在client-html/src/main/webapp/js/minifier上，运行命令：

   ```shell
   mvn clean install
   ```

   它生成一个缩小文件文件夹，位于client-html/src/main/webapp/js下，其中包含缩小的main.js和registry.js。

>[!NOTE]
>
>缩小仅适用于64位JVM。

>[!NOTE]
>
>如果缩小，您的升级将受到影响。
