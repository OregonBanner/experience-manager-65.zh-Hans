---
title: 主畫面
seo-title: Home screen
description: AEM Forms應用程式首頁畫面的元件說明
seo-description: Description of the components of the AEM Forms app Home screen
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 主畫面{#home-screen}

登入AEM Forms應用程式時，系統會將您重新導向至首頁畫面。

## 預設主畫面 {#default-home-screen}

根據預設，「首頁」畫面會顯示所有表單，包括起點和任務(如果連線的伺服器已啟用AEM Forms Workflow)，以及關聯的縮圖。 您可以在AEM Forms伺服器中指定縮圖。

下圖會以預設首頁畫面上的重要元件標註來註解。

![Forms應用程式首頁](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **功能表按鈕**：點選 **選單** 按鈕以導覽至「工作」、「Forms」、「寄件匣」和「設定」。 如果您的AEM Forms應用程式已連線至AEM Forms JEE伺服器，您會看到「工作」選項。 「任務」選項也會儲存從流程中的任務建立的草稿。 若為AEM Forms OSGi伺服器，任務選項會隱藏。 Outbox會先儲儲存存的表單和草稿，然後再與伺服器同步。 應用程式啟用時，「寄件匣」中所有儲存的表單和草稿都會上傳至AEM Forms伺服器 [與伺服器同步](../../forms/using/sync-app.md). 如需有關設定的詳細資訊，請參閱 [更新一般設定](../../forms/using/update-general-settings.md).
1. **任務或表單**：點選列出的任務或您要使用的表單。
1. **水準省略符號**：表示動作可供表單使用。 點選省略符號會顯示作者提供的動作和說明。 此 **刪除草稿** 和 **完成** 點選省略符號時會顯示選項。
1. **重新整理圖示**：點選重新整理圖示，以將您的應用程式與AEM Forms伺服器同步。

### 自訂首頁畫面 {#customizing-the-home-screen}

![常规设置](assets/gen-settings.png)

您可以從以下位置變更應用程式的預設Home畫面： **[一般設定](../../forms/using/update-general-settings.md)** 或來自應用程式的 **偏好設定** 索引標籤中的「HTML工作區」。

應用程式上對「首頁」畫面設定所做的變更，會為目前登入的使用者或目前行動裝置上的使用者影響「首頁」畫面。

不過，在HTML Workspace中所做的變更會影響所有登入AEM Forms伺服器的AEM Forms應用程式使用者。
