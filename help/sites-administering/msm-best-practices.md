---
title: MSM 最佳实践
description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，以協助啟動並執行AEM多網站管理員。
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 41%

---

# MSM 最佳实践{#msm-best-practices}

## 常规 {#general}

MSM 是用于自动化内容部署的可配置框架。实施通常涉及网站的主要部分，并且跨多个组织和地理区域。因此，强烈建议您像规划网站一样仔细规划 MSM 实施：

* 在开始实施之前，仔细&#x200B;**规划结构和内容流**。
* **將即時副本的數量維持在最小。** 處理即時副本是一項耗用大量資源的工作。 您的系統中存在的即時副本越多，會影響效能的程度就越高：從處理內部即時副本索引、透過即時副本作業（例如轉出）到UI作業（例如在「網站管理員參考」邊欄中顯示即時副本關係）。 最佳實務是建立網站或網站分支的即時副本，其中即時副本關係會繼承至網站或分支中的頁面。 當整個結構可成為即時副本時，請避免為網站或分支中的頁面建立個別即時副本。
* **进行所需数量的自定义，越少越好。** 雖然MSM支援高度自訂（例如轉出設定），但網站在效能、可靠性和可升級性方面的最佳作法通常是儘可能減少自訂。
* 尽早建立&#x200B;**治理**&#x200B;模型，并相应地培训用户以确保成功。從治理的角度來看，最佳實務是 **將本機內容製作者擁有的許可權降至最低** 來配置/連線內容給其他本機使用者及其各自的即時副本。 这是因为，不受控制的链式继承会大大增加 MSM 结构的复杂性并降低其性能和可靠性。

* 在針對您的結構、內容流程、自動化和控管制定計畫後 —  **建立原型並徹底測試您的系統**，然後再開始即時實作。
* 请记住，**Adobe 咨询和领先的系统集成商**&#x200B;在使用 MSM 规划和实施内容自动化方面拥有丰富的经验，他们可以帮助您启动 MSM 项目并完成整个实施。

>[!NOTE]
>
>有關使用MSM的更多資訊，請參閱知識庫文章：
>
>* [解决 MSM 问题和常见问题](troubleshoot-msm.md)
>


