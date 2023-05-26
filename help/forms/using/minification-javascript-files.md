---
title: JavaScript文件缩小
seo-title: Minification of the JavaScript files
description: 有关在AEM Forms工作区自定义以优化Web版JS文件后生成缩小的代码的说明。
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

# JavaScript文件缩小 {#minification-of-the-javascript-files}

缩小会从源代码中删除多余的字符，如空格、换行符和注释。 这通过减小代码的大小改进了性能。 虽然缩小不会影响功能，但它会降低代码的可读性。

要生成用于语义更改的缩小代码，请执行以下步骤。

1. 复制 `client-html/src/main/webapp/js` 文件系统上的src-package。

   >[!NOTE]
   >
   >参见 [自定义AEM Forms工作区简介](/help/forms/using/introduction-customizing-html-workspace.md) 以了解有关包的更多详细信息。

1. 更新中的路径 `main.js` 位于client-html/src/main/webapp/js下，用于添加/更新的模型/视图。

   例如，添加新的Sharequeue模型（如mySharequeue）后，会更改：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   收件人

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 如果中别名发生了更改/添加 `main.js`.

   例如，添加新的Sharequeue模型（如mySharequeue）后，会更改：

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

   它生成一个文件夹缩小文件，位于client-html/src/main/webapp/js下，其中包含缩小的main.js和registry.js。

>[!NOTE]
>
>缩小操作仅适用于64位JVM。

>[!NOTE]
>
>如果缩小，则升级会受到影响。
