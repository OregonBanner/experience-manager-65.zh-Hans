---
title: 更新檔案的連結
seo-title: Updating the link to the documentation
description: 如何更新AEM Forms工作區中工作區說明連結的目的地，以指向您的自訂檔案連結。
seo-description: How-to update the destination of Workspace Help link in AEM Forms workspace to point to your custom documentation link.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 3%

---

# 更新檔案的連結 {#updating-the-link-to-the-documentation}

您可以選取「 」，存取AEM Forms工作區的預設說明內容 **「說明>工作區說明」**. 它指向Adobe網站上的線上檔案。 不過，您可以更新以指向任何其他URL。

請考量下列您可能想要變更預設說明URL的使用案例：

* 以您選擇的語言提供當地語系化說明。
* 提供自訂工作區的自訂說明內容。

若要更新線上檔案的URL，請遵循 [自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md) 然後執行下列步驟。

1. 複製 `userinfo.html` 檔案來源 `/libs/ws/js/runtime/templates` 至 `/apps/ws/js/runtime/templates`.
1. 更改:

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

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜尋和取代 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 替換為 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
