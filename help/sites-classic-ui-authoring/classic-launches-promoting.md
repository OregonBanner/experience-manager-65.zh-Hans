---
title: 提升启动项
description: 您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# 提升启动项{#promoting-launches}

您必須提升啟動頁面，才能在發佈前將內容移回來源（生產環境）。 提升啟動頁面時，來源頁面的對應頁面會取代為提升頁面的內容。 提升啟動頁面時，有以下選項可供使用：

* 僅提升目前頁面還是整個啟動。
* 是否要升級目前頁面的子頁面。
* 是提升完整啟動項，還是僅提升已變更的頁面。

## 提升啟動頁面 {#promoting-launch-pages}

若要提升頁面，請在編輯要提升的啟動頁面時，執行下列步驟：

1. 於 **頁面** 在Sidekick中按一下「 」 **提升啟動**.
1. 指定要提升的頁面：

   * （預設）若要僅提升目前頁面，請選取 **將頁面變更提升至生產版本**.
   * 若要同時提升目前頁面的子頁面，請選取 **包含子頁面**.
   * 若要提升啟動項中的所有頁面，請選取 **將完整啟動項提升至生產版本**.

1. 若要將生產頁面新增至工作流程封裝，請選取「 」 **新增至Workflow封裝** 然後選取workflow封裝。
1. 按一下 **提升**.

## 使用 AEM 工作流处理提升的页面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來大量處理提升的「啟動」頁面：

1. 建立工作流程封裝。
1. 作者提升Launch頁面時，會將頁面儲存在Workflow套件中。
1. 使用封裝作為裝載啟動工作流程模型。

若要在提升頁面時自動啟動工作流程， [設定工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) （針對套件節點）。

例如，您可以在作者提升啟動頁面時自動產生頁面啟用請求。 設定工作流程啟動器，以便在修改封裝節點時啟動「請求啟用」工作流程。

![chlimage_1-136](assets/chlimage_1-136.png)
