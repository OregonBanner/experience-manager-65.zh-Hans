---
title: 命名约定
seo-title: Naming Conventions
description: Java包名称中的连字符
seo-description: Hyphens in Java Package Name
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# 命名约定 {#naming-conventions}

## Java包名称中的连字符 {#hyphens-in-java-package-name}

在为Java类创建位置时，请注意，包名称必须与存储库文件夹位置的名称匹配，并且路径中的任何连字符都应正确转义。

虽然在AEM开发中，建议在存储库项目的名称中使用连字符，但Java包名称中的连字符非法。

底层CRX平台必须能够区分实际下划线 `_ `和连字符 `-`. 因此，在JCR中，连字符必须替换为其unicode值(u002d)，并使用下划线进行转义 `_`.

例如，如果存储库路径为 **/apps/my-example/component/info/Info.java**，包名称应为 `java package apps.my_002dexample.component.info;`

请注意，下划线同样必须转义，以便 `_` 变为 `_005f`.
