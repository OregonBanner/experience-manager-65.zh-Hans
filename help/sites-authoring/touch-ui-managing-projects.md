---
title: 管理项目
seo-title: Managing Projects
description: 專案可讓您將資源分組到一個實體中以組織您的專案，該實體可在「專案」主控台中存取和管理
seo-description: Projects lets you organize your project by grouping resources into one entity which can be acessed and managed intheProjects console
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 9%

---


# 管理项目 {#managing-projects}

在 **專案** 主控台，即可存取及管理您的專案。

![“项目”控制台](assets/projects-console.png)

使用主控台，您可以建立專案、將資源與專案相關聯，也可以刪除專案或資源連結。

## 存取需求 {#access-requirements}

專案標準AEM功能，不需要任何其他設定。

不過，若使用者在專案中使用專案（例如當建立專案、建立任務/工作流程或檢視和管理團隊時）時檢視其他使用者/群組，這些使用者需要擁有讀取許可權 `/home/users` 和 `/home/groups`.

最簡單的方法是提供 **projects-users** 群組讀取存取權至 `/home/users` 和 `/home/groups`.

## 创建项目 {#creating-a-project}

請依照下列步驟建立新專案。

1. 在 **專案** 主控台，點選或按一下 **建立** 以開啟 **建立專案** 精靈。
1. 选择模板并单击&#x200B;**下一步**。您可以進一步瞭解標準專案範本 [此處。](/help/sites-authoring/projects.md#project-templates)

   ![建立專案精靈](assets/create-project-wizard.png)

1. 定义&#x200B;**标题**&#x200B;和&#x200B;**描述**，然后根据需要添加&#x200B;**缩略图**&#x200B;图像。您也可以新增或刪除使用者，以及使用者所屬的群組。

   ![精靈的「屬性」步驟](assets/create-project-wizard-properties.png)

1. 点按/单击&#x200B;**创建**。確認會詢問您是要開啟新專案，還是返回主控台。

建立專案的程式與所有專案範本相同。 專案型別之間的差異與可用專案有關 [使用者角色](/help/sites-authoring/projects.md) 和 [工作流程。](/help/sites-authoring/projects-with-workflows.md)

### 將資源與專案建立關聯 {#associating-resources-with-your-project}

專案可讓您將資源分組到一個實體中，以便整體管理它們。 因此，您需要將資源與專案相關聯。 這些資源在專案中分組為 **圖磚**. 您可以新增的資源型別在中說明 [專案動態磚](/help/sites-authoring/projects.md#project-tiles).

若要將資源與專案建立關聯，請執行下列動作：

1. 從開啟您的專案 **專案** 主控台。
1. 點選/按一下 **新增圖磚** 並選取您要連結至專案的圖磚。 您可以选择多种类型的拼贴。

   ![添加拼贴](assets/project-add-tile.png)

1. 点按/单击&#x200B;**创建**。您的资源随即会链接到项目，从现在开始，您便可以从项目中访问该资源。

### 新增專案至圖磚 {#adding-items-to-a-tile}

在某些圖磚中，您可能會想要新增多個專案。 例如，您可能會同時執行多個工作流程，或執行多個體驗。

若要新增專案至圖磚：

1. 在 **專案**，導覽至專案，並按一下要新增專案至之圖磚右上角的向下>形圖示，然後選取適當的選項。

   * 選項檢視磚型別而定。 例如，它可能是 **建立任務** 的 **任務** 圖磚或 **開始工作流程** 的 **工作流程** 圖磚。

   ![平鋪V形](assets/project-tile-create-task.png)

1. 新增專案至圖磚，就像建立新圖磚時一樣。 說明專案拼貼 [此處。](/help/sites-authoring/projects.md#project-tiles)

## 檢視專案資訊 {#viewing-project-info}

專案的主要用途是將相關資訊分組到一個位置，使其更方便存取及操作。 您可以透過多種方式存取此資訊。

### 開啟圖磚 {#opening-a-tile}

您可能想要檢視目前圖磚中包含哪些專案，或修改或刪除圖磚中的專案。

若要開啟圖磚，以便檢視或修改專案，請執行下列動作：

1. 點選或按一下圖磚右下方的省略符號圖示。

   ![「任務」圖磚](assets/project-tile-tasks.png)

1. AEM會開啟主控台，以顯示與動態磚相關聯的專案型別，以及根據所選專案建立的篩選器。

   ![專案任務](assets/project-tasks.png)

### 查看项目时间线 {#viewing-a-project-timeline}

项目时间线提供了项目中的资产上次使用时间的相关信息。若要檢視專案時間表，請按照以下步驟操作。

1. 在 **專案** 主控台，按一下或點選 **時間表** 在主控台左上角的邊欄選擇器中。
   ![選取時間軸模式](assets/projects-timeline-rail.png)
2. 在主控台中，選取您要檢視其時間表的。
   ![專案時間表檢視](assets/project-timeline-view.png)

資產會顯示在邊欄中。 完成後，使用邊欄選擇器返回正常檢視。

### 檢視非作用中專案 {#viewing-active-inactive-projects}

若要在作用中及之間切換 [非使用中專案，](#making-projects-inactive-or-active) 在 **專案** 主控台，按一下 **切換使用中專案** 圖示加以檢視。

![切換作用中專案圖示](assets/projects-toggle-active.png)

根據預設，主控台會顯示作用中的專案。 按一下 **切換使用中專案** 圖示一次，切換為檢視非作用中專案。 再按一下以切換回使用中的專案。

## 組織專案 {#organizing-projects}

有數個選項可協助您組織專案以保留 **專案** 主控台可管理。

### 專案資料夾 {#project-folders}

您可以在中建立資料夾 **專案** 主控台可將類似的專案分組並加以組織。

1. 在 **專案** 主控台點選或按一下 **建立** 然後 **建立資料夾**.

   ![创建文件夹](assets/project-create-folder.png)

1. 為資料夾指定標題，然後按一下 **建立**.

1. 資料夾會新增至主控台。

您現在可以在資料夾中建立專案。 您可以建立多個資料夾，也可以巢狀內嵌資料夾。

### 停用專案 {#making-projects-inactive-or-active}

如果專案已完成，您可能想要將其標示為非使用中，但您仍想要保留有關專案的資訊。 [非使用中專案現在會顯示](#viewing-active-inactive-projects) 根據預設，在 **專案** 主控台。

若要停用專案，請執行下列步驟。

1. 開啟 **專案屬性** 視窗中。
   * 您可以從主控台執行此操作，方法是透過選取專案，或從專案內透過 **專案資訊** 圖磚。
1. 在 **專案屬性** 視窗，變更 **專案狀態** 滑桿來源 **作用中** 至 **非使用中**.

   ![屬性視窗中的專案狀態選擇器](assets/project-status.png)

1. 點選或按一下 **儲存並關閉** 以儲存變更。

### 刪除專案 {#deleting-a-project}

請依照下列步驟刪除專案。

1. 導覽至頂層 **專案** 主控台。
1. 在主控台中選取您的專案。
1. 點選或按一下 **刪除** （在工具列中）。
1. AEM可以在刪除專案時移除/修改關聯的專案資料。 選取您需要的選項 **刪除專案** 對話方塊。
   * 删除项目组和角色
   * 刪除專案資產資料夾
   * 终止项目工作流

   ![專案刪除選項](assets/project-delete-options.png)
1. 點選或按一下 **刪除** 刪除已選取選項的專案。

若要深入瞭解專案自動建立的群組，請參閱 [自動群組建立](/help/sites-authoring/projects.md#auto-group-creation) 以取得詳細資訊。
