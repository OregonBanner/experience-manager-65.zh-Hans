---
title: 設定重新導向頁面
seo-title: Configuring redirect page
description: 填寫最適化表單後，使用者會被重新導向至表單作者可在建立表單時設定的網頁。
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 設定重新導向頁面{#configuring-redirect-page}

表單作者可為每個表單設定一個頁面，表單使用者在提交表單後即重新導向至該頁面。

1. 在編輯模式中，選取元件，然後按一下 ![欄位層級](assets/field-level.png) > **最適化表單容器**，然後按一下 ![cmppr](assets/cmppr.png).

1. 在側邊欄中，按一下 **提交**.

1. 在「提交」區段的「感謝頁面」下提供重新導向頁面的URL。
1. 或者，您可以在「送出動作」下，針對「送出至REST端點」動作，設定要傳遞至重新導向頁面的引數。

![重新導向頁面設定](assets/thank-you-setting-1.png)

重新導向頁面設定

表單作者可以使用以下傳遞至感謝頁面的引數。 對於所有可用的提交動作， `status` 和 `owner` 引數已傳遞。 除了這兩個引數外，系統還會為下列提交動作傳遞其他引數：

* **存放區內容動作** （已棄用） ： `contentPath` — 傳遞提交的資料儲存於存放庫中的節點路徑。

* **儲存PDF動作** （已棄用） ： `contentPath` — 已提交的資料以及儲儲存存於儲存庫中PDF檔案之節點的路徑 — 會通過。

* **提交至Forms工作流程**：傳遞從表單工作流程傳回的輸出引數。

* **提交至REST端點**：傳遞為欄位內與引數對應新增的引數。 `status` 和 `owner` 此提交動作中未傳遞引數。 如需詳細資訊，請參閱 [設定提交至REST端點提交動作](../../forms/using/configuring-submit-actions.md).
