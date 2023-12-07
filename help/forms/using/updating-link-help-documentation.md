---
title: 更新指向文档的链接
description: 如何更新AEM Forms工作区中“工作区帮助”链接的目标以指向您的自定义文档链接。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# 更新指向文档的链接 {#updating-the-link-to-the-documentation}

您可以通过选择，访问AEM Forms工作区的默认帮助内容 **帮助>工作区帮助**. 它指向Adobe网站上的在线文档。 但是，您可以将其更新为指向任何其他URL。

在您需要更改默认帮助URL时，请考虑以下用例：

* 以您选择的语言提供本地化帮助。
* 用于为您的自定义工作区提供自定义帮助内容。

要更新在线文档的URL，请按照 [自定义的常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md) 然后执行以下步骤。

1. 复制 `userinfo.html` 文件来源 `/libs/ws/js/runtime/templates` 到 `/apps/ws/js/runtime/templates`.
1. 更改：

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   到

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 执行以下操作：

   1. 打开/apps/ws/js/registry.js进行编辑。
   1. 搜索和替换 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 替换为 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
