---
title: 为 SPA 实施 React 组件
seo-title: Implementing a React Component for SPA
description: 本文介紹如何改寫簡單的現有React元件以與AEM SPA編輯器搭配使用的範例。
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: afd2afe182d65e64c0ad851b86021886078a9dd5
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 11%

---

# 为 SPA 实施 React 组件{#implementing-a-react-component-for-spa}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。開發人員希望能夠使用SPA架構建立網站，而作者則希望能夠順暢地編輯使用SPA架構建立之網站的AEM內容。

SPA製作功能提供全方位的解決方案，可支援AEM中的SPA。 本文介紹如何改寫簡單的現有React元件以與AEM SPA編輯器搭配使用的範例。

>[!NOTE]
>
>SPA編輯器是建議解決方案，適用於需要SPA架構使用者端轉譯的專案(例如React或Angular)。

## 简介 {#introduction}

有了AEM所需的簡單且輕量型的合約，以及SPA與SPA編輯器之間的建立合約，直接了當要採用現有的Javascript應用程式，並將其調整為與AEM中的SPA搭配使用時，就很簡單了。

本文說明We.Retail Journal範例SPA上的天氣元件範例。

您應熟悉 [適用於AEM的SPA應用程式結構](/help/sites-developing/spa-getting-started-react.md) 閱讀本文之前。

>[!CAUTION]
>本檔案使用 [We.Retail日誌應用程式](https://github.com/adobe/aem-sample-we-retail-journal) 僅供展示之用。 不应将它用于任何项目工作。
>
>任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 天氣元件 {#the-weather-component}

氣象元件可在We.Retail Journal應用程式的左上角找到。 它會顯示定義位置的目前氣象，以動態方式提取天氣資料。

### 使用天氣Widget {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

在SPA編輯器中編寫SPA的內容時，天氣元件會以任何其他AEM元件的形式出現、使用工具列完成並可編輯。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

城市可在對話方塊中更新，就像任何其他AEM元件一樣。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

此變更會持續存在，而元件會自動以新天氣資料更新。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 天氣元件實作 {#weather-component-implementation}

天氣元件實際上是根據公開可用的React元件，稱為 [React Open Weather](https://www.npmjs.com/package/react-open-weather)，此元件已改編為We.Retail Journal範例SPA應用程式中的元件。

以下是使用React Open Weather元件的NPM檔案片段。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

檢閱自訂天氣元件的程式碼( `Weather.js`)在We.Retail日誌應用程式中：

* **第16行**：React Open Weather Widget會視需要載入。
* **第46行**：此 `MapTo` 函式將此React元件與對應的AEM元件建立關聯，以便在SPA編輯器中編輯它。

* **第22-29行**：此 `EditConfig` 會定義，檢查是否已填入城市，如果為空，則會定義值。

* **第31-44行**：天氣元件會延伸 `Component` 類別，並根據NPM使用檔案中的定義，為React Open Weather元件提供必要資料，以及呈現元件。

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

雖然後端元件必須已存在，但前端開發人員可以在We.Retail Journal SPA中善用React Open Weather元件，且只需很少的程式碼。

## 后续步骤 {#next-step}

如需針對AEM開發SPA的詳細資訊，請參閱文章 [針對AEM開發SPA](/help/sites-developing/spa-architecture.md).
