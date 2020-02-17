---
title: 解决 AEM 中有关创作方面的问题
seo-title: 解决 AEM 中有关创作方面的问题
description: 以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。
seo-description: 以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

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

* **解决方案**：

   * 这里列举了各种可能的情况：
   * 确认页面复制正确。检查页面状态，如有必要，检查复制队列的状态。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * Add `?` to the end of the page URL. For example:

      `http://localhost:4502/sites.html/content?`

      这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。

   * 如果复制队列存在问题，请与系统管理员联系。

## Sidekick 不可见 {#sidekick-not-visible}

* **问题**：

   * 在创作环境中编辑内容页面时，Sidekick 不可见。

* **原因**：

   * 在少数情况下，您可能将 Sidekick 标头放在了当前窗口的范围之外。这会导致您无法重新调整其位置。

* **解决方案**：

   * 从当前会话注销，然后重新登录。Sidekick 将返回到默认位置。

## 查找并替换 - 未替换所有实例 {#find-replace-not-all-instances-are-replaced}

* **问题：**

   * When using the **Find &amp; Replace** option it can happen that not all instances of the `find` term are replaced on a page.

* **原因**：

   * **查找并替换**&#x200B;的功能取决于内容的保存方式以及内容是否可搜索。例如，博客文本是以 `jcr:text` 属性存储的，而该属性未配置为可搜索。查找并替换 servlet 的默认范围涵盖以下属性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解决方案**：

   * 可使用“**Web 控制台**”通过 **Day CQ WCM 查找替换 Servlet** 的配置来更改这些定义；例如，在

      `http://localhost:4502/system/console/configMgr`

