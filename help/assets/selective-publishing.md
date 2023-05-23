---
title: 使用 Dynamic Media 中的“选择性发布”功能
description: 您可以選擇在檔案夾層級向Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用管理出版物或快速發佈，而非僅能依賴在Dynamic Media執行個體使用相同資料夾設定的Dynamic Media設定。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 664e22cc4c6acd74f285a4ec1a0dbd7d301240b7
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 4%

---

# 在Dynamic Media中設定檔案夾層級的選擇性發佈 {#selective-publish-configure-folder}

您可以選擇在檔案夾層級向Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用 **[!UICONTROL 管理發布]** 或 **[!UICONTROL 快速發佈]** 不要僅依賴 **[!UICONTROL Dynamic Media設定]** 其設定是整個Dynamic Media執行個體中所有資料夾的全域設定。

例如，透過選擇性發佈，您可以處理尚未上線的產品資產。 在這種情況下，行銷團隊可以存取同步至Dynamic Media的智慧型裁切影像和動態轉譯。 他們可以建立促銷材料，而完全無須將這些資產發佈至Dynamic Media進行全球傳送。

>[!IMPORTANT]
>
>選擇性發佈僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>*複製* 來往資料夾的資產會清除這些資產的發佈狀態。 然而，當您 *移動* 資料夾屬性設為「 」的資料夾的來往資產 **[!UICONTROL 選擇性發佈]**，則會維護這些資產的發佈狀態。

如果您稍後決定變更 **[!UICONTROL 選擇性發佈]** 資料夾中的設定，則這些變更只會影響您從此時間點上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態將維持不變，直到您從以下任一位置手動變更資產為止 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理發布]** 對話方塊。

資料夾層級 **[!UICONTROL Dynamic Media發佈模式]** 選項一律預設為可在下列位置找到的值： **[!UICONTROL 發佈資產]** 在您的 **[!UICONTROL Dynamic Media設定]**. 不過，本主題中的下列步驟會向您說明如何在資料夾層級手動變更此預設值（如下列步驟所述），以覆寫 **[!UICONTROL Dynamic Media設定]** 值。

無論您是否仰賴下列其中一項：

* **[!UICONTROL 發佈資產]** 值設定於 **[!UICONTROL Dynamic Media設定]**.
* **[!UICONTROL Dynamic Media發佈模式]** 在資料夾層級屬性中設定的值。

您可以選擇 **[!UICONTROL 立即]**， **[!UICONTROL 啟動時]**，或 **[!UICONTROL 選擇性發佈]**. 例如，您可以設定 **[!UICONTROL 發佈資產]** 中的值 **[!UICONTROL Dynamic Media設定]** 至 **[!UICONTROL 啟動時]**，但設定 **[!UICONTROL Dynamic Media發佈]** 資料夾層級的模式值至 **[!UICONTROL 選擇性發佈]**，反之亦然。

在資料夾中設定選擇性發佈後，您可以執行下列任一項作業：

