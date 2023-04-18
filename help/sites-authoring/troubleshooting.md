---
title: 在AEM中创作时的疑难解答
description: 使用AEM时可能会遇到的一些问题。
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 42%

---

# 解决 AEM 中有关创作方面的问题{#troubleshooting-aem-when-authoring}

以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>遇到问题时，也值得查看 [已知问题](/help/release-notes/release-notes.md) 例如，您的实例（版本和Service Pack）。

>[!NOTE]
>
>具有管理员权限并想要解决AEM问题的用户可以使用 [AEM疑难解答（适用于管理员）](/help/sites-administering/troubleshoot.md). 如果您没有足够的权限，请与系统管理员联系，了解有关对AEM进行故障诊断的信息。

## 发布站点上仍显示旧的页面版本 {#old-page-version-still-on-published-site}

* **问题**：

   * 您已对页面进行了更改并将页面复制到发布站点，但 *旧* 发布网站上仍显示页面版本。

* **原因**:

   * 这可能有多种原因，通常是缓存（本地浏览器或调度程序），但有时可能是复制队列的问题。

* **解决方案**：

   * 这里有多种可能性：
   * 确认页面已正确复制。 检查页面状态，如有必要，检查复制队列的状态。
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
