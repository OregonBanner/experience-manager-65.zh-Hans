---
title: AEM Sites- GDPR就绪性
seo-title: AEM Sites- GDPR就绪性
description: 了解AEM SitesGDPR准备情况的详细信息。
seo-description: 了解AEM SitesGDPR准备情况的详细信息。
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---


# AEM Sites- GDPR就绪性{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下各节中用作示例，但涵盖的详细信息适用于所有数据保护和隐私法规； 例如GDPR、CCPA等。

欧洲合并的《数据隐私权一般数据保护规定》自2018年5月起生效。

AEM Sites愿意帮助客户履行GDPR合规义务。 本页指导客户完成AEM Sites中处理GDPR请求的过程。 它描述了存储的私有数据的位置，以及如何手动或使用代码删除这些数据。

有关详细信息，请 [参阅Adobe隐私中心的GDPR页面](https://www.adobe.com/privacy/general-data-protection-regulation.html)。

>[!NOTE]
>
>有关更 [多详细信息，请参阅](/help/managing/data-protection-and-privacy.md) AEM GDPR就绪性。

## 作者服务器 {#author-server}

创作服务器上的用户帐户和UGC内容在PlatformGDPR文 [档中介绍](/help/managing/data-protection-and-privacy.md)。

## 发布服务器 {#publish-server}

用于验证站点上访客的用户帐户以及发布服务器上的UGC内容的用户帐户在 [PlatformGDPR文档中介绍](/help/managing/data-protection-and-privacy.md)。

默认情况下，AEM Sites组件不存储访客在发布服务器上输入的表单数据。 建议将数据转发给第三方系统或Adobe Campaign以进一步处理。

## 选择加入／选择退出 {#opt-in-opt-out}

AEM提供 [了cookie选择退出服务](/help/sites-developing/cookie-optout.md) ，可用于管理用户的选择加入／选择退出。

## 增强了Analytics的洞察 {#enhanced-insights-by-analytics}

AEM Sites可选地与Analytics的“增强的洞察”集成，后者使用AdobeAnalytics点播服务中的功能。

有关管理与Adobe Analytics相关的GDPR数据主体请求的更多信息，请 [参阅AdobeAnalytics和GDPR](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)。

## 通过Target增强个性化 {#enhanced-personalization-by-target}

AEM Sites包括Target与增强个性化的可选集成，该集成使用Adobe Target点播服务中的功能。

有关管理与Adobe Target相关的GDPR数据主体请求的更多信息，请 [参阅Adobe Target-隐私和一般数据保护规定](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

AEM为ContextHub提供可选数 [据层](/help/sites-developing/contexthub.md)。 这会在浏览器中保留特定于访客的数据，以便用于基于规则的个性化。

默认情况下，此访客数据不存储在AEM中； AEM将规则发送到数据层，以便在浏览器中做出个性化决策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（ContextHub的较早版本）确实会将数据发送到服务器，但并未存储它们。
>
>Adobe CQ 5.5及更早版本现已EOL，本文档未涵盖此版本。

### 实施加入／退出 {#implementing-opt-in-opt-out}

站点所有者需要根据以下准则实施退出组件。

这些准则将选择加入作为默认实施。 因此，网站访客必须明确同意，然后才能将任何个人数据存储在浏览器的（客户端）持久性中。

* 每次包含ContextHub组件时都应包含退出组件。
* 与网站的GDPR相关的条款和条件必须显示在网站访客，允许他们：

   * 接受
   * 拒绝
   * 更改前一选择

* 如果站点访客接受站点的条款和条件，则应删除ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果站点访客不接受该站点的条款和条件，则应设置ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要检查ContextHub是否在退出模式下运行，应在浏览器的控制台中进行以下调用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 预览ContextHub的持久性 {#previewing-persistence-of-contexthub}

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台； 例如：

   * 铬黄：

      * 打开“开发人员工具”>“应用程序”>“存储”:

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookies >（网站）> SessionPersistence
   * Firefox:

      * 打开“开发人员工具”>“存储”:

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookies >（网站）> SessionPersistence
   * Safari:

      * 打开菜单栏中的“首选项”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示JavaScript控制台”

         * “控制台”>“存储”>“本地存储”>（网站）> ContextHubPersistence
         * “控制台”>“存储”>“会话存储”>（网站）> ContextHubPersistence
         * 控制台>存储> Cookies >（网站）> ContextHubPersistence
   * Internet Explorer:

      * 打开“开发人员工具”>“控制台”

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* 使用浏览器控制台中的ContextHub API:

   * ContextHub提供以下数据持久性层：

      * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub存储定义将使用的持久性层，因此，应检查所有层的持久性的当前状态。


例如，要视图存储在localStorage中的数据：

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台：

   * Chrome —— 打开“开发人员工具”>“应用程序”>“存储”:

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookies >（网站）> SessionPersistence
   * Firefox —— 打开“开发人员工具”>“存储”:

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookies >（网站）> SessionPersistence


* 使用浏览器控制台中的ContextHub API:

   * ContextHub提供以下数据持久性层：

      * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub存储定义将使用的持久性层，因此，应检查所有层的持久性的当前状态。


例如，要视图存储在localStorage中的数据：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的持久性 {#clearing-persistence-of-contexthub}

要清除ContextHub持久性，请执行以下操作：

* 清除当前加载的存储的持久性：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定的持久性层； 例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久性层，必须为所有层调用相应的代码：

   * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

