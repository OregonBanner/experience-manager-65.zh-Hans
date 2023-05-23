---
title: 项目
seo-title: Projects
description: 專案可讓您將資源群組到一個實體中，其共用的共用環境可讓您輕鬆管理專案。
seo-description: Projects let you group resources into one entity whose common, shared environment makes it easy to manage your projects
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 85e993000c016240c0fbf398ec8192990e60eee6
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 14%

---


# 项目 {#projects}

專案可讓您將資源分組到一個實體中。 共用的共用環境可讓您輕鬆管理專案。 您可以與專案建立關聯的資源型別在AEM中稱為「圖磚」。 拼贴可以包含项目和团队信息、资产、工作流及其他类型的信息，如[项目拼贴](#project-tiles)中详述。

身為使用者，您可以：

* 建立和刪除專案
* 將內容和資產資料夾關聯至專案
* 從專案移除內容連結

## 存取需求 {#access-requirements}

專案標準AEM功能，不需要任何其他設定。

不過，若使用者在專案中使用專案（例如當建立專案、建立任務/工作流程或檢視和管理團隊時）時檢視其他使用者/群組，這些使用者需要擁有讀取許可權 `/home/users` 和 `/home/groups`.

最簡單的方法是提供 **projects-users** 群組讀取存取權至 `/home/users` 和 `/home/groups`.

## 專案主控台 {#projects-console}

專案主控台是您在AEM中存取和管理專案的地方。

![專案主控台](assets/screen-shot_2019-03-05at125110.png)

「專案」主控台類似於AEM中的其他主控台，允許對個別專案執行許多動作，以及調整您的專案檢視。

### 切換您的模式 {#modes}

您可以使用邊欄選擇器，在主控台模式之間變更。

![边栏选择器](assets/projects-rail.png)

#### 仅限内容 {#content-only}

開啟主控台時，「僅內容」是預設模式。 它會顯示您的所有專案。

#### 时间线 {#timeline}

時間表檢視可讓您選取個別專案並檢視其上的活動。 使用邊欄選擇器或快速鍵 `alt+1` 以變更為此檢視。

![時間軸模式](assets/project-timeline.png)

### 切換檢視 {#views}

您可以使用檢視選擇器，在以大型圖磚檢視專案（預設）、以清單檢視專案或是在行事曆上檢視專案之間變更。

![视图](assets/projects-views.png)

### 篩選您的檢視 {#filter}

您可以使用篩選器在所有專案和僅作用中專案之間切換。

![过滤器](assets/projects-filter.png)

### 選取和檢視專案 {#selecting}

將滑鼠移至專案拼貼上，並按一下核取記號以選取專案。

按一下專案以檢視專案的詳細資訊，以向下鑽研專案的詳細資訊。

### 建立新專案 {#creating}

按一下 **建立** 以新增專案。

## 專案動態磚 {#project-tiles}

專案由您想要一起管理的不同資訊型別組成。 此資訊由不同的專案表示 **圖磚**.

您可以讓下列圖磚與專案相關聯。

* [Assets](#assets)
* [資產集合](#asset-collections)
* [体验](#experiences)
* [链接](#links)
* [專案資訊](#project-info)
* [团队](#team)
* [登录页面](#landing-pages)
* [电子邮件](#emails)
* [工作流](#workflows)
* [启动项](#launches)
* [任务](#tasks)

按一下任何圖磚右上方的下拉式功能表，即可新增更多資料至圖磚。

按一下任何圖磚右下方的省略符號按鈕，以在其關聯主控台中開啟圖磚的資料。

### 资产 {#assets}

在 **資產** 圖磚，即可收集您用於特定專案的所有資產。

![“资产”拼贴](assets/project-tile-assets.png)

您直接在圖磚中上傳資產。

### 資產集合 {#asset-collections}

與資產類似，您可以新增 [資產集合](/help/assets/manage-collections.md) 直接存取您的專案。 您可以在Assets中定義集合。

![資產集合圖磚](assets/project-tile-asset-collection.png)

通过单击&#x200B;**添加收藏集**&#x200B;并从列表中选择相应的收藏集来添加收藏集。

### 体验 {#experiences}

此 **體驗** 圖磚可讓您將行動應用程式、網站或出版物新增至專案。

![體驗圖磚](assets/project-tile-experiences.png)

這些圖示會指出所代表的體驗型別。

* 網站
* 行動應用計畫

### 链接 {#links}

此 **連結** 圖磚可讓您將外部連結與專案建立關聯。

![連結圖磚](assets/project-tile-links.png)

您可以使用易于识别的名称来命名链接并更改其缩略图。

### 项目信息 {#project-info}

此 **專案資訊** 圖磚提供專案的一般資訊，包括說明、專案狀態（非使用中或作用中）、到期日和成員。 此外，您可以新增顯示在主「專案」頁面上的專案縮圖。

![專案資訊拼貼](assets/project-tile-info.png)

### 翻译作业 {#translation-job}

此 **翻譯工作** 圖磚是您開始翻譯的地方，也是您檢視翻譯狀態的地方。

![翻译作业拼贴](assets/project-tile-translation.png)

若要設定翻譯，請參閱檔案 [建立翻譯專案。](/help/assets/translation-projects.md)

### 团队 {#team}

您可以在此圖磚中指定專案團隊的成員。 編輯時，您可以輸入專案團隊成員的名稱並指派使用者角色。

![“团队”拼贴](assets/project-tile-team.png)

您可以在团队中添加和删除团队成员。此外，您还可以编辑向团队成员分配的[用户角色](#userroles)。

### 登录页面 {#landing-pages}

此 **登陸頁面** 圖磚可讓您請求新的登陸頁面。

![登陸頁面動態磚](assets/project-tile-landing.png)

本檔案將說明此工作流程[建立登入頁面工作流程。](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### 电子邮件 {#emails}

此 **電子郵件** 圖磚可協助您管理電子郵件請求。 它會開始 **要求電子郵件** 工作流程。

![電子郵件動態磚](assets/project-tile-email.png)

如需詳細資訊，請參閱 [請求電子郵件工作流程。](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### 工作流 {#workflows}

您可以開始專案的工作流程。 如果有任何工作流程在執行中，其狀態會顯示在 **工作流程** 圖磚。

![工作流程動態磚](assets/project-tile-workflows.png)

根據您建立的專案，有不同的可用工作流程。

這些內容的說明請參閱 [使用專案工作流程。](/help/sites-authoring/projects-with-workflows.md)

### 启动项 {#launches}

此 **啟動** 圖磚會顯示「 」要求的任何啟動 [請求啟動工作流程。](/help/sites-authoring/projects-with-workflows.md)

![「啟動」圖磚](assets/project-tile-launches.png)

### 任务 {#tasks}

任務可讓您監控任何專案相關任務的狀態，包括工作流程。 [处理任务](/help/sites-authoring/task-content.md)中详细介绍了任务。

![「任務」圖磚](assets/project-tile-tasks.png)

## 项目模板 {#project-templates}

範本是啟動專案的基礎。 AEM提供這些標準專案範本。

* **媒體專案**  — 此為媒體相關活動的參考範例專案。 其中包含數個與媒體相關的專案角色，也包括與媒體內容相關的工作流程。
* **[產品拍照專案](/help/sites-authoring/managing-product-information.md)**  — 此為管理電子商務相關產品攝影的參考範例。
* **[翻譯專案](/help/sites-administering/translation.md)**  — 此為管理翻譯相關活動的參考範例。 其中包含基本角色，並包含管理翻譯的工作流程。
* **簡單專案**  — 這是任何不符合其他類別之專案的參考範例。 其中包含三個基本角色和四個一般AEM工作流程。

根據您選取的範本，您可在專案中取得不同的選項，例如提供的使用者角色和工作流程。

## 專案中的使用者角色 {#user-roles-in-a-project}

不同的使用者角色在專案範本中定義，主要原因有二：

1. 許可權：使用者角色屬於列出的三個類別之一：觀察者、編輯者、擁有者。 例如，攝影師或撰稿人將擁有與編輯者相同的許可權。 這些許可權會決定使用者可以對專案中的內容執行的操作。
1. 工作流程：工作流程會決定指派給專案中任務的使用者。 任务可以与项目角色关联。例如，您可以將任務指派給攝影師，這樣所有擁有攝影師角色的團隊成員都會獲得任務。

所有專案都支援下列預設角色，可讓您管理安全性及控制許可權。

| 角色 | 描述 | 权限 | 组成员资格 |
|---|---|---|---|
| 观察者 | 此角色的使用者可以檢視專案詳細資訊，包括專案狀態。 | 專案的唯讀許可權 | `workflow-users` 组 |
| 编辑器 | 此角色的使用者可以上傳和編輯專案內容。 | 對專案、相關中繼資料和相關資產的讀寫存取權<br>上傳快照清單、拍照以及檢閱和核准資產的許可權<br>寫入許可權： `/etc/commerce`<br>修改特定專案的許可權 | `workflow-users` 组 |
| 所有者 | 具有此角色的使用者可以建立專案、在專案中起始工作，並將核准的資產移至生產資料夾。 擁有者也可以檢視和執行專案中的所有其他任務。 | `/etc/commerce` 的写入权限 | `dam-users` 群組才能建立專案<br>`project-administrators` 群組以建立專案和移動資產 |

對於創意專案，也會提供其他角色，例如攝影師。 您可以使用這些角色來衍生特定專案的自訂角色。

### 自動群組建立 {#auto-group-creation}

在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。

例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。

如果刪除專案，則只有在您選取適當的選項時，才會刪除這些群組 [刪除專案時。](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) 管理員也可以手動刪除中的群組 **工具** > **安全性** > **群組**.

## 其他资源 {#additional-resources}

如需有關使用專案的詳細資訊，請參閱下列附加檔案：

* [管理项目](/help/sites-authoring/touch-ui-managing-projects.md)
* [处理任务](/help/sites-authoring/task-content.md)
* [使用项目工作流](/help/sites-authoring/projects-with-workflows.md)
* [Creative Project與PIM整合](/help/sites-authoring/managing-product-information.md)
