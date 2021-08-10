---
title: 使用 Dynamic Media 中的“选择性发布”功能
description: 有关如何在Dynamic Media中使用“选择性发布”功能的信息。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: 发布
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '2945'
ht-degree: 4%

---

# 在Dynamic Media的文件夹级别配置选择性发布 {#selective-publish-configure-folder}

您可以在文件夹级别选择向Adobe Experience Manager或Dynamic Media发布或取消发布资产，或从中取消发布资产。 您可以使用&#x200B;**[!UICONTROL 管理发布]**&#x200B;或&#x200B;**[!UICONTROL 快速发布]**，而不是仅依赖其设置全局应用于Dynamic Media实例中的所有文件夹的&#x200B;**[!UICONTROL Dynamic Media配置]**。

例如，通过选择性发布，您可以处理尚未上线的产品的资产。 在这种情况下，营销团队可以访问同步到Dynamic Media的智能裁剪图像和动态演绎版。 它们可以创建促销材料，而无需将这些资产发布到Dynamic Media进行全球交付。

>[!IMPORTANT]
>
>“选择性发布”仅在Dynamic Media - Scene7模式下可用。

>[!NOTE]
>
>** 将资产复制到文件夹和从文件夹复制资产会清除这些资产的发布状态。但是，当您&#x200B;*将*&#x200B;资产移动到文件夹（其文件夹属性设置为&#x200B;**[!UICONTROL 选择性发布]**）)或从文件夹移动资产时，这些资产的发布状态将保持不变。

如果您稍后决定更改文件夹中的&#x200B;**[!UICONTROL 选择性发布]**&#x200B;设置，则这些更改仅会影响您从此时上传到该文件夹的新资产。 文件夹中现有资产的发布状态将保持原样，直到您从&#x200B;**[!UICONTROL 快速发布]**&#x200B;或&#x200B;**[!UICONTROL 管理发布]**&#x200B;对话框中手动更改它们为止。

文件夹级别&#x200B;**[!UICONTROL Dynamic Media发布模式]**&#x200B;选项始终默认为&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;设置中的值。 但是，本主题中的以下步骤将向您展示如何在文件夹级别手动更改此默认值（如以下步骤中所述）以覆盖&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;值。

无论您是否依赖以下任一项：

* **[!UICONTROL 发布]** 在Dynamic Media配置中 **[!UICONTROL 设置的资产值]**。
* **[!UICONTROL Dynamic Media在文]** 件夹级别属性中设置发布模式值。

您可以选择&#x200B;**[!UICONTROL 立即]**、**[!UICONTROL 激活时]**&#x200B;或&#x200B;**[!UICONTROL 选择性发布]**。 例如，您可以将&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;值设置为&#x200B;**[!UICONTROL 激活时]**，但将文件夹级别的&#x200B;**[!UICONTROL Dynamic Media发布]**&#x200B;模式值设置为&#x200B;**[!UICONTROL 选择性发布]**，反之则设置为。

在文件夹中配置选择性发布后，可以执行以下任一操作：

