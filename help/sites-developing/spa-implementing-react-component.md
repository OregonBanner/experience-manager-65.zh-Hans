---
title: 为SPA实施React组件
seo-title: 为SPA实施React组件
description: 本文举了一个示例，说明如何调整简单的现有React组件以与AEM SPA Editor一起使用。
seo-description: 本文举了一个示例，说明如何调整简单的现有React组件以与AEM SPA Editor一起使用。
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579

---


# 为SPA实施React组件{#implementing-a-react-component-for-spa}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，作者希望在AEM内为使用SPA框架构建的站点无缝编辑内容。

SPA创作功能优惠了用于在AEM中支持SPA的全面解决方案。 本文举了一个示例，说明如何调整简单的现有React组件以与AEM SPA Editor一起使用。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## 简介 {#introduction}

由于AEM需要在SPA和SPA编辑器之间签订简单而轻量的合同，采用现有的Javascript应用程序并将其改编为与AEM中的SPA一起使用非常简单。

本文说明了We.Retail日志示例SPA上天气组件的示例。

在阅读本文之前， [您应熟悉AEM的SPA应用程](/help/sites-developing/spa-getting-started-react.md) 序的结构。

>[!CAUTION]
>此文档仅将 [We.Retail日志应用程序用](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应利 [用AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，该原型支持使用React或Angular的SPA项目并利用SPA SDK。

## 天气组件 {#the-weather-component}

天气组件位于We.Retail日志应用程序的左上角。 它显示已定义位置的当前天气，动态获取天气数据。

### 使用天气构件 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在SPA编辑器中创作SPA内容时，天气组件将显示为任何其他AEM组件，并带有工具栏，并且可编辑。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

可以像任何其他AEM组件一样在对话框中更新城市。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

更改将被保留，并且组件会使用新的天气数据自动更新自己。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 气象组件实施 {#weather-component-implementation}

天气组件实际上基于一个公开的React组件，称 [为React Open Weather](https://www.npmjs.com/package/react-open-weather)，该组件已经过调整，可作为We.Retail日志范例SPA应用程序中的组件使用。

以下是NPM文档中使用React Open Weather组件的片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png)![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

在We.Retail日志应用程序中查 `Weather.js`看自定义天气组件()的代码：

* **第16行**: React Open Weather构件会根据需要加载。
* **第46行**: 该函 `MapTo` 数将此React组件与相应的AEM组件关联，以便在SPA编辑器中编辑它。

* **第22-29行**: 定 `EditConfig` 义城市，检查城市是否已填充，如果为空，则定义值。

* **第31-44行**: Weather组件扩展了类 `Component` 并提供React Open Weather组件的NPM使用文档中定义的所需数据，并渲染该组件。

```
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
import {MapTo} from '@adobe/cq-react-editable-components';

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

尽管后端组件必须已存在，但前端开发人员只需很少的编码即可在We.Retail日志SPA中利用React Open Weather组件。

## 下一步 {#next-step}

有关为AEM开发SPA的更多信息，请参阅为AEM [开发SPA一文](/help/sites-developing/spa-architecture.md)。