* [使用管理發布選擇性將資產發佈到Dynamic Media或Experience Manager](#selective-publish-manage-publication).
* [使用管理發布選擇性從Dynamic Media或Experience Manager取消發佈資產](#selective-unpublish-manage-publication).
* [使用快速發佈將資產發佈到Dynamic Media或Experience Manager](#quick-publish-aem-dm).
* [透過搜尋結果選擇性地發佈或取消發佈資產](#selective-publish-unpublish-search-results).

**若要在Dynamic Media中設定檔案夾層級的選擇性發佈：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「 」 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 执行下列操作之一：
   * 編輯現有資料夾的屬性 — 在 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，導覽至您要編輯其屬性的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 屬性]**.
   * 編輯新資料夾的屬性 — 在 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，在頁面的右上角附近，選取 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**. 在 **[!UICONTROL 建立資料夾]** 對話方塊中，輸入資料夾的標題（必要），然後選取 **[!UICONTROL 建立]**. 選取資料夾，然後在工具列上選取 **[!UICONTROL 屬性]**.

1. 在 **[!UICONTROL 同步模式]** 從下拉式清單中選取下列其中一項：

   | 同步模式 | 描述 |
   | --- | --- |
   | **[!UICONTROL 已继承]** | 資料夾上沒有明確的同步值；而是會繼承其父資料夾之一的同步值，或是中設定的預設模式。 **[!UICONTROL Dynamic Media設定]**. 的詳細狀態 **[!UICONTROL 已繼承]** 以工具提示的方式顯示。 |
   | **[!UICONTROL 將此資料夾子樹狀結構中的所有專案同步至Dynamic Media]** | 若要成功發佈至Dynamic Media，資產必須同步至Dynamic Media。 選取此選項會包含此子樹狀結構中要同步至Dynamic Media的所有資產。 檔案夾特定設定會覆寫中的預設設定。 **[!UICONTROL Dynamic Media設定]**. |
   | **[!UICONTROL 從Dynamic Media同步處理中排除此資料夾子樹狀結構中的所有專案]** | 排除此子樹狀結構中的所有資產，使其無法同步至Dynamic Media。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在 **[!UICONTROL Dynamic Media發佈模式]** 從下拉式清單中選取一個選項。 此 **[!UICONTROL Dynamic Media發佈模式]** 選項一律預設為在中設定的值 **[!UICONTROL Dynamic Media設定]**. 不過，您可以手動覆寫此預設值 **[!UICONTROL Dynamic Media設定]** 使用下列其中一個選項來獲得value。

   >[!IMPORTANT]
   >
   >無論您選取的Dynamic Media發佈模式選項為何，之後對資產進行的任何更新都會是 *已經* 發佈後，這些更新會立即發佈，使用者毋須採取任何進一步動作。
   >
   >如果發佈的視訊已更新，則必須再次發佈以反映傳送上的變更。

   | Dynamic Media發佈模式選項 | 描述 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 將資產上傳至此資料夾時，系統會將資產擷取至Experience Manager，並立即提供URL/內嵌。 此選項僅與Experience Manager發佈繫結，使用者無需干預即可發佈資產。<br>此選項為 *not* 若您選取，則可用 **[!UICONTROL 從Dynamic Media同步處理中排除此資料夾子樹狀結構中的所有專案]** 在 **[!UICONTROL 同步模式]** 在上一步中。 |
   | **[!UICONTROL 激活后]** | 將資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅與Experience Manager發佈繫結。<br>此選項為 *not* 若您選取，則可用 **[!UICONTROL 從Dynamic Media同步處理中排除此資料夾子樹狀結構中的所有專案]** 在 **[!UICONTROL 同步模式]** 在上一步中。 |
   | **[!UICONTROL 选择性发布]** | 資產會發佈至您選擇的Experience Manager或Dynamic Media，以便在公共網域中傳送。 這兩種發佈方法彼此互斥。 也就是說，您可以將資產發佈至DMS7，以使用智慧型裁切或動態轉譯等功能。 或者，您也可以將資產獨家發佈到Experience Manager以進行安全預覽；這些相同的資產為 *not* 發佈至DMS7以在公共網域中傳送。 如果您選取「 」，則無法使用此選項 **[!UICONTROL 從Dynamic Media同步處理中排除此資料夾子樹狀結構中的所有專案]** 在 **[!UICONTROL 同步模式]** 在上一步中。 |

1. 在頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**，然後選取 **[!UICONTROL 確定]** 以返回Experience Manager Assets。

## 使用管理發布選擇性將資產發佈到Dynamic Media或Experience Manager{#selective-publish-manage-publication}

在您使用之前 **[!UICONTROL 管理發布]** 若要選擇性地將資產發佈至Dynamic Media或Experience Manager，請確定您已設定下列其中一項：

* 此 **[!UICONTROL 發佈資產]** 中的選項 **[!UICONTROL Dynamic Media設定]** 至 **[!UICONTROL 選擇性發佈]**
* 已在資料夾層級設定選擇性發佈。

另請參閱 [建立Dynamic Media設定](#configuring-dynamic-media-cloud-services) 或 [在Dynamic Media中設定檔案夾層級的選擇性發佈](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>選擇性發佈僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>*複製* 來往資料夾的資產會清除這些資產的發佈狀態。 然而，當您 *移動* 資料夾屬性設為「 」的資料夾的來往資產 **[!UICONTROL 選擇性發佈]**，則會維護這些資產的發佈狀態。

**若要使用「管理發布」將資產選擇性發佈到Dynamic Media或Experience Manager：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「 」 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，請執行下列任一項作業：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 管理發布]**. 使用 **[!UICONTROL 清單檢視]** 以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取 **[!UICONTROL 管理發布]**. 使用 **[!UICONTROL 清單檢視]** 以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >若 **[!UICONTROL 管理發布]** 工具列上看不到，請改為選取省略符號按鈕，然後選取 **[!UICONTROL 管理發布]** 從清單功能表。

1. 在 **[!UICONTROL 管理發布 — 選項]** 頁面，底下 **[!UICONTROL 動作]**，選取您想要的啟動型別。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 發佈]** (至Experience Manager) | 選取此選項，您就可以將資產發佈到Experience Manager以進行安全預覽。 |
   | **[!UICONTROL 发布到 Dynamic Media]** | 選取此選項，您就可以將資產發佈到Dynamic Media以在公共網域中傳送，或者也可以使用智慧型裁切或動態轉譯等功能。<br>此選項僅在以下情況下可用： **[!UICONTROL Dynamic Media發佈模式]** 設為 **[!UICONTROL 選擇性發佈]** 在資料夾的屬性中。 |

1. 下 **[!UICONTROL 排程]**，設定發佈時間。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍后]** | 選取此選項可在特定日期和時間發佈資產。 |

1. 在的右上角 **[!UICONTROL 管理發布]** 頁面，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 管理發布 — 範圍]** 頁面，執行下列任一項作業：

   * 如有必要，請選取一或多個要從發佈中移除的資產。
   * 在的右上角 **[!UICONTROL 管理發布 — 範圍]** 頁面，選取 **[!UICONTROL 發佈]** 或 **[!UICONTROL 發佈至Dynamic Media]**.
