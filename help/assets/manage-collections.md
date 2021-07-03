---
title: 管理数字资产收藏集
description: 了解管理资产收藏集的任务，如创建、查看、删除、编辑和下载收藏集。
contentOwner: AG
mini-toc-levels: 1
role: User
feature: 收藏集，资产管理
exl-id: 2117b2de-8024-4aa8-9ce0-68a156928356
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 17%

---

# 管理收藏集 {#managing-collections}

集合是[!DNL Adobe Experience Manager Assets]内的一组资产。 使用收藏集可在用户之间共享资产。该集可以是静态收藏集或基于搜索结果的动态收藏集。

与文件夹不同，收藏集可以包含来自不同位置的资产。 您可以与分配了不同权限级别（包括查看、编辑等）的各种用户共享收藏集。

您可以与一个用户共享多个收藏集。每个收藏集都包含对资产的引用。收藏集中会保持资产的引用完整性。

收藏集的类型如下，具体取决于收藏集整理资产的方式：

* 包含资产、文件夹和其他收藏集的静态引用列表的收藏集。

* 一种智能收藏集，可根据搜索条件动态包含资产。

## 访问收藏集控制台 {#navigating-the-collections-console}

要打开&#x200B;**[!UICONTROL 收藏集]**，请在[!DNL Experience Manager]界面中，转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Collections]**。

## 创建收藏集 {#creating-a-collection}

您可以创建包含[静态引用](#creating-a-collection-with-static-references)的集合，也可以基于基于[搜索条件的筛选器](#creating-a-smart-collection)。 您还可以从灯箱创建收藏集。

### 创建包含静态引用的集合 {#creating-a-collection-with-static-references}

您可以创建包含静态引用的收藏集，例如包含对资产、文件夹、收藏集、旋转集和图像集的引用的收藏集。

1. 导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;控制台。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建收藏集]**&#x200B;页面中，输入收藏集的标题和可选描述。
1. 向收藏集添加成员并分配相应的权限。或者，选择&#x200B;**[!UICONTROL 公共收藏集]**，以允许所有用户访问该收藏集。

   >[!NOTE]
   >
   >要使成员能够与其他用户共享收藏集，请在路径`home/users`上提供`dam-users`组读取权限。 为位于`/content/dam/collections`位置的用户授予权限，以允许用户在弹出列表中查看收藏集。 或者，将用户设为`dam-users`组的一部分。