* [使用管理发布可选择性地将资产发布到Dynamic Media或Experience Manager](#selective-publish-manage-publication)。
* [使用管理发布可选择性地从Dynamic Media或Experience Manager中取消发布资产](#selective-unpublish-manage-publication)。
* [使用快速发布将资产发布到Dynamic Media或Experience Manager](#quick-publish-aem-dm)。
* [通过搜索结果有选择地发布或取消发布资产](#selective-publish-unpublish-search-results)。

**要在Dynamic Media中的文件夹级别配置选择性发布，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择导航图标（就在工具图标的上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 执行下列操作之一：
   * 编辑现有文件夹的属性 — 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，导航到要编辑其属性的文件夹。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 属性]**。
   * 编辑新文件夹的属性 — 在页面右上角附近的&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**。 在&#x200B;**[!UICONTROL 创建文件夹]**&#x200B;对话框中，输入文件夹的标题（必需），然后选择&#x200B;**[!UICONTROL 创建]**。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 属性]**。

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉列表中，选择以下选项之一：

   | 同步模式 | 描述 |
   | --- | --- |
   | **[!UICONTROL 已继承]** | 文件夹上没有明确的同步值；相反，文件夹会从其上级文件夹之一继承同步值，或继承在&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中设置的默认模式。 **[!UICONTROL Inherited]**&#x200B;的详细状态通过工具提示显示。 |
   | **[!UICONTROL 将此文件夹子树中的所有内容同步到Dynamic Media]** | 要成功发布到Dynamic Media，必须将资产同步到Dynamic Media。 选择此选项将包含此子树中要同步到Dynamic Media的所有资产。 特定于文件夹的设置将覆盖&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的默认设置。 |
   | **[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]** | 从同步到Dynamic Media中排除此子树中的所有资产。 |

   ![文件夹级别选择性发布](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL Dynamic Media发布模式]**&#x200B;下拉列表中，选择一个选项。 **[!UICONTROL Dynamic Media发布模式]**&#x200B;选项始终默认为在&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中设置的值。 但是，您可以使用以下选项之一手动覆盖此默认的&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;值。

   >[!IMPORTANT]
   >
   >无论您选择何种Dynamic Media发布模式选项，您稍后对已&#x200B;**&#x200B;发布的资产所做的任何更新，都会立即发布这些更新，而无需执行任何进一步的用户操作。

   | Dynamic Media发布模式选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 将资产上传到此文件夹后，系统会将资产摄取到Experience Manager中，并立即提供URL/嵌入。 此选项仅与Experience Manager发布绑定，发布资产时无需用户干预。<br>如果您在上一步 ** 中选择了从Dynamic Media同 **[!UICONTROL 步模式中排除此文件夹子树中的所有]** 内容，则 **[!UICONTROL 此选项]** 将不可用。 |
   | **[!UICONTROL 激活后]** | 将资产上传到此文件夹后，您必须先明确发布资产，然后才能提供URL/嵌入链接。 此选项仅与Experience Manager发布绑定。<br>如果您在上一步 ** 中选择了从Dynamic Media同 **[!UICONTROL 步模式中排除此文件夹子树中的所有]** 内容，则 **[!UICONTROL 此选项]** 将不可用。 |
   | **[!UICONTROL 选择性发布]** | 资产会发布到您选择的Experience Manager或Dynamic Media，以在公共域中交付。 两种发布方法是相互排斥的。 也就是说，您可以将资产发布到DMS7，以便使用智能裁剪或动态演绎版等功能。 或者，您也可以将资产专门发布到Experience Manager，以便进行安全预览；这些相同的资产是&#x200B;*not*&#x200B;发布到DMS7以在公共域中交付的资产。 如果您在上一步中选择了&#x200B;**[!UICONTROL 同步模式]**&#x200B;的从Dynamic Media同步&#x200B;]**中，从**[!UICONTROL &#x200B;排除此文件夹子树中的所有内容，则此选项不可用。 |

1. 在页面的右上角，选择&#x200B;**[!UICONTROL 保存并关闭]**，然后选择&#x200B;**[!UICONTROL 确定]**&#x200B;以返回到Experience Manager资产。

## 使用管理发布有选择地将资产发布到Dynamic Media或Experience Manager{#selective-publish-manage-publication}

在使用&#x200B;**[!UICONTROL 管理发布]**&#x200B;有选择地将资产发布到Dynamic Media或Experience Manager之前，请确保已设置以下选项之一：

* **[!UICONTROL Dynamic Media配置]**&#x200B;中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;选项发布到&#x200B;**[!UICONTROL 选择性发布]**
* 在文件夹级别配置了选择性发布。

请参阅[创建Dynamic Media配置](#configuring-dynamic-media-cloud-services)或[在Dynamic Media](#selective-publish-configure-folder)中的文件夹级别配置选择性发布

>[!IMPORTANT]
>
>“选择性发布”仅在Dynamic Media - Scene7模式下可用。

>[!NOTE]
>
>** 将资产复制到文件夹和从文件夹复制资产会清除这些资产的发布状态。但是，当您&#x200B;*将*&#x200B;资产移动到文件夹（其文件夹属性设置为&#x200B;**[!UICONTROL 选择性发布]**）)或从文件夹移动资产时，这些资产的发布状态将保持不变。

**要使用管理发布有选择地将资产发布到Dynamic Media或Experience Manager，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择导航图标（就在工具图标的上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，执行以下操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便您能够更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资产。 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便您能够更轻松地检查特定资产的发布状态。

      >[!NOTE]
      >
      >如果工具栏上未显示&#x200B;**[!UICONTROL 管理发布]**，请改为选择省略号按钮，然后从列表菜单中选择&#x200B;**[!UICONTROL 管理发布]**。

1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面的&#x200B;**[!UICONTROL 操作]**&#x200B;下，选择所需的激活类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 发布]** (到Experience Manager) | 选择此选项，以便您可以将资产发布到Experience Manager以进行安全预览。 |
   | **[!UICONTROL 发布到 Dynamic Media]** | 选择此选项，可以将资产发布到Dynamic Media以在公共域中交付，或者使用智能裁剪或动态演绎版等功能。<br>仅当将Dynamic Media发布模式设 **[!UICONTROL 置为选]** 择性发布文件夹属 **[!UICONTROL 性]** 时，此选项才可用。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，设置发布的时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择以立即发布资产。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间发布资产。 |

1. 在&#x200B;**[!UICONTROL 管理发布]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 下一个]**。
1. 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，执行以下操作之一：

   * 如有必要，请选择一个或多个要从发布中删除的资产。
   * 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 发布]**&#x200B;或&#x200B;**[!UICONTROL 发布到Dynamic Media]**。
1. 选择&#x200B;**[!UICONTROL 确定]**。

### 使用管理发布功能，可以选择性地从Dynamic Media或Experience Manager中取消发布资产 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择导航图标（就在工具图标的上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，执行以下操作之一：
   * 导航到要取消发布其资产的文件夹。 选择文件夹，然后在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便您能够更轻松地检查特定文件夹的发布状态。
   * 导航到要取消发布其资产的文件夹。 打开文件夹，然后选择一个或多个资产。 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便您能够更轻松地检查特定资产的发布状态。

      >[!NOTE]
      >
      >如果工具栏上未显示&#x200B;**[!UICONTROL 管理发布]**，请改为选择省略号按钮，然后从列表菜单中选择&#x200B;**[!UICONTROL 管理发布]**。

1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面的&#x200B;**[!UICONTROL 操作]**&#x200B;下，选择所需的取消激活类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 取消发布]** (从Experience Manager) | 如果要从Experience Manager中取消发布资产，请选择此选项。 |
   | **[!UICONTROL 从 Dynamic Media 取消发布]** | 如果要从Dynamic Media中取消发布资产，请选择此选项。<br>仅当将Dynamic Media发布模式设 **[!UICONTROL 置为选]** 择性发布文件夹属 **[!UICONTROL 性]** 时，此选项才可用。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，设置取消激活的时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择以立即取消发布资产。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间取消发布资产。 |

1. 在&#x200B;**[!UICONTROL 管理发布]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 下一个]**。
1. 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，执行以下操作之一：
   * 选择要从取消发布中删除的一个或多个资产。
   * 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 取消发布]**&#x200B;或&#x200B;**[!UICONTROL 从Dynamic Media取消发布]**。
1. 选择&#x200B;**[!UICONTROL 确定]**。

## 使用快速发布将资产发布到Dynamic Media或Experience Manager {#quick-publish-aem-dm}

您可以使用&#x200B;**[!UICONTROL 快速发布]**&#x200B;来处理简单的资产激活案例。 **[!UICONTROL 快速发]** 布会立即发布选定的资产，而无需进行任何进一步的用户交互。由于此操作，任何未发布的引用也会自动发布。

>[!NOTE]
>
>要使用&#x200B;**[!UICONTROL 快速发布]**&#x200B;将资产发布到Dynamic Media或Experience Manager，请确保在&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;或选定文件夹的文件夹属性中启用了&#x200B;**[!UICONTROL 选择性发布]**。

**要使用“快速发布”将资产发布到Dynamic Media或Experience Manager，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在页面左侧，选择导航图标（就在“工具”图标的上方），然后在页面右侧选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，执行以下操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 快速发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便您能够更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资产。 在工具栏中，选择&#x200B;**[!UICONTROL 快速发布]**。 使用&#x200B;**[!UICONTROL 列表视图]**，以便您能够更轻松地检查特定资产的发布状态。

      >[!NOTE]
      >
      >如果工具栏上未显示&#x200B;**[!UICONTROL 快速发布]**，请选择省略号按钮，然后从列表菜单中选择&#x200B;**[!UICONTROL 快速发布]**。

      ![文件夹级别快速发布到Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 从&#x200B;**[!UICONTROL 快速发布]**&#x200B;菜单列表中选择以下选项之一。

   | “快速发布”选项 | 它的作用 |
   | --- | --- | 
   | 发布到Experience Manager | 将选定的资产立即发布到Experience Manager。 |
   | 发布至 Brand Portal | 将选定的资产立即发布到&#x200B;**[!UICONTROL Brand Portal]**。<br>仅当您的Experience Manager资产实例已配置Brand Portal时，此选 **[!UICONTROL 项]** 才可用。 |
   | 发布到 Dynamic Media | 将选定的资产立即发布到Dynamic Media。<br>资产必须同步到Dynamic Media。如有必要，请确保文件夹属性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已设置为&#x200B;**[!UICONTROL 将此文件夹子树中的所有内容同步到Dynamic Media]**。 |

1. 选择&#x200B;**[!UICONTROL 确定]**，然后选择&#x200B;**[!UICONTROL 关闭]**。

## 通过搜索结果有选择地发布或取消发布资产 {#selective-publish-unpublish-search-results}

搜索结果可以跨具有不同Dynamic Media发布设置的资产文件夹显示资产。 当您从搜索结果中选择多个资产，并且每个资产具有不同的Dynamic Media发布模式设置时，您可以从工具栏中触发&#x200B;**[!UICONTROL 管理发布]**&#x200B;以发布或取消发布。

另请参阅[搜索Experience Manager](/help/assets/search-assets.md)中的资产。

**要通过搜索结果有选择地发布或取消发布资产，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标以访问全局导航控制台。 在页面左侧，选择导航图标（就在“工具”图标的上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 在工具栏的页面右上角附近，选择搜索图标（放大镜）。
1. 在&#x200B;**[!UICONTROL Type to search]**&#x200B;文本字段中，输入关键字，然后按&#x200B;**[!UICONTROL Enter]**。
1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 列表视图]**&#x200B;图标。
1. 在页面的左上角附近，选择&#x200B;**[!UICONTROL Filters]**&#x200B;图标。

   ![搜索结果中的列表视图和过滤器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左侧面板中，展开&#x200B;**[!UICONTROL 状态]**，然后展开&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜索谓词。
1. 使用&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]**复选框，可根据Dynamic Media资产的已发布状态进一步优化搜索结果。
或者，您也可以将这些复选框与**[!UICONTROL Publish]**&#x200B;搜索谓词一起使用，以优化&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]** Experience Manager资产的搜索结果。
1. 执行下列操作之一：
   * 选择要发布或取消发布的一个或多个资产。
   * 在&#x200B;**[!UICONTROL 搜索结果]**&#x200B;页面的右上角附近，选择&#x200B;**[!UICONTROL 全选]**。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。 选择工具栏上的省略号图标，以便您可以打开&#x200B;**[!UICONTROL 管理发布]**。
1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面上，选择所需的操作。

   | 所选操作 | 发布Dynamic Media配置中的资产设置 | 资产包括 |
   | --- | --- | --- |
   | 发布 | 立即激活或激活时 | 发布到Experience Manager和Dynamic Media。 |
   | 发布 | 选择性发布 | 仅发布到Experience Manager。 |
   | 取消发布 | 立即激活或激活时 | 未从Experience Manager和Dynamic Media中发布。 |
   | 取消发布 | 选择性发布 | 仅从Experience Manager取消发布。 |
   | 发布到 Dynamic Media | 立即激活或激活时 | 未发布到Experience Manager、Dynamic Media或两者。 |
   | 发布到 Dynamic Media | 选择性发布 | 仅发布到Dynamic Media。 |
   | 从 Dynamic Media 取消发布 | 立即激活或激活时 | 未从Experience Manager、Dynamic Media或两者中取消发布。 |
   | 从 Dynamic Media 取消发布 | 选择性发布 | 仅从Dynamic Media取消发布。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，设置取消激活的时间。

   | 选定的计划 | 发生了什么 |
   | --- | --- |
   | 现在 | 将立即执行所选操作。 |
   | 稍后 | 所选操作将在选定的特定日期和时间运行。 |

1. 在&#x200B;**[!UICONTROL 管理发布 — 选项]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 下一个]**。
1. （可选）在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，查看选定资产的表中的&#x200B;**[!UICONTROL 发布目标]**&#x200B;列。

   | 发布Dynamic Media配置中的资产设置 | 所选操作 | 发布目标 |
   | --- | --- | --- |
   | 激活后立即或<br> | 发布 | Experience Manager和Dynamic Media |
   | 激活后立即或<br> | 发布到 Dynamic Media | 无 |
   | 选择性发布 | 发布 | Experience Manager |
   | 选择性发布 | 发布到 Dynamic Media | Dynamic Media |
   | 激活后立即或<br> | 取消发布 | Experience Manager和Dynamic Media |
   | 激活后立即或<br> | 从 Dynamic Media 取消发布 | 无 |
   | 选择性发布 | 取消发布 | Experience Manager |
   | 选择性发布 | 从 Dynamic Media 取消发布 | Dynamic Media |

1. 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面中，执行以下操作之一：
   * 选择要从发布或取消发布中删除的一个或多个资产。
   * 在&#x200B;**[!UICONTROL 管理发布 — 范围]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 发布]**&#x200B;或&#x200B;**[!UICONTROL 取消发布]**&#x200B;以开始操作。
1. 选择&#x200B;**[!UICONTROL 确定]**。

## 检查资产的发布状态 {#check-publish-status-of-asset}

您可以在Experience Manager中将&#x200B;**[!UICONTROL 时间轴]**&#x200B;与&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;一起使用，以快速检查资产的发布状态。

**要检查资产的发布状态，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标以访问全局导航控制台。 在页面左侧，选择导航图标（就在“工具”图标的上方），然后选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**。
1. 在&#x200B;**[!UICONTROL 卡片视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**（下面的屏幕截图显示了&#x200B;**[!UICONTROL 列表视图]**）中，打开包含已发布或未发布的资产的文件夹。
1. 选择资产，以便显示带复选标记的资产。 有关示例，请参阅下面的屏幕截图。
1. 在页面的左上角附近，从下拉菜单中，选择&#x200B;**[!UICONTROL 时间轴]**。 左侧面板中的&#x200B;**[!UICONTROL 状态]**区域显示选定资产的发布状态。
使用**[!UICONTROL 列表视图]**&#x200B;时，将显示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;发布状态的额外列。
   * 默认情况下，配置为同步到Dynamic Media的文件夹会显示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;列。
   * 配置为同步到Dynamic Media的&#x200B;*not*文件夹不显示Dynamic Media列。
      ![列表视图和时间轴](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 选择性发布故障诊断 {#selective-publish-troubleshoot}

资产未同步到Dynamic Media，但在其上触发了Dynamic Media发布操作，从而导致出现以下错误消息和解决方案：

![选择性发布错误](/help/assets/assets-dm/selective-publish-error.png)
