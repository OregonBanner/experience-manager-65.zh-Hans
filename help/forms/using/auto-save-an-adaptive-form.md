---
title: 自动保存自适应表单
seo-title: 自动保存自适应表单
description: 您可以配置自适应表单，以便根据事件或预定义的时间间隔自动开始保存内容
seo-description: 您可以配置自适应表单，以便根据事件或预定义的时间间隔自动开始保存内容
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: 自适应表单
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# 自动保存自适应表单{#auto-save-an-adaptive-form}

您可以配置自适应表单，以便根据事件或预定义的时间间隔自动开始保存内容。 默认情况下，自适应表单的内容会在用户操作（如按保存按钮）中保存。 自动保存选项在以下位置很有用：

* 自动保存匿名用户和登录用户的内容
* 在无需或最少用户干预的情况下保存表单的内容
* 开始根据用户事件保存表单的内容
* 在指定的时间间隔后重复保存表单的内容

## 为自适应表单{#enable-autosave-for-an-adaptive-form}启用自动保存

对于自适应表单，不会开箱即用地启用自动保存选项。 您可以从自适应表单属性的&#x200B;**自动保存**&#x200B;部分启用自动保存选项。 **自动保存**&#x200B;部分还提供了其他几个配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，点按![字段级别](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后点按![cmpr](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 自动保存]**&#x200B;部分， **[!UICONTROL 启用]**&#x200B;自动保存选项。
1. 在&#x200B;**[!UICONTROL 自适应表单事件]**&#x200B;框中，指定1或TRUE，以在浏览器中加载表单时自动开始保存表单。 您还可以为事件指定条件表达式，当触发并返回true时，将开始保存表单的内容。
1. 指定触发器。 会根据您的配置触发自动保存。 您的选项包括：

   * **[!UICONTROL 基于时间：]** 选择选项以根据特定时间间隔开始保存内容。
   * **[!UICONTROL 基于事件：]** 选择选项，以在触发事件时开始基于内容进行保存。

   选择触发器时，将启用“策略配置”框。 “策略配置”框允许您：

   * 如果选择&#x200B;**[!UICONTROL 基于时间]**&#x200B;触发器，请指定时间间隔。
   * 如果选择&#x200B;**[!UICONTROL 基于事件]**&#x200B;的触发器，请指定事件名称。

   您还可以创建自定义策略并将其添加到列表中。 有关详细信息，请参阅[实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （仅限基于时间的自动保存）执行以下步骤以配置基于时间的自动保存的选项。

   1. 在&#x200B;**[!UICONTROL 自动保存此间隔]**&#x200B;框中，以秒为单位指定时间间隔。 在间隔框中指定的秒数过后，表单会重复保存。

1. （仅限基于事件的自动保存）执行以下步骤以配置用于基于事件的自动保存的选项。

   1. 在&#x200B;**此事件后自动保存**&#x200B;框中，指定[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)事件。 每次表达式计算为TRUE时，都会保存表单。

1. （可选）要自动保存匿名用户的内容，请选择&#x200B;**为匿名用户启用自动保存**&#x200B;选项，然后单击&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   >
   >要使自动保存选项对匿名用户有效，请确保您配置Forms通用配置服务，以允许所有用户预览、验证和签名表单。
   >
   >要配置服务，请转到`https://server:port/system/console/configMgr`的AEM Web控制台配置，然后编辑&#x200B;**[!UICONTROL Forms Common Configuration Service]**，以在&#x200B;**[!UICONTROL Allow]**&#x200B;字段中选择&#x200B;**[!UICONTROL All Users]**&#x200B;选项，并保存配置。

## 实施自定义策略以为自适应表单启用自动保存功能{#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以实施自定义事件以触发自动保存功能。 执行以下步骤以创建和实施自定义事件：

1. 创建客户端库和客户端库文件夹。 有关详细步骤，请参阅[使用客户端库文档](/help/sites-developing/clientlibs.md)。

   例如，以下脚本使用自定义`emailFocusChange`事件触发自动保存功能：

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
   >在创建客户端库文件夹时定义类别属性。 请准备好分配给类别属性的值。

1. 在创作模式下打开自适应表单。

1. 在编辑模式下，选择一个组件，点按![字段级别](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后点按![cmpr](assets/cmppr.png)。
1. 在属性中，打开&#x200B;**[!UICONTROL Basic]**&#x200B;部分。 在&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;框中，输入创建客户端库文件夹时定义的类别属性值。
1. 打开自动保存部分。 在&#x200B;**[!UICONTROL 此事件后自动保存]**&#x200B;框中，指定已在客户端库中定义的自定义事件。 单击&#x200B;**[!UICONTROL 确定]**。
