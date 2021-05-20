---
title: 配置验证消息
seo-title: 配置验证消息
description: 了解如何指定验证消息的显示方式及其相对于Web浏览器中返回的表单的位置。
seo-description: 了解如何指定验证消息的显示方式及其相对于Web浏览器中返回的表单的位置。
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---

# 配置验证消息{#configuring-validation-messages}

对于呈现为HTML的表单，会向用户显示发生的表单验证错误。 您可以自定义验证消息的显示方式。 根据验证消息的显示位置，您还可以控制消息的格式位置和框架边框的大小。

## 指定验证消息的显示方式{#specify-how-validation-messages-are-displayed}

1. 在管理控制台中，单击服务>表单。
1. 在“验证输出”的“报表”列表下，选择以下选项之一：

   **消息框：** 在单独的对话框中显示验证消息。

   **框架：** 在同一窗口的框架内显示验证消息。

   **无框架：** 在同一窗口中显示验证消息。此值为默认值。

   **通过API（包含数据）：** 通过API（包含数据）返回验证消息。验证消息未显示在屏幕上。

   **通过API（使用表单）：** 通过API（使用表单）返回验证消息。验证消息未显示在屏幕上。

   **无：** 不显示验证消息。

1. 单击保存。

## 指定验证消息相对于Web浏览器中返回的表单的位置{#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

将“报表”设置为“框架”或“无框架”时，您可以指定验证消息的位置。

1. 在“验证输出”(Validation Output)下的“位置”(Position)列表中，选择以下选项之一：

   **左：** 在Web浏览器的左侧显示验证消息。

   **右侧：** 在Web浏览器的右侧显示验证消息。

   **顶部**:用于在Web浏览器顶部显示验证消息。此值为默认值。

   **底部**:用于在Web浏览器底部显示验证消息。

1. 单击保存。

## 指定帧边框大小{#specify-the-frame-border-size}

将“报告”设置为“帧”时，可以指定帧边框大小。

1. 在“验证输出”下的“边框大小”框中，键入边框的大小（以像素为单位）。

   边框大小必须等于或大于0。 默认值为 1。

1. 单击保存。
