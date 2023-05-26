---
title: 链接检查器
description: Link Checker可帮助验证内部链接和外部链接，并允许链接重写。
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 0b9de3261d8747f3e7107962b6aea1dbdf9d6773
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# 链接检查器 {#the-link-checker}

内容作者无需自行验证其内容页面中包含的每个链接。

Link Checker会自动运行以帮助内容作者使用其链接，包括：

* 验证添加到内容的链接
* 显示内容中所有外部链接的列表
* 执行链接转换

链接检查器包含多个 [配置选项](#configuring) 例如，定义验证内部、允许在验证中忽略某些链接或链接模式，以及重写链接重写规则。

Link Checker验证两者 [内部链接](#internal) 和 [外部链接。](#external)

>[!NOTE]
>
>由于Link Checker会检查每个内容页面的链接，因此Link Checker可能会影响大型存储库的性能。 在这种情况下，您可能需要 [配置链接检查器运行的频率](#configuring) 或 [禁用它。](#disabling)

## 内部链接检查 {#internal}

内部链接是指向AEM存储库中其他内容的链接。 可以使用RTE中的路径选择器或使用自定义组件添加内部链接。 例如：

* 您的页面 `/content/wknd/us/en/adventures/ski-touring.html`
* 包含指向的链接 `/content/wknd/us/en/adventures/extreme-ironing.html` 在 [文本组件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

内容作者添加指向页面的内部链接后，将立即验证内部链接。 如果该链接无效：

* 已从发布器中将其删除。 链接文本会保留，但链接本身会被删除。
* 在创作界面中，该链接显示为断开的链接。

![创作页面时断开的内部链接](assets/link-checker-invalid-link-internal.png)

## 外部链接检查 {#external}

外部链接是指向AEM存储库外部内容的链接。 可以使用RTE或使用自定义组件添加外部链接。 例如：

* 您的页面 `/content/wknd/us/en/adventures/ski-touring.html`
* 包含指向的链接 `https://bunwarmerthermalunderwear.com` 在 [文本组件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

验证外部链接的语法和检查其可用性。 此检查在可配置的内部异步完成。 如果Link Checker发现外部链接无效：

* 已从发布器中将其删除。 链接文本会保留，但链接本身会被删除。
* 在创作界面中，该链接显示为断开的链接。

![创作页面时断开的内部链接](assets/link-checker-invalid-link-external.png)

此外， [外部链接检查程序](#external-link-checker) 界面提供了内容页面上所有外部链接的概述。

### 使用外部链接检查器 {#external-link-checker}

要使用外部链接检查器，请执行以下操作：

1. 使用 **导航**，选择 **工具**，则 **站点**.
1. 选择 **外部链接检查程序** 此时将显示所有外部链接的列表。

![外部链接检查器窗口](assets/external-link-checker.png)

将显示以下信息：

* **状态**  — 链接的验证状态，可以是以下状态之一：
   * **有效**  — 外部链接可通过链接检查器访问
   * **待处理**  — 外部链接已添加到站点内容，但尚未通过链接检查器验证
   * **无效**  — 链接检查器无法访问外部链接
* **URL**  — 外部链接
* **反向链接**  — 包含外部链接的内容页面
   * 仅填充 [如果已配置。](#configuring)
* **上次检查**  — 上次链接检查器验证外部链接的时间
   * 检查链接的频率 [可配置。](#configuring)
* **上次状态**  — 链接检查后上次检查外部链接时返回的最后HTML状态代码
* **上次可用**  — 链接上次对链接检查器可用的时间
* **上次访问**  — 自上次在创作界面中访问带有外部链接的页面以来的时间

您可以使用链接列表顶部的两个按钮来操作窗口内容：

* **刷新**  — 刷新列表内容
* **Check**  — 检查列表中选定的单个外部链接

### 外部链接检查器的工作原理 {#how-it-works}

尽管易于使用，但External Link Checker依赖于许多服务，并了解这些服务的工作方式有助于您了解如何 [配置Link Checker](#configuring) 以满足您的需求。

1. 每当内容作者保存指向页面的任何链接时，都会触发事件处理程序。
1. 事件处理程序遍历下的所有内容 `/content` 和会检查新链接或更新后的链接，并将它们添加到链接检查器的缓存中。
1. 此 **Day CQ链接检查器服务** 然后定期执行以检查缓存中的条目是否为有效语法。
1. 随后，经过语法验证的链接将显示在 [外部链接检查程序](#external-link-checker) 窗口。 但是，它们将 **待处理** 省/州。
1. 此 **Day CQ Link Checker任务** 然后定期执行，以通过进行GET调用来验证链接。
1. 此 **Day CQ Link Checker任务** 然后，使用GET调用的结果更新“外部链接检查器”窗口中的条目。

## 配置链接检查器 {#configuring}

链接检查器在AEM中可自动开箱即用。 但是，可以修改许多OSGi配置以更改其行为：

* **Day CQ链接检查器信息存储服务**  — 此服务定义存储库中Link Checker缓存的大小。
* **Day CQ链接检查器服务**  — 此服务执行外部链接语法的异步检查。 除了其他选项外，您还可以定义检查器跳过的检查时段和链接类型。
* **Day CQ Link Checker任务**  — 此服务执行外部链接的GET验证。 它允许单独定义间隔，以检查其他选项中的坏链接和好链接。
* **Day CQ链接检查器转换器**  — 允许根据用户定义的规则集转换链接。

查看文档 [OSGi配置](/help/sites-deploying/osgi-configuration-settings.md) 有关如何更改OSGi设置的更多详细信息。

## 禁用链接检查器 {#disabling}

您可以选择完全禁用Link Checker。 为此，请执行以下操作：

1. 打开OSGi控制台。
1. 编辑 **Day CQ链接检查器转换器**
1. 选中要禁用的选项：
   * **禁用检查**  — 禁用链接验证
   * **禁用重写**  — 禁用链接转换

>[!NOTE]
>
>如果在开始创建内容后禁用链接检查，您仍可能会看到 [“外部链接检查器”窗口](#external-link-checker)，但不会再更新它们。
