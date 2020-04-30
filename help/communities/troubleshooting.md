---
title: 疑难解答
seo-title: 疑难解答
description: 社区疑难解答（包括已知问题）
seo-description: 社区疑难解答（包括已知问题）
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 疑难解答 {#troubleshooting}

本节包含常见问题和已知问题。

## 已知问题 {#known-issues}

### 调度程序重取失败 {#dispatcher-refetch-fails}

当将Dispatcher 4.1.5与Jetty的较新版本一起使用时，在等待请求超时后，重取可能导致“无法从远程服务器接收响应”。

使用Dispatcher 4.1.6或更高版本可解决此问题。

### 从CQ 5.4升级后无法访问论坛帖子 {#cannot-access-forum-post-after-upgrading-from-cq}

如果在CQ 5.4上创建了论坛并发布了主题，然后将站点升级到AEM 5.6.1或更高版本，则尝试视图现有帖子可能会导致页面上出现错误：

非法模式字符&#39;a&#39;不能在此服务器上向 `/content/demoforums/forum-test.html` 该服务器发送请求，且日志包含以下内容：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

问题是com.day.cq.commons.date.RelativeTimeFormat的格式字符串在5.4和5.5之间发生了更改，以便不再接受“ago”的“a”。

因此，使用RelativeTimeFormat()API的任何代码都需要更改：

* 发件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 收件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

创作和发布时失败有所不同。 创作时，它将失败且不显示论坛主题。 在发布时，它会在页面上引发错误。

有关更 [多信息，请参阅com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API。

## 常见问题 {#common-concerns}

### 日志中的警告：已弃用Handlebars {#warning-in-logs-handlebars-deprecated}

在启动过程中（不是第1次启动，但之后每次启动），日志中可能会显示以下警告：

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 已替换为 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

由于 `jknack.handlebars.Handlebars`SCF [（自带i18n辅助实用程序）](scf.md#handlebarsjavascripttemplatinglanguage)使用，因此可以安全地忽略此警告。 开始时，它将替换为特定于AEM的 [i18n帮助程序](handlebars-helpers.md#i-n)。 此警告由第三方库生成，用于确认对现有助手的覆盖。

### 日志中的警告：OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

发布大量社交社区论坛主题可能会导致OakResourceListener processOsgiEventQueue中大量的警告和信息日志。

这些警告可以安全地忽略。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 日志中出错：IndexElementFactory的NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

将AEM 5.6.1 GA升级到最新的cq-socialcommunities-pkg-1.4.x或AEM 6.0会在启动过程中导致日志文件中出现错误，该情况将解析自身，以重新启动时未看到错误为证。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
