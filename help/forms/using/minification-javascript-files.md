---
title: JavaScript文件的缩小
seo-title: JavaScript文件的缩小
description: 关于在AEM Forms工作区自定义之后生成简化代码以优化Web JS文件的说明。
seo-description: 关于在AEM Forms工作区自定义之后生成简化代码以优化Web JS文件的说明。
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# JavaScript文件的缩小 {#minification-of-the-javascript-files}

“微型化”从源代码中删除冗余字符，如空白、新行和注释。 这通过减小代码大小来改进性能。 虽然细化不会影响功能，但会降低代码的可读性。

要为语义更改生成简化代码，请按照以下步骤操作。

1. 从文 `client-html/src/main/webapp/js` 件系统上的src包复制。

   >[!NOTE]
   >
   >有关 [包的更多详细信息，请参阅自定义AEM Forms工作区的介绍](/help/forms/using/introduction-customizing-html-workspace.md) 。

1. 更新位于 `main.js` client-html/src/main/webapp/js下的路径，用于添加／更新的型号/视图。

   例如，添加了新的Sharequeue模型（如mySharequeue），请更改：

   ```
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   
   To
   
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 新，以防在中更改／添加别名 `main.js`。

   例如，添加了新的Sharequeue模型（如mySharequeue），请更改：

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   
   To
   
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. 在client-html/src/main/webapp/js/minifier上，运行命令：

   ```shell
   mvn clean install
   ```

   它会在client-html/src/main/webapp/js下生成一个文件夹，其中包含main.js和registry.js。

>[!NOTE]
>
>缩小功能仅适用于64位JVM。

>[!NOTE]
>
>如果您是小型的，则升级会受到影响。
