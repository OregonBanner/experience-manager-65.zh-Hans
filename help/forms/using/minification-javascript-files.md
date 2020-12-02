---
title: JavaScript文件的精简
seo-title: JavaScript文件的精简
description: 关于在AEM Forms工作区自定义后生成简化代码以优化Web JS文件的说明。
seo-description: 关于在AEM Forms工作区自定义后生成简化代码以优化Web JS文件的说明。
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# JavaScript文件{#minification-of-the-javascript-files}的精简

“微型化”从源代码中删除多余的字符，如空白、新行和注释。 这通过减小代码大小来改进性能。 虽然细化不会影响功能，但会降低代码的可读性。

要为语义更改生成简化代码，请执行以下步骤。

1. 从文件系统上的src-package复制`client-html/src/main/webapp/js`。

   >[!NOTE]
   >
   >有关包的详细信息，请参见[自定义AEM Forms工作区简介](/help/forms/using/introduction-customizing-html-workspace.md)。

1. `main.js`中的更新路径（位于client-html/src/main/webapp/js下），用于添加／更新的型号/视图。

   例如，添加新的Sharequeue模型（如mySharequeue），请更改：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   收件人

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新`registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,`，以防在`main.js`中出现别名的更改／添加。

   例如，添加新的Sharequeue模型（如mySharequeue），请更改：

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

   它在client-html/src/main/webapp/js下生成一个文件夹minified-files，其中包含minifed main.js和registry.js。

>[!NOTE]
>
>缩小功能仅适用于64位JVM。

>[!NOTE]
>
>如果您是小型的，则升级会受到影响。
