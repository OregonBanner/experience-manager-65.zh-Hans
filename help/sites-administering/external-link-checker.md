---
title: 链接检查器
description: 链接检查器有助于验证内部和外部链接，并允许链接重写。
translation-type: tm+mt
source-git-commit: 861cd74e1b2fd3d210647d83dee5d9a6fcead22a
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# 链接检查器{#the-link-checker}

内容作者不必担心验证其内容页面中包含的每个链接。

“链接检查器”会自动为内容作者提供链接，包括：

* 在链接添加到内容时验证链接
* 显示内容中所有外部链接的列表
* 执行链接转换

链路检查器具有许多[配置选项](#configuring)，如定义内部验证、允许在验证中忽略某些链接或链路路径以及重写链接重写规则。

链接检查器验证[内部链接](#internal)和[外部链接。](#external)

>[!NOTE]
>
>由于链接检查器检查每个内容页面的链接，因此链接检查器可能会影响大型存储库的性能。 在这种情况下，您可能需要[配置链接检查器运行](#configuring)或[的频率。](#disabling)

## 内部链路检查{#internal}

内部链接是指向AEM存储库中其他内容的链接。 内部链接可以使用RTE的路径选取器或使用自定义组件进行添加。 例如：

* 您的页面`/content/wknd/us/en/adventures/ski-touring.html`
* 在[文本组件中包含指向`/content/wknd/us/en/adventures/extreme-ironing.html`的链接。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

内容作者添加到页面的内部链接后，将立即验证内部链接。 如果链接变为无效：

* 它从发布者中删除。 链接文本将保留，但链接本身将被删除。
* 它在创作界面中显示为一个断开的链接。

![创作页面时断开内部链接](assets/link-checker-invalid-link-internal.png)

## 外部链路检查{#external}

外部链接是指向AEM存储库外的内容的链接。 外部链接可以使用RTE或使用自定义组件添加。 例如：

* 您的页面`/content/wknd/us/en/adventures/ski-touring.html`
* 在[文本组件中包含指向`https://bunwarmerthermalunderwear.com`的链接。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

外部链接会验证其语法并检查其可用性。 此检查在可配置的内部异步完成。 如果链接检查器发现外部链接无效：

* 它从发布者中删除。 链接文本将保留，但链接本身将被删除。
* 它在创作界面中显示为一个断开的链接。

![创作页面时断开内部链接](assets/link-checker-invalid-link-external.png)

此外，[外部链接检查器](#external-link-checker)界面还概述了内容页面上的所有外部链接。

### 使用外部链接检查器{#external-link-checker}

要使用外部链接检查器：

1. 使用&#x200B;**导航**，选择&#x200B;**工具**，然后选择&#x200B;**站点**。
1. 选择&#x200B;**外部链接检查器**，将显示所有外部链接的列表。

![](assets/external-link-checker.png)

将显示以下信息：

* **状态** -链接的验证状态
   * **有效** -链接检查器可以访问外部链接
   * **待定** -已将外部链接添加到站点内容，但尚未通过链接检查器验证
   * **无效** -链接检查器无法访问外部链接。
* **URL**  —— 外部链接
* **推荐人** -包含外部链接的内容页面
   * 如果已配置，则仅填充[。](#configuring)
* **上次检查** -链接检查器上次验证外部链接的时间
   * 可配置链接检查频率[。](#configuring)
* **上次状态** -当上次检查链接时返回的最后一个HTML状态代码
* **上次可用** -自上次链接可用于链接检查器以来的时间
* **上次访问** -自上次链接检查器访问链接以来的时间

您可以使用链接列表顶部的两个按钮来操作窗口的内容：

* **刷新** -刷新列表的内容
* **检查** -检查在列表中选择的单个外部链接

### 外部链接检查器的工作方式{#how-it-works}

外部链接检查器易于使用，但它依赖于许多服务并了解它们的工作方式，有助于您了解如何[配置链接检查器](#configuring)以满足您的需求。

1. 只要内容作者保存指向页面的任何链接，就会触发事件处理程序。
1. 事件处理函数遍历`/content`下的所有内容，检查新的或更新的链接，并将它们添加到链接检查器的缓存中。
1. 然后，**Day CQ Link Checker Service**&#x200B;在常规计划上执行，检查缓存中的条目是否有效语法。
1. 经过语法验证的链接随后会显示在[外部链接检查器](#external-link-checker)窗口中。 但是，它们将处于&#x200B;**Pending**&#x200B;状态。
1. 然后，**Day CQ链路检查器任务**&#x200B;定期执行，以通过进行GET调用来验证链路。
1. **Day CQ链接检查器任务**&#x200B;随后会使用GET调用的结果更新“外部链接检查器”窗口中的条目。

## 配置链接检查器{#configuring}

在AEM中，“链接检查器”自动现成可用。 但是，有许多OSGi配置可以修改以更改其行为：

* **Day CQ Link Checker Info Service**  —— 此服务定义存储库中链接检查器缓存的大小。
* **Day CQ Link Checker Service**  —— 此服务执行外部链接语法的异步检查。您可以定义检查期，检查器在其他选项中跳过哪些类型的链接。
* **第CQ天链接检查器任务** -此服务执行外部链接的GET验证。它允许对时间间隔进行单独定义，以检查其他选项之间的不良和良好链接。
* **Day CQ Link Checker Transformer**  —— 允许基于用户定义的规则集转换链接。

有关如何更改OSGi设置的更多详细信息，请参阅文档[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

## 禁用链接检查器{#disabling}

您可以选择完全禁用链接检查器。 为此，请执行以下操作：

1. 打开OSGi控制台。
1. 编辑&#x200B;**Day CQ链路检测器转换器**
1. 选中要禁用的选项：
   * **禁用检查** -禁用链接验证
   * **禁用重写** -禁用链接转换

>[!NOTE]
>
>如果在开始创建内容后禁用链接检查，您仍可能在[外部链接检查器窗口](#external-link-checker)中看到条目，但它们将不再更新。
