---
title: AEM Sites - GDPR就绪
seo-title: AEM Sites - GDPR就绪
description: 了解有关为AEM Sites做好GDPR准备的详细信息。
seo-description: 了解有关为AEM Sites做好GDPR准备的详细信息。
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# AEM Sites - GDPR就绪{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR用作以下部分的示例，但相关详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等

欧盟的《数据隐私权通用数据保护条例》已于2018年5月正式生效。

AEM Sites随时准备帮助客户履行其GDPR合规义务。 本页面将指导客户完成在AEM Sites中处理GDPR请求的过程。 它描述了存储的专用数据的位置，以及如何手动或使用代码删除这些数据。

有关更多信息，请参阅Adobe隐私中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[GDPR页面。

>[!NOTE]
>
>有关更多详细信息，请参阅[AEM GDPR就绪](/help/managing/data-protection-and-privacy.md)。

## 作者服务器{#author-server}

[Platform GDPR文档](/help/managing/data-protection-and-privacy.md)中介绍了作者服务器上的用户帐户和UGC内容。

## 发布服务器{#publish-server}

[平台GDPR文档](/help/managing/data-protection-and-privacy.md)中介绍用于验证网站访客和发布服务器上UGC内容的用户帐户。

默认情况下，AEM Sites组件不存储访客在发布服务器上输入的表单数据。 建议将数据转发到第三方系统或Adobe Campaign以进行进一步处理。

## 选择启用/选择禁用{#opt-in-opt-out}

AEM具有[cookie选择退出服务](/help/sites-developing/cookie-optout.md) ，可用于管理用户的选择加入/选择退出。

## Analytics的增强分析功能{#enhanced-insights-by-analytics}

AEM Sites包含与Analytics“增强的分析”的可选集成，后者使用Adobe Analytics按需服务中的功能。

有关管理与Adobe Analytics相关的GDPR数据主体请求的更多信息，请参阅[Adobe Analytics和GDPR](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)。

## 按Target增强的个性化{#enhanced-personalization-by-target}

AEM Sites包含与Enhanced Personalization by Target的可选集成，后者使用Adobe Target On-demand Service中的功能。

有关管理与Adobe Target相关的GDPR数据主体请求的更多信息，请参阅[Adobe Target — 隐私和《通用数据保护条例》](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

AEM提供了一个可选的数据层，其中包含[ContextHub](/help/sites-developing/contexthub.md)。 这会保留浏览器中特定于访客的数据，以便用于基于规则的个性化。

默认情况下，此访客数据不存储在AEM中；AEM会向数据层发送规则，以便在浏览器中做出个性化决策。

>[!NOTE]
>
>在Adobe CQ 5.6之前，ClientContext（ContextHub的早期版本）确实将数据发送到了服务器，但并未存储这些数据。
>
>Adobe CQ 5.5及更早版本现在处于生命周期终止状态，且未包含在本文档中。

### 实施选择启用/选择禁用{#implementing-opt-in-opt-out}

站点所有者需要根据以下准则实施选择退出组件。

这些准则将选择加入作为默认实施。 因此，在将任何个人数据存储到浏览器的（客户端）持久性中之前，网站访客必须明确同意。

* 每次包含ContextHub组件时，都应包含选择退出组件。
* 与网站GDPR相关的条款和条件必须显示给网站访客，以便他们能够：

   * 接受
   * 拒绝
   * 更改其先前的选择

* 如果网站访客接受网站的条款和条件，则应删除ContextHub选择退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果网站访客不接受网站的条款和条件，则应设置ContextHub选择退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要检查ContextHub是否在选择退出模式下运行，应在浏览器控制台中进行以下调用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 预览ContextHub {#previewing-persistence-of-contexthub}的持久性

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台；例如：

   * 铬黄：

      * 打开开发人员工具>应用程序>存储：

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookie >（网站）> SessionPersistence
   * Firefox:

      * 打开开发人员工具>存储：

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookie >（网站）> SessionPersistence
   * Safari:

      * 在菜单栏中打开“首选项”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示JavaScript控制台”

         * 控制台>存储>本地存储>（网站）> ContextHubPersistence
         * 控制台>存储>会话存储>（网站）> ContextHubPersistence
         * 控制台>存储> Cookie >（网站）> ContextHubPersistence
   * Internet Explorer:

      * 打开开发人员工具>控制台

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* 在浏览器控制台中使用ContextHub API:

   * ContextHub提供以下数据持久层：

      * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub存储定义将使用哪个持久层，以便查看持久层的当前状态，所有层都应被检查。


例如，要查看存储在localStorage中的数据，请执行以下操作：

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台：

   * Chrome — 打开开发人员工具>应用程序>存储：

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookie >（网站）> SessionPersistence
   * Firefox — 打开开发人员工具>存储：

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookie >（网站）> SessionPersistence


* 在浏览器控制台中使用ContextHub API:

   * ContextHub提供以下数据持久层：

      * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      ContextHub存储定义将使用哪个持久层，以便查看持久层的当前状态，所有层都应被检查。


例如，要查看存储在localStorage中的数据，请执行以下操作：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub {#clearing-persistence-of-contexthub}的持久性

要清除ContextHub持久性，请执行以下操作：

* 要清除当前已加载存储的持久性，请执行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定持久层；例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久层，必须为所有层调用相应的代码：

   * ContextHub.Utils.Persistence.Modes.LOCAL（默认）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
