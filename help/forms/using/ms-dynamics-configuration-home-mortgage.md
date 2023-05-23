---
title: 設定Microsoft Dynamics 365，以用於We.Finance參考網站的住房抵押貸款工作流程
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: 瞭解如何透過最適化表單針對We.Finance參考網站的住房抵押貸款工作流程運用Microsoft® Dynamics 365服務
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 設定Microsoft Dynamics 365，以用於We.Finance參考網站的住房抵押貸款工作流程 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

瞭解如何透過最適化表單針對We.Finance參考網站的住房抵押貸款工作流程運用Microsoft® Dynamics 365服務

## 概述 {#overview}

Microsoft® Dynamics 365是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案來建立和管理客戶帳戶、聯絡人、銷售機會、機會和案例。

AEM Forms提供雲端服務，將Dynamics 365與整合 [Forms資料整合](/help/forms/using/data-integration.md) 模組。 您必須先設定Microsoft® Dynamics 365，以與We.Finance參考網站搭配使用，才能透過Microsoft® Dynamics案例使用Home Mortgage應用程式逐步說明。

## 前提条件 {#prerequisites}

開始設定和設定Dynamics 365之前，請確定您具備：

* AEM 6.3 Forms Service Pack 1及更新版本
* Microsoft® Dynamics 365帳戶
* 使用Microsoft® Azure Active Directory為Dynamics 365服務註冊的應用程式
* 註冊的應用程式的使用者端ID和使用者端密碼

## 將住房抵押貸款電腦連結至您的網站首頁 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在作者執行個體上，前往以下頁面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下捲動至「住房抵押貸款電腦」。
1. 反白顯示右側欄的（電腦）面板，然後點選以顯示快顯功能表。 在快顯功能表中，點選「設定」。 「編輯AEM Forms容器」對話方塊隨即顯示。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. 在「編輯AEM Forms容器」對話方塊中，瀏覽資產路徑並選取以下路徑的home-mortgage-calculator ，然後點選 **確認**：

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 點選 **完成**.
1. 發佈已編輯的頁面。

   >[!NOTE]
   >
   >計算器欄位與FDM的繫結是透過We.Finance參考站台套件預先設定。 若要檢視繫結，您可以在撰寫模式下開啟表單，並檢視欄位繫結參考。

1. 若要建立自訂實體來儲存房屋抵押貸款申請的申請人記錄，請將AEMFormsFSIRefsite_1_0.zip解決方案套件匯入您的Microsoft® Dynamics執行個體：

   1. 從下列位置下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 將解決方案套件匯入至Microsoft® Dynamics執行個體。 在您的Microsoft® Dynamics執行個體中，前往 **設定** > **解決方案** 然後點選 **匯入**.

1. 若要設定重新設定網站中使用的使用者聯絡詳細資訊，請將Sarah Rose Contact.CSV套件匯入您的Microsoft® Dynamics執行個體：

   1. 從下列位置下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 將套件匯入您的Microsoft® Dynamics執行個體。 在您的Microsoft® Dynamics執行個體中，前往 **銷售** > **連絡人** 然後點選 **匯入資料**.
