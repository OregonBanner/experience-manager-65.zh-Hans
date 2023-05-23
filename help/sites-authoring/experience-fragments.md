---
title: AEM Sites製作中的體驗片段
description: 体验片段
uuid: 9a1d12ef-5690-4a2e-8635-a710775efa39
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4c5b52c3-5e23-4125-9306-48bf2ded23cb
docset: aem65
exl-id: 1ff9ac47-9a3a-4a4e-8af8-bc73048e0409
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 65%

---

# 体验片段{#experience-fragments}

體驗片段是一組一或多個元件，包括可在頁面中參考的內容和版面。 它們可以包含任何元件。

体验片段：

* 是體驗（頁面）的一部分。
* 可以跨多個頁面使用。
* 以範本為基礎（僅可編輯）以定義結構和元件。
* 此模板用于创建体验片段的&#x200B;*根页面*。
* 由段落系統中一或多個元件組成，具有版面。
* 可以包含其他體驗片段。
* 可與其他元件（包括其他體驗片段）結合以形成完整頁面（體驗）。
* 可以基于根页面创建一个或多个变体。
* 这些变体可以共享内容和/或组件。
* 可以划分为可在片段的多个变体中使用的构建块。

您可以使用体验片段：

* 如果作者想要重複使用頁面的部分（體驗的片段），他們需要複製並貼上該片段。 创建并维护这些复制/粘贴体验非常费时，而且容易导致用户错误。体验片段无需复制/粘贴。
* 支持 headless CMS 用例。
作者希望仅将 AEM 用于创作，而不是用于提供给客户。第三方系统/触点会使用该体验，然后将其提供给最终用户。

>[!NOTE]
>
>对体验片段的写访问权限要求在组中注册用户帐户：
>
>    `experience-fragments-editors`
如果您遇到任何問題，請聯絡您的系統管理員。

## 何時應使用體驗片段？ {#when-should-you-use-experience-fragments}

該使用「體驗片段」的情況：

* 每當您想要重複使用體驗時。

   * 將與相同或類似內容重複使用的體驗

* 当您使用 AEM 作为第三方的内容投放平台时。

   * 任何需要使用 AEM 作为内容投放平台的解决方案
   * 將內容內嵌於第三方接觸點

* 如果您有具有不同變數或轉譯的體驗。

   * 管道或內容特定變數
   * 對群組有意義的體驗（例如跨頻道具有不同體驗的行銷活動）

