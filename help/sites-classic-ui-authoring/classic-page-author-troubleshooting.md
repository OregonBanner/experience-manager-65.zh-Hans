---
title: 解决AEM中有关创作方面的问题
description: 以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 27%

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

* **原因**：

   * 这可能有多种原因，通常是缓存（本地浏览器或Dispatcher），但有时也可能是复制队列问题。

* **解决方案**：

   * 下面提供了多种可能性：
   * 确认已正确复制该页面。 检查页面状态，并在必要时检查复制队列的状态。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * 向页面 URL 的结尾处添加 `?`。例如：

     `http://localhost:4502/sites.html/content?`

     这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。

   * 如果复制队列存在问题，请与系统管理员联系。

## Sidekick不可见 {#sidekick-not-visible}

* **问题**：

   * 在创作环境中编辑Sidekick页面时，内容不可见。

* **原因**：

   * 在极少数情况下，您可能会将Sidekick的标头放在当前窗口的范围之外。 这意味着您无法再次调整其位置。

* **解决方案**：

   * 注销当前会话并重新登录。 Sidekick将返回到默认位置。

## 查找并替换 — 并非所有实例都将被替换 {#find-replace-not-all-instances-are-replaced}

* **问题：**

   * 使用时 **查找并替换** 选项，可能并非所有的 `find` 替换页面上的术语。

* **原因**：

   * 的功能 **查找并替换** 取决于内容的保存方式以及是否可搜索内容。 例如，博客文本存储在 `jcr:text` 未配置为要搜索的属性。 查找和替换servlet的默认范围包括以下属性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解决方案**：

   * 可以使用配置更改这些定义 **Day CQ WCM查找替换Servlet** 使用 **Web控制台**；例如，

     `http://localhost:4502/system/console/configMgr`
