---
title: 將AEM表單工作區與Microsoft Office SharePoint Server整合
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: 您可以整合AEM表單工作區與Microsoft Office SharePoint Server。
seo-description: You can integrate AEM forms workspace with Microsoft Office SharePoint Server.
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 將AEM表單工作區與Microsoft Office SharePoint Server整合{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- 要求**

**必備條件知識**
在您可以將AEM Forms工作區新增至SharePoint伺服器之前，您必須擁有具有適當許可權的存取SharePoint伺服器的許可權，而且您必須知道存取工作區的URL。 以下步驟假設您熟悉SharePoint Server。 如需SharePoint Server網頁元件的詳細資訊，請參閱Windows SharePoint Services網頁元件。

**使用者層級**
開始

您可以在AEM Forms Office SharePoint Server (例如，Microsoft Office SharePoint Server 2007)中將Microsoft Workspace用作Web元件。 使用者可以使用網頁瀏覽器連線至您的AEM Forms伺服器，以提供統一的體驗來存取SharePoint工作區。 在本文章中，您將瞭解在Microsoft Office SharePoint Server中將AEM Forms Workspace顯示為網頁元件的基本步驟。 您可以執行本文中所述的步驟，以提供統一的體驗，讓連線至您SharePoint伺服器的使用者可以從相同的連線埠存取AEM Forms工作區。

>[!NOTE]
>
>本文列出的步驟為特定的Microsoft SharePoint Server 2007。 您也可以使用其他支援的Microsoft SharePoint版本設定HTML工作區。

## 將AEM Forms工作區與Microsoft Office SharePoint Server 2007整合 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

執行以下步驟，將AEM Forms Workspace整合至網頁元件：

1. 在網頁瀏覽器中，導覽至SharePoint網站，例如 `https://[myMOSSserver]:44299/default.aspx` 位置 `[myMOSSserver]` 是Sharepoint伺服器的名稱或IP位址。

   >[!NOTE]
   >
   >44299是SharePoint伺服器的預設連線埠號碼。 連線埠號碼取決於您安裝的SharePoint Server。

1. 在網頁的右上角，按一下 **網站動作** 並選取 **編輯頁面**.
1. 按一下 **新增網頁元件** 按鈕。
1. 在「新增網頁元件 — 網頁」對話方塊的「雜項」下，選取 **頁面檢視器網頁元件** 然後按一下 **新增**.
1. 在「頁面檢視器網頁元件」方塊中，按一下 **編輯** 並選取 **修改共用的網頁元件**.

   >[!NOTE]
   >
   >「頁面檢視器Web元件」方塊會顯示在 **新增網頁元件** 您在步驟3中按下的按鈕，如下圖所示（圖1）：

   ![Microsoft Office SharePoint伺服器中的「頁面檢視器」網頁元件方塊。](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   圖1. - Microsoft Office SharePoint伺服器中的「頁面檢視器」網頁元件方塊。

1. 在「頁面檢視器」頁面上，執行下列工作：

   1. 在「連結」方塊中，輸入AEM Forms工作區的URL，例如 `https://[AEM_forms_Server]:8080/lc/ws` 位置 `[AEM_forms_Server]` 代表AEM表單伺服器的IP或名稱。
   1. 按一下 **外觀** 並修改高度、寬度和標題，以便檢視整個Workspace使用者介面。 例如，您可以將高度和寬度分別設定為6英吋和11英吋。
   1. 按一下 **測試連結**. 會出現一個新的Web瀏覽器視窗，其中顯示工作區。
   1. （可選）按一下 **版面** 並修改網頁元件中的工作區版面。
   1. （可選）按一下 **進階** 並修改其他設定，例如說明，以及工作區在網頁元件中是否可以最小化或關閉。

      按一下 **套用**.

1. 按一下 **退出編輯模式** 並確認您可以存取工作區。

完成上述步驟後，您的SharePoint網站外觀會類似於下圖（圖2）：

![AEM Forms工作區與Microsoft Office SharePoint Server整合](assets/aem-forms-workspace.jpg)

圖2 - AEM Forms工作區與Microsoft Office SharePoint Server整合
