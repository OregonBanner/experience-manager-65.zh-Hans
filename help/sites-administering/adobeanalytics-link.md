---
title: 为Adobe Analytics配置链接跟踪
seo-title: 为Adobe Analytics配置链接跟踪
description: 了解如何为SiteCatalyst配置链接跟踪。
seo-description: 了解如何为SiteCatalyst配置链接跟踪。
uuid: b6d5bd1c-f91a-4d38-9e9e-dc2bcb271dae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fe6ba6af-f500-4c0d-b984-fb617d4bf48a
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# 为Adobe Analytics配置链接跟踪{#configuring-link-tracking-for-adobe-analytics}

当用户单击网站页面上的链接时，您可以在Adobe Analytics中捕获相关信息。 例如，使用链接跟踪可了解用户如何与您的网站交互、跟踪文件下载和跟踪退出链接。

## 为Adobe Analytics框架{#configuring-link-tracking-for-an-adobe-analytics-framework}配置链接跟踪

1. 使用&#x200B;**Navigation**，通过&#x200B;**Deployment**、**Cloud Services**&#x200B;到&#x200B;**Adobe Analytics**&#x200B;部分。

1. 使用&#x200B;**显示配置**，打开所需的Adobe Analytics框架。
1. 展开&#x200B;**链接跟踪配置**&#x200B;部分并根据需要进行配置（本页提供了更多详细信息）：

   ![aa-08](assets/aa-08.png)

## 跟踪文件下载{#tracking-file-downloads}

配置Adobe Analytics框架，以便从关联页面下载的文件在Adobe Analytics中作为下载自动进行跟踪。 启用下载跟踪后，将只跟踪您指定的文件类型。

默认情况下会跟踪以下文件类型的下载：

* exe
* zip
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

因此，例如，在为PDF文件启用下载跟踪的情况下，每当用户单击指向PDF文件的链接时，都会跟踪PDF的下载。

框架的下载跟踪属性将作为代码实施在为页面生成的`analytics.sitecatalyst.js`文件中。 以下代码示例表示默认的下载跟踪配置：

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

要为Adobe Analytics框架启用下载跟踪，请执行以下操作：

