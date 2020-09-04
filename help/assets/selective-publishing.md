---
title: 在Dynamic Media中使用选择性发布
description: 有关如何在Dynamic Media中使用选择性发布的信息。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 68e3e80b1c1dda8352ff30989f85f83e82bde261
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 4%

---


# 在Dynamic Media的文件夹级别配置选择性发布 {#selective-publish-configure-folder}

您可以选择在文件夹级别向AEM或Dynamic Media发布资产或从取消发布资产， **[!UICONTROL 而不是只依赖设置对Dynamic Media实例中所有]** 文件夹都是全局性的Dynamic Media Configuration ******** 。

例如，通过选择性发布，您可以处理尚未上市的产品的资源。 在这种情况下，营销团队可以访问同步到Dynamic Media的智能裁剪图像和动态演绎版，以便创建促销材料，而无需将这些资产发布到Dynamic Media进行全局投放。

>[!IMPORTANT]
>
>选择性发布仅在Dynamic Media -Scene7模式下可用。

>[!NOTE]
>
>*将资产* 复制到文件夹和从文件夹复制资产会清除这些资产的发布状态。 但是，当您将资 *产移至* /从其文件夹属性设置为“选择性发 **[!UICONTROL 布”的文件夹时]**，将保留这些资产的发布状态。

如果您稍后决定更改文 **[!UICONTROL 件夹中的]** “选择性发布”设置，这些更改只影响您从此时起上传到该文件夹的新资产。 在您从“快速发布”或“管理发布”对话框手动更改文件夹中现有资 **[!UICONTROL 产的发布]** 状态 **[!UICONTROL 之前，该状]** 态将保持不变。

文件夹级 **[!UICONTROL 别的Dynamic Media发布模式]** 选项始终默认为Dynamic Media配置中 **[!UICONTROL 的发布资产]** 设置 **[!UICONTROL 中的值。]** 但是，本主题中的以下步骤会向您显示如何在文件夹级别手动更改此默认值（如以下步骤所述）以覆盖Dynamic **[!UICONTROL Media配置值]** 。

无论您是依赖在Dynamic Media Configuration中设 **[!UICONTROL 置的Assets]** 值，还是依赖在文件夹级别中设置的Dynamic Media Publish模式值 **[!UICONTROL ，您都仍然能够选择立即发布、激活发布]****************[!UICONTROL 、选择性发布。]** 例如，您可以在Dynamic Media配 **[!UICONTROL 置中将]** Assets值设置为Pon **[!UICONTROL Dynamic Media Publish Assets值，但]** 将Dynamic Media Mode值设置在 ************&#x200B;文件夹级别，将Dynamic Media Publish 激活发布，反之亦然，等等。

在文件夹中配置选择性发布后，可以执行下列任一操作：

