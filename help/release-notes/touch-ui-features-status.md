---
title: 触屏 UI 功能状态
description: 特定版本注意事項 [!DNL Adobe Experience Manager] 觸控式UI。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 15%

---

# 触屏 UI 功能状态 {#touch-ui-feature-status}

AEM 6.4以後 [傳統UI已過時](../release-notes/deprecated-removed-features.md). Adobe將不會再對Classic UI進行增強，並且鼓勵使用者利用觸控式UI中提供的強大新功能。

從6.0版開始，AEM推出了稱為「觸控式UI」（簡稱為「觸控式UI」）的新使用者介面，此介面會與 [!DNL Adobe Experience Cloud] 以及整體Adobe使用者介面指南。 隨著功能接近同等，這已成為AEM中的標準UI，具有稱為「傳統UI」的舊式案頭導向介面。

雖然大部分的功能都存在於觸控式UI中，但有些功能尚不完整，而且會在未來版本中新增。

下列清單顯示AEM 6.5中實作之功能的目前狀態。

如需升級至AEM 6.5之客戶的建議，請參閱 [客戶適用的使用者介面建議](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>本頁僅說明與傳統UI的功能對等性。 Classic UI中未列出的觸控式UI中新增及特有功能。

>[!NOTE]
>
>此清單力求完整，但並非詳盡無遺。

## 图例 {#legend}

* **完成**：觸控式UI可完全使用此功能。
* **大部分**：此功能主要在觸控式UI中提供。
* **遺失**：觸控式UI中未出現此功能，必須使用傳統UI來執行此動作。
* **已取代**：功能已由運作方式不同的新實作所取代。
* **已移除**：觸控式UI中不再提供此功能，且不會予以取代。

## 功能狀態：網站管理員 {#feature-status-sites-admin}

這是傳統UI網站管理員(`/siteadmin`)在觸控式UI中具有和狀態(`/sites.html`)。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 瀏覽網站階層 | 完成 | AEM 6.4推出了 [內容樹狀檢視](/help/sites-authoring/basic-handling.md#content-tree). |
| 启动工作流 | 完成 |  |
| 建立新頁面 | 完成 |  |
| 建立新網站 | 完成 |  |
| 建立新的啟動 | 完成 |  |
| 建立新的即時副本 | 完成 |  |
| 创建文件夹 | 完成 |  |
| 顯示發佈狀態 | 完成 | 從AEM 6.5開始，工作流程狀態會顯示在清單檢視中。 |
| 搜索 | 完成 |  |
| 複製並貼上頁面（複製） | 完成 |  |
| 移動頁面 | 完成 |  |
| 發佈頁面 | 完成 |  |
| 沒有復寫許可權的發佈頁面 | 完成 |  |
| 稍后发布 | 完成 |  |
| 發佈樹狀結構 | 完成 |  |
| 取消發佈頁面 | 完成 |  |
| 取消發佈沒有復寫許可權的頁面 | 完成 |  |
| 稍后取消发布 | 完成 |  |
| 删除 | 完成 |  |
| 鎖定/解鎖 | 完成 |  |
| 檢視/編輯屬性 | 完成 |  |
| 設定頁面許可權 | 完成 |  |
| 版本記錄 | 完成 |  |
| 還原版本 | 完成 |  |
| 還原樹狀結構並還原已刪除的頁面 | 遺失 | 使用傳統UI。 |
| 顯示舊版本和目前版本之間的差異 | 完成 |  |
| 即時複製動作（轉出） | 完成 |  |
| 檢視語言副本 | 完成 |  |
| 查找并替换 | 遺失 | 使用傳統UI。 |
| 通知收件匣（JCR事件） | 遺失 | 使用傳統UI。 將取代為不同的實作。 |
| 引用 | 完成 | 顯示新增至AEM 6.5的傳入頁面連結。 |

## 功能狀態：頁面編輯器 {#feature-status-page-editor}

這是傳統UI頁面編輯器的功能清單(`/cf#`)在已啟用觸控功能(`/editor.html`)。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 編輯網頁 | 完成 |  |
| 編輯行動網頁 | 完成 |  |
| 編輯透過Design Importer匯入的內容 | 完成 |  |
| 編輯電子郵件 | 完成 |  |
| 編輯混合行動應用程式 | 完成 |  |
| 編輯Forms | 完成 |  |
| 編輯選件 | 完成 |  |
| 編輯工作流程模型 | 完成 |  |
| 模式：編輯和預覽 | 完成 |  |
| 回應式預覽 | 完成 |  |
| 模式：編輯設計 | 完成 |  |
| 模式：支架 | 完成 |  |
| 模式：即時副本狀態 | 完成 |  |
| 新增註解 | 完成 |  |
| 编辑属性 | 完成 |  |
| 轉出頁面 | 完成 |  |
| 開始和顯示工作流程 | 完成 |  |
| 工作流程封裝處理 | 大部分 | 完全可在觸控式UI中使用。 傳統UI中仍會顯示多個工作流程裝載。 |
| 鎖定/解鎖頁面 | 完成 |  |
| 发布页面 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 复制页面 | 已删除 | 使用網站管理員 [複製頁面](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| 移动页面 | 已删除 | 使用網站管理員 [移動頁面](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| 删除页面 | 已删除 | 使用網站管理員 [刪除頁面](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| 显示引用 | 已删除 | 使用網站管理員檢視 [詳細參考清單](/help/sites-authoring/author-environment-tools.md#references). |
| 审查日志 | 已删除 | 使用網站管理員和 [開啟活動邊欄](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| 创建版本 | 已删除 | 使用網站管理員 [建立新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| 恢复版本 | 已删除 | 使用網站管理員 [還原版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| 切換啟動 | 已删除 | 使用網站管理員 [在啟動之間切換](/help/sites-authoring/launches-promoting.md). |
| 翻譯頁面 | 已删除 | 使用網站管理員 [新增頁面至翻譯專案](/help/sites-administering/tc-manage.md). |
| 時間扭曲（選擇日期/時間，並依其外觀瀏覽網站） | 完成 |  |
| 設定許可權 | 完成 |  |
| Client Context UI | 已取代 | 使用 [ContextHub](/help/sites-authoring/ch-previewing.md) UI向下一個方向發展。 |
| 各種媒體型別的內容尋找器 | 完成 |  |
| 组件列表 | 完成 |  |
| 複製和貼上元件 | 完成 |  |
| 剪貼簿中的元件清單 | 遺失 |  |
| 还原/重做 | 完成 |  |
| 將內容拖曳至元件預留位置 | 完成 |  |
| 透過自動建立元件將內容直接拖曳至parsys預留位置 | 完成 |  |

## 功能狀態：文字、表格和影像編輯器 {#feature-status-text-table-and-image-editors}

這是傳統UI文字、表格和影像編輯器所具有的功能清單，以及觸控式UI中的狀態。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 富文本编辑器 | 完成 | 可在原位、對話方塊及全熒幕中使用。 |
| 啟用/停用RTE外掛程式 | 完成 | 可使用以下專案完成 [範本編輯器](/help/sites-authoring/templates.md). |
| 針對純文字使用RTE | 完成 |  |
| RTE外掛程式：連結和錨點 | 完成 |  |
| RTE外掛程式：字元對應 | 完成 |  |
| RTE外掛程式：複製/貼上 | 完成 |  |
| RTE外掛程式：從Microsoft Word貼上 | 完成 |  |
| RTE外掛程式：尋找和取代 | 完成 |  |
| RTE外掛程式：文字格式（粗體、...） | 完成 |  |
| RTE外掛程式：Sub和superscript | 完成 |  |
| RTE外掛程式：左右對齊 | 完成 |  |
| RTE外掛程式：清單（專案符號/數字） | 完成 |  |
| RTE外掛程式：段落格式 | 完成 |  |
| RTE外掛程式：文字樣式 | 完成 |  |
| RTE外掛程式：來源編輯器(編輯HTML) | 完成 | 僅適用於對話方塊和全熒幕。 |
| RTE外掛程式：拼字檢查 | 完成 |  |
| RTE外掛程式：表格（內嵌表格編輯器） | 完成 |  |
| RTE外掛程式：還原/重做 | 完成 |  |
| RTE外掛程式：允許內嵌影像 | 完成 |  |
| 表格編輯器 | 完成 | 可在原位、對話方塊及全熒幕中使用。 |
| 將影像拖曳至表格儲存格 | 完成 | 可內嵌使用 |
| 图像编辑器 | 完成 | 可在原位、對話方塊及全熒幕中使用。 |
| 啟用/停用IPE外掛程式 | 完成 | AEM 6.3在中引入了UI [範本編輯器](/help/sites-authoring/templates.md). |
| IPE外掛程式：裁切 | 完成 |  |
| IPE外掛程式：翻轉 | 完成 |  |
| IPE外掛程式：還原/重做 | 完成 |  |
| IPE外掛程式：影像地圖 | 完成 |  |
| IPE外掛程式：旋轉 | 完成 |  |
| IPE外掛程式：縮放 | 完成 |  |

## 功能狀態：工具 {#feature-status-tools}

這是傳統UI所擁有的各種工具清單，以及觸控式UI中的狀態。

| 专题 | 状态 | 注释 |
|--- |--- |--- |
| 任务管理 | 已取代 | 6.0推出專案與任務。 |
| 工作流程收件匣 | 完成 |  |
| 頁面範本設定的工作流程(`/etc/workflow/wcm/templates.html`) | 遺失 | 使用傳統UI。 |
| 標籤管理員UI | 完成 |  |
| MSM/Blueprint控制中心 | 完成 |  |
| Blueprint Manager UI | 完成 |  |
| 轉出設定UI | 遺失 | 使用傳統UI。 |
| 使用者、群組和許可權UI | 大部分完成 | 若要進行進階許可權編輯，請使用傳統UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 遺失 | 使用傳統UI。 |
| 外部链接检查程序 (`/etc/linkchecker.html`) | 遺失 | 使用傳統UI。 |
| 大量編輯器(`/etc/importers/bulkeditor.html`) | 遺失 | 使用傳統UI。 |
| 上傳縮圖以新增或覆寫縮圖 | 遺失 | 使用傳統UI。 |
