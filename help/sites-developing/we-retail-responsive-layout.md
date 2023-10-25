---
title: 在We.Retail中尝试响应式布局
seo-title: Trying out Responsive Layout in We.Retail
description: 了解如何使用We.Retail在Adobe Experience Manager中试用响应式布局。
seo-description: null
uuid: d9613655-f54e-458f-9175-d07bb868f58b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2d374e88-ea09-43d5-986c-5d77b0705b93
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 6%

---

# 在We.Retail中尝试响应式布局{#trying-out-responsive-layout-in-we-retail}

所有We.Retail页面都使用布局容器组件来实施响应式设计。 布局容器提供了一个段落系统，允许您在响应式网格内放置组件。 此网格可以根据设备/窗口大小和格式重新安排布局。该组件将与 **布局** 模式，允许您创建和编辑依赖于设备的响应式布局。

## 正在尝试 {#trying-it-out}

1. 在语言母版分支的体验部分中编辑“北极冲浪”页面。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. 切换到 **预览** 用于查看呈现给网站访客的页面。 向下滚动到文章的内容 *挪威北部阿罗哈烈酒*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 调整浏览器窗口大小并观察布局如何动态适应大小调整。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 切换到布局模式。 模拟器工具栏会自动显示，允许您按目标设备规划布局。

   选择某个组件时，会在“编辑”菜单中显示浮动和隐藏选项，以及组件的调整大小手柄。

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. 抓住并拖动组件的调整大小手柄会自动显示布局网格，以帮助您调整大小。

   ![chlimage_1-181](assets/chlimage_1-181.png)

## 更多信息 {#further-information}

有关详细信息，请参阅创作文档 [响应式布局](/help/sites-authoring/responsive-layout.md) 或管理员文档 [配置布局容器和布局模式](/help/sites-administering/configuring-responsive-layout.md) 以了解完整的技术详细信息。
