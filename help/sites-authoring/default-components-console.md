---
title: 组件控制台
seo-title: Components Console
description: 组件控制台
seo-description: null
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 54%

---

# 组件控制台{#components-console}

「元件」主控台可讓您瀏覽針對執行個體定義的所有元件，並檢視每個元件的關鍵資訊。

该控制台可从&#x200B;**工具** -> **常规** -> **组件**&#x200B;中访问。在控制台中，卡片视图和列表视图均可用。 由于组件没有树结构，因此列视图不可用。

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>「元件主控台」會顯示系統中的所有元件。 [组件浏览器](/help/sites-authoring/author-environment-tools.md#components-browser)显示可用于创作的组件，并隐藏任何以句点 (`.`) 开头的组件组。

## 搜索 {#searching}

通过&#x200B;**仅限内容**&#x200B;图标（左上方），您可以打开&#x200B;**搜索**&#x200B;面板以搜索和/或筛选组件：

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### 组件详细信息 {#component-details}

若要檢視特定元件的詳細資訊，請點選/按一下所需的資源。 三個索引標籤提供：

* **属性**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   在“属性”选项卡上，您可以：

   * 查看组件的常规属性。
   * 檢視 [圖示或縮寫已定義](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 用於元件。

      * 按一下圖示的來源會前往該元件。
   * 檢視 **資源型別** 和 **資源超級型別** （如果已定義）。

      * 按一下「資源超級型別」即可前往該元件。
   >[!NOTE]
   >
   >由于 `/apps` 在运行时不可编辑，因此组件控制台为只读。

* **策略**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **实时使用情况**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >由于为此视图收集的信息的性质所致，它可能需要一段时间才能进行整理/显示。

* **文档**

   如果開發人員已提供 [元件的檔案](/help/sites-developing/developing-components.md#documenting-your-component)，它會顯示在 **檔案** 標籤。 如果没有可用文档，则不会显示&#x200B;**文档**&#x200B;选项卡。

   ![chlimage_1-171](assets/chlimage_1-171.png)