* 当您使用全渠道商业时。

   * 共用商務相關內容於 [社群媒體](/help/sites-developing/experience-fragments.md#social-variations) 大規模管道
   * 使接觸點具有交易性

## 组织您的体验片段 {#organizing-your-experience-fragments}

建议执行以下操作：
* 使用文件夹组织您的体验片段；

* [在这些文件夹中配置允许的模板](#configure-allowed-templates-folder)。

创建文件夹允许您：

* 为您的体验片段创建有意义的结构；例如，根据分类

   >[!NOTE]
   无需将体验片段的结构于站点的页面结构保持一致。

* [在文件夹级别分配允许的模板](#configure-allowed-templates-folder)

   >[!NOTE]
   您可以使用[模板编辑器](/help/sites-authoring/templates.md)创建自己的模板。

WKND 项目可根据 `Contributors` 构建一些体验片段。使用的结构还说明了如何使用其他功能，如多站点管理（包括语言副本）。

请参阅：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![体验片段的文件夹](/help/sites-authoring/assets/xf-folders.png)

## 为体验片段创建和配置文件夹 {#creating-and-configuring-a-folder-for-your-experience-fragments}

要为体验片段创建和配置文件夹，建议执行以下操作：

1. [创建文件夹](/help/sites-authoring/managing-pages.md#creating-a-new-folder)。

1. [为该文件夹配置允许的体验片段模板](#configure-allowed-templates-folder)。

>[!NOTE]
也可以[为实例配置允许的模板](#configure-allowed-templates-instance)，但&#x200B;**不**&#x200B;建议使用此方法，因为升级时会覆盖这些值。

### 为文件夹配置允许的模板 {#configure-allowed-templates-folder}

>[!NOTE]
这是指定&#x200B;**允许的模板**&#x200B;的推荐方法，因为升级时不会覆盖这些值。

1. 导航到所需的&#x200B;**体验片段**&#x200B;文件夹。

1. 选择文件夹，然后选择&#x200B;**属性**。

1. 在&#x200B;**允许的模板**&#x200B;字段中指定用于检索所需模板的正则表达式。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   请参阅：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![体验片段属性 – 允许的模板](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   请参阅[体验片段的模板](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments)，以进一步了解详细信息。

1. 选择&#x200B;**保存并关闭**。

### 为实例配置允许的模板 {#configure-allowed-templates-instance}

>[!CAUTION]
不建议使用此方法更改&#x200B;**允许的模板**，因为指定的模板在升级时会被覆盖。
此对话框仅供参考之用。

1. 导航到所需的&#x200B;**体验片段**&#x200B;控制台。

1. 选择&#x200B;**配置选项**：

   ![“配置”按钮](assets/ef-02.png)

1. 在&#x200B;**配置体验片段**&#x200B;对话框中指定所需的模板：

   ![配置体验片段](assets/ef-01.png)

   >[!NOTE]
   请参阅[体验片段的模板](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments)，以进一步了解详细信息。

1. 选择&#x200B;**保存**。

## 创建体验片段 {#creating-an-experience-fragment}

要创建体验片段，请执行以下操作：

1. 从全局导航中选择体验片段。

   ![xf-01](assets/xf-01.png)

1. 導覽至所需的資料夾，然後選取 **建立**.

   ![xf-02](assets/xf-02.png)

1. 选择&#x200B;**体验片段**，以打开&#x200B;**创建体验片段**&#x200B;向导。

   选择所需的&#x200B;**模板**，然后选择&#x200B;**下一步**：

   ![xf-03](assets/xf-03.png)

1. 输入&#x200B;**体验片段**&#x200B;的&#x200B;**属性**。

   A **標題** 為必填欄位。 如果 **名稱** 保留為空白，其衍生自 **標題**.

   ![xf-04](assets/xf-04.png)

   >[!NOTE]
   体验片段模板中的标记不会与此体验片段根页面上的标记合并。
   它们是完全独立的。

1. 单击&#x200B;**创建**。

   將顯示訊息。 选择:

   * **完成**，可返回至控制台

   * **打开**，可打开片段编辑器

## 编辑您的体验片段 {#editing-your-experience-fragment}

体验片段编辑器提供了与普通页面编辑器类似的功能。

>[!NOTE]
另請參閱 [編輯頁面內容](/help/sites-authoring/editing-content.md) 以取得有關如何使用頁面編輯器的詳細資訊。

下列範例程式說明如何為產品建立Teaser：

1. 拖放 **Teaser** 從 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser).

   ![xf-05](assets/xf-05.png)

1. 選取 **[設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)** 元件工具列中的。
1. 添加&#x200B;**资产**，并根据需要定义&#x200B;**属性**。
1. 確認定義，透過 **完成** （勾選圖示）。
1. 根据需要添加更多组件。

## 创建体验片段变体 {#creating-an-experience-fragment-variation}

您可以根據需求建立體驗片段的變體：

1. 開啟您的片段，用於 [編輯](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment).
1. 打开&#x200B;**变体**&#x200B;选项卡。

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. **建立** 可讓您建立：

   * **变体**
   * **[live-copy 形式的变量](/help/sites-administering/msm.md#live-copies)**.

1. 定義必要的屬性：

   * **模板**
   * **标题**
   * **名稱**；如果留空，將從「標題」衍生出來
   * **描述**
   * **变体标记**

   ![xf-06](assets/xf-06.png)

1. 確認方式 **完成** （勾選圖示），新的變數將顯示在面板中：

   ![xf-07](assets/xf-07.png)

## 使用您的体验片段 {#using-your-experience-fragment}

您现在可以在创作页面时使用您的体验片段：

1. 開啟任何頁面進行編輯。

   例如： [https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. 從元件瀏覽器將元件拖曳至頁面段落系統，建立體驗片段元件的例項：

   ![xf-08](assets/xf-08.png)

1. 向组件实例添加实际的体验片段；通过：

   * 從「資產瀏覽器」拖放所需的片段至元件
   * 選取 **設定** 從元件工具列並指定要使用的片段，確認使用 **完成** （勾選）

   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   组件工具栏中的“编辑”将用作在片段编辑器中打开片段的快捷方式。

## 构建块 {#building-blocks}

您可以选择一个或多个组件来创建用于在片段中回收的构建块：

### 创建构建块 {#creating-a-building-block}

要创建构建块，请执行以下操作：

1. 在體驗片段編輯器中，選取您要重複使用的元件：

   ![xf-10](assets/xf-10.png)

1. 从组件工具栏中选择&#x200B;**转换为构建块**：

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. 输入&#x200B;**构建块**&#x200B;的名称，然后使用&#x200B;**转换**&#x200B;进行确认：

   ![xf-11](assets/xf-11.png)

1. **构建基块**&#x200B;将显示在选项卡中，并可在段落系统中进行选择：

   ![xf-12](assets/xf-12.png)

#### 管理构建块 {#managing-a-building-block}

您的构建块会显示在&#x200B;**构建块**&#x200B;选项卡中。對於每個區塊，都可使用下列動作：

* 转至母版：在新选项卡中打开根页面变体
* 重命名
* 删除

![xf-13](assets/xf-13.png)

#### 使用构建块 {#using-a-building-block}

您可以将构建块拖动到任何片段的段落系统，就像对任何组件一样。

## 您的体验片段的详细信息 {#details-of-your-experience-fragment}

可以查看片段的详细信息：

1. 详细信息将显示在&#x200B;**体验片段**&#x200B;控制台的所有视图中，其中&#x200B;**列表视图**&#x200B;包含[导出到 Target](/help/sites-administering/experience-fragments-target.md) 的详细信息：

   ![ef-03](assets/ef-03.png)

1. 在您打开体验片段的&#x200B;**属性**&#x200B;时：

   ![ef-04](assets/ef-04.png)

   这些属性位于各种选项卡中：

   >[!CAUTION]
   当您从体验片段控制台中打开&#x200B;**属性**&#x200B;时，会显示这些选项卡。
   如果在编辑体验片段时&#x200B;**打开属性**，则会显示相应的[页面属性](/help/sites-authoring/editing-page-properties.md)。

   ![ef-05](assets/ef-05.png)

   * **基本**

      * **标题** – 必填项

      * **描述**
      * **标记**
      * **变体总数** – 仅供参考

      * **Web 变体的数量** – 仅供参考
      * **非網路變數的數量** - inf **僅格式**

      * **使用此片段的页数** – 仅供参考
   * **Cloud Service**

      * **云配置**
      * **Cloud Service 配置**
      * **Facebook 页面 ID**
      * **Pinterest 钉板**
   * **引用**

      * 引用列表.
   * **社交媒体状态**

      * 社交媒体变体的详细信息。




## 纯 HTML 演绎版 {#the-plain-html-rendition}

可使用 URL 中的 `.plain.` 选择器从浏览器访问纯 HTML 演绎版。

>[!NOTE]
虽然这可以直接从浏览器获得，[但主要目的是允许其他应用程序（例如，第三方 Web 应用程序、自定义移动实现）仅使用 URL 直接访问体验片段的内容](/help/sites-developing/experience-fragments.md#the-plain-html-rendition)。

## 匯出體驗片段 {#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 AEM和協力廠商管道均可使用此功能。

若要匯出至Adobe Target，也可以使用JSON。 另請參閱 [Target與體驗片段的整合](/help/sites-administering/experience-fragments-target.md) 以取得完整資訊。
