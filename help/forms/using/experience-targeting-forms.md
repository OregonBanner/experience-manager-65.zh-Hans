---
title: 在AEM Forms创造有针对性的体验
seo-title: 在AEM Forms创造有针对性的体验
description: 使用AEM Forms的目标为目标客户创建自定义体验。
seo-description: 使用AEM Forms的目标为目标客户创建自定义体验。
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# 在AEM Forms创建目标体验{#create-targeted-experiences-in-aem-forms}

## 将Adobe Target与AEM Forms整合{#integrate-adobe-target-with-aem-forms}

Adobe Target与AEM集成，使您能够创建为目标受众定制的体验。 借助Adobe Target，您可以创建A/B测试、评估用户响应并为目标用户生成自定义Web内容。 您可以将Adobe Target与AEM Forms集成，以目标自适应表单和交互式通信的图像组件。

在AEM中配置Adobe Target以将其与自适应表单和交互式通信一起使用，请参阅[在AEM](/help/sites-administering/target.md)中创建目标配置和[添加框架](/help/sites-administering/target.md)。

>[!NOTE]
>
>当使用主机名或IP地址呈现您的自适应表单或交互式通信时，定位即有效。 当使用localhost呈现自适应表单或交互式通信时，该功能将失败。

## 创建目标活动{#creating-a-target-activity}

1. 点按&#x200B;**Adobe Experience Manager>个性化>活动**。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 在活动页面中，点按&#x200B;**创建>创建品牌**。
1. 系统会要求您选择模板并输入属性。

   选择模板，点按&#x200B;**下一步。** 在“属性”部分输入品牌标题，然后点按创 **建。**
您的品牌现在列在活动页面中。

1. 在活动页面中点击您的品牌。
1. 在品牌的主控区域中，点按&#x200B;**创建** > **创建活动**。

   创建活动时，需指定其详细信息、目标和设置。

   “详细信息”部分包括名称、定位引擎和目标。 选择Adobe Target作为定位引擎时，将启用目标云配置选项。 选择您的目标云配置，选择活动类型，提供活动的目标，然后点按&#x200B;**下一步**。 交互通信仅支持体验定位活动类型。

   目标部分允许您添加受众体验并命名它。 单击&#x200B;**添加体验**&#x200B;以启用&#x200B;**选择受众**&#x200B;和&#x200B;**名称体验**&#x200B;选项。 点按&#x200B;**选择受众**&#x200B;可查看受众及其源的列表。 从“受众名”列表中选择一个受众。 点按&#x200B;**添加体验**&#x200B;以命名体验，然后点按&#x200B;**下一步**。

   通过“目标和设置”部分，您可以计划活动并排定优先级。 设置开始日期、结束日期和活动的优先级、目标度量、附加度量，然后点按&#x200B;**保存**。

   活动现在列在您的品牌页面中。

   >[!NOTE]
   >
   >您可能会忽略错误“您的活动已保存，但它未同步到目标。 原因：“以下体验没有优惠”(如果在保存活动时遇到)。

1. 要启用目标，请编辑。jsp文件，以包含自适应表单模板使用的客户端库。

   例如，在现成的实现中，单击&#x200B;**工具** > **CRXDE Lite**。

   在CRXDE Lite地址栏中，键入/libs/fd/af/components/page/base/head.jsp以编辑head.jsp文件。

   此实现使用simpleEngroment模板。 在此实现中，修改head.jsp文件以包含以下客户端库：

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 要为自适应表单启用目标框架，请导航到表单或交互式通信，然后在编辑模式下打开它。

   要在编辑模式下打开表单或交互式通信，请点按&#x200B;**选择**，然后点按&#x200B;**打开**。

   或者，当您将指针移动到表单或交互式通信图标上时，不选择该图标就会显示四个按钮。 可以点按显示的&#x200B;**编辑**&#x200B;按钮，以在编辑模式下打开表单。

1. 在页面工具栏中，点按&#x200B;**页面信息** ![主题选项](assets/theme-options.png) > **打开属性**。
1. 在“常规”选项卡中，为&#x200B;**Adobe Target**&#x200B;字段选择配置。 点按&#x200B;**保存并关闭**。

## 将创建的活动应用于自适应表单图像或交互式通信图像{#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 打开自适应表单和交互式通信进行编辑。 如果要打开交互式通信，请打开Web渠道。

1. 在交互式通信或自适应表单的创作模式中，添加要定位的图像。

   >[!NOTE]
   >
   >AEM Forms仅支持将图像组件定位为目标。 确保承载图像组件的面板不包含任何其他组件，并且面板的列数设置为1。

1. 从&#x200B;**编辑**&#x200B;模式切换到&#x200B;**定位**&#x200B;模式。 切换模式的选项位于右上角附近。
1. 选择&#x200B;**BRAND**，选择&#x200B;**活动**，然后点按&#x200B;**开始定位**。 **受众**&#x200B;菜单显示在编辑器的右侧。

   ![定位菜单](assets/targeting-menu.png)

1. 从&#x200B;**受众**&#x200B;菜单中选择一个受众，然后点按图像以目标。 出现菜单。 在菜单中，点按&#x200B;**目标**。 点按图像，然后点按&#x200B;**配置**。 在“属性”窗口中，选择要为选定受众显示的图像。 对所有受众重复此步骤。 交互式通信或自适应表单中的图像启用了体验定位。

## 检查创建的活动是否与目标服务器{#check-if-the-created-activity-syncs-with-the-target-server}同步

用于定位的活动与目标服务器同步。 要检查您的活动是否与目标服务器同步，请检查您的品牌页面中活动的状态。

确保活动的状态已同步。

## 验证目标行为{#validate-target-behavior}

要验证目标行为，请执行以下操作：

* 在创作模式下对`wcmmode preview`使用定位
* 在发布模式下对`wcmmode preview`和`wcmmode disabled`使用定位

## 图像组件{#monitor-targeting-for-the-image-component}的监视器定位

要监视表单上图像组件的定位，请发布图像、活动和自适应表单。

## 未解决问题{#open-issues}

可见性表达式，自适应表单上目标图像的焦点设置失败。
