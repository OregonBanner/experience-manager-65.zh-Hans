---
title: 为 SPA 实施 React 组件
seo-title: 为 SPA 实施 React 组件
description: 本文提供了一个示例，说明如何调整现有的简单React组件以与AEM SPA Editor一起使用。
seo-description: 本文提供了一个示例，说明如何调整现有的简单React组件以与AEM SPA Editor一起使用。
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 7%

---

# 为 SPA 实施 React 组件{#implementing-a-react-component-for-spa}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者则希望在AEM中无缝编辑使用SPA框架构建的站点的内容。

SPA创作功能提供了一个全面的解决方案，可在AEM中支持SPA。 本文提供了一个示例，说明如何调整现有的简单React组件以与AEM SPA Editor一起使用。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## 简介 {#introduction}

由于AEM要求在SPA和SPA编辑器之间签订简单而轻量的合同，因此获取现有的Javascript应用程序并对其进行改编以用于AEM中的SPA非常简单。

本文说明了We.Retail Journal示例SPA上天气组件的示例。

在阅读本文之前，您应该熟悉AEM](/help/sites-developing/spa-getting-started-react.md)的SPA应用程序的[结构。

>[!CAUTION]
>本文档仅将[We.Retail Journal应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)用于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应使用[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

## 天气组件{#the-weather-component}

天气组件位于We.Retail Journal应用程序的左上角。 它显示定义位置的当前天气，并动态提取天气数据。

### 使用天气小组件{#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在SPA编辑器中创作SPA内容时，天气组件会显示为任何其他AEM组件（带有工具栏且可编辑）。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

与任何其他AEM组件一样，可以在对话框中更新城市。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

将保留更改，并且组件会使用新天气数据自动更新自身。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 天气组件实施{#weather-component-implementation}

天气组件实际上基于一个公开提供的React组件，称为[React Open Weather](https://www.npmjs.com/package/react-open-weather)，该组件已经过修改，可用作We.Retail Journal示例SPA应用程序中的组件。

以下是NPM文档中关于React Open Weather组件用法的片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

查看We.Retail Journal应用程序中自定义天气组件(`Weather.js`)的代码：

* **第16行**:根据需要加载React Open Weather小组件。
* **第46行**:该函 `MapTo` 数将此React组件与相应的AEM组件相关联，以便在SPA编辑器中对其进行编辑。

* **第22-29行**:定 `EditConfig` 义，检查城市是否已填充，如果为空，则定义值。

* **第31-44行**:天气组件对类进行扩 `Component` 展，并提供React Open Weather组件的NPM使用文档中定义的所需数据，并渲染组件。

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

尽管后端组件必须已存在，但前端开发人员可以利用We.Retail Journal SPA中的React Open Weather组件，而且只需极少的编码。

## 下一步 {#next-step}

有关开发AEM SPA的更多信息，请参阅文章[开发AEM for SPA](/help/sites-developing/spa-architecture.md)。
