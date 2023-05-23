---
title: 輸出服務概觀
seo-title: Overview of output service
description: 「輸出」可讓您將XML表單資料與「設計工具」中建立的表單設計合併，以建立各種格式的檔案輸出資料流。
seo-description: Output lets you merge XML form data with a form design created in Designer to create a document output stream in various formats.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 輸出服務概觀 {#overview-of-output-service}

「輸出」可讓您將XML表單資料與「設計工具」中建立的表單設計合併，以建立各種格式的檔案輸出資料流。 輸出資料流可以傳送到網路印表機、本機印表機或磁碟檔案

您可以使用管理主控台中的「輸出」頁面來管理「輸出」服務。 若未透過AEM Forms API指定對等設定，您設定的設定會在執行階段使用。 透過AEM Forms SDK完成的設定會覆寫使用管理主控台設定的設定。

如需Output服務的詳細資訊，請參閱 [服務參考](https://www.adobe.com/go/learn_aemforms_services_61).

在Administration Console的Output頁面上，您可以執行幾個工作：

* 指定國際化的字元集。 (請參閱 [變更字元集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* 指定URL、URI、XCI和檔案位置的絕對和相對路徑。 (請參閱 [指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* 設定快取大小和原則。 (請參閱 [指定快取模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 和 [正在設定快取設定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* 讓字型可用於應用程式伺服器。 (請參閱 [讓字型可供使用](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* 指定要嵌入的字型。 (請參閱 [指定要嵌入的字型](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* 指定XCI設定選項。 (請參閱 [指定XCI設定選項](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* 指定安全性設定。 (請參閱 [指定安全性設定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

變更設定後，按一下「儲存」以將其套用至「輸出」。 您不需要重新啟動伺服器即可讓變更生效，但在設定快取設定時，您可能需要重新啟動Output服務。
