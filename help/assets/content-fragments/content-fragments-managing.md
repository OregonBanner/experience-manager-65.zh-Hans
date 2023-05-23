---
title: 管理内容片段
description: 瞭解如何使用Assets控制檯來管理您的AEM內容片段，這是Headless內容的基礎。
feature: Content Fragments
role: User
exl-id: 25c91a85-06ff-4666-a809-46778a689e25
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 81%

---

# 管理内容片段 {#managing-content-fragments}

瞭解如何使用Assets控制檯來管理您的AEM內容片段，這是Headless內容的基礎。

定义完您的[内容片段模型](#creating-a-content-model)后，您可以使用这些模型[创建您的内容片段](#creating-a-content-fragment)。

[内容片段编辑器](#opening-the-fragment-editor)提供各种[模式](#modes-in-the-content-fragment-editor)，使您能够：

* [编辑内容](#editing-the-content-of-your-fragment)和[管理变体](#creating-and-managing-variations-within-your-fragment)
* [在片段中添加批注](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [将内容与片段关联](#associating-content-with-your-fragment)
* [配置元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [查看结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览 JSON 表示形式](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用内容片段：
>
>* 创作页面时；请参阅[使用内容片段进行页面创作](/help/sites-authoring/content-fragments.md)。
>* 用于[使用带有 GraphQL 的内容片段](/help/assets/content-fragments/content-fragments-graphql.md)的 Headless 内容投放。


>[!NOTE]
>
>內容片段儲存為 **資產**，因此主要由 **資產** 主控台。

## 创建内容片段 {#creating-content-fragments}

### 创建内容模型 {#creating-a-content-model}

[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)可在使用结构化内容创建内容片段之前启用和创建。

### 创建内容片段 {#creating-a-content-fragment}

建立內容片段的方法是：

1. 导航到要 **创建片段** 的Assets文件夹。
1. 选择 **创建**，然后选择 **内容片段** ，以打开向导。
1. 向导的第一步要求您指定新片段的基础。

   * [模型](/help/assets/content-fragments/content-fragments-models.md)  — 用來建立需要結構化內容的片段；例如 **冒險** 模型

      * 所有可用模型都會顯示。

   選取後，使用 **下一個** 以繼續進行。

   ![片段基礎](assets/cfm-managing-01.png)

1. 在属性 **步骤中** ，指定：

   * **基本**

      * **标题**

         片段標題。

         强制.

      * **描述**

      * **标记**
   * **高级**

      * **名称**

         名稱；將用於組成URL。

         必要；將自動從標題衍生，但可以更新。


1. 选 **择创建** ，以完成操作，然后打开片段 **进行编辑** ，或返回控制台并执行完 **成**。

   >[!NOTE]
   >在 **清單** 控制檯的模式，您可以更新 **檢視設定** 以啟用 **內容片段模型** 欄。

## Assets控制檯中內容片段的動作 {#actions-for-a-content-fragment-assets-console}

在 **資產** 主控台提供一系列可用於您的內容片段的動作，包括：

* 從工具列；選擇片段後，所有適當的動作都可使用。
* 作為 [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)；可用於個別片段卡片之動作的子集。

![動作](assets/cfm-managing-02.png)

選取片段以顯示包含適用動作的工具列：

* **下载**

   * 將片段儲存為ZIP檔案；您可以定義是否包含元素、變數、中繼資料。

* **创建**
* **签出**
* **属性**

   * 可讓您檢視和/或編輯片段的中繼資料。

* **编辑**

   * 允許您 [開啟片段以編輯內容](/help/assets/content-fragments/content-fragments-variations.md) 及其元素、變數、關聯內容和中繼資料。

* **管理标记**
* **目标收藏集**
* **複製** (和 **貼上**)
* **移动**
* **快速发布**
* **管理发布**
* **删除**

>[!NOTE]
>
>其中許多是 [資產標準動作](/help/assets/manage-assets.md) 和/或 [AEM案頭應用程式](https://helpx.adobe.com/cn/experience-manager/desktop-app/aem-desktop-app.html).

## 打开片段编辑器 {#opening-the-fragment-editor}

打开片段进行编辑：

>[!CAUTION]
>
>要编辑内容片段，您需要[相应的权限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)。 如果您遇到问题，请联系您的系统管理员。

>[!CAUTION]
>
>要编辑内容片段，您需要相应的权限。 如果您遇到问题，请联系您的系统管理员。

1. 使用 **資產** 控制檯以導覽至您的內容片段位置。
1. 透過以下任一方式開啟片段進行編輯：

   * 按一下/點選片段或片段連結（這取決於主控台檢視）。
   * 選取片段，然後 **編輯** （從工具列）。

1. 将打开片段编辑器。 根据需要进行更改：

   ![片段编辑器](assets/cfm-managing-03.png)

1. 进行更改后，请使用&#x200B;**保存**，**保存并关闭**&#x200B;或&#x200B;**关闭**。

   >[!NOTE]
   >
   >**保存并关闭** 可通过&#x200B;**保存**&#x200B;下拉菜单使用。

   >[!NOTE]
   >
   >**保存并关闭**&#x200B;和&#x200B;**关闭**&#x200B;都将退出编辑器 – 请参阅[保存、关闭和版本](#save-close-and-versions)了解有关内容片段的各种选项如何操作的完整信息。

## 内容片段编辑器中的模式和操作 {#modes-actions-content-fragment-editor}

内容片段编辑器中提供了多种模式和操作。

### 内容片段编辑器中的模式 {#modes-in-the-content-fragment-editor}

使用侧面板中的图标在各种模式中导航：

* 变体：[编辑内容](#editing-the-content-of-your-fragment)和[管理变体](#creating-and-managing-variations-within-your-fragment)

* [注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [关联的内容](#associating-content-with-your-fragment)
* [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [结构树](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [预览](/help/assets/content-fragments/content-fragments-json-preview.md)

![模式](assets/cfm-managing-04.png)

### 内容片段编辑器中的工具栏操作 {#toolbar-actions-in-the-content-fragment-editor}

顶部工具栏中的某些功能可以从多种模式使用：

![模式](assets/cfm-managing-top-toolbar.png)

* 当内容页面上已引用片段时，将显示一条消息。 您可以&#x200B;**关闭**&#x200B;消息。

* 可以使用&#x200B;**切换侧面板**&#x200B;图标来隐藏/显示侧面板。

* 在片段名称下方，您可以看到用于创建当前片段的[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)的名称：

   * 该名称还是一个将打开模型编辑器的链接。

* 查看片段的状态；例如，有关创建、修改或发布时间的信息。 

* **保存**&#x200B;提供对&#x200B;**保存并关闭**&#x200B;选项的访问。

* 三个圆点(**...**)下拉列表提供了对其他操作的访问权限：
   * **更新页面引用**
      * 这会更新任何页面引用。
   * **[快速发布](#publishing-and-referencing-a-fragment)**
   * **[管理发布](#publishing-and-referencing-a-fragment)**

<!--
* See the status of the fragment; for example, information about when it was created, modified or published. The status is also color-coded:

  * **New**: grey
  * **Draft**: blue
  * **Published**: green
  * **Modified**: orange
  * **Deactivated**: red
-->

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. 
-->

## 保存、关闭和版本 {#save-close-and-versions}

>[!NOTE]
>
>版本也可以从时间线[创建、比较和还原](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

编辑器具有各种选项：

* **保存**&#x200B;和&#x200B;**保存并关闭**

   * **保存**&#x200B;将保存最新更改并保留在编辑器中。
   * **保存并关闭**&#x200B;将保存最新更改并退出编辑器。

   >[!CAUTION]
   >
   >要编辑内容片段，您需要[相应的权限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)。 如果您遇到问题，请联系您的系统管理员。

   >[!NOTE]
   >
   >在保存之前，可以保留在编辑器中并进行一系列更改。

   >[!CAUTION]
   >
   >除了仅保存您的更改外，这些操作还会更新任何引用，并确保 Dispatcher 按需要刷新。 这些更改可能需要一些时间才能处理。 因此，对于大型/复杂/重载系统，性能可能会受到影响。
   >
   >在使用&#x200B;**保存并关闭**&#x200B;时请记住这一点，然后快速重新进入片段编辑器以进行并保存进一步的更改。

* **关闭**

   将退出编辑器，而不保存最新更改（即自上次&#x200B;**保存**）。

在编辑您的内容片段时，AEM 会自动创建版本，以确保在您取消更改时可以恢复先前的内容（使用&#x200B;**关闭**&#x200B;而不保存）：

1. 打开内容片段以编辑 AEM 时，会检查是否存在基于 Cookie 的令牌，以指示&#x200B;*编辑会话*&#x200B;存在：

   1. 如果找到令牌，则该片段将被视为现有编辑会话的一部分。
   2. 如果令牌为&#x200B;*不*&#x200B;可用，用户便开始编辑内容，并创建一个版本，并将此新编辑会话的令牌发送到客户端，客户端将保存在 Cookie 中。

2. 当有一个&#x200B;*活动*&#x200B;编辑会话时，正在编辑的内容每 600 秒自动保存一次（默认）。

   >[!NOTE]
   >
   >自动保存间隔可使用`/conf`机制进行配置。
   >
   >默认值，请参阅：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户取消编辑，则会恢复在编辑会话开始时创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择&#x200B;**保存**&#x200B;编辑，将保留更新的元素/变体，并删除令牌以结束编辑会话。

## 编辑片段的内容 {#editing-the-content-of-your-fragment}

打开片段后，您可以使用[变体](/help/assets/content-fragments/content-fragments-variations.md)选项卡来创作内容。

## 创建和管理片段中的变体 {#creating-and-managing-variations-within-your-fragment}

创建主控内容后，即可创建和管理[变体](/help/assets/content-fragments/content-fragments-variations.md)内容的一部分。

## 将内容与片段关联 {#associating-content-with-your-fragment}

您还可以[关联内容](/help/assets/content-fragments/content-fragments-assoc-content.md)与片段。 这提供了一个连接，以便在将资产（即图像）添加到内容页面时，可以（可选）与片段一起使用资产（即图像）。

## 查看和编辑片段的元数据（属性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用[元数据](/help/assets/content-fragments/content-fragments-metadata.md)选项卡查看和编辑片段的属性。

## 内容片段的时间线 {#timeline-for-content-fragments}

除了标准选项外，[时间线](/help/assets/manage-assets.md#timeline)提供特定于内容片段的信息和操作：

* 查看有关版本、注释和批注的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)**（选择现有片段，然后选择特定版本）

   * **[与当前比较](#comparing-fragment-versions)**（选择现有片段，然后选择特定版本）

   * 添加&#x200B;**标签**&#x200B;和/或&#x200B;**注释**（选择现有片段，然后选择特定版本）

   * **保存为版本**（选择现有片段，然后选择时间线底部的向上箭头）

* 注释操作

   * **删除**

>[!NOTE]
评论包括：
* 所有资产的标准功能
* 在时间线中制造
* 与片段资产相关
>
注释（适用于内容片段）包括：
* 在片段编辑器中输入
* 特定于片段中选定的文本区段
>


例如：

![时间线](assets/cfm-managing-05.png)

## 比较片段版本 {#comparing-fragment-versions}

选择特定版本后，[时间线](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)中的&#x200B;**与当前比较**&#x200B;操作可用。

此时将打开：

* **当前**（最新）版本（左）

* 所选版本 **v&lt;*x.y*>**（右）

它们将并排显示，其中：

* 任何差异都会突出显示

   * 已删除的文本 – 红色
   * 插入的文本 – 绿色
   * 替换文本 – 蓝色

* 全屏图标允许您自行打开任一版本；然后切换回并行视图
* 您可以&#x200B;**还原**&#x200B;到特定版本
* **完成**&#x200B;将返回控制台

>[!NOTE]
比较片段时无法编辑片段内容。

![比较](assets/cfm-managing-06.png)

## 恢复到某个版本  {#reverting-to-a-version}

您可以还原到片段的特定版本：

* 直接从[时间线](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

   选择所需的版本，然后&#x200B;**还原到此版本**&#x200B;操作。

* [将版本与当前版本进行比较](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)时，您可以&#x200B;**还原**&#x200B;到所选版本。

## 发布和引用片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
如果您的片段基于模型，则应确保[模型已发布](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)。
如果发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

必须发布内容片段才能在发布环境中使用。 它們可以發佈：

* 建立之後；使用 [Assets控制檯中可用的動作](#actions-for-a-content-fragment-assets-console).
* 从[内容片段编辑器](#toolbar-actions-in-the-content-fragment-editor).
* 當您 [發佈使用片段的頁面](/help/sites-authoring/content-fragments.md#publishing)；片段將會列在頁面參考中。

>[!CAUTION]
片段发布和/或引用后，当作者再次打开片段进行编辑时，AEM 将显示警告。 这是为了警告，对片段所做的更改也会影响引用的页面。

## 删除片段 {#deleting-a-fragment}

删除片段：

1. 在 **Assets** 控制台导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   **删除**&#x200B;操作不能作为快速操作使用。

3. 从工具栏中选择&#x200B;**删除**。
4. 确认&#x200B;**删除**&#x200B;操作。

   >[!CAUTION]
   如果片段已在页面中被引用，您将看到一条警告消息，需要您确认是否继续执行&#x200B;**强制删除**。片段及其内容片段组件将从任何内容页面中删除。
