---
title: 疑难解答
seo-title: 疑难解答
description: 社区故障诊断（包括已知问题）
seo-description: 社区故障诊断（包括已知问题）
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---

# 疑难解答 {#troubleshooting}

本节包含一些常见问题和已知问题。

## 已知问题 {#known-issues}

### Dispatcher重取失败{#dispatcher-refetch-fails}

将Dispatcher 4.1.5与较新版本的Jetty一起使用时，重新获取可能会在等待请求超时后导致“无法从远程服务器接收响应”。

使用Dispatcher 4.1.6或更高版本将解决此问题。

### 从CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}升级后无法访问论坛帖子

如果在CQ 5.4上创建论坛并发布了主题，然后将网站升级到AEM 5.6.1或更高版本，则尝试查看现有帖子可能会导致页面上出现错误：

非法模式字符“a”
无法向此服务器上的`/content/demoforums/forum-test.html`提供请求，并且日志包含以下内容：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

问题在于com.day.cq.commons.date.RelativeTimeFormat的格式字符串在5.4和5.5之间发生了更改，以便不再接受“ago”的“a”。

因此，使用RelativeTimeFormat()API的任何代码都需要更改：

* 发件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 收件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

创作和发布失败的情况不同。 创作时，该过程会静默失败，而且只会不显示论坛主题。 在发布时，它会在页面上引发错误。

有关更多信息，请参阅[com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API 。

## 常见问题{#common-concerns}

### 日志中的警告：已弃用的Handlebars {#warning-in-logs-handlebars-deprecated}

在启动期间（不是第1次，但是之后每次启动），日志中可能会显示以下警告：

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 已被  `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

此警告可以安全地忽略，因为[SCF](scf.md#handlebarsjavascripttemplatinglanguage)使用的`jknack.handlebars.Handlebars`是其自带的i18n帮助程序实用程序。 启动时，它被替换为特定于AEM的[i18n帮助程序](handlebars-helpers.md#i-n)。 此警告由第三方库生成，用于确认覆盖现有帮助程序。

### 日志中的警告：OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

发布大量社交社区论坛主题可能会从OakResourceListener processOsgiEventQueue中生成大量警告和信息日志。

可以安全地忽略这些警告。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 日志中出错：IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}的NoClassDefFoundError

将AEM 5.6.1 GA升级到最新的cq-socialcommunities-pkg-1.4.x或AEM 6.0时，在启动期间，如果某个条件会自行解析，则日志文件中会出现错误，这是重新启动时未看到的错误所证明的。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
