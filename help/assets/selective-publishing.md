---
title: 使用 Dynamic Media 中的“选择性发布”功能
description: 您可以选择在文件夹级别向Adobe Experience Manager或Dynamic Media发布资产或从中取消发布资产。 您可以使用管理发布或快速发布，而不是仅依赖其设置全局应用于Dynamic Media实例中的所有文件夹的Dynamic Media配置。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# 在Dynamic Media中配置文件夹级别的选择性发布 {#selective-publish-configure-folder}

您可以选择在文件夹级别向Adobe Experience Manager或Dynamic Media发布资产或从中取消发布资产。 您可以使用以下任一选项 **[!UICONTROL 管理发布]** 或 **[!UICONTROL 快速发布]** 而不是仅依赖 **[!UICONTROL Dynamic Media配置]** 其设置全局应用于Dynamic Media实例中的所有文件夹。

例如，通过选择性发布，您可以处理尚未上线的产品的资产。 在这种情况下，营销团队可以访问同步到Dynamic Media的智能裁切图像和动态演绎版。 他们可以创建促销材料，而无需将这些资源发布到Dynamic Media进行全球交付。

>[!IMPORTANT]
>
>“选择性发布”仅在Dynamic Media - Scene7模式下可用。

>[!NOTE]
>
>*正在复制* 与文件夹之间的资源将清除这些资源的发布状态。 但是，当您 *移动* 资源到文件夹或从文件夹属性设置为的文件夹 **[!UICONTROL 选择性发布]**，则会维护这些资源的发布状态。

如果您决定稍后更改 **[!UICONTROL 选择性发布]** 中的设置，则这些更改只会影响您从此时间点上传到该文件夹的新资源。 文件夹中现有资源的发布状态将保持不变，直到您从任一位置手动更改它们 **[!UICONTROL 快速发布]** 或 **[!UICONTROL 管理发布]** 对话框。

文件夹级别 **[!UICONTROL Dynamic Media发布模式]** 选项的值始终默认为 **[!UICONTROL 发布资产]** 在中设置 **[!UICONTROL Dynamic Media配置]**. 但是，本主题中的以下步骤向您展示了如何在文件夹级别手动更改此默认值（如以下步骤中所述）以覆盖 **[!UICONTROL Dynamic Media配置]** 值。

无论您是否依赖以下任一项：

* **[!UICONTROL 发布资产]** 值设置于 **[!UICONTROL Dynamic Media配置]**.
* **[!UICONTROL Dynamic Media发布模式]** 在文件夹级别属性中设置的值。

您可以选择 **[!UICONTROL 立即]**， **[!UICONTROL 激活]**，或 **[!UICONTROL 选择性发布]**. 例如，您可以设置 **[!UICONTROL 发布资产]** 值 **[!UICONTROL Dynamic Media配置]** 到 **[!UICONTROL 激活]**，但设置 **[!UICONTROL Dynamic Media发布]** 文件夹级别的模式值设置为 **[!UICONTROL 选择性发布]**，反之亦然。

在文件夹中配置选择性发布后，可以执行以下任一操作：

