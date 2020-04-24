---
title: 命名约定
seo-title: 命名约定
description: Java包名称中的连字符
seo-description: Java包名称中的连字符
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# 命名约定 {#naming-conventions}

## Java包名称中的连字符 {#hyphens-in-java-package-name}

为Java类创建位置时，请注意，包名称必须与存储库文件夹位置的名称匹配，路径中的任何连字符必须正确转义。

在AEM开发中，建议在存储库项目名称中使用连字符，但连字符在Java包名称中是非法的。

基础CRX平台必须能够区分实际的下划线 `_ `和连字符 `-`。 因此，在JCR中，连字符必须替换为其unicode值(u002d)，并用下划线转义 `_`。

例如，如果存储库路径为/apps/my-example/component/info/Info.java ****，则包名称应为 `java package apps.my_002dexample.component.info;`

请注意，下划线同样必须转义，这样才 `_` 会变 `_005f`成。