1. [打开Adobe Analytics框架并展开链接跟踪配置部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 启用&#x200B;**跟踪下载**。
1. 在&#x200B;**下载文件类型**&#x200B;框中，键入要跟踪的文件类型的文件扩展名。

## 跟踪外部链接{#tracking-external-links}

您可以跟踪页面上外部链接（退出链接）的单击情况。

要跟踪Adobe Analytics框架的外部链接，请执行以下操作：

1. [打开Adobe Analytics框架并展开链接 **跟踪配** 置部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根据您的要求配置以下资产。

单击外部链接时用于跟踪的属性：

* **跟踪**
外部链接跟踪。

* **外部过滤器**
（可选）定义用于匹配链接目标的外部URL的过滤器。当链接目标与过滤器匹配时，将跟踪该链接。 外部过滤器可用于仅跟踪页面上的某些外部链接。

   要指定要跟踪的外部链接，请键入链接目标URL的全部或部分。 用逗号分隔多个过滤器。 在单引号内引住字符串文字。 没有值（默认值`''`，两个单引号）会导致跟踪所有外部链接。

* **内部**
过滤器定义用于匹配内部链接URL的过滤器。当链接定位与此过滤器匹配的URL时，不会跟踪该链接。 默认值是javascript命令，可返回当前窗口地址的URL的主机名。

   要指定未跟踪的内部链接，请键入链接目标内部URL的全部或部分内容。 用逗号分隔多个过滤器。 在单引号内引住字符串文字。

   默认值为 `'javascript:,'+window.location.hostname`

* **在评估与内**
部和外部过滤器的匹配项时，请保留查询字符串包含URL参数。

   在根据外部和内部过滤器评估链接目标URL时，允许包含URL参数。

外部链接跟踪属性作为代码实施在为页面生成的`analytics.sitecatalyst.js`文件中。 为与已使用以下配置启用外部链接跟踪的框架关联的页面生成以下示例代码：

* 外部筛选器为`'google.com'`
* 内部筛选器是`'javascript:,'+window.location.hostname`的默认值
* 根据过滤器评估链接目标时，不包含查询字符串。

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## 通过链接点击发送变量数据{#sending-variable-data-with-link-clicks}

您可以将AEM配置为在用户单击链接时将事件和变量数据发送到Adobe Analytics。 通过&#x200B;**链接跟踪配置**&#x200B;属性，您可以指定在发生链接点击时要跟踪的Adobe Analytics事件和变量。

框架映射确定事件和变量值。 您可以将Adobe Analytics变量映射到内容组件的变量，这些变量存储您在单击链接时要跟踪的数据。

要通过链接点击发送变量数据，请执行以下操作：

1. [打开Adobe Analytics框架并展开链接跟踪配置部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根据您的要求配置以下资产。

用于通过链接点击发送变量数据的属性：

* **链接跟**
踪事件输入要用于计数链接点击量的Adobe Analytics事件变量。

   用逗号分隔多个变量名称。

   默认值`None`不会导致事件跟踪。

* **链接跟**
踪变量输入单击链接时要发送到Adobe Analytics的Adobe Analytics变量。用逗号分隔多个变量名称。

   默认值`None`不会发送任何变量数据。

指定要发送的事件和变量时，该配置将作为代码实施在为页面生成的`analytics.sitecatalyst.js`文件中。 框架跟踪`event10`事件和`prop4`属性时，将为页面生成以下示例代码：

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## 链接跟踪配置示例{#example-link-tracking-configuration}

请执行以下步骤来探索Adobe Analytics集成的链接跟踪行为。 此过程显示[Adobe Marketing Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)的结果。

### 常规配置{#general-configuration}

此示例说明映射在跟踪和调试器上下文中的工作方式：

1. 打开与网页关联的框架。
1. 将&#x200B;**Page**&#x200B;组件拖动到框架的映射区域。 **Page**&#x200B;组件属于Sidekick中的&#x200B;**General**&#x200B;组件组。

   >[!NOTE]
   >
   >在现实场景中，您应使用的组件取决于从继承的组件（如果有）。
   >
   >如果不是，则应在此处显示您自己的组件（通过在其页面组件中定义分析子节点）。

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
   <td>自定义1(event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. 将搜索组件拖动到框架的映射区域。 搜索组件属于Sidekick中的常规组件组。 通过从左侧面板拖动Analytics(SiteCatalyst)变量，根据下表配置映射：

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
   <td>自定义2(event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### 配置外部链接跟踪{#configure-external-link-tracking}

1. 在框架中，展开&#x200B;**链接跟踪配置**&#x200B;区域。
1. 取消选择&#x200B;**跟踪下载**。

1. 选择&#x200B;**跟踪外部**。
1. 取消选择&#x200B;**保留查询字符串**。
1. 为&#x200B;**External Filters**&#x200B;列表使用以下值将其标识为外部URL:

   `‘yahoo.com’`

1. 将以下值添加到&#x200B;**链接跟踪事件**&#x200B;字段：

   ```
       event1,event2
   ```

1. 将以下值添加到&#x200B;**链接跟踪变量**&#x200B;字段：

   ```
       eVar1,eVar2
   ```

1. 在与框架关联的页面上，添加&#x200B;**Text**&#x200B;组件。 在&#x200B;**Text**&#x200B;组件内，添加指向以下地址的超链接：

   `https://search.yahoo.com/?p=this`

1. 切换到&#x200B;**预览模式**&#x200B;并单击链接。

使用Adobe Marketing Cloud Debugger查看时，所发出的调用将如下所示：

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>URL不包含查询字符串：`?p=this`

### 包含URL参数{#include-the-url-parameter}

1. 在框架中，展开&#x200B;**链接跟踪配置**&#x200B;区域。
1. 启用&#x200B;**保留查询字符串**。
1. 重新加载页面预览，然后单击链接。

Adobe Marketing Cloud Debugger中显示的调用详细信息与以下示例类似：

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>此时，URL包含查询字符串：`?p=this`

## 临时链接跟踪{#ad-hoc-link-tracking}

临时链接跟踪允许内容作者为组件配置链接跟踪。 组件的配置将覆盖框架的&#x200B;**链接跟踪配置**，因此在与框架关联的页面上，可以配置&#x200B;**Text**&#x200B;组件以跟踪URL的链接。

通过临时链接跟踪，您可以跟踪下载链接、外部链接以及事件和变量数据。

要启用临时链接跟踪，您需要：

* [将包含Textcomponent的页 **** 面与框架关联](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。
* [配置Adobe Analytics框架以启用临时链接跟踪](#enabling-ad-hoc-link-tracking)。
* [为文本组件配置链接跟踪](#configuring-link-tracking-for-a-text-component)。

### 启用Ad-hoc Link跟踪{#enabling-ad-hoc-link-tracking}

配置Adobe Analytics框架以启用临时链接跟踪。

1. 打开Adobe Analytics框架并展开&#x200B;**链接跟踪配置**&#x200B;部分。

1. 启用&#x200B;**Ad-hoc Link跟踪**。

   >[!NOTE]
   >
   >并非所有用户类型都有权访问此复选框。 如果您需要访问，请联系您的站点管理员。

>[!NOTE]
>
>XSS Antisamy配置现在位于路径&#x200B;**/libs/sling/xss.config.xml**&#x200B;下的SLING中，需要将以下规则添加到，临时链接才能正常工作：

#### 锚点标记规则扩展{#anchor-tag-rule-extension}

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

在为&#x200B;**Text**&#x200B;组件本身配置临时链接跟踪之前，必须已实施以下配置：

* [Adobe Analytics框架配置为启用临时链接跟踪](#enabling-ad-hoc-link-tracking)。
* 包含&#x200B;**Text**&#x200B;组件的[页面与框架](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)关联。

请按照以下过程为&#x200B;**Text**&#x200B;组件配置链接跟踪：

1. 在编辑模式下打开页面，并编辑&#x200B;**Text**&#x200B;组件。

1. 选择要用作超文本的文本，然后单击“超链接”按钮。

   ![](do-not-localize/chlimage_1.png)

1. 在链接到框中添加目标URL，然后展开链接跟踪区域。

   >[!NOTE]
   >
   >自定义链接跟踪作为单独的操作显示在链接/取消链接操作（Analytics图标）旁边。
   >
   >只有在RTE中选择了有效链接后，才会启用该链接。

   ![aa-17](assets/aa-17.png)

1. 启用&#x200B;**自定义链接跟踪**&#x200B;以覆盖Adobe Analytics框架的链接跟踪配置并启用当前链接的链接跟踪。

1. （可选）要通过链接点击跟踪事件，请在&#x200B;**Include Adobe Analytics Variables**&#x200B;字段中添加Adobe Analytics事件名称。 使用逗号分隔多个事件名称，例如

   `event1, event22`。

1. （可选）要通过链接点击跟踪变量数据，请在&#x200B;**包含Adobe Analytics变量**&#x200B;字段中添加Adobe Analytics变量。 使用以下任一格式：

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*:  *`‘CONSTANT'`*

   以下示例说明了每种格式：

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`

   用逗号分隔多个值。

1. 选择&#x200B;**确定**。
