---
title: 为Adobe Analytics配置链接跟踪
seo-title: 为Adobe Analytics配置链接跟踪
description: 了解如何配置链接跟踪以进行SiteCatalyst。
seo-description: 了解如何配置链接跟踪以进行SiteCatalyst。
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---


# 为Adobe Analytics配置链接跟踪{#configuring-link-tracking-for-adobe-analytics}

当用户单击您网站页面上的链接时，您可以在Adobe Analytics捕获相关信息。 例如，使用链接跟踪来了解用户如何与您的站点交互、跟踪文件下载和跟踪退出链接。

## 为Adobe Analytics框架{#configuring-link-tracking-for-an-adobe-analytics-framework}配置链接跟踪

1. 使用&#x200B;**导航**，通过&#x200B;**部署**、**Cloud Services**&#x200B;到&#x200B;**Adobe Analytics**&#x200B;部分。

1. 使用&#x200B;**显示配置**&#x200B;打开所需的Adobe Analytics框架。
1. 展开&#x200B;**链接跟踪配置**&#x200B;部分并根据需要进行配置（本页提供更多详细信息）:

   ![aa-08](assets/aa-08.png)

## 跟踪文件下载{#tracking-file-downloads}

配置Adobe Analytics框架，以便从关联页面下载的文件作为下载在Adobe Analytics自动跟踪。 启用下载跟踪时，只会跟踪您指定的文件类型。

默认情况下，跟踪以下文件类型的下载：

* exe
* zip
* 瓦夫
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

例如，在为PDF文件启用下载跟踪的情况下，每当用户单击指向PDF文件的链接时，都会跟踪PDF的下载。

框架的下载跟踪属性作为为页面生成的`analytics.sitecatalyst.js`文件中的代码实现。 以下代码示例表示默认下载跟踪配置：

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

要为您的Adobe Analytics框架启用下载跟踪，请执行以下操作：

