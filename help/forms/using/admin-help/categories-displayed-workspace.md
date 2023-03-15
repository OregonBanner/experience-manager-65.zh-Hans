---
title: 管理工作区中显示的类别
seo-title: Managing the categories displayed in Workspace
description: 在Workspace中，用户可以启动的进程在左侧导航窗格中以类别显示。 了解如何管理工作区中显示的这些类别。
seo-description: In Workspace, the processes that a user can start are displayed in categories in the left navigation pane. Learn how you can manage these categories displayed in Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# 管理工作区中显示的类别 {#managing-the-categories-displayed-in-workspace}

在Workspace中，用户可以启动的进程在左侧导航窗格中以类别显示。 您可以在管理控制台中设置类别，或者流程设计人员可以在Workbench中设置类别。 当流程设计人员创建流程时，会将流程分配给类别。

指定类别名称后，请创建类别名称，以便它们在Workspace导航窗格中正确显示。 默认情况下，左侧导航窗格的固定宽度为210像素，约为24个字符。 如果指定的类别名称太长，无法容纳在左侧导航窗格的固定宽度内，则该类别名称会被截断。 仅当将鼠标指针悬停在全名上时，才会显示全名。 尝试避免将截断的类别名称。 以下示例说明了适合的类别名称和被截断的类别名称：

**符合以下条件的类别名称：** 出席和休假

**被截断的类别名称：** 出席和休假（美国）

在Workspace中，类别中的进程通常在“启动进程”页面上显示为信息卡。 通常，在用户需要滚动查看剩余卡片之前，某个类别的屏幕上可以显示六张卡。 由于滚动会增加查找进程的难度，请考虑将每个类别限制为六个进程，或者，根据您的分辨率，限制可以在屏幕上显示的进程数，而无需任何滚动。

如果您将MySQL用作AEM表单数据库，管理控制台无法区分仅使用扩展字符时不同的两个类别名称。 例如，如果您创建名为abcde的类别和名为abcde的类别，则它们被视为相同。

## 添加类别 {#add-a-category}

1. 在管理控制台中，单击服务>应用程序和服务>类别管理。
1. 单击添加。如果要添加子类别，请选择一个类别，然后单击“添加”。
1. 在“名称”框中，键入类别的名称，然后在“说明”框中，键入类别的说明。
1. 单击添加。类别显示在“类别管理”页面上。

   ***注释&#x200B;**：在创建类别时，您最多只能添加五个层次结构级别。*

## 编辑类别 {#edit-a-category}

1. 在管理控制台中，单击服务>应用程序和服务>类别管理。
1. 选择要编辑的类别，然后单击编辑。 或者，也可以双击要编辑的类别。
1. 在“名称”框中编辑类别的名称。

## 删除类别 {#remove-a-category}

您只能删除未使用的类别。

1. 在管理控制台中，单击服务>应用程序和服务>类别管理。
1. 在“类别管理”页面上，选中要删除的类别的复选框，然后单击“删除”。 类别不再显示。
