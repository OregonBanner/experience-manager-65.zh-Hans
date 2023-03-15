---
title: Analytics与外部提供程序
seo-title: Analytics with External Providers
description: 了解使用外部提供程序的Analytics。
seo-description: Learn about Analytics with External Providers.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# Analytics与外部提供程序 {#analytics-with-external-providers}

Analytics可向您提供有关网站的使用方式的重要且有趣的信息。

各种现成的配置可用于与相应的服务集成，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您还可以配置自己的实例 **通用Analytics代码片段** 以定义新的服务配置。

然后，通过添加到网页中的代码小片段来收集信息。 例如：

>[!CAUTION]
>
>脚本不得包含在 `script` 标记之间。

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

通过此类片段，可以收集数据并生成报告。 实际收集的数据取决于提供商和实际使用的代码段。 统计信息示例包括：

* 一段时间内访客的数量
* 访问的页面数量
* 使用的搜索词
* 登陆页面

>[!CAUTION]
>
>Geometrixx-Outdoors演示站点已进行配置，以便“页面属性”中提供的属性被附加到html源代码中(位于 `</html>` endtag) `js` 脚本。
>
>如果您自己的 `/apps` 不继承自默认页面组件( `/libs/foundation/components/page`)您（或您的开发人员）必须确保 `js` 包含脚本，例如，通过包含 `cq/cloudserviceconfigs/components/servicescomponents`，或使用类似的机制。
>
>没有它，任何服务（通用、Analytics、Target等）都无法正常工作。

## 使用通用代码片段创建新服务 {#creating-a-new-service-with-a-generic-snippet}

对于基本配置：

1. 打开 **工具** 控制台。
1. 从左窗格展开 **Cloud Services配置**.
1. 双击 **通用Analytics代码片段** 要打开页面，请执行以下操作：

   ![](assets/analytics_genericoverview.png)

1. 单击+以使用对话框添加新配置；至少指定一个名称，例如google analytics：

   ![](assets/analytics_addconfig.png)

1. 单击 **创建**，将会立即打开代码片段对话框 — 将相应的javascript代码片段粘贴到字段中：

   ![](assets/analytics_snippet.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 在页面上使用新服务 {#using-your-new-service-on-pages}

创建服务配置后，您现在需要配置所需的页面才能使用它：

1. 导航到页面。
1. 打开 **页面属性** 从sidekick，然后 **Cloud Services** 选项卡。
1. 单击 **添加服务**，然后选择所需的服务；例如 **通用Analytics代码片段**：

   ![](assets/analytics_selectservice.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。
1. 您将会返回到 **Cloud Services** 选项卡。 此 **通用Analytics代码片段** 现在与消息一起列出 `Configuration reference missing`. 使用下拉列表选择您的特定服务实例；例如google-analytics：

   ![](assets/analytics_selectspecificservice.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

   现在，如果您查看页面的页面源，则可以看到该代码片段。

   经过适当的时间段后，您将能够查看已收集的统计数据。

   >[!NOTE]
   >
   >如果将配置附加到具有子页面的页面，则这些页面也会继承服务。
