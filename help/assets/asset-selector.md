---
title: 资产选择器
description: 了解如何使用资产选择器搜索、筛选、浏览和获取Adobe Experience Manager Assets中资产的元数据。 另外，了解如何自定义资产选择器界面。
contentOwner: AG
feature: Asset Management,Metadata,Search
role: User
exl-id: 4b518ac0-5b8b-4d61-ac31-269aa1f5abe4
source-git-commit: 4139b42d5cd3d7d1d93863dc07cfafd58c3f64f2
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 资产选择器 {#asset-selector}

>[!NOTE]
>
>调用了资产选择器 [资产选取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 在以前的版本中 [!DNL Experience Manager].

资产选择器允许您浏览、搜索和筛选 [!DNL Adobe Experience Manager] 资产。 您还可以使用资产选择器获取您选择的资产的元数据。 要自定义资产选择器界面，您可以使用支持的请求参数启动该界面。 这些参数用于为特定方案设置资产选择器的上下文。

目前，您可以传递请求参数 `assettype` (*图像/视频/文本*)和选择 `mode` (*单个/多个*)作为资产选择器的上下文信息，在整个选择过程中，该信息将保持不变。

资产选择器使用HTML5 **Window.postMessage** 消息，以将选定资产的数据发送给收件人。

资产选择器基于Granite的基础选取器词汇。 默认情况下，资产选择器在浏览模式下运行。 但是，您可以使用Omnisearch体验应用过滤器，以优化对特定资产的搜索。

您可以将任何网页（无论它是否是CQ容器的一部分）与资产选择器(`https://[AEM_server]:[port]/aem/assetpicker.html`)。

## 上下文参数 {#contextual-parameters}

您可以在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 作为URL中资源后缀的文件夹路径：`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 要启动资产选择器并选择特定文件夹，例如文件夹 `/content/dam/we-retail/en/activities` ，则URL应为以下形式： `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | 如果在启动资产选择器时需要选择特定文件夹，则会将其作为资源后缀传递。 |
| 模式 | 单个，多个 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 在多个模式下，您可以使用资产选择器同时选择多个资产。 |
| 对话框 | true，false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 使用这些参数以Granite对话框的形式打开资产选择器。 仅当您通过Granite路径字段启动资产选择器，并将其配置为pickerSrc URL时，此选项才适用。 |
| 根 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 使用此选项可为资产选择器指定根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接/间接）。 |
| 视图模式 | 搜索 |  | 要在搜索模式下启动资产选择器，请使用assettype和mimetype参数。 |
| assettype(S) | 图像、文档、多媒体、存档 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 使用此选项可根据传递的值筛选资产类型。 |
| mimetype | mimetype(s)(`/jcr:content/metadata/dc:format`)（也支持通配符） | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | 使用它可以根据MIME类型筛选资产 |

## 使用资产选择器 {#using-the-asset-selector}

1. 要访问资产选择器界面，请转到 `https://[AEM_server]:[port]/aem/assetpicker`.
1. 导航到所需的文件夹，然后选择一个或多个资产。

   ![chlimage_1-441](assets/chlimage_1-441.png)

   或者，您也可以从OmniSearch框中搜索所需的资产，然后将其选中。

   ![chlimage_1-442](assets/chlimage_1-442.png)

   如果您使用OmniSearch框搜索资产，则可以从 **[!UICONTROL 过滤器]** 窗格来优化搜索。

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 点按/单击 **[!UICONTROL 选择]** 中。
