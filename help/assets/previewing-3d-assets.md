---
title: 预览 3D 资源
description: 瞭解如何以Experience Manager預覽3D資產。
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 8%

---

# 在Adobe Experience Manager中預覽3D資產 {#previewing-3d-assets-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | 本文 |

Experience Manager支援3D資產的上傳、傳送和互動式預覽，這是製作程式的一部分。

您可從Experience Manager的資產詳細資訊頁面使用互動式3D檢視器。 该查看器提供了各种控件，其中包括一组交互式相机控件，可让您对 3D 资产执行绕行、缩放和平移操作。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## 支援的Experience Manager3D預覽格式 {#supported-3d-previewing-assets}

互動式3D預覽支援下列檔案格式：

| 3D副檔名 | 檔案格式 | MIME型別 | 注释 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary |  |
| GLTF | 總帳傳輸格式 | model/gltf+json | 另請參閱 **注意** 下方的。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體光刻 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 僅支援內嵌；無法預覽。 |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | 僅支援內嵌；無法預覽。 |

>[!NOTE]
>
>如果材質未在gLTF模型的預覽中轉譯，請確定已在 `textures` 與模型位於相同根資料夾中的資料夾，類似於以下內容：

    資產（資料夾）
    model.gltf
    model.bin
    紋理（資料夾）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 在Experience Manager中預覽3D資產時的效能考量事項{#performance-3d-previewing-assets}

在資產詳細資料檢視頁面中開啟3D資產所需的時間取決於多種因素，例如頻寬、影像複雜性和伺服器延遲。

此外，使用者端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也是您以互動方式操作相機時也必須考量的重要因素。 功能相當強大、圖形功能良好的系統，可讓互動式3D觀賞體驗更順暢、更理想。

**若要以Experience Manager預覽3D資產：**

1. 請確定您已將3D資產上傳至Experience Manager。
另請參閱 [支援的3D預覽格式](#supported-3d-previewing-assets) 和 [上傳資產](/help/assets/manage-assets.md#uploading-assets).
1. 從Experience Manager，在 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.

   ![導覽頁面](/help/assets/assets-dm/navigation-assets.png)

1. 在頁面的右上角附近，從「檢視」下拉式清單中選取 **[!UICONTROL 卡片檢視]**，然後導覽至您要預覽的3D資產。

   ![3D卡片選取](/help/assets/assets-dm/3d-card-select.png)
   _在「卡片檢視」中，選取您要預覽之3D資產的卡片。_

1. 選取3D資產的卡片。

   ![互動式3D預覽](/help/assets/assets-dm/3d-preview.png)
   _在資產詳細資料檢視頁面中互動式預覽3D資產。_
1. 在3D資產的資產詳細資訊檢視頁面上，執行下列任一項作業：

   | 查看 | 描述 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 围绕 3D 场景和对象旋转视图。 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下滑鼠右鍵+拖曳。 | 兩指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的一點。 | 按兩下。 | 點兩下。 |
   | **重置** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以完整的方式顯示資產，並維持合理的檢視大小。 |  |  |
   | **全屏模式** | 若要進入全熒幕模式，請在頁面的右下角，選取「全熒幕」圖示。 |  |  |

1. 完成後，在頁面的右上角附近，選取 **[!UICONTROL 關閉]**.
