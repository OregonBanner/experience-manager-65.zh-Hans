---
title: 开发和页面差异
seo-title: 开发和页面差异
description: 'null'
seo-description: 'null'
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 开发和页面差异{#developing-and-page-diff}

## 功能概述 {#feature-overview}

内容创建是一个迭代过程。要进行高效创作，需要能够发现从一次迭代到另一次迭代所发生的更改。逐个查看页面版本的方式效率低下且容易出错。作者希望能够并排比较当前页面与先前版本，并突出显示差异。

页面差异允许用户将当前页面与启动项、先前版本等进行比较。 有关此用户功能的详细信息，请参阅 [页面差异](/help/sites-authoring/page-diff.md)。

## 操作详细信息 {#operation-details}

在比较页面版本时，AEM会在后台重新创建用户希望进行比较的先前版本，以便进行比较。 这需要能够呈现内容以 [进行并排比较](/help/sites-developing/pagediff.md#operation-details)。

此休闲操作由AEM在内部完成，对用户是透明的，无需任何干预。 但是，查看存储库（例如在CRX DE Lite中）的管理员可以在内容结构中看到这些重新创建的版本。

比较内容时，将在以下位置重新创建整个树到要比较的页面：

`/tmp/versionhistory/`

自动运行清除任务以清除此临时内容。

## 权限 {#permissions}

以前，在经典UI中，必须考虑特殊开发因素以便利AEM差异化(如使用标签库或将 `cq:text``DiffService` OSGi服务自定义集成到组件中)。 由于差异是通过DOM比较在客户端进行，因此新差异功能不再需要此功能。

但是，开发人员需要考虑许多限制。

* 此功能使用与AEM产品无间隔的CSS类。 如果页面中包含具有相同名称的其他自定义CSS类或第三方CSS类，则差异的显示可能会受到影响。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由于差异是客户端，并在页面加载时执行，因此在客户端差异服务运行后对DOM所做的任何调整都不会被计入。 这可能会影响

   * 使用AJAX包含内容的组件
   * 单页应用程序
   * 在用户交互时操作DOM的基于Javascript的组件。
