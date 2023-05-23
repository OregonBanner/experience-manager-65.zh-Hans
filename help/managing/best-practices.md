---
title: 管理專案 — 最佳實務檢查清單
seo-title: Managing Projects - Best Practices Checklist
description: 管理專案以實作Adobe Experience Manager (AEM)需要規劃和瞭解。 「專案檢查清單」旨在作為專案交付的一組最佳實務。 它們會引導您完成專案生命週期的所有階段，並提供您目前狀態的高層級監控。
seo-description: Managing a project to implement Adobe Experience Manager (AEM) requires planning and understanding. The Project Checklists are intended as a set of best practices for project delivery. They guide you through all phases of the project life cycle and provide high level monitoring of your current status.
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 1%

---

# 管理專案 — 最佳實務檢查清單{#managing-projects-best-practices-checklist}

管理專案以實作Adobe Experience Manager (AEM)需要規劃和瞭解，以確保您瞭解需要做出的問題和（相關）決策（在實施專案之前和期間）。

為協助您，最佳實務包括：

* 一個 [互動式檢查清單](/help/managing/best-practices-checklist.md) 可讓您透過這些最佳實務來追蹤及監控進度。

   * 根據階段、里程碑和角色定義輸入和交付專案。
   * 提供自動概述（品質、健全和完整性）以指出進度和專案健全性。