>[!NOTE]
>
>您也可以使用 [參照元件](/help/sites-authoring/default-components-foundation.md#reference) 重複使用單一頁面或段落。 但請記住：
>
>* MSM更為靈活，可讓您對同步的內容和時間進行細微控制。
>* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 現在建議使用，而不使用基礎元件。
>


## Live Copy 源和 Blueprint 配置 {#live-copy-sources-and-blueprint-configurations}

請記住，可使用以下任一方式建立即時副本 [一般頁面](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 或 [Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 二者都是有效的用例。

使用 Blueprint 配置的额外好处是：

* 允許作者使用 **轉出** blueprint上的選項 — 以（明確）推送修改至繼承自此blueprint的即時副本。
* 允許作者使用 **建立網站**；這可讓使用者輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關聯的即時副本定義預設轉出設定。

如果未參考Blueprint設定，則轉出只能從即時副本本身啟動，基本上是從來源提取內容。

使用即時副本建立新網站時，建立Blueprint設定以確保完整MSM功能集的可用性是有利的。

>[!NOTE]
>
>请注意，“权限”选项卡中的 CUG 无法从 Blueprint 转出到 Live Copy。请在配置 Live Copy 时对此进行规划。

## 组件和容器同步 {#components-and-container-synchronization}

通常，MSM 中关于组件同步的转出规则是：

* 组件转出时将与 Blueprint 中包含的任何资源同步。
* 容器仅同步当前资源。

这意味着组件将被视为聚合，并且在转出时，组件本身及其所有子组件都将替换为 Blueprint 中的组件。这意味着，如果本地将资源添加到此类组件中，它将在转出时移至 Blueprint 的内容中。

为了支持组件的嵌套，以便在转出中维护本地添加的组件，必须将组件声明为容器。例如，預設parsys會宣告為容器，以便支援本機新增的內容。

>[!NOTE]
>
>将属性 `cq:isContainer` 添加到组件中以将它指定为容器。

## 创建站点 {#create-site}

請注意，AEM有兩個主要方法可建立即時副本：

* 時間 [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   這可視為較通用的方法，可讓您從任何頁面建立即時副本。 即時副本的內容結構與來源完全相符。

* 時間 [建立網站](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   這是一種更專業的方法，主要用於建立具有多語言結構的網站。

建立網站時，請謹記以下一些考量事項：

* 要创建新站点，您需要 [Blueprint 配置](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)。
* 要允许选择在新站点中创建的语言路径，相应的语言根必须存在于 Blueprint（源）中。
* 一次a [新網站已建立為即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **建立**，則 **網站**)，此即時副本的前兩個層級為 *淺*. 页面的子级不属于实时关系，但如果找到与触发器匹配的实时关系，则转出仍会下降。

   這有助於避免：

   * 在Blueprint中手動新增語言（第一個層級以下）
   * 手動將內容直接新增至語言根下，
   * 不會導致在轉出時自動將此新內容傳送至即時副本。

## MSM 和多语言网站 {#msm-and-multilingual-websites}

MSM 可通过两种方式来帮助创建多语言网站：

* 建立語言主版時。

   * 虽然 MSM 本身&#x200B;**不提供内容翻译**，但它可以与第三方翻译连接器集成。请注意：

      * MSM可讓您在頁面和/或元件層級取消繼承。 這有助於防止在下一次轉出時覆寫已翻譯內容（來自即時副本，以及來自Blueprint的尚未翻譯內容）。
      * 一些第三方翻译连接器会自动实施对 MSM 继承的管理。

         请与您的翻译服务提供商联系以获取更多信息。

      * 创建并翻译语言母版的另一种方法是将语言副本与 AEM 的现成的翻译集成框架结合使用。

* 從語言主版轉出內容時。

   * 例如，從法語主版到國家/地區特定網站，例如法國/法語、加拿大/法語、瑞士/法語。

如需詳細資訊，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md) 和 [翻譯最佳實務](/help/sites-administering/tc-bp.md).

## 结构更改和转出 {#structure-changes-and-rollouts}

對Blueprint/來源樹狀結構中內容結構的修改會以不同方式反映在即時副本中。 这取决于修改类型：

* **建立** Blueprint中的新頁面將導致在使用標準轉出設定轉出後，在即時副本中建立對應的頁面。

* **正在刪除** 使用標準轉出設定進行轉出後，Blueprint中的頁面將導致對應的頁面從即時副本中刪除。

* **移動** Blueprint中的頁面將 **not** 使用標準轉出設定進行轉出後，會在即時副本中移動對應的頁面：

   * 此行为的原因是页面移动隐式包含页面删除。这可能会导致发布时出现意外行为，因为删除创作实例上的页面会自动停用发布实例上的相应内容。這也可能對相關專案（例如連結、書籤等）產生連鎖效應。
   * 個別即時副本頁面中的內容繼承會更新，以反映其來源在Blueprint中的新位置。
   * 若要完全實現從Blueprint到即時副本的頁面移動，請考慮以下最佳實務：

>[!NOTE]
>
>這僅適用於 [在轉出觸發時](/help/sites-administering/msm-sync.md#rollout-triggers).

* 建立自訂轉出設定：

   * 此新設定必須包含動作：

      `PageMoveAction`

      不要向此配置添加其他操作。

* 定位新設定：

   * 若要完全轉出頁面移動，同時在即時副本中的舊位置刪除個別頁面：

      * 将新创建的配置放置在标准转出配置的前面。

         標準轉出設定會負責刪除舊位置的頁面。
   * 若要轉出頁面移動，同時將個別頁面保留在即時副本中的舊位置（基本上是重複內容）：

      * 将新创建的配置放置在标准转出配置的后面。

         這將確保即時副本中不會刪除內容或從發佈中停用。


## 自定义转出 {#customizing-rollouts}

MSM 转出配置是高度自定义的。您应意识到，自动化转出可能会产生深远的影响。最佳做法是規劃 *非常* 之前請務必小心，例如：

* 自動化轉出；例如，使用 [onModify觸發程式](#onmodify)，
* 自訂 [節點型別/屬性](#node-types-properties)，
* 開始後續工作流程，
* 和/或啟用轉出中的內容。

### onModify {#onmodify}

在使用[转出触发器](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` 时，您应考虑：

* 使用 `onModify` 触发器自动化转出可能会对创作性能产生负面影响，因为它们会在每次修改页面后触发转出。**

* 转出结果可能与预期结果不同：

   * 您不能指定生成的修改事件的顺序。
   * 基于事件的架构不能保证传递给 Rollout Manager 的事件的顺序。

* 如果对同一资源进行并发更新，则使用此转出配置可能会导致发生提交冲突。

因此，建議您 *僅限* use `onModify` 如果自動轉出啟動的好處多於任何潛在的效能問題，則會觸發。

### 节点类型/属性 {#node-types-properties}

請記住：

* 除了自定义转出操作之外，MSM 还允许您自定义正在转出的节点属性。此 [MSM OSGi設定可讓您排除節點型別](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) 從來源複製到即時副本。

## 更多信息 {#further-information}

本頁及以下頁面涵蓋相關問題：

* [创建并同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
