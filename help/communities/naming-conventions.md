---
title: Java&trade；包名称中的命名约定
description: 了解命名惯例以及Java&trade；包名称中连字符的使用。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---

# 命名约定 {#naming-conventions}

## Java™包名称中的连字符 {#hyphens-in-java-package-name}

在创建Java™类的位置时，包名称必须与存储库文件夹位置的名称匹配，并且路径中的所有连字符都应正确转义。

虽然在AEM开发中，建议在存储库项目的名称中使用连字符，但Java™包名称中的连字符非法。

底层CRX平台必须能够区分实际下划线 `_ `和连字符 `-`. 因此，在JCR中，连字符必须替换为其Unicode值(u002d)，并使用下划线进行转义 `_`.

例如，如果存储库路径为 **/apps/my-example/component/info/Info.java**，包名称应为 `java package apps.my_002dexample.component.info;`

请注意，下划线必须同样进行转义，以便 `_` 变为 `_005f`.
