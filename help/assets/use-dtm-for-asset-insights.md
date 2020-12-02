---
title: 通过DTM实现资产洞察
description: 了解如何使用Adobe动态标签管理(DTM)启用资产分析。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# 通过DTM{#enable-asset-insights-through-dtm}启用资产分析

Adobe动态标签管理是一种激活数字营销工具的工具。 酒店免费提供给Adobe Analytics客户。 您可以自定义跟踪代码，使第三方CMS解决方案能够使用资产分析，也可以使用DTM插入资产分析标记。 只支持并提供图像洞察。

>[!CAUTION]
>
>AdobeDTM已弃用，但支持[!DNL Adobe Experience Platform Launch]，很快将达到[寿命结束](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)。 Adobe建议您[使用 [!DNL Launch] 获得资产洞察](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)。

执行这些步骤，通过DTM启用资产分析。

1. 单击Experience Manager标志，然后转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 洞察配置]**。
1. [使用DTMExperience Manager配置Cloud Service](/help/sites-administering/dtm.md)

   登录[https://dtm.adobe.com](https://dtm.adobe.com/)并访问用户用户档案中的&#x200B;**[!UICONTROL 帐户设置]**&#x200B;后，API令牌应可用。 从资产分析的角度来看，不需要执行此步骤，因为Experience Manager站点与资产分析的集成仍在进行中。

1. 登录[https://dtm.adobe.com](https://dtm.adobe.com/)，然后根据需要选择公司。
1. 创建或打开现有Web属性

   * 选择&#x200B;**[!UICONTROL Web属性]**&#x200B;选项卡，然后单击&#x200B;**[!UICONTROL 添加属性]**。

   * 根据需要更新字段，然后单击&#x200B;**[!UICONTROL 创建属性]**。 请参阅[文档](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)。

   ![创建编辑Web属性](assets/Create-edit-web-property.png)

1. 在&#x200B;**[!UICONTROL 规则]**&#x200B;选项卡中，从导航窗格中选择&#x200B;**[!UICONTROL 页面加载规则]**，然后单击&#x200B;**[!UICONTROL 创建新规则]**。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 展开&#x200B;**[!UICONTROL JavaScript /Third Party Tags]**。 然后，在&#x200B;**[!UICONTROL 顺序HTML]**&#x200B;选项卡中单击&#x200B;**[!UICONTROL 添加新脚本]**&#x200B;以打开“脚本”对话框。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. 单击Experience Manager标志，然后转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。
1. 单击&#x200B;**[!UICONTROL 洞察页面跟踪器]**，复制跟踪器代码，然后将其粘贴到您在步骤6中打开的“脚本”对话框中。 保存更改。

   >[!NOTE]
   >
   >* `AppMeasurement.js` 。它预计可通过DTM的Adobe Analytics工具获得。
   >* 将删除对`assetAnalytics.dispatcher.init()`的调用。 一旦DTM的Adobe Analytics工具完成加载，该函数将被调用。
   >* 根据资产分析页面跟踪器的托管位置(例如Experience Manager、CDN等)，脚本源的来源可能需要更改。
   >* 对于托管Experience Manager的页面跟踪器，源应使用调度程序实例的主机名指向发布实例。


1. 访问 `https://dtm.adobe.com`. 单击web属性中的&#x200B;**[!UICONTROL 概述]**，然后单击&#x200B;**[!UICONTROL 添加工具]**&#x200B;或打开现有的Adobe Analytics工具。 创建工具时，可将&#x200B;**[!UICONTROL 配置方法]**&#x200B;设置为&#x200B;**[!UICONTROL 自动]**。

   ![添加Adobe Analytics工具](assets/Add-Adobe-Analytics-Tool.png)

   根据需要选择暂存／生产报表包。

1. 展开&#x200B;**[!UICONTROL 库管理]**，并确保将&#x200B;**[!UICONTROL 在]**&#x200B;加载库设置为&#x200B;**[!UICONTROL 页顶部]**。

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 展开&#x200B;**[!UICONTROL 自定义页面代码]**，然后单击&#x200B;**[!UICONTROL 打开编辑器]**。

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 在窗口中粘贴以下代码：

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * DTM中的页面加载规则只包含`pagetracker.js`代码。 任何`assetAnalytics`字段都被视为默认值的覆盖。 默认情况下，它们不是必需的。
   * 确保`_satellite.getToolsByType('sc')[0].getS()`已初始化且`assetAnalytics,dispatcher.init`可用后，代码调用`assetAnalytics.dispatcher.init()`。 因此，您可以跳过在步骤11中添加它。
   * 如分析页面跟踪器代码（**[!UICONTROL 工具>资产>洞察页面跟踪器]**）中的注释所示，当页面跟踪器未创建`AppMeasurement`对象时，前三个参数(RSID、跟踪服务器和访客命名空间)将不起作用。 而是传递空字符串以突出显示它。\
      其余参数与“分析配置”页（**[!UICONTROL 工具>资产>分析配置]**）中配置的参数相对应。
   * 通过查询`satelliteLib`所有可用的SiteCatalyst引擎来检索AppMeasurement对象。 如果配置了多个标记，请相应地更改数组选择器的索引。 阵列中的条目按DTM界面中可用的SiteCatalyst工具进行排序。

1. 保存并关闭“代码编辑器”窗口，然后在“工具”配置中保存更改。
1. 在&#x200B;**[!UICONTROL 批准]**&#x200B;选项卡中，批准两个待批准。 DTM标记已准备好插入网页。 有关如何在网页中插入DTM标记的详细信息，请参阅[在自定义页面模板中集成DTM](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)。