* 檔案，直接根據 [檢查清單](/help/managing/best-practices-checklist.md)，其中詳細說明：

   * [專案心率](#projectheartbeat) 分析。
   * [按角色顯示狀態](#status-by-role) 概述。
   * [階段和里程碑](#phases-and-milestones).
   * [關鍵角色](#persona) 以及參與每個（相關）階段。
   * A [字彙表](/help/managing/best-practices-glossary.md) 的 [必要檔案與交付專案](#required-documents-and-deliverables).

* [進一步參考資料](/help/managing/best-practices-further-reference.md) 素材，以提供特定區域的更多細節。

## 專案心率控制面板 {#project-heartbeat-dashboard}

此 **專案心率** 工作表提供專案重要度量的圖形化概要：

* **階段品質**

   * 指示的品質 [必要檔案與交付專案](#required-documents-and-deliverables) 整個專案。

* **階段健康狀態**

   * 專案的高層級狀態指標；用於強調可能有風險的區域。

* **階段完整性**

   * 在專案期間的任何時間點，這表示專案每個階段的已完成程度。

## 按角色顯示狀態 {#status-by-role}

此 **按角色顯示狀態** 工作表顯示下列專案的詳細劃分： [**健康狀況**， **品質** 和 **完整性**](#projectheartbeat) 作者： **[階段](#phases-and-milestones)** 和 **[角色](#persona)**.

## 階段和里程碑 {#phases-and-milestones}

專案計畫會劃分為不同（高階）階段。

每個階段都包含自己的里程碑。 針對每個 [角色](#persona) （或角色）時，會列出相關里程碑，以及產生已定義交付專案所需的檔案。

>[!NOTE]
>
>個別必要檔案和交付專案之間沒有直接的1:1關係。

### 準備 {#preparation}

專案的準備工作構成了整個專案的基礎。 您需要定義主要需求，並明確目標與期望：

* **業務理由**

   * 進行專案的基本理由和理由。

* **範圍和排程**

   * 應提供基本範圍和粗略排程，以定義所需的內容以及時間範圍；如果有助於釐清情況，您也可以定義範圍以外的內容。

您準備、規劃及執行專案以及實作解決方案的方式，將受您所操作的限制所影響，例如固定預算、固定時間表、內容數量、所需品質。

一如既往，調整任何因素都會影響其他因素。 例如，減少時間，但要求相同品質等級可能會提高價格，同時減少您可以滿足的內容數量。 預算通常是關鍵因素，因此這類關係無法忘記。

四個因素：

![projectphods_fourphods](assets/projectphases_fourphases.png)

#### 里程碑 {#milestones}

* **验证**

   在此階段中，您需要驗證並確認專案的目標；例如：

   * 您想要達成目標/提供什麼？
   * 誰會受益？
   * 範圍為何？

      * 如果這有助於釐清狀況，您也可以定義範圍以外的內容。
   * 如何定義成功？
   * 如何衡量成功？
   * 有哪些需求、業務與技術？
   * 是否有需要取代的舊系統，若是，是否有需要移轉的資料？
   * 誰會參與？
   * 您將如何測量進度？
   * 在專案生命週期中，您多久檢視一次進度？


* **預算**

   在開始任何專案之前，您需要對實作成本做出可靠且實際的估計：

   * 使用驗證里程碑的資訊作為估算的基礎。
   * 在估算時務實地考量。
   * 請考慮並遵守使用者端可能遵守的任何使用者端准則、程式或限制。
   * 如果稍後階段需要審查或調整預算，請考慮應急和審查程式。
   * 請記住，成本有多種形式；購買、使用資源和費用等等。

### 规划 {#planning}

計畫您的專案會整合準備工作。 在這裡，您需要開始將目標和期望轉換為由具體任務組成的定義明確的藍圖，並以明確的溝通和嚴格的評審來衡量進度。

#### 里程碑 {#milestones-1}

* **切換**

   乾淨的交接可確保適當的角色/群組瞭解其在專案中的職責。

   應提供/產生完整的詳細資訊，以確保他們完全瞭解所有相關方面，包括藍圖、範圍、目標、要求和KPI。

* **風險評估**

   為避免意外情況，請使用風險評估來識別和量化任何潛在風險及其影響和機率。

   這應在專案生命週期的初期完成，以確保識別並評估任何變數。 您可以根據調查結果，向利害關係人報告是否能夠實施完整需求，以及是否可能計畫要採取和追蹤的適當行動（如有必要）。

* **通訊**

   溝通永遠是任何專案成功的關鍵。 您需要清楚且有效率的溝通，以確保每個人：

   * 致力於相同的基本目標
   * 從相同的資訊庫
   * 使用相同的管道

* **開始**

   Kick Off會議是用來提高人們對專案已開始的認識。 這是您進行下列操作的良機：

   * 邀請所有感興趣的當事方（或至少是群組代表）。
   * 呈現專案的關鍵事實。
   * 回答問題。
   * 確保每個人都擁有相同的知識庫。
   * 獲得所有參與者的承諾 — 這必須贏得。

      * 若在專案開始時讓主要參與者（包括潛在作者）參與，您就有機會獲得他們對專案的承諾。

### 開發準備 {#development-preparation}

規劃開發是確保您的專案是由具備所需知識的團隊以可靠的設計為基礎而建置的關鍵。

#### 里程碑 {#milestones-2}

* **配備人員和訓練有素的開發團隊**

   在開始任何專案之前，您應該確保您的開發團隊已配備適當的人員，並且所有團隊成員都已接受手頭任務的培訓。

* **內容架構**

   內容架構會定義並描述內容的未來架構，包括：

   * 內容樹狀結構；包括資產
   * 基本結構；包括行銷活動等。
   * 多網站和多語言結構（MSM、翻譯等）
   * 支援內容（包括標籤和標籤概念）
   * 快取和內容重複使用策略

* **系統架構**

   系統架構會定義系統的概念檢視，包括（與其他資訊一起）：

   * [系統結構](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 適用於所有必要環境
   * 子系統
   * 協力廠商系統
   * 介面；硬體、軟體與人力互動
   * 每個環境的伺服器；請參閱 [技術需求](/help/sites-deploying/technical-requirements.md) 和 [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md)

   * 每個環境的程式；例如，部署和維護需求
   * 維護活動（Datastore GC、TarPM最佳化等）
   * [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 快取
   * [叢集](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 發佈/Authorshare
   * 使用者端的效能（JS精簡、concat、css指令集、http要求總數等）

* **應用程式架構**

   應用程式架構會定義並描述建議的應用程式行為。

   其重點為：

   * 他們如何彼此互動以及如何與使用者互動。
   * 由應用程式使用和產生的資料，而非其內部結構。

   定義應涵蓋：

   * 專案的基本程式碼結構
   * 程式碼成品（套件組合、套件等）
   * 範本/元件及其關係的劃分
   * 所需自訂的高層級詳細資料（稍後將會顯示特定覆蓋圖）
   * 設計解決方案所需的工作流程（例如內容建立、核准、發佈、轉換、匯入、匯出等）
   * 任何複雜模組（例如MSM、Commerce、協力廠商整合）的特殊考量


* **系統整合**

   系統整合需要您規劃（然後實作）：

   * 所有子系統和 [解決方案整合](/help/sites-administering/integration.md) 將彙集在一起，以一個連貫的系統運作
   * 如何整合任何協力廠商系統；以及任何特殊考量，例如離線/線上、使用者端/瀏覽器端，或在協力廠商系統故障時進行容錯移轉處理

* **測試概念**

   在開始開發之前，您應該起草一個深入且全面的「全部」概念 [測試](/help/sites-developing/planning.md) 您專案的要求。

   這應該包括（其中包括）：

   * 要執行之所有測試的詳細資訊
   * 準備這些測試所需的任何內容
   * 要使用的任何測試工具的資訊
   * 提供參與測試人員的詳細指示；尤其是QA團隊以外的群組
   * 測試自動化的詳細資訊；例如，使用Selenium或AEM開發人員模式

* **體驗設計**

   體驗設計(XD)涉及為解決方案設計使用者體驗。

   您應針對作者和網站的最終使用者來分析和開發使用者體驗。

* **支援設定**

   在開發之前，所有部署、發佈、測試和報告問題所需的支援流程都應設定就緒。

   另請參閱 [Adobe支援入口網站](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html).

### 作業計畫與作業 {#operations-planning-and-operations}

在類似的基礎上，必須正確規劃作業，以確保您擁有所需的環境 — 專案生命週期的所有階段。 您也需要適當的程式來進行維護。

#### 里程碑 {#milestones-3}

* **权限**

   您需要針對將使用該解決方案的所有使用者/群組規劃並實作角色和許可權概念。

   例如：

   * 具有下列專案的角色（即群組）清單 `read`/ `write` 每個的存取定義

   * 影響發佈環境的許可權使用的定義；例如， `replicate`
   * 對於具有最低許可權的使用者，應定義工作流程
   * 中的使用者 `editor` 群組不應有 `admin` 權利，也不屬於 `administrators` 群組

   如需詳細資訊，請參閱 [使用者管理與安全性](/help/sites-administering/security.md).

* **監控與維護**

   監控與維護是確保解決方案上線後順利運作的關鍵環節。 為此，您需要定義：

   * 需要監控的專案
   * 維護任務；包括一般和特殊情況

   另請參閱 [監控與維護](/help/sites-deploying/monitoring-and-maintaining.md) 以取得詳細資訊。

* **迁移**

   任何來自舊版系統的內容都應經過檢閱和驗證，以便進行移轉。

* **復原計畫**

   確保您有適當的復原計畫。 在緊急情況下，這必須可用，以確保AEM的生產使用。 這應該包括備份、還原、移轉和其他情況。

### 开发 {#development}

開發是關鍵階段，不僅需要程式碼。

#### 里程碑 {#milestones-4}

* **開發環境**

   規劃並記錄您的開發環境，包括：

   * 架构
   * [開發工具](/help/sites-developing/dev-tools.md)

      * 典型的環境包括：

         * 問題追蹤系統；例如Jira
         * IDE；例如Eclipse
         * 組建管理工具，例如Maven
         * 持續整合的工具；例如Jenkins
         * 版本控制工具；例如GIT/SVN
         * 組建成品存放庫管理員，例如Archiva/Nexus
   * 協力廠商軟體整合/相依性
   * [解決方案整合/相依性](/help/sites-administering/integration.md)
   * 部署節奏


* **測試系統**

   規劃並記錄您的測試環境，包括：

   * 架构
   * 對開發組建的相依性；包括夜間組建
   * 測試協力廠商軟體整合/相依性的可能性或限制
   * 測試工具
   * 自動化測試策略

* **Production System**

   規劃並記錄您的生產環境，包括：

   * 架构
   * 部署節奏
   * 協力廠商軟體整合/相依性
   * 安全性設定
   * 基準線效能已透過執行 [艱苦的日常測試](/help/sites-developing/tough-day.md) 在生產設定上
   * 效能測試的需求；請參閱 [品質保證的最佳實務](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **集成**

   規劃、記錄及測試系統的所有方面，以及 [解決方案整合](/help/sites-administering/integration.md)，包括：

   * 自動化測試策略
   * 將流程自動化至 [將應用程式從開發移至測試，然後移至生產](/help/managing/enterprise-devops.md#code-movement)
   * 將流程自動化至 [將內容從生產環境移至測試和開發環境](/help/managing/enterprise-devops.md#content-movement)

* **迁移**

   規劃、記錄及測試內容移轉的各個層面，包括：

   * 內容架構
   * 移轉策略

* **通訊**

   確保所有團隊成員和專案角色在必要時保持最新。

* **文档**

   完整記錄解決方案；包括：

   * 作業手冊
   * 可能影響升級的任何自訂
   * 发行说明

### 效能與測試 {#performance-and-testing}

新應用程式推出後，需要經過嚴格的功能與測試測試 [績效](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>任何測試團隊都應被允許保持中立並交付測試結果。
>
>專案經理有責任評估結果的任何影響，並決定適當的行動。

#### 里程碑 {#milestones-5}

* **使用者驗收測試**

   [使用者驗收測試](/help/sites-developing/acceptance-signoff.md) (UAT)對於確保：

   * 此解決方案符合使用者/客戶的需求
   * 客戶/使用者接受解決方案（功能、設計和效能）

   客戶移交時應有正式的核對清單；最好是自動化處理，每晚對照快照執行。 應將結果傳送給專案經理和開發團隊

* **效能和負載測試**

   使用效能和負載測試，以確保解決方案在平均和尖峰負載下符合所需的效能等級。

   如需效能測試的詳細資訊，請參閱：

   * [性能测试](/help/sites-deploying/configuring-performance.md)
   * [如何規劃及執行測試](/help/sites-developing/planning.md)

   * [基本效能准則](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >在正常使用AEM期間，此過程必須繼續，但這些初始階段是最關鍵的。

### 转出 {#rollout}

推出新應用程式需要謹慎規劃，以確保順利上線。 這包括確認高水準的安全性、培訓所有潛在的使用者，以及進行多次試用，以確認所有問題皆已解決。

#### 里程碑 {#milestones-6}

* **準備**

   準備和規劃將有助於確保順利推出。

* **培訓**

   確定所有相關人員都經過培訓。

   另請參閱 [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) 在課程目錄中。

* **已訓練的管理員**

   確保您的解決方案管理員具備：

   * 已訓練
   * 已收到適當的訓練資料
   * 已收到適當的檔案

* **已訓練的使用者**

   確保您的作者具備：

   * 已訓練
   * 已收到適當的訓練資料
   * 已收到適當的檔案；例如，使用手冊

* **滲透測試**

   滲透測試會模擬電腦系統上的攻擊，以找出潛在的安全性弱點。

* **滲透/安全性測試**

   為確保解決方案的安全性，請執行特定的滲透測試，以及範圍更廣的安全性測試。

   請參閱 [安全性檢查清單](/help/sites-administering/security-checklist.md) 以取得更多詳細資料。

### 上线 {#go-live}

您希望您的上線儘可能順利。 同樣地，最終步驟需要規劃以徹底執行。

#### 里程碑 {#milestones-7}

* **準備**

   準備和規劃將有助於確保順利上線。

* **安全性**

   確認您的解決方案對內部和外部使用者及其內容的安全性。

* **回退**

   確保遞補所需的所有系統、程式和機制在上線之前都已就緒。

* **支持**

   確定支援服務已就緒並準備就緒。

* **过渡**

   規劃並執行向生產環境和使用者的轉變。

* **轉出**

   準備並執行您的煙霧測試。

## 角色 {#persona}

檢查清單由人員設計。 這些角色與專案生命週期有關聯。

此外，還有 [其他角色](#other-persona) 與特定工作有關的資訊。

### 專案贊助者 {#project-sponsor}

專案贊助者為：

* 負責提供/展示專案的業務案例。
* 決定和定義專案範圍的關鍵；包括：

   * 成功的定義和標準
   * 主要KPI

* 根據使用者端藍圖提供主要里程碑。

### 项目经理 {#project-manager}

專案經理是：

* 根據專案贊助者提供的需求（例如範圍、KPI、成功標準和定義），負責專案的整體交付。
* 負責定義預算，並根據該預算為專案配置資源。
* 專案中所有角色的主要通訊點。

### 架構者 {#architect}

解決方案架構師：

* 負責解決方案與系統的高階設計。
* 協助定義AEM的實施策略。 例如，是實作叢集安裝、冷待命或需要內容傳遞網路(CDN)時。
* 也根據使用者端需求定義AEM解決方案架構。 這可以包括使用者角色（具有相關許可權）的概念、範本與元件之間的關係，或何時使用多網站管理。

### 業務分析人員 {#business-analyst}

業務分析人員：

* 主要負責收集和分析高階需求，然後將其轉換為規格：

   * 供專案經理在規劃開發時使用
   * 供開發團隊在設計和開發期間使用。

* 與客戶緊密合作以分析需求。 這些規則可與：

   * 成功的定義。
   * 成功的標準。
   * KPI （以業務和效能為基礎）。

### 開發負責人 {#development-lead}

開發負責人：

* 負責專案的技術傳遞。
* 負責選取符合使用者端需求的開發方法。
* 擬定開發策略：

   * 確保符合業務和效能KPI
   * 將成功標準和定義列入考量

* 與架構師緊密合作(尤其是在草擬AEM的開發策略時)以定義範本與元件之間的關係、第三方應用程式的整合策略及任何特殊功能等方面。

### 品質銷售機會 {#quality-lead}

品質銷售機會：

* 負責傳遞品質；確保符合成功標準及使用者端定義的任何KPI。
* 定義品品質度、與所有利害關係人保持一致、制定測試計畫並確保其執行。
* 建立報告並傳送給專案關係人。

### 系統工程師 {#system-engineer}

系統工程師：

* 負責監督專案基礎結構。
* 負責：

   * 內部開發和測試環境的設定
   * 將這些系統與使用者端系統配對

* 在上線之前和之後，提供硬體建議、監控各種實作並提供營運支援。

### 安全性主管 {#security-lead}

安全性領導：

* 負責解決方案的整體安全性概念，確保符合客戶的任何需求和政策。
* 針對任何硬體安全概念（例如區域和防火牆），提供安全概念、安全操作和建議。

### 其他角色 {#other-persona}

* 利害關係人

   * 對專案成功有興趣（持股）的人員（通常是企業人員）。 他們經常會貢獻預算。

* 合法的

   * 洽談合約時需要法律建議。

* 教員

   * 根據專案的規模和性質，可使用專門的培訓師為相關團隊制定和舉辦培訓課程。

* 技術作者

   * 根據專案的規模和性質，可以使用專門的技術撰寫人員為特定群組撰寫准則和手冊；例如，為系統管理員撰寫維護手冊，或為作者撰寫使用手冊。

* 系統管理員

   * 負責系統的持續運作。

* 作者與一般使用者

   * 將使用系統建立和維護您的網站內容的人。

## 必要檔案與交付專案 {#required-documents-and-deliverables}

檢查清單涵蓋 **必要檔案** 和 **交付專案** 代表每個里程碑。

* 這些之間並沒有1:1關係；例如，一組必要檔案可產生單一交付專案。
* 來自一個角色的可交付結果可以是另一個角色在相同里程碑期間的必要檔案。

### 必要檔案 {#required-documents}

此 **必要檔案** 適當角色在製作其交付專案時所需的資源。

針對每個 **必要檔案** 該角色應指示：

* **Y/N**：是否收到。
* **1-3**：所接收檔案品質的指示。

### 交付專案 {#deliverables}

對於每個里程碑，適當的角色負責傳遞特定檔案，因此實現他們對特定里程碑的責任。

針對每個 **交付專案** 角色必須指出：

* **Y/N**：是否完成。

交付專案通常用作 **必要檔案** 用於目前或之後的里程碑。

## 相關最佳實務 {#related-best-practices}

如需部署、管理、開發或撰寫的最佳實務，請參閱下列內容：

* 與管理AEM專案相關的其他最佳實務和准則：
   * [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [SEO和URL管理最佳作法](/help/managing/seo-and-url-management.md)
   * [AEM與網頁協助工具准則](/help/managing/web-accessibility.md)
   * [一般資料保護規範](/help/managing/data-protection-and-privacy.md)* [部署和維護最佳實務](/help/sites-deploying/best-practices.md)
* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [開發最佳實務](/help/sites-developing/best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)

## 重要檔案領域 {#key-documentation-areas}

* AEM檔案此外，下列AEM檔案章節特別值得注意（不過，此清單並非詳盡無遺）：

   * [安全性](/help/sites-developing/security.md)
   * [建議的部署](/help/sites-deploying/recommended-deploys.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [硬體大小](/help/managing/hardware-sizing-guidelines.md)
   * AEM的概念：

      * [開發 — 基本知識](/help/sites-developing/the-basics.md)
      * [MSM概念](/help/sites-administering/msm.md)
      * [HTML範本語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

* 相關檔案

   * ADOBE EXPERIENCE CLOUD - [Adobe Experience Cloud規劃](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)
