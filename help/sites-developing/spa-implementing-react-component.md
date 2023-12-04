---
title: 为 SPA 实施 React 组件
description: 本文介绍了如何调整简单的现有React组件以用于Adobe Experience Manager (AEM) SPA编辑器的示例。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# 为 SPA 实施 React 组件{#implementing-a-react-component-for-spa}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而创作者则希望能够在Adobe Experience Manager (AEM)中为使用SPA框架构建的站点无缝编辑内容。

SPA创作功能提供了一个全面的解决方案，用于在AEM中支持SPA。 本文介绍了如何调整简单的现有React组件以用于AEM SPA编辑器的示例。

>[!NOTE]
>
>SPA编辑器是推荐的解决方案，适用于需要基于SPA框架的客户端渲染(例如React或Angular)的项目。

## 简介 {#introduction}

由于AEM需要并在SPA和SPA编辑器之间建立的简单且轻量的合同，采用现有JavaScript应用程序并将其调整为用于AEM中的SPA是一件简单的事情。

本文说明了We.Retail Journal示例SPA上的天气组件示例。

您应该熟悉 [适用于AEM的SPA应用程序的结构](/help/sites-developing/spa-getting-started-react.md) ，然后再阅读本文。

>[!CAUTION]
>本文档使用 [We.Retail日志应用程序](https://github.com/adobe/aem-sample-we-retail-journal) 仅供演示之用。 请勿将其用于任何项目工作。
>
>任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 天气组件 {#the-weather-component}

天气组件在We.Retail Journal应用程序的左上角找到。 它显示定义位置的当前天气，动态提取天气数据。

### 使用天气小组件 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在SPA编辑器中创作SPA的内容时，天气组件显示为任何其他AEM组件，在工具栏中完成，并且可以编辑。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

城市可以在对话框中更新，就像任何其他AEM组件一样。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

更改将持续存在，并且组件会自动使用新天气数据更新自身。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 天气组件实施 {#weather-component-implementation}

天气组件基于公开可用的React组件，称为 [React Open Weather](https://www.npmjs.com/package/react-open-weather). 它已调整为在We.Retail Journal示例SPA应用程序中用作组件。

以下是React Open Weather组件用法的NPM文档片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

查看自定义天气组件的代码( `Weather.js`)在We.Retail日志应用程序中：

* **16号线**：根据需要加载React Open Weather构件。
* **46号线**：和 `MapTo` 函数将此React组件与相应的AEM组件相关联，以便在SPA编辑器中编辑它。

* **第22-29行**：和 `EditConfig` 定义，检查是否已填充城市，如果为空，则定义值。

* **第31-44行**：天气组件扩展 `Component` 类，并按照React Open Weather组件的NPM使用文档中的定义提供所需数据并呈现该组件。

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

虽然后端组件必须已存在，但前端开发人员可以使用We.Retail Journal SPA中的React Open Weather组件，并且只需很少的编码。

## 后续步骤 {#next-step}

有关为AEM开发SPA的更多信息，请参阅文章 [开发SPA for AEM](/help/sites-developing/spa-architecture.md).