1. 選取 **[!UICONTROL 確定]**.

### 使用管理發布選擇性從Dynamic Media或Experience Manager取消發佈資產 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「 」 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，請執行下列任一項作業：
   * 導覽至您要取消發佈其資產的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 管理發布]**. 使用 **[!UICONTROL 清單檢視]** 以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要取消發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取 **[!UICONTROL 管理發布]**. 使用 **[!UICONTROL 清單檢視]** 以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >若 **[!UICONTROL 管理發布]** 工具列上看不到，請改為選取省略符號按鈕，然後選取 **[!UICONTROL 管理發布]** 從清單功能表。

1. 在 **[!UICONTROL 管理發布 — 選項]** 頁面，底下 **[!UICONTROL 動作]**，選取您想要的停用型別。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (從Experience Manager) | 如果要從Experience Manager取消發佈資產，請選取此選項。 |
   | **[!UICONTROL 从 Dynamic Media 取消发布]** | 如果要從Dynamic Media取消發佈資產，請選取此選項。<br>此選項僅在以下情況下可用： **[!UICONTROL Dynamic Media發佈模式]** 設為 **[!UICONTROL 選擇性發佈]** 在資料夾的屬性中。 |

1. 下 **[!UICONTROL 排程]**，設定停用的時間。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍后]** | 選取此選項可在特定日期和時間取消發佈資產。 |

1. 在的右上角 **[!UICONTROL 管理發布]** 頁面，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 管理發布 — 範圍]** 頁面，執行下列任一項作業：
   * 選取一或多個要從取消發佈中移除的資產。
   * 在的右上角 **[!UICONTROL 管理發布 — 範圍]** 頁面，選取 **[!UICONTROL 取消發佈]** 或 **[!UICONTROL 從Dynamic Media取消發佈]**.
1. 選取 **[!UICONTROL 確定]**.

## 使用快速發佈將資產發佈到Dynamic Media或Experience Manager {#quick-publish-aem-dm}

您可以使用 **[!UICONTROL 快速發佈]** 用於簡單的資產啟用案例。 **[!UICONTROL 快速發佈]** 立即發佈選取的資產，使用者不再進行任何互動。 因為此動作，所有未發佈的參考也會自動發佈。

