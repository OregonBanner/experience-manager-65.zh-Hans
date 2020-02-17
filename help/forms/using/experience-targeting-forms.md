---
title: 在AEM Forms中创建目标体验
seo-title: 在AEM Forms中创建目标体验
description: 在AEM Forms中使用Target为目标客户创建自定义体验。
seo-description: 在AEM Forms中使用Target为目标客户创建自定义体验。
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# 在AEM Forms中创建目标体验 {#create-targeted-experiences-in-aem-forms}

## 将Adobe target与AEM Forms集成 {#integrate-adobe-target-with-aem-forms}

与AEM集成的Adobe Target使您能够为目标受众创建自定义的体验。 借助Adobe Target，您可以创建A/B测试、评估用户响应并为目标用户生成自定义Web内容。 您可以将Adobe Target与AEM Forms集成，以针对自适应表单和交互式通信的图像组件。

在AEM中配置Adobe Target以将其与自适应表单和交互式通信一起使用，请参阅 [在AEM中创建目标配置](/help/sites-administering/target.md)[和添加框架](/help/sites-administering/target.md)。

>[!NOTE]
>
>当使用主机名或IP地址呈现您的自适应表单或交互式通信时，定位即可生效。 当您的自适应表单或交互式通信使用localhost呈现时，它将失败。

## 创建目标活动 {#creating-a-target-activity}

1. 点按 **Adobe Experience Manager >个性化>活动**。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 在“活动”页面中，点按创 **建>创建品牌**。
1. 系统会要求您选择模板并输入属性。

   选择模板，点按下 **一步。** 在“属性”部分输入品牌标题，然后点按创 **建。**
您的品牌现在列在“活动”页面中。

1. 在“活动”页面中点击您的品牌。
1. 在品牌的主区域中，点按创 **建** >创 **建活动**。

   创建活动时，需指定其详细信息、目标和设置。

   “详细信息”部分包括名称、定位引擎和目标。 当您选择Adobe Target作为定位引擎时，您将启用Target云配置选项。 选择您的Target云配置，选择活动类型，提供活动的目标，然后点按下 **一步**。 交互通信仅支持体验定位活动类型。

   通过“目标”部分，您可以添加受众体验并命名它。 单击 **添加体验** ，以启用选择 **受众** 和命名 **体验选项** 。 点按 **选择受众** ，以查看受众及其源的列表。 从“受众名称”列表中选择受众。 点按 **添加体验** ，命名体验，然后点按下 **一步**。

   通过“目标和设置”部分，可以计划活动并排定其优先级。 设置活动的开始日期、结束日期和优先级、目标量度、其他量度，然后点按保 **存**。

   活动现在列在您的品牌页面中。

   >[!NOTE]
   >
   >您可能会忽略错误“您的活动已保存，但未同步到Target。 原因：以下体验没有选件”（如果在保存活动时遇到）。

1. 要启用目标，请编辑。jsp文件以包含自适应表单模板使用的客户端库。

   例如，在现成的实现中，单击“工具” **>** CRXDE Lite ****。

   在CRXDE lite地址栏中，键入/libs/fd/af/components/page/base/head.jsp以编辑head.jsp文件。

   此实施使用simpleEngroment模板。 在此实现中，修改head.jsp文件以包括以下客户端库：

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 要为自适应表单启用目标框架，请导航到表单或交互式通信，然后在编辑模式下打开它。

   要在编辑模式下打开表单或交互式通信，请点按 **选择** ，然后点按 **打开**。

   或者，当您将指针移到表单或交互式通信图标上而不选择它时，会显示四个按钮。 您可以点按显示 **的“编辑** ”按钮，以在编辑模式下打开表单。

1. 在页面工具栏中，点按页 **面信息**![主题选项](assets/theme-options.png) >打 **开属性**。
1. 在“常规”选项卡中，为 **Adobe Target字段选择配置** 。 点按 **保存并关闭**。

## 将创建的活动应用于自适应表单图像或交互式通信图像 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 打开自适应表单和交互式通信进行编辑。 如果要打开交互式通信，请打开Web渠道。

1. 在交互式通信或自适应表单的创作模式中，添加要定位的图像。

   >[!NOTE]
   >
   >AEM Forms支持仅定位图像组件。 确保承载图像组件的面板不包含任何其他组件，并且面板的列数设置为1。

1. 从“编 **辑** ”模式切 **换到** “定位”模式。 切换模式的选项位于右上角附近。
1. 选择一 **个品牌**，选择 **活动**，然后点按 **开始定位**。 “ **受众** ”菜单显示在编辑器的右侧。

   ![定位菜单](assets/targeting-menu.png)

1. 从“受众”菜单中选 **择受众** ，然后点按要定位的图像。 出现菜单。 在菜单中，点按 **目标**。 点按图像，然后点按 **配置**。 在“属性”窗口中，选择要为选定受众显示的图像。 为所有受众重复该步骤。 交互式通信或自适应表单中的图像启用了体验定位。

## 检查创建的活动是否与Target服务器同步 {#check-if-the-created-activity-syncs-with-the-target-server}

用于定位的活动与Target服务器同步。 要检查您的活动是否与目标服务器同步，请检查您的品牌页面中的活动状态。

确保活动的状态已同步。

## 验证Target行为 {#validate-target-behavior}

要验证Target行为，请执行以下操作：

* 在创作模 `wcmmode preview` 式中使用定位
* 在发布模式 `wcmmode preview` 下和 `wcmmode disabled` 在发布模式下使用定位

## 图像组件的监视定位 {#monitor-targeting-for-the-image-component}

要监视表单上图像组件的定位，请发布图像、活动和自适应表单。

## 未解决问题 {#open-issues}

可见性表达式，自适应表单上的目标图像设置焦点失败。
