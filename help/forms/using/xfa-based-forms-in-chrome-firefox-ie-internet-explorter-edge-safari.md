---
title: 无法在Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer或Apple Safari中打开基于XFA的PDF forms
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
docset: aem65
feature: Adaptive Forms
source-git-commit: 12d8978f685dd7bdae12e51275edeb50fa930eb0
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# 无法在Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer或Apple Safari中打开基于XFA的PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

许多最新的浏览器版本都对基于XFA的PDF forms提供了有限的支持。 尽管这些浏览器可以打开基于XFA的PDF forms，但支持的范围尚不明确。 如果您无法在现代浏览器中打开或提交基于XFA的PDF表单，请使用以下方法之一：

* 使用 [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) 或 [Adobe®Adobe®Reader®](https://get.adobe.com/reader/)、版本8或更高版本，以打开并提交基于XFA的PDF forms。
* Acrobat和Reader在Microsoft® Windows®上，允许您配置为在“受保护视图”模式下打开PDF，这会阻止打开基于XFA的PDF forms。 确保禁用Acrobat或Reader中的“受保护视图”模式。 有关更多信息，请参阅 [受保护视图（仅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* 如果您尝试在移动设备上访问基于XFA的PDF forms，请使用Adobe Reader进行移动设备。 有关更多信息，请参阅 [Adobe Reader移动应用程序](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
* (对于Forms开发人员)Adobe Experience Manager Forms还支持
   * [将基于XFA的表单渲染到HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) 这样，在支持HTML5的浏览器(包括在iPad等移动设备上运行的浏览器)中就可以打开表单。 表单的HTML5呈现版本维护表单设计的布局，并支持XFA表单模板中嵌入的大多数表单逻辑（如JavaScript、表单计算和表单验证）。
   * [将基于XFA的表单转换为移动响应式自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). 这些表单提供了响应式布局和个性化功能，并可根据需要添加或删除字段或部分，从而动态地适应用户响应。 它们还为各种数据源提供开箱即用的连接器、记录文档功能，以及轻松连接到Adobe Analytics以进行性能评估。 有关更多信息，请参阅 [主要特性和功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

这样，您对XFA表单的技术投资便可以轻松转移到运行Adobe Reader插件不可行的设备上。 有关更多信息，请参阅 [Adobe Experience Manager Forms产品文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
