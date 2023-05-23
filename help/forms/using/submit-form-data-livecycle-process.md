---
title: 設定AEM Forms將表單資料提交至AEM Forms on JEE程式
seo-title: Configuring AEM Forms to submit form data to an AEM Forms on JEE process
description: AEM Forms可讓您將最適化表單與AEM Forms on JEE程式整合，以處理表單資料。
seo-description: AEM Forms allows you to integrate adaptive forms with AEM Forms on JEE processes for processing form data.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Admin
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 設定AEM Forms將表單資料提交至AEM Forms on JEE程式{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

調適型表單支援將資料提交至AEM Forms on JEE程式以供進一步處理。 它可讓您使用已提交表單中的可用資料觸發JEE上的AEM Forms程式。 執行以下步驟，讓您的AEM Forms執行個體能夠在JEE程式上向AEM Forms提交最適化表單：

## 設定您的AEM Forms伺服器 {#configure-your-aem-forms-server}

執行以下步驟，讓您的AEM表單伺服器將資料提交至JEE伺服器上的AEM Forms：

1. 前往AEM Web設定主控台，網址為https://[*主機*]：[*連線埠*]/system/console/configMgr。

1. 找到並按一下 **AdobeLiveCycle使用者端SDK設定** 元件。
1. 按一下以編輯JEE伺服器上AEM Forms的設定伺服器URL、使用者名稱和密碼。
1. 檢閱設定並按一下 **儲存**.

![AdobeLiveCycle使用者端SDK設定](assets/clientsdkconfiguration.jpg)

## 將資料與程式欄位對應 {#map-data-with-process-fields}

設定AEM Forms後，將提交表單中的資料XML和附件對應至AEM Forms on JEE程式中的欄位。 要执行此操作：

1. 在AEM Web設定主控台中，按一下以編輯 **指南LiveCycle處理定位器與呼叫器** 設定。
1. 指定下列引數：

   * **資料xml引數的名稱** （必要）：指定需要處理提交資料之AEM Forms on JEE程式的XML屬性檔案。 預設值為 **資料XML**.

   * **檔案附件引數的名稱** （選用）：指定AEM Forms on JEE程式需要處理的檔案物件清單。 預設值為 **fileAttachmentsList**.

1. 檢閱設定並按一下 **儲存**.

![指南LiveCycle處理定位器與呼叫器](assets/test3.jpg)

設定完成後，提交至Forms Workflow提交動作會列出JEE伺服器處理序（包含指定的資料xml引數）上的AEM Forms。
