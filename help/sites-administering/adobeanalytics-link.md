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
translation-type: tm+mt
source-git-commit: 6f49e01aa3e9841c7b2917870593452b778667d2

---


# 为Adobe Analytics配置链接跟踪{#configuring-link-tracking-for-adobe-analytics}

当用户单击网站页面上的链接时，您可以在Adobe Analytics中捕获相关信息。 例如，使用链接跟踪了解用户如何与您的站点交互、跟踪文件下载和跟踪退出链接。

## 为Adobe Analytics Framework配置链接跟踪 {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. 使用 **Adobe****Analytics**，通过Deployment **,** Cloud Services **，转到** Adobe Analytics导航部分。

1. 使用 **显示配置**，打开所需的Adobe Analytics框架。
1. 展开“链 **接跟踪配置** ”部分，并根据需要进行配置（此页提供更多详细信息）:

   ![aa-08](assets/aa-08.png)

## 跟踪文件下载 {#tracking-file-downloads}

配置Adobe Analytics框架，以便从关联页面下载的文件在Adobe Analytics中作为下载自动跟踪。 启用下载跟踪后，将仅跟踪您指定的文件类型。

默认情况下，会跟踪以下文件类型的下载：

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

例如，在为PDF文件启用下载跟踪的情况下，每当用户单击指向PDF文件的链接时，都会跟踪PDF的下载。

框架的下载跟踪属性作为为页面生成的 `analytics.sitecatalyst.js` 文件中的代码实现。 以下代码示例表示默认的下载跟踪配置：

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

要为Adobe Analytics框架启用下载跟踪，请执行以下操作：

