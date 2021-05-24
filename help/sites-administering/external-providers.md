---
title: Analytics与外部提供程序
seo-title: Analytics与外部提供程序
description: 了解Analytics与外部提供程序。
seo-description: 了解Analytics与外部提供程序。
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
source-wordcount: '442'
ht-degree: 3%

---

# Analytics与外部提供程序{#analytics-with-external-providers}

Analytics可以为您提供有关网站使用方式的重要且有趣的信息。

各种开箱即用的配置可用于与相应的服务集成，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您还可以配置自己的&#x200B;**通用Analytics代码片段**&#x200B;实例，以定义新的服务配置。

然后，通过添加到网页的代码片段来收集信息。 例如：

>[!CAUTION]
>
>脚本不得包含在`script`标记中。

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

这样的代码片段可以收集数据并生成报告。 收集的实际数据取决于提供程序和使用的实际代码段。 示例统计信息包括：

* 一段时间内的访客人数
* 访问的页数
* 使用的搜索词
* 登陆页面

>[!CAUTION]
>
>配置了Geometrixx-Outdoors演示网站，以便将“页面属性”中提供的属性附加到相应`js`脚本中的html源代码（紧靠`</html>` endtag上方）。
>
>如果您自己的`/apps`不从默认的页面组件(`/libs/foundation/components/page`)继承，则您（或您的开发人员）必须确保包含相应的`js`脚本，例如通过包含`cq/cloudserviceconfigs/components/servicescomponents`或使用类似机制。
>
>如果没有此功能，则任何服务（通用、Analytics、Target等）都将无法正常运行。

## 使用通用代码片段{#creating-a-new-service-with-a-generic-snippet}创建新服务

对于基本配置：

1. 打开&#x200B;**工具**&#x200B;控制台。
1. 从左窗格展开&#x200B;**Cloud Services配置**。
1. 双击&#x200B;**通用Analytics代码片段**&#x200B;以打开页面：

   ![](assets/analytics_genericoverview.png)

1. 单击+以使用对话框添加新配置；至少分配一个名称，例如google analytics:

   ![](assets/analytics_addconfig.png)

1. 单击&#x200B;**创建**，将立即打开代码片段对话框 — 将相应的Javascript代码片段粘贴到字段中：

   ![](assets/analytics_snippet.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 在{#using-your-new-service-on-pages}页面上使用新服务

创建了服务配置后，您现在需要配置所需的页面才能使用它：

1. 导航到页面。
1. 从Sidekick中打开&#x200B;**页面属性** ，然后打开&#x200B;**Cloud Services**&#x200B;选项卡。
1. 单击&#x200B;**添加服务**，然后选择所需的服务；例如，**通用Analytics代码片段**:

   ![](assets/analytics_selectservice.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。
1. 您将返回到&#x200B;**Cloud Services**&#x200B;选项卡。 **常规Analytics代码片段**&#x200B;现在随消息`Configuration reference missing`一起列出。 使用下拉列表选择您的特定服务实例；例如google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

   现在，如果您查看页面的页面源，则可以查看代码片段。

   在经过适当的时间段后，您将能够查看已收集的统计资料。

   >[!NOTE]
   >
   >如果配置附加到具有子页面的页面，则这些页面也会继承该服务。
