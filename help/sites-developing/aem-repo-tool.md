---
title: AEM Repo 工具
description: AEM Repo Tool是一种简单的解决方案，它通过类似于FTP的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo工具与Jackrabbit FileVault工具类似，但速度更快，具有最小的依赖关系，并且是一个简单的bash脚本。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 2%

---

# AEM Repo 工具{#aem-repo-tool}

AEM Repo Tool是一种简单的解决方案，可通过类似于FTP的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo工具类似于 [Jackrabbit FileVault工具](/help/sites-developing/ht-vlttool.md)，但速度更快，具有最小的依赖关系，并且是一个简单的bash脚本。

此工具简化了开发人员的文件传输，并且还可以集成到IntelliJ和Eclipse中，以提高开发效率。

## 概述 {#overview}

对于内的给定路径 `jcr_root` filevault结构在文件系统上，AEM Repo Tool为整个子树创建一个带有单个过滤器的包，并将该包推送到服务器（与FTP类似） `put`)，从服务器获取它( `get`)或比较两者之间的差异( `status` 和 `diff`)。

该工具不支持多个过滤器路径或FileVault的 `filter.xml`.

>[!CAUTION]
>
>AEM Repo Tool始终覆盖指定的整个文件或目录。

## 下载和文档 {#download-and-documentation}

此 [通过此链接可在GitHub上找到AEM Repo Tool](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及详细的安装和使用说明。

如果要下载AEM Repo Tool的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
