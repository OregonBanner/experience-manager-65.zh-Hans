---
title: 在We.Retail中嘗試可編輯的範本
seo-title: Trying out Editable Templates in We.Retail
description: 在We.Retail中嘗試可編輯的範本
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 9%

---

# 在We.Retail中嘗試可編輯的範本{#trying-out-editable-templates-in-we-retail}

使用可編輯的範本時，建立和維護範本不再是開發人員專屬的工作。 稱為範本作者的權力使用者型別，現在可以建立範本。 开发人员仍需要设置环境、创建客户端库和创建要使用的组件，但是，在这些基础知识到位后，模板作者就可以灵活地创建和配置模板，而无需开发项目。 

We.Retail中的所有頁面都是以可編輯的範本為基礎，讓非開發人員能夠調整及自訂範本。

## 正在試用 {#trying-it-out}

1. 編輯語言主分支的「裝置」頁面。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. 請注意，模式選擇器不再提供設計模式。 We.Retail的所有頁面都以可編輯的範本為基礎，若要變更可編輯範本的設計，必須在範本編輯器中編輯這些頁面。
1. 從 **頁面資訊** 功能表選取 **編輯範本**.
1. 您現在正在編輯主圖頁面範本。

   頁面的結構模式可讓您修改範本的結構。 例如，這包括配置容器中允許的元件。

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. 設定配置容器原則以定義容器中允許哪些元件。

   原則等同於設計組態。

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. 在配置容器的設計對話方塊中，您可以

   * 選取現有原則或建立容器的新原則
   * 選取容器中允許的元件
   * 定義將資產拖曳至容器時要置入的預設元件

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. 回到範本編輯器，您可以在版面配置容器中編輯文字元件的原則。

   這可讓您：

   * 選取現有原則或建立容器的新原則
   * 定義頁面作者使用此元件時可用的功能，例如

      * 允許的貼上來源
      * 格式選項
      * 允許的段落樣式
      * 允許的特殊字元

   許多以核心元件為基礎的元件，都允許透過可編輯的範本在元件層級設定選項，消除了開發人員自訂的需求。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 返回範本編輯器，您可以使用模式選取器變更為 **初始內容** 模式，定義頁面上所需的內容。

   **版面** 模式可在正常頁面上使用，以定義範本的版面。

## 更多信息 {#more-information}

如需進一步資訊，請參閱撰寫檔案 [建立頁面範本](/help/sites-authoring/templates.md) 或開發人員檔案頁面 [範本 — 可編輯](/help/sites-developing/page-templates-editable.md) 以取得可編輯範本的完整技術詳細資訊。

您可能也想要調查 [核心元件](/help/sites-developing/we-retail-core-components.md). 請參閱撰寫檔案 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 核心元件和開發人員檔案的功能概觀 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 以取得技術概覽。
