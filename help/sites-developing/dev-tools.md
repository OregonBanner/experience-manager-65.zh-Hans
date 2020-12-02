---
title: 开发工具
seo-title: 开发工具
description: 要开发JCR、Apache Sling或AEM应用程序，可使用许多工具集
seo-description: 要开发JCR、Apache Sling或AEM应用程序，可使用许多工具集
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 2%

---


# 开发工具{#development-tools}

要开发JCR、Apache Sling或AEM应用程序，可使用以下工具集：

* 一组由[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)和WebDAV组成。 CRXDE Lite已嵌入到CRX/AEM中，使您能够在浏览器中执行标准开发任务。 利用CRXDE Lite，您可以在记录和集成SVN时创建和编辑文件（如。jsp和。java）、文件夹、模板、组件、对话框、节点、属性和捆绑包。

   当您无法直接访问CRX/AEM服务器，通过扩展或修改现成组件和Java包开发应用程序时，或者您不需要专用调试器、代码完成和语法突出显示时，建议使用CRXDE Lite。

* 一组由集成开发环境组成(例如：[Eclipse](/help/sites-developing/howto-projects-eclipse.md)或[IntelliJ](/help/sites-developing/ht-intellij.md))，一种构建工具(例如：[Apache Maven](/help/sites-developing/ht-projects-maven.md))、由Adobe开发以将存储库映射到文件系统的FileVault、版本控制系统(例如：Subversion)，一个错误跟踪器系统(例如：Jira)，一个中央依赖管理系统(例如：Apache Archiva)和构建自动化系统(例如：Apache Continuum)。

   此设置允许您将应用程序（内容、代码、配置）完全集成到任何开发环境和进程中。不同元素之间的链接是通过FileVault表示存储库的文件系统，因为上述所有开发工具都可以处理文件。

## 集成开发环境的扩展{#extensions-for-integrated-development-environments}

Adobe发布了以下扩展：

* [AEM Eclipse扩展](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets扩展](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ Extension](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) （来自Headwire）

### 其他工具{#other-tools}

AEM附带其他有助于开发的工具：

* [对话框编辑器](/help/sites-developing/dialog-editor.md)
* [使用翻译器管理字典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse开发AEM项目](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA开发AEM项目](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用代理服务器工具](/help/sites-developing/ht-proxy-server.md)
* [对话框转换工具](/help/sites-developing/dialog-conversion.md)
* [AEM Repo工具](/help/sites-developing/aem-repo-tool.md)

用于促进新项目创建的工具：

* [AEM 项目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>以下教程可能对启动新的AEM项目很有兴趣：
>[AEM Sites第1部分入门——项目设置](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

