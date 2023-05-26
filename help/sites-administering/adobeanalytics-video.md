---
title: 为 Adobe Analytics 配置视频跟踪
seo-title: Configuring Video Tracking for Adobe Analytics
description: 了解如何为SiteCatalyst配置视频跟踪。
seo-description: Learn about configuring video tracking for SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# 为 Adobe Analytics 配置视频跟踪{#configuring-video-tracking-for-adobe-analytics}

有多种方法可用于跟踪视频事件，其中2种是旧版Adobe Analytics的旧版选项。 这些旧版选项为：旧版里程碑和旧版秒数。

>[!NOTE]
>
>在继续之前，请确保您拥有 **可播放视频** 已在AEM中上传。
>
>要确保视频在页面上播放，请参阅 **[本教程](/help/sites-authoring/default-components-foundation.md#video)** 有关如何在AEM中转码视频文件的信息。

使用以下过程设置框架，以便使用每种方法跟踪视频。

>[!NOTE]
>
>对于新的实施，建议您 **不使用** 用于视频跟踪的旧版选项。 请使用 **里程碑** 方法。

## 常见步骤 {#common-steps}

1. 通过拖动来设置网页 **视频组件** 添加一个可玩的 **视频作为资产** 对于组件

1. [创建Adobe Analytics配置和框架](/help/sites-administering/adobeanalytics.md).

   * 以下部分中的示例使用名称 **my-sc-configuration** （对于配置和） **videofw** 用于框架。

1. 在framework页上，选择RSID并将用法设置为all。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 从Sidekick中的“常规”组件类别中，将视频组件拖动到框架上。
1. 选择跟踪方法：

   * [里程碑](/help/sites-administering/adobeanalytics.md)
   * [非传统里程碑](/help/sites-administering/adobeanalytics.md)
   * [旧版里程碑](/help/sites-administering/adobeanalytics.md)
   * [旧版秒数](/help/sites-administering/adobeanalytics.md)

1. 当您选择跟踪方法时，CQ变量的列表会相应更改。 有关如何进一步配置组件以及如何将CQ变量映射到Adobe Analytics属性的信息，请参阅以下部分。

## 里程碑 {#milestones}

Milestones方法可跟踪有关视频的大多数信息，高度可自定义，并且易于配置。

要使用“里程碑”方法，请指定基于时间的跟踪偏移以定义里程碑。 当视频播放超过里程碑时，页面调用Adobe Analytics以跟踪事件。 对于您定义的每个里程碑，组件会创建一个CQ变量，您可以将该变量映射到Adobe Analytics资产。 这些CQ变量的名称使用以下格式：

```shell
eventdata.events.milestoneXX
```

XX后缀是定义里程碑的轨道偏移。 例如，指定4、8、16、20和28秒的跟踪偏移会生成以下CQ变量：

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

下表介绍了为Milestones方法提供的默认CQ变量：

<table>
 <tbody>
  <tr>
   <th>CQ变量</th>
   <th>Adobe Analytics资产</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>映射到此的变量将包含 <strong>用户友好</strong> 名称(<strong>标题</strong>)；如果未设置，则视频的 <strong>文件名</strong> 将改为发送。 仅在播放视频开始时发送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此的变量将包含文件名。 仅与eventdata.events.a.media.view一起发送 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此的变量将包含文件在服务器上的路径。 仅与eventdata.events.a.media.view一起发送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>每次超过区段里程碑时发送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>每次触发里程碑时都会发送，用户观看给定区段所花费的秒数也会与此事件一起发送。 例如eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>在初始化视频视图时发送</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>视频播放完时发送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>当超过给定的里程碑时发送，X代表里程碑触发的秒数<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>在每个里程碑时发送；在Adobe Analytics调用中显示为pev3，通常以“视频”形式发送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>与eventdata.videoName完全匹配 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>包含有关已查看区段的信息，例如2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以设置视频的 **用户友好** ，方法是打开视频在DAM中进行编辑，然后设置 **标题** 将元数据字段更改为所需的名称。

1. 选择里程碑作为跟踪方法后，在跟踪偏移框中，输入以逗号分隔的跟踪偏移列表（以秒为单位）。 例如，以下值定义在视频开始后的4、8、16、20和28秒处的里程碑：

   ```xml
   4,8,16,20,24
   ```

   偏移值必须是大于0的整数。 默认值为 `10,25,50,75`。

1. 要将CQ变量映射到Adobe Analytics属性，请将Adobe Analytics属性从ContentFinder拖动到组件上的CQ变量旁边。

   有关优化映射的信息，请参见 [在Adobe Analytics中测量视频](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 指南。

1. [添加框架](/help/sites-administering/adobeanalytics.md) 到页面。
1. 在中测试设置 **预览模式**，播放视频以触发Adobe Analytics调用。

以下的Adobe Analytics跟踪数据示例适用于使用4、8、16、20和24的跟踪偏移以及CQ变量的以下映射的里程碑跟踪：

<table>
 <tbody>
  <tr>
   <th>CQ 变量</th>
   <th>Adobe Analytics资产</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1， prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

对于此示例，视频组件在框架页面上如下所示：

![video1](assets/video1.png)

>[!NOTE]
>
>要查看对Adobe Analytics的调用，请使用适当的工具，如DigitalPulse Debugger或Fiddler。

使用DigitalPulse Debugger查看时，使用提供的示例对Adobe Analytics的调用应如下所示：

![chlimage_1-128](assets/chlimage_1-128.png)

*这是&#x200B;**第一次调用**对Adobe Analytics的更改，包含以下值：*

* *eventdata.a.media.name的prop1和eVar1，*
* *props2-4，以及包含contentType（视频）和区段(1)的eVar2和eVar3:O:1-4)*
* *已映射到eventdata.events.a.media.view的event3。*

![chlimage_1-129](assets/chlimage_1-129.png)

*这是&#x200B;**第三个调用**向Adobe Analytics发出：*

* *prop1和eVar1包含a.media.name；*
* *event1，因为已查看区段*
* *event2发送时已播放时间= 4*
* *event11已发送，因为已达到eventdata.events.milestone8*
* *prop2到4未发送（因为未触发eventdata.events.a.media.view）*

## 非传统里程碑 {#non-legacy-milestones}

除了使用轨道长度的百分比定义里程碑之外，非传统里程碑方法与里程碑方法类似。 共同之处如下：

* 当视频播放超过里程碑时，页面调用Adobe Analytics以跟踪事件。
* 此 [CQ变量的静态集](#cqvars) 为使用Adobe Analytics属性映射而定义的属性。
* 对于您定义的每个里程碑，组件会创建一个CQ变量，您可以将该变量映射到Adobe Analytics资产。

这些CQ变量的名称使用以下格式：

XX后缀是定义里程碑的轨道长度的百分比。 例如，指定百分比10、25、50和75会生成以下CQ变量：

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 选择“非传统里程碑”作为跟踪方法后，在“跟踪偏移”框中，输入以逗号分隔的跟踪长度百分比列表。 例如，以下默认值将里程碑定义为轨道长度的10%、25%、50%和75%：

   ```xml
   10,25,50,75
   ```

   偏移值必须是大于0的整数。

1. 要将CQ变量映射到Adobe Analytics属性，请将Adobe Analytics属性从ContentFinder拖动到组件上的CQ变量旁边。

   有关优化映射的信息，请参见 [在Adobe Analytics中测量视频](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 指南。

1. [添加框架](/help/sites-administering/adobeanalytics.md) 到页面。
1. 在中测试设置 **预览模式**，播放视频以触发Adobe Analytics调用。

## 旧版里程碑 {#legacy-milestones}

此方法类似于里程碑方法，不同之处在于 *跟踪偏移* 字段是视频中的百分比，而不是设置点。

>[!NOTE]
>
>“跟踪偏移”字段仅接受一个逗号分隔的列表，该列表包含1到100之间的整数。

1. 设置“跟踪”偏移。

   * e.g.10,50,75,100

   此外，发送到Adobe Analytics的信息的可自定义性较低；只有3个变量可用于映射：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoname <br /> </td>
   <td>映射到此的变量将包含 <strong>用户友好</strong> 名称(<strong>标题</strong>)；如果未设置标题，则视频的 <strong>文件名</strong> 将改为发送。 仅在播放视频开始时发送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此的变量将包含文件名。 仅在播放视频开始时发送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此的变量将包含文件在服务器上的路径。 仅在播放视频开始时发送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以设置视频的 **用户友好** ，方法是打开视频在DAM中进行编辑，然后设置 **标题** 将元数据字段更改为所需的名称。 您还需要保存完成时所做的更改。

1. 将这些变量映射到prop 1至3

   此 **其他相关信息** 在中，调用将被连接发送到 **一** 命名的变量 **pev3**.

   **示例调用** 使用DigitalPulse Debugger查看时，使用提供的示例访问Adobe Analytics应如下所示：

   ![lmilestones1](assets/lmilestones1.png)

   *此&#x200B;**pev3**调用中发送的变量包含以下信息：*

   * *名称*  — 视频文件的名称(*film.avi*)

   * *长度*  — 视频文件的长度，以秒为单位(*100*)

   * *播放器名称*  — 用于播放视频文件的视频播放器(*HTML5视频*)

   * *已播放的总秒数*  — 播放视频的总秒数(*25*)

   * *开始时间戳*  — 标识视频播放开始时间的时间戳(*1331035567*)

   * *播放会话*  — 播放会话的详细信息。 此字段指示用户如何与视频交互。 这可能包括数据，例如他们开始播放视频的位置、他们是否使用视频滑块来推进视频，以及他们停止播放视频的位置(*L10E24S58L58 — 视频在秒处停止。 L10节的25节，然后跳过到秒。 48*)

## 旧版秒数 {#legacy-seconds}

使用**旧版秒**方法时，每隔N秒触发一次Adobe Analytics调用，其中N在“跟踪偏移”字段中指定。

1. 将“跟踪偏移”设置为任意秒数，

   * 例如6
   >[!NOTE]
   >
   >“跟踪偏移”字段仅接受大于0的整数

   发送到Adobe Analytics的信息不太可自定义。 只有3个变量可用于映射：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoname <br /> </td>
   <td>映射到此的变量将包含 <strong>用户友好</strong> 名称(<strong>标题</strong>)；如果未设置标题，则视频的 <strong>文件名</strong> 将改为发送。 仅在播放视频开始时发送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此的变量将包含文件名。 仅在播放视频开始时发送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到此的变量将包含文件在服务器上的路径。 仅在播放视频开始时发送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以设置视频的 **用户友好** ，方法是打开视频在DAM中进行编辑，然后设置 **标题** 将元数据字段更改为所需的名称。 您还需要保存完成时所做的更改。

1. 将这些变量映射到prop1、prop2和prop3

   此 **其他相关信息** 中的将连接发送到 **一** 命名的变量 **pev3**.

   使用DigitalPulse Debugger查看时，使用提供的示例对Adobe Analytics的调用应如下所示：

   ![lseconds](assets/lseconds.png)

   *此调用类似于上面的旧版里程碑调用。 请查看pev3的信息&#x200B;**[此处提供](/help/sites-administering/adobeanalytics.md)**.*

**本教程中使用的引用：**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