1. [打开Adobe Analytics框架并展开“链接跟踪配置”部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 启用 **跟踪下载**。
1. 在“下 **载文件类型** ”框中，键入要跟踪的文件类型的文件扩展名。

## 跟踪外部链接 {#tracking-external-links}

您可以跟踪页面上外部链接（退出链接）的单击情况。

要跟踪Adobe Analytics框架的外部链接，请执行以下操作：

1. [打开Adobe Analytics框架并展开“链接跟 **踪配置”部分**](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根据您的要求配置以下属性。

用于跟踪外部链接何时被单击的属性：

* **跟踪外部**&#x200B;启用外部链接跟踪。

* **外部过滤器**（可选）定义用于匹配链接目标的外部URL的过滤器。 当链接目标与筛选器匹配时，将跟踪链接。 外部过滤器仅用于跟踪页面上的某些外部链接。

   要指定要跟踪的外部链接，请键入链接目标的全部或部分URL。 用逗号分隔多个过滤器。 将字符串文本括在单引号中。 没有值(默认值为， `''`两个单引号)会导致跟踪所有外部链接。

* **内部过滤**&#x200B;器定义用于匹配内部链接URL的过滤器。 当链接的目标URL与此过滤器匹配时，不跟踪链接。 默认值是javascript命令，它返回当前窗口地址的URL的主机名。

   要指定未跟踪的内部链接，请键入链接目标的全部或部分内部URL。 用逗号分隔多个过滤器。 将字符串文本括在单引号中。

   默认值为 `'javascript:,'+window.location.hostname`

* **在评估与内部**&#x200B;和外部过滤器的匹配时，请保留“查询字符串包括URL”参数。

   启用此选项，可在根据外部和内部过滤器评估链接目标URL时包含URL参数。

外部链接跟踪属性作为为页面生成的 `analytics.sitecatalyst.js` 文件中的代码实现。 将为与框架关联的页面生成以下示例代码，该框架通过以下配置启用了外部链接跟踪：

* 外部过滤器为 `'google.com'`
* 内部过滤器是 `'javascript:,'+window.location.hostname`
* 根据筛选器评估链接目标时，不包括查询字符串。

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## 通过单击链接发送变量数据 {#sending-variable-data-with-link-clicks}

您可以配置AEM，以在用户单击链接时向Adobe Analytics发送事件和变量数据。 通过 **“链接跟踪配置** ”属性，可指定Adobe Analytics事件和变量，以跟踪链接单击的发生时间。

框架映射确定事件和变量值。 您可以将Adobe Analytics变量映射到内容组件的变量，这些变量存储您在单击链接时要跟踪的数据。

要通过单击链接发送变量数据，请执行以下操作：

1. [打开Adobe Analytics框架并展开“链接跟踪配置”部分](#configuring-link-tracking-for-an-adobe-analytics-framework)。
1. 根据您的要求配置以下属性。

用于通过单击链接发送变量数据的属性：

* **链接跟踪事**&#x200B;件输入要用于计数链接点击次数的Adobe Analytics事件变量。

   用逗号分隔多个变量名称。

   默认值不会 `None` 导致事件跟踪。

* **链接跟踪**&#x200B;变量输入您要在单击链接时发送到Adobe Analytics的Adobe Analytics变量。 用逗号分隔多个变量名称。

   默认值 `None` 不会发送变量数据。

指定要发送的事件和变量时，配置将作为为页面生成的 `analytics.sitecatalyst.js` 文件中的代码实现。 当框架跟踪事件和属性时，将为页面生成以 `event10` 下示例代 `prop4` 码：

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## 链接跟踪配置示例 {#example-link-tracking-configuration}

请执行以下步骤来了解Adobe Analytics集成的链接跟踪行为。 该过程显示 [Adobe Marketing Cloud调试器的结果](https://marketing.adobe.com/resources/help/en_US/sc/implement/debugger_install.html)。

### General configuration {#general-configuration}

此示例说明映射在跟踪和调试器上下文中的工作方式：

1. 打开已与网页关联的框架。
1. 将页 **面组件** 拖到框架的映射区域。 页 **面组件** ，属于Sidekick中的“ **常规** ”组件组。

   >[!NOTE]
   >
   >在真实场景中应使用的组件取决于继承自的组件（如果是）。
   >
   >如果不是，您应该在此处公开您自己的组件（通过在其页面组件中定义分析子节点）。

   通过从左侧面板拖动Analytics(SiteCatalyst)变量，根据下表配置映射：

<table>
 <tbody>
  <tr>
   <th>CQ Variable<br /> </th>
   <th>变量浏览器中的条目<br /> </th>
   <th>Adobe Analytics变量</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>自定义eVar 1(eVar1)</td>
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
   <th>CQ Variable<br /> </th>
   <th>变量浏览器中的条目</th>
   <th>Adobe Analytics变量</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>自定义eVar 2(eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>自定义eVar 3(eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>自定义2(event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### 配置外部链接跟踪 {#configure-external-link-tracking}

1. 在您的框架中，展开“链 **接跟踪配置** ”区域。
1. 取消选 **择“跟踪下载**”。

1. 选择 **跟踪外部**。
1. 取消选 **择“保留查询字符串**”。
1. 对“外部过滤器”列 **表使用以下值** ，将其标识为外部URL:

   `‘yahoo.com’`

1. 在“链接跟踪事件”字 **段中添加以下值** :

   ```
       event1,event2
   ```

1. 将以下值添加到“链 **接跟踪变量** ”字段：

   ```
       eVar1,eVar2
   ```

1. 在与框架关联的页面上，添加一个 **Text** 组件。 在“文 **本** ”组件中，添加指向以下地址的超链接：

   `https://search.yahoo.com/?p=this`

1. 切换到“ **预览”模式** ，然后单击链接。

使用Adobe Marketing cloud调试程序查看时，发出的调用将如下：

![aa-leavequerysearch-blank](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>URL不包含查询字符串： `?p=this`

### 包括URL参数 {#include-the-url-parameter}

1. 在框架中，展开“链 **接跟踪配置** ”区域。
1. 启用 **保留查询字符串**。
1. 重新加载页面预览，然后单击链接。

Adobe Marketing cloud调试器中显示的调用详细信息与以下示例类似：

![aa-leavequerysearch-active](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>此时，URL确实包含查询字符串： `?p=this`

## Ad-Hoc Link Tracking {#ad-hoc-link-tracking}

点对点链接跟踪允许内容作者为组件配置链接跟踪。 组件的配置将覆盖框架的 **链接跟踪配置** ，因此，在与框架关联的页面上，可以配置 **** Text组件以跟踪URL的链接。

临时链接跟踪使您能够跟踪下载链接、外部链接以及事件和变量数据。

要启用点对点链接跟踪，您需要：

* [将包含文本组件的页 **面与框** 架相关联](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。
* [配置Adobe Analytics框架以启用点对点链接跟踪](#enabling-ad-hoc-link-tracking)。
* [为文本组件配置链接跟踪](#configuring-link-tracking-for-a-text-component)。

### 启用点对点链接跟踪 {#enabling-ad-hoc-link-tracking}

配置Adobe Analytics框架以启用点对点链接跟踪。

1. 打开Adobe Analytics框架并展开“链接跟 **踪配置”部分** 。

1. 启 **用点对点链接跟踪**。

   >[!NOTE]
   >
   >并非所有用户类型都有权访问此复选框。 如果需要访问，请与站点管理员联系。

>[!NOTE]
>
>XSS Antisamy配置现在位于路径/libs/sling/xss.config.xml **下的SLING中** ，需要添加以下规则才能进行临时链接：

#### 锚标记规则扩展 {#anchor-tag-rule-extension}

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

### 为文本组件配置链接跟踪 {#configuring-link-tracking-for-a-text-component}

在为 **Text** 组件本身配置点对点链接跟踪之前，必须已实施以下配置：

* Adobe [Analytics框架配置为启用点对点链接跟踪](#enabling-ad-hoc-link-tracking)。
* 包 [含Text组件的页 **面与框架相关联**](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework)。

请按照以下过程为文本组件配置链 **接跟** 踪：

1. 在编辑模式下打开页面并编辑文 **本组** 件。

1. 选择要用作超文本的文本，然后单击“超链接”按钮。

   ![](do-not-localize/chlimage_1.png)

1. 在“链接到”框中添加目标URL，然后展开“链接跟踪”区域。

   >[!NOTE]
   >
   >自定义链接跟踪可以作为单独的操作显示，位于链接／取消链接操作（分析图标）旁边。
   >
   >只有在RTE中选择了有效的链接后，才会启用该链接。

   ![aa-17](assets/aa-17.png)

1. 启用 **自定义链接跟踪** ，以覆盖Adobe Analytics框架的链接跟踪配置，并启用当前链接的链接跟踪。

1. （可选）要通过链接单击跟踪事件，请在“包括Adobe Analytics变量”字段中添 **加Adobe Analytics事件名称** 。 用逗号分隔多个事件名称，例如

   `event1, event22`.

1. （可选）要通过链接单击跟踪变量数据，请在“包括Adobe Analytics变量”字 **段中添加Adobe Analytics变量** 。 使用以下任一格式：

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`‘CONSTANT'`*
   以下示例说明了每种格式：

   * `eVar10:pagedata.title`
   * `prop1: ‘Aubergine'`
   用逗号分隔多个值。

1. 选择 **确定**。

