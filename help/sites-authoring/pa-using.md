---
title: 查看页面分析数据以衡量页面内容的有效性
description: 使用页面分析数据来衡量其页面内容的有效性
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# 查看页面分析数据{#seeing-page-analytics-data}

使用页面分析数据来衡量页面内容的有效性。

## Analytics在控制台中可见 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

页面分析数据显示在 [列表视图](/help/sites-authoring/basic-handling.md#list-view) 站点控制台的。 当页面以列表格式显示时，默认情况下以下列可用：

* 页面视图
* 独特访客
* 页面停留时间

每列显示一个当前报告期的值，并指示该值自上一个报告期以来是增加还是减少。 您看到的数据每12小时更新一次。

>[!NOTE]
>
>要更改更新周期， [配置导入间隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. 打开 **站点** 控制台；例如 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. 在工具栏的最右侧（右上角），单击或点按图标以选择 **列表视图** (显示的图标将取决于 [当前视图](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 同样，在工具栏的最右侧（右上角），单击或点按图标，然后选择 **查看设置**. 此 **配置列** 此时将打开对话框。 进行所需的任何更改并通过进行确认 **更新**.

   ![aa-04](assets/aa-04.png)

### 选择报告周期 {#selecting-the-reporting-period}

选择站点控制台上显示Analytics数据的报告时段：

* 过去 30 天的数据
* 过去 90 天的数据
* 本年度的数据

当前报告时段显示在站点控制台的工具栏上（顶部工具栏的右侧）。 使用下拉菜单选择所需的报告时段。
![aa-05](assets/aa-05.png)

### 配置可用数据列 {#configuring-available-data-columns}

Analytics-administrators用户组的成员可以配置Sites控制台，以便作者能够查看额外的Analytics列。

>[!NOTE]
>
>当页面树包含与不同Adobe Analytics云配置关联的子项时，无法为页面配置可用数据列。

1. 在列表视图中，使用视图选择器（工具栏的右侧），选择 **查看设置** 然后 **添加自定义分析数据**.

   ![aa-15](assets/aa-15.png)

1. 在站点控制台中选择要向作者显示的量度，然后单击 **添加**.

   显示的列检索自Adobe Analytics。

   ![aa-16](assets/aa-16.png)

### 从站点打开内容分析 {#opening-content-insights-from-sites}

打开 [内容分析](/help/sites-authoring/content-insights.md) 以进一步调查页面有效性。

1. 在站点控制台中，选择要查看其内容分析的页面。
1. 在工具栏上，单击Analytics和Recommendations图标。

   ![](do-not-localize/chlimage_1-16a.png)

## 在页面编辑器中可见的Analytics(Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>在以下情况下将显示此选项： [Activity Map已配置](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) （对于您的网站）。

>[!NOTE]
>
>Activity Map的数据获取自Adobe Analytics。

当您的网站 [已为Adobe Analytics配置](/help/sites-administering/adobeanalytics-connect.md)，您可以使用 [模式Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 以查看相关数据。 例如：

![aa-07](assets/aa-07.png)

### 访问Activity Map {#accessing-the-activity-map}

选择 [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 模式时，将要求您输入Adobe Analytics凭据。

![aa-03](assets/aa-03.png)

此 **分析** 此时将显示浮动工具栏；您可以：

* 使用双箭头(**>>**)
* 切换页面详细信息（眼睛图标）
* 配置Activity Map设置（齿轮图标）
* 选择要显示的分析（各种下拉选择器）
* 退出Activity Map并关闭工具栏(x)

![aa-09](assets/aa-09.png)

### 选择要显示的分析 {#selecting-the-analytics-to-show}

您可以使用各种标准选择要显示的分析数据及其显示方式：

* **标准**/**实时**

* 事件类型
* 用户组
* **气泡**/**渐变**/**获胜方和失败方**/**关闭**

* 要显示的期间

![aa-13](assets/aa-13.png)

### 配置Activity Map {#configuring-the-activity-map}

使用 **显示设置** 图标以打开 **Activity Map设置** 对话框。

![aa-04-1](assets/aa-04-1.png)

此 **Activity Map设置** 对话框在三个选项卡上提供了一系列选项：

![aa-06](assets/aa-06.png)

* 常规

   * 报表包
   * 页面名称
   * 语言
   * 为叠加图添加以下标签
   * 标签字体大小
   * 渐变颜色
   * 气泡颜色
   * 颜色渐变依据
   * 渐变透明度

* 标准

   * 显示（链接类型和数量）
   * 隐藏未收到点击量的链接所对应的叠加图

* 实时版

   * 显示排名最前的（获胜方或失败方）
   * 排除最后%
   * 自动更新（数据和期间）
