---
title: 通过DTM启用资产分析
description: 了解如何使用AdobeDynamic Tag Management (DTM)来启用资产分析。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# 通过DTM启用资产分析 {#enable-asset-insights-through-dtm}

AdobeDynamic Tag Management是一款可激活您的数字营销工具的工具。 Adobe Analytics客户可以免费使用。 您可以自定义跟踪代码以启用第三方CMS解决方案来使用资产分析，也可以使用DTM插入资产分析标记。 仅支持图像并提供见解。

>[!CAUTION]
>
>AdobeDTM已弃用，取而代之 [!DNL Adobe Experience Platform] 并且很快就能达到 [生命周期结束](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe建议您 [使用 [!DNL Adobe Experience Platform] 用于资产分析](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

执行这些步骤可通过DTM启用资产分析。

1. 单击Experience Manager徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 分析配置]**.
1. [使用DTMCloud Service配置Experience Manager部署](/help/sites-administering/dtm.md)

   API令牌应在您登录之后可用 [https://dtm.adobe.com](https://dtm.adobe.com/) 和访问 **[!UICONTROL 帐户设置]** 在用户配置文件中。 从Assets Insights的角度来看，此步骤不是必需的，因为Experience Manager Sites与Assets Insights的集成仍在进行中。

1. 登录 [https://dtm.adobe.com](https://dtm.adobe.com/)，并根据需要选择公司。
1. 创建或打开现有Web属性

   * 选择 **[!UICONTROL Web属性]** 选项卡，然后单击 **[!UICONTROL 添加属性]**.

   * 更新相应的字段，然后单击 **[!UICONTROL 创建属性]**. 请参阅 [文档](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans).

   ![创建编辑Web属性](assets/Create-edit-web-property.png)

1. 在 **[!UICONTROL 规则]** 选项卡，选择 **[!UICONTROL 页面加载规则]** 从导航窗格中单击 **[!UICONTROL 创建新规则]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 展开 **[!UICONTROL JavaScript /第三方标记]**. 然后单击 **[!UICONTROL 添加新脚本]** 在 **[!UICONTROL 顺序HTML]** 选项卡，打开脚本对话框。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. 单击Experience Manager徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]**.
1. 单击 **[!UICONTROL 分析页面跟踪器]**，复制跟踪器代码，然后将其粘贴到在第6步中打开的脚本对话框中。 保存更改。

   >[!NOTE]
   >
   >* `AppMeasurement.js` 将被删除。 它应通过DTM的Adobe Analytics工具提供。
   >* 对的调用 `assetAnalytics.dispatcher.init()` 将被删除。 DTM的Adobe Analytics工具完成加载后，预计会调用函数。
   >* 根据托管资产分析页面跟踪器的位置(例如，Experience Manager、CDN等)，可能需要更改脚本源的来源。
   >* 对于Experience Manager托管的页面跟踪器，源应使用调度程序实例的主机名指向发布实例。

1. 访问 `https://dtm.adobe.com`. 单击 **[!UICONTROL 概述]** 在Web属性中，然后单击 **[!UICONTROL 添加工具]** 或打开现有的Adobe Analytics工具。 在创建工具时，可以设置 **[!UICONTROL 配置方法]** 到 **[!UICONTROL 自动]**.

   ![添加Adobe Analytics工具](assets/Add-Adobe-Analytics-Tool.png)

   根据需要选择暂存/生产报表包。

1. 展开 **[!UICONTROL 库管理]**，并确保 **[!UICONTROL 库加载位置]** 设置为 **[!UICONTROL 页面顶部]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 展开 **[!UICONTROL 自定义页面代码]**，然后单击 **[!UICONTROL 打开编辑器]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 将以下代码粘贴到窗口中：

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
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

   * DTM中的页面加载规则仅包括 `pagetracker.js` 代码。 任何 `assetAnalytics` 字段被视为默认值的覆盖。 默认情况下，它们不是必需的。
   * 代码调用 `assetAnalytics.dispatcher.init()` 在确保 `_satellite.getToolsByType('sc')[0].getS()` 已初始化，并且 `assetAnalytics,dispatcher.init` 可用。 因此，可跳过在步骤11中添加缩览图。
   * 如分析页面跟踪器代码(**[!UICONTROL 工具>资产>分析页面跟踪器]**)，页面跟踪器不会创建 `AppMeasurement` 对象、前三个参数（RSID、跟踪服务器和访客命名空间）无关。 而是传递空字符串以突出显示此内容。\
     其余参数对应于“分析配置”页面中配置的参数(**[!UICONTROL 工具>资产>分析配置]**)。
   * 通过查询检索AppMeasurement对象 `satelliteLib` 所有可用的SiteCatalyst引擎的日志。 如果配置了多个标记，请相应地更改阵列选择器的索引。 数组中的条目按照DTM界面中提供的SiteCatalyst工具进行排序。

1. 保存并关闭代码编辑器窗口，然后在工具配置中保存更改。
1. 在 **[!UICONTROL 审批]** 选项卡，批准两个待处理批准。 DTM标记已准备好插入到您的网页中。
