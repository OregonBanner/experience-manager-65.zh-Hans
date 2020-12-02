---
title: 解决 AEM 中有关创作方面的问题
seo-title: 解决 AEM 中有关创作方面的问题
description: 使用 AEM 时可能遇到的一些问题
seo-description: 使用 AEM 时可能遇到的一些问题
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 100%

---


# 解决 AEM 中有关创作方面的问题{#troubleshooting-aem-when-authoring}

以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。

>[!NOTE]
>
>遇到问题时，还可以查阅实例（发行版本或服务包）的[已知问题](/help/release-notes/known-issues.md)列表。

>[!NOTE]
>
>拥有管理员权限并希望解决 AEM 问题的用户可以使用 [AEM 疑难解答（适用于管理员）](/help/sites-administering/troubleshoot.md)中介绍的疑难解答方法。如果没有足够的权限，请咨询您的系统管理员以了解如何解决 AEM 问题。

## 发布网站上仍显示旧的页面版本 {#old-page-version-still-on-published-site}

* **问题**：

   * 您对某个页面进行了更改，并将该页面复制到发布站点，但发布站点中仍显示&#x200B;*旧*&#x200B;版页面。

* **原因**：

   * 这种情况可能有几个原因，最常见的原因是本地浏览器或调度程序缓存问题，但有时也可能是复制队列的问题。

* **解决方案**:

   * 这里列举了各种可能的情况：
   * 确认页面复制正确。检查页面状态，如有必要，检查复制队列的状态。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * 向页面 URL 的结尾处添加 `?`。例如：

      * `http://localhost:4502/sites.html/content?`
      * 这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。
   * 如果复制队列存在问题，请与系统管理员联系。


## 组件操作在工具栏上不可见 {#component-actions-not-visible-on-toolbar}

* **问题**：

   * 在创作环境中编辑内容页面时，所有适用的组件操作均不可见。

* **原因**：

   * 在极少数的情况下，之前的操作可能会影响工具栏。

* **解决方案**：

   * 刷新页面。

