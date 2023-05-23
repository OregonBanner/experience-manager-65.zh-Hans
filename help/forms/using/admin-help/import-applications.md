---
title: 匯入和管理應用程式
seo-title: Import and manage applications
description: 瞭解如何匯入和管理應用程式。
seo-description: Learn how to import and manage applications.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 匯入和管理應用程式{#import-and-manage-applications}

在AEM forms中， *應用計畫* 是用於儲存實施AEM表單解決方案所需資產的容器。 資產範例包括表單設計、表單片段、影像、程式、DDX檔案、表單參考線、HTML頁面和SWF檔案。 在專案的開發階段中，Workbench使用者可以直接從Workbench的「應用程式」檢視部署應用程式。 部署後，這些應用程式會顯示在管理主控台的「應用程式管理」頁面的「應用程式」標籤上。

當應用程式完成並準備好要部署到生產伺服器時，Workbench使用者會將應用程式封裝到 *AEM forms應用程式檔案* (.lca)。 然後，管理員會使用「應用程式管理」頁面上的「應用程式」頁簽，使用管理主控台匯入和建置應用程式檔案。

您也可以使用「應用程式管理」頁面上的「封存」標籤，匯入使用Workbench 8.x建立的LCA。

>[!NOTE]
>
>有一個已知問題，即未來版本的LCA檔案不一定能回溯相容。 雖然您可以從未來版本的AEM Forms （例如預覽版本）檢視和匯入LCA檔案，但這樣做不受支援，並可能導致異常行為。

使用「應用程式」頁標，匯入和管理在Workbench中建立的應用程式。 應用程式管理員也可以匯出應用程式的執行階段組態。 匯出執行階段設定後，您就不需要在啟動已部署的應用程式之前，手動重新設定生產環境中的設定。 執行階段組態檔包含：

* 服務組態設定
* 集區組態設定
* 端點組態設定
* 安全性設定檔

## 匯入應用程式或封存 {#import-an-application-or-archive}

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 按一下「匯入」。
1. 按一下「瀏覽」並選取要匯入的.lca檔案，然後按一下「預覽」。 「預覽應用程式」頁面會顯示有關應用程式的資訊。
1. （可選）若要檢視應用程式中包含的資產清單，請按一下檢視資產。
1. （選用）若要將資產部署到執行階段，請選取匯入完成時將資產部署到執行階段。 如果您未選取此選項，可以稍後部署資產。
1. 按一下「匯入」。 應用程式會顯示在「應用程式」標籤上。
1. 使用管理員認證登入CRX存放庫。
1. 導覽至content/dam/lcapplications

   >[!NOTE]
   >
   >匯入的應用程式會顯示在lcpapplications節點中。

1. 按一下其中一個匯入的應用程式。

   右側的「屬性」標籤會顯示所選CRX節點的屬性。

   此 **syncState** 屬性指出AEM表單伺服器與CRX存放庫之間資料同步的狀態。 匯入程式一開始，此狀態就會設為0 （零）。 此狀態表示資料目前未同步。 資料同步時，狀態會設為1。

## 部署應用程式 {#deploy-an-application}

您可以部署已匯入的應用程式，或是從Workbench匯入的Workbench使用者。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 選取您要部署的應用程式旁的核取方塊，然後按一下部署。
1. 在出現的確認對話方塊中，按一下「確定」。

## 取消部署應用程式 {#undeploy-an-application}

您可以從執行階段取消部署應用程式。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 選取您要取消部署的應用程式旁的核取方塊，然後按一下取消部署。
1. 在出現的確認對話方塊中，按一下「確定」。

## 從伺服器移除應用程式 {#remove-an-application-from-the-server}

從伺服器移除應用程式之前，請先解除部署應用程式。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 選取您要移除之應用程式旁的核取方塊，然後按一下移除。
1. 在出現的確認對話方塊中，按一下「確定」。

## 匯入應用程式的執行階段設定 {#import-an-application-s-runtime-configuration}

如果應用程式管理員匯出應用程式的執行階段組態，您可以將其匯入已部署的應用程式。 您可以使用管理主控台或透過指令碼LCA部署匯入它。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「匯入執行階段設定」。
1. 按一下「瀏覽」並選取包含執行階段組態的XML檔案。
1. 按一下「匯入」。

## 匯出應用程式的執行階段設定 {#export-an-application-s-runtime-configuration}

您可以匯出已部署應用程式的執行階段組態資訊。

1. 在Administration Console中，按一下「服務>應用程式和服務>應用程式管理」。
1. 按一下應用程式的名稱。
1. 按一下「匯出執行階段組態」(Export Runtime Config)並儲存產生的組態檔(XML)。

## AEM表單應用程式的指令碼部署 {#scripted-deployment-of-aem-forms-applications}

您也可以使用指令碼部署工具來部署應用程式檔案，包括指定下列設定的settings.xml檔案：

* 服務組態設定
* 集區組態設定
* 端點組態設定
* 安全性設定檔

透過指令碼部署，您不必在啟動部署的應用程式之前，手動重新配置生產環境中的設定。

1. 在命令提示字元中，瀏覽至 *[aem-forms根]*/sdk/misc/Foundation/ArchiveManagement。
1. 請檢閱ReadMe.txt檔案以取得更詳細的指示。
1. 手動修改scriptedDeploy.bat和sample-files/sample.xml檔案，如readme.txt檔案中所述。
1. 執行scriptedDeploy.bat檔案。 此動作會部署包含覆寫設定的AEM表單封存檔案。
