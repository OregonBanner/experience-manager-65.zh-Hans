---
title: 管理内容片段
seo-title: 管理内容片段
description: 内容片段存储为资产，因此主要通过资产控制台进行管理。
seo-description: 内容片段存储为资产，因此主要通过资产控制台进行管理。
uuid: 675e1a6b-2583-488f-bbb4-210daed3e1b0
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 21a18d60-f3fe-4048-9949-8416b5cb4596
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 11%

---


# 管理内容片段{#managing-content-fragments}

内容片段存储为&#x200B;**资产**，因此主要通过&#x200B;**资产**&#x200B;控制台进行管理。

>[!NOTE]
>
>内容片段随后用于创作页面；请参阅[使用内容片段创作页面](/help/sites-authoring/content-fragments.md)。

## 创建内容片段{#creating-content-fragments}

### 创建内容模型{#creating-a-content-model}

[在创建具](/help/assets/content-fragments/content-fragments-models.md) 有结构化内容的内容片段之前，可以启用和创建内容片段模型。

>[!NOTE]
>
>有关模板的更多信息，请参见[开发内容片段](/help/sites-developing/customizing-content-fragments.md);用于简单内容片段。

### 创建内容片段{#creating-a-content-fragment}

创建内容片段的方法（对于简单片段和结构化片段）基本相同：

1. 导航到要 **创建片段** 的Assets文件夹。
1. 选择 **创建**，然后选择 **内容片段** ，以打开向导。
1. 向导的第一步要求您指定新片段的基础。

   * 这可以是：

      * [模板](/help/sites-developing/content-fragment-templates.md) -例如简 **单片段**

      * [模型](/help/assets/content-fragments/content-fragments-models.md) -用于创建需要结构化内容的片段；例如， **** Airportmodel
   * 将显示所有可用的模板和模型。

   选择后，使用&#x200B;**Next**&#x200B;继续。

   ![cfm-6420-15](assets/cfm-6420-15.png)

1. 在属性 **步骤中** ，指定：

   * **基本**

      * **标题**

         片段标题。

         强制.

      * **描述**

      * **标记**
   * **高级**

      * **名称**

         名称；将用于形成URL。

         强制；将自动从标题派生，但可以更新。


1. 选 **择创建** ，以完成操作，然后打开片段 **进行编辑** ，或返回控制台并执行完 **成**。

## 内容片段{#actions-for-a-content-fragment}的操作

在&#x200B;**资产**&#x200B;控制台中，您的内容片段可以执行一系列操作，其中一项是：

