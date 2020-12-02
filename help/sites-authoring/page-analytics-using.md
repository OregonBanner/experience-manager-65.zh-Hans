---
title: 查看页面分析数据
seo-title: 查看页面分析数据
description: 可使用页面分析数据评估页面内容的有效性
seo-description: 可使用页面分析数据评估页面内容的有效性
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 84%

---


# 查看页面分析数据{#seeing-page-analytics-data}

可使用页面分析数据评估页面内容的有效性。

## 可从控制台中查看分析数据  {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

页面分析数据显示在站点控制台的[列表视图](/help/sites-authoring/basic-handling.md#list-view)中。当页面以列表格式显示时，默认情况下可使用以下列：

* 页面查看次数
* 独特访客
* 页面停留时间

每列会显示当前报表时间段的值，同时还会显示自上一报表时间段以来该值是增加还是减少。您查看的数据每 12 小时更新一次。

>[!NOTE]
>
>要更改更新周期，请[配置导入时间间隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)。

1. 打开&#x200B;**站点**&#x200B;控制台；例如[https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. 在工具栏的最右侧（右上角），单击或点按相应的图标以选择&#x200B;**列表视图**（显示的图标将取决于[当前视图](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)）。

1. 再次在工具栏的最右侧（右上角），单击或点按相应的图标，然后选择&#x200B;**查看设置**。此时将打开&#x200B;**配置列**&#x200B;对话框。执行所需的更改，然后单击&#x200B;**更新**&#x200B;以进行确认。

   ![spad-02](assets/spad-02.png)

### 选择报表时间段 {#selecting-the-reporting-period}

选择在“站点”控制台上显示的分析数据的报表时间段：

* 过去 30 天的数据
* 过去 90 天的数据
* 本年度的数据

当前报表时间段会显示在“站点”控制台的工具栏上（顶部工具栏右侧）。可使用下拉菜单选择所需的报表时间段。

![aa-05](assets/aa-05.png)

### 配置可用数据列 {#configuring-available-data-columns}

分析管理员用户组的成员可以配置站点控制台，以使作者能够查看其他分析列。

>[!NOTE]
>
>当页面树包含与不同 Adobe Analytics 云配置关联的子项时，您无法为页面配置可用数据列。

1. 在列表视图中，使用视图选择器（工具栏右侧），选择&#x200B;**视图设置**，然后选择&#x200B;**添加自定义分析数据**。

   ![spad-03](assets/spad-03.png)

1. 在站点控制台中选择要向作者公开的量度，然后单击&#x200B;**添加**。

   显示的列从Adobe Analytics检索。

   ![aa-16](assets/aa-16.png)

### 从站点打开内容分析 {#opening-content-insights-from-sites}

从“站点”控制台打开[内容分析](/help/sites-authoring/content-insights.md)以进一步调查页面有效性。

1. 在站点控制台中，选择要查看“内容分析”的页面。
1. 在工具栏上，单击“分析和建议”图标。

   ![](do-not-localize/chlimage_1-14.png)

## 可从页面编辑器 (Activity Map) 中查看分析数据  {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，因此无法再使用 AEM 中包含的 Activity Map 版本。
>
>现在应使用Adobe Analytics](https://docs.adobe.com/content/help/zh-Hans/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap插件。
