---
title: 對話方塊編輯器
seo-title: Dialog Editor
description: 對話方塊編輯器提供圖形介面，可輕鬆建立和編輯對話方塊和支架
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 對話方塊編輯器{#dialog-editor}

對話方塊編輯器提供圖形介面，可輕鬆建立和編輯對話方塊和支架。

若要檢視其運作方式，請前往「CRXDE Lite」，開啟瀏覽器樹狀結構以 `/libs/foundation/components/chart` 並連按兩下節點 `dialog`：

![chlimage_1-247](assets/chlimage_1-247.png)

對話方塊節點將會在 **對話方塊編輯器**：

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 使用者介面概觀 {#user-interface-overview}

對話方塊編輯器介面由四個窗格組成：

* 此 **浮動面板**，位於左上角。 此窗格包含可用於建立對話方塊的Widget，例如索引標籤面板、文字欄位、選取專案清單和按鈕。 您可以按一下所需的分隔線列，以展開浮動視窗中的不同類別。
* 此 **結構** 窗格，位於左下角。 此窗格顯示組成對話方塊定義的節點階層結構。 您可以透過在CRXDE Lite或CRX內容總管中展開對話方塊節點來檢視相同的結構。
* 此 **轉譯** 窗格，位於視窗中央。 此窗格顯示結構窗格中定義的對話方塊定義如何呈現為實際對話方塊。
* 此 **屬性** 窗格。 此窗格顯示結構窗格中目前反白顯示的節點屬性。

### 使用對話方塊編輯器 {#using-the-dialog-editor}

若要建立對話方塊，使用者會將元素從浮動視窗拖放到結構窗格，放置到對話方塊定義階層內的位置。

完成所需結構後，使用者按一下 **儲存**，位於轉譯器窗格頂端。

>[!CAUTION]
>
>請注意，對話方塊編輯器用於建立相對簡單的對話方塊，可能無法編輯更複雜的對話方塊定義。 在對話方塊編輯器不允許編輯對話方塊結構的情況下，必須透過直接編輯節點結構來手動建立和/或編輯對話方塊定義，例如，使用CRXDE Lite或CRX內容總管。

### 建立新對話方塊 {#creating-a-new-dialog}

若要建立新對話方塊，您必須選取所需元件，請按一下 **建立……** 然後 **建立對話方塊……**.

輸入必要的詳細資訊，然後按一下 **全部儲存**  — 現在您可以連按兩下對話方塊，以使用編輯器將其開啟。

### 使用支架的對話方塊編輯器 {#using-the-dialog-editor-for-scaffolds}

支架是包含表單的特殊頁面，可在一個步驟中填寫和提交。 這可讓您使用輸入的內容快速建立頁面。

組成支架的表單是由對話方塊定義所定義，就像一般的對話方塊，不過它以不同的形式出現在支架頁面上。 因為對話方塊定義是用來定義支架，所以可使用對話方塊編輯器來設計支架。 請注意，以這種方式使用對話方塊編輯器時，轉譯器窗格仍會以對話方塊的形式顯示對話方塊定義，而不是作為支架。

另請參閱 [支架](/help/sites-authoring/scaffolding.md) 有關使用對話方塊編輯器建立支架的詳細資訊。
