---
title: 自动保存自适应表单
description: 您可以将自适应表单配置为根据事件或预定义的时间间隔自动开始保存内容
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 7%

---

# 自动保存自适应表单 {#auto-save-an-adaptive-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

您可以配置自适应表单，以根据事件或预定义的时间间隔自动开始保存内容。 默认情况下，自适应表单的内容会在用户操作时保存，例如按保存按钮时。 自动保存选项在以下方面很有用：

* 自动为匿名和登录用户保存内容
* 保存表单内容而不需要用户干预或用户干预最少
* 开始基于用户事件保存表单内容
* 在指定的时间间隔后重复保存表单的内容

## 为自适应表单启用自动保存 {#enable-autosave-for-an-adaptive-form}

对于自适应表单，不会现成启用自动保存选项。 您可以从以下位置启用自动保存选项 **自动保存** 自适应表单的属性中的部分。 此 **自动保存** 部分还提供了几个其他配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后选择 ![字段级](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后选择 ![cmppr](assets/cmppr.png).
1. 在 **[!UICONTROL 自动保存]** 部分， **[!UICONTROL 启用]** 自动保存选项。
1. 在 **[!UICONTROL 自适应表单事件]** 框中，指定1或TRUE以在浏览器中加载表单时自动开始保存表单。 您还可以为事件指定条件表达式，该表达式在触发并返回true时开始保存表单的内容。
1. 指定触发器。 根据您的配置触发自动保存。 您的选项包括：

   * **[!UICONTROL 基于时间：]** 选择选项，以根据特定时间间隔开始保存内容。
   * **[!UICONTROL 基于事件：]** 选择选项以在触发事件时开始保存内容。

   选择触发器后，将启用“策略配置”框。 通过“策略配置”框，您可以：

   * 如果您选择，请指定时间间隔 **[!UICONTROL 基于时间]** 触发器。
   * 如果您选择，请指定事件名称 **[!UICONTROL 基于事件]** 触发器。

   您还可以创建自己的自定义策略并将其添加到列表中。 有关详细信息，请参阅 [实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. （仅限基于时间的自动保存）执行以下步骤来配置基于时间的自动保存选项。

   1. 在 **[!UICONTROL 在此间隔自动保存]** 框中，以秒为单位指定时间间隔。 在间隔框中指定的秒数过后，将重复保存该表单。

1. （仅限基于事件的自动保存）执行以下步骤来配置用于基于事件的自动保存的选项。

   1. 在 **在此事件后自动保存** 框，指定 [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 事件。 每当表达式的计算结果为TRUE时，将保存表单。

1. （可选）要自动为匿名用户保存内容，请选择 **为匿名用户启用自动保存** 选项，然后单击 **[!UICONTROL 确定]**.

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保将Forms通用配置服务配置为允许所有用户预览、验证和签署表单。
   >
   >要配置该服务，请转到AEM Web控制台配置，网址为 `https://server:port/system/console/configMgr` 并编辑 **[!UICONTROL Forms通用配置服务]** 以选择 **[!UICONTROL 所有用户]** 中的选项 **[!UICONTROL 允许]** 字段，并保存配置。

## 实施自定义策略以启用自适应表单的自动保存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以实施自定义事件以触发自动保存功能。 执行以下步骤以创建和实施自定义事件：

1. 创建客户端库和客户端库文件夹。 有关详细步骤，请参见 [使用客户端库文档](/help/sites-developing/clientlibs.md).

   例如，以下脚本使用自定义 `emailFocusChange`事件以触发自动保存功能：

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >在创建客户端库文件夹时定义类别属性。 随时准备分配给类别属性的值。

1. 在创作模式下打开自适应表单。

1. 在编辑模式下，选择一个组件，然后选择 ![字段级](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后选择 ![cmppr](assets/cmppr.png).
1. 在属性中，打开 **[!UICONTROL 基本]** 部分。 在 **[!UICONTROL 客户端库类别]** 框中，输入创建客户端库文件夹时定义的category属性的值。
1. 打开自动保存部分。 在 **[!UICONTROL 在此事件后自动保存]** 框中，指定已在客户端库中定义的自定义事件。 单击&#x200B;**[!UICONTROL 确定]**。
