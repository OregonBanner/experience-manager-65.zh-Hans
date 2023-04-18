---
title: 解决AEM创作问题
description: 以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 29%

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

      `http://localhost:4502/sites.html/content?`

      这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。

   * 如果复制队列存在问题，请与系统管理员联系。

## Sidekick不可见 {#sidekick-not-visible}

* **问题**：

   * 在创作环境中编辑内容页面时，Sidekick不可见。

* **原因**:

   * 在极少数情况下，您可能已将Sidekick的标题放在当前窗口的范围之外。 这表示您无法重新调整其位置。

* **解决方案**:

   * 从当前会话注销，然后重新登录。 Sidekick将返回到默认位置。

## 查找并替换 — 并非替换所有实例 {#find-replace-not-all-instances-are-replaced}

* **问题:**

   * 使用 **查找和替换** 选项，并非所有实例 `find` 术语会在页面上替换。

* **原因**:

   * 的 **查找和替换** 取决于内容的保存方式以及内容是否可搜索。 例如，博客文本存储在 `jcr:text` 未配置为搜索的属性。 查找和替换Servlet的默认范围涵盖以下属性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解决方案**:

   * 这些定义可通过 **Day CQ WCM查找替换Servlet** 使用 **Web控制台**;例如，在

      `http://localhost:4502/system/console/configMgr`
