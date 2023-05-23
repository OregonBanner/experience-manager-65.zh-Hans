---
title: 在指派任務步驟中使用自訂電子郵件範本
seo-title: Use custom email templates in an Assign Task step
description: 表單工作流程電子郵件通知的自訂電子郵件範本
seo-description: Custom email templates for forms workflow email notifications
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# 在指派任務步驟中使用自訂電子郵件範本{#use-custom-email-templates-in-an-assign-task-step}

您可以使用「指派任務」步驟來建立任務並指派給使用者或群組。 當任務指派給使用者或群組時，會傳送電子郵件通知給已定義的使用者或已定義群組的每個成員。 典型的電子郵件通知包含指派任務的連結以及與該任務相關的資訊。 下列影像顯示範例電子郵件通知：

![使用現成可用範本的電子郵件通知](do-not-localize/default_email_template_new.png)

您可以自訂外觀，並在電子郵件通知中使用自訂中繼資料。 AEM Forms提供立即可用的電子郵件通知範本。 您可以自訂現成可用的範本或從頭開始建立新範本。

電子郵件通知範本是根據 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email). 這些電子郵件會因應不同的電子郵件使用者端和熒幕大小。 此外，電子郵件的樣式會在範本中定義。

以下影像顯示自訂的電子郵件通知：

![使用自訂範本的電子郵件通知](do-not-localize/customized-email.png)

## 自訂現有範本 {#customize-the-existing-template}

AEM Forms提供立即可用的電子郵件通知範本。 範本提供指派任務的標題說明、到期日、優先順序、工作流程名稱和連結。 您可以自訂範本以變更外觀。 執行以下步驟來自訂範本：

1. 使用管理員帳戶登入CRXDE。

1. 導覽至/libs/fd/dashboard/templates/email。

1. 開啟htmlEmailTemplate.txt檔案。 它包含預設範本。

1. 將htmlEmailTemplate.txt檔案的內容取代為自訂內容。

   電子郵件通知範本是 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email). 您可以使用自訂程式碼取代現有的html程式碼，以變更範本的外觀。

1. 保存文件。現在，自訂範本已可供使用。

## 建立電子郵件範本 {#create-an-email-template}

AEM Forms提供立即可用的電子郵件通知範本。 範本提供指派任務的標題說明、到期日、優先順序、工作流程名稱和連結。 您也可以新增自訂電子郵件範本（您自己的範本）給指派任務步驟。 執行以下步驟以新增自訂電子郵件範本：

1. 使用管理員帳戶登入CRXDE。

1. 導覽至/libs/fd/dashboard/templates/email。

1. 建立.txt檔案。 例如，EmailOnTaskAssign.txt。

1. 將自訂HTML程式碼新增至檔案。

   電子郵件通知範本是 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email). 您可以將自訂HTML程式碼新增至檔案以建立新範本。

1. 保存文件。範本已準備好用於指派任務步驟。

## 在指派任務步驟中使用電子郵件範本 {#use-an-email-template-in-an-assign-task-step}

現成可用的指派工作步驟已設定為使用預設範本htmlEmailTemplate.txt。 您可以選擇使用自訂範本。 若要變更範本：

1. 開啟指派工作步驟。

1. 導覽至「受指派人>HTML電子郵件範本」。

1. 選取新建立的HTML電子郵件範本。

1. 单击确定。範本已變更。

電子郵件通知也會使用 [中繼資料](../../forms/using/use-metadata-in-email-notifications.md). 例如，到期日、優先順序、工作流程名稱等。 您也可以設定範本以使用 [自訂中繼資料](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
