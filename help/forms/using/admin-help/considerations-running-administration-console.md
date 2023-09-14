---
title: 运行Administration Console时的注意事项
description: 本文档列出了运行Administration Console时要考虑的一些要点。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 运行Administration Console时的注意事项 {#considerations-when-running-administrationconsole}

运行Administration Console时需要考虑以下几点：

* 如果您使用URL访问管理控制台 `https://[hostname]:'port'/adminui`，指定的主机名不能包含下划线字符。 否则，指向管理控制台某些区域的链接可能无法正常工作。
* 如果在日语操作系统的Windows资源管理器中运行管理控制台，则可能会遇到以下问题：

   * 单击链接会返回登录页面，而不是预期的链接。
   * 单击链接会显示权限错误。

  最佳实践是从其他浏览器（如Mozilla Firefox）运行管理控制台，以确保没有任何链接失败。

* 在管理控制台中执行搜索时，请勿使用反斜杠字符()。