* [使用管理发布，有选择地将资产发布到Dynamic Media或AEM。](#selective-publish-manage-publication)
* [使用管理发布从Dynamic Media或AEM选择性地取消发布资产。](#selective-unpublish-manage-publication)
* [使用快速发布将资产发布到Dynamic Media或AEM。](#quick-publish-aem-dm)
* [通过搜索结果有选择地发布或取消发布资产。](#selective-publish-unpublish-search-results)

**在Dynamic Media中在文件夹级别配置选择性发布**

1. 在AEM中，点按AEM徽标以访问全局导航控制台。 在左侧，点按导航图标（就在工具图标上方），然后点按资产> **[!UICONTROL 文件。]**
1. 执行下列操作之一：
   * 编辑现有文件夹的属性——在卡 **[!UICONTROL 片视图]**、 **[!UICONTROL 列视图或]**&#x200B;列表视图中 **[!UICONTROL ，导]**&#x200B;航到要编辑其属性的文件夹。 选择文件夹，然后在工具栏中点按 **[!UICONTROL 属性。]**
   * 编辑新文件夹的属性——在 **[!UICONTROL 卡片视图]**、列 **[!UICONTROL 视图或]**&#x200B;列表视图 **[!UICONTROL 中，在页面的右上角附]**&#x200B;近，点按 **[!UICONTROL 创建>文件夹。]** 在“创 **[!UICONTROL 建文件夹]** ”对话框中，输入文件夹的标题（必需），然后点按 **[!UICONTROL 创建。]** 选择文件夹，然后在工具栏中点按 **[!UICONTROL 属性。]**

1. 在“同 **[!UICONTROL 步模式]** ”下拉列表中，选择以下选项之一：

   | 同步模式 | 描述 |
   | --- | --- |
   | **[!UICONTROL 已继承]** | 文件夹上没有明确的同步值；相反，文件夹会从其父文件夹或Dynamic Media配置中设置的默认模式继承 **[!UICONTROL 同步值。]** “已继承 **[!UICONTROL ”]** (Inherited)的详细状态通过工具提示显示。 |
   | **[!UICONTROL 将该文件夹子树中的所有内容同步到 dynamicmedia]** | 要成功发布到Dynamic Media，资产必须同步到Dynamic Media。 选择此选项将包括此子树中用于同步到Dynamic Media的所有资产。 特定于文件夹的设置将覆盖Dynamic Media配置中的默 **[!UICONTROL 认设置。]** |
   | **[!UICONTROL 从dynamicmedia sync中排除此文件夹子树中的所有内容]** | 排除此子树中的所有资产，使其不能同步到Dynamic Media。 |

   ![文件夹级别选择性发布](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在Dynamic **[!UICONTROL Media发布模式下拉列表]** ，选择一个选项。 请注意，Dynamic **[!UICONTROL Media发布模式]** 选项始终默认为在Dynamic Media配置中 **[!UICONTROL 设置的值。]** 但是，您可以使用以下选项 **[!UICONTROL 之一手动覆盖]** 此默认的Dynamic Media配置值。

   >[!IMPORTANT]
   >
   >请注意，无论您选择的Dynamic Media发布模式选项是什么，您以后对已发布的资产所做的任何更新 ** ，都会立即发布这些更新，而不会执行任何其他用户操作。

   | Dynamic Media发布模式选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 资产上传到此文件夹后，系统会将资产引入AEM并立即提供URL/Embed。 此选项仅与AEM发布相关联，发布资产不需要用户干预。<br>如果您在上 *一步* 的“同步”模式 **[!UICONTROL 中选择“从Dynamicmedia sync中排除此文件夹子树中的所有内容]** ”，则 **[!UICONTROL 此选项不]** 可用。 |
   | **[!UICONTROL 激活后]** | 将资产上传到此文件夹后，您需要先明确发布资产，然后才能提供URL/嵌入链接。 此选项仅绑定到AEM发布。<br>如果您在上 *一步* 的“同步”模式 **[!UICONTROL 中选择“从Dynamicmedia sync中排除此文件夹子树中的所有内容]** ”，则 **[!UICONTROL 此选项不]** 可用。 |
   | **[!UICONTROL 选择性发布]** | 资产会发布到您选择的AEM或Dynamic Media，以便在公共域中投放。 两种出版方法相互排斥。  即，您可以将资产发布到DMS7，以便使用智能裁剪或动态演绎版等功能。 或者，您也可以将资产仅发布到AEM以进行安全预览；这些相同的资 *产不* 会发布到DMS7，以便在公共域中进行投放。 如果您在上一步的“同步”模 **[!UICONTROL 式下从Dynamicmedia同步中排除此文件夹子树中的]** 所有内容，则此选 **[!UICONTROL 项不可用]** 。 |

1. 在页面的右上角，点按保 **[!UICONTROL 存并关闭]**，然后点 **[!UICONTROL 按确]** 定，返回AEM Assets。

## 使用管理发布，有选择地将资产发布到Dynamic Media或AEM{#selective-publish-manage-publication}

在使用管理发 **[!UICONTROL 布之前]** ，请务必先在动态媒体配置中设置“发布资产”选项，以在文件夹级别 **[!UICONTROL 选择性发布或配置]** 选择性发布，然后再使用管理发布 ******** 功能将资产有选择地发布到Dynamic Media或AEM。

请参 [阅在Dynamic Media的文](#configuring-dynamic-media-cloud-services)[件夹级别创建Dynamic Media配置或配置选择性发布](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>选择性发布仅在Dynamic Media -Scene7模式下可用。

>[!NOTE]
>
>*将资产* 复制到文件夹和从文件夹复制资产会清除这些资产的发布状态。 但是，当您将资 *产移至* /从其文件夹属性设置为“选择性发 **[!UICONTROL 布”的文件夹时]**，将保留这些资产的发布状态。

**使用管理发布有选择地将资产发布到Dynamic Media或AEM**

1. 在AEM中，点按AEM徽标以访问全局导航控制台。 在左侧，点按导航图标（就在工具图标上方），然后点按资产> **[!UICONTROL 文件。]**
1. 在 **[!UICONTROL 卡视图]**、列 **[!UICONTROL 视图]**&#x200B;或 **[!UICONTROL 列表视图]**&#x200B;中，执行下列操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中点按管 **[!UICONTROL 理发布。]**  您可能会发现使用列表 **[!UICONTROL 视图很有帮]** 助，因此您可以更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资产。 在工具栏中，点按管 **[!UICONTROL 理发布。]** 您可能会发现使用列表 **[!UICONTROL 视图很有帮]** 助，因此您可以更轻松地检查特定资产的发布状态。

      >[!NOTE]
      >
      >如 **[!UICONTROL 果工具栏]** 上未显示管理发布 **[!UICONTROL ，请点按省略号按钮，然后从列表菜单]** 中选择管理发布。

1. 在“管 **[!UICONTROL 理发布——选项]** ”页面 **[!UICONTROL 的“操作]**”下，选择所需的激活类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 发布]** (到AEM) | 选择此选项可将资产发布到AEM以实现安全预览。 |
   | **[!UICONTROL 发布到 Dynamic Media]** | 选择此选项可将资产发布到Dynamic Media以在公共域中投放，或者这样您就可以使用智能裁剪或动态演绎版等功能。<br>只有在文件夹属性中 **[!UICONTROL 的“Dynamic Media Publish]** ”模式设置 **[!UICONTROL 为“Selective Publish]** ”时，此选项才可用。 |

1. 在 **[!UICONTROL 计划]**&#x200B;下，设置发布的时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择以立即发布资产。 |
   | **[!UICONTROL 稍后]** | 选择以在特定日期和时间发布资产。 |

1. 在“管理发布”页面的右 **[!UICONTROL 上角]** ，点按下 **[!UICONTROL 一步。]**
1. 在“管 **[!UICONTROL 理发布——范围]** ”页中，执行下列操作之一：
   * 根据需要，选择要从发布中删除的一个或多个资产。
   * 在“管理发布——范围”页 **[!UICONTROL 面的右上角]** ，点按 **[!UICONTROL 发布]** 或 **[!UICONTROL 发布到Dynamic Media。]**
1. 点按 **[!UICONTROL 确定。]**

### 使用管理发布从Dynamic Media或AEM选择性地取消发布资产 {#selective-unpublish-manage-publication}

1. 在AEM中，点按AEM徽标以访问全局导航控制台。 在左侧，点按导航图标（就在工具图标上方），然后点按资产> **[!UICONTROL 文件。]**
1. 在 **[!UICONTROL 卡视图]**、列 **[!UICONTROL 视图]**&#x200B;或 **[!UICONTROL 列表视图]**&#x200B;中，执行下列操作之一：
   * 导航到要取消发布其资产的文件夹。 选择文件夹，然后在工具栏中点按管 **[!UICONTROL 理发布。]**  您可能会发现使用列表 **[!UICONTROL 视图很有帮]** 助，因此您可以更轻松地检查特定文件夹的发布状态。
   * 导航到要取消发布其资产的文件夹。 打开文件夹，然后选择一个或多个资产。 在工具栏中，点按管 **[!UICONTROL 理发布。]** 您可能会发现使用列表 **[!UICONTROL 视图很有帮]** 助，因此您可以更轻松地检查特定资产的发布状态。

      >[!NOTE]
      >
      >如 **[!UICONTROL 果工具栏]** 上未显示管理发布 **[!UICONTROL ，请点按省略号按钮，然后从列表菜单]** 中选择管理发布。

1. 在“管 **[!UICONTROL 理发布——选项]** ”页面 **[!UICONTROL 的“操作]**”下，选择所需的取消激活类型。

   | 操作 | 描述 |
   | --- | --- |
   | **[!UICONTROL 取消发布]** (从AEM) | 选择此选项可从AEM中取消发布资产。 |
   | **[!UICONTROL 从 Dynamic Media 取消发布]** | 选择此选项可从Dynamic Media中取消发布资产。<br>只有在文件夹属性中 **[!UICONTROL 的“Dynamic Media Publish]** ”模式设置 **[!UICONTROL 为“Selective Publish]** ”时，此选项才可用。 |

1. 在 **[!UICONTROL 计划]**&#x200B;下，设置取消激活的时间。

   | 计划 | 描述 |
   | --- | --- |
   | **[!UICONTROL 现在]** | 选择以立即取消发布资产。 |
   | **[!UICONTROL 稍后]** | 选择此项可在特定日期和时间取消发布资产。 |

1. 在“管理发布”页面的右 **[!UICONTROL 上角]** ，点按下 **[!UICONTROL 一步。]**
1. 在“管 **[!UICONTROL 理发布——范围]** ”页中，执行下列操作之一：
   * 选择要从取消发布中删除的一个或多个资产。
   * 在“管理发布——范围”页 **[!UICONTROL 面的右上角]** ，点 **[!UICONTROL 按取消发布]** 或 **[!UICONTROL 从Dynamic Media取消发布。]**
1. 点按 **[!UICONTROL 确定。]**

## 使用快速发布将资产发布到Dynamic Media或AEM {#quick-publish-aem-dm}

您可以对简单 **[!UICONTROL 的资产激活]** ，使用快速发布。 **[!UICONTROL 快速发布]** ，可立即发布选定的资产，无需进行任何进一步的用户交互。 因此，任何未发布的引用也会自动发布。

>[!NOTE]
>
>要使用 **[!UICONTROL 快速发布]** 将资产发布到Dynamic Media或AEM，请确保在Dynamic Media配置中或在选定文件夹的 **[!UICONTROL 文件夹属性中启用“选]** 择性发布 **** ”。

**使用快速发布将资产发布到Dynamic Media或AEM**

1. 在AEM中，点按AEM徽标以访问全局导航控制台。 在页面的左侧，点按导航图标（就在工具图标的上方），然后在页面的右侧，点按资产> **[!UICONTROL 文件。]**
1. 在 **[!UICONTROL 卡视图]**、列 **[!UICONTROL 视图]**&#x200B;或 **[!UICONTROL 列表视图]**&#x200B;中，执行下列操作之一：
   * 导航到要发布其资产的文件夹。 选择文件夹，然后在工具栏中点按快 **[!UICONTROL 速发布。]**  您可能会发现使用列表 **[!UICONTROL 视图很有帮]** 助，因此您可以更轻松地检查特定文件夹的发布状态。
   * 导航到要发布其资产的文件夹。 打开文件夹，然后选择一个或多个资产。 On the toolbar, tap **[!UICONTROL Quick Publish.]** 您可能会发现使用列表 **[!UICONTROL 视图很有帮]** 助，因此您可以更轻松地检查特定资产的发布状态。

      >[!NOTE]
      >
      >如 **[!UICONTROL 果工具栏]** 上未显示快速发布 **[!UICONTROL ，请点按省略号按钮，然后从列表菜单]** 中选择快速发布。

      ![文件夹级快速发布到Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 从“快速发布”菜单列表 **[!UICONTROL 中选择以]** 下选项之一。

   | 快速发布选项 | 它的用途 |
   | --- | --- | 
   | 发布到 AEM | 将选定的资产立即发布到AEM。 |
   | 发布至 Brand Portal | 将选定的资产立即发布 **[!UICONTROL 到Brand Portal。]**<br>仅当您的AEM Assets实例已配置Brand Portal时，**[!UICONTROL &#x200B;此选项&#x200B;]**才可用。 |
   | 发布到 Dynamic Media | 将选定的资产立即发布到Dynamic Media。<br>资产必须已同步到Dynamic Media。 如有必要，请确 **[!UICONTROL 保将文件夹]** 属性中的“同步模式”设置 **[!UICONTROL 为将此文件夹子树中的所有内容同步到dynamicmedia。]** |

1. 点按 **[!UICONTROL 确定]**，然后点按 **[!UICONTROL 关闭。]**

## 通过搜索结果有选择地发布或取消发布资产 {#selective-publish-unpublish-search-results}

搜索结果可以显示具有不同Dynamic Media发布设置的不同资产文件夹中的资产。 如果您已从搜索结果中选择一个或多个资产，且资产具有不同的Dynamic Media发布模式设置，则您可以从工具栏触发 **[!UICONTROL 管理发布]** ，以进行发布或取消发布。

另请参阅 [在AEM中搜索资产。](/help/assets/search-assets.md)

**通过搜索结果有选择地发布或取消发布资产**

1. 在AEM的页面左上角，点按AEM徽标以访问全局导航控制台。 在页面的左侧，点按导航图标（在工具图标上方），然后点按资产> **[!UICONTROL 文件。]**
1. 在工具栏中，点按页面右上角附近的“搜索”图标（放大镜）。
1. 在“要 **[!UICONTROL 搜索的类型]** ”文本字段中，输入关键字，然后按 **[!UICONTROL Enter。]**
1. 在页面的右上角附近，点按 **[!UICONTROL 列表视图图标]** 。
1. 在页面的左上角附近，点按 **[!UICONTROL 过滤器]** 。

   ![列表视图和搜索结果中的过滤器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左面板中，展开 **[!UICONTROL 状态]**，然后展开 **[!UICONTROL Dynamic Media]** 搜索谓词。
1. 使用已 **[!UICONTROL 发布]** 和 **[!UICONTROL 未发布]** 的复选框，根据Dynamic Media资产的已发布状态进一步优化搜索结果。
（可选）您可以将这些复选框与发布搜索谓 **[!UICONTROL 词结合使用]** ，以优化已发布和未发布 **[!UICONTROL 的AEM资]** 资 **[!UICONTROL 产的搜索结]** 果。
1. 执行下列操作之一：
   * 选择要发布或取消发布的一个或多个资产。
   * 在“搜索结果”页面的右上 **[!UICONTROL 角附近]** ，点按 **[!UICONTROL 全选。]**
1. 在工具栏中，点按管 **[!UICONTROL 理发布。]** 您可能需要点按工具栏上的省略号图标才能看到管理 **[!UICONTROL 发布。]**
1. 在“管 **[!UICONTROL 理发布——选项]** ”页面上，选择所需的操作。

   | 所选操作 | Dynamic Media配置中的“发布资产”设置 | 资产包括 |
   | --- | --- | --- |
   | 发布 | 立即或在激活 | 已发布到AEM和Dynamic Media。 |
   | 发布 | 选择性发布 | 仅发布到AEM。 |
   | 取消发布 | 立即或在激活 | 从AEM和Dynamic Media取消发布。 |
   | 取消发布 | 选择性发布 | 仅从AEM取消发布。 |
   | 发布到 Dynamic Media | 立即或在激活 | 未发布到AEM或Dynamic Media，或两者。 |
   | 发布到 Dynamic Media | 选择性发布 | 仅发布到Dynamic Media。 |
   | 从 Dynamic Media 取消发布 | 立即或在激活 | 未从AEM或Dynamic Media或两者取消发布。 |
   | 从 Dynamic Media 取消发布 | 选择性发布 | 仅从Dynamic Media取消发布。 |

1. 在 **[!UICONTROL 计划]**&#x200B;下，设置取消激活的时间。

   | 所选计划 | 发生了什么 |
   | --- | --- |
   | 现在 | 将立即执行选定的操作。 |
   | 稍后 | 所选操作将在所选的特定日期和时间运行。 |

1. 在“管理发布——选项”页 **[!UICONTROL 面的右上角]** ，点按下 **[!UICONTROL 一步。]**
1. （可选）在管 **[!UICONTROL 理发布——范围]** 页面中，查看 **[!UICONTROL 选定资产]** 的表中的发布目标列。

   | Dynamic Media配置中的“发布资产”设置 | 所选操作 | 发布目标 |
   | --- | --- | --- |
   | 立即或 <br>在激活 | 发布 | AEM和Dynamic Media |
   | 立即或 <br>在激活 | 发布到 Dynamic Media | 无 |
   | 选择性发布 | 发布 | AEM |
   | 选择性发布 | 发布到 Dynamic Media | Dynamic Media |
   | 立即或 <br>在激活 | 取消发布 | AEM和Dynamic Media |
   | 立即或 <br>在激活 | 从 Dynamic Media 取消发布 | 无 |
   | 选择性发布 | 取消发布 | AEM |
   | 选择性发布 | 从 Dynamic Media 取消发布 | Dynamic Media |

1. 在“管 **[!UICONTROL 理发布——范围]** ”页中，执行下列操作之一：
   * 选择要从发布或取消发布中删除的一个或多个资产。
   * 在“管理发布——范围”页 **[!UICONTROL 面的右上角]** ，点 **[!UICONTROL 按发布]** 或 **[!UICONTROL 取消发布]** ，开始执行操作。
1. 点按 **[!UICONTROL 确定。]**

## 检查资产的发布状态 {#check-publish-status-of-asset}

您可以将时 **[!UICONTROL 间轴与]** 卡视图 **[!UICONTROL 、列视图]**&#x200B;或列表AEM的 **[!UICONTROL 视图结合使]****** 用，以快速检查资产的发布状态。

**检查资产的发布状态**

1. 在AEM的页面左上角，点按AEM徽标以访问全局导航控制台。 在页面的左侧，点按导航图标（在工具图标上方），然后点按资产> **[!UICONTROL 文件。]**
1. 在卡 **[!UICONTROL 片视图]**、列 **[!UICONTROL 视图或列表]**&#x200B;视图中(下面的截图显示 ********&#x200B;了列表视图的)，打开一个包含您已发布或取消发布的资产的文件夹。
1. 选择资产，以便显示带有复选标记的资产。 请参见下面的屏幕截图。
1. Near the upper-left corner of the page, from the drop-down menu, select **[!UICONTROL Timeline.]** 左 **[!UICONTROL 面板中]** 的“状态”区域显示选定资产的发布状态。
使用列表 **[!UICONTROL 视图]**&#x200B;时，将显示另一 **[!UICONTROL 列作为Dynamic Media]** 发布状态。
   * 默认情况下，配置为同步到Dynamic Media的文件夹 **[!UICONTROL 将显示]** Dynamic Media列。
   * 未配置为 *同步* 到Dynamic Media的文件夹将不显示Dynamic Media列。
      ![列表视图和时间轴](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 选择性发布疑难解答 {#selective-publish-troubleshoot}

未同步到Dynamic Media但触发了Dynamic Media发布操作的资产会导致以下错误消息和解决方案：

![选择性发布错误](/help/assets/assets-dm/selective-publish-error.png)

