---
title: 開發工具
seo-title: Development Tools
description: 若要開發您的JCR、Apache Sling或AEM應用程式，可使用許多工具集
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
ht-degree: 3%

---

# 開發工具{#development-tools}

若要開發您的JCR、Apache Sling或AEM應用程式，可使用下列工具集：

* 一組包含 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 和WebDAV。 CRXDE Lite內嵌於CRX/AEM中，可讓您在瀏覽器中執行標準開發工作。 透過CRXDE Lite，您可以在記錄並與SVN整合時建立和編輯檔案(如.jsp和.java)、資料夾、範本、元件、對話方塊、節點、屬性和組合。

   當您無法直接存取CRX/AEM伺服器、透過擴充或修改現成元件和Java套件組合來開發應用程式，或當您不需要專用的除錯程式、程式碼完成和語法醒目提示時，建議使用CRXDE Lite。

* 由整合式開發環境所組成的集合(例如： [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 或 [IntelliJ](/help/sites-developing/ht-intellij.md))，建置工具(例如： [Apache Maven](/help/sites-developing/ht-projects-maven.md))、Adobe開發的將存放庫對應至檔案系統的FileVault、版本控制系統（例如：Subversion）、錯誤追蹤器系統（例如：Jira）、中央相依性管理系統（例如：Apache Archiva）和組建自動化系統（例如：Apache Continuum）。

   此設定可讓您將應用程式（內容、程式碼、組態）完全整合到任何開發環境和程式中。不同元素之間的連結是透過FileVault表示存放庫的檔案系統，因為上述所有開發工具都可以處理檔案。

## 整合式開發環境的擴充功能 {#extensions-for-integrated-development-environments}

Adobe發行了下列擴充功能：

* [AEM Eclipse擴充功能](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets擴充功能](/help/sites-developing/aem-brackets.md)

### 其他工具 {#other-tools}

AEM隨附其他有助於開發的工具：

* [對話方塊編輯器](/help/sites-developing/dialog-editor.md)
* [使用翻譯工具管理字典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理套件](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse開發AEM專案](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA開發AEM專案](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用Proxy伺服器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 现代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo 工具](/help/sites-developing/aem-repo-tool.md)

有助於建立新專案的工具：

* [AEM 项目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones範本](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>下列教學課程可能會對開始新的AEM專案有所幫助：
>[AEM Sites快速入門。第1部分 — 專案設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