1. （可选）为收藏集添加缩略图。
1. 单击&#x200B;**[!UICONTROL 创建]**，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。 具有指定标题和属性的集合将在“收藏集”控制台中打开。

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] 允许您为收藏集创建审核任务，其方式与为资产文件夹创建审核任务类似。

   要将资产添加到收藏集，请导航到[!DNL Assets]用户界面。 有关详细信息，请参阅[将资产添加到收藏集](#adding-assets-to-a-collection)。

### 使用拖放区创建收藏集 {#create-collections-using-dropzone}

您可以将资产从[!DNL Assets]用户界面拖至收藏集。 您还可以创建收藏集的副本，并将资产拖动到此处。

1. 从[!DNL Assets]用户界面中，选择要添加到收藏集的资产。
1. 将资产拖到&#x200B;**[!UICONTROL 收藏集]**&#x200B;区域。 或者，单击工具栏中的&#x200B;**[!UICONTROL 收藏集]**。

   ![drop_in_collection](assets/drop_in_collection.png)

1. 在&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，单击工具栏中的&#x200B;**[!UICONTROL 创建收藏集]** 。

   如果要将资产添加到现有收藏集，请从页面中选择它，然后单击&#x200B;**[!UICONTROL 添加]**。 默认情况下，将选择最近更新的集合。

1. 在&#x200B;**[!UICONTROL 创建新收藏集]**&#x200B;对话框中，指定收藏集的名称。如果希望所有用户都可以访问该收藏集，请选择&#x200B;**[!UICONTROL 公共收藏集]**。
1. 单击&#x200B;**[!UICONTROL 继续]**&#x200B;以创建集合。

### 创建智能收藏集 {#creating-a-smart-collection}

智能收藏集使用搜索条件动态填充资产。 您可以仅使用文件，而不使用文件夹或文件和文件夹来创建智能收藏集。

要创建智能收藏集，请执行以下步骤：

1. 导航到[!DNL Assets]用户界面，然后单击搜索。

1. 在Omnisearch框中键入搜索关键词，然后选择`Enter`。 打开“过滤器”面板并应用搜索过滤器。

1. 从&#x200B;**[!UICONTROL 文件和文件夹]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 文件]**。

   ![files_option](assets/files_option.png)

1. 单击&#x200B;**[!UICONTROL 保存智能收藏集]**。

1. 指定集合的名称。 选择&#x200B;**[!UICONTROL Public]**&#x200B;以将具有查看者角色的DAM用户组添加到智能收藏集。

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >如果选择&#x200B;**[!UICONTROL Public]**，则在创建智能收藏集后，具有所有者角色的每个人都可以使用该智能收藏集。 如果取消&#x200B;**[!UICONTROL Public]**&#x200B;选项，则DAM用户组不再与智能收藏集关联。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以创建智能收藏集，然后关闭消息框以完成该过程。

   新的智能收藏集也会添加到&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表。

   ![collection_listing](assets/collection_listing.png)

   **[!UICONTROL 创建智能选择]**&#x200B;选项的标签将更改为&#x200B;**[!UICONTROL 编辑智能选择]**。 要编辑智能收藏集的设置，请从“文件和文 **[!UICONTROL 件夹]** ”列 **[!UICONTROL 表中选择“文件]** ”。 单击&#x200B;**[!UICONTROL 编辑智能选择]** ![编辑智能收藏集](assets/do-not-localize/edit-smart-collection.png)选项。

## 将资产添加到收藏集 {#adding-assets-to-a-collection}

您可以将资产添加到包含一系列引用的资产或文件夹的收藏集中。智能收藏集可使用搜索查询来填充资产。因此，对资产和文件夹的静态引用不适用于此类收藏集。

1. 在[!DNL A]资产用户界面中，选择资产，然后单击工具栏中的&#x200B;**[!UICONTROL 要收藏集]** ![要添加到收藏集](assets/do-not-localize/add-to-collection.png)。
或者，您也可以将资产拖到界面的**[!UICONTROL 收藏集]**&#x200B;区域。 当区域的标签变为&#x200B;**[!UICONTROL 拖放到添加]**&#x200B;时，添加资产。

1. 在&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，选择要将资产添加到的收藏集。

1. 单击&#x200B;**[!UICONTROL 添加]**，然后关闭确认消息。 资产会添加到收藏集。

## 编辑智能收藏集 {#editing-a-smart-collection}

智能收藏集是通过保存搜索来构建的，因此您可以通过修改[保存的搜索](#saved-searches)的搜索参数来更改其内容。

1. 在[!DNL Assets]用户界面中，单击工具栏中的搜索选项![搜索选项](assets/do-not-localize/search_icon.png)。
1. 将光标置于Omnisearch框中，选择`Return`键。
1. 在[!DNL Experience Manager]界面中，打开“过滤器”面板。
1. 从&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中，选择要修改的智能收藏集。“搜索”面板显示为保存的搜索配置的过滤器。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 从&#x200B;**[!UICONTROL 文件和文件夹]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 文件]**。
1. 根据需要修改一个或多个过滤器。 单击&#x200B;**[!UICONTROL 编辑智能收藏集]**。

   您还可以编辑智能收藏集的名称。

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。此时会出现&#x200B;**[!UICONTROL 编辑智能收藏集]**&#x200B;对话框。
1. 单击&#x200B;**[!UICONTROL 覆盖]**&#x200B;以将原始智能收藏集替换为已编辑的收藏集。 或者，选择&#x200B;**[!UICONTROL 另存为]**&#x200B;以单独保存已编辑的集合。
1. 在确认对话框中，单击&#x200B;**[!UICONTROL 保存]**&#x200B;以完成该过程。

## 查看和编辑集合元数据 {#view-edit-collection-metadata}

收藏集元数据由与收藏集相关的数据组成，其中包括添加的任何标记。

1. 从[!UICONTROL 收藏集]控制台中，选择收藏集，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，从&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡中查看收藏集元数据。
1. 根据需要修改元数据。 要保存更改，请单击工具栏中的&#x200B;**[!UICONTROL 保存并关闭]**。

## 批量编辑多个收藏集的元数据 {#editing-collection-metadata-in-bulk}

您可以同时编辑多个收藏集的元数据。 此功能可帮助您快速在多个集合中复制常用元数据。

1. 在收藏集控制台中，选择两个或更多收藏集。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 收藏集元数据]**&#x200B;页面中，根据需要编辑&#x200B;**[!UICONTROL 基本]**&#x200B;和&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡下的元数据。
1. 要查看特定收藏集的元数据属性，请在收藏集列表中取消选择其余的收藏集。 元数据编辑器字段中填充了特定集合的元数据。

   >[!NOTE]
   >
   >* 在[!UICONTROL 属性]页面中，可以通过取消选择从集合列表中删除集合。 默认情况下，收藏集列表会选择所有收藏集。 [!DNL Experience Manager] 不会更新您删除的集合的元数据。
   >* 在列表顶部，选中&#x200B;**[!UICONTROL Title]**&#x200B;附近的复选框，可在选择收藏集和清除列表之间进行切换。


1. 单击工具栏中的&#x200B;**[!UICONTROL 保存并关闭]** ，然后关闭确认对话框。
1. 要将新元数据与现有元数据追加，请选择&#x200B;**[!UICONTROL 追加模式]**。 如果不选中此选项，则新元数据将替换字段中的现有元数据。单击&#x200B;**[!UICONTROL Submit]**。

   >[!NOTE]
   >
   >您为选定收藏集添加的元数据将覆盖这些收藏集之前的元数据。 使用[!UICONTROL 附加模式]在可包含多个值的字段中向现有元数据添加新值。 单值字段始终被覆盖。 您在[!UICONTROL 标记]字段中添加的任何标记都会附加到元数据中的现有标记列表。

要自定义元数据[!UICONTROL 属性]页面（包括添加、修改和删除元数据属性），请使用架构编辑器。

>[!TIP]
>
>批量编辑方法适用于收藏集中的可用资产。 对于跨文件夹提供的资产或符合通用条件的资产，可以在搜索](/help/assets/search-assets.md#metadataupdates)后[批量更新元数据。

## 搜索收藏集 {#searching-collections}

您可以从“收藏集”控制台中搜索收藏集。在Omnisearch框中使用关键字搜索时， [!DNL Assets]会搜索收藏集名称、元数据和添加到收藏集的标记。

如果您从顶级搜索收藏集，则搜索结果中只返回单个收藏集。 [!DNL Assets] 或收藏集中的文件夹将被排除。在所有其他情况下（例如，在单个收藏集或文件夹层次结构中），都会返回所有相关的资产、文件夹和收藏集。

## 在收藏集中搜索 {#searching-within-collections}

在收藏集控制台中，单击某个收藏集以将其打开。

在收藏集中，[!DNL Experience Manager]搜索仅限于您正在查看的收藏集中的资产（及其标记和元数据）。 在文件夹中搜索时，将返回当前文件夹中所有匹配的资产和子文件夹。 在收藏集中搜索时，只会返回与收藏集直接成员匹配的资产、文件夹和其他收藏集。

## 编辑收藏集设置 {#editing-collection-settings}

您可以编辑收藏集设置（如标题和描述），或向收藏集添加成员。

1. 选择收藏集，然后单击工具栏中的&#x200B;**[!UICONTROL 设置]**。 或者，使用收藏集缩览图中的&#x200B;**[!UICONTROL Settings]**&#x200B;快速操作。
1. 在&#x200B;**[!UICONTROL 收藏集设置]**&#x200B;页面中修改收藏集设置。例如，按照[添加收藏集](#creating-a-collection)中所述，修改收藏集标题、描述、成员和权限。

1. 要保存更改，请单击&#x200B;**[!UICONTROL Save]**。

## 删除集合 {#deleting-a-collection}

1. 从收藏集控制台中，选择一个或多个收藏集，然后单击工具栏中的删除。

1. 在对话框中，单击&#x200B;**[!UICONTROL Delete]**&#x200B;以确认删除操作。

   >[!NOTE]
   >
   >您也可以通过[删除保存的搜索](#saved-searches)来删除智能收藏集。

## 下载收藏集 {#downloading-a-collection}

下载收藏集时，会下载收藏集内整个资产层次结构，包括文件夹和子收藏集。

1. 从收藏集控制台中，选择要下载的一个或多个收藏集。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 下载]**。
1. 在&#x200B;**[!UICONTROL 下载]**&#x200B;对话框中，单击&#x200B;**[!UICONTROL 下载]**。 如果要下载收藏集中资产的演绎版，请选择&#x200B;**[!UICONTROL 演绎版]**。 选择&#x200B;**[!UICONTROL Email]**&#x200B;选项，以向集合所有者发送电子邮件通知。

   选择要下载的收藏集时，将下载该收藏集下的完整文件夹层次结构。 要将您下载的每个收藏集（包括嵌套在父收藏集下的子收藏集中的资产）包含在单个文件夹中，请选择&#x200B;**[!UICONTROL 为每个资产创建单独的文件夹]**。

## 创建嵌套收藏集 {#creating-nested-collections}

您可以将一个收藏集添加到另一个收藏集中，从而创建嵌套式收藏集。

1. 从收藏集控制台中，选择所需的收藏集或收藏集组，然后单击工具栏中的&#x200B;**[!UICONTROL 要收藏集]**。

1. 从&#x200B;**[!UICONTROL 添加到收藏集]**&#x200B;页面中，选择要在其中添加收藏集的收藏集。

   >[!NOTE]
   >
   >默认情况下，最近更新的集合会在&#x200B;**[!UICONTROL 添加到集合]**&#x200B;页面中选中。

1. 单击&#x200B;**[!UICONTROL 添加]**。系统会显示一条消息，确认该集合已添加到&#x200B;**[!UICONTROL Select Destination]**&#x200B;页面中的目标集合中。 关闭消息以完成该过程。

>[!NOTE]
>
>无法嵌套智能收藏集。也就是说，智能收藏集不能包含其他任何收藏集。

## 保存的搜索 {#saved-searches}

在[!DNL Assets]用户界面中，您可以根据特定规则、搜索条件或自定义搜索彩块化来搜索或筛选资产。 如果将这些搜索另存为&#x200B;**[!UICONTROL 保存的搜索]**，则以后可以从“过滤器”面板的&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中访问它们。创建保存的搜索也会创建智能收藏集。

![saved_searches_list](assets/saved_searches_list.png)

创建智能收藏集时将创建保存的搜索。智能收藏集会自动添加到&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表。收藏集的[!UICONTROL 保存的搜索]查询将保存在CRXDE的`dam:query`属性中的相对位置`/content/dam/collections/`。 对于可保存的搜索和列表中显示的已保存搜索，没有任何限制。

>[!NOTE]
>
>您可以像共享静态收藏集一样共享智能收藏集。

编辑保存的搜索与编辑智能收藏集相同。 有关详细信息，请参阅[编辑智能收藏集](#editing-a-smart-collection)。

要删除保存的搜索，请执行以下步骤：

1. 在[!DNL Assets]用户界面中，单击搜索![搜索选项](assets/do-not-localize/search_icon.png)。
1. 将光标置于Omnisearch字段中，选择`Return`键。
1. 在[!DNL Experience Manager]界面中，打开“过滤器”面板。
1. 从&#x200B;**[!UICONTROL 保存的搜索]**&#x200B;列表中，单击要删除的智能收藏集旁边的&#x200B;**[!UICONTROL 删除]**。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 在对话框中，单击&#x200B;**[!UICONTROL Delete]**&#x200B;以删除保存的搜索。

## 对集合执行工作流 {#running-a-workflow-on-a-collection}

您可以为收藏集中的资产运行工作流。 如果收藏集包含嵌套收藏集，则工作流还会在嵌套收藏集中的资产上运行。 但是，如果收藏集和嵌套收藏集包含重复的资产，则此类资产的工作流仅运行一次。

1. 打开&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 收藏集]**。 要对特定收藏集执行工作流，请选择它。
1. 打开&#x200B;**[!UICONTROL 时间轴]**&#x200B;边栏。 单击![V形标记向上](assets/do-not-localize/chevron-up-icon.png)并单击&#x200B;**[!UICONTROL 启动工作流]**。
1. 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;部分，从列表中选择工作流模型。例如，选择 **[!UICONTROL DAM 更新资产]**&#x200B;模型。
1. 输入工作流的标题，然后单击&#x200B;**[!UICONTROL 启动]**。
1. 在对话框中，单击&#x200B;**[!UICONTROL 继续]**。 工作流会处理选定收藏集中的所有资产。

>[!MORELIKETHIS]
>
>* [配置Experience Manager资产电子邮件通知](/help/sites-administering/notification.md#assetsconfig)
* [为收藏集创建审核任务](bulk-approval.md)

