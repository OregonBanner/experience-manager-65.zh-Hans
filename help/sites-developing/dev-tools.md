---
title: 开发工具
seo-title: Development Tools
description: 要开发JCR、Apache Sling或AEM应用程序，可以使用许多工具集
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: 4967a6d9ad92272a1ff442456fe65de51cc46a73
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 4%

---

# 开发工具{#development-tools}

要开发JCR、Apache Sling或AEM应用程序，可以使用以下工具集：

* 一组包含 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 和WebDAV。 CRXDE Lite已嵌入到CRX/AEM中，并允许您在浏览器中执行标准开发任务。 使用CRXDE Lite，您可以在日志记录和与SVN集成时创建和编辑文件(如.jsp和.java)、文件夹、模板、组件、对话框、节点、属性和捆绑包。

   当您无法直接访问CRX/AEM服务器，当您通过扩展或修改现成的组件和Java捆绑包来开发应用程序，或者当您不需要专用的CRXDE Lite、代码完成和语法突出显示时，建议使用Debugger。

* 由集成开发环境组成的一组(例如： [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 或 [IntelliJ](/help/sites-developing/ht-intellij.md))，构建工具(例如： [Apache Maven](/help/sites-developing/ht-projects-maven.md))、Adobe开发的用于将存储库映射到文件系统的FileVault、版本控制系统（例如：Subversion）、错误跟踪器系统（例如：Jira）、中心依赖项管理系统（例如：Apache Archiva）和构建自动化系统（例如：Apache Continuum）。

   通过此设置，您可以将应用程序（内容、代码、配置）完全集成到任何开发环境和流程中。不同元素之间的链接是通过FileVault表示存储库的文件系统，因为上述所有开发工具都可以处理文件。

## 集成开发环境的扩展 {#extensions-for-integrated-development-environments}

Adobe发布了以下扩展：

* [AEM Eclipse扩展](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets扩展](/help/sites-developing/aem-brackets.md)

### 其他工具 {#other-tools}

AEM附带了其他有助于开发的工具：

* [对话框编辑器](/help/sites-developing/dialog-editor.md)
* [使用Translator管理词典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse开发AEM项目](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA开发AEM项目](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用代理服务器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 现代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo 工具](/help/sites-developing/aem-repo-tool.md)

有助于创建新项目的工具：

* [AEM 项目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybone模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>以下教程可能对启动新的AEM项目有帮助：
>[AEM Sites快速入门第1部分 — 项目设置](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
