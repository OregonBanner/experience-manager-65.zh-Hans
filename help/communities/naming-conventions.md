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
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 命名约定{#naming-conventions}

## Java包名称{#hyphens-in-java-package-name}中的连字符

在为Java类创建位置时，请注意，包名称必须与存储库文件夹位置的名称匹配，且路径中的任意连字符会被正确转义。

在AEM开发中，建议在存储库项目名称中使用连字符，但在Java包名称中，连字符是非法的。

基础CRX平台必须能够区分实际的下划线`_ `和连字符`-`。 因此，在JCR中，连字符必须替换为其unicode值(u002d)，并使用下划线`_`进行转义。

例如，如果存储库路径为&#x200B;**/apps/my-example/component/info/Info.java**，则包名称应为`java package apps.my_002dexample.component.info;`

请注意，下划线必须同样进行转义，以便`_`变为`_005f`。
