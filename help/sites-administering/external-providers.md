---
title: Analytics与外部提供程序
description: 了解如何配置您自己的通用分析代码片段实例，以定义新的服务配置。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# Analytics与外部提供程序 {#analytics-with-external-providers}

Analytics可向您提供有关您网站的使用方式的重要且有趣的信息。

各种现成的配置可用于与相应的服务集成，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您也可以配置自己的实例 **通用Analytics片段** 以定义新的服务配置。

然后，通过添加到网页中的代码小片段来收集信息。 例如：

>[!CAUTION]
>
>请勿将脚本包含在 `script` 标记之间。

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

通过此类片段，可以收集数据并生成报表。 实际收集的数据取决于提供商和实际使用的代码段。 示例统计信息包括：

* 一段时间内访客的数量
* 已访问页面的数量
* 使用的搜索词
* 登陆页面

>[!CAUTION]
>
>Geometrixx-Outdoors演示站点已进行配置，因此在“页面属性”中提供的属性已附加到html源代码中(位于 `</html>` 结束标记) `js` 脚本。
>
>如果您自己的 `/apps` 不继承默认页面组件( `/libs/foundation/components/page`)您（或您的开发人员）必须确保 `js` 通过包含脚本来包含脚本，例如 `cq/cloudserviceconfigs/components/servicescomponents`，或使用类似的机制。
>
>没有这些，任何服务（通用、Analytics、Target等）都将无法正常工作。

## 使用通用代码片段创建服务 {#creating-a-new-service-with-a-generic-snippet}

对于基本配置：

1. 打开 **工具** 控制台。
1. 从左窗格中，展开 **Cloud Service配置**.
1. 双击 **Generic Analytics代码片段** 要打开页面，请执行以下操作：

   ![Generic Analytics Snippet](assets/analytics_genericoverview.png)

1. 单击+以使用该对话框添加新配置。 请至少指定一个名称，例如Google Analytics：

   ![创建配置](assets/analytics_addconfig.png)

1. 单击 **创建**，将会立即打开代码片段对话框 — 将相应的JavaScript代码片段粘贴到字段中：

   ![编辑组件](assets/analytics_snippet.png)

1. 单击 **确定** 以保存。

## 在页面上使用新服务 {#using-your-new-service-on-pages}

创建服务配置后，现在必须配置所需的页面才能使用它：

1. 导航到页面。
1. 打开 **页面属性** 从sidekick，然后 **Cloud Service** 选项卡。
1. 单击 **添加服务**，然后选择所需的服务。 例如， **Generic Analytics代码片段**：

   ![添加云服务](assets/analytics_selectservice.png)

1. 单击 **确定** 以保存。
1. 您将返回 **Cloud Service** 选项卡。 此 **Generic Analytics代码片段** 现已与消息一起列出 `Configuration reference missing`. 使用下拉列表选择特定的服务实例。 例如，google-analytics：

   ![添加云服务配置](assets/analytics_selectspecificservice.png)

1. 单击 **确定** 以保存。

   现在，如果您查看页面的页面源，则可以看到相应代码片段。

   经过一段时间后，可以查看收集的统计数据。

   >[!NOTE]
   >
   >如果配置附加到具有子页面的页面，则这些页面也会继承服务。
