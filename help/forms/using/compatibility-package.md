---
title: 相容性套件
seo-title: Compatibility Package
description: 在AEM Forms 6.5上安裝相容性套件可讓您使用AEM Forms 6.4及舊版的「通訊管理」資產，以及已棄用的調適型表單範本和頁面
seo-description: Installing the Compatibility package on AEM Forms 6.4 allows you to use the Correspondence Management assets from AEM Forms 6.4 and deprecated adaptive forms templates and pages
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 2%

---

# 相容性套件{#compatibility-package}

## 概述 {#overview}

在AEM Forms 6.5中，互動式通訊是建立客戶通訊的預設和建議方法。若要繼續使用AEM Forms 6.5中的字母，您必須安裝最新的 [AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

AEMFD相容性套件也可讓您 [在AEM Forms 6.5上使用AEM Forms 6.4、6.3和6.2的以下資產：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 檔案片段
* 书信
* 資料字典
* 最適化表單已棄用的範本和頁面

如需詳細資訊，請參閱 [透過安裝相容性套件，使資產與AEM Forms 6.5相容](../../forms/using/compatibility-package.md#assetsmadecompatible).

## 在AEM Forms 6.5中新增對AEM Forms 6.4、6.3和6.2資產的支援 {#add-support-for-aem-forms-and-assets-in-aem-forms}

執行升級後，請執行以下操作以安裝AEMFD相容性套件，並讓您的資產相容於6.5：

確定您擁有 [AEM相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 已預先安裝。

1. 安裝最新的6.5 [相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   如需上傳和安裝套件的詳細資訊，請參閱 [如何使用套件](/help/sites-administering/package-manager.md).

1. 在記錄穩定之後，請重新啟動伺服器。
1. 使用移轉公用程式，讓您的資產相容於6.5。

   如需詳細資訊，請參閱 [移轉公用程式](../../forms/using/migration-utility.md).

## 透過安裝相容性套件，使資產與AEM Forms 6.5相容 {#assetsmadecompatible}

透過安裝相容性套件，您可以使下列資產和範本與AEM Forms 6.5相容：

* 來自AEM 6.4和更早版本的通訊管理資產：

   * [书信](../../forms/using/create-letter.md)
   * [数据字典](/help/forms/using/data-dictionary.md)
   * 文档片段

* 最適化表單已棄用的範本：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 調適型表單已棄用頁面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
