---
title: 开发和页面差异
description: 开发和页面差异
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 10%

---

# 开发和页面差异{#developing-and-page-diff}

## 功能概述 {#feature-overview}

内容创建是一个迭代过程。要进行高效创作，需要能够发现从一次迭代到另一次迭代所发生的更改。逐个查看页面版本的方式效率低下且容易出错。作者希望能够并排比较当前页面与先前版本，并突出显示差异。

页面差异允许用户将当前页面与启动项、先前版本等进行比较。 有关此用户功能的详细信息，请参阅 [页面差异](/help/sites-authoring/page-diff.md).

## 操作详细信息 {#operation-details}

当比较页面的版本时，用户希望比较的先前版本由AEM在后台重新创建，以促进差异。 需要此项才能渲染内容 [用于并排比较](/help/sites-developing/pagediff.md#operation-details).

此娱乐操作由AEM在内部完成，对用户是透明的，无需干预。 但是，查看存储库的管理员(例如，在CRXDE Lite中)会在内容结构中看到这些重新创建的版本。

比较内容时，将在以下位置重新创建截至要比较的页面的整个树：

`/tmp/versionhistory/`

自动运行清理任务以清理此临时内容。

## 权限 {#permissions}

以前，在经典UI中，必须考虑特殊开发考虑以便于AEM差异(例如使用 `cq:text` 标记库，或自定义集成 `DiffService` OSGi服务转换为组件)。 新的diff功能不再需要此项，因为差异是通过DOM比较在客户端发生的。

但是，开发人员必须考虑一些限制。

* 此功能使用的CSS类没有命名空间到AEM产品。 如果页面上包含其他具有相同名称的自定义CSS类或第三方CSS类，则差异的显示可能会受到影响。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由于diff是客户端的，并在页面加载时执行，因此不会考虑在客户端差异服务运行后对DOM所做的任何调整。 这可能会影响

   * 使用AJAX包含内容的组件
   * 单页面应用程序
   * 基于JavaScript的组件，可在用户交互时处理DOM。

>[!NOTE]
>
>页面差异比较仅适用于具有有效cq：editConfig节点的组件。
