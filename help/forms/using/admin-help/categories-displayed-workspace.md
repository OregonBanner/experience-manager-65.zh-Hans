---
title: 管理在Workspace中显示的类别
seo-title: 管理在Workspace中显示的类别
description: 在Workspace中，用户可以开始的进程以类别显示在左侧导航窗格中。 了解如何管理在Workspace中显示的这些类别。
seo-description: 在Workspace中，用户可以开始的进程以类别显示在左侧导航窗格中。 了解如何管理在Workspace中显示的这些类别。
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# 管理Workspace {#managing-the-categories-displayed-in-workspace}中显示的类别

在Workspace中，用户可以开始的进程以类别显示在左侧导航窗格中。 您可以在管理控制台中设置类别，流程设计人员也可以在Workbench中设置它们。 当流程设计者创建流程时，他们会将流程分配给类别。

指定类别名称时，请创建这些名称，以便它们正确显示在“工作区”导航窗格中。 默认情况下，左侧导航窗格的固定宽度为210像素，大约为24个字符。 如果指定的类别名称太长，无法适应左侧导航窗格的固定宽度，则会截断该名称。 仅当鼠标指针暂停在名称上方时，全名才显示。 尝试避免类别名称被截断。 以下示例说明了适合的类别名称和被截断的名称：

**适合的类别姓名：** 出席和休假

**类别名称被截断：** 出席和离开（美国）

在Workspace中，类别内的进程通常在开始进程页面上显示为卡。 通常，在用户需要滚动到类别剩余卡之前，屏幕上可显示6个卡，用于视图。 由于滚动使查找过程更加困难，请考虑将每个类别限制为六个进程，或根据分辨率限制无需滚动即可在屏幕上显示的进程数。

如果您使用MySQL作为AEM表单类别库，Administration Console无法区分两个仅在使用扩展字符时不同的名。 例如，如果您创建名为abcde的类别和名为âbcdè的类别，则它们被视为相同。

## 添加类别{#add-a-category}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“类别管理”。
1. 单击添加。如果要添加子类别，请选择类别，然后单击添加。
1. 在“名称”框中，键入类别的名称，在“说明”框中，键入类别的说明。
1. 单击添加。类别显示在“类别管理”页面上。

   ***注&#x200B;**:在创建类别时，最多可以将层次结构的五个级别相加。*

## 编辑类别{#edit-a-category}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“类别管理”。
1. 选择要编辑的类别，然后单击“编辑”。 或者，您也可以多次单击要编辑的类别。
1. 在“名称”框中编辑类别的名称。

## 删除类别{#remove-a-category}

您只能删除未使用的类别。

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“类别管理”。
1. 在“类别管理”页面上，选中要删除的类别对应的复选框，然后单击“删除”。 类别不再显示。

