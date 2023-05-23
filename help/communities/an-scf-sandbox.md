---
title: 建立SCF沙箱
seo-title: Create An SCF Sandbox
description: 本教學課程主要供初次接觸AEM且有興趣使用SCF元件的開發人員使用。  它會逐步建立SCF沙箱網站
seo-description: This tutorial is primarily for developers, new to AEM, who are interested in using SCF components.  It walks through the creation of An SCF Sandbox site
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# 建立SCF沙箱  {#create-an-scf-sandbox}


自AEM 6.1社群起，快速建立沙箱最簡單的方式就是建立社群網站。 另請參閱 [AEM Communities快速入門](getting-started.md).

另一個對開發人員有用的工具是 [社群元件指南](components-guide.md)，可讓您探索及快速建立Communities元件和功能的原型。

建立網站的練習有助於瞭解AEM網站的結構，其中可能包含Communities功能，同時也提供簡單頁面，讓您探索如何使用 [社交元件架構(SCF)](scf.md).

本教學課程主要供初次接觸AEM且有興趣使用SCF元件的開發人員使用。 它會逐步建立SCF沙箱網站，類似於的教學課程 [如何建立功能齊全的網際網路網站](../../help/sites-developing/website.md) 其著重於網站結構，例如導覽、標誌、搜尋、工具列和列出子頁面。

開發會在作者執行個體上進行，而實驗網站最適合在發佈執行個體上進行。

本教學課程中的步驟為：

* [設定網站結構](setup-website.md)
* [初始沙箱應用程式](initial-app.md)
* [初始沙箱內容](initial-content.md)
* [開發沙箱應用程式](develop-app.md)
* [新增Clientlibs](add-clientlibs.md)
* [開發沙箱內容](develop-content.md)

>[!CAUTION]
>
>本教學課程不會使用建立的功能來建立社群網站 [社群網站主控台](sites-console.md). 例如，本教學課程未說明如何設定登入、自我註冊、 [社交登入](social-login.md)、傳訊、設定檔等。
>
>如果偏好使用簡單的社群網站，請遵循 [建立範例頁面](create-sample-page.md) 教學課程。

## 前提条件 {#prerequisites}

本教學課程假設您已安裝一個AEM作者和一個AEM發佈執行個體，該執行個體具有 [最新版本](deploy-communities.md#latest-releases) 社群的。

以下是一些實用的連結，供不熟悉AEM平台的開發人員使用：

* [快速入門](../../help/sites-deploying/deploy.md#getting-started)：用於部署AEM執行個體。

   * [基本知識](../../help/sites-developing/the-basics.md)：適用於網站和功能的開發人員。
   * [作者的首要步驟](../../help/sites-authoring/first-steps.md)：用於編寫頁面內容。

## 使用CRXDE Lite開發環境 {#using-crxde-lite-development-environment}

AEM開發人員的大部分時間都花在 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 製作執行個體上的開發環境。 CRXDE Lite提供對CRX存放庫的較少限制存取。 傳統UI工具和觸控式UI主控台提供對CRX存放庫特定部分的更具結構化的存取。

以管理許可權登入後，有多種方式可存取CRXDE Lite：

1. 在全域導覽中選取導覽 **[!UICONTROL 「工具」>「CRXDE Lite」]**.

   ![crxde-lite](assets/tools-crxde.png)

2. 從 [傳統UI歡迎頁面](http://localhost:4502/welcome.html)，向下捲動並按一下 **[!UICONTROL CRXDE Lite]** 在右側面板中。

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. 直接瀏覽至 `CRXDE Lite`： `<server>:<port>/crx/de`

   例如，在本機作者執行個體上： [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

若要使用CRXDE Lite，您必須使用開發人員或管理員許可權登入。 對於預設的localhost執行個體，您可以透過以下方式登入：

* `username: admin`
* `password: admin`


**注意** 此登入將會逾時，您需要使用CRXDe Lite工具列右端的下拉式功能表，定期重新登入。

如果未登入，您將無法導覽JCR存放庫或執行任何編輯/儲存操作。

***如有疑問，請重新登入！***

![重新登入](assets/relogin.png)
