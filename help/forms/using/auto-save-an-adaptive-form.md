---
title: 自动保存自适应表单
seo-title: 自动保存自适应表单
description: 您可以配置自适应表单以根据开始或预定义的时间间隔自动保存内容
seo-description: 您可以配置自适应表单以根据开始或预定义的时间间隔自动保存内容
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# 自动保存自适应表单 {#auto-save-an-adaptive-form}

您可以配置自适应表单，以根据开始或预定义的时间间隔自动保存内容。 默认情况下，自适应表单的内容会保存在用户操作上，如按保存按钮时。 “自动保存”选项在以下位置很有用：

* 自动保存匿名和登录用户的内容
* 在无需或最少用户干预的情况下保存表单的内容
* 开始根据用户事件保存表单的内容
* 在指定的时间间隔后重复保存表单的内容

## 为自适应表单启用自动保存 {#enable-autosave-for-an-adaptive-form}

对于自适应表单，不启用自动保存选项。 您可以从自适应表单属性的“自 **动保存** ”部分启用自动保存选项。 “自 **动保存** ”部分还提供了其他几个配置选项。 执行以下步骤以启用和配置自适应表单的自动保存选项：

1. 要访问属性中的自动保存部分，请选择一个组件，然后点 ![按字段级](assets/field-level.png) >自 **[!UICONTROL 适应表单容器]**，然后点 ![按cmppr](assets/cmppr.png)。
1. 在“自 **[!UICONTROL 动保存]** ”部分 **[!UICONTROL ，启]** 用“自动保存”选项。
1. 在“自 **[!UICONTROL 适应表单事件]** ”框中，指定1或TRUE可在表单加载到浏览器时自动开始保存表单。 您还可以为事件指定条件表达式，当触发并返回true时，开始将保存表单的内容。
1. 指定触发器。 自动保存会根据您的配置触发。 您的选择包括：

   * **[!UICONTROL 基于时间：]** 选择选项以开始根据特定时间间隔保存内容。
   * **[!UICONTROL 事件:]** 选择开始选项，以在触发事件时保存内容。

   选择触发器时，“策略配置”框处于启用状态。 “策略配置”框允许您：

   * 如果选择基于时间的触发器，请 **[!UICONTROL 指定时间间隔]** 。
   * 如果选择基于事件的触发器，请 **[!UICONTROL 指定事件]** 名称。

   您还可以创建自定义策略并将其添加到列表。 有关详细信息，请 [参阅实施自定义策略以自动保存表单](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （仅限基于时间的自动保存）执行以下步骤以配置基于时间的自动保存的选项。

   1. 在“自动 **[!UICONTROL 保存此时间间隔]** ”框中，以秒为单位指定时间间隔。 在经过间隔框中指定的秒数后，将重复保存表单。

1. (仅基于事件的自动保存)执行以下步骤以配置基于事件的自动保存选项。

   1. 在此事件 **后自动保存** ，请指定GuideBridge [事件](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 。 每次表达式计算结果为TRUE时，将保存表单。

1. （可选）要自动保存匿名用户的内容，请选择“为匿名 **用户启用自动保存** ”选项，然后单 **[!UICONTROL 击“确定”]**。

   >[!NOTE]
   >
   >要使自动保存选项适用于匿名用户，请确保配置Forms Common Configuration Service以允许所有用户对表单进行预览、验证和签名。
   >
   >要配置服务，请转到AEM Web Console配置，并 `https://server:port/system/console/configMgr` 编辑Forms **[!UICONTROL Common Configuration Service]** ，在“允 **[!UICONTROL 许”字段中选]** 择“所有用户 **[!UICONTROL ”选项]** ，然后保存配置。

## 实施自定义策略，为自适应表单启用自动保存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以实现自定义事件以触发自动保存功能。 请执行以下步骤以创建和实施自定义事件:

1. 创建客户端库和客户端库文件夹。 有关详细步骤，请参 [阅使用客户端库文档](/help/sites-developing/clientlibs.md)。

   例如，以下脚本使用自定义 `emailFocusChange`事件触发自动保存功能：

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
   >创建客户端库文件夹时会定义类别属性。 请准备好分配给类别属性的值。

1. 在创作模式下打开自适应表单。

1. 在编辑模式中，选择一个组件，点按 ![字段级别](assets/field-level.png) > **[!UICONTROL 自适应表单容器]**，然后点 ![按cmppr](assets/cmppr.png)。
1. 在属性中，打开“基 **[!UICONTROL 本]** ”部分。 在“客 **[!UICONTROL 户端库类别]** ”框中，输入创建客户端库文件夹时定义的类别属性值。
1. 打开“自动保存”部分。 在“在 **[!UICONTROL 此事件后自动保存]** ”框中，指定已在客户端库中定义的自定义事件。 单击&#x200B;**[!UICONTROL 确定]**。

