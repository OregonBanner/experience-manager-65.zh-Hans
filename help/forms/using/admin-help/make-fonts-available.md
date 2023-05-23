---
title: 讓字型可供使用
seo-title: Make fonts available
description: 確保表單內使用的字型可用於託管AEM表單的J2EE應用程式伺服器。
seo-description: Ensure that the fonts used within a form are available for use on the J2EE application server hosting AEM forms.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 讓字型可供使用 {#make-fonts-available}

確保表單內使用的字型可用於託管AEM表單的J2EE應用程式伺服器。 例如，請考量下列情況。 表單設計工具會將字型新增至Designer使用的字型目錄，並在個別電腦上建立使用該字型的表單。 為了讓Output服務使用字型，請將其放在Customer fonts目錄中。 如果Customer fonts目錄不存在，請在裝載AEM表單的J2EE應用程式伺服器上建立目錄。

如需其他字型設定的詳細資訊，請參閱 [設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**指定客戶字型目錄的位置**

1. 在管理控制檯中，按一下設定>核心系統設定>設定。
1. 在「System Fonts目錄的位置」方塊中，輸入Customer Fonts目錄的路徑。 可以新增多個目錄，以分號分隔 **；**
1. 单击确定。
1. 重新啟動安裝AEM表單的系統。

>[!NOTE]
>
>從Windows系統字型快取中挑選字型，需要重新啟動系統才能更新快取。 指定Customer font目錄後，請確定重新啟動安裝AEM表單的系統。
