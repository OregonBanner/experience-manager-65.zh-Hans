---
title: 指定要嵌入的字型
seo-title: Specify fonts to embed
description: 瞭解如何指定要嵌入的字型。
seo-description: Learn how to specify fonts to embed.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 指定要嵌入的字型{#specify-fonts-to-embed}

您可以指定哪些字型永遠會嵌入或絕不會嵌入到輸出使用的表單中。 嵌入字型會增加表單的檔案大小。 嵌入使用者不太可能在其系統上擁有的異常字型，並且不要嵌入他們將會安裝的常見字型。

>[!NOTE]
>
>如果您已經為輸出指定了自訂XCI檔案，則XCI檔案中的內嵌字型選項會覆寫這些設定。 (請參閱 [指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. 在Administration Console中，按一下「服務>輸出」。
1. 在「字型內嵌設定」下的「一律內嵌字型」方塊中，鍵入要內嵌於表單的字型名稱（以逗號分隔）。 您指定的字型只有在用於表單時，才會內嵌在產生的表單中。 如果在傳遞給服務的XCI檔案中開啟了內嵌字型選項，則會忽略此設定。 在這種情況下，PDF中使用的所有字型一律會內嵌。
1. 在「永不嵌入字型」方塊中，輸入不要嵌入表單的字型名稱，並以逗號分隔。 您指定的字型不會內嵌在PDF中，即使這些字型用於產生的PDF中亦然。 如果在傳遞給服務的XCI檔案中關閉了內嵌字型選項，則會忽略此設定。 在這種情況下，PDF中使用的字型都不會嵌入。
1. 单击“保存”。
