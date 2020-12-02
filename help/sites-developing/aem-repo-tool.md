---
title: AEM Repo工具
seo-title: AEM Repo工具
description: AEM Repo Tool是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo Tool与Jackrabbit FileVault工具类似，但速度更快，相关性最小，是一个简单的bash脚本。
seo-description: AEM Repo Tool是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo Tool与Jackrabbit FileVault工具类似，但速度更快，相关性最小，是一个简单的bash脚本。
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo Tool与[Jackrabbit FileVault工具](/help/sites-developing/ht-vlttool.md)类似，但速度更快，相关性最小，是一个简单的bash脚本。

此工具为开发人员简化了文件传输，还可集成到IntelliJ和Eclipse中，使开发更高效。

## 概述 {#overview}

对于文件系统上`jcr_root`文件结构内的给定路径，AEM Repo Tool会为整个子树创建一个具有单个过滤器的包，并将它推送到服务器（类似于FTP `put`），从服务器(`get`)中获取它或比较差异（`status`和`diff`）。

该工具不支持多个筛选器路径或FileVault的`filter.xml`。

>[!CAUTION]
>
>请注意，AEM Repo Tool将始终覆盖指定的整个文件或目录。

## 下载和文档{#download-and-documentation}

[AEM Repo Tool可通过此链接](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上提供，并提供详细的安装和使用说明。

如果您希望下载AEM Repo Tool的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

