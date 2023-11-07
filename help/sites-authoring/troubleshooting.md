---
title: 在AEM中创作时疑难解答
description: 您在使用AEM时可能会遇到的一些问题。
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 42%

---

# 解决 AEM 中有关创作方面的问题{#troubleshooting-aem-when-authoring}

以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>如果遇到问题，也值得检查 [已知问题](/help/release-notes/release-notes.md) 适用于您的实例（发行版和Service Pack）。

>[!NOTE]
>
>具有管理员权限的用户以及希望对AEM问题进行故障排除的用户，可以使用中所述的故障排除方法 [AEM故障诊断（适用于管理员）](/help/sites-administering/troubleshoot.md). 如果您没有足够的权限，请与系统管理员联系，了解有关AEM疑难解答的信息。

## 发布站点上仍显示旧的页面版本 {#old-page-version-still-on-published-site}

* **问题**：

   * 您已经更改了一个页面，并将该页面复制到发布站点，但是 *旧* 发布网站上仍显示该页面的版本。

* **原因**:

   * 这可能有多种原因，通常是缓存（本地浏览器或Dispatcher），但有时也可能是复制队列问题。

* **解决方案**：

   * 下面提供了多种可能性：
   * 确认已正确复制该页面。 检查页面状态，并在必要时检查复制队列的状态。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * 向页面 URL 的结尾处添加 `?`。例如：

      * `http://localhost:4502/sites.html/content?`
      * 这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。

   * 如果复制队列存在问题，请与系统管理员联系。

## 组件操作在工具栏上不可见 {#component-actions-not-visible-on-toolbar}

* **问题**：

   * 在创作环境中编辑内容页面时，所有适用的组件操作均不可见。

* **原因**:

   * 在极少数情况下，之前的操作可能会影响工具栏。

* **解决方案**:

   * 刷新页面。
