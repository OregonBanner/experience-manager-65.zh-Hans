---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: AEM存储库工具是一个简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo tool与Jackrabbit fileVault工具类似，但速度更快，相关性最小，是一个简单的bash脚本。
seo-description: AEM存储库工具是一个简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo tool与Jackrabbit fileVault工具类似，但速度更快，相关性最小，是一个简单的bash脚本。
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Repo Tool{#aem-repo-tool}

AEM存储库工具是一个简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo tool与 [Jackrabbit fileVault工具类似](/help/sites-developing/ht-vlttool.md)，但速度更快，相关性最小，是一个简单的bash脚本。

此工具为开发人员简化了文件传输，还可集成到IntelliJ和Eclipse中以使开发更加高效。

## 概述 {#overview}

对于文件系统上的文件结构内的给定路径， `jcr_root` AEM Repo Tool会为整个子树创建一个包含单个过滤器的包，并将其推送到服务器(与FTP相似 `put`)，从服务器获取它( `get`)或比较差异( `status``diff`和)。

该工具不支持多个过滤器路径或FileVault的过滤器 `filter.xml`。

>[!CAUTION]
>
>请注意，AEM Repo Tool将始终覆盖指定的整个文件或目录。

## 下载和文档 {#download-and-documentation}

GitHub上 [提供AEM Repo Tool](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) （AEM回购工具），此链接以及详细的安装和使用说明。

如果您希望下载AEM Repo tool的源，请参阅以下链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

