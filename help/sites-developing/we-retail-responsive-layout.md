---
title: 在We.Retail中尝试响应式布局
seo-title: 在We.Retail中尝试响应式布局
description: 'null'
seo-description: 'null'
uuid: d9613655-f54e-458f-9175-d07bb868f58b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2d374e88-ea09-43d5-986c-5d77b0705b93
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在We.Retail中尝试响应式布局{#trying-out-responsive-layout-in-we-retail}

所有We.Retail页面都使用布局容器组件来实现响应式设计。 布局容器提供了段落系统，允许您将组件放置在响应式网格内。 此网格可以根据设备/窗口大小和格式重新安排布局。The component is used in conjunction with the **Layout** mode in the page editor, which allows you to create and edit your responsive layout dependent on device.

## 试用 {#trying-it-out}

1. 在语言主分支的“体验”部分编辑“北极冲浪”页面。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. 切换到“ **预览** ”可查看页面呈现给网站访客的效果。 向下滚动到挪威北部的Aloha spirits *文章的内容*。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 调整浏览器窗口的大小，并观察布局如何动态调整为调整大小。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 切换到布局模式。 模拟器工具栏会自动显示，允许您根据目标设备规划布局。

   选择组件后，编辑菜单中会显示浮动和隐藏选项以及组件的调整大小手柄。

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. 抓取并拖动组件的调整大小手柄会自动显示布局网格以帮助您调整大小。

   ![chlimage_1-181](assets/chlimage_1-181.png)

## 更多信息 {#further-information}

有关详细信息，请参阅创作文档响应式布 [局](/help/sites-authoring/responsive-layout.md) ，或管理员文档配置布 [局容器和布局模式](/help/sites-administering/configuring-responsive-layout.md) ，以获得完整的技术详细信息。
