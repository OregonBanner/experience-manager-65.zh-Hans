---
title: 指定要嵌入的字型
seo-title: Specifying fonts to embed
description: 瞭解如何指定要嵌入的字型。
seo-description: Learn how to specify fonts to embed.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 指定要嵌入的字型 {#specifying-fonts-to-embed}

您可以指定哪些字型一律以Forms服務產生的表單內嵌或永不內嵌。 嵌入字型會增加表單的檔案大小。 內嵌使用者很少在其系統上使用的非尋常字型。 請勿嵌入通常已安裝的常見字型。

>[!NOTE]
>
>如果您已為Forms指定了自訂XCI檔案，則XCI檔案中的內嵌字型選項會覆寫這些設定。 (請參閱 [設定Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. 在管理控制檯中，按一下 **[!UICONTROL 服務> Forms]**.
1. 下 **[!UICONTROL 字型內嵌設定]**，在 **[!UICONTROL 永遠嵌入字型]** 方塊中，鍵入要嵌入表單的字型名稱，並以逗號分隔。 您指定的字型只有在用於表單時，才會內嵌在產生的表單中。 如果已在傳遞至服務的XCI檔案中開啟內嵌字型選項，則會忽略此設定，因為在這種情況下，PDF中使用的所有字型都會內嵌。
1. 在 **[!UICONTROL 從不嵌入字型]** 方塊中，輸入不要嵌入表單的字型名稱，以逗號分隔。 您指定的字型不會內嵌在PDF中，即使這些字型用於產生的PDF中亦然。 如果在傳遞給服務的XCI檔案中關閉了內嵌字型選項，則會忽略此設定，因為在這種情況下，PDF中使用的字型都不會內嵌。
1. 单击“**[!UICONTROL 保存]**”。
