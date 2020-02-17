---
title: 外部提供商的分析
seo-title: 外部提供商的分析
description: 了解与外部提供商的Analytics。
seo-description: 了解与外部提供商的Analytics。
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# 外部提供商的分析 {#analytics-with-external-providers}

Analytics可为您提供有关网站使用情况的重要而有趣的信息。

各种现成配置可用于与相应的服务集成，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您还可以配置自己的通用分析代码 **片段实例** ，以定义新的服务配置。

然后，通过添加到网页的小代码片段来收集信息。 例如：

>[!CAUTION]
>
>脚本不能包含在标记 `script` 中。

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

这样的片段使得能够收集数据并生成报告。 收集的实际数据取决于提供者和使用的实际代码片断。 统计数据示例包括：

* 一段时间内有多少访客
* 访问页数
* 使用的搜索词
* 登陆页面

>[!CAUTION]
>
>配置Geometrixx-Outdoors演示站点，以便将“页面属性”中提供的属性附加到相应脚本中的html源代码(刚好在 `</html>` endtag的上方) `js` 中。

>如果您自 `/apps` 己不继承默认的页面组件( `/libs/foundation/components/page`)，您（或您的开发人员）必须确保包括相应的脚本，例如，通过包括或使用类似机制 `js``cq/cloudserviceconfigs/components/servicescomponents`来包含这些脚本。
>
>如果没有此选项，则任何服务（通用、分析、目标等）都无法正常工作。

## 使用通用代码片断创建新服务 {#creating-a-new-service-with-a-generic-snippet}

对于基本配置：

1. Open the **Tools** console.
1. 从左侧窗格展开“ **云服务配置”**。
1. 双击“通用分 **析代码片断** ”以打开页面：

   ![](assets/analytics_genericoverview.png)

1. 单击+，使用对话框添加新配置；至少分配一个名称，例如google分析：

   ![](assets/analytics_addconfig.png)

1. 单击 **创建**，代码片断对话框将立即打开——将相应的javascript代码片断粘贴到字段中：

   ![](assets/analytics_snippet.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 在页面上使用新服务 {#using-your-new-service-on-pages}

创建服务配置后，您现在需要配置所需的页面才能使用它：

1. 导航到页面。
1. 从Sidekick中 **打开页面属性** ，然后打开云 **服务选项卡** 。
1. 单击 **添加服务**，然后选择所需的服务；例如，“通用 **分析代码片断”**:

   ![](assets/analytics_selectservice.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。
1. 您将返回到“云服务 **”选项卡** 。 通用 **分析代码片断** ，现在会随消息一起列出 `Configuration reference missing`。 使用下拉列表选择您的特定服务实例；例如google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

   现在，如果查看页面的页面源，则可以查看该片段。

   经过适当的时间段后，您将能够查看已收集的统计信息。

   >[!NOTE]
   如果配置附加到具有子页面的页面，则这些页面也会继承该服务。
