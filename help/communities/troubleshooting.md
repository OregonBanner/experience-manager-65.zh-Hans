---
title: 社群疑難排解
description: 疑難排解社群，包括已知問題
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# 社群疑難排解 {#troubleshooting}

本節包含疑難排解Community時的常見問題和已知問題。

## 已知问题 {#known-issues}

### Dispatcher重新擷取失敗 {#dispatcher-refetch-fails}

將Dispatcher 4.1.5與較新版本的Jetty搭配使用時，重新擷取可能會在等待請求逾時後導致「無法從遠端伺服器接收回應」。

使用Dispatcher 4.1.6或更新版本可解決此問題。

### 從CQ 5.4升級後無法存取論壇貼文 {#cannot-access-forum-post-after-upgrading-from-cq}

如果在CQ 5.4上建立了論壇並張貼了主題，然後網站升級為AEM 5.6.1或更新版本，嘗試檢視現有文章可能會導致頁面上的錯誤：

不合法的模式字元&#39;a&#39;無法將請求提供給 `/content/demoforums/forum-test.html` 和記錄檔包含下列專案：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題在於com.day.cq.commons.date.RelativeTimeFormat的格式字串在5.4和5.5之間已變更，使得「ago」的「a」不再被接受。

因此，使用RelativeTimeFormat() API的任何程式碼都必須變更：

* 发件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 收件人: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

作者和發佈的失敗情況不同。 在作者上，它會無訊息地失敗，並且不會顯示論壇主題。 發佈時，會在頁面上擲回錯誤。

請參閱 [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API以取得詳細資訊。

## 常見問題 {#common-concerns}

### 記錄檔中的警告：已棄用Handlebars {#warning-in-logs-handlebars-deprecated}

在啟動期間（不是第一次 — 但之後每次），可能會在記錄中看到以下警告：

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` 已取代為 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

此警告可以安全地忽略，因為 `jknack.handlebars.Handlebars`，使用者： [SCF](scf.md#handlebarsjavascripttemplatinglanguage)，隨附專屬的i18n helper公用程式。 啟動時，此變數會被AEM指定的變數取代 [i18n協助程式](handlebars-helpers.md#i-n). 此警告由第三方程式庫產生，以確認覆寫現有的協助程式。

### 記錄檔中的警告： OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

張貼多個Social Communities論壇主題可能會導致OakResourceListener processOsgiEventQueue的大量警告和資訊記錄。

可以安全地忽略這些警告。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### 記錄檔錯誤：IndexElementFactory的NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

將AEM 5.6.1 GA升級至最新的cq-socialcommunities-pkg-1.4.x或升級至AEM 6.0，會在啟動期間導致記錄檔中的狀況發生錯誤，此狀況會自我解決，其證據為重新啟動時未看到錯誤。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
