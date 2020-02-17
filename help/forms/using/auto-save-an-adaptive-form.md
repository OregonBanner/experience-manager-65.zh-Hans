---
title: 自动保存自适应表单
seo-title: 自动保存自适应表单
description: 您可以配置自适应表单以根据事件或预定义的时间间隔自动开始保存内容
seo-description: 您可以配置自适应表单以根据事件或预定义的时间间隔自动开始保存内容
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# 自动保存自适应表单 {#auto-save-an-adaptive-form}

您可以配置自适应表单以根据事件或预定义的时间间隔自动开始保存内容。 默认情况下，自适应表单的内容会保存在用户操作上，如按保存按钮时。 “自动保存”选项在以下位置很有帮助：

* 自动保存匿名用户和登录用户的内容
* 无需或最少的用户干预即可保存表单的内容
* 开始保存基于用户事件的表单内容
* 在指定的时间间隔后重复保存表单的内容

## 为自适应表单启用自动保存 {#enable-autosave-for-an-adaptive-form}

对于自适应表单，不会立即启用自动保存选项。 您可以从自适应表单属性中的“自 **动保存** ”部分启用自动保存选项。 “自 **动保存** ”部分还提供了若干其他配置选项。 执行以下步骤以为自适应表单启用和配置自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后点按字 ![段级别](assets/field-level.png) >自适应表单容器 **[!UICONTROL ，然后点按]** cmppr ![](assets/cmppr.png)。
1. 在“自 **[!UICONTROL 动保存]** ”部分， **[!UICONTROL 启用]** “自动保存”选项。
1. 在“自适 **[!UICONTROL 应表单事件]** ”框中，指定1或TRUE，以在表单加载到浏览器中时自动开始保存表单。 您还可以为事件指定条件表达式，当触发并返回true时，该表达式会开始保存表单的内容。
1. 指定触发器。 自动保存会根据您的配置触发。 您的选择包括：

   * **** 基于时间：选择选项以根据特定时间间隔开始保存内容。
   * **** 基于事件：选择此选项可在触发事件时开始保存内容。
   当您选择触发器时，“策略配置”框处于启用状态。 “战略配置”框允许您：

   * 如果选择基于时间的触发器，请指 **[!UICONTROL 定时间间隔]** 。
   * 如果选择基于事件的触发器，请指 **[!UICONTROL 定事件名]** 称。
   您还可以创建自定义策略并将其添加到列表中。 有关详细信息，请参 [阅实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （仅限基于时间的自动保存）执行以下步骤以配置基于时间的自动保存的选项。

   1. 在“在 **[!UICONTROL 此间隔上自动保存]** ”框中，以秒为单位指定时间间隔。 在经过间隔框中指定的秒数后，将重复保存表单。

1. （仅基于事件的自动保存）执行以下步骤以配置基于事件的自动保存选项。

   1. 在“在此 **事件后自动保存** ”框中，指定 [GuideBridge事件](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 。 每次表达式的计算结果为TRUE时都会保存表单。

1. （可选）要自动保存匿名用户的内容，请选择“为匿名用户启 **用自动保存”选项** ，然后单击“确 **[!UICONTROL 定”]**。

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保您配置Forms Common Configuration Service，以允许所有用户预览、验证和签署表单。
   >
   >要配置服务，请转到上的AEM Web Console配置，并编辑 `https://[server]:[host]/system/console/configMgr`**[!UICONTROL Forms Common Configuration Service]** ，以在“允许”字段中选择“ **[!UICONTROL 所有用户]** ”选项 **** ，然后保存该配置。

## 实施自定义策略以启用自适应表单的自动保存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以实现自定义事件以触发自动保存功能。 执行以下步骤以创建和实施自定义事件：

1. 创建客户端库和客户端库文件夹。 有关详细步骤，请参 [阅使用客户端库文档](/help/sites-developing/clientlibs.md)。

   例如，以下脚本使用自定义事 `emailFocusChange`件触发自动保存功能：

   ```
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
   >在创建客户端库文件夹时会定义类别属性。 让分配给类别属性的值保持方便。

1. 在创作模式下打开自适应表单。

1. 在编辑模式中，选择一个组件，然后点 ![按字段级别](assets/field-level.png) >自 **[!UICONTROL 适应表单容器]**，然后点 ![按cmppr](assets/cmppr.png)。
1. 在属性中，打开“基 **[!UICONTROL 本]** ”部分。 在“客 **[!UICONTROL 户端库类别]** ”框中，输入在创建客户端库文件夹时定义的类别属性的值。
1. 打开“自动保存”部分。 在“在此 **[!UICONTROL 事件后自动保存]** ”框中，指定已在客户端库中定义的自定义事件。 单击&#x200B;**[!UICONTROL 确定]**。