1. [打开Adobe Analytics框架并展开“链接跟踪配置”部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 启用&#x200B;**跟踪下载**。
1. 在&#x200B;**下载文件类型**&#x200B;框中，键入要跟踪的文件类型的文件扩展名。

## 跟踪外部链接{#tracking-external-links}

您可以跟踪页面上外部链接（退出链接）的单击情况。

要跟踪Adobe Analytics框架的外部链接：

1. [打开Adobe Analytics框架并展开“链 **接跟踪配** 置”部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根据您的要求配置以下属性。

用于跟踪何时单击外部链接的属性：

* **跟踪外**
部启用外部链接跟踪。

* **外部过滤器**
（可选）定义用于匹配链接目标的外部URL的过滤器。当链接目标与筛选器匹配时，将跟踪链接。 外部过滤器仅用于跟踪页面上的某些外部链接。

   要指定要跟踪的外部链接，请键入链接目标的全部或部分URL。 用逗号分隔多个过滤器。 将字符串文本括在单引号中。 没有值（默认值`''`，两个单引号）会导致跟踪所有外部链接。

* **内部**
过滤器定义用于匹配内部链接URL的过滤器。当链接目标与此筛选器匹配的URL时，不跟踪链接。 默认值为javascript命令，它返回当前窗口地址的URL的主机名。

   要指定未跟踪的内部链接，请键入链接目标的全部或部分内部URL。 用逗号分隔多个过滤器。 将字符串文本括在单引号中。

   默认值为 `'javascript:,'+window.location.hostname`

* **评估与内**
部和外部查询的匹配时，请保留过滤器字符串包括URL参数。

   启用此选项，可在根据外部和内部目标评估链接过滤器URL时包含URL参数。

外部链接跟踪属性作为为页面生成的`analytics.sitecatalyst.js`文件中的代码实现。 为与已使用以下配置启用外部链接跟踪的框架关联的页面生成以下示例代码：

* 外部过滤器为`'google.com'`
* 内部筛选器是`'javascript:,'+window.location.hostname`的默认值
* 查询字符串在评估链接目标时不包括过滤器。

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## 通过单击链接发送变量数据{#sending-variable-data-with-link-clicks}

您可以配置AEM以在用户单击链接时向Adobe Analytics发送事件和变量数据。 使用&#x200B;**链接跟踪配置**&#x200B;属性，可以指定在发生链接单击时要跟踪的Adobe Analytics事件和变量。

框架映射确定事件和变量值。 您可以将Adobe Analytics变量映射到内容组件的变量，这些变量存储您在单击链接时要跟踪的数据。

要通过单击链接发送变量数据，请执行以下操作：

1. [打开Adobe Analytics框架并展开“链接跟踪配置”部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根据您的要求配置以下属性。

通过链接点击发送变量数据的属性：

* **链接跟**
踪事件输入要用于计算链接点击次数的Adobe Analytics事件变量。

   用逗号分隔多个变量名称。

   默认值`None`导致无事件跟踪。

* **链接跟**
踪变量输入单击链接时要发送到Adobe Analytics的Adobe Analytics变量。用逗号分隔多个变量名称。

   默认值`None`导致不发送变量数据。

指定要发送的事件和变量时，配置将作为为页面生成的`analytics.sitecatalyst.js`文件中的代码实现。 当框架跟踪`event10`事件和`prop4`属性时，将为页面生成以下示例代码：

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## 链接跟踪配置示例{#example-link-tracking-configuration}

请执行以下过程来了解Adobe Analytics集成的链接跟踪行为。 过程显示来自[Adobe Marketing Cloud调试器](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)的结果。

### 常规配置{#general-configuration}

此示例说明映射在跟踪和调试器上下文中的工作方式：

1. 打开已与网页关联的框架。
1. 将&#x200B;**Page**&#x200B;组件拖动到框架的映射区域。 **Page**&#x200B;组件属于Sidekick中的&#x200B;**General**&#x200B;组件组。

   >[!NOTE]
   >
   >在实际场景中应使用的组件取决于从中继承的组件（如果有）。
   >
   >如果不是，您应将您自己的组件公开在那里（通过在其页面组件中定义分析子节点）。

   通过从左侧面板拖动Analytics(SiteCatalyst)变量，根据下表配置映射：

<table>
 <tbody>
  <tr>
   <th>CQ变量<br /> </th>
   <th>变量浏览器中的条目<br /> </th>
   <th>Adobe Analytics变量</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>自定义eVar1(eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>自定义1(事件1)</td>
   <td>事件1</td>
  </tr>
 </tbody>
</table>

1. 将“搜索”组件拖到框架的映射区域。 搜索组件属于Sidekick中的常规组件组。 通过从左侧面板拖动Analytics(SiteCatalyst)变量，根据下表配置映射：

<table>
 <tbody>
  <tr>
   <th>CQ变量<br /> </th>
   <th>变量浏览器中的条目</th>
   <th>Adobe Analytics变量</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>自定义eVar2(eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>自定义eVar3(eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>自定义2(事件2)</td>
   <td>事件2</td>
  </tr>
 </tbody>
</table>

### 配置外部链路跟踪{#configure-external-link-tracking}

1. 在框架中，展开&#x200B;**链接跟踪配置**&#x200B;区域。
1. 取消选择&#x200B;**跟踪下载**。

1. 选择&#x200B;**跟踪外部**。
1. 取消选择&#x200B;**保留查询字符串**。
1. 对&#x200B;**外部过滤器**&#x200B;列表使用以下值将其标识为外部URL:

   `‘yahoo.com’`

1. 在&#x200B;**链接跟踪事件**&#x200B;字段中添加以下值：

   ```
       event1,event2
   ```

1. 在&#x200B;**链接跟踪变量**&#x200B;字段中添加以下值：

   ```
       eVar1,eVar2
   ```

1. 在与框架关联的页面上，添加&#x200B;**Text**&#x200B;组件。 在&#x200B;**Text**&#x200B;组件中，添加指向以下地址的超链接：

   `https://search.yahoo.com/?p=this`

1. 切换到&#x200B;**预览模式**&#x200B;并单击链接。

通过Adobe Marketing Cloud调试程序查看时，所发出的调用将如下所示：

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>URL不包含查询字符串：`?p=this`

### 包含URL参数{#include-the-url-parameter}

1. 在框架中，展开&#x200B;**链接跟踪配置**&#x200B;区域。
1. 启用&#x200B;**保留查询字符串**。
1. 重新加载页面预览，然后单击链接。

在Adobe Marketing Cloud调试器中显示的调用详细信息与以下示例类似：

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>此时，URL确实包含查询字符串：`?p=this`

## 点对点链路跟踪{#ad-hoc-link-tracking}

点对点链接跟踪允许内容作者为组件配置链接跟踪。 组件的配置将覆盖框架的&#x200B;**链接跟踪配置**，因此，在与框架关联的页面上，可以配置&#x200B;**文本**&#x200B;组件以跟踪URL。

临时链接跟踪使您能够跟踪下载链接、外部链接以及事件和变量数据。

要启用点对点链接跟踪，您需要：

* [将包含Text组件的页 **** 面与框架关联](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。
* [配置Adobe Analytics框架以启用点对点链接跟踪](#enabling-ad-hoc-link-tracking)。
* [为文本组件配置链接跟踪](#configuring-link-tracking-for-a-text-component)。

### 启用点对点链路跟踪{#enabling-ad-hoc-link-tracking}

配置您的Adobe Analytics框架以启用点对点链接跟踪。

1. 打开Adobe Analytics框架并展开&#x200B;**链接跟踪配置**&#x200B;部分。

1. 启用&#x200B;**点对点链接跟踪**。

   >[!NOTE]
   >
   >并非所有用户类型都有权使用此复选框。 如果您需要访问，请与站点管理员联系。

>[!NOTE]
>
>XSS Antisamy配置现在位于路径&#x200B;**/libs/sling/xss.config.xml**&#x200B;下的SLING中，需要添加以下规则才能进行点对点链接：

#### 锚标记规则扩展{#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### 为文本组件{#configuring-link-tracking-for-a-text-component}配置链接跟踪

在为&#x200B;**Text**&#x200B;组件本身配置点对点链路跟踪之前，必须已实现以下配置：

* [Adobe Analytics框架配置为启用点对点链路跟踪](#enabling-ad-hoc-link-tracking)。
* 包含&#x200B;**Text**&#x200B;组件的[页与框架](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)相关联。

请按照以下过程为&#x200B;**Text**&#x200B;组件配置链接跟踪：

1. 在编辑模式下打开页面并编辑&#x200B;**Text**&#x200B;组件。

1. 选择要用作超文本的文本，然后单击“超链接”按钮。

   ![](do-not-localize/chlimage_1.png)

1. 在“链接到”框中添加目标URL，然后展开“链接跟踪”区域。

   >[!NOTE]
   >
   >自定义链接跟踪可以作为单独的操作显示，在链接／取消链接操作（分析图标）旁边。
   >
   >只有在RTE中选择了有效的链接后，才会启用该链接。

   ![aa-17](assets/aa-17.png)

1. 启用&#x200B;**自定义链接跟踪**&#x200B;以覆盖Adobe Analytics框架的链接跟踪配置，并启用当前链接的链接跟踪。

1. （可选）要通过单击链接跟踪事件，请在&#x200B;**包括Adobe Analytics变量**&#x200B;字段中添加Adobe Analytics事件名称。 用逗号分隔多个事件名，例如

   `event1, event22`。

1. （可选）要通过单击链接跟踪变量数据，请在&#x200B;**包含Adobe Analytics变量**&#x200B;字段中添加Adobe Analytics变量。 使用以下格式之一：

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*:  *`‘CONSTANT'`*

   以下示例说明了每种格式：

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   用逗号分隔多个值。

1. 选择&#x200B;**确定**。