* 工具栏；选择片段后，所有适当的操作都可用。
* 作为[快速操作](/help/sites-authoring/basic-handling.md#quick-actions);可用于单个片段卡的操作子集。

![cfm-6420-17](assets/cfm-6420-17.png)

选择片段以显示包含适用操作的工具栏：

* **下载**

   * 将片段另存为ZIP文件；您可以定义是否包括元素、变量、元数据。

* **创建**
* **签出**
* **属性**

   * 允许您视图和／或编辑片段的元数据。

* **编辑**

   * 允许您[打开片段以编辑内容](/help/assets/content-fragments/content-fragments-variations.md)及其元素、变量、相关内容和元数据。

* **管理标记**
* **目标收藏集**

   * 将片段添加到集合。
   * 当[将集合与片段](/help/assets/content-fragments/content-fragments-assoc-content.md#adding-associated-content)关联时，也可以执行此操作。

* **复制**/粘&#x200B;**贴**

* **移动**
* **快速发布**
* **管理发布**
* **删除**

>[!NOTE]
>
>其中许多是[资产](/help/assets/manage-assets.md)和／或[AEM桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)的标准操作。

## 打开片段编辑器{#opening-the-fragment-editor}

要打开片段进行编辑，请执行以下操作：

>[!CAUTION]
>
>要编辑内容片段，您需要[相应的权限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)。 如果您遇到问题，请与系统管理员联系。

1. 使用&#x200B;**资产**&#x200B;控制台导航到内容片段的位置。
1. 通过以下任一方式打开要编辑的片段：

   * 单击／点按片段或片段链接(这取决于控制台视图)。
   * 选择片段，然后从工具栏中选择&#x200B;**编辑**。

   将打开片段编辑器：

   ![cfm-6420-18](assets/cfm-6420-18.png)

   >[!NOTE]
   >
   >1. 当内容页面上已引用片段时，将显示一条消息。
   >2. 使用&#x200B;**切换侧面板**&#x200B;图标可隐藏／显示侧面板。


1. 使用侧面板中的图标在三种模式之间导航：

   * 变量：[编辑内容](#editing-the-content-of-your-fragment)和[管理变量](#creating-and-managing-variations-within-your-fragment)

   * [注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
   * [关联的内容](#associating-content-with-your-fragment)
   * [元数据](#viewing-and-editing-the-metadata-properties-of-your-fragment)

   ![cfm-10](assets/cfm-10.png)

1. 进行更改后，根据需要使用&#x200B;**Save**&#x200B;或&#x200B;**Cancel**。

   >[!NOTE]
   >
   >“保 **存** ”和“取消 **”将退出编辑器——有关这两个选项如何对内容片段进行操作的完整信息，请参阅**[](#save-cancel-and-versions) “保存”、“取消”和“版本”。

## 保存、取消和版本{#save-cancel-and-versions}

>[!NOTE]
>
>还可以从时间轴[创建、比较和还原版本。](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)

编辑器有两个选项：

* **保存**

   将保存最新更改并退出编辑器。

   >[!CAUTION]
   >
   >要编辑内容片段，您需要[相应的权限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)。 如果您遇到问题，请与系统管理员联系。

   >[!NOTE]
   >
   >在选择&#x200B;**保存**&#x200B;之前，可以保留在编辑器中并进行一系列更改。

   >[!CAUTION]
   >
   >除了简单地保存更改外，**Save**&#x200B;还更新了任何引用，并确保调度程序根据需要被刷新。 这些更改可能需要时间才能处理。 因此，对于大型／复杂／重载的系统，可能会产生性能影响。
   >
   >
   >请在使用&#x200B;**保存**&#x200B;时牢记这一点，然后快速重新输入片段编辑器以进行并保存进一步的更改。

* **取消**

   将退出编辑器，而不保存最新更改。

编辑内容片段时，AEM会自动创建版本，以确保在&#x200B;**取消**&#x200B;更改时，可以恢复以前的内容：

1. 打开内容片段以编辑AEM时，会检查是否存在基于cookie的令牌，该令牌指示是否存在&#x200B;*编辑会话*:

   1. 如果找到令牌，则片段被视为现有编辑会话的一部分。
   2. 如果令牌&#x200B;*不*&#x200B;可用，且用户开始编辑内容，则会创建一个版本，并将此新编辑会话的令牌发送到客户端，在客户端将其保存在cookie中。

2. 当存在&#x200B;*active*&#x200B;编辑会话时，每600秒（默认）自动保存一次正在编辑的内容。

   >[!NOTE]
   >
   >可使用`/conf`机制配置自动保存间隔。
   >
   >
   >默认值，请参阅：
   >
   >
   >`/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果用户选择&#x200B;**取消**&#x200B;编辑，则恢复在编辑会话开始创建的版本，并删除令牌以结束编辑会话。
4. 如果用户选择&#x200B;**保存**&#x200B;编辑，则更新的元素／变量将被保留，并删除令牌以结束编辑会话。

## 编辑片段{#editing-the-content-of-your-fragment}的内容

打开片段后，可使用[变量](/help/assets/content-fragments/content-fragments-variations.md)选项卡创作内容。

## 在片段{#creating-and-managing-variations-within-your-fragment}中创建和管理变量

创建主控内容后，即可创建和管理该内容的[变量](/help/assets/content-fragments/content-fragments-variations.md)。

## 将内容与片段{#associating-content-with-your-fragment}关联

您还可以[将内容](/help/assets/content-fragments/content-fragments-assoc-content.md)与片段关联。 这提供了一个连接，以便在将片段添加到内容页面时，可以（可选）将资产（即图像）与片段一起使用。

## 查看和编辑片段{#viewing-and-editing-the-metadata-properties-of-your-fragment}的元数据（属性）

您可以使用[元数据](/help/assets/content-fragments/content-fragments-metadata.md)选项卡视图和编辑片段的属性。

## 内容片段{#timeline-for-content-fragments}的时间轴

除标准选项外，[时间轴](/help/assets/manage-assets.md#timeline)还提供特定于内容片段的信息和操作：

* 视图有关版本、注释和批注的信息
* 版本操作

   * **[还原到此版本](#reverting-to-a-version)** （选择现有片段，然后选择特定版本）

   * **[与当前版本](#comparing-fragment-versions)** （先选择一个现有片段，然后选择特定版本）

   * 添加&#x200B;**标签**&#x200B;和／或&#x200B;**注释**（选择现有片段，然后选择特定版本）

   * **另存为版本** （选择现有片段，然后选择时间轴底部的向上箭头）

* 注释操作

   * **删除**

>[!NOTE]
>
>评论包括：
>
>* 适用于所有资产的标准功能
>* 在时间轴中制作
>* 与片段资产相关

>
>
注释（针对内容片段）包括：
>
>* 在片段编辑器中输入
>* 特定于片段中的选定文本段

>



例如：

![cfm-6420-19-2019](assets/cfm-6420-19-2019.png)

## 比较片段版本{#comparing-fragment-versions}

选择特定版本后，可从[时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)中执行&#x200B;**与当前**&#x200B;比较操作。

此选项将打开：

* **当前**（最新）版本（左）

* 所选版本&#x200B;**v *x.y***（右）

它们将并排显示，其中：

* 突出显示所有差异

   * 删除的文本——红色
   * 插入的文本——绿色
   * 替换文本——蓝色

* 全屏图标允许您自行打开任一版本；然后切换回并行视图
* 您可以&#x200B;**还原到特定版本**
* **** Donew会将您返回控制台

>[!NOTE]
>
>在比较片段时，无法编辑片段内容。

![cfm-6420-20](assets/cfm-6420-20.png)

## 还原到版本{#reverting-to-a-version}

您可以还原到片段的特定版本：

* 直接从[时间轴](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

   选择所需的版本，然后执行&#x200B;**还原到此版本**&#x200B;操作。

* 当[将版本与当前版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)进行比较时，您可以&#x200B;**将**&#x200B;还原到选定版本。

## 发布和引用片段{#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>如果片段基于模型，则应确保[模型已发布](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)。
>
>如果发布的内容片段尚未发布模型，则将显示一个选择列表来指示此情况，并且该模型将随片段一起发布。

必须发布内容片段才能在发布环境中使用。 可以发布它们：

* 创建后；从&#x200B;**资产**&#x200B;控制台。
* 当[发布使用片段](/help/sites-authoring/content-fragments.md#publishing)的页面时；片段将列在页面引用中。

>[!CAUTION]
>
>在发布和／或引用片段后，当作者打开片段以再次进行编辑时，AEM将显示一条警告消息。 这将警告对片段所做的更改也会影响引用的页面。

## 删除片段{#deleting-a-fragment}

要删除片段，请执行以下操作：

1. 在&#x200B;**资产**&#x200B;控制台中，导航到内容片段的位置。
2. 选择片段。

   >[!NOTE]
   >
   >**Delete**&#x200B;操作不能作为快速操作使用。

3. 从工具栏中选择&#x200B;**删除**。
4. 确认&#x200B;**删除**&#x200B;操作。

   >[!CAUTION]
   >
   >如果片段已在页面中被引用，您将看到一条警告消息，需要您确认是否继续执行&#x200B;**强制删除**。片段及其内容片段组件将从任何内容页面中删除。

