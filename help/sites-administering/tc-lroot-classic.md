---
title: 使用Classic UI建立語言根
seo-title: Creating a Language Root Using the Classic UI
description: 瞭解如何使用Classic UI建立語言根。
seo-description: Learn how to create a language root using the Classic UI.
uuid: 62e40d39-2868-4d3d-9af7-c60a1a658be0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: b88edad4-2a2e-429b-86a2-cc68ba69697e
docset: aem65
feature: Language Copy
exl-id: 1ae21d80-0683-4ab9-afaa-4d733ff47720
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 使用Classic UI建立語言根{#creating-a-language-root-using-the-classic-ui}

下列程式會使用傳統UI建立網站的語言根。 如需詳細資訊，請參閱 [建立語言根目錄](/help/sites-administering/tc-prep.md#creating-a-language-root).

1. 在網站主控台中的網站樹狀結構中，選取網站的根頁面。 ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. 新增代表網站語言版本的子頁面：

   1. 按一下「新增>新增頁面」。
   1. 在對話方塊中，指定「標題」和「名稱」。 名稱格式必須是 `<language-code>` 或 `<language-code>_<country-code>`，例如en、en_US、en_us、en_GB、en_gb。

      * 支援的語言程式碼為ISO-639-1所定義的小寫雙字母程式碼
      * 支援的國家代碼是小寫或大寫、兩個字母的代碼，如ISO 3166所定義
   1. 選取範本，然後按一下「建立」。

   ![newpagefr](assets/newpagefr.png)

1. 在網站主控台中的網站樹狀結構中，選取網站的根頁面。
1. 在「工具」功能表中，選取「語言副本」。

   ![toolslanguagecopy](assets/toolslanguagecopy.png)

   「語言複製」對話方塊會顯示可用語言版本和網頁的矩陣。 語言欄中的x表示頁面可使用該語言。

   ![languagecopydialog](assets/languagecopydialog.png)

1. 若要將現有頁面或頁面樹狀結構複製到語言版本，請在語言欄中選取該頁面的儲存格。 按一下箭頭，然後選取要建立的複製型別。

   在下列範例中，裝置/太陽鏡/愛爾蘭版頁面正在複製到法文版。

   ![languagecopydilogdropdown](assets/languagecopydilogdropdown.png)

   | 語言副本型別 | 描述 |
   |---|---|
   | auto | 使用父頁面的行為 |
   | 忽略 | 不建立此頁面及其子頁面的復本 |
   | `<language>+` （例如French+） | 複製該語言的頁面及其所有子頁面 |
   | `<language>` （例如法文） | 僅複製該語言的頁面 |

1. 按一下「確定」關閉對話方塊。
1. 在下一個對話方塊中，按一下「是」以確認複製。
