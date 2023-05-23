---
title: 应用 Dynamic Media 图像预设
description: 瞭解如何在Dynamic Media中套用影像預設集
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# 套用Dynamic Media影像預設集 {#applying-image-presets}

影像預設集可讓資產動態傳送不同大小、不同格式或動態產生之其他影像屬性的影像。 您可在匯出影像時選擇預設集。 預設集會根據管理員指定的規格重新格式化影像。

此外，您也可以選擇回應式影像預設集(由 **[!UICONTROL RESS]** 按鈕)。

本節說明如何使用影像預設集。 [管理員可以建立和設定影像預設集](managing-image-presets.md).

>[!NOTE]
>
>智慧型影像處理可搭配您現有的影像預設集運作，並在傳送的最後毫秒內運用智慧功能，根據瀏覽器或網路連線速度，進一步縮減影像檔案大小。 另請參閱 [智慧型影像](imaging-faq.md) 以取得詳細資訊。

您可以隨時將影像預設集套用至影像預覽。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，影像預設集僅支援影像資產。

**若要套用Dynamic Media影像預設集：**

1. 開啟資產，然後在左側邊欄中選取下拉式功能表，然後選取「 」 **[!UICONTROL 轉譯]**.

   >[!NOTE]
   >
   >* 靜態轉譯會顯示在窗格的上半部。 動態轉譯會顯示在下半部。 若僅限動態轉譯，您可以使用URL來顯示影像。 此 **[!UICONTROL URL]** 按鈕僅在您選取動態轉譯時顯示。 此 **[!UICONTROL RESS]** 按鈕僅在您選取回應式影像預設集時顯示。
   >
   >* 當您選取時，系統會顯示許多轉譯 **[!UICONTROL 轉譯]** 在資產的「詳細資訊」檢視中。 您可以增加可查看的预设数。另請參閱 [增加顯示的影像預設集數目](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 執行下列任一項作業：

   * 選取動態轉譯，以便預覽影像預設集。
   * 若要顯示快顯視窗，請選取 **[!UICONTROL URL]**， **[!UICONTROL 內嵌]**，或 **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >如果資產 *和* 影像預設集尚未發佈，因此 **[!UICONTROL URL]** 按鈕(或 **[!UICONTROL URL]** 和 **[!UICONTROL RESS]** 按鈕（如果適用）不可用。
   >
   >另請注意，影像預設集會自動發佈在Dynamic Media伺服器上。