* [使用“管理发布”有选择地将资源发布到Dynamic Media或Experience Manager](#selective-publish-manage-publication).
* [使用管理发布从Dynamic Media或Experience Manager有选择地取消发布资源](#selective-unpublish-manage-publication).
* [使用快速发布将资源发布到Dynamic Media或Experience Manager](#quick-publish-aem-dm).
* [通过搜索结果有选择地发布或取消发布资产](#selective-publish-unpublish-search-results).

**要在Dynamic Media中的文件夹级别配置选择性发布，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择导航图标（位于“工具”图标正上方），然后选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 执行下列操作之一：
   * 编辑现有文件夹的属性 — 在 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]**，导航到要编辑其属性的文件夹。 选择文件夹，然后在工具栏中选择 **[!UICONTROL 属性]**.
   * 编辑新文件夹的属性 — 在 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]**，在页面的右上角附近，选择 **[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**. 在 **[!UICONTROL 创建文件夹]** 对话框中，输入文件夹的标题（必需），然后选择 **[!UICONTROL 创建]**. 选择文件夹，然后在工具栏中选择 **[!UICONTROL 属性]**.

1. 在 **[!UICONTROL 同步模式]** 下拉列表，选择下列选项之一：

   | 同步模式 | 描述 |
   | --- | --- |
   | **[!UICONTROL 已继承]** | 文件夹中没有明确的同步值；相反，该文件夹会从其上级文件夹之一继承同步值，或者继承在中设置的默认模式。 **[!UICONTROL Dynamic Media配置]**. 的详细状态 **[!UICONTROL 已继承]** 以刀尖的方式显示。 |
   | **[!UICONTROL 将此文件夹子树中的所有内容同步到Dynamic Media]** | 要成功发布到Dynamic Media，必须将资源同步到Dynamic Media。 选择此选项将包含此子树中用于同步到Dynamic Media的所有资源。 文件夹特定的设置会覆盖 **[!UICONTROL Dynamic Media配置]**. |
   | **[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]** | 从同步到Dynamic Media中排除此子树中的所有资源。 |

   ![文件夹级别的选择性发布](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在 **[!UICONTROL Dynamic Media发布模式]** 从下拉列表中选择一个选项。 此 **[!UICONTROL Dynamic Media发布模式]** 选项始终默认为在中设置的值。 **[!UICONTROL Dynamic Media配置]**. 但是，您可以手动覆盖此默认值 **[!UICONTROL Dynamic Media配置]** 值，方法为使用以下选项之一。

   >[!IMPORTANT]
   >
   >无论您选择哪个Dynamic Media发布模式选项，以后对以下资源进行的任何更新： *已经* 发布后，这些更新将立即发布，用户无需执行任何进一步操作。
   >
   >如果发布的视频已更新，则必须再次发布该视频以反映投放时的更改。

   | Dynamic Media发布模式选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 将资源上传到此文件夹后，系统会将这些资源摄取到Experience Manager中，并立即提供URL/Embed。 此选项仅绑定到Experience Manager发布，无需用户干预即可发布资产。<br>此选项为 *非* 可用（如果已选择） **[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]** 在 **[!UICONTROL 同步模式]** 在上一步中。 |
   | **[!UICONTROL 激活时]** | 将资源上传到此文件夹后，必须先明确发布资源，然后才能提供URL/嵌入链接。 此选项仅绑定到Experience Manager发布。<br>此选项为 *非* 可用（如果已选择） **[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]** 在 **[!UICONTROL 同步模式]** 在上一步中。 |
   | **[!UICONTROL 选择性发布]** | 资源将发布到您选择的Experience Manager或Dynamic Media以在公共域中交付。 两种发布方法相互排斥。 也就是说，您可以将资源发布到DMS7，以便使用智能裁剪或动态呈现版本等功能。 或者，您也可以将资源专门发布到Experience Manager以便安全预览；这些相同的资源包括 *非* 发布到DMS7以在公共域中交付。 如果您选择“ ”，则此选项不可用 **[!UICONTROL 从Dynamic Media同步中排除此文件夹子树中的所有内容]** 在 **[!UICONTROL 同步模式]** 在上一步中。 |

1. 在页面的右上角，选择 **[!UICONTROL 保存并关闭]**，然后选择 **[!UICONTROL 确定]** 返回Experience Manager Assets。

## 使用“管理发布”有选择地将资源发布到Dynamic Media或Experience Manager{#selective-publish-manage-publication}

在可以使用之前 **[!UICONTROL 管理发布]** 要有选择地将资源发布到Dynamic Media或Experience Manager，请确保已设置以下任一设置：

* 此 **[!UICONTROL 发布资产]** 中的选项 **[!UICONTROL Dynamic Media配置]** 到 **[!UICONTROL 选择性发布]**
* 已配置文件夹级别的选择性发布。

请参阅 [创建Dynamic Media配置](#configuring-dynamic-media-cloud-services) 或 [在Dynamic Media中配置文件夹级别的选择性发布](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>“选择性发布”仅在Dynamic Media - Scene7模式下可用。

>[!NOTE]
>
>*正在复制* 与文件夹之间的资源将清除这些资源的发布状态。 但是，当您 *移动* 资源到文件夹或从文件夹属性设置为的文件夹 **[!UICONTROL 选择性发布]**，则会维护这些资源的发布状态。

**要使用“管理发布”将资源有选择地发布到Dynamic Media或Experience Manager，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择导航图标（位于“工具”图标正上方），然后选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 在 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]**，请执行下列操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中选择 **[!UICONTROL 管理发布]**. 使用 **[!UICONTROL 列表视图]** 这样您就可以更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资源。 在工具栏上，选择 **[!UICONTROL 管理发布]**. 使用 **[!UICONTROL 列表视图]** 这样您就可以更轻松地检查特定资产的发布状态。

     >[!NOTE]
     >
     >如果 **[!UICONTROL 管理发布]** 在工具栏上看不到，请改为选择省略号按钮，然后选择 **[!UICONTROL 管理发布]** 从列表菜单中。

1. 在 **[!UICONTROL 管理发布 — 选项]** 页面，在 **[!UICONTROL 操作]**&#x200B;中，选择所需的激活类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL Publish]** (到Experience Manager) | 选择此选项可将资源发布到Experience Manager以进行安全预览。 |
   | **[!UICONTROL 发布到Dynamic Media]** | 选择此选项可将资源发布到Dynamic Media以便在公共域中交付，或者也可使用智能裁剪或动态呈现等功能。<br>此选项仅在以下情况下可用 **[!UICONTROL Dynamic Media发布模式]** 设置为 **[!UICONTROL 选择性发布]** 在文件夹的属性中。 |

1. 下 **[!UICONTROL 计划]**，设置发布时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择可立即发布资源。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间发布资源。 |

1. 在右上角 **[!UICONTROL 管理发布]** 页面，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 管理发布 — 范围]** 页面，执行以下操作之一：

   * 如有必要，请选择要从发布中删除的一个或多个资源。
   * 在右上角 **[!UICONTROL 管理发布 — 范围]** 页面，选择 **[!UICONTROL Publish]** 或 **[!UICONTROL 发布到Dynamic Media]**.
1. 选择 **[!UICONTROL 确定]**.

### 使用管理发布从Dynamic Media或Experience Manager有选择地取消发布资源 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在左侧，选择导航图标（位于“工具”图标正上方），然后选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 在 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]**，请执行下列操作之一：
   * 导航到要取消发布其资产的文件夹。 选择文件夹，然后在工具栏中选择 **[!UICONTROL 管理发布]**. 使用 **[!UICONTROL 列表视图]** 这样您就可以更轻松地检查特定文件夹的发布状态。
   * 导航到要取消发布其资产的文件夹。 打开文件夹，然后选择一个或多个资源。 在工具栏上，选择 **[!UICONTROL 管理发布]**. 使用 **[!UICONTROL 列表视图]** 这样您就可以更轻松地检查特定资产的发布状态。

     >[!NOTE]
     >
     >如果 **[!UICONTROL 管理发布]** 在工具栏上看不到，请改为选择省略号按钮，然后选择 **[!UICONTROL 管理发布]** 从列表菜单中。

1. 在 **[!UICONTROL 管理发布 — 选项]** 页面，在 **[!UICONTROL 操作]**&#x200B;中，选择所需的停用类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 取消发布]** (从Experience Manager) | 如果要从Experience Manager中取消发布资源，请选择此选项。 |
   | **[!UICONTROL 从Dynamic Media取消发布]** | 如果要从Dynamic Media取消发布资源，请选择此选项。<br>此选项仅在以下情况下可用 **[!UICONTROL Dynamic Media发布模式]** 设置为 **[!UICONTROL 选择性发布]** 在文件夹的属性中。 |

1. 下 **[!UICONTROL 计划]**，设置取消激活的时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择可立即取消发布资源。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间取消发布资源。 |

1. 在右上角 **[!UICONTROL 管理发布]** 页面，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 管理发布 — 范围]** 页面，执行以下操作之一：
   * 选择一个或多个要从取消发布中移除的资产。
   * 在右上角 **[!UICONTROL 管理发布 — 范围]** 页面，选择 **[!UICONTROL 取消发布]** 或 **[!UICONTROL 从Dynamic Media取消发布]**.
1. 选择 **[!UICONTROL 确定]**.

## 使用快速发布将资源发布到Dynamic Media或Experience Manager {#quick-publish-aem-dm}

您可以使用 **[!UICONTROL 快速发布]** 用于简单的资产激活案例。 **[!UICONTROL 快速发布]** 立即发布选定的资源，无需进行任何进一步的用户交互。 由于此操作，所有未发布的引用也会自动发布。

>[!NOTE]
>
>使用 **[!UICONTROL 快速发布]** 要将资源发布到Dynamic Media或Experience Manager，请确保 **[!UICONTROL 选择性发布]** 的任一页面中 **[!UICONTROL Dynamic Media配置]** 或在所选文件夹的文件夹属性中查找。

**要使用快速发布将资源发布到Dynamic Media或Experience Manager，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。 在页面的左侧，选择“导航”图标（位于“工具”图标的正上方），然后在页面的右侧选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 在 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]**，请执行下列操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中选择 **[!UICONTROL 快速发布]**. 使用 **[!UICONTROL 列表视图]** 这样您就可以更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资源。 在工具栏上，选择 **[!UICONTROL 快速发布]**. 使用 **[!UICONTROL 列表视图]** 这样您就可以更轻松地检查特定资产的发布状态。

     >[!NOTE]
     >
     >如果 **[!UICONTROL 快速发布]** 在工具栏上看不到，请改为选择省略号按钮，然后选择 **[!UICONTROL 快速发布]** 从列表菜单中。

     ![文件夹级别快速发布到Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 从中选择以下选项之一 **[!UICONTROL 快速发布]** 菜单列表。

   | “快速发布”选项 | 作用 |
   | --- | --- | 
   | 发布到Experience Manager | 将立即发布选定的资源以Experience Manager。 |
   | 发布至 Brand Portal | 将所选资源立即发布到 **[!UICONTROL Brand Portal]**.<br>仅当您的Experience Manager Assets实例具有 **[!UICONTROL Brand Portal]** 已配置。 |
   | 发布到 Dynamic Media | 将选定的资源立即发布到Dynamic Media。<br>资源必须同步到Dynamic Media。 如有必要，请确保 **[!UICONTROL 同步模式]** 文件夹中的属性已设置为 **[!UICONTROL 将此文件夹子树中的所有内容同步到Dynamic Media]**. |

1. 选择 **[!UICONTROL 确定]**，然后选择 **[!UICONTROL 关闭]**.

## 通过搜索结果有选择地发布或取消发布资产 {#selective-publish-unpublish-search-results}

搜索结果可以显示具有不同Dynamic Media发布设置的资源文件夹中的资源。 如果您从搜索结果中选择多个资源，并且每个资源都具有不同的Dynamic Media发布模式设置，则可以触发 **[!UICONTROL 管理发布]** ，以发布或取消发布。

另请参阅 [在Experience Manager中搜索资源](/help/assets/search-assets.md).

**要通过搜索结果有选择地发布或取消发布资产，请执行以下操作：**

1. 在Experience Manager中，在页面的左上角，选择Experience Manager徽标以访问全局导航控制台。 在页面的左侧，选择“导航”图标（位于“工具”图标的正上方），然后选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 在靠近页面右上角的工具栏上，选择“搜索”图标（放大镜）。
1. 在 **[!UICONTROL 键入以搜索]** 文本字段，输入关键字，然后按 **[!UICONTROL 输入]**.
1. 在页面的右上角附近，选择 **[!UICONTROL 列表视图]** 图标。
1. 在页面的左上角附近，选择 **[!UICONTROL 过滤器]** 图标。

   ![搜索结果中的列表视图和筛选器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左侧面板中，展开 **[!UICONTROL 状态]**，然后展开 **[!UICONTROL Dynamic Media]** 搜索谓词。
1. 使用 **[!UICONTROL 已发布]** 和 **[!UICONTROL 已取消发布]** 复选框可根据Dynamic Media资源的已发布状态进一步优化搜索结果。
或者，您可以将这些复选框与 **[!UICONTROL Publish]** 用于优化搜索结果的搜索谓词 **[!UICONTROL 已发布]** 和 **[!UICONTROL 已取消发布]** Experience Manager资源。
1. 执行下列操作之一：
   * 选择要发布或取消发布的一个或多个资源。
   * 在右上角附近 **[!UICONTROL 搜索结果]** 页面，选择 **[!UICONTROL 全选]**.
1. 在工具栏上，选择 **[!UICONTROL 管理发布]**. 选择工具栏上的省略号图标，以便您打开 **[!UICONTROL 管理发布]**.
1. 在 **[!UICONTROL 管理发布 — 选项]** 页面上，选择所需的操作。

   | 选定的操作 | Dynamic Media配置中的发布资源设置 | 资源为 |
   | --- | --- | --- |
   | 发布 | 立即激活或激活时 | 已发布到Experience Manager和Dynamic Media。 |
   | 发布 | 选择性发布 | 仅发布到Experience Manager。 |
   | 取消发布 | 立即激活或激活时 | 已从Experience Manager和Dynamic Media取消发布。 |
   | 取消发布 | 选择性发布 | 仅从Experience Manager取消发布。 |
   | 发布到 Dynamic Media | 立即激活或激活时 | 未发布到Experience Manager或Dynamic Media，或同时发布到两者。 |
   | 发布到 Dynamic Media | 选择性发布 | 仅发布到Dynamic Media。 |
   | 从 Dynamic Media 取消发布 | 立即激活或激活时 | 不会从Experience Manager和/或Dynamic Media取消发布。 |
   | 从 Dynamic Media 取消发布 | 选择性发布 | 仅从Dynamic Media取消发布。 |

1. 下 **[!UICONTROL 计划]**，设置取消激活的时间。

   | 选定的计划 | 发生什么情况 |
   | --- | --- |
   | 现在 | 将立即执行选定的操作。 |
   | 稍后 | 选定的操作将在选定的特定日期和时间运行。 |

1. 在右上角 **[!UICONTROL 管理发布 — 选项]** 页面，选择 **[!UICONTROL 下一个]**.
1. （可选）在 **[!UICONTROL 管理发布 — 范围]** 页面，查看 **[!UICONTROL 发布目标]** 列中的选定资源的列表。

   | Dynamic Media配置中的发布资源设置 | 选定的操作 | 发布目标 |
   | --- | --- | --- |
   | 立即或 <br>激活时 | 发布 | Experience Manager和Dynamic Media |
   | 立即或 <br>激活时 | 发布到 Dynamic Media | 无 |
   | 选择性发布 | 发布 | Experience Manager |
   | 选择性发布 | 发布到 Dynamic Media | Dynamic Media |
   | 立即或 <br>激活时 | 取消发布 | Experience Manager和Dynamic Media |
   | 立即或 <br>激活时 | 从 Dynamic Media 取消发布 | 无 |
   | 选择性发布 | 取消发布 | Experience Manager |
   | 选择性发布 | 从 Dynamic Media 取消发布 | Dynamic Media |

1. 在 **[!UICONTROL 管理发布 — 范围]** 页面，执行以下操作之一：
   * 选择一个或多个要从发布或取消发布中移除的资产。
   * 在右上角 **[!UICONTROL 管理发布 — 范围]** 页面，选择 **[!UICONTROL Publish]** 或 **[!UICONTROL 取消发布]** 以开始操作。
1. 选择 **[!UICONTROL 确定]**.

## 检查资源的发布状态 {#check-publish-status-of-asset}

您可以使用 **[!UICONTROL 时间线]** 替换为 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]** Experience Manager中，用于快速检查资源的发布状态。

**要检查资源的发布状态，请执行以下操作：**

1. 在Experience Manager中，在页面的左上角，选择Experience Manager徽标以访问全局导航控制台。 在页面的左侧，选择“导航”图标（位于“工具”图标的正上方），然后选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 在 **[!UICONTROL 卡片视图]**， **[!UICONTROL 列视图]**，或 **[!UICONTROL 列表视图]** (下面的屏幕截图显示了 **[!UICONTROL 列表视图]**)，打开包含已发布或已取消发布的资产的文件夹。
1. 选择一个资产，使其带有复选标记显示。 例如，请参阅下面的屏幕截图。
1. 在页面的左上角附近，从下拉菜单中选择 **[!UICONTROL 时间线]**. 此 **[!UICONTROL 状态]** 左侧面板中的区域显示所选资源的发布状态。
当您使用 **[!UICONTROL 列表视图]**，为添加额外的列 **[!UICONTROL Dynamic Media]** 此时会显示发布状态。
   * 配置为同步到Dynamic Media的文件夹将显示 **[!UICONTROL Dynamic Media]** 列中。
   * 文件夹是 *非* 配置为同步到Dynamic Media不显示Dynamic Media列。
     ![列表视图和时间线](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 选择性发布故障诊断 {#selective-publish-troubleshoot}

某个资源未同步到Dynamic Media，但却触发了Dynamic Media发布操作，从而导致出现以下错误消息和解决方案：

![选择性发布错误](/help/assets/assets-dm/selective-publish-error.png)