>[!NOTE]
>
>使用 **[!UICONTROL 快速發佈]** 若要將資產發佈至Dynamic Media或Experience Manager，請確定 **[!UICONTROL 選擇性發佈]** 已在以下任一位置啟用： **[!UICONTROL Dynamic Media設定]** 或在所選資料夾的資料夾屬性中。

**若要使用「快速發佈」將資產發佈到Dynamic Media或Experience Manager：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後在頁面右側選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，請執行下列任一項作業：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 快速發佈]**. 使用 **[!UICONTROL 清單檢視]** 以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取 **[!UICONTROL 快速發佈]**. 使用 **[!UICONTROL 清單檢視]** 以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >若 **[!UICONTROL 快速發佈]** 工具列上看不到，請改為選取省略符號按鈕，然後選取 **[!UICONTROL 快速發佈]** 從清單功能表。

      ![資料夾層級快速發佈至Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從下列選項中選取一個： **[!UICONTROL 快速發佈]** 功能表清單。

   | 快速發佈選項 | 作用 |
   | --- | --- | 
   | 發佈至Experience Manager | 立即發佈選取的資產以Experience Manager。 |
   | 发布至 Brand Portal | 立即將選取的資產發佈至 **[!UICONTROL Brand Portal]**.<br>只有在您的Experience Manager Assets執行個體具備以下條件時，才能使用此選項 **[!UICONTROL Brand Portal]** 已設定。 |
   | 发布到 Dynamic Media | 立即將選取的資產發佈至Dynamic Media。<br>資產必須同步至Dynamic Media。 如有必要，請確定 **[!UICONTROL 同步模式]** 在資料夾中，屬性已設為 **[!UICONTROL 將此資料夾子樹狀結構中的所有專案同步至Dynamic Media]**. |

1. 選取 **[!UICONTROL 確定]**，然後選取 **[!UICONTROL 關閉]**.

## 透過搜尋結果選擇性地發佈或取消發佈資產 {#selective-publish-unpublish-search-results}

搜尋結果會顯示不同Dynamic Media發佈設定的資產資料夾中的資產。 從搜尋結果中選取多個資產，且每個資產有不同的Dynamic Media發佈模式設定時，您可以觸發 **[!UICONTROL 管理發布]** ，以發佈或取消發佈。

另請參閱 [搜尋Experience Manager中的資產](/help/assets/search-assets.md).

**若要透過搜尋結果選擇性地發佈或取消發佈資產：**

1. 在Experience Manager中，在頁面的左上角，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「 」 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在工具列上，在頁面的右上角附近，選取「搜尋」圖示（放大鏡）。
1. 在 **[!UICONTROL 輸入以搜尋]** 文字欄位，輸入關鍵字，然後按 **[!UICONTROL 輸入]**.
1. 在頁面的右上角附近，選取 **[!UICONTROL 清單檢視]** 圖示。
1. 在頁面的左上角附近，選取 **[!UICONTROL 篩選器]** 圖示。

   ![搜尋結果中的清單檢視和篩選器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開 **[!UICONTROL 狀態]**，然後展開 **[!UICONTROL Dynamic Media]** 搜尋述詞。
1. 使用 **[!UICONTROL 已發佈]** 和 **[!UICONTROL 已取消發佈]** 核取方塊，以根據Dynamic Media資產的已發佈狀態進一步調整搜尋結果。
或者，您可以將這些核取方塊與 **[!UICONTROL 發佈]** 搜尋述詞以縮小搜尋結果 **[!UICONTROL 已發佈]** 和 **[!UICONTROL 已取消發佈]** Experience Manager資產。
1. 执行下列操作之一：
   * 選取一或多個要發佈或取消發佈的資產。
   * 在右上角附近 **[!UICONTROL 搜尋結果]** 頁面，選取 **[!UICONTROL 全選]**.
1. 在工具列上，選取 **[!UICONTROL 管理發布]**. 選取工具列上的省略符號圖示，以便您開啟 **[!UICONTROL 管理發布]**.
1. 於 **[!UICONTROL 管理發布 — 選項]** 頁面中，選取所需的動作。

   | 選取的動作 | Dynamic Media設定中的發佈資產設定 | 資產為 |
   | --- | --- | --- |
   | 发布 | 立即或啟動時 | 已發佈至Experience Manager和Dynamic Media。 |
   | 发布 | 选择性发布 | 僅發佈至Experience Manager。 |
   | 取消发布 | 立即或啟動時 | 已從Experience Manager和Dynamic Media取消發佈。 |
   | 取消发布 | 选择性发布 | 僅從Experience Manager取消發佈。 |
   | 发布到 Dynamic Media | 立即或啟動時 | 未發佈至Experience Manager或Dynamic Media，或兩者皆有。 |
   | 发布到 Dynamic Media | 选择性发布 | 僅發佈至Dynamic Media。 |
   | 从 Dynamic Media 取消发布 | 立即或啟動時 | 不會從Experience Manager或Dynamic Media取消發佈，或兩者同時取消發佈。 |
   | 从 Dynamic Media 取消发布 | 选择性发布 | 僅從Dynamic Media取消發佈。 |

1. 下 **[!UICONTROL 排程]**，設定停用的時間。

   | 選取的排程 | 發生什麼情況 |
   | --- | --- |
   | 现在 | 選取的動作會立即執行。 |
   | 稍后 | 選取的動作會在選取的特定日期和時間執行。 |

1. 在的右上角 **[!UICONTROL 管理發布 — 選項]** 頁面，選取 **[!UICONTROL 下一個]**.
1. （選用）在 **[!UICONTROL 管理發布 — 範圍]** 頁面，檢閱 **[!UICONTROL 發佈目標]** 欄中選取的資產。

   | Dynamic Media設定中的發佈資產設定 | 選取的動作 | 发布目标 |
   | --- | --- | --- |
   | 立即或 <br>啟動時 | 发布 | Experience Manager和Dynamic Media |
   | 立即或 <br>啟動時 | 发布到 Dynamic Media | 无 |
   | 选择性发布 | 发布 | Experience Manager |
   | 选择性发布 | 发布到 Dynamic Media | Dynamic Media |
   | 立即或 <br>啟動時 | 取消发布 | Experience Manager和Dynamic Media |
   | 立即或 <br>啟動時 | 从 Dynamic Media 取消发布 | 无 |
   | 选择性发布 | 取消发布 | Experience Manager |
   | 选择性发布 | 从 Dynamic Media 取消发布 | Dynamic Media |

1. 在 **[!UICONTROL 管理發布 — 範圍]** 頁面，執行下列任一項作業：
   * 選取一或多個要從發佈或取消發佈中移除的資產。
   * 在的右上角 **[!UICONTROL 管理發布 — 範圍]** 頁面，選取 **[!UICONTROL 發佈]** 或 **[!UICONTROL 取消發佈]** 以開始動作。
1. 選取 **[!UICONTROL 確定]**.

## 檢查資產的發佈狀態 {#check-publish-status-of-asset}

您可以使用 **[!UICONTROL 時間表]** 替換為 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]** 在Experience Manager中快速檢查資產的發佈狀態。

**若要檢查資產的發佈狀態：**

1. 在Experience Manager中，在頁面的左上角，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「 」 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**， **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]** (下面的熒幕擷圖顯示 **[!UICONTROL 清單檢視]**)，開啟包含您已發佈或取消發佈之資產的資料夾。
1. 選取資產，使其以核取記號顯示。 如需範例，請參閱下方的熒幕擷圖。
1. 在頁面的左上角附近，從下拉式選單中選取 **[!UICONTROL 時間表]**. 此 **[!UICONTROL 狀態]** 左側面板中的區域會顯示所選資產的發佈狀態。
當您使用 **[!UICONTROL 清單檢視]**，額外的欄 **[!UICONTROL Dynamic Media]** 發佈狀態隨即顯示。
   * 設定為同步至Dynamic Media的資料夾會顯示 **[!UICONTROL Dynamic Media]** 欄依預設。
   * 資料夾 *not* 設定為同步至Dynamic Media時，不會顯示Dynamic Media欄。
      ![清單檢視和時間表](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈 {#selective-publish-troubleshoot}

某個資產未同步至Dynamic Media，但已在其上觸發Dynamic Media發佈動作，會導致以下錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)
